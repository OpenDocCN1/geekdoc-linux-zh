## Compiling a kernel takes a lot of disk space

tip Make sure you have enough disk space before you compile a kernel. Once you compile a default kernel, it occupies approximately 3.5 gigabytes. This disk space must be available on the file- system in which you compile the kernel.

# # Downloading the Kernel Source Code

This section describes two ways to download kernel source code on the local system: **aptitude** (or Synaptic, page 133) and **git**. If you want to download code that has not been customized (patched) by Ubuntu, visit kernel.org or see the section on git.

# ## aptitude: Downloading and Installing the Kernel Source Code

The easiest way to download and install the updated kernel source code for the most recently released version of the Ubuntu kernel is to use **aptitude**. The following commands make sure that the package index is up-to-date and download the linux-source package. The **dpkg postinst** script puts the compressed source code in **/usr/src/linux-source\***:

```
$ sudo aptitude update
...
$ sudo aptitude install linux-source
...
The following NEW packages will be installed:
  linux-source linux-source-2.6.32{a}
...
$ ls -l /usr/src/linux-source*
-rw-r--- 1 root root 65726108 2010-04-09 18:23 /usr/src/linux-source-2.6.32.tar.bz2
```

Because **/usr/src** is associated with the **src** group, if you are a member of this group (page 492), you can extract and build kernels in the **/usr/src** directory. Otherwise, you can unpack the kernel in any directory you have write access to.

## Do not work with root privileges

cation You do not need to—and should not—work as a user with **root** privileges for any portion of config-uring or building the kernel except for installation (the last step). The kernel **README** file says, “Don’t take the name of root in vain.” As long as you are a member of the **src** group, you can down- load, configure, and compile the kernel in a directory under **/usr/src** without working with **root** privileges.

You can add a user to the **src** group using **usermod**. The following command adds Max to the **src** group so he can work in **/usr/src**. Max must log out and log in again to have the system recognize him as a member of the **src** group.

$ sudo usermod --append --groups src max