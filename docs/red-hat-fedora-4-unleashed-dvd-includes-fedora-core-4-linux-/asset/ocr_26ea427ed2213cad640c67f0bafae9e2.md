double-check), and the master/slave jumpers. If all these are fine, you might have a bad drive, or the two hard drives if made by different manufactures) might not be playing nice with each other (especially if they were made by different manufacturers).

To check further, reset the jumper of the new drive to make it the master drive, disconnect the old drive, and plug in the new one in its place. If the new drive is now correctly detected, suspect some incompatibility between the drives. Always make cable changes to the drives with the power off, or you will damage the drive.

> **TIP**
> 
> If you were to examine the partition table with a hexadecimal editor, you would find that with only 10 bits in which to store the partition's cylinder offset (an index to data on the disk); no disk can have any more than 1,024 cylinders.
> 
> One creative way to get around that limitation is to increase the number of heads so that the number of cylinders can remain small enough to fit the partition table. This scheme is known as Logical Block Addressing, or LBA. Modern BIOSes (post-1998 or so) support it, but older ones do not. But because Linux is capable of being told about the drive geometry at boot time, it is not as big a problem to Linux users as it is to users of other operating systems. For more detailed information, you can look at the Large Disk HOWTO and the BootPrompt HOWTO if you have problems with large hard disks.

# ## Creating the Partition Table and Formatting the Disk

Once installed and recognized by the BIOS, a partition table needs to be created. Use fdisk (or the program of your choice) to create a single partition on the drive, remembering to write the changes to the MBR before you exit the program (see “Creating the Partition Table,” earlier in this chapter).

Formatting the drive is next. Because we are creating a new ext3 file system, we use the j option, as

```
# mke2fs -cJ /dev/hdb1
```

Notice that we are checking the drive (using the -c option) for bad blocks as we format. Even though it adds considerable time to formatting the drive, an initial bad block check is always a good idea. The program will identify bad blocks and not use them; bad blocks would only corrupt our data if we didn't mark the file system to ignore them.

# ## Mount the New Partition and Populating It with the Relocated Files

For the example that follows, it is assumed that /home was a directory that was part of the partition mounted at /, not a separate partition to begin with.

Here, we create a temporary mount point and mount the new partition:

```
# mkdir /mnt/newpartition
# mount -t ext3 /dev/hdb1 /mnt/newpartition
```