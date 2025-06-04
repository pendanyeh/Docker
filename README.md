# Introduction to Docker and what a Devops and Cloud engineer should know about this tool.

## Repo to learn Docker with examples. Contributions are most welcome.

## Requirements for Docker Desktop installation

**Docker Desktop on Windows**

**System Requirements:**
- Windows 10 64-bit (Pro, Enterprise, or Education, Build 19044 or newer)
- Windows 11 64-bit (all editions)
- WSL 2 (Windows Subsystem for Linux v2) must be installed and enabled
- Virtualization enabled in BIOS (Intel VT-x or AMD-V)
- At least 4 GB RAM (8 GB or more recommended)
- Hyper-V and Containers features are enabled in Windows

**Docker Desktop on macOS**  

**System Requirements:**
- macOS Monterey 12.5 or later, including Ventura
- Compatible with both Apple Silicon (M1/M2, Rosetta 2 needed for some x86 images) and Intel Macs
- Minimum 4 GB RAM

**Docker Desktop on Linux**  

**System Requirements (Preview/Stable for Some Distros):**

- Supported distributions: Ubuntu 22.04+, Debian 11+, Fedora 35+
- 64-bit architecture
- systemd as the init system
- Virtualization support
- At least 4 GB RAM
- Kernel version 5.15 or newer

**General Requirements for All Platforms:**

- Administrative or root access for installation
- Reliable internet connection to download Docker images and updates

## Commonly used terminology: Docker Engine, Docker Daemon, Docker Desktop, Dockerhub

## 1. Docker Engine

- The main part of Docker, responsible for building, running, and managing containers.  

**It works as a client-server application and includes:**

- Docker Daemon (`dockerd`)
- Docker Command Line Interface (docker)
It operates on Linux and handles all container-related tasks.

## 2. Docker Daemon (`dockerd`)

- This is the background process that manages containers.  
- It listens for Docker API requests (from the CLI, Docker Desktop, etc.), and is responsible for starting and
  stopping containers, as well as managing images, volumes, and networks.  
- It’s a key part of the Docker Engine.

## 3. Docker Desktop 

- An all-in-one application for Mac and Windows that provides a graphical interface and environment for Docker.
  
**It comes with:**
  
- Docker Engine (including the Daemon)
- Docker CLI
- Optional Kubernetes support
- A GUI dashboard
- WSL 2 integration (on Windows)

- Docker Desktop simplifies Docker usage for developers by handling setup and configuration.
  
## 4. Dockerhub

**Docker Hub**  

- An online registry service (similar to GitHub, but for Docker images).
- It allows you to upload, download, and share Docker images.
- Supports both public and private repositories.

## Breakdown note:

| Component      | Role                                                   |
| -------------- | ------------------------------------------------------ |
| Docker Desktop | GUI + bundled setup for developers                     |
| Docker Engine  | The container platform powering everything             |
| Docker Daemon  | The backend service that does the work (inside Engine) |
| Docker Hub     | Cloud-based image storage & distribution service       |
 
# Docker Architecture in a diagram 

![image](https://github.com/user-attachments/assets/6026d7f1-9c85-4bdc-a173-2cbd1345c3fd)

## Follow the link below to visit the Docker website

https://docs.docker.com/get-started/images/docker-architecture.webp

# Prerequisites

## 1. Basic Command Line Skills

**You should be comfortable with:**

* Navigating directories (cd, ls, pwd)

* Editing files (nano, vim, or using VS Code)

* Running scripts and installing packages

## 2. Operating Systems & Virtualization Concepts

* Understand how traditional applications run on OSes

* Know what virtual machines are (optional but useful)

* Learn the difference between VMs vs Containers

## 3. Networking Basics
* What are ports and IP addresses

* What is localhost

* Basics of client-server communication (e.g., HTTP)

## 4. Software Development & Deployment Basics
* Know what builds, environments, and dependencies are

* Familiarity with package managers (e.g., npm, pip, apt)

* Concept of an application stack (e.g., Node.js + MongoDB)

## 5. Understanding of Source Control (Git)
* You don’t need to be a Git expert, but you should:

* Know how to clone, commit, and push

* Be able to manage basic branches

## 6. Familiarity with YAML & Configuration Files
* Docker and related tools (like Docker Compose or Kubernetes) rely heavily on configuration in YAML and .env files.

## 7. Optional but Helpful: Linux Fundamentals
* Knowing basic file system layout (e.g., /etc, /usr, /var)

* Managing permissions

* Running services or daemons

* Once you're comfortable with these, start learning Docker with small projects—like containerizing a simple web app.

  

# 🐳 Getting Started with Docker: 

## 1. What is Docker?
* Docker is a containerization tool that packages applications and their dependencies into containers.
  Containers are lightweight, fast, and portable across environments—ideal for DevOps.

## 2. Why Use Docker?
* Works the same on any system (dev, staging, prod)

* Fast startup, isolated environments

* Easy to scale and integrate with cloud and CI/CD

## 3. Install Docker

Ways to install Docker, Cloud based installation or Locally based installation. For the latter,
find the link below. Window users please make sure to check if your Windows OS is AMD64 or ARM64
before you start any installation.

* Windows/macOS: Install Docker Desktop from https://www.docker.com/products/docker-desktop
* For Windows OS, Open Settings > System > About

### Look for:

→ System type

* If it says "64-bit operating system, x64-based processor" 

 ### You're on AMD64

* If it says "64-bit operating system, ARM-based processor"
  
 ### You're on ARM64

### For Linux Os in the Cloud or WSL on Windows, follow this instructions:

* Linux: Use your distro's package manager

* sudo apt install docker.io
* sudo systemctl start docker
* sudo systemctl enable docker

* Make sure to verify your installation:

→ docker --version
→ docker run hello-world

## 4. Docker Basics

* Command	Description

* docker ps	List running containers
* docker images	List local images
* docker pull	Download image from Docker Hub
* docker run	Start container
* docker stop	Stop container

* docker run -d -p 80:80 nginx

* This runs NGINX in the background and maps port 80.

## 5. Dockerfile: Build Your Own Image

* Create a file called Dockerfile:

### Dockerfile, example:

FROM python:3.10
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]

