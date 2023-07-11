# Application Containerization and Microservice Orchestration

## Stage Setup

Let’s get started by first cloning the demo code repository, changing the working directory, and checking the ```demo``` branch out.

![1](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/fc7f16f7-8ba2-4ba0-b603-b21a4cf589a0)

## Step 0: Basic Link Extractor Script

Checkout the ```step0``` branch and list files in it.

![2](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/badfc877-5457-4cf6-9141-00b3b447073e)

The ```linkextractor.py``` file is the interesting one here, so let’s look at its contents:

![3](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/eae29cf3-f467-42cf-8150-9e3ae4499e43)

However, this seemingly simple script might not be the easiest one to run on a machine that does not meet its requirements. The ```README.md``` file suggests how to run it, so let’s give it a try:

![4](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/aab3ac6c-0e02-4afd-be0c-e732d5d64834)

When we tried to execute it as a script, we got the ```Permission denied``` error. Let’s check the current permissions on this file:

![5](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/34a492ac-fd16-42be-af49-17107fe97941)

This current permission ```-rw-r--r--``` indicates that the script is not set to be executable. We can either change it by running ```chmod a+x linkextractor.py``` or run it as a Python program instead of a self-executing script as illustrated below:

![6](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f7c078ca-9dd0-4a0d-ad4b-34f501677490)

## Step 1: Containerized Link Extractor Script

Checkout the ```step1``` branch and list files in it.

![7](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/4b3befe7-53f1-416b-b213-7b9ca783d5c1)

We have added one new file (i.e., ```Dockerfile```) in this step. Let’s look into its contents:

![8](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/d00f2fdd-be1d-4023-a153-28df1c7ce5ea)

Using this ```Dockerfile``` we can prepare a Docker image for this script. We start from the official ```python``` Docker image that contains Python’s run-time environment as well as necessary tools to install Python packages and dependencies. We then add some metadata as labels (this step is not essential, but is a good practice nonetheless). Next two instructions run the ```pip install``` command to install the two third-party packages needed for the script to function properly. We then create a working directory ```/app```, copy the ```linkextractor.py``` file in it, and change its permissions to make it an executable script. Finally, we set the script as the entrypoint for the image.

So far, we have just described how we want our Docker image to be like, but didn’t really build one. So let’s do just that:

![9](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/20fb31a5-486e-4823-ba81-f397293fa40f)

We have created a Docker image named ```linkextractor:step1``` based on the ```Dockerfile``` illustrated above. If the build was successful, we should be able to see it in the list of image:

![10](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f9211b2c-9b36-44b8-a5f5-8f7a6cb3def3)

This image should have all the necessary ingredients packaged in it to run the script anywhere on a machine that supports Docker. Now, let’s run a one-off container with this image and extract links from some live web pages:

![11](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/68d7332a-f735-4029-9f40-b321acad1494)

Let’s try it on a web page with more links in it:

![12](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/74940896-f75a-49c9-888c-138eadbfd871)

## Step 2: Link Extractor Module with Full URI and Anchor Text

Checkout the ```step2``` branch and list files in it.

![13](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/de570d90-f417-44a8-9e04-831b6c1e4f96)

Let’s have a look at the updated script:

![14](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c1a8f200-2d0b-474b-9545-61d80cf3dac9)

Now, let’s build a new image and see these changes in effect:

![15](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/6a2351b2-26e3-41f9-b5da-0e06a8b947d3)

We have used a new tag ```linkextractor:step2``` for this image so that we don’t overwrite the image from the ```step1``` to illustrate that they can co-exist and containers can be run using either of these images.

![16](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/7944e141-fe40-47aa-9846-74e7aa3097d5)

Running a one-off container using the ```linkextractor:step2``` image should now yield an improved output:

![17](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/25ee69b4-3958-45e2-a96e-4066d880488a)

Running a container using the previous image ```linkextractor:step1``` should still result in the old output:

![18](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/855d4c02-61cb-48be-9441-cc4c08186c08)

## Step 3: Link Extractor API Service

Checkout the step3 branch and list files in it.

![19](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f1516e5e-7da4-4a76-9f10-ec7e2396c4bb)

Let’s first look at the ```Dockerfile``` for changes:

![20](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/b9ab653c-9555-4d20-b900-b4e819f4933d)

The ```linkextractor.py``` module remains unchanged in this step, so let’s look into the newly added ```main.py``` file:

![21](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/352c0c1d-6ede-4238-8fb7-dca42983e755)

It’s time to build a new image with these changes in place:

![22](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/4e6471bc-6fea-402e-9e47-1583f0e3898f)

Then run the container in detached mode (```-d``` flag) so that the terminal is available for other commands while the container is still running. Note that we are mapping the port ```5000``` of the container with the ```5000``` of the host (using ```-p 5000:5000``` argument) to make it accessible from the host. We are also assigning a name (```--name=linkextractor```) to the container to make it easier to see logs and kill or remove the container.

![23](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/59d660ac-37cf-4e09-97bd-4a6391392fb1)

If things go well, we should be able to see the container being listed in Up condition:

![24](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/e7843370-a017-4ca1-91f0-fdfc4c62391c)

We can now make an HTTP request in the form ```/api/<url>``` to talk to this server and fetch the response containing extracted links:

![25](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f80f039e-6463-43a4-9c19-d4b4aaa326fb)

Since the container is running in detached mode, so we can’t see what’s happening inside, but we can see logs using the name ```linkextractor``` we assigned to our container:

![26](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/b9d0c7e7-dff6-4898-b70a-d5a0d2809d8c)

We can see the messages logged when the server came up, and an entry of the request log when we ran the curl command. Now we can kill and remove this container:

