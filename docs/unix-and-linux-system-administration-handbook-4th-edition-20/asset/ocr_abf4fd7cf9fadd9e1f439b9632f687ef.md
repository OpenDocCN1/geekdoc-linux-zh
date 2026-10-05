# Chapter 13

# Drivers and the Kernel

Hardware vendors are becoming more aware of the UNIX and Linux markets, and sometimes they provide UNIX and Linux drivers for their products. In the optimal case, your vendor furnishes you with both drivers and installation instructions. Occasionally, you only find the driver you need on sketchy-looking and uncommon web page. For either case, this section shows what you is really going on when you add a driver to your system.

# Device files and device numbers

Most devices have a corresponding file in /dev; network devices are notable exceptions on modern operating systems. Complex servers support hundreds of devices. Solaris handles this complexity nicely by using a subdirectory of /dev for each type of device: disk, cdom, terminal, etc.

By virtue of being device files, the files in /dev each have a major and minor device number associated with them. The kernel uses these numbers to map device-file references to the corresponding driver.

The major device number identifies the driver with which the file is associated (in other words, the type of device). The minor device number usually identifies which particular instance of a given device is to be addressed. The minor device number is sometimes called the unit number.

You can see the major and minor number of a device file with ls:

```
linux$ ls -l /dev/sda
brw-rw---- 1 root disk 8, 0 Jul 13 01:38 /dev/sda
```

This example shows the first disk on a Linux system. It has a major number of 8 and a minor number of 0.

The minor device number is sometimes used by the driver to select or enable certain characteristics particular to that device. For example, a tape drive can have one file in /dev that rewinds the drive automatically when it is closed and another file does not exist. The driver is free to interpret the minor device number in whatever it wants. Look up the man page for the driver to determine what it's using.

There are actually two primary types of device files: block devices and character files. A block device is read or written one block (group of bytes, usually a multiple of 512) at a time; a character device can be read or write one byte at a time. Disks and tapes lead dual loads: terminals and printers do not.

Device drivers provide a standard interface to the kernel. Each driver has routines for performing some or all of the following functions:

```
attach close dump ioctl open probe
size read receive reset select stop
strategy timeout transmit write
```