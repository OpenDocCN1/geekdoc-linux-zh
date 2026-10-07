# CHAPTER 10 Managing the Filesystem

To check further, reset the jumper of the new drive to make it the master drive, disconnect the old drive and plug in the new one in its place. If the new drive is now correctly detected, suspect some incompatibility between the drives. Always make cable changes to the drives with the power off, or you will damage the drive.

> > TIP If you were to examine the partition table with a hexadecimal editor, you would find that only 10 bits in which to store the partition's cylinder offset (an index to data on the disk), no disk can have more than 1024 cylinders.
One way to get around it is to increase the number of heads so that the cylinders can remain small enough to fit the partition table. This scheme is known as Logical Block Addressing, or LBA. Modern BioES (post-1998 or so) supports it, but older ones do not. because Linux is capable of being told about the drive geometry at boot time, it isn't as big as a problem to Linux as it is to users of other operating systems. For more detailed information, you can look at the Large Disk HOWTO and the BootPrompt HOWTO if you have problems with large hard disks.

# Creating the Partition Table and Formatting the Disk

Once installed and recognized by the BIOS, a partition table needs to be created. Use fdisk (or the program of your choice) to create a single partition on the drive, remember-writing the changes to the MBR before you execute the program (“Creating the Partition Table,” earlier in this chapter).

Formatting the drive is next. Because we are creating a new ext3 filesystem, we use the -j option, like this:

```
# mke2fs -c -j /dev/hdb1
```

Notice that we are checking the drive (using the -c option) for bad blocks as we format. Even though it adds considerable time to formatting the drive, an initial bad block check is always a good idea. The program will identify bad blocks and not use them; they would only corrupt our data if we didn't ignore them. Even though it adds considerable time to formatting the drive, an initial bad block check is always a good idea.

# Mount the New Partition and Populating It with the Relocated Files

Next, we create a temporary mount point and mount the new partition:

```
# mkdir /mnt/newpartition
```

```
# mount -t ext3 /dev/hdb1 /mnt/newpartition
```

It's now time to copy all the files from /home to /mnt/newpartition. It's important that we preserve the time and date stamp for the files and the permissions. We're copying entire