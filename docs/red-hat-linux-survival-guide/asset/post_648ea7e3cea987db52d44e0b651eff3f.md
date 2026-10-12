
Gtop enables you to sort by any column. For example, you can sort all the running processes by their CPU usage by simply clicking on the CPU column header, or sort by owner (user) by clicking on the User column. The resident memory usage information is displayed separately. Click the Memory Usage (resident) tab to view a screen similar to the one shown in Figure 10-14.

![](img/9eb7e89292d2f85707b4d49102c865b7_260_0.png)

Figure 10-14 Viewing resident memory usage.

## Using Time Tool

To set system time and date use the Time Tool. This is a very simple tool that enables you to change the system's time or date. The interface is shown in Figure 10-15.

![](img/9eb7e89292d2f85707b4d49102c865b7_261_0.png)

Figure 10-15 The Time Tool.

## Using netcfg

See Chapter 6 for details on using netcfg.

## Using printtool

See Chapter 15 for details on using printtool.

## Using the kernel configuration tool

See Chapter 11 for details on using the kernel configuration tool.

## Using the help search tool

The help search tool that the control panel runs is called helptool, which searches online documents including man pages, info files, and random documents in the /usr/doc and /usr/local/doc directories to locate matches for keywords you specify.

## Using Red Hat Network Update Agent

The Red Hat Update Agent is a graphical tool that uses Red Hat Network to find out which packages on your system needs to be updated and updates them automatically. See Chapter 2 for details.

## Chapter 11

## Configuring the Kernel

## IN THIS CHAPTER

- Understanding the need for kernel upgrades
- Preparing for a kernel upgrade
- Installing a new kernel
- Compiling a custom kernel from the source
- Patching a kernel's source code
- Setting up the kernel with `kernelcfg`

Linux is probably the only operating system that develops a new kernel fairly often. Generally speaking, you can expect a new kernel from Red Hat every two to three months. This should tell you how heavy developmental efforts are in this platform. In this chapter, you learn to upgrade, configure, compile, and install custom kernels.

Linux runs on many hardware architectures, such as x86 (Intel), PowerPC, Alpha, and Sparc, among others. It is practically impossible to discuss kernel issues for all platforms in a single chapter, and therefore I assume that, like a majority of Red Hat Linux users, you have an x86 (Intel)-based system. However, if you are running Red Hat Linux on a system based on the mighty Alpha processor, you can find useful kernel-related information at www.alphalinux.org/. Also, for all architectures, you can go to www.kernel.org/.

## Why Do You Need a Newer Kernel?

The most common reason to upgrade a kernel is to take advantage of new device drivers to handle specific devices. For example, suppose that you have a fancy SCSI controller that has a bare-bones driver and you find that a vendor has released a new module or that a driver guru has written one that allows you to customize your SCSI controller more, or use features that you couldn't with the bare-bones driver. Another reason you might want to upgrade your Linux kernel is to plug security holes in the kernel or in a module. You should monitor the following Web site for availability of updated packages:

```
www.redhat.com/corp/support/errata/index.html
```

Of course, many people (perhaps those with lots of time) want to upgrade just to be on the cutting edge of the Linux revolution. If you are such a Linux disciple, my only recommendation is that you keep the latest and the greatest Linux kernel away from any of your production servers. Playing with the latest development-grade Linux kernel on a personal workstation can be quite an amusing task for people who “dig it.” This chapter shows you how to upgrade and customize your kernel.

## Finding Out Which Linux Kernel You Have

Before you do anything else, determine the version of the current kernel in your system. For example, you can run the following command:

```
rpm -q kernel \
    kernel-headers \
    kernel-ibcs \
    kernel-pcmcia-cs \
    kernel-source > /current-kernel-pkgs.txt
```

The current-kernel-pkgs.txt file has version information for kernel-related packages. You also need to know the version numbers for

mkinitrd (used to create initial ramdisk images), SysVinit (the init package), and the initscripts (the /etc/rc.d scripts) packages that often change with the new kernels. You can run the following command to add version information for these packages to the current-kernel-pkgs.txt file.

```
rpm -q mkinitrd SysVinit initscripts > /current-kernel-pkgs.txt
```

By running the preceding rpm commands, you have placed version information for all the typical packages you need for a full kernel upgrade. Table 11-1 lists the names and RPM descriptions of these packages.

## Table 11-1 Typical Packages Needed for Kernel Upgrades

| Package | Description Found in the RPM |
|---|---|
| kernel-2.x.xx-x.i386.rpm | This package contains the Linux kernel used to boot and run your system. It contains few device drivers for specific hardware. Modules loaded after booting support most hardware. |
| kernel-headers-2.x.xx-x.i386.rpm | These are C header files for the Linux kernel, which define structures and constants that you need to build most standard programs under Linux, as well as to rebuild the kernel. |
| kernel-ibcs2-2.x.xx-x.i386.rpm | This package allows you to run programs in the iBCS2 (Intel Binary Compatibility Standard, version 2) and in related executable formats. You can download this package from www.rpmfind.net. |
| kernel-pcmcia-cs-2.x.xx-x.i386.rpm | Many laptop machines (and some others) support PCMCIA cards for expansion. Also known as "credit card adapters," PCMCIA cards are small cards for everything from SCSI support to modems. They are hot-swappable (you can exchange them without rebooting the system) and quite convenient. This package contains support for PCMCIA cards of all varieties and supplies a daemon that allows you to hot-swap them. |
| kernel-source-2.x.xx-x.i386.rpm | This is the source code for the Linux kernel. It is required to build most C programs, as C programs depend on constants defined here. You can also build a custom kernel that is better tuned to your hardware. The source code is shipped in the second CD-ROM of the official Red Hat Linux distribution. |

## Table 11-1 Continued

| Package | Description Found in the RPM |
|---|---|
| `mkinitrd-x.x-x.rpm` | You can build Generic kernels without drivers for any SCSI adapters that load the SCSI driver as a module. You use an initial `ramdisk` to solve the problem of allowing the kernel to read the module without being able to address the SCSI adapter. The operating system loader (such as `LILO`) loads the `ramdisk` and is available to the kernel as soon as it is loaded. That image is responsible for loading the proper SCSI adapter and allowing the kernel to mount the root file system. This program creates such a `ramdisk` image using information in `/etc/conf.modules`. The source code is shipped in the second CD-ROM of the official Red Hat Linux distribution. |
| `SysVinit-x.xx-x.rpm` | SysVinit is the first program the Linux kernel starts when the system boots, controlling the startup, running, and shutdown of all other programs. |
| `initscripts-x.xx-x.rpm` | This package contains scripts used to boot a system, change run levels, and shut the system down cleanly. It also contains the scripts that activate and deactivate most network interfaces. |

To find out which kernel you are using to boot the system, take a look at your /etc/lilo.conf file. For example, my /etc/lilo.conf on a Red Hat Linux 7 system has the following lines:

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
message=/boot/message
linear
default=linux

image=/boot/vmlinuz-2.2.16-21
    label=linux
    read-only
    root=/dev/hda2
```
