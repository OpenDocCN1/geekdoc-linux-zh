# ## ■ PARTITIONING A DRIVE FOR LINUX

A drive can be in four partition states when you get ready to install Linux. It can already have data, using all available space, it can have unpartitioned free space available, it can have an unused partition available, or it can have free space available in an actively used partition.

If all available space is being used, your choices are limited. You have to either reformat the existing partitions or install a second hard drive. This is necessary when using an existing system and often when using a new preconfigured system.

If you have unpartitioned free space, you can create partitions within the free space without interfering with existing partitions. Usually if you have this condition, it is a new install or you are installing more than one operating system.

If you have an existing partition that is no longer needed, you can use it for Linux. To reuse a partition, you need to delete the partition and then create a Linux partition.

Free space in an actively used partition is a little more difficult to use. To use this type of partition you have to back up the existing data, remove the existing partition, create two or more new partitions; restore the data, and then install the Linux operating system. If there is an operating system on the drive you are repartitioning, you will have to reinstall the operating system.

> **NOTE**

The Logical Volume Management (LVM) partition type provides for increasing and decreasing existing partitions. This is discussed in Chapter 12.

# ### Device Names

If you are familiar with partitions in a DOS/Windows environment, you know that the first hard drive partition is C, the second is D, and so on. Linux uses a different approach. Instead of using single letters to indicate partitions it uses a file-based schema to name a device. Device names are usually in the form:

*/dev/xyN*

where

+   - /dev is the name of the directory where all devices are stored
- xx indicates the type of device (hd for IDE, sd for SCSI)
- y indicates which physical device the partition is on (hda for the first IDE hard disk, sdb for the second SCSI drive)
- N indicates which partition of a drive. The first four partitions are numbered 1 through 4; logical partitions start at 5.

To use the device, you link it to a mount point.

# ### Mount Points

In DOS or Windows, the mount points are easily distinguished by drive letters. If you refer to the first partition you use C, and so on through the alphabet. In Linux, the mount points are part of a single set of files and directories. For example, if you want user data to be stored on /dev/hdb4, you can mount /home on that partition. /home will appear as any other directory in the file system, but it will actually be a drive or partition separate from other directories on the system.

This process is useful when tuning your system for performance. If high-use areas are mounted to multiple drives, work can be spread across the drives, improving overall