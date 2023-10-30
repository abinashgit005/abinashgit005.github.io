---
title: Docker
layout: post
post-image: "/assets/images/docker.png"
description: A Basic Introduction to Docker
tags:
- DevOps
- Docker
---

# Welcome to Docker

## || Docker ||

* Docker is an open-source centralised platform designed to create and run applications.
* Docker uses container on the host OS to run applications. Itallows applications to use the same linux kernelas a system on the host computer, rather than creating a whole virtual OS.
* We can install docker on any OS but Docker engine run natively on linux distribution.
* Docker written is go language.
* Docker is a tool that performs OS level virtualisation also known as containerzation. 
* Before Docker, many users face the problem that a particular code is running in developer’s system but not in user’s system.
* Docker was first released in march 2003. It was founded by Solomen hykes, SebastienPahl and Kamel Founadi.
* Docker is aset of platform as a service that use OS Level virtulisation to deliver software in packages called containers.
* Vmware uses hardware level virtualisation.

In the above scenario, we want to create 2 containers 
    1. Ubuntu   2. Kalilinux
The host OS is linux/RHEL.
We know all these OS have similarities as all are flavours of linux/UNIX.
Now Docker Engiene will go to docker hub and pull 5% code ,(Image)  which is specifically required for ubuntu / kali linux because 95% of code we can get from the Host OS it self .
Then, docker engine will keep a copy of that (Image) with itself and copy to container. Now it became ubuntu container.

## Advantages
* No pre-allocation of RAM.
* CI Efficiency-Docker enables you to build a container image and use that same image across every step of the Deployment process. 
* Less cost.
* It is light in weight.
* It can run on physical hardware/ virtual hardware or on cloud.
* Ypou can re-use the image.
* It took very less time to create container.

Disadvantage of Docker

* Docker is not a good solution for application that requires rich GUI.
* Difficult to manage large amount of containers.
* Docker does not provide cross-platform compatibility means if an application is designed to run in a docker container on windows , then it can’t run on linux or vice-versa.
* Suitable when the development  OS and testing OS are same. If the OS is differnt, we should use VM.
* No solution for data recovery and back up.


Components of Docker

*Docker  Daemon*

* Docker daemon runs on the host OS.
* It is responsible for running containers to manage docker services.
* Docker Daemon can communicate with other daemons.

*Docker client*

* Docker users can intract with docker daemon through a client (CLI).
* Docker client uses command (CLI) and Rest API to Communicate with the Docker Daemon.
* When a client runs any server command on the docker client terminal , the client terminal sends the docker commands to the Docker Daemon .
* It is possible for docker client to communicate with more than none Daemon.

*Docker host*
* Docker Host is used to provide an environment to execute and run applications.
* It contains the Docker Daemon , images containers, networks and storages.

*Docker Hub / Registry*

Docker registry manages and stores the docker Images. There are two types of registries in the docker.
1. Public Registry :-  Public registry is also called as docker hub.
2. Private Registry :- It is used to share images with in the enterprise.

*Docker Images*

>Docker images are the read only binary templates used to create docker containers.

`or`

>Single file with all depedencies and configuration required to run a program.

*Ways to create an Images*

1. Take image from Docker Hub.
2. Create image from Docker file.
3. Create image from existing Docker Containers.

*Docker Container*

* Container hold the entire packages that is needed to run the application. In other words , we can say that , the image is a template and the container is a copy of that template.
* Containers is like a virtual machine.
* Images became container when they run on Docker  engine.

*Commands:*
``` docker
yum install docker -y          # to download the docker in Amazon-linux.
docker images                  # to see all the images inside your local machine.
docker search <image_name>     # to search the image in docker HUB.
docker pull<image_name>        # to download the image from docker HUB to your local machine.
docker run -it --name abidevops ubuntu /bin/bash.
                               # -it stands for interactive mode & terminal.
                               # we can write as -i -t as well.
                               # run will create and start.
                               # here abidevops is the new name i want to give to the contaiber.
                               # Ubuntu is thge image name to which i want to create and give a name.
service docker status          # to see service has start or not.
docker start <container name>  # to start the container
docker stop <container_name>   # to stop the container.
docker rm <container_name>     # to delete container.
docker attach <container_name> # to go insude the container.
docker ps                      # to see all the containers.
                               # PS stands for process status
docker ps -a                   # to see all the containers including in stopped stage.
```
>Inside a container if you want to see the os-release then, cat /etc/os-release.
>If you want to see the difference between the base image and any changes you have done on it,
```bash
docker diff mycontainer #Here you can give any container name*
```

## Create an Image from Container
```bash
docker commit mycontainer updateimage

#mycontainer is your container name and updateimage is the new image you have created from the container
```

## Docker File
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. 

*Docker Components ~*
```bash
FROM #This can be used to set the base image for the instructions. We need to mention this in the first line of docker file.
RUN
MAINTAINER
COPY # copy files from local
ADD
eXPOSE
WORKDIR
CMD
ENTRYPOINT
ENV
ARG
```
## || Docker Compose ||

Compose is a tool for defining and running multi-container Docker applications.
``` bash
version: '3'
services:
  webapp1:
    image: nginx
    ports:
      - "8000:80"

  webapp2:
    image: nginx
    ports:
      - "8001:80"
```
*Commands*

