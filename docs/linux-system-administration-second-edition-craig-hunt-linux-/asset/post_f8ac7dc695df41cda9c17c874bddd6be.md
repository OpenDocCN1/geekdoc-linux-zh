
configuration entirely. For this example, select **Test This Config**. If you see a box asking whether or not you can read it, click the OK button.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_61_0.png)

Figure 2.7: The X Configuration screen

## Tying Up Loose Ends

Next you will be greeted with the message that your Red Hat installation is complete. Remove any floppy or CD-ROM still in its drive and reboot the system. Remember that if you skipped the boot loader installation, you must put your boot disk into the floppy drive. After your computer finishes powering up, assuming you went with the GRUB boot loader, you’ll see the graphical boot loader menu. Select a boot label corresponding to the operating system that you wish to work in. The default boot label for your Red Hat 7.3 system will be Red Hat Linux (2.4.28-3). If you specified any other boot labels during the installation, you may boot them by scrolling to the one you want and then pressing Enter. If you press the Enter key alone, the default boot entry will be booted. If you do nothing, the boot loader will pause for the specified timeout period (30 seconds by default) and then will boot the default boot entry. When your system is booted, you’ll be greeted with a login prompt. Enjoy.

## In Sum

In this chapter we saw how to implement disk caching, RAID, and clustering using Linux. We took a look at the most popular Linux distributions and the hallmark features of each. We discussed hardware configuration and, if you were following along, you have now installed a Linux server and a Linux workstation. In the next chapter we get into the internals of the Linux operating system, familiarizing you with the startup and shutdown processes.

# Chapter 3: Startup and Shutdown

## Overview

The process of starting up Linux is multifaceted. So much happens during a system boot that it is easy to lose touch with what procedures actually take place. Much of the wizardry of system administration is simply familiarity with a process such as booting. Knowing this process well makes it fairly easy to configure the system, to fix it when it breaks, and to explain it to your users. To understand the Linux startup, we'll walk through it from start to finish in this chapter. Linux startup and shutdown are further complicated by the fact that there are two different standards for how they are done: the BSD-style startup method and the System V-style method. Understanding the differences between the two is important since some Linux distributions—Debian and Slackware for example—use BSD-style system initialization scripts, while other distributions, such as Red Hat and Caldera, use System V-style startup scripts.

In this chapter we talk about the boot loaders (GRUB, LOADLIN, and LILO)—what they are and how they work. We look at different boot methods, including booting into single-user mode and booting from a floppy. We examine the Linux startup scripts in some detail, and the related user startup files that run when a user logs in to the system. Finally we discuss the log files that help you to troubleshoot when a system won't start up normally.

The system performs a similar sequence of tasks after you command it to shut down. There are many active processes that must be shut down and devices and filesystems that must be unmounted to avoid causing damage to your system. This process also occurs in stages. We'll also walk through this process to gain a full understanding of how shutdown works and what it does. The shutdown scripts and log files are discussed in order to make the whole process clear.

## The Linux Boot Process

When you start up a Linux system, a series of events occurs after you power up and before you receive a login prompt. This sequence is referred to as the boot process. Although this sequence can vary based on configuration, the basic steps of the boot process can be summed up as follows:

1.  The Basic Input/Output System (BIOS) starts and checks for hardware devices. Stored in the computer's ROM (Read-Only Memory), the BIOS is described as firmware because it is built into the hardware memory. The BIOS will automatically run when the power is applied to the computer. The purpose of the BIOS is to find the hardware devices that will be needed by the boot process, to load and initiate the boot program stored in the Master Boot Record (MBR), and then to pass off control to that boot program. In the case of Linux, the BIOS performs its checks and then looks to the MBR, which contains the first-stage boot loader, such as GRUB or LILO. After finding the boot loader, the BIOS initiates it.
    *Note: Sometimes, however, the MBR contains another boot loader, which in turn finds the boot loader on the first sector of a Linux partition.*
2.  The BIOS hands over control to the first-stage boot loader, which then reads in the partition table and looks for the second-stage boot loader on the partition configured as bootable.
3.  The first-stage boot loader runs the second-stage boot loader, which then finds the kernel image and runs it.
4.  The kernel image contains a small, uncompressed program that decompresses the compressed portion of the kernel and runs it. The kernel scans for system information.
5.  The kernel starts the init process by running /sbin/init.
6.  As outlined in the later section "Initialization and Startup Scripts," the init process starts up Getty programs for the virtual consoles and serial terminals and initiates other processes as configured and monitors them until shutdown.

