Our new disk is too damn small to be usefully partitioned, however—whether to anticipate additional swap space needs, or simply to allow multiple virtual disks. But let's get started:

```
# fdisk /dev/hdb

Command (m for help): m
Command action
a  toggle a bootable flag
b  edit bsd disklabel
c  toggle the dos compatibility flag
d  delete a partition
l  list known partition types
m  print this menu
n  add a new partition
o  create a new empty DOS partition table
p  print the partition table
q  quit without saving changes
s  create a new empty Sun disklabel
t  change a partition's system id
u  change display/entry units
v  verify the partition table
w  write table to disk and exit
x  extra functionality (experts only)
```

As you can see, there are many options within fdisk. The most important commands are d (delete a partition), p (print partition table), n (add a new partition), and w (write partition information and quit).

3. The process of formatting a disk without any partitions is quite straightforward, but let's start by looking at the device itself:

```
Command (m for help): p

Disk /dev/hdb: 16 heads, 63 sectors, 507 cylinders
Units = cylinders of 1008 * 512 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hdb1 | 1 | 507 | 255496+ | b | FAT32 |

There's a problem lurking here: We don't want the disk to be a FAT32 disk (a Windows format), but rather a Unix disk. We'll need to delete the existing partition and write a new one of the appropriate format:

```
Command (m for help): d
Partition number (1-4): 1

Command (m for help): p

Disk /dev/hdb: 16 heads, 63 sectors, 507 cylinders
Units = cylinders of 1008 * 512 bytes
```