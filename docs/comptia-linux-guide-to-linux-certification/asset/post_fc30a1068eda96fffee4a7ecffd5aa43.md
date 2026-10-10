
Note from the preceding output that the `fdisk` command displays a prompt for the user to accept *fdisk* commands; a list of possible *fdisk* commands can be seen if the user presses the **m** key at this prompt, as shown in the following example:

```text
Command (m for help): m
Help:

DOS (MBR)
    a    toggle a bootable flag
    b    edit nested BSD disklabel
    c    toggle the dos compatibility flag

Generic
    d    delete a partition
    l    list known partition types
    n    add a new partition
    p    print the partition table
    t    change a partition type
    v    verify the partition table

Misc
    m    print this menu
    u    change display/entry units
    x    extra functionality (experts only)

Save & Exit
    w    write table to disk and exit
    q    quit without saving changes

Create a new label
    g    create a new empty GPT partition table
    G    create a new empty SGI (IRIX) partition table
    o    create a new empty DOS partition table
    s    create a new empty Sun partition table
Command (m for help):
```

To print a list of the partitions currently set on /dev/sda, you could press the **p** key at the fdisk prompt:

```text
Command (m for help): p

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0000996b
```

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| /dev/sda1 | | 2048 | 4196351 | 2097152 | 82 | Linux swap / Solaris |
| /dev/sda2 | * | 4196352 | 30679039 | 13241344 | 83 | Linux |
| /dev/sda3 | | 30679040 | 41943039 | 5632000 | 83 | Linux |

```text
Command (m for help):
```

Notice that the device names appear on the left side of the preceding output, including the partition that is booted to (/dev/sda2), the start and end location of partitions on the physical hard disk (start and end cylinders), the number of total blocks for storing information in the partition, as well as the partition type and description (83 is a Linux partition, 82 is a Linux swap partition). A Linux partition can contain a Linux filesystem—for example, ext4.

To remove the /dev/sda3 partition and all the data contained on the filesystem within, you could use the d key noted earlier:

```text
Command (m for help): d

Partition number (1-3, default 3): 3

Command (m for help): p

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0000996b
```

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| /dev/sda1 | | 2048 | 4196351 | 2097152 | 82 | Linux swap / Solaris |
| /dev/sda2 | * | 4196352 | 30679039 | 13241344 | 83 | Linux |

```text
Command (m for help):
```

To create an extended partition using the fourth primary partition (/dev/sda4) with two logical drives (/dev/sda5 and /dev/sda6), you could use the n key noted earlier and specify the partition to create, the starting cylinder on the hard disk, and the size in blocks (+5G makes a 5GB partition):

```text
Command (m for help): n

Partition type:
  p  primary partition (2 primary, 0 extended, 2 free)
  e  extended
Select (default p): e

Partition number (3,4, default 3): 4

First sector (30679040-41943039, default 30679040): 30679040

Last sector, +sectors or +size{K,M,G,T,P} (30679040-41943039, default 41943039): +5G

Created a new partition 4 of type 'Extended' and of size 5 GiB.
```

```text
Command (m for help): p
Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0000996b

  Device  Boot Start End  Blocks  Id System
  /dev/sda1  2048 4196351 2097152 82 Linux swap / Solaris
  /dev/sda2  *  4196352 30679039 13241344 83 Linux
  /dev/sda4  30679040 41164799 5242880 5 Extended
```

```text
Command (m for help): n
Partition type:
  p  primary (2 primary, 1 extended, 1 free)
  l  logical (numbered from 5)
Select (default p): l

Adding logical partition 5
First sector (30681088-41164799, default 30681088): 30681088
Last sector, +sectors or +size{K,M,G,T,P} (30681088-41164799, default 41164799): +3GB

Created a new partition 5 of type 'Linux' and of size 2.8 GiB.
```

```text
Command (m for help): p
Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0000996b

  Device  Boot Start End  Blocks  Id System
  /dev/sda1  2048 4196351 2097152 82 Linux swap / Solaris
  /dev/sda2  *  4196352 30679039 13241344 83 Linux
  /dev/sda4  30679040 41164799 5242880 5 Extended
  /dev/sda5  30681088 36540415 2929664 83 Linux
```

```text
Command (m for help): n
Partition type:
  p  primary (2 primary, 1 extended, 1 free)
  l  logical (numbered from 5)
Select (default p): l

Adding logical partition 6
First sector (36542464-41164799, default 36542464): 36542464
Last sector, +sectors or +size{K,M,G,T,P} (36542464-41164799, default 41164799): +2G

Created a new partition 6 of type 'Linux' and of size 2 GiB.
```