This general boot process can be affected by various factors even within the same distribution. For instance, the steps above assume the system has only one bootable kernel image. That's probably the case when you first install, but you might also have a bootable sector installed with another operating system, like Windows, or a different distribution of Linux. Later, if you install a different version of the kernel and compile it, you'll have to configure your boot loader to see it. As you'll see later in the chapter, there are a number of parameters that you can specify at the boot prompt, but first let's take a closer look at the Master Boot Record.

## The Master Boot Record

The Master Boot Record (MBR) plays a crucial role in the bootup process. Located on the first disk drive, in the first sector of the first cylinder of track 0 and head 0 (this whole track is generally reserved for boot programs), it is a special area on your hard drive that is automatically loaded by your computer's BIOS. Since the BIOS is loaded on an electronically erasable programmable read-only memory (EEPROM) chip, which is generally not reprogrammed at the user/administrator level, the MBR is the earliest point at which a configured boot loader can take control of the boot process. Figure 3.1 shows a hard drive with its MBR and five Linux partitions.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_64_0.png)

Figure 3.1: A hard drive’s partition layout

Three of these (/dev/hda1 through /dev/hda3) are primary partitions that are pointed to directly, and two (/dev/hda5 and /dev/hda6) are logical partitions that reside within an extended partition (/dev/hda4). This baroque arrangement is the result of early limitations on the number of partitions in the PC’s partition table and is further discussed in Chapter 6, "Filesystems and Disk Management." Linux uses the Third Extended Filesystem (ext3fs), which is also detailed in Chapter 6. Basically, the filesystem is the structure imposed on each partition for the purpose of organizing files. It is the underlying frame to which the data is added.

## Boot Loaders

There are several boot loaders to choose from. Alternatives include System Commander, NTLLDR, Linux Loader (LILO), and the Grand Unified Bootloader (GRUB). System Commander is a boot management utility that allows you to choose from up to 100 operating systems at boot time. Information is available at http://www.v-com.com/. NTLLDR is the boot manager for Windows NT. More information about NTLLDR is available at http://microsoft.com/. Most likely, the default boot loader for your distribution will be either LILO or GRUB, but any of these boot loaders can be installed after the initial operating system installation. Whichever you choose, this boot loader is the first non-BIOS step in the boot process.

### GRUB: Definition and Configuration

As of Red Hat 7.2, Red Hat began to use GRUB as the default boot loader. The main advantage of GRUB over LILO is that GRUB is far more flexible. GRUB does not require you to run an install program each time you make changes. If you make changes to LILO, say updating a kernel image that is included in the LILO configuration, and forget to run the LILO installer program, you might have to boot a rescue disk to get back into your system. With GRUB, you do not encounter this problem. Additionally, you can view some information from your system using the GRUB boot prompt, which is not possible with other boot loaders.

GRUB comes with several different pre-configured files to be used to boot its supported operating systems: BSD FFS, DOS FAT16 and FAT32, Minix fs, Linux ext2fs and ext3fs, ReiserFS, and VSTafs. GRUB is much larger than other boot loaders, but the size is justified by the flexibility that the extra features offer. GRUB's ability to access data on any device that is recognized by the BIOS is one feature that we wouldn't want to do without. For example, you may view the /etc/fstab file before the system is completely booted, by using the cat command at the GRUB prompt like this:

```text
grub> cat /etc/fstab
```

Another nice feature is the ability to decompress files that were compressed using gzip; the decompression is transparent to the user. GRUB also cares less about disk geometries than other boot loaders. In fact, you can relocate the kernel image and GRUB will still find it. Other boot loaders have to know the block location of the image.

The GRUB configuration files are intended to be human-readable. The grub.conf file is a little strange to those used to LILO, but it takes very little time to get used to. See Listing 3.1. Each section that defines a bootable kernel or non-Linux partition is known as a stanza.

Listing 3.1: A Sample grub.conf File

```text
# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making changes to this file
# NOTICE:  You do not have a /boot partition.  This means that
#          all kernel and initrd paths are relative to /, eg.
#          root (hd0,0)
#          kernel /boot/vmlinuz-version ro root=/dev/hda1
#          initrd /boot/initrd-version.img
#boot=/dev/hda
default=0
```
