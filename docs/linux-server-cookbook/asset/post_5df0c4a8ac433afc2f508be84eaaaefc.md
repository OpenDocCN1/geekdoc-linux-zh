
## Docker

The project **Docker** was a revolution in the IT Industry because it made it easier to implement **Containers**. Traditionally, **Virtualization** was a fresh air of change for the companies to reduce costs and complexity in their infrastructures. However, it did not solve all the problems related to the development of the applications and the systems that were deployed. The introduction of the **Containers** in the development life-cycle helped *Developers* to be able to perform their tasks without the need for the creation of specific environments. Using the solution provided by **Docker**, they were able to use their own workstation or a server provided by the *IT team* to run their own applications inside **Containers** and generate **Images** that would be promoted to a different environment (such as *testing, pre-production, or production*).

The popularity and implementation of **Containers** also helped the developers be able to isolate their applications and create *Microservices*, as described previously. This made the development team more flexible and less dependent on the infrastructure team. A new role named *DevOps* appeared with the implementation of **Containers** and new practices focused on the *Cloud*.

**Docker** is based on a *Daemon* running, which will monitor the status of the *Containers* running in the system. This further allows it to start or stop the containers, among other tasks. **Docker** is available on Linux, Windows, and Mac systems. **Docker** has two main products:

-   * **Docker engine**: is an open-source containerization technology for building and containerizing your applications.
-   * **Docker desktop**: is an application for MacOS and Windows machines for the building and sharing of containerized applications and microservices.

The steps for **Docker Engine** installation in different Linux distributions are detailed in the following link: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/). After the installation, a service called *docker.service* is available in the system to start, stop, or obtain status. When the **Docker Daemon** is started, it is possible to use the command *docker* to perform different tasks with containers and images.

### Run the first container

The first command is to run a sample container. Refer to the *figure 13.5*:

```
root@ubuntu:~# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest: sha256:e18f0a777aefabe0474671ab3ec3eed0541447c951ab1a6f352a06974245fe7
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
1. The Docker client contacted the Docker daemon.
2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
   (amd64)
3. The Docker daemon created a new container from that image which runs the
   executable that produces the output you are currently reading.
4. The Docker daemon streamed that output to the Docker client, which sent it
   to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
$ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
https://hub.docker.com/

For more examples and ideas, visit:
https://docs.docker.com/get-started/
```

*Figure 13.5: First container execution with Docker*

### Obtain information about client and server

The command **docker** allows, as the first argument, the word *run* to execute a container. A **Container** is based on an **Image**, and the argument *hello-world* indicates the image to be used. The first line of the output indicates that the **Image** was not downloaded previously. The **Image** is downloaded automatically, and then the **Container** is created using it. The rest of the output comes from the execution. This container will be automatically stopped after showing the message.

The command **docker** **info** shows information about the client and the server. The following code shows an example output:

```
root@ubuntu:~# docker info
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Docker Buildx (Docker Inc., v0.9.1-docker)
  compose: Docker Compose (Docker Inc., v2.12.2)
  scan: Docker Scan (Docker Inc., v0.21.0)

Server:
Containers: 1
Running: 0
Paused: 0
Stopped: 1
Images: 1
Server Version: 20.10.21
Storage Driver: overlay2
Backing Filesystem: extfs
(omitted)
Logging Driver: json-file
Cgroup Driver: systemd
Cgroup Version: 2
Plugins:
Volume: local
Network: bridge host ipvlan macvlan null overlay
Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
Swarm: inactive
Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 1c90a442489720eec95342e1789ee8a5e1b9536f
runc version: v1.1.4-0-g5fd4c4d
init version: de40ad0
(omitted)
Kernel Version: 5.15.0-52-generic
Operating System: Ubuntu 22.04.1 LTS
OSType: linux
Architecture: x86_64
CPUs: 2
Total Memory: 3.832GiB
Name: ubuntu
ID: SEHR:RO0N:MTHA:DFD2:A4S3:56BX:IDC6:NP34:SZ03:7WYD:XYC4:3S5Z
Docker Root Dir: /var/lib/docker
Debug Mode: false
Registry: https://index.docker.io/v1/
Labels:
Experimental: false

Insecure Registries:
127.0.0.0/8

Live Restore Enabled: false
```

The preceding output provides useful information about the **Docker Client** and the **Docker Daemon**:

-   The client has enabled the plugins: **app** (used to run containers), **buildx** (used to generate images), **compose** (used for orchestration), and **scan** (to check vulnerabilities on local images).
-   The server has one container and is stopped (the previous example executed); it uses the storage driver called **overlay2** and the driver **json-file** for the logging.
-   The output lists the available plugins for volumes, network, and logging.
-   The server uses the runtime named **containerd**. The data will be stored in the directory `/var/lib/docker`.
-   The output shows information about the system where it is running, such as the distribution version, **Kernel** version, available CPUs, and memory.

### Operate with containers

The argument **ps** for the command `docker` will list the **Containers** running in the system. Adding the option `-a` will display the *containers*, which are stopped. `Figure 13.6` shows an output example:

![](img/863afa537de4eed7deb11978bfbfa90e_444_0.png)

The previous output includes the following columns:

-   **Container ID**: When a *container* is created, an auto-generated **ID** is assigned to it. The length is 64, but the output shows the first 12 characters.
-   **Image**: The *image* used to run the *container*.
-   **Command**: The *command* executed inside of the container.
-   **Created**: When the container was created.
-   **Status**: The status of the container; if it was exited, it will indicate when it was stopped, and the status (0 indicates the *container* finished correctly).
-   **Ports**: Forwarded ports to access the service offered by the *container*. In the previous example, no ports were exposed.

