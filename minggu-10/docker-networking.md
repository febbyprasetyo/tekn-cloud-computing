# Docker Networking Hands-on Lab

### Tasks:

- [Section #1 - Networking Basics](https://training.play-with-docker.com/docker-networking-hol/#task1)

- [Section #2 - Bridge Networking](https://training.play-with-docker.com/docker-networking-hol/#task2)

- [Section #3 - Overlay Networking](https://training.play-with-docker.com/docker-networking-hol/#task3)

- [Cleaning Up](https://training.play-with-docker.com/docker-networking-hol/#cleanup)

## Section #1 - Networking Basics

### Step 1: The Docker Network Command

The ```docker network``` command is the main command for configuring and managing container networks. Run the ```docker network``` command from the first terminal.

![1](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/70dbdb24-1daa-4d01-ba97-6919d958c52c)

### Step 2: List networks

Run a ``docker network ls`` command to view existing container networks on the current Docker host.

![2](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/447030cf-175c-4967-a9e4-fcd3b2a3da1c)

### Step 3: Inspect a network

The ```docker network inspect``` command is used to view network configuration details. These details include; name, ID, driver, IPAM driver, subnet info, connected containers, and more.

Use ```docker network inspect <network>``` to view configuration details of the container networks on your Docker host. The command below shows the details of the network called ```bridge```.

![3](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/72ef5ba8-89b1-4375-8319-db032d929a08)

### Step 4: List network driver plugins

The ```docker info``` command shows a lot of interesting information about a Docker installation.

Run the ```docker info``` command and locate the list of network plugins

![4](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/6481178c-7e68-4d03-822b-be1886b84723)

## Section #2 - Bridge Networking

### Step 1: The Basics

Every clean installation of Docker comes with a pre-built network called bridge. Verify this with the docker ```network ls```.

![5](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/9e6b54f2-2ff0-47d0-972c-5c434def8479)

Install the ```brctl``` command and use it to list the Linux bridges on your Docker host. You can do this by running ```sudo apt-get install bridge-utils```.

![6](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f0aa1ab2-15a7-4896-807e-fd0e92cca239)

![7](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/bf639101-5074-4a66-a61f-07e085730f4f)

Then, list the bridges on your Docker host, by running ```brctl show```.

![8](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/19cdbe76-3474-405b-978a-767f0b2b20da)

You can also use the ```ip a``` command to view details of the docker0 bridge.

![9](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/08a5a90c-6fea-4e16-80d5-f027f44ae630)

### Step 2: Connect a container

The bridge network is the default network for new containers. This means that unless you specify a different network, all new containers will be connected to the bridge network.

Create a new container by running ```docker run -dt ubuntu sleep infinity```.

![10](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/73ec09f8-0e09-43ae-bb7c-8a4b25181821)

This command will create a new container based on the ```ubuntu:latest``` image and will run the ```sleep``` command to keep the container running in the background. You can verify our example container is up by running ```docker ps```.

![11](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/8ba9bc3b-0aa7-4245-bec0-b73c95f1f7d4)

Run the ```brctl show``` command again.

![12](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/5dbf84eb-eeda-4e07-a944-bce1e4b9bc4f)

You can inspect the bridge network again, by running ```docker network inspect bridge```, to see the new container attached to it.

![13](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/9478189d-cfb5-4db5-bfd2-f9cfa7012a3a)

### Step 3: Test network connectivity

First, we need to get the ID of the container started in the previous step. You can run ```docker ps``` to get that.

![14](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f61c10a8-4dee-46d9-9033-5dbddfeffba3)

Lets ping www.github.com by running ```ping -c5 www.github.com```.

![15](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/dd907df3-6b41-475a-90f1-cc8102092cc4)

Finally, lets disconnect our shell from the container, by running ```exit```.

![16](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/312c76d6-2436-4097-b3af-fa7fec874a2c)

We should also stop this container so we clean things up from this test, by running ```docker stop <CONTAINER ID>```.

![17](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/40746bda-371b-44c0-9bea-25aa28290b7b)

### Step 4: Configure NAT for external connectivity

In this step we’ll start a new NGINX container and map port 8080 on the Docker host to port 80 inside of the container. This means that traffic that hits the Docker host on port 8080 will be passed on to port 80 inside the container.

Start a new container based off the official NGINX image by running ```docker run --name web1 -d -p 8080:80 nginx```.

![18](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/47899a96-a649-4a6c-9c24-6a969fbb12d9)

Review the container status and port mappings by running ```docker ps```.

![19](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/14c29b56-c97d-41de-bdc7-bed293a68d27)

If for some reason you cannot open a session from a web broswer, you can connect from your Docker host using the curl ```127.0.0.1:8080``` command.

![20](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/37dd4e00-db3a-4ccf-971e-cb3fdb0cf92f)

## Section #3 - Overlay Networking

### Step 1: The Basics
In this step you’ll initialize a new Swarm, join a single worker node, and verify the operations worked.

Run ```docker swarm init --advertise-addr $(hostname -i)```.

![21](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/57533e62-1778-48c4-99dd-6ad4f1799fb7)

Run a ```docker node ls``` to verify that both nodes are part of the Swarm.

![22](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/4a281297-bb16-400d-abeb-251c956f16ab)

### Step 2: Create an overlay network

Now that you have a Swarm initialized it’s time to create an overlay network.

Create a new overlay network called “overnet” by running ```docker network create -d overlay overnet```.

![23](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/de2f11dc-1668-4f45-bf74-167df567f514)

Use the ```docker network ls``` command to verify the network was created successfully.

Run the same ```docker network ls``` command from the second terminal.

![24](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/844c2d6c-0182-494c-a482-3da4d8d12485)

Use the ```docker network inspect <network>``` command to view more detailed information about the “overnet” network. You will need to run this command from the first terminal.

![26](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/7e7ff145-02b3-4417-acda-21e41cab0bff)

### Step 3: Create a service

Now that we have a Swarm initialized and an overlay network, it’s time to create a service that uses the network.

Execute the following command from the first terminal to create a new service called myservice on the overnet network with two tasks/replicas.

![27](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/d7abdd38-e25c-4449-a801-e2c21adc45be)

Verify that the service is created and both replicas are up by running ```docker service ls```.

![28](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/01f3adb5-4d7d-4dde-9718-e7020f4534cf)

Verify that a single task (replica) is running on each of the two nodes in the Swarm by running ```docker service ps myservice```.

![29](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/761a1218-2202-4705-b36c-4b8a37e62e74)

Now that the second node is running a task on the “overnet” network it will be able to see the “overnet” network. Lets run ```docker network ls``` from the second terminal to verify this.

![30](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/33c2c9bf-0248-4a5a-8fe3-9eb0624c8089)

We can also run ```docker network inspect overnet``` on the second terminal to get more detailed information about the “overnet” network and obtain the IP address of the task running on the second terminal.

### Step 4: Test the network

To complete this step you will need the IP address of the service task running on node2 that you saw in the previous step (10.0.0.3).

Execute the following commands from the first terminal.

![31](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/583e44e4-759a-4387-a2ce-f797cd9d1fc9)

Run a ```docker ps``` command to get the ID of the service task so that you can log in to it in the next step.

![32](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/a69bca7d-7d7a-41a6-a232-40b1147aebfb)

Log on to the service task. Be sure to use the container ID from your environment as it will be different from the example shown below. We can do this by running ```docker exec -it <CONTAINER ID> /bin/bash```.

![33](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f07b13fa-bac0-4bd7-81cf-c000220c1f03)

Install the ping command and ping the service task running on the second node where it had a IP address of 10.0.0.3 from the docker network inspect overnet command.

![34](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/1390983c-0b37-4d82-a5c6-dee0fe05d641)

### Step 5: Test service discovery

Now that you have a working service using an overlay network, let’s test service discovery.

If you are not still inside of the container, log back into it with the ```docker exec -it <CONTAINER ID> /bin/bash``` command.

Run ```cat /etc/resolv.conf``` form inside of the container.

![35](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/70f3894d-4e2f-4371-9a7e-8bdd10b74f3f)

Try and ping the “myservice” name from within the container by running ```ping -c5 myservice```.

![36](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/3c6019b8-ff17-408a-b00b-636c35b6d20e)

Type the ```exit``` command to leave the exec container session and return to the shell prompt of your Docker host.

Inspect the configuration of the “myservice” service by running ```docker service inspect myservice```. Lets verify that the VIP value matches the value returned by the previous ```ping -c5 myservice``` command.

![37](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/1389af60-12fc-403c-9916-cacf3e5de7ba)

## Cleaning Up
Hopefully you were able to learn a little about how Docker Networking works during this lab. Lets clean up the service we created, the containers we started, and finally disable Swarm mode.

Execute the docker ```service rm myservice``` command to remove the service called myservice.

![38](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/51e432dd-12d2-4822-96cc-de22c9316fa0)

Execute the ```docker ps``` command to get a list of running containers.

![39](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/8df327ba-440c-4491-b4dd-36f7523e7a78)

Lets run ```docker swarm leave --force```

![40](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/024e7523-0271-4573-9f28-95960075d0a1)

Congratulations! You’ve completed this lab!




