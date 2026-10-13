# 13 VMware Tips for Linux

The tips in this chapter are for your Linux guest operating systems, which are independent of the host operating system that you run VMware on: Windows or Linux. Some of the tips are not really VMware related, but because of the usage scenarios for VMware, they are important to know when getting started with Windows and VMware.

# 13.1 Keep the Kernel and Kernel Source at the Same Patch Level

When you install VMware Workstation for Linux or when you install the VMware Tools inside a Linux guest operating system, on many occasions you need to compile modules for your product. One example of such a module is vmmon. The installation script will check the kernel version that you are running and will try to compile the modules for your kernel. In addition, it also accesses the kernel source files. If you install these kernel source files from a CD-ROM when you need them, then you most likely will install another version than is currently on your system. If you ran an update for your operating system, the kernel could very well be updated to a kernel patch level and since you did not install the kernel source files during initial installation the kernel is patched but the sources are not. Figure 13.1 shows an example where the usr/src/linux directory for the current kernel level (found with the uname -r command) is not correct.

```
linux:/usr/src/linux # uname -r
2.6.5-7.151-default
linux:/usr/src # ll
total 1
drwxr-xr-x 6 root root 248 Sep 5 16:35 .
drwxr-xr-x 12 root root 344 Apr 3 20:14 ..
lrwxrwxrwx 1 root root 17 Sep 5 16:35 linux -> linux-2.6.5-7.111
drwxr-xr-x 3 root root 96 Sep 5 16:31 linux-2.6.5-7.111
drwxr-xr-x 20 root root 712 Apr 3 20:33 linux-2.6.5-7.151
drwxr-xr-x 3 root root 72 Mar 18 18:06 linux-2.6.5-7.151-obj
lrwxrwxrwx 1 root root 21 Apr 3 20:34 linux-obj -> linux-2.6.5-7.151-obj
drwxr-xr-x 7 root root 168 Mar 23 14:15 packages
linux:/usr/src #
```

Figure 13.1: An example of a Linux installation with a mismatched kernel source.

If you run into a problem, such as when the running kernel and the sources are not identical, then the easiest option is to use your distributions installation directory to re-install the kernel sources package and have them updated automatically.

If you know how to download and install the correct sources manually, then you can find them at the following URL: www.kernel.org.

When it was necessary to build the vmmon module, it could have displayed a message saying: Module.symvers is missing' modules will have no modversions and Unable to build the vmmon module.