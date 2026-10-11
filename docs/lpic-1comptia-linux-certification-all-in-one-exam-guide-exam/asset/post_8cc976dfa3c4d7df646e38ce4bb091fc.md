
## Building a File System with mkfs

Even though we've created a partition with fdisk, we can't use it yet. That's because it hasn't been formatted with a file system yet. This is accomplished using one of the several commands. In this part of the chapter, we will look at the following topics:

- Using mkfs
- Using mkreiserfs
- Creating xfs and vfat file systems
- Using mkswap

### Using mkfs

The mkfs utility is used to make an ext2, ext3, or ext4 file system on a partition. You can even use it to create a FAT file system on the partition (which is used by Windows and DOS). This utility is actually just a front end for the real commands that make each specific type of file system:

- /sbin/mkfs.minix
- /sbin/mkfs.ntfs
- /sbin/mkfs.bfs

WARNING: DOS-compatible mode is deprecated. It’s strongly recommended to switch off the mode (command 'c') and change display units to sectors (command 'u').

Command (m for help):

Notice that, because this is a new disk in the system, it has to be initialized with a disk label. The fdisk utility takes care of this for you when you load the program. However, the change won’t be applied until you write the disk.

With fdisk running, you have a Command: prompt that you can use to enter fdisk commands. At this point, one of the best things you can do is to enter m to view the fdisk help. When you do, a list of commands is displayed that you can use to perform actions with fdisk. These are shown in this example:

```text
Command (m for help): m
Command action
a	toggle a bootable flag
b	edit bsd disklabel
c	toggle the dos compatibility flag
d	delete a partition
l	list known partition types
m	print this menu
n	add a new partition
o	create a new empty DOS partition table
p	print the partition table
q	quit without saving changes
s	create a new empty Sun disklabel
t	change a partition’s system id
u	change display/entry units
v	verify the partition table
w	write table to disk and exit
x	extra functionality (experts only)
```

Command (m for help):

> CAUTION You can enter d to delete an existing partition. Be very careful about using this action. Any data on that partition will be lost! Once the changes are committed to disk, they are not reversible. You can back off from changes made with fdisk without committing them to disk by entering q. With fdisk, q is your friend!

Before creating a partition, you should enter p to view any existing partitions on the disk. This will help you determine if there is sufficient space and, if there is, what number must be assigned to a new partition created on the disk.

To create a new partition, you enter n. You can then specify whether you want to create a primary disk partition or an extended disk partition. Any hard disk in your system can have up to four partitions defined in its partition table. These can be either primary or extended partitions. If you intend to create four partitions or fewer, you can simply use primary partitions.

However, if you want to create more than four partitions on the disk, you must create at least one extended partition. Extended partitions are great. Within one extended partition, you can create many logical partitions. This allows you to get around the four-partition limitation. The general rule of thumb is to create your primary partitions first, then create your extended partition using the remaining space on the drive and create your logical partitions within it.

To create a primary partition, enter p when prompted. To create an extended partition, enter e. You are then prompted to specify a partition number, as shown in this example:

```text
Command (m for help): n
Command action
     e   extended
     p   primary partition (1-4)
P
Partition number (1-4): 1
```

You need to specify the next available partition number for the partition being created. In other words, if your disk already has two partitions on it, you would enter 3. In the preceding example, no partitions currently exist on the drive, so I’ve entered 1 to create the first primary partition. If you try to enter a partition number that’s already being used by an existing partition, the fdisk utility will complain!

At this point, you must specify the size of the partition. This is done by specifying the beginning and ending cylinders. You first specify the cylinder that you want to begin the partition on. By default, fdisk displays the next available cylinder. If you don’t have any partitions on the disk, this will be cylinder 1. If you already have partitions on the disk, the next unused cylinder will be listed. After specifying your start cylinder, you have several options for specifying the overall size of the partition, as shown here:

```text
Partition number (1-4): 1
First cylinder (1-1044, default 1): 1
Last cylinder, +cylinders or +size[K,M,G] (1-1044, default 1044):
```

You can:

- Enter the last cylinder to be used in the partition.
- Enter the size of the partition in gigabytes by entering **size**G. For **example**, you could create an **80GB** partition by entering **80G**.

After specifying the size, you should verify your new partition by entering p. This will display all partitions for the disk, as shown in the next example:

```text
Command (m for help): p

Disk /dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x165e0dd4

Device  Boot  Start  End  Blocks  Id  System
/dev/sdb1  1  8  64228+  83  Linux

Command (m for help): 
```

It's important to note that, at this point, the partition hasn't been written to disk. All changes are saved in memory before being committed to disk. This allows you to tweak your partitions before actually committing the changes.

Before committing the partition to disk, however, you may need to change the partition type. Notice in the preceding example that the partition being created is a standard Linux partition by default. Usually, this is sufficient. However, suppose you were creating a swap partition. You would need to use a different type of partition. This is done by entering t and then entering the ID of the partition type you want to change to. If you don't know the ID number of the partition type you want to use, you can enter l (lowercase L) to list all of the valid partition types and their associated ID numbers, as shown here:

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_405_0.png)

For example, the ID for a Linux swap partition is 82. To change the type of the partition, you could enter t and specify a partition ID of 82 if you wanted to change the partition to a swap partition.

You can also delete partitions using fdisk. To do this, enter d at the command prompt and then specify the partition number you want to delete. Remember, any data that resides on this partition will be lost once you commit the change to disk!

At this point, you're ready to commit your partition to disk. If you're unhappy with the partitioning proposal, you can always enter q to quit without applying the new partitions. If you are happy, however, you can apply your changes by entering w. This will commit the partition to disk and exit fdisk, as shown in this example:

```text
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

wsl:~ #
```

It's important to note here that you must reboot the system before the Linux kernel will recognize the partition changes you made with fdisk. However, you can also use the partprobe command at the shell prompt to force the kernel to recognize the new partition table without rebooting. The syntax is **partprobe -s**. The -s option causes the partprobe command to show a summary of devices and their partitions, as shown in this example:

```text
wsl:~ # partprobe -s
Warning: WARNING: the kernel failed to re-read the partition table on /dev/sda
(Device or resource busy). As a result, it may not reflect all of your changes until after reboot.

/dev/sdb: msdos partitions 1
wsl:~ #
```

The warning message about /dev/sda is displayed because the current directory (/root) in my shell session is on /dev/sda3, hence the device is busy. But I really don't care in this situation because my new partition resides in /dev/sdb, which was updated correctly.

Now that you know how to manage partitions with fdisk, let's next learn how to make a file system using mks.

## Building a File System with mkfs

Even though we've created a partition with fdisk, we can't use it yet. That's because it hasn't been formatted with a file system yet. This is accomplished using one of the several commands. In this part of the chapter, we will look at the following topics:

- Using mkfs
- Using mkreiserfs
- Creating xfs and vfat file systems
- Using mkswap

### Using mkfs

The mkfs utility is used to make an ext2, ext3, or ext4 file system on a partition. You can even use it to create a FAT file system on the partition (which is used by Windows and DOS). This utility is actually just a front end for the real commands that make each specific type of file system:

- /sbin/mkfs.minix
- /sbin/mkfs.ntfs
- /sbin/mkfs.bfs