``` docker
docker-compose start #Starts existing containers for a service.

docker-compose stop #Stops running containers without removing them.

docker-compose pause #Pauses running containers of a service.

docker-compose unpause #Unpauses paused containers of a service.

docker-compose ps #Lists containers.

docker compose ls	# List running compose projects

docker-compose up #Builds, (re)creates, starts, and attaches to containers for a service.

docker-compose down #Stops containers and removes containers, networks, volumes, and images created by up.

docker-compose create # Creates containers for a service.

docker compose version	# Show the Docker Compose version information

docker compose kill	# Force stop service containers.

docker compose logs	# View output from containers.

docker compose port	# Print the public port for a port binding.

docker compose rm	# Removes stopped service containers

docker compose pull	# Pull service images

docker compose push	# Push service images

docker compose restart	# Restart service containers

```
*Example:*

```bash
# lets take the above example we have webapp1 and webapp2.
# NOw we want to scale it up.

docker compose scale webapp1 =4 webapp2=4
# The above command will create total 8 containers (4 webapp1 & 4 webapp2)
```

## || Docker Swarm ||
*Assume 3 machines master worker01 and worker02*

``` bash
docker swarm init
docker swarm info
docker node ls # lists all nodes
docker swarm join-token manager # join as master
docker swarm join-token worker #join as a worker
docker swarm leave # to leave from cluster
docker node rm worker01 # to remove node from cluster
docker node rm worker02 # to force remove node from cluster
docker node inspect worker01 #inspect node worker01
docker node inspect worker01 | less
docker node promote worker01 worker02 # promote worker node to master
docker node demote worker01 worker02 # demote worker node
docker service ls # list all services.
docker service scale 9m=7 # here 9m is service_ID & this command scale the replicas to 7.
docker service create -d --replicas 4 alpine ping 192.168.25.10 # create a service named alpine and ping the IP
```

![dockermaster](/assets/images/dockermaster.jpg)

## || Docker Volume ||
Docker vloumes are persistent storage locations for the containers and managed by docker completely. It can be easily attached and removed from containers. We can back up our volumes as well.
``` bash
sudo docker volume create myvolume #create a docker volume named my volume
sudo docker volume ls # list all the volume in machine.
sudo docker volume inspect myvolume # it gives volume information.
# mountpoint is the particular place inside the host, where docker assigned the volume.
sudo docker volume rm myvolume # it removes volume "myvolume".
sudo docker volume prune # It remove all local volume not used by atleast any one container.
```
#There are two ways we can use volume while creating container. we can use --mount or --volume.

#We can use mount flag with bind mount and tmfs 
```bash
sudo docker run --it -d -name containerA --mount source=vol1,target=/apps ubuntu
sudo docker run --it -d -name containerB --volume vol2:/apps ubuntu
```
#We can create readonly volume.
``` bash
sudo docker volume create myvolumeRO # create a read-only volume named "myvolumeRO"
sudo docker run --it -d -name containerC --mount source=myvolumeRO,target=/apps,readonly ubuntu
```

## || Bind Mount ||
* When you use a bind mount, a file or directory on the host machine is mounted into a container.

* The file or directory is referenced by its absolute path on the host machine. 

* *By contrast, when you use a volume, a new directory is created within Docker’s storage directory on the host machine, and Docker manages that directory’s contents.*


```bash
sudo docker run -d -it --name containerD --mount type=bind,source="$(pwd)"/target,target=/apps ubuntu
```
## || Tmpfs Mount ||
 Tmpfs is not persistent like volumes and tmpfs and get removed when container to which they are attached are stopped.


### Limitations of tmpfs mounts :
* Unlike volumes and bind mounts, you can’t share tmpfs mounts between containers.

* This functionality is only available if you’re running Docker on Linux.

```bash
sudo docker run -d -it --name tmptest --mount type=tmpfs,destination=/apps ubuntu
  ```
## || Docker Network ||
docker network is a connection in between one or more containers 

One advantage is we can connect docker containers  together, or connect them to non-Docker workloads.

### Types of Docker Network

![Docker Networking](/assets/images/docker_networking.jpg)

### Bridge:
 * The default network driver. If you don’t specify a driver, this is the type of network you are creating. Bridge networks are usually used when your applications run in standalone containers that need to communicate

 * Here an internal private network is getting created, which is attached to docker host and containers.
 

### Host: 
For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly

here the container is attached to the host network itself and there is no network  isolation in between the host and container 

```
docker run --network host nginx
```

### Overlay: 
Overlay networks connect multiple Docker daemons together and enable swarm services to communicate with each other. You can also use overlay networks to facilitate communication between a swarm service and a standalone container, or between two standalone containers on different Docker daemons. This strategy removes the need to do OS-level routing between these containers

### Macvlan: 
Macvlan networks allow you to assign a MAC address to a container, making it appear as a physical device on your network. The Docker daemon routes traffic to containers by their MAC addresses. Using the macvlan driver is sometimes the best choice when dealing with legacy applications that expect to be directly connected to the physical network, rather than routed through the Docker host’s network stack.

### None: 
For this container, disable all networking. Usually used in conjunction with a custom network driver. none is not available for swarm services.
```
docker run --network none nginx
```
## Network related Command
```bash
docker network ls # list all networks
ip link
ipnetns
```

### Docker Stack:
Docker stack is a group of inter-related services that together form an entire Application.\
Example: imagine a stack consists of 3 node.js applications and 1 Redis messaging service and 2 databases