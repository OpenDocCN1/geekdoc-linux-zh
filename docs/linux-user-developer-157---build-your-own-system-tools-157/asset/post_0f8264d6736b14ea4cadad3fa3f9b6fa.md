
## Launch your first Docker container

![](img/e7f197876caa0b235fb5da2d16a578ea_43_0.png)

**Nithish Tiwari**
is a software developer by profession and an open-source enthusiast by heart. As well as writing for leading open source magazines, he helps firms set up and use open source software for their business needs

## Resources
- Docker
- [docker.com](docker.com)

## Containers are the coolest tech right now — everyone wants to run their software in Docker containers

**Linux containers provide a simple way to run applications in an isolated environment**. Applications are bundled with the libraries and other required binaries, and then run in an isolated manner via containers. Containers have been around for some time – projects like LXC, OpenVZ and so on were released around 2005 – but things really changed with Docker. Not only did containerisation go mainstream among users, but more businesses are now using Docker for their production systems.

Before we jump onto Docker and its basics, let’s try to get some clarity over one of the basic questions – the difference between containerisation and virtualisation. Virtualisation involves creating a target kernel on the host machine, so you will have as many kernels as virtual machines on your system. Now this may be required in some scenarios, but having a separate kernel is generally a big overhead. Containers, on the other hand, just isolate the runtime of the application you need to run, but at the lower layer, all the containers on your machine use the same kernel – this makes them lightweight and very fast to deploy. However, this also means that all of the containers are tied to one OS and you don’t have the freedom to run apps for different operating systems on one host. You can install Docker on any OS, though.

## 01 Docker architecture

Docker is based on client-server architecture: Docker client accepts the commands from users and then talks to the Docker daemon that does the core tasks such as building, running and even distributing the Docker containers. Note that Docker client and the daemon communicate via RESTful APIs, therefore the communication is asynchronous. Also, this makes the system loosely coupled: it is possible to have the client and daemon run on the same system, or different systems, based on your requirements. However, it is important to understand that the Docker daemon should run on the host machine: for example, the machine where containers are supposed to run and that the client runs on the system being used as the interface, because the Docker client is the primary interface to Docker for the user.

## 02 Docker components

Apart from the server and the client, there are three other components of Docker that are important to clarify in order to understand its overall working. These are Docker images, containers and registries.

```
n@lakh:nithish-VirtualBox:~ $ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from hello-world
51125ac580d: Pull complete
5f70cb1826b2: Already exists
hello-world:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.
Digest: sha256:af506d50c957eeccd1f99f08778679686f3284c76a3886158182bed336df4ccb3721eae52
Status: Downloaded newer image for hello-world:latest
Hello from Docker.
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
1. The Docker client contacted the Docker daemon.
2. The Docker daemon pulled the 'hello-world' image from the Docker Hub.
3. The Docker daemon created a new container from that image which runs the executable that produces the output you are currently reading.
4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.
To try something more ambitious, you can run an Ubuntu container with:
  $ docker run -it ubuntu bash
Share images, automate workflows, and more with a free Docker Hub account:  https://hub.docker.com
For more examples and ideas, visit: https://docs.docker.com/useguide/
n@lakh:nithish-VirtualBox:~ $
```

**Right** A Docker container can be created using command **docker run** `<image-name>`

![](img/e7f197876caa0b235fb5da2d16a578ea_44_0.png)

A Docker image is a read-only template in a predefined format that the Docker daemon can run – so any application that you want to run as a Docker container first needs to be made as a Docker image. Images generally contain the base operating system, the libraries and binaries required for the application to be run, and obviously the application itself. Docker provides simple ways to build new images or update old ones. You can also download images that others have built via the Docker registry.

A Docker registry is a storage and content delivery system, holding Docker images. You can interact with a registry using the `push` and `pull` commands. A registry can be private or public depending on your requirements. Docker also provides the official Docker registry as a SaaS (software-as-a-service) platform, called the Docker hub. Docker hub can be thought of as a huge repository of Docker images that are free to be downloaded and run. You can also create your own image and push it to the Docker hub.

## 03 Docker containers

Probably the most important component of the Docker ecosystem, containers can be thought of as running instances of Docker images. The image (which is going to be run as container) tells Docker what the container holds, what process to run when the container is launched and a variety of other configuration data. As mentioned in the previous step, images are read-only, but when the image being executed (ie converted to a container), Docker creates a read-write layer on top of the image so that applications can run normally. Later, when the container is stopped, the top read-write layer is lost and the image is available as it is.

> “Containers isolate the runtime of the application you need to run, but all the containers use the same kernel”

Docker provides commands such as `run`, `start`, `stop`, `ps`, `rm` and so on, in order to interact with containers. You can type, `docker <command-name> --help` to get the help that’s related to `<command-name>`.

Now that you have a clear idea of the important components and how they work together in Docker, let’s install Docker and see the components in action. Note that I have used Ubuntu 14.04 as the base system for installation and demo purposes.