* Then build and run:

* docker build -t my-python-app .
* docker run -p 5000:5000 my-python-app

## 6. Docker Compose (COMPLETELY Optional, but you should knbow it exist)

* Use Compose for multi-container apps:

version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  db:
    image: postgres
    
* Run it:

* docker-compose up

## What to keep in mind:

* Learn about volumes (persistent data) (You will learn in in our Kubernetes program)

* Explore networks (inter-container communication) (You will learn in in our Kubernetes program)

* Push your images to Docker Hub

## Virtual Machines(VM) VS Containers

| Feature                | Virtual Machines (VMs)                                   | Containers                                         |
|------------------------|---------------------------------------------------------|----------------------------------------------------|
| **Definition**         | Emulates a full computer system with its own OS, running on a hypervisor above the host hardware | Runs applications in isolated environments that share the host OS kernel |
| **OS Usage**           | Each VM has its own complete guest operating system      | Containers share the host OS kernel, no separate OS |
| **Resource Usage**     | Consumes more memory and storage                        | Lightweight, uses less memory and disk space        |
| **Startup Time**       | Slower to boot                                          | Starts up almost instantly                          |
| **Isolation**          | Strong isolation, better hardware emulation             | Process-level isolation, less overhead              |
| **Use Case**           | Good for running different operating systems on one host | Best for microservices, rapid deployment, scaling   |

---
- **VMs:** Each application runs inside its own OS, managed by a hypervisor.
- **Containers:** Applications share the host OS kernel, making them more efficient and faster to start.

**Diagram: Virtual Machines vs Containers**

