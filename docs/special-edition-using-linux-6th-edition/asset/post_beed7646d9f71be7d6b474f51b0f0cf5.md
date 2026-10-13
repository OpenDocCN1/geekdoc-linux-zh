
| Device | Description |
|---|---|
| `/dev/sda` | First SCSI drive |
| `/dev/sdb` | Second SCSI drive |
| `/dev/sdc` | Third SCSI drive |

> **Note:** Some drives might be removable devices, such as Jaz and Zip drives.

When the drive is accessible as a device under Linux it can be partitioned in preparation for creating a filesystem. Like DOS, the utility for partitioning a hard drive is fdisk; however, the Linux version is much more powerful. The options available with the Linux version of fdisk are displayed in the Help menu as follows:

```text
# fdisk /dev/hda

Command (m for help): m
Command action
  a   toggle a bootable flag
  b   edit bsd disklabel
  c   toggle the dos compatibility flag
  d   delete a partition
  l   list known partition types
  m   print this menu
  n   add a new partition
  o   create a new empty DOS partition table
  p   print the partition table
  q   quit without saving changes
  t   change a partition’s system id
  u   change display/entry units
  v   verify the partition table
  w   write table to disk and exit
  x   extra functionality (experts only)

Command (m for help):
```

The steps for creating a new Linux partition are as follows:

1. Run fdisk on the new hard drive.
2. Examine any existing partitioning.
3. Create a new partition.
4. Select the partition type (primary, extended, or logical).
5. Select the partition number.
6. Select the beginning cylinder.
7. Select the ending cylinder or size.
8. Set the partition system ID.
9. Set the boot partition.
10. Write the new partition table.
11. Reboot the computer to update the partition table.

If you choose to use the Debian-distributed cfdisk, follow these steps:

1. Run cfdisk on the new hard drive.
2. Examine any existing partitions and delete if desired.
3. Select free space to use with the up and down arrows.
4. Select New using the left and right arrows.
5. Select Primary, Logical, or Cancel.
6. Select size of partition in Mb (max size is shown).
7. Set the boot partition (if necessary).
8. Write the new partition table.
9. Reboot the computer to update the partition table.

The following sections provide a closer look at each of these steps under fdisk. (The cfdisk utility will not be covered in detail, but is similar, as a comparison with the previous steps shows.)

## STEP 1

Run the fdisk utility and specify which hard drive (by device name) you want to partition.
The following is displayed on the screen:

```text
# fdisk /dev/hda
Command (m for help): m
```

## STEP 2

The letter p is used to display the current partition table, if any exists. If no partitions are present, the following is displayed onscreen:

```text
Command (m for help): p

Disk /dev/hda: 32 heads, 63 sectors, 827 cylinders
Units = cylinders of 2016 * 512 bytes

   Device Boot    Start    End   Blocks   Id System
```

If the partitions are already configured, the following is displayed:

```text
Command (m for help): p

Disk /dev/hda: 32 heads, 63 sectors, 827 cylinders
Units = cylinders of 2016 * 512 bytes

   Device Boot    Start    End   Blocks   Id System
/dev/hda1          1       17    17104+  82 Linux Swap
/dev/hda2   *     18      827   816480   83 Linux Native
```

## STEP 3

Create a new partition as follows:

```text
Command (m for help): n
Command action
    e  extended
    p  primary partition (1-4)
```

## STEP 4

Select a partition type. Unlike DOS, where only one primary partition is allowed, Linux supports a hard drive of all primary partitions, or any combination of primary or extended partitions, with logical partitions inside the extended partitions. Each disk can have up to four primary partitions. If you need more partitions, you must give up one primary partition to create an extended partition. Although a primary partition is formatted for use with an operating system, an extended partition is not handled like this. Within an extended partition, you create logical partitions, which are formatted. You must plan your use of partitions with some care, because although Linux will boot from a logical partition inside an extended partition, some operating systems require a primary partition from which to boot.

