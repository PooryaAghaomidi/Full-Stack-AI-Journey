# Docker tutorial

<p align="center">
  <img src="Images/docker.svg" width="400"/>
</p>

## Table of Contents

- [Installation](#installation)
- [Introduction](#introduction)
- [Section One: Basic Commands](#section-one-basic-commands)
- [Section Two: WorkFlow](#section-two-workflow)

## Installation

Download and install docker from the official website: https://docs.docker.com/engine/install/

Follow the instructions in the link above, since there are a number of requirements for installing docker.

Then you can run git commands on your command shell (e.g. WSL, CMD, PowerShell, etc.)

## Introduction

### Overview

Docker is a platform designed to help developers build, share, and run container applications.

`Container`: A Docker container is a lightweight, portable, executable package of software that includes everything
needed to run an application: code, runtime, system tools, system libraries and settings.

`Image`: Docker images are read-only templates that contain instructions for creating a container. A Docker image is a
snapshot or blueprint of the libraries and dependencies required inside a container for an application to run.

`DockerFile`: A Dockerfile is a text file that contains a series of instructions on how to build a Docker image. It
specifies the base image, necessary software installations, file copies, environment settings, and commands to run
inside the container. Docker reads the Dockerfile to automate the image creation process.

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

`Defining Host Port`:

1. You can define any port number between 1 and 65535 for your localhost applications.
2. Ensure the port is available and not already in use.
3. Prefer ports above 1024 to avoid conflicts with well-known services.

### Docker Network

`Docker Network`: In Docker, a network is a communication pathway that allows different Docker containers to talk to
each other or to communicate with other networks, such as the internet or your local network.

## Section One: Basic Commands

* `docker pull <image>:<tage>`: download an image with a specific version (if you do not specify the version, it will
  download the latest one)
* `docker images`: display all downloaded images (along with tag, image id, date, and size)
* `docker run <image>`: run an image in a container
* `docker run -d <image>`: run an image in a container without displaying information and engaging command shell
* `docker run --name <container name> <image>`: run an image in a container with specifying the containers name
* `docker run -p <host port>:<container port> <image>`: run an image in a container with specific ports
* `docker ps`: display all running containers (along with image, date, status, and port)
* `docker ps -a`: display all running and stopped containers
* `docker stop <container id/name>`: stop running the container
* `docker start <container id/name>`: restart running an existed stopped container
* `docker logs <container id/name>`: display all logs for the container
* `docker exec -it <container id/name> /bin/hash`: display inside the container and all the required information of it (
  deactivate by exit)

## Section Two: WorkFlow

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
