# Adding a New Disk Drive to a RHEL 9 System

```
/dev/sda /dev/sda1 /dev/sda2 /dev/sdb
```

The new hard drive has been assigned to the device file /dev/sdb. The drive has no partitions shown (because we have yet to create any).

At this point, we can create partitions and file systems on the new drive and mount them for access or add the disk as a physical volume as part of a volume group. To perform the former continue with this chapter; otherwise, read “Adding a New Disk to a RHEL 9 Volume Group and Logical Volume” for details on configuring Logical Volumes.

# 31.3 Creating Linux Partitions

The next step is to create one or more Linux partitions on the new disk drive. This is achieved using the fdisk utility, which takes as a command-line argument the device to be partitioned:

```
# fdisk /dev/sdb
```

```
Welcome to fdisk (util-linux 2.37.4).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0x64d68d00.

Command (m for help):
```

To view the current partitions on the disk, enter the p command:

```
Command (m for help): p
Disk /dev/sdb: 14.46 GiB, 15525216256 bytes, 30322688 sectors
Disk model: USB 2.0 FD
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x64d68d00
```

As we can see from the above fdisk output, the disk currently has no partitions because it was previously unused. The next step is to create a new partition on the disk, a task which is performed by entering n (for new partition) and p (for primary partition):

```
Command (m for help): n
Partition type
  p   primary (0 primary, 0 extended, 4 free)
  e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1):
```

In this example, we only plan to create one partition, which will be partition 1. Next, we need to specify where the partition will begin and end. Since this is the first partition, we need it to start at