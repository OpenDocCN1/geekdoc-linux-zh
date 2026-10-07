# Chapter 5: Installing Linux 99

server performance. Just be certain you get a high-quality hard drive with good access times.

Most computers that you see advertised will come with an IDE hard drive. While this standard hard drive interface is for personal use, a SCSI hard drive is the preferred choice for Web servers. SCSI peripherals can achieve data transfer rates far higher than IDE devices, especially if the latest wide SCSI or ultrafasc SCSI cards are used. This higher data rate is critical in a busy Web server, where the hard drive can be a bottleneck for server performance.

# Using Modules for Hardware Support

Linux and the drivers that interact with hardware are great at using hardware to its maximum potential. Most of the drivers can be tuned to use specific software addresses or certain feature sets.

The 2.0 kernel includes a great feature: the capability to use modules for hardware support or other functionality. A module is a small piece of software that can be loaded into the kernel at any time. As you install OpenLinux, remember that each module supports a specific type of hardware. Some modules are more generic (like a floppy disk support, which is very standardized) and some are very specific, like a module for a certain model of SCSI CD-ROM drive that has specific features no of the generic SCSI or CD-ROM drivers work with it.

> Modules used for many things in Linux, including Java and many types of networking (such as PPP and IP/SPX). I discuss modules relative to how they are used during the installation of OpenLinux. You can learn more about modules from the insmod manual page or the Kernel Hacker's Guide (part of the Linux Documentation Project on the OpenLinux CD-ROM).

![](bbox=[0.047, 0.553, 0.148, 0.603])

Modules make it easy to add just the hardware support you need without having everything with the kitchen sink in the Linux kernel and “making” the kernel (recompiling from the source code) to add support for new hardware. The modules enable hardware support to be added or removed without rebooting the Linux system, an important feature for a busy web site.

When you install the OpenLinux CD-ROM, default modules are loaded. Depending on your hardware, you can load other modules to provide support for your system.

After the installation is complete and you have started up your Linux system, you can use simple commands to list the modules that the kernel is using or to add or remove a module from the running system. Table 5-1 lists the commands you can use to examine the modules on your system after you've installed Linux.