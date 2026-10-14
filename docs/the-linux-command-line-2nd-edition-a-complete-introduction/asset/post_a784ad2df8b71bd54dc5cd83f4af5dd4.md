
in the interest of demonstration, we will change it to indicate a Linux partition. To do this, we must first find out what ID is used to identify a Linux partition. In the listing above, we see that the ID “b” is used to specify the existing partition. To see a list of the available partition types, we refer back to the program menu. There we can see the following choice:

```
1  list known partition types
```

If we enter “l” at the prompt, a large list of possible types is displayed. Among them we see “b” for our existing partition type and “83” for Linux.

Going back to the menu, we see this choice to change a partition ID:

```
t   change a partition's system id
```

We enter “t” at the prompt and enter the new ID:

```
Command (m for help): t
Selected partition 1
Hex code (type L to list codes): 83
Changed system type of partition 1 to 83 (Linux)
```

This completes all the changes that we need to make. Up to this point, the device has been untouched (all the changes have been stored in memory, not on the physical device), so we will write the modified partition table to the device and exit. To do this, we enter “w” at the prompt:

```
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.

WARNING: If you have created or modified any DOS 6.x
partitions, please see the fdisk manual page for additional
information.
Syncing disks.
[me@linuxbox ~]$
```

If we had decided to leave the device unaltered, we could have entered “q” at the prompt, which would have exited the program without writing the changes. We can safely ignore the ominous sounding warning message.

## Creating A New File System With mkfs

With our partition editing done (lightweight though it might have been) it's time to create a new file system on our flash drive. To do this, we will use mkfs (short for "make file system"), which can create file systems in a variety of formats. To create an ext3 file system on the device, we use the "-t" option to specify the "ext3" system type, followed by the name of the device containing the partition we wish to format:

```
[me@linuxbox ~]$ sudo mkfs -t ext3 /dev/sdb1
mke2fs 1.40.2 (12-Jul-2007)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
3904 inodes, 15608 blocks
780 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=15990784
2 block groups
8192 blocks per group, 8192 fragments per group
1952 inodes per group
Superblock backups stored on blocks:
8193

Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 34 mounts or
180 days, whichever comes first. Use tune2fs -c or -i to override.
[me@linuxbox ~]$
```

The program will display a lot of information when ext3 is the chosen file system type. To re-format the device to its original FAT32 file system, specify "vfat" as the file system type:

```
[me@linuxbox ~]$ sudo mkfs -t vfat /dev/sdb1
```

This process of partitioning and formatting can be used anytime additional storage devices are added to the system. While we worked with a tiny flash drive, the same process can be applied to internal hard disks and other removable storage devices like USB hard drives.

## Testing And Repairing File Systems

In our earlier discussion of the /etc/fstab file, we saw some mysterious digits at the end of each line. Each time the system boots, it routinely checks the integrity of the file systems before mounting them. This is done by the fsck program (short for “file system check”). The last number in each fstab entry specifies the order in which the devices are to be checked. In our example above, we see that the root file system is checked first, followed by the home and boot file systems. Devices with a zero as the last digit are not routinely checked.

In addition to checking the integrity of file systems, fsck can also repair corrupt file systems with varying degrees of success, depending on the amount of damage. On Unix-like file systems, recovered portions of files are placed in the lost+found directory, located in the root of each file system.

To check our flash drive (which should be unmounted first), we could do the following:

```
[me@linuxbox ~]$ sudo fsck /dev/sdb1
fsck 1.40.8 (13-Mar-2008)
e2fsck 1.40.8 (13-Mar-2008)
/dev/sdb1: clean, 11/3904 files, 1661/15608 blocks
```

In my experience, file system corruption is quite rare unless there is a hardware problem, such as a failing disk drive. On most systems, file system corruption detected at boot time will cause the system to stop and direct you to run fsck before continuing.

## What the fsck?

In Unix culture, the word “fsck” is often used in place of a popular word with which it shares three letters. This is especially appropriate, given that you will probably be uttering the aforementioned word if you find yourself in a situation where you are forced to run fsck.

## Formatting Floppy Disks

For those of us still using computers old enough to be equipped with floppy diskette