## 04 Installation

Docker installation is pretty straightforward. Firstly, log in to your system and check if you have wget installed, using the which `wget` command. If it isn’t installed, run the commands `sudo apt-get update` and `sudo apt-get install wget`. After successfully installing wget, let’s install Docker. Run the command `wget -qO- https://get.docker.com/ | sh`. The system prompts you for the root password, then downloads and installs Docker and its dependencies. To verify if Docker is successfully installed, you can run the command `sudo docker run hello-world`. This will download a test image and run it in a container on your system. If you take a close look at the output on the opposite page, you’ll see the steps Docker followed to generate the message. This gives an idea of how components interact in Docker.

## Docker Swarm

Docker swarm lets you create a native cluster for Docker – you can create a pool of Docker hosts. And since Docker Swarm serves the standard Docker API, any tool that already communicates with a Docker daemon can use Swarm to transparently scale to multiple hosts.

Though Docker Swarm is in the initial stages now, changes are expected to occur in how it will handle the backend.

![](img/e7f197876caa0b235fb5da2d16a578ea_45_0.png)

![](img/e7f197876caa0b235fb5da2d16a578ea_45_1.png)

## 05 Create a Docker group

The Docker installation is successful and we have verified that using the **docker run** command, however, you may have noticed that we need to add **sudo** before running any Docker command, and therefore every time you run a Docker command in a new terminal, you need to enter the root password. This is because the Docker daemon binds to a Unix socket instead of a TCP port and the root user owns the Unix socket. To avoid using **sudo**, you can create a group called docker and add users to it; users here means the users exposed to run Docker commands. Now, when the Docker daemon starts, it sets the ownership of the Unix socket read/write to all users in the docker group.

To create the group and add a user, log in to Ubuntu as the user who needs to run Docker commands. Then run the command **sudo usermod -aG docker username**—don’t forget to replace username with the actual username. Then log out of the system and log in again. Verify if Docker commands now work without **sudo** by typing **docker run hello-world**. If this works successfully, the group mechanism we added works. Now there is no need to enter the password every time you want to run a Docker command.

## 06 Base image

As discussed, Docker containers are created using images. An image can be basic, with nothing but the operating system fundamentals, or it can consist of a sophisticated pre-built application stack ready for launch. All this is possible because of Docker’s layered approach to images. This provides an extremely powerful abstraction for building up application containers, where one step serves as the base for the next one, ie new tools, applications, content, patches and more, which form additional layers on the foundation (the base image).

A base image is the one without any further layers below; this is the most basic form of a Docker image that has just the operating system. The Docker hub has base images for all of the major Linux distros, but you are also free to create your own base image. To do so, you can use the scratch repository in the Docker hub, just use **FROM scratch** in the Dockerfile (more on Dockerfiles in the next part). Another way is using the **tar** command. Type

```bash
$ sudo debootstrap trusty trusty > /dev/null
$ sudo tar -C trusty -c . | sudo docker import - trusty
```

Here, the above command creates a tar file of the current directory and outputs it to STDOUT, while **docker import** takes it from STDIN and then creates a base image called trusty from it.

## 07 Dockerfile

As we saw in the previous step, creating a base image doesn’t involve many Dockerfile instructions. However, as you add more and more layers to the base image, knowledge of Dockerfile instructions will become very important to you.

Let’s start with its definition. A Dockerfile is a script composed of various commands (instructions) and arguments listed successively to automatically perform actions on a base image in order to create a new one. Creating a Dockerfile is as simple as listing the instructions one by one in a plain text file (named Dockerfile) and then calling the **docker build** command (in the same directory) to create the image. Typical Dockerfile syntax looks like this:

```bash
# Print 'Hello World'
RUN echo "Hello World"
```

Dockerfile consists of two types of lines: comments starting with # and commands (with arguments) starting with an instruction (written in capital letters). Also, it is worth mentioning here that a Dockerfile should always start with the **FROM** instruction, meant to indicate the base image.

![](img/e7f197876caa0b235fb5da2d16a578ea_45_2.png)

## 08 Dockerfile instructions

There are about a dozen different commands that a Dockerfile can use to build a Docker image. Let’s look at a few of the important Dockerfile instructions and their usage:

**ADD** – The ADD command needs two arguments: a source and a destination. It copies files from the source (on the host) into the container’s OS filesystem at the set destination. It can also take a URL, as the source. Example:

```bash
# ADD Usage
ADD /my_source_path /my_docker_dest_path
```

**ENV** – The ENV instruction is used to set the environment variables (one or more). These variables consist of key-value pairs that can be accessed within the container by scripts and applications alike. This is similar to environment variables set in Windows systems.

```bash
# ENV Usage
ENV Default 6
```

**FROM** – This directive is probably the most crucial amongst all the other listed here. It defines the base image to use to start the build process. It can be any image, including the ones you have created previously. Also, it should be the first instruction in the Dockerfile.

```bash
# FROM Usage
FROM ubuntu
```
