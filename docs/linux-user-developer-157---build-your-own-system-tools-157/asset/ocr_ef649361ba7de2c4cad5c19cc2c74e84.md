![](bbox=[0.08, 0.04, 0.45, 0.08])

![](bbox=[0.06, 0.16, 0.17, 0.43])

# 05  Create a Docker group

The Docker installation is successful and we have verified that using the **docker run** command, however, you may have noticed that we need to add **sudo** before running any Docker command, and therefore every time you run a Docker command in a new terminal, you need to enter the root password. This is because the Docker daemon binds to a Unix socket instead of a TCP port and the root user owns the Unix socket. To avoid using **sudo**, you can create a group called docker and add users to it; users here means the users exposed to run Docker commands. Now, when the Docker daemon starts, it sets the ownership of the Unix socket read/write to all users in the docker group.

To create the group and add a user, log in to Ubuntu as the user who needs to run Docker commands. Then run the command **sudo usermod -aG docker username**—don’t forget to replace username with the actual username. Then log out of the system and log in again. Verify if Docker commands now work without **sudo** by typing **docker run hello-world**. If this works successfully, the group mechanism we added works. Now there is no need to enter the password every time you want to run a Docker command.

# 06  Base image

As discussed, Docker containers are created using images. An image can be basic, with nothing but the operating system fundamentals, or it can consist of a sophisticated pre-built application stack ready for launch. All this is possible because of Docker’s layered approach to images. This provides an extremely powerful abstraction for building up application containers, where one step serves as the base for the next one, ie new tools, applications, content, patches and more, which form additional layers on the foundation (the base image).

A base image is the one without any further layers below; this is the most basic form of a Docker image that has just the operating system. The Docker hub has base images for all of the major Linux distros, but you are also free to create your own base image. To do so, you can use the scratch repository in the Docker hub, just use **FROM scratch** in the Dockerfile (more on Dockerfiles in the next part). Another way is using the **tar** command. Type

```
```
$ sudo debootstrap trusty trusty > /dev/null
$ sudo tar -C trusty -c . | sudo docker import - trusty
```
```

Here, the above command creates a tar file of the current directory and outputs it to STDOUT, while **docker import** takes it from STDIN and then creates a base image called trusty from it.

# 07  Dockerfile

As we saw in the previous step, creating a base image doesn’t involve many Dockerfile instructions. However, as you add more and more layers to the base image, knowledge of Dockerfile instructions will become very important to you.

Let’s start with its definition. A Dockerfile is a script composed of various commands (instructions) and arguments listed successively to automatically perform actions on a base image in order to create a new one. Creating a Dockerfile is as simple as listing the instructions one by one in a plain text file (named Dockerfile) and then calling the **docker build** command (in the same directory) to create the image. Typical Dockerfile syntax looks like this:

```
```bash
# Print 'Hello World'
RUN echo "Hello World"
```
```

Dockerfile consists of two types of lines: comments starting with # and commands (with arguments) starting with an instruction (written in capital letters). Also, it is worth mentioning here that a Dockerfile should always start with the **FROM** instruction, meant to indicate the base image.

![](bbox=[0.55, 0.43, 0.92, 0.6])

# 08  Dockerfile instructions

There are about a dozen different commands that a Dockerfile can use to build a Docker image. Let’s look at a few of the important Dockerfile instructions and their usage:

**ADD** – The ADD command needs two arguments: a source and a destination. It copies files from the source (on the host) into the container’s OS filesystem at the set destination. It can also take a URL, as the source. Example:

```
```bash
# ADD Usage
ADD /my_source_path /my_docker_dest_path
```
```

**ENV** – The ENV instruction is used to set the environment variables (one or more). These variables consist of key-value pairs that can be accessed within the container by scripts and applications alike. This is similar to environment variables set in Windows systems.

```
```bash
# ENV Usage
ENV Default 6
```
```

**FROM** – This directive is probably the most crucial amongst all the other listed here. It defines the base image to use to start the build process. It can be any image, including the ones you have created previously. Also, it should be the first instruction in the Dockerfile.

```
```bash
# FROM Usage
FROM ubuntu
```
```

46