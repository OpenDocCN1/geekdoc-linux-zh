# # Unpacking the Kernel Source Code

Until now, you've probably seen most packages come in files with file extension .rpm. You've accustomed to using one of the tools that came with the system (such as gLinux or gNorpm) to install the package. Kernel source code is a little different and requires more user participation. Let's go through the steps to unpack the kernel.

You'll start by removing the existing tree so that you can revert back to it if the new version doesn't work out. Once the old tree is safe, you'll create a new directory for the version of Linux you're going to unpack. Only then are you ready to unpack it. Overall, it's really a straightforward process.

For the remainder of this chapter, we'll assume you are working out of the /usr/src directory. This is the traditional location of the kernel source tree.

Save the Current Source Tree. Before unpacking the new source tree, save and rename the current one. In the directory tree in /usr/src, you'll see a directory called linux.

```
```bash
[root@ford src]# ls -l
total 2
drwxr-xr-x 3 root     root      1024 Jun 10 09:33 linux
-rw-r----- 1 root     root     11292345 Jun  6 21:34 linux-2.2.10.tar.gz
drwxr-xr-x  7 root     root      1024 Jun 10 09:36 redevat
[root@ford src]#
```
```

In the linux directory is the current source tree. (Note that some distributions, including Red Hat, do not install the entire source tree by default. Only the necessary files for development purposes are installed.) The safe path to upgrading is to rename the existing tree with a suffix indicating its associated version number. Find out the current version number with the uname command, like so:

```
```bash
[root@ford src]# uname -r
2.2.5-15
[root@ford src]#
```
```

In this case, we want to rename the linux directory linux-2.2.5-15.

```
```bash
[root@ford src]# mv linux linux-2.2.5-15
```
```

> > **NOTE:** If someone has previously updated the running kernel, it's possible that the running kernel does not match the source in /usr/src/linux. In this situation, you can find out the version of the kernel by looking at the file Makefile in the /usr/src/linux directory. At the top of the file you'll see three identifying values: version, patch level, and sublevel. If version=2, patch-level=3, and sublevel=30, you have kernel version 2.3.30.