```text
Command (m for help): n
Command action
    e  extended
    p  primary partition (1-4)
p
Partition number (1-4):
```

## STEP 5

Select the partition number. If this is to be the first partition on this drive, select 1:

```text
Command (m for help): n
Command action
    e  extended
    p  primary partition (1-4)
p
Partition number (1-4): 1
```

## STEP 6

Select the first cylinder number:

```text
Command (m for help): n
Command action
    e  extended
    p  primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-827): 1
```

## STEP 7

Select the last desired cylinder number, or select the partition size in cylinders, megabytes, or kilobytes:

```text
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-827): 1
Last cylinder or +size or +sizeM or +sizeK (1-17): 17
```

After the partition type, partition number, first cylinder, and last cylinder are set, the main fdisk prompt is displayed as follows:

```text
Command (m for help):
```

## STEP 8

Set the partition system ID. For a Linux filesystem, this is always type 83, Linux native:

```text
Command (m for help): t
Partition number: 1
Hex code (type L to list codes): L

0 Empty          b  Win95 FAT32       75 PC/IX          a7 NEXTSTEP
1 DOS 12-bit     c  Win95 FAT32 (LB   80 Old MINIX      a9 NetBSD
2 XENIX root     e  Win95 FAT16 (LB   81 Linux/MINIX    b7 BSDI fs
3 XENIX usr      f  Win95 Extended    82 Linux swap     b8 BSDI swap
4 DOS 16-bit <32M 40 Venix 80286      83 Linux native   c7 Syrinx
5 Extended       51 Novell?           85 Linux extended db CP/M
6 DOS 16-bit >=32M 52 Microport        93 Amoeba         e1 DOS access
7 OS/2 HPFS       63 GNU HURD         94 Amoeba BB      e3 DOS R/O
8 AIX             64 Novell Netware   a5 BSD/386        f2 DOS secondary
9 AIX bootable    65 Novell? Netware  a6 OpenBSD        ff BB
a OS/2 Boot Manager

Hex code (type L to list codes):
```

Enter type 83 for a Linux native, second extended (ext2) filesystem:

```text
Hex code (type L to list codes): 83

Command (m for help):
```

> **Tip**  Repeat steps 3–8 for each additional partition. Be sure to make at least one partition a type 82, Linux swap.

## STEP 9

Write out new partition table information to the hard drive as follows:

```text
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

After the new partition table is written to disk, reboot your system to ensure that the partition table is updated. The newly created partitions are now ready for a Linux filesystem.

> **Note**
> 
> You can examine the existing partition of any drive by running fdisk with the option -l. For example, `fdisk -l /dev/hda` displays the existing partitions on the first IDE drive on the primary controller. You can display the partitions for all hard drives by just supplying the `-l` option without specifying any particular hard drive.

## Linux Filesystems

Even though the newly added drive is now recognized by the operating system, it’s not usable until it is partitioned and a filesystem is created on it. The default filesystem for Linux is the extended type-2 filesystem (ext2). Characteristics of an ext2 filesystem are listed in Table 9.3.

**Table 9.3. Second Extended (ext2) Filesystem Characteristics**

| Characteristic | Limit |
|---|---|
| Maximum filesystem size | 4 terabytes |
| Maximum file size | 2 gigabytes |
| Maximum filename length | 255 characters |
| Minimum block size | 1,024 bytes |
| Default inode allocation | 1 per 4,096 bytes of partition space |

The filesystem structure is built when the *make filesystem* utility (mkfs) is run. This utility is actually just a front-end program that calls subordinate routines for filesystem creation. When making an ext2 filesystem, the mkfs utility actually calls mke2fs to create the correct filesystem structure. After the filesystem structure is created, it cannot be modified without reformatting the partition, or—in other words—remaking a new filesystem with the mkfs utility.

> **Caution**
> 
> The mkfs utility completely erases all data. You are not prompted to continue. It runs without any user intervention. Use it with caution.
