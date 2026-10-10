table, the BSD disk label within the FreeBSD slice, and the filesystem within the BSD partitions.

# Using fdisk

Like the disk partitioning programs in other OSes, FreeBSD's `fdisk` lets you examine or edit the x86 partition table. This program can display information on a partition table, write a new partition table from data stored in a configuration file, or write data based on information it collects from you using a rigid prompting order. If you want to alter partitions in a more arbitrary manner, you should use `sysinstall` or a non-FreeBSD partitioning tool.

The `fdisk` command can be used with one of two syntax forms:

```
fdisk -f configfile [-itv] [disk]
fdisk [-B|a|stul] [-b bootcode] [-1234] [disk]
```

The first form collects data from a configuration file stored on disk (configfile). If you routinely partition disks that are identical in capacity, you might consider creating a file describing the layout of these disks and using this format of the command. The result can be quicker and less error-prone partitioning. The format of this file is described in the `fdisk` man page, so consult it if you want to use this option.

The second form of the command either displays information on the disk or enables you to edit the partition table. If you specify only the target disk (such as `/dev/ad0` for the first EIDE disk or `/dev/dal` for the second SCSI disk), `fdisk` displays the partition table information, thus:

```
# fdisk /dev/ad0
\*\*\*\*\*\* Working on device /dev/ad0 \*\*\*\*\*\*
parameters extracted from in-core disklabel are:
cylinders=784 heads=255 sectors/track=63 (16065 blks/cyl)

parameters to be used for BIOS calculations are:
cylinders=784 heads=255 sectors/track=63 (16065 blks/cyl)

Media sector size is 512
Warning: BIOS sector numbering starts with sector 1
Information from DOS bootblock is:
The data for partition 1 is:
sysid 12, (DOS or Windows 95 with 32 bit FAT, LBA)
start 63, size 4192902 (2047 Meg), flag 0
beg: cyl 0/ head 1/ sector 1;
end: cyl 260/ head 254/ sector 63
The data for partition 2 is:
sysid 165, (FreeBSD/NetBSD/386BSD)
start 4192965, size 8401995 (4102 Meg), flag 80 (active)
```