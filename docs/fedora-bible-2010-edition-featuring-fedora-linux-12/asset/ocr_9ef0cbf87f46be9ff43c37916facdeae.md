> NOTE: This procedure assumes that Fedora is already installed and working on the computer. If this is not the case, follow the instructions for adding a hard disk on your current operating system. Later, when you install Fedora, you can identify this disk when asked to partition your hard disk(s).

+   1. Install the hard disk into your computer. Follow the manufacturer's instructions for physically installing and connecting the new hard disk. If, presumably, this is a second hard disk, you may need to change jumpers on the hard disk unit itself to have it operate as a slave hard disk. You may also need to change the BIOS settings.

+   2. Boot your computer to Linux.

+   3. Determine the device name for the hard disk. As root user from a shell, type:

```
# dmesg | less
```

From the output, look for an indication that the new hard disk was found. For example, if it is a second hard disk, you should see sdb in the output. Be sure you identify the right disk or you will erase all the data from disks you probably want to keep!

> NOTE: Note that prior to Fedora 7, IDE hard drives began with /dev/hd and SCSI drives began with /dev/sd. Now, both IDE and SCSI drives begin with /dev/sd, as in /dev/sda and /dev/sdb.

+   4. Use the fdisk command to create partitions on the new disk. For example, if you are formatting the second hard disk (sdb), you could type the following:

```
# fdisk /dev/sdb
```

+   5. If the disk had existing partitions on it, you can change or delete those partitions now. Or, you can simply reformat the whole disk to blow everything away. Use p to view all partitions and d to delete a partition.

+   6. To create a new partition, type the following:

```
n
```

You are asked to choose an extended or primary partition.

+   7. To choose a primary partition, type the following:

```
p
```

You are asked the partition number.

+   8. If you are creating the first partition (or for only one partition), type the number 1:

```
1
```

You are asked to enter the first cylinder number (with 1 being the default).

+   9. To begin at the second cylinder, type the number 2 as follows:

```
2
```