![image](https://github.com/user-attachments/assets/29c0e35a-83c3-4686-acd8-2edabe182046)


### What is a Kernel?

**Definition:**  

- The kernel is the central component of an operating system, responsible for handling interactions between software and hardware.

**Description:**  
- It manages essential functions such as memory allocation
-  Process scheduling
-  File system operations, and
-  Device input/output. 

### Critical notice

**Applications access hardware resources through the kernel rather than directly for several important reasons:**

- **Safety and Security:** The kernel prevents applications from interfering with each other or the system, protecting data and hardware from unauthorized access or damage.
  
- **Resource Management:** The kernel manages and allocates hardware resources (CPU, memory, devices) efficiently among all running applications.

- **Abstraction:** The kernel provides a consistent interface for applications, so they don’t need to handle hardware differences or complexities.
  
- **Stability:** By controlling hardware access, the kernel helps prevent crashes and system instability caused by faulty or malicious applications.

**The kernel acts as a protective and organizing layer between applications and hardware. Take a look at the diagram below**

![image](https://github.com/user-attachments/assets/54142db8-4d77-4139-920e-1180cb16b792)









## What is a container?

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

Ok, let me make it easy !!!

A container is a bundle of Application, Application libraries required to run your application and the minimum system dependencies.

![Screenshot 2023-02-07 at 7 18 10 PM](https://user-images.githubusercontent.com/43399466/217262726-7cabcb5b-074d-45cc-950e-84f7119e7162.png)



## Containers vs Virtual Machine 

Containers and virtual machines are both technologies used to isolate applications and their dependencies, but they have some key differences:

    1. Resource Utilization: Containers share the host operating system kernel, making them lighter and faster than VMs. VMs have a full-fledged OS and hypervisor, making them more resource-intensive.

    2. Portability: Containers are designed to be portable and can run on any system with a compatible host operating system. VMs are less portable as they need a compatible hypervisor to run.

    3. Security: VMs provide a higher level of security as each VM has its own operating system and can be isolated from the host and other VMs. Containers provide less isolation, as they share the host operating system.

   4.  Management: Managing containers is typically easier than managing VMs, as containers are designed to be lightweight and fast-moving.



## Why are containers lightweight?

Containers are lightweight because they use a technology called containerization, which allows them to share the host operating system's kernel and libraries, while still providing isolation for the application and its dependencies. This results in a smaller footprint compared to traditional virtual machines, as the containers do not need to include a full operating system. Additionally, Docker containers are designed to be minimal, only including what is necessary for the application to run, further reducing their size.

Let's try to understand this with an example:

Below is the screenshot of the official Ubuntu base image you can use for your container. It's just ~ 22 MB, isn't it very small? on the contrary, if you look at the official Ubuntu VM image it will be close to ~ 2.3 GB. So the container base image is almost 100 times less than the VM image.

![Screenshot 2023-02-08 at 3 12 38 PM](https://user-images.githubusercontent.com/43399466/217493284-85411ae0-b283-4475-9729-6b082e35fc7d.png)


To provide a better picture of files and folders that container base images have and files and folders that containers use from the host operating system (not 100 percent accurate -> varies from base image to base image). Refer below.



### Files and Folders in containers base images

```
    /bin: contains binary executable files, such as the ls, cp, and ps commands.

    /sbin: contains system binary executable files, such as the init and shutdown commands.

    /etc: contains configuration files for various system services.

    /lib: contains library files that are used by the binary executables.

    /usr: contains user-related files and utilities, such as applications, libraries, and documentation.

    /var: contains variable data, such as log files, spool files, and temporary files.

    /root: is the home directory of the root user.
```



### Files and Folders that containers use from the host operating system

```
    The host's file system: Docker containers can access the host file system using bind mounts, which allow the container to read and write files in the host file system.

    Networking stack: The host's networking stack is used to provide network connectivity to the container. Docker containers can be connected to the host's network directly or through a virtual network.

    System calls: The host's kernel handles system calls from the container, which is how the container accesses the host's resources, such as CPU, memory, and I/O.

    Namespaces: Docker containers use Linux namespaces to create isolated environments for the container's processes. Namespaces provide isolation for resources such as the file system, process ID, and network.

    Control groups (cgroups): Docker containers use cgroups to limit and control the number of resources, such as CPU, memory, and I/O, that a container can access.
    
```

It's important to note that while a container uses resources from the host operating system, it is still isolated from the host and other containers, so changes to the container do not affect the host or other containers.

**Note:** There are multiple ways to reduce your VM image size as well, but I am just talking about the default for easy comparison and understanding.

so, in a nutshell, container-based images are typically smaller compared to VM images because they are designed to be minimalist and only contain the necessary components for running a specific application or service. VMs, on the other hand, emulate an entire operating system, including all its libraries, utilities, and system files, resulting in a much larger size. 

I hope it is now very clear why containers are lightweight in nature.



## Docker


### What is Docker ?

Docker is a containerization platform that provides an easy way to containerize your applications, which means, using Docker you can build container images, run the images to create containers, and also push these containers to container registries such as DockerHub, Quay.io, and so on.

In simple words, you can understand `containerization is a concept or technology` and `Docker Implements Containerization`.


### Docker Architecture?

![image](https://user-images.githubusercontent.com/43399466/217507877-212d3a60-143a-4a1d-ab79-4bb615cb4622.png)

The above picture, clearly indicates that Docker Deamon is the brain of Docker. If Docker Deamon is killed and stops working for some reason, Docker is brain-dead :p (sarcasm intended).

### Docker LifeCycle 

We can use the above Image as a reference to understand the lifecycle of Docker.

There are three important things,

1. docker build -> builds docker images from Dockerfile
2. docker run   -> runs container from docker images
3. docker push  -> push the container image to public/private registries to share the docker images.

![Screenshot 2023-02-08 at 4 32 13 PM](https://user-images.githubusercontent.com/43399466/217511949-81f897b2-70ee-41d1-b229-38d0572c54c7.png)



### Understanding the terminology (Inspired by Docker Docs)


#### Docker daemon

The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.


#### Docker client

The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.


#### Docker Desktop

Docker Desktop is an easy-to-install application for your Mac, Windows, or Linux environment that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (dockerd), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper. For more information, see Docker Desktop.


#### Docker registries

A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your private registry.

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.
Docker objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.


#### Dockerfile

Dockerfile is a file where you provide the steps to build your Docker Image. 


#### Images

An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the Ubuntu image but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast when compared to other virtualization technologies.



## INSTALL DOCKER

Very detailed instructions to install Docker are provided in the below link

https://docs.docker.com/get-docker/

For Demo, 

You can create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

```
sudo apt update
sudo apt install docker.io -y
```


### Start Docker and Grant Access

A very common mistake that many beginners make is, After they install docker using the sudo access, they miss the step to Start the Docker daemon and grant access to the user they want to use to interact with docker and run docker commands.

Always ensure the docker daemon is up and running.

An easy way to verify your Docker installation is by running the below command

```
docker run hello-world
```

If the output says:

```
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

This can mean two things, 
1. Docker deamon is not running.
2. Your user does not have access to run docker commands.


### Start Docker daemon

You use the below command to verify if the docker daemon is started and Active

```
sudo systemctl status docker
```

If you notice that the docker daemon is not running, you can start the daemon using the below command

```
sudo systemctl start docker
```


### Grant Access to your user to run docker commands

To grant access to your user to run the docker command, you should add the user to the Docker Linux group. A Docker group is created by default when Docker is installed.

```
sudo usermod -aG docker ubuntu
```

In the above command `ubuntu` is the name of the user, you can change the username appropriately.

**NOTE:** : You need to logout and login back for the changes to be reflected.


### Docker is Installed, up and running 🥳🥳

Use the same command again, to verify that docker is up and running.

```
docker run hello-world
```

The output should look like this:

```
....
....
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
...
```


## Great Job, Now start with the examples folder to write your first Dockerfile and move to the next examples. Happy Learning :)

### Clone this repository and "cd" to the "example folder/directory"

```
https://github.com/rayeeta/Docker.git
cd  examples
```

### Login to Docker [Create an account with https://hub.docker.com/]

```
docker login
```

```
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: brightmindtech
Password: xyz123
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

### Build your first Docker Image

You need to change the username accordingly in the below command

```
docker build -t brightmindtech/docker:latest .
```

Output of the above command

```
    Sending build context to Docker daemon  992.8kB
    Step 1/6 : FROM ubuntu:latest
    latest: Pulling from library/ubuntu
    677076032cca: Pull complete
    Digest: sha256:9a0bdde4188b896a372804be2384015e90e3f84906b750c1a53539b585fbbe7f
    Status: Downloaded newer image for ubuntu:latest
     ---> 58db3edaf2be
    Step 2/6 : WORKDIR /app
     ---> Running in 630f5e4db7d3
    Removing intermediate container 630f5e4db7d3
     ---> 6b1d9f654263
    Step 3/6 : COPY . /app
     ---> 984edffabc23
    Step 4/6 : RUN apt-get update && apt-get install -y python3 python3-pip
     ---> Running in a558acdc9b03
    Step 5/6 : ENV NAME World
     ---> Running in 733207001f2e
    Removing intermediate container 733207001f2e
     ---> 94128cf6be21
    Step 6/6 : CMD ["python3", "app.py"]
     ---> Running in 5d60ad3a59ff
    Removing intermediate container 5d60ad3a59ff
     ---> 960d37536dcd
    Successfully built 960d37536dcd
    Successfully tagged abhishekf5/my-first-docker-image:latest
```

### Verify Docker Image is created

```
docker images
```

Output 

```
REPOSITORY                         TAG       IMAGE ID       CREATED          SIZE
brightmindtech/docker              latest    3cc5d1d1de8f   About a minute ago   802MB
ubuntu                             latest    58db3edaf2be   13 days ago      77.8MB
hello-world                        latest    feb5d9fea6a5   16 months ago    13.3kB
```

### Run your First Docker Container

```
docker run -it brightmindtech/docker
```

Output

```
Hello World
```

### Push the Image to DockerHub and share it with the world

```
docker push brightmindtech/docker
```

Output

```
Using default tag: latest
The push refers to a repository [docker.io/brightmindtech/docker]
896818320e80: Pushed
b8088c305a52: Pushed
69dd4ccec1a0: Pushed
c5ff2d88f679: Mounted from library/ubuntu
latest: digest: sha256:6e49841ad9e720a7baedcd41f9b666fcd7b583151d0763fe78101bb8221b1d88 size: 1157
```

### You must be feeling like a champ already right 

## If you found this repo useful, give it a STAR 🌠


