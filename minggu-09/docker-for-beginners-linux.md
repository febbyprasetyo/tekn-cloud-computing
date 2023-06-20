# Docker for Beginners - Linux

Tasks:

- [Task 0: Prerequisites](https://training.play-with-docker.com/beginner-linux/#Task_0)

- [Task 1: Run some simple Docker containers](https://training.play-with-docker.com/beginner-linux/#Task_1)

- [Task 2: Package and run a custom app using Docker](https://training.play-with-docker.com/beginner-linux/#Task_2)

- [Task 3: Modify a Running Website](https://training.play-with-docker.com/beginner-linux/#Task_3)

## Task 0: Prerequisites

You will need all of the following to complete this lab:

- A clone of the lab’s GitHub repo.
- A DockerID.

### Clone the Lab’s GitHub Repo

Use the following command to clone the lab’s repo from GitHub (you can click the command or manually type it). This will make a copy of the lab’s repo in a new sub-directory called ``linux_tweet_app``.

![1](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/80e4f933-83b0-4780-8ae6-b15be27414de)

### Make sure you have a DockerID

If you do not have a DockerID (a free login used to access Docker Hub), please visit [Docker Hub](https://hub.docker.com/) and register for one. You will need this for later steps.

## Task 1: Run some simple Docker containers

There are different ways to use containers. These include:

1. To run a single task: This could be a shell script or a custom app.

2. Interactively: This connects you to the container similar to the way you SSH into a remote server.

3. In the background: For long-running services like websites and databases.

In this section you’ll try each of those options and see how Docker manages the workload.

### Run a single task in an Alpine Linux container

1. Run the following command in your Linux console.

![2](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/5a3f4170-2d95-4a5f-afeb-3e7399541b76)

The output below shows that the ``alpine:latest`` image could not be found locally. When this happens, Docker automatically pulls it from Docker Hub.

2. Docker keeps a container running as long as the process it started inside the container is still running. In this case the hostname process exits as soon as the output is written. This means the container stops. However, Docker doesn’t delete resources by default, so the container still exists in the Exited state.

![3](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/a253cb3e-97bd-4408-baad-9dde1020a1a9)

### Run an interactive Ubuntu container

1. Run a Docker container and access its shell.

![4](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/88453e63-9de5-4630-ad93-3284518ba618)

2. Run the following commands in the container.

![5](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/cc9a2593-1e22-436e-b5da-6c0f1419f74d)

3. Type exit to leave the shell session. This will terminate the bash process, causing the container to exit.

![6](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c1b73961-6da4-4b72-a277-1843ad08cd2d)

4. For fun, let’s check the version of our host VM.

![7](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/ada45493-811e-4b16-9583-b1dce44a2eea)

### Run a background MySQL container

1. Run a new MySQL container with the following command.

![8](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/7e5b81f4-a4c4-4868-831f-ea457803a1a8)

2. List the running containers.

![9](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/275c55ba-a43e-4687-ad54-e7aac0329b2a)

3. You can check what’s happening in your containers by using a couple of built-in Docker commands: ``docker container logs`` and ``docker container top``.

![10](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/5033680a-d0b8-452f-810f-204cac0c67fe)

Let’s look at the processes running inside the container.

![11](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/59ad9a4b-e17c-4e2f-bbbc-fa5662d43afc)

4. List the MySQL version using ``docker container exec``.

![12](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/082fda3e-8b0e-46b4-8a41-3d5b5f6541c3)

5. You can also use ``docker container exec`` to connect to a new shell process inside an already-running container. Executing the command below will give you an interactive shell (sh) inside your MySQL container.

![13](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/fa3b0ec3-dd6a-4b6b-b37c-4c6d664b83d1)

6. Let’s check the version number by running the same command again, only this time from within the new shell session in the container.

![14](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/8a6ca9cb-a332-4d2e-9dc9-96f1a7ad9d40)

7. Type exit to leave the interactive shell session.

![15](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/eddaeb04-87a8-40b6-834c-76c817fa2ef0)

## Task 2: Package and run a custom app using Docker

### Build a simple website image

Let’s have a look at the Dockerfile we’ll be using, which builds a simple website that allows you to send a tweet.

1. Make sure you’re in the ``linux_tweet_app`` directory.

![16](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f079a113-b4f5-49bc-a418-15c1d1a52c82)

2. Display the contents of the Dockerfile.

![17](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/6ac69600-7d66-466e-a4ff-1002161e57df)

3. In order to make the following commands more copy/paste friendly, export an environment variable containing your DockerID (if you don’t have a DockerID you can get one for free via Docker Hub).

You will have to manually type this command as it requires your unique DockerID.

```
export DOCKERID=<your docker id>
```

4. Echo the value of the variable back to the terminal to ensure it was stored correctly.

![18](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/21208015-fe06-4533-b7c1-edb2b925f922)

5. Use the docker image build command to create a new Docker image using the instructions in the Dockerfile

![19](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/b7f16853-67bb-4185-aea1-9a14f0170401)

6. Use the docker container run command to start a new container from the image you created.

![20](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/5a40bc8c-8eda-4f56-aa81-d028c52e11cd)

7. Click here to load the website which should be running

![23](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c2521982-e5d8-4b1c-b557-67468edd82d4)

## Task 3: Modify a running website

## Start our web app with a bind mount

1. Let’s start the web app and mount the current directory into the container.

In this example we’ll use the --mount flag to mount the current directory on the host into ``/usr/share/nginx/html`` inside the container.

Be sure to run this command from within the ``linux_tweet_app`` directory on your Docker host.

![24a](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/84dd5827-4da2-446e-a95b-16062beff838)

### Modify the running website

1. Copy a new ``index.html`` into the container.

![25a](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/7f4a469b-2757-4899-9e9f-d130b3495366)

2. Go to the running website and refresh the page. Notice that the site has changed.

![29](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/75246dc7-ffa1-4e6a-877d-b5a24567469f)

Even though we’ve modified the index.html local filesystem and seen it reflected in the running container, we’ve not actually changed the Docker image that the container was started from.

To show this, stop the current container and re-run the 1.0 image without a bind mount.

1. Stop and remove the currently running container.

![25](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f49c2425-3dcd-4afc-89c2-cd3be7ad3708)

2. Rerun the current version without a bind mount.

![24a](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/84dd5827-4da2-446e-a95b-16062beff838)


3. Notice the website is back to the original version.

![23](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c2521982-e5d8-4b1c-b557-67468edd82d4)

4. Stop and remove the current container

![25](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f49c2425-3dcd-4afc-89c2-cd3be7ad3708)

### Update the image

1. Build a new image and tag it as 2.0

![26](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/3a6244d2-b528-4d24-8ea2-0c730f1c5290)

2. Let’s look at the images on the system.

![27](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/7639ae85-5f29-4ec4-a799-2cfd4bbfc62a)

### Test the new version

1.Test the new version

![28](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/6d13f094-b59e-4007-9b72-635975d95060)

2. Check the new version of the website (You may need to refresh your browser to get the new version to load).

![29](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/75246dc7-ffa1-4e6a-877d-b5a24567469f)

3. Run another new container, this time from the old version of the image.

![30](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/e9f85fe6-7cb2-4fb5-b6f5-d5ceb20b25ec)

4. View the old version of the website.

![23](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c2521982-e5d8-4b1c-b557-67468edd82d4)

### Push your images to Docker Hub

1. List the images on your Docker host.

![31](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/4a9cb50e-1730-4790-9127-c3ce5ba038e2)

2. Before you can push your images, you will need to log into Docker Hub.

![32](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/663751c8-6552-4721-8582-ba62b6805c0b)

3. Push version 1.0 of your web app using ``docker image push``.

![33](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/8e053e82-e951-457c-9f05-b4e1038233cc)

4. Now push version 2.0

![34](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/65f0570f-db36-44fe-b30b-3c9e180bc085)

![35](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/23b79bf7-28c9-4e15-9bbb-6c4f43a1a59f)











