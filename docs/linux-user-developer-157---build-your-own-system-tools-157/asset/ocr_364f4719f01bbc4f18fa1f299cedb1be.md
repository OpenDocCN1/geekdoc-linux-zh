# # Launch your first Docker container

![](bbox=[0.06, 0.285, 0.18, 0.375])

**Nithish Tiwari**
is a software developer by
profession and an open-source enthusiast by
heart. As well as writing
for leading open source
magazines, he helps
firms set up and use open
source software for their
business needs

# ## Resources

+   - Docker
+     [docker.com](docker.com)

# ## Containers are the coolest tech right now — everyone wants to run their software in Docker containers

**Linux containers provide a simple way to run applications in an isolated environment**. Applications are bundled with the libraries and other required binaries, and then run in an isolated manner via containers. Containers have been around for some time – projects like LXC, OpenVZ and so on were released around 2005 – but things really changed with Docker. Not only did containerisation go mainstream among users, but more businesses are now using Docker for their production systems.

Before we jump onto Docker and its basics, let’s try to get some clarity over one of the basic questions – the difference between containerisation and virtualisation. Virtualisation involves creating a target kernel on the host machine, so you will have as many kernels as virtual machines on your system. Now this may be required in some scenarios, but having a separate kernel is generally a big overhead. Containers, on the other hand, just isolate the runtime of the application you need to run, but at the lower layer, all the containers on your machine use the same kernel – this makes them lightweight and very fast to deploy. However, this also means that all of the containers are tied to one OS and you don’t have the freedom to run apps for different operating systems on one host. You can install Docker on any OS, though.

# 01 Docker architecture

Docker is based on client-server architecture: Docker client accepts the commands from users and then talks to the Docker daemon that does the core tasks such as building, running and even distributing the Docker containers. Note that Docker client and the daemon communicate via RESTful APIs, therefore the communication is asynchronous. Also, this makes the system loosely coupled: it is possible to have the client and daemon run on the same system, or different systems, based on your requirements. However, it is important to understand that the Docker daemon should run on the host machine: for example, the machine where containers are supposed to run and that the client runs on the system being used as the interface, because the Docker client is the primary interface to Docker for the user.

# 02 Docker components

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