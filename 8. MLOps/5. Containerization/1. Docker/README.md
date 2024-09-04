# Docker tutorial

<p align="center">
  <img src="Images/docker.svg" width="400"/>
</p>

## Table of Contents

- [Installation](#installation)
- [Introduction](#introduction)
- [Section One: Basic Commands](#section-one-basic-commands)
- [Section Two: Docker Compose](#section-two-docker-compose)
- [Section Three: Docker File](#section-three-docker-file)

## Installation

Download and install docker from the official website: https://docs.docker.com/engine/install/

Follow the instructions in the link above, since there are a number of requirements for installing docker.

Then you can run git commands on your command shell (e.g. WSL, CMD, PowerShell, etc.)

## Introduction

### Overview

Docker is a platform designed to help developers build, share, and run container applications.

`Layer`: Layers in Docker images are incremental changes or instructions that make up the final image, created from each
command in the Dockerfile. These layers stack on top of each other, starting from a base layer, such as an operating
system, and adding additional layers like software installations or application code. Layers are reusable and shared
between images, which optimizes storage and speeds up the building and deployment processes.

`DockerFile`: A Dockerfile is a text file that contains a series of instructions on how to build a Docker image. It
specifies the base image, necessary software installations, file copies, environment settings, and commands to run
inside the container. Docker reads the Dockerfile to automate the image creation process.

`Image`: Docker images are read-only templates that contain instructions for creating a container. A Docker image is a
snapshot or blueprint of the libraries and dependencies required inside a container for an application to run.

`Container`: A Docker container is a lightweight, portable, executable package of software that includes everything
needed to run an application: code, runtime, system tools, system libraries and settings.

<p align="center">
  <img src="Images/flow.png" width="600"/>
</p>

`Docker Hub`: Docker Hub is a container registry where developers and open source contributors can find, use, and share
container images. It allows hosting public repositories for free and private repositories for teams and enterprises.

### Comparisons

`Docker images vs. DockerFiles`: The Dockerfile contains all the instructions to build the image. You have to place the
Dockerfile along with all associated libraries and dependencies in a folder to build the image.

`Docker images vs. Containers`: A Docker image is a blueprint or template, while a container is the running instance
created from that image. The image provides the instructions, and the container is the executable environment for
running applications.
Think of a container as a shipping container for software — it holds important content like files and programs so that
an application can be delivered efficiently from producer to consumer. Docker uses images to create containers and
containers to run the applications.

`Docker vs. Virtual Machines`: Docker containers share the host OS kernel, making them lightweight and fast to start,
while VMs run a full OS, making them more resource-intensive and slower to start but providing stronger isolation and
the ability to run different OSes.

<p align="center">
  <img src="Images/comparison.png" width="600"/>
</p>

Here you can see a comparison between docker and virtual machines:

<p align="center">
  <img src="Images/structure.png" width="600"/>
</p>

This picture is true about Docker when Linux is the host OS. In host operating systems other than Linux, Docker uses a
lightweight virtual machine to provide the necessary Linux kernel environment. On Windows, Docker Desktop uses Hyper-V
or WSL 2 to run a minimal Linux VM, while on macOS, a similar lightweight VM is used. This VM allows Docker to
efficiently run Linux containers by sharing the host system's resources without creating a full virtualized OS.

### Ports

`Host Port`: The host port is a specific communication endpoint on this machine that is exposed to the outside world.
When you map a host port to a container port, you're making the container's service accessible via this port on your
host machine.

`Container Port`: The container port is the specific port inside the container that your application listens to.

`Port Management`: Imagine you have a web application running inside a Docker container on port 80. If you want to
access this web application from your host machine, you need to map a host port to this container port. Let's say you
map host port 8080 to container port 80. The mapping can be represented as 8080:80. If you have 2 images with similar
ports, you should solve this conflict by binding them with 2 different ports of the host.

`Note`: Defining Host Port:

1. You can define any port number between 1 and 65535 for your localhost applications.
2. Ensure the port is available and not already in use.
3. Prefer ports above 1024 to avoid conflicts with well-known services.

`Note`: You can type `localhost:<host port>` and see a running container that is connected to that port.

### Docker Network

`Docker Network`: In Docker, a network is a communication pathway that allows different Docker containers to talk to
each other or to communicate with other networks just by calling container name. Everything outside the docker network
communicate with the network by ports.

`Note`: If you want to connect two containers in a network, you should follow these steps:

1. Create a network
2. Create a container for the first image by defining port, name, and the created network
3. Create another container for the second image by defining a different port, different name, and the same network and
   also defining the server in environment variable as the first container

### Docker Volumes

`Docker volumes`: Docker volumes store data outside containers, so the data isn't lost when containers stop or restart.
They help share data between containers and keep data safe on the host machine.

`Note`: Docker saves the data in the docker installation folder.

## Section One: Basic Commands

### Image

* `docker pull <image>:<tage>`: download an image with a specific version (if you do not specify the version, it will
  download the latest one)
* `docker images`: display all downloaded images (along with tag, image id, date, and size)
* `docker rmi <image id>`: delete the image

### Network

* `docker network create <network name>`: create a network by specifying a name
* `docker network ls`: display all available networks

### Create a Container

* `docker run <image>`: run an image in a container
* `docker run -d <image>`: run an image in a container without displaying information and engaging command shell
* `docker run --name <container name> <image>`: run an image in a container with specifying the containers name
* `docker run -p <host port>:<container port> <image>`: run an image in a container with specific ports
* `docker run --net <network name>`: run an image in a container in a specific network
* `docker run -e <environment variable parameter>=<environment variable value>`: run an image in a container with
  specifying environment variable parameters
* `docker run -it <image> <command shell>`: run an image while we can run commands interactively inside the container's
  shell (e.g. bash and sh)
* `docker run -v <data name>:<path of the data you want to survive>`: run an image while copying its data into the host
  directory

### Manage a Container

* `docker ps`: display all running containers (along with image, date, status, and port)
* `docker ps -a`: display all running and stopped containers
* `docker stop <container id/name>`: stop running the container
* `docker start <container id/name>`: restart running an existed stopped container
* `docker logs <container id/name>`: display all logs for the container
* `docker exec -it <container id/name> /bin/<command shell>`: open command shell inside the container (deactivate by
  exit)
* `docker rm <container id>`: delete the container

## Section Two: Docker Compose

### Concepts

`Docker compose`: Docker Compose is a tool that simplifies running multi-container Docker applications by using a single
YAML configuration file (typically `docker-compose.yaml`) to define the services, networks, and volumes needed. This
file allows you to describe how your application's containers should be set up and interact with each other, providing
easy commands to manage the entire application stack.

### Codes

* `docker-compose -f <yaml file name>.yaml up`: run the yaml file and create all defined containers in a network
* `docker-compose -f <yaml file name>.yaml down`: stop the containers and the network created by the yaml file

Every time you stop a container, all the configurations you made will be lost.

### Sample

`docker-compose.yaml`:

```yaml
version: '<compose version>' (latest is 3)

services:
  <container name>:
    image: <image name>
    ports:
      - <host port>:<container port>
    environment:
      - <environment variable parameter>=<environment variable value>
    volumes:
      - <data name>:<path of the data you want to survive>

  <other container name>:
    ...
volumes:
  <data name>:
    driver: local
```

It creates a network automatically, and defining it manually is not required.

## Section Three: Docker File

### Concepts

`Note`: parent image should be downloaded from docker hub separately.

`Note`: you can use `\` to continue writing one single line of command in the next line, and `&&` means we want to write
another line.

`Note`: every command in docker will apply to the container environment, not the host environment.

`Note`: The symbols `.` and `./` refer to paths on your host machine where Docker commands are executed (docker build,
docker run). But `/` refers to paths inside the Docker container's filesystem that's being built by the Docker image.

`Note`: some points about paths:

1. Paths in COPY commands refer to the host (source) and the container (destination).
2. Paths in CMD or WORKDIR commands refer to the container's filesystem.

### Codes

* `FROM <parent image>:<version>`: set the parent image for the image (like python)
* `SET <environment variable parameter>=<environment variable value>`: change an environment variable
* `RUN <cmd command>`: run cmd commands
* `COPY <source> <destination>`: copy from source to destination (if we use `.` as source, it means we are copying from
  host)
* `CMD ["<parent image without version>", <"main file that we want to execute">]`: run the main code with the parent
  image
* `WORKDIR`: specifies the working directory inside the Docker container
* `EXPOSE`: documents the ports on which the container listens for connections

### Sample

`Dockerfile` sample:

Assume the folders are like this:

```text
my_project/
├── Dockerfile
├── app/
│   ├── main.py
│   └── requirements.txt
```

Then we can write a dockerfile like this:

```text
FROM python:3.8-slim

WORKDIR /app

COPY ./app/requirements.txt /app

COPY ./app /app

EXPOSE 5000

CMD ["python", "app/main.py"]
```

* `docker build -t <image name>:<image version> <docker file location>`: create an image out of the dockerfile

By running this image, docker will compose the yaml file automatically and use the specified images.

### Push the image

After building the image, you can push your image into a docker repository platform like aws and docker hub. But first,
you should tag that image.

* `docker tag <image name>:<image version> <platform domain>/<image name>:<image version>`: copy the image and rename it
  to the domain name with the specified tag
* `docker push <platform domain>/<image name>:<image version>`: push the image to the platform

## Note

```text
I will update this tutorial if I acquire any new information.
```

## Sources

```text
www.docker.com
www.youtube.com/@TechWorldwithNana
www.linkedin.com/in/ashishyadav711
```