![27](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/260659ed-c71d-4f10-98ed-27e364ed9110)

In this step we have successfully ran an API service listening on port ```5000```. This is great, but APIs and JSON responses are for machines, so in the next step we will run a web service with a human-friendly web interface in addition to this API service.

## Step 4: Link Extractor API and Web Front End Services

Checkout the ```step4``` branch and list files in it.

![28](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/e4e9a864-68f4-4362-9a20-3a853331875e)

In this step we are planning to run two separate containers, one for the API and the other for the web interface. The latter needs a way to talk to the API server. For the two containers to be able to talk to each other, we can either map their ports on the host machine and use that for request routing or we can place the containers in a single private network and access directly. Docker has excellent support for networking and provides helpful commands for dealing with networks. Additionally, in a Docker network containers identify themselves using their names as hostnames to avoid hunting for their IP addresses in the private network. However, we are not going to do any of this manually, instead we will be using Docker Compose to automate many of these tasks.

So let’s look at the ```docker-compose.yml``` file we have:

![29](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/ab27f216-596e-46a5-99ae-c3e7d953a190)

Now, let’s have a look at the user-facing ```www/index.php``` file:

![31](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/e6ce2b49-a747-4a29-a852-5b0518524517)

Let’s bring these services up in detached mode using ```docker-compose``` utility:

![32](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/48413f3b-e63e-4d6f-9b42-b798ad2d214d)

This output shows that Docker Compose automatically created a network named ```linkextractor_default```, pulled ```php:7-apache``` image from DockerHub, built ```api:python``` image using our local ```Dockerfile```, and finally, spun two containers ```linkextractor_web_1``` and ```linkextractor_api_1``` that correspond to the two services we have defined in the YAML file above.

Checking for the list of running containers confirms that the two services are indeed running:

![33](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/b2c68e71-ce25-4d46-a2b5-e0abf0159819)

We should now be able to talk to the API service as before:

![34](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/470071a8-3f8d-489a-afb4-20f80fa61b11)

To access the web interface click to open the Link Extractor. Then fill the form with https://training.play-with-docker.com/ (or any HTML page URL of your choice) and submit to extract links from it.

![35](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/296a5926-0ab7-4d95-90f7-12174d70494d)

Now, let’s modify the ```www/index.php``` file to replace all occurrences of ```Link Extractor``` with ```Super Link Extractor```:

![37](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/df93ef07-3765-4182-9e0f-608a37111904)

Reloading the web interface of the application (or clicking here) should now reflect this change in the title, header, and footer

![36](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/1848a02b-a696-4838-b4e4-c85c0a0479c8)

Let’s revert these changes now to clean the Git tracking:

![39](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/aec508ec-00fd-4787-bd37-85df44c84457)

Before we move on to the next step we need to shut these services down, but Docker Compose can help us take care of it very easily:

![40](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/357aa0f6-589c-40db-8e06-6c3807a3efec)

In the next step we will add one more service to our stack and will build a self-contained custom image for our web interface service.

## Step 5: Redis Service for Caching

Checkout the ```step5``` branch and list files in it.

![41](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/2d55a37d-2076-4bc1-b60b-e0d07a46d571)

Let’s first inspect the newly added ```Dockerfile``` under the ```./www folder```:

![42](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/e07905f3-80d4-43cc-b41d-df6a54b7e87b)

Next, we will look at the API server’s ```api/main.py``` file where we are utilizing the Redis cache:

![44](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/fd01c592-a228-4b97-a5cf-52a2ac0686f3)

Now, let’s look into the updated ```docker-compose.yml``` file:

![43](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/e78e7a1f-6b07-414e-bd1a-90c8e16760fb)

Let’s boot these services up:

![45](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/4e984b0c-59e1-4649-9726-2bb51967d4dc)

Now, that all three services are up, access the web interface by clicking the Link Extractor. There should be no visual difference from the previous step. However, if you extract links from a page with a lot of links, the first time it should take longer, but the successive attempts to the same page should return the response fairly quickly. To check whether or not the Redis service is being utilized, we can use ```docker-compose exec``` followed by the ```redis``` service name and the Redis CLI’s monitor command:

![46](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/48032702-607b-4bcb-8532-e43d1ca0ecd1)

Now, try to extract links from some web pages using the web interface and see the difference in Redis log entries for pages that are scraped the first time and those that are repeated. Before continuing further with the tutorial, stop the interactive monitor stream as a result of the above ```redis-cli``` command by pressing ```Ctrl + C``` keys while the interactive terminal is in focus.

Now that we are not mounting the ```/www``` folder inside the container, local changes should not reflect in the running service:

![49](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/69c057a6-2a92-4d10-b95d-81cdfdfc5c06)

![47](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f0cbc88f-ff06-434f-8ff0-7c972ced7567)

![48](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/bb44fef9-7226-4fbb-93ac-180c718ffda1)

Verify that the changes made locally do not reflect in the running service by reloading the web interface and then revert changes:

![51](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/8eb620d8-0416-445b-a14d-dd6d02e35d13)

Now, shut these services down and get ready for the next step:

![40](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/357aa0f6-589c-40db-8e06-6c3807a3efec)

## Conclusions

We started this tutorial with a simple Python script that scrapes links from a given web page URL. We demonstrated various difficulties in running the script. We then illustrated how easy to run and portable the script becomes onces it is containerized. In the later steps we gradually evolved the script into a multi-service application stack. In the process we explored various concepts of microservice architecture and how Docker tools can be helpful in orchestrating a multi-service stack. Finally, we demonstrated the ease of microservice component swapping and data persistence.

