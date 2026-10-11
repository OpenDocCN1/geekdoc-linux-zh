# Listing 3: Starting a Container

```
### Current version
$ docker run -it ubuntu
### Ubuntu 20.04
$ docker run -it ubuntu:20.04
### Ubuntu 16.04
$ docker run -it ubuntu:16.04
```

If you are new to containers, the terms “image” and “container” might be confusing. An image is essentially a collection of files, supplemented by various metadata, such as the computer architecture or specifications for environment variables. It only acts as a template for creating a container. When you run the `docker run <image>` command, Docker creates a container from the specified image file. To do this, the tool unpacks the image. You will find the files in a subfolder of /var/lib/docker/overlay2/.

Docker then launches a program from that folder, pretending that the folder is the root filesystem. The program cannot access files located further up in the filesystem, which protects your normal Linux system against manipulation attempts from inside the container. Besides being locked into a subfolder, far more happens. Among other things, the container has its own network settings, which are independent of the host system.

You can use a single image file to create multiple containers in which separate processes then run. The containers change at runtime because you can delete, recreate, or edit files in them. If you are looking for an analogy for the difference between images and containers: Compared with virtualizers such as VMware and VirtualBox, an image would correspond to a virtual appliance, while the container would correspond to the individual VM.

# Disposable Containers

Containers (unlike VMs) are often used just once. In this case a single command runs the container, and Docker immediately deletes it afterwards.

# Listing 4: In the Container

```
01 esser@percent:~$ docker run -it ubuntu
02 root@4eac4c755505:/# ps
03
04  PID TTY      TIME CMD
05  1 pts/0    00:00:00 bash
06  9 pts/0    00:00:00 ps
07 root@4eac4c755505:/# grep PRETTY /etc/os-release
08 PRETTY_NAME="Ubuntu 22.04.1 LTS"
```

# Listing 5: Command Call

```
$ docker run --rm fedora grep PRETTY /etc/os-release PRETTY_NAME="Fedora Linux 38 (Container Image)"
```

Docker comes with a `--rm` option, which automates the delete process.

This wasteful use of containers is possible (and makes sense) because creating and deleting containers is virtually effortless. It is only when you first launch a container that you need to obtain the matching image, typically from Docker Hub [6]. On all subsequent launches, it will already exist in Docker’s local cache directory.

Because containers are often short-lived, it has become common practice to store configuration files and anything else that you want keep outside the container. To do this, you can either make part of the normal filesystem available in the container or create special container volumes.

# Ubuntu Versions

You can use the commands in Listing 3 to create containers with different versions of Ubuntu. Each of these commands creates a container from an Ubuntu image and starts a Bash shell in it. The options -i (interactive) and -t (terminal) tell the container to run in interactive mode with a virtual terminal, so you can control it from the current terminal window. Without these options the container would start in the background.

At the root prompt, you can see that you have administrator privileges in the container (Listing 4, lines 2 to 5). In the shell you can now enter commands in the usual way (lines 2 and 6). If you use external programs for this, you need to start the versions from the container. To find out which distribution version is running in the container, you can look for the /etc/os-release, /etc/debian_version, or /etc/redhat-release files (line 6).

If you already know when starting the container that you do not need a shell, but simply want to execute a specific command, you append it after the image name in the call (Listing 5). Simply omit the -i and -t options if interactive use is not required. Figure 2 shows how to launch containers with different versions of Ubuntu. To do this, simply append a colon and the desired version to the image name (such as ubuntu:16.04).

> You cannot use the Docker tool to find out which versions are available, but you can get this information from the Docker Hub page [6]. Use the search function there, select the appropriate image from the matches, and then switch to the Tags tab.