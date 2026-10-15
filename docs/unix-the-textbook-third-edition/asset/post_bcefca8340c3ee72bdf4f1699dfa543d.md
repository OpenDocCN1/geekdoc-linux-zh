
When a USB thumb drive is automatically mounted on Solaris or PC-BSD, the path to it is /media.

It is possible, though, to add a removable medium for use with ZFS to either PC-BSD or Solaris, and we actually do this in Chapter 24, Section 24.2.2, Examples 24.5 and 24.6. But you must be cautious when creating zpools and ZFS datasets on removable media and then removing the media without properly unmounting the ZFS datasets. These procedures are addressed more fully in Chapter 24.

## 23.4.1 Preliminary Considerations when Adding New Disk Drives

If you insert a USB thumb drive that you know is functioning properly into your computer running either Solaris or PC-BSD, and it doesn’t automount or is not recognized, the chances are that your UNIX system does not have a device driver available to enable communication between the computer and the thumb drive.

The same is true when you connect a SATA bus hard drive properly, but the probability of this is much lower. The best and easiest thing to do in a case like this is to use another USB or SATA device. Both Solaris and PC-BSD have facilities to find and install device drivers on your system for a device, but this process is time consuming and may not be fruitful for the particular device in question. Also, it is possible to write a driver for your device, which is even more time consuming. The important thing here is not that the USB thumb drive is formatted to FAT32, but that a manufacturer has the device drivers available automatically when their device is inserted. This is not always true.

It is important to know the physical device name, the instance name, and the logical device name of disk drives on your system, but practically speaking, for the system administrator, easily finding out the logical device name of a disk drive is most important. This is because in the ZFS file system on Solaris and PC-BSD, the logical device name is what you use to create zpools, the critical first step in using ZFS. This is shown in full detail in Chapter 24.

You may want to add a hard disk to your UNIX system that has been used on another computer operating system previously. In that case, the following examples can be deployed to repartition and prepare that hard disk for new use on your UNIX system. Because ZFS is a volume manager, it is also possible to deploy a disk drive formatted and sliced for another operating system, and use ZFS on it simultaneously with the other operating system partitions.

## 23.4.2 A Quick and Easy Way to Find Out the Logical Device Names of Disks Actually Installed on Your System

Before attaching a new disk drive to your UNIX system, it is important to know how to determine, in a very quick and easy manner, what the currently installed logical device names of the disk drives actually attached and usable on your system are. What we mean by "attached and useable" is that the disk drive is properly connected and recognized by the system, and has a device driver that the system can use to communicate with it.

Before and after: If you want to find out the logical device name of a new disk you want to add to the system, use one of the following methods to see what disks are on your system

before you add the new disk, and then use the same method after the new disk has been added and note the difference. The different or new logical name that appears will be the logical name of the new disk.

The simple methods that follow show how to determine what disk drives are attached and usable on your system, and what the logical device names of those and any others you might want to add to your system are. These methods are done differently in Solaris and PC-BSD.

PC-BSD methods: Change your current working directory to /dev. Type ls. Hard drives, for example, show up in the ls listing as ada0, ada1, etc. The full path to the first slice on one of these disks is specified as /dev/ada0s1. A USB bus device, like a thumb drive, would show up in the ls listing as da0, and the full path to the first slice on it would be /dev/da0s1.

Additionally, you can type gpart show on the command line in a terminal window, and it will list the drives available for slicing, such as ada0, ada1s1, or da0s1 for disks and USB devices. The logical device names to all of those devices is provided in a compact and easily understood listing.

Solaris methods: For SCSI, SATA, or IDE bus hard disk drives, type format on the command line as superuser. The output of this command shows your main hard drive—for example, disk 0—as /dev/dsk/c0d0s0. Type exit to leave the format facility.

For USB bus thumb drives or hard drives, type rmformat on the command line as superuser. The output of this command shows, for example, a USB thumb drive as /dev/rdsk/c9t0d0p1. A CD or DVD writer would show up here too, not on the USB bus, but on the SATA bus.

Additionally, you can use the Gparted Partition Editor, as shown in Example 23.3.

## EXERCISE 23.9

Insert a USB thumb drive into either a PC-BSD or Solaris computer, and mount it if necessary. What is the logical device name for this thumb drive, and how did you find it out?

## 23.4.3 Adding a New Disk to the System

The following three examples show how to add a new hard disk to your system:

- Example 23.3 uses a GUI method in Solaris. This GUI technique not only lets you find out what the logical device names of disks are, but also allows you to slice newly added disks at the same time. It uses the Gparted Partition Editor program that comes installed with Solaris.
- Example 23.4 uses a GUI method in PC-BSD, by launching the PC-BSD Disk Manager. It also lets you find out the logical device names of disks on your system, and allows you to slice newly added disks.
