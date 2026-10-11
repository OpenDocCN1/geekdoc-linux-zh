fips.exe can be downloaded at http://Sunsite.unc.edu/pub/Linux/system/install. Whenever you use a program such as fips, you should always make a full backup and read the documentation before starting.

Copy fips.exe and restartbx.exe to a floppy. A copy of your old Master Boot Record (MBR) will be copied to this floppy during the installation program. This backup copy of your MBR can be used in case you ever need to restore your system to its original state. Be sure to label and date the diskette.

A copy of the old MBR also will be saved on your Linux partition as /boot/boot.0300 (for IDE drives) or /boot/boot.0800 (for SCSI drives). Do not ever delete the original file from your hard disk. If you delete it, you will not be able to restore the old MBR.

> **Key concept**
> 
> You can use the fips utility to dynamically divide an existing FAT partition to create space for installing Linux.

# fdisk

Be sure to keep good notes while partitioning your drive. You will want to note starting and ending cylinders, partition size in blocks, and any error messages you might get.

*Cylinder* refers to the total of the tracks that have the same location on each disk’s surface. *Tracks* are the concentric circles on a disk.

When using fdisk, you must enter starting and ending cylinders for each partition. To create a partition, follow these steps:

+   1. Size the partition.
+   2. Designate its type.
+   3. Write it to the partition table.

Using fdisk and each of the previous steps are covered in the following sections.

fdisk takes the name of the disk you want to partition as an argument or value.

For example, to create partitions on the second SCSI drive in your system, you would type

```
fdisk /dev/sdb
```