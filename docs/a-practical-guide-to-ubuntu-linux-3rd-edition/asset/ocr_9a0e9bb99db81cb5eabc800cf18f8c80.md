The **sysctl** utility modifies kernel parameters while the system is running. This utility takes advantage of the facilities of /proc/sys, which defines the parameters that **sysctl** can modify.

The command `sysctl -a` displays a complete list of **sysctl** parameters. An example of displaying and changing the **domainname** kernel parameter follows. The quotation marks are not required in this example, but you must quote any characters that would otherwise be interpreted by the shell.

```
```
$ /sbin/sysctl kernel.domainname
kernel.domainname = tcorp.com
$ sudo /sbin/sysctl -w kernel.domainname="example.com"
kernel.domainname = example.com
$ /sbin/sysctl kernel.domainname
kernel.domainname = example.com
```
```

# Have the installation CD/DVD handy when you build a new kernel

When you build a new Linux kernel to install a new version or to change the configuration of the existing version, make sure you have the installation CD/DVD handy. This disk allows you to reboot the system, even when you have destroyed the system software completely. Having this CD/DVD available can mean the difference between momentary panic and a full-scale nervous breakdown.

Before you can start building a new kernel, you must download, install, and clean the source code. You also need to build a configuration file that describes the new kernel you want to build. This chapter describes the steps involved in completing these tasks.

# PREREQUISITES

Install the following packages:

+   - **linux-source** (the latest released Ubuntu kernel source code; not needed if you use `git` to download the code) Attempting to install **linux-source** displays the name of the package holding the latest kernel, which you then install; refer to the next section.
+   - **build-essential** (metapackage; includes the packages required to compile the code)
+   - **fakeroot**, **kernel-package** (kernel-specific)
+   - **git-core** (to use `git` to download the kernel source code)
+   - **ncurses-dev** (to configure the kernel using `make menuconfig`)
+   - **libglade2-dev** (to configure the kernel using `make gconfig`)
+   - **module-assistant**, **debhelper** (to create modules)