```text
Command (m for help): p
Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0000996b
```

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| /dev/sda1 | | 2048 | 4196351 | 2097152 | 82 | Linux swap / Solaris |
| /dev/sda2 | * | 4196352 | 30679039 | 13241344 | 83 | Linux |
| /dev/sda4 | | 30679040 | 41164799 | 5242880 | 5 | Extended |
| /dev/sda5 | | 30681088 | 36540415 | 2929664 | 83 | Linux |
| /dev/sda6 | | 36542464 | 40736767 | 2097152 | 83 | Linux |

```text
Command (m for help):
```

Notice from the preceding output that the default type for new partitions created with fdisk is 83 (Linux); to change this, you can type the t key at the fdisk prompt. To change the /dev/sda6 partition to type 82 (Linux swap), you can do the following at the fdisk prompt:

```text
Command (m for help): t
Partition number (1,2,4-6, default 6): 6
Hex code (type L to list all codes): L
```

| Hex | Name | Hex | Name | Hex | Name | Hex | Name |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | Empty | 24 | NEC DOS | 81 | Minix / old lin | bf | Solaris |
| 1 | FAT12 | 39 | Plan 9 | 82 | Linux swap / So | c1 | DRDOS/sec (FAT- |
| 2 | XENIX root | 3c | PartitionMagic | 83 | Linux | c4 | DRDOS/sec (FAT- |
| 3 | XENIX usr | 40 | Venix 80286 | 84 | OS/2 hidden C: | c6 | Dell /PTOS / |
| 4 | FAT16 <32M | 41 | PPC PReP Boot | 85 | Linux extended | c7 | Syrrix |
| 5 | Extended | 42 | SFS | 86 | NTFS volume set | da | Non-FTS data |
| 6 | FAT16 | 4d | QNX.x | 87 | NTFS volume set | db | CP/M / CTOS / . |
| 7 | HPFS/NTFS | 4e | QNX.x 2nd part | 88 | Linux plaintext | de | Dell Utility |
| 8 | AIX | 4f | QNX.x 3rd part | 8e | Linux LVM | df | Boot It |
| 9 | AIX bootable | 50 | OnTrack DM | 93 | Amoeba | e1 | DOS access |
| a | DOS/2 Boot Manag | 51 | OnTrack DM6 Aux | 94 | Amoeba BBT | e3 | DOS R/O |
| b | W95 FAT32 | 52 | CP/R | 9f | BSD/OS | e4 | SpeedStor |
| c | W95 FAT32 (LBA) | 53 | OnTrack DM6 Aux | a0 | IBM Thinkpad hi | eb | BeOS fs |
| e | W95 FAT16 (LBA) | 54 | OnTrackDM6 | a5 | FreeBSD | ee | GPT |
| f | W95 Ext-d (LBA) | 55 | EZ-Drive | a6 | OpenBSD | ef | EFI (FAT-12/16/ |
| 10 | OPUS | 56 | Golden Bow | a7 | NextSTEP | f0 | Linux/PA-RISC b |

```text
Hex code (type L to list all codes): 82

Changed type of partition ‘Linux’ to ‘Linux swap / Solaris’.

Command (m for help): p

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x0000996b
```

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| /dev/sda1 | | 2048 | 4196351 | 2097152 | 82 | Linux swap / Solaris |
| /dev/sda2 | * | 4196352 | 30679039 | 13241344 | 83 | Linux |
| /dev/sda4 | | 30679040 | 41164799 | 5242880 | 5 | Extended |
| /dev/sda5 | | 30681088 | 36540415 | 2929664 | 83 | Linux |
| /dev/sda6 | | 36542464 | 40736767 | 2097152 | 82 | Linux swap / Solaris |

```text
Command (m for help):
```

Finally, to save partition changes to the hard disk and attempt to reload the new partition information back into memory, simply use the w key at the fdisk prompt:

```text
Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Re-reading the partition table failed.: Device or resource busy

The kernel still uses the old table. The new table will be used at the next reboot or after you run partprobe(8) or kpartx(8).

[root@server1~]#
```

If the fdisk command indicates that the new partition information must be reloaded manually (as in the preceding example), simply reboot your machine. This is the most reliable way to ensure that the MBR is reloaded into memory successfully. For this reason, it is good form to always reboot your machine after running fdisk.

An easier alternative to fdisk is the cfdisk utility. When you run the cfdisk command, you see the interactive graphical utility shown in Figure 5-7. You can use this utility to
