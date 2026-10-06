# 750  Linux Administration: A Beginner's Guide

Some terms and concepts are unique and commonly used in the Docker world. Here, we outline and explain some of these concepts:

+   - Docker images form the building blocks for the Docker ecosystem. They are the read-only blueprints from which containers are created. When Docker runs a container from an image, it adds a read-write layer on top of the image.
- Docker containers are the actual workhorses created from Docker images to run the applications.
- Registry This refers to any repository or source of Docker images. The default-main registry is a public repository called Docker Hub, which contains thousands of images contributed by various open source projects, companies, and individuals. The registry can be accessed via its web interface (https://hub.docker.com) or via various client tools.
- Docker Host Host system on which Docker application is installed.
- Docker daemon The daemon is responsible for managing the containers on the Docker where it is running. It receives commands from the Docker client.
- Docker client Consists of the user-land tools and applications that issue commands to the daemon to perform container-related management.
- dockerfile This is a type of configuration file that describes the steps needed to assemble an image.

# Docker Installation and Startup

On our sample Fedora server, we'll walk through installing Docker, starting the daemon service, and enabling it for future automatic startups in the following steps:

+   - While logged in as root, use dnf to install Docker by running
```[root@fedora-server ~]## dnf -y install docker```
- After the software has been successfully installed, use systemctl to check the status of the docker:
```[root@fedora-server ~]## systemctl is-enabled docker```
- If the output shows that the service is disabled from automatic startup, we can enable it by running
```[root@fedora-server ~]## systemctl enable docker```
- Next, start the docker daemon service:
```[root@fedora-server ~]## systemctl start docker```

If the daemon fails to start on Red Hat-like distros with Btrfs-formatted file system running SELinux in enforcing mode, you can try working around this by removing --selinux-enabled from the OPTIONS line in the /etc/sysconfig/docker file. Save your changes to the file and then try to start the docker again.