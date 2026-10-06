
# CHAPTER 7 File Systems

the obvious: Check for reliable power and well-connected cables; check to make sure you are using good quality cables; for mechanical drives, make sure there are no clicking sounds; and so on.

When all else fails, fsck doesn't fix the issue, it will often give you a hint as to what's wrong. You can use this hint to perform a search on the Internet and see what other people have done to resolve the issue.

## The lost+found Directory

Another situation occurs when fsck finds file segments that cannot rejoin with the original file. In those cases, it will place the fragment in the lost-found directory. This directory is located where the partition is mounted, or if /dev/mapper/fedora-home is mounted at /home, for example, then /home/lost+found correlates to the lost-found directory for that particular file system.

Anything can go into a lost+found directory—file fragments, directories, and even special files. When normal files wind up there, a file owner should be attached, and you can contact the owner and if they need the data (typically, they won't). If you encounter a directory in lost+found, you'll likely want to restore it from the most recent backups than to reconstruct it from lost+found. At the very least, lost+found tells you whether anything been displaced. Again, such errors are extraordinarily rare.

## Adding a New Disk

On systems PC hardware architecture, the process of adding a disk under Linux is relatively easy. You are adding a disk that is of similar type to your existing disks—example, adding a SATA disk to a system that already has SATA drives—the system should automatically detect the new disk at boot. All that remains is partitioning and creating a file system on.

If you are adding a new type of disk (such as a SAS [Serial Attached SCSI] disk on a system that has) you may need to ensure that your kernel supports the hardware. This support can be built into the kernel or be a loadable module (driver). Note that the kernels of most Linux distributions come with many popular disk/storage controllers, which may on rare occasions come across troublesome kernel and hardware combinations, especially with the new motherboards that have exotic chipsets.

Once the disk is in, simply reboot the system, and you're ready to go. If you aren't sure about whether the system can see the new disk, run dmesg command and check whether the driver loaded and was able to find your disk. Here's an example:

```
[root@server ~]# dmesg | egrep -i "hd|sd|disk"
```

## Overview of Partitions

For the sake of clarity, and in case you need to know what a partition is partitioned before it works, let's briefly review this subject. Disks typically need to be partitioned before use. Partitions divide the disk into segments, and each segment acts as a complete disk by itself. Once a partition is filled with data, the data cannot automatically overflow onto another partition.

Various things can be done with a partitioned disk, such as installing an OS into a single partition that installing several different OSs into their own separate partitions in what is commonly called a "dual-boot" configuration, and using the different partitions to separate and restrict certain system functions into their work areas.

This example is especially relevant on a multisuer system, where the content of users' home directories should not be allowed to overcrowd and disrupt OS functions.

## Traditional Disk and Partition Naming Conventions

Modern Linux distributions use the libATA library to provide support within the Linux kernel for various storage devices as well as controllers. Under Linux, each disk is given its own device name. The device files are stored under the /dev directory.

Hard disks start with the name sdX, where X can range a through z, with each letter representing a physical block device. For example, in a system with two hard disks, the first hard would be /dev/sda and the second hard disk would be /dev/sdb.

When partitions are created, corresponding device files are created. They take the form of /dev/sdXY, where X is the device letter (as described in the preceding paragraph) and Y is the partition number.

### The Old Days of IDE Device Naming
In the old days before the advent of the current libATA subsystem, the IDE device naming convention for hard disks were very distinct from other hard drive interfaces such as SCSI or SATA. The device naming for IDE drives used to be something like /dev/hdX. This means that device names started with hd instead of sd. For example, in an IDE-only system with one hard disk and one CD-ROM, both on the same IDE chain, the hard disk would be /dev/hda and the CD-ROM would be /dev/hdb. This information is provided for legacy systems.

Thus, the first partition on the /dev disk is /dev/sda1, the second partition on the third disk would be /dev/sdc2, and so on. SCSI disks follow the same basic scheme.

Some standard devices are automatically created during system installation, and others are created as they are connected to the system.

## Volume Management

You may have noticed earlier that we use the terms “partition” and “volume” interchangeably in parts of the text. Although they are not exactly the same, they are similar in a conceptual way.

Volume management is a new approach to dealing with disks and partitions: Instead of viewing a disk or entity along partition boundaries, the boundaries are no longer present and everything is now as volumes. (That made perfect sense, didn't? If it didn't; this's a tricky concept. Let's try this again with more detail.)

This approach to dealing with partitions is called Logical Volume Management (LVM) in Linux. It lends itself to several benefits and removes the restrictions, constraints, and limitations that the concept of partitions imposes. Following are some of the benefits:

- Greater flexibility for disk partitioning
- Easier resizing of volumes
- Easier to increase storage space by simply adding new disks to the storage pool
- Use of snapshots

Following are some important volume management terms:

- Physical volume (PV) This typically refers to the physical hard disk(s) or another physical storage entity, such as a hardware Redundant Array of Inexpensive Disks (RAID) or software RAID device(s). Only a single storage entity (for example, one partition) can exist in a PV.
- Volume group (VG) Volume groups are used to house one or more physical volumes and logical volumes in a single administrative unit. A volume group is created out of physical volumes. VGs are simply a collection of Volumes; however, VGs are not mountable. They are more like virtual disks.
- Logical volume (LV) This is perhaps the trickiest LVM concept to grasp, because logical volumes (LVs) are the equivalent of partitions in a non-LVM world. To the administrator, an LV appears as a standard device. We put file systems on the LV, and the LV gets mounted.

## Creating Partitions and Logical Volumes

During the installation process, you probably used a "pretty" tool with a nice GUI front-end to create partitions. The GUI tools available across the Linux distributions vary greatly in looks and usability. Two tools that can be used to perform most partitioning tasks, and have a unified look and feel regardless of the Linux flavor, are the parted and fdisk utilities.

Although fdisk is simple and somewhat awkward, it's a reliable command-line tool. parted, on the other hand, is much more user-friendly and has a lot more built-in functionalities than other tools. In fact, a lot of GUI partitioning tools call parted in their back-end. Furthermore, in the event you need to troubleshoot a system that has really gone wrong, you should be familiar with basic tools such as parted and fdisk. Other powerful command-line utilities for managing partitions are sfdisk and cfdisk.

During the installation of the OS, as covered in Chapter 2, you were asked to leave some free partition. We will now use that space to demonstrate some LVM concepts by walking through the steps required to create a logical volume.

In particular, we will create a logical volume that will house the contents of the current /var directory. Because a separate /var volume was not created during the OS installation, the contents of the /var directory are currently stored within the volume that holds the root (/) tree. The general idea is that the /var directory is typically used to hold frequently and changing data (such as log files), it is prudent to put its content on its own separate file system.

The steps involved in creating a logical volume can be summarized this way:

1. Initialize a regular partition for the LVM system, or simply create a partition of the type lvm.
2. Create physical volumes from the hard disk.
3. Assign the physical volume(s) to volume group.
4. Finally, create logical volumes within the volume groups, and assign mount points to the logical volumes after formatting.
