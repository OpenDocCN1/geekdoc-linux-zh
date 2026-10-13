
The dummy option for cdrecord lets you test the CD writing operation for a given image.

## dvd+rw Tools

The primary dvd+rw tool is **growisofs**, with which you create DVD+RW/R disks. Two other minor supporting tools are also included, a formatter, dvd+rw-format, and a compatibility tool, dvd+rw-booktype. See the dvd+rw-tools page in `/usr/share/doc` for detailed instructions.

The **growisofs** tool functions like the **mkisofs** tool, except that it writes directly to the DVD+RW/R disc, rather than to an image. It has the same options as **mkisofs**, with a few exceptions, and is actually a front end to the **mkisofs** command. There is, of course, no `-o` option for specifying a disk image. You specify the DVD device instead. For example, to write the contents of the newsongs directory to a DVD+RW disc, you would use **growisofs** directly.

```
growisofs -v -V "Goodsongs" -Z /dev/scd0 newsongs
```

The device is specified by its name, usually `/dev/scd0` for the first SCSI device. Recall that IDE DVD writers are configured as SCSI devices by the ide-scsi module when your system boots up. **growisofs** provides a special `-Z` option for burning an initial session. For multi-sessions (DVD-RW), you can use the **mkisofs -M** option. If you want to reuse a DVD-RW disc, just overwrite it. You do not have to reformat it.

To burn an ISO image file to the disc, use the `-Z` option and assign the iso image to the device.

```
growisofs -v -V "Goodsongs" -Z /dev/scd0=moresongs.iso
```

Though **growisofs** will automatically format new DVD+RW disks, the dvd+rw tools also include the dvd+rw-format tool for explicitly performing formats only. You use the dvd+rw-format tool only to explicitly format new DVD+RW (read/write) disks, preparing them for writing. This is done only once, and only for DVD+RW disks that have never been used before. DVD+R discs do not need any formatting.

The dvd+rw-booktype tool sets the compatibility setting for older DVD-ROM readers that may not be able to read DVD+RW/R disks.

# Chapter 31: RAID and LVM

## Overview

With the onset of cheap, efficient, and very large hard drives, even the most professional systems employ several hard drives. The use of multiple hard drives opens up opportunities for ensuring storage reliability as well as more easily organizing access to your hard disks. Linux provides two methods for better managing your hard disks: Redundant Arrays of Independent Disks (RAID) and Logical Volume Management (LVM). RAID is a way of storing the same data in different places on multiple hard disks. These multiple hard drives are treated as a single hard drive. They include recovery information that allows you to restore your files should one of the drives fail. LVM is a method for organizing all your hard disks into logical volumes, letting you pool the storage capabilities of several hard disks into a single logical volume. Your system then sees one large storage device, and you do not have to micromanage each underlying hard disk and their partitions.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_743_0.png)

## Enabling RAID and LVM in the Kernel

Red Hat provides methods for creating, installing, and configuring RAID and LVM devices during the Linux installation process. If, instead, you wish to add these devices later, you need to first enable support for RAID in the kernel. RAID is not enabled by default unless you installed RAID devices during installation. As discussed in Chapters 32 and 33, you need to configure kernel modules-in this case, modules for RAID and LVM devices. During kernel configuration, select Multi-Device Support (RAID and LVM) from the Linux Kernel Configuration window. You can then choose to enable support for RAID and LVM, either as modules or as a built-in kernel feature (if you make them parts of the kernel, you will have to rebuild the entire kernel). For RAID devices, you can choose the type of Linux software RAID devices you want to install.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_744_0.png)

## Configuring RAID Devices

RAID is a method of storing data across several disks to provide greater performance and redundancy. In effect, you can have several hard disks treated as just one hard disk by your operating system. RAID then efficiently stores and retrieves data across all these disks, instead of having the operating system access each one as a separate file system. Lower-level details of storage and retrieval are no longer a concern of the operating system. This allows greater flexibility in adding or removing hard disks, as well as implementing redundancy in the storage system to provide greater reliability. With RAID, you can have several hard disks that are treated as one virtual disk, where some of the disks are used as real-time mirrors, duplicating data. You can use RAID in several ways depending upon the degree of reliability you need. When you place data on multiple disks, I/O operations can overlap in a balanced way, improving performance. Because having multiple disks increases the mean time between failures (MTBF), storing data redundantly also increases fault-tolerance.

RAID can be implemented on a hardware or software level. On a hardware level, you can have hard disks connected to a RAID hardware controller, usually a special PC card. Your operating system then accesses storage through the RAID hardware controller. Alternatively, you can implement RAID as a software controller, letting a software RAID controller program manage access to hard disks treated as RAID devices. The software version lets you use IDE hard disks as RAID disks. Linux uses the MD driver, supported in the 2.4 kernel, to implement a software RAID controller. Linux software RAID supports five levels (linear, 0, 1, 4, and 5), whereas hardware RAID supports many more. Hardware RAID levels, such as 6 through 10, provide combinations of greater performance and reliability.

> **Tip**: Before you can use RAID on your system, make sure it is supported on your kernel, along with the RAID levels you want to use. If not, you will have to reconfigure and install a RAID module for the kernel. Check the Multi-Device Support component in your kernel configuration. You can specify support for any or all of the RAID levels.

## Linux Software RAID Levels

Linux software RAID can be implemented at different levels, depending on whether you want organization, efficiency, redundancy, or reconstruction capability. Each capability corresponds to different RAID levels. For most levels, the size of the hard disk devices should be the same. For mirroring, RAID 1, disks of the same size are required, and for RAID 5 they are recommended. Linux software RAID supports five levels as shown in Table 31-1. (On Red Hat, level 4 is implemented as part of level 5.)

Table 31-1: Linux Software RAID Levels

| RAID Level | Capability | Description |
|---|---|---|
| Linear | Appending | Simply treats RAID hard drives as one virtual drive with no striping, mirroring, or parity reconstruction. |
| 0 | Striping | Implements disk striping across drives with no redundancy. |
| 1 | Mirroring | Implements a high level of redundancy. Each drive is treated as a mirror for all data. |
| 5 | Distributed Parity | Implements data reconstruction capability using parity information. Parity information is distributed across all drives, instead of using a separate drive as in RAID 4. |

## Linear

The linear level lets you simply organize several hard disks into one logical hard disk, providing a pool of continuous storage. Instead of being forced to set up separate partitions on each hard drive, in effect you have only one hard drive. The storage is managed sequentially. When one hard disk fills up, the next one is used. In effect, you are appending one hard disk to the other. This level provides no recovery capability. If you had a hard disk RAID array containing two 80GB disks, after you used up the storage on one, you would
