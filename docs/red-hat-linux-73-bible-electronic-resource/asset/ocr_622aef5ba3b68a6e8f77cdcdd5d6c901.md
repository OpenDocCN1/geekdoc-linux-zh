+   * **Networking options** — Network should be on by default. It should be on even if you are not connected to a network because the X Window System (your graphical desktop) relies on it. Otherwise, you will want to reconfigure networking options if Linux is operating as a router and you want to optimize it as such (by default, it is optimized to act as a host). Certain experimental options (X.25, SPX, and others) are also turned off by default.
+   
+   * **Block devices** — For some older disk drives, you may need to use an old disk-only driver on the primary interface. With that selected, you won't be able to have an IDE/ATAPI CD-ROM attached to the primary IDE interface. However, turning on the disk-only driver may be necessary for some older disk drives.
+   
+   * **QoS and/or fair queuing** — If your network devices include some real-time devices that require a minimum quality of service (QoS), you can change some of these QoS values to favor certain interfaces when there is a lot of demand for service. Turning on QoS lets you try any of a handful of different algorithms.

As you read this and other documents that describe how to use Red Hat Linux, the documents may describe features that require changing the kernel for those features to work. By using tools such as the X kernel configuration tool, you can determine which features are turned on and off by default, and build a kernel to suit your needs.

> **NOTE:** If you need to support a hardware device that is only added temporarily or occasionally to your computer, you should try to configure it as a loadable module. In that way, you can load and unload the module as needed, without making the kernel bear any performance penalty when the device is not needed.

# Installing kernel source code

To reconfigure the kernel, you need the Linux source code. You can install that source code from the second Red Hat Linux installation CD that comes with this book (CD-2). If the source code is already installed on your Linux system, it should be in the `/usr/src/linux*` directory (for example, `/usr/src/linux-2.4`).

The kernel source code is contained in the kernel-source package in RedHat/RPMS directory on the second installation CD. When I checked the disk space, the source code consumed about 127MB of disk space in `/usr/src/linux-2.4` (which is a link to a directory that has a name reflecting the kernel release, such as `linux-2.4.18-0.13`). To install the kernel source code from the RPMS directory, type:

```
# rpm -i kernel-source*
```

# Starting to reconfigure the kernel

The steps for reconfiguring your kernel include configuring the options, checking for dependencies, cleaning up the files, and compiling the new kernel. Each of these steps is fairly straightforward and described in the text that follows: