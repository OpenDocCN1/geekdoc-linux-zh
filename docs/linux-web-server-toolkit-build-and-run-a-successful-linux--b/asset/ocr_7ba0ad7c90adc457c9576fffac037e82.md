# Chapter 5: Installing Linux

# 109

![](bbox=[0.056, 0.111, 0.133, 0.163])

When creating a new partition for any operating system, always use a tool from that operating system to create the partition. Use the FDISK command in DOS to create DOS partitions; use the fdisk command in Linux to create Linux partitions, and so forth. You can also try special partitioning and dual-boot software such as Partition Magic from PowerQuest Software (http://www.powerquest.com) or System Commander from V Communications (http://www.v-comm.com). Just don't use DOS to create Linux partitions, or vice versa.

To install Linux, you need to prepare space on the hard disk to hold it. Basically, there are three possible scenarios that determine how best to do this, as follows:

+   1. You plan to use the system to only run Linux, so all hard disks on the system are dedicated to Linux.
2. You are using a separate hard disk for Linux, with another operating system on another hard disk. This is equivalent to option 1, because a hard disk doesn't have to be partitioned between more than one operating system.
3. You are putting Linux on part of a hard disk (a partition), with other partitions on the same hard disk being used by one or more other operating systems.

If your Linux plans put you in the first or second situations outlined previously, your job is easy. Go ahead and skip to the section in this chapter titled "Installing Linux". You'll use the fdisk utility during the installation program to prepare your hard disk.

If you plan to implement the third scenario, you will have to make room on the hard drive for Linux. This can involve several steps, depending on your operating system.

One method to create a Linux partition is to follow these steps:

+   1. Backup your entire system (twice).
2. Make a bootable floppy disk using a command such as SYS. Include in the floppy some basic commands such as FORMAT and FDISK or equivalents.
3. Reformat your hard disk.
4. Use the disk utility of your other operating system (SCO UNIX, OS/2, Windows, or whatever) to make a partition for that operating system. (Make it smaller than it was before, so there is free space on the hard disk for Linux.)