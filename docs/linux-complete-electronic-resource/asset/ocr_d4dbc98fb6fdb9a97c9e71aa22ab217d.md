The section, "Using Internet Services with Dynamic IP Numbers," provides information on the (main) services affected and what you can do (if anything) to overcome this.

# # CONFIGURING YOUR LINUX KERNEL

In order to use PPP, your Linux kernel must be compiled to include PPP support. Obtain the Linux source code for your kernel if you do not already have this—it belongs in `/usr/src/linux` on Linux's standard file system.

Check out this directory—many Linux distributions install the source tree (the files and subdirectories) as part of their installation process.

At bootup, your Linux kernel prints out a great deal of information. Among this is information about PPP support if the kernel includes it. To view this information, look at your `syslog` file or use `dmesg less` to display the information to the screen. If your kernel includes PPP support, you will see lines like

```
PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.
PPP line discipline registered.
```

(this is for the Linux 2.0.x kernel series).

Linux kernel sources can be obtained by ftp from `MetaLab.unc.edu` or its mirror sites.

# # Installing the Linux Kernel Source

The following are brief instructions for obtaining and installing the Linux kernel sources. Full information can be obtained from the Linux Kernel HOWTO (see http://`MetaLab.unc.edu/`mdw/HOWTO/Kernel1-HOWTO.html).

In order to install and compile the Linux kernel, you need to be logged in as root.

+   1. Change directory to the `/usr/src` directory `cd /usr/src`.
+   2. Check in `/usr/src/linux` to see if you already have the sources installed.
+   3. If you don't have the sources, get them from the Linux kernel source directory (`ftp://MetaLab.unc.edu/pub/Linux/kernel/v2.0`) or your nearest mirror. If you are looking for