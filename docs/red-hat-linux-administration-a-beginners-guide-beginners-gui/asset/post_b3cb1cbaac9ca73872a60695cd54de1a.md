
| Partition | Description |
| :--- | :--- |
| / | The root partition is for those core system files necessary to bring a system to single-user mode. Once established, the partition’s contents shouldn’t vary at all and definitely shouldn’t need to grow. The intent is to isolate this file system from other file systems, to prevent interference with core operations. |
| /usr | This partition is used for system software such as user tools, compilers, X, and so forth. Because you may one day need to find a bigger home for your system software, you put this in a separate partition. |
| /var | The /var partition is used to hold files that change a lot—this usually includes spool directories (mail, print, etc.) and log files. What makes this partition worrisome is that external events can make its contents grow beyond allocated space. Log files from a web server, for instance, can grow quickly and beyond your control. To keep these files from spilling over into the rest of your system, it’s wise to keep this partition separate. (A type of attack via the network can be mounted by artificially generating so much activity on your server that the disk fills up with system logs and the system behaves unreliably.) |
| /tmp | Similar to /var, files in /tmp can unexpectedly consume substantial space. This can occur when users leave files unattended or application programs create large temporary files. Either way, maintaining this partition is a good safety mechanism. |
| /home | If you need to store home directories on your disk, especially for users whose disk consumption needs to be restricted, you’ll definitely want to have this separate partition. |
| swap | The swap partition is necessary to hold virtual memory. Although it isn’t required, swap is often a good idea in case you do exhaust all your physical RAM. In general, you’ll want this partition to be the same size as your RAM. |

## Table 7-5 Partition Descriptions and Configuration

The last partition would be an “extended” partition, unseen by the user but able to contain additional partitions.

The next question: Which partition number? (You can see the limit of four primary partitions as part of the question.) You start with one, picking the default starting cylinder, and then specify that you want 25MB allocated to it.

To create the second partition for swap, type the following:

```
Command (m for help): n
Command action
     e   extended
     p   primary partition (1-4)
p
Partition number (1-4): 2
First cylinder (68-665, default 68): 68
Last cylinder or +size or +sizeM or +sizeK (52-665, default 665): +16M
Command (m for help):
```

This time, the prompts are identical to those used for the previous partition, with slightly different numbers. However, by default, **fdisk** is creating ext2 partitions. You need this partition to be of type **swap**. To do this, use the t (change partition type) command:

```
Command (m for help): t
Partition number (1-4): 2

Hex code (type L to list): L

1  Empty
2  FAT12
3  XENIX root
4  XENIX usr
5  FAT16 <32M>
6  Extended
7  FAT16
8  HPFS/NTFS
9  AIX bootable
a  OS/2 Boot Manager
b  Win95 FAT32
c  Win95 FAT32 (LBA)
d  Win95 FAT16 (LBA)
e  Win95 Ext'd (LBA)
10 OPUS
11 Hidden FAT12
12 Compq diagnost
14 Hidden FAT16
16 Hidden FAT16
17 Hidden HPFS/NTFS
18 AST Windows swap
24 NEC DOS
3c PartitionMagic
40 Venix 80286
41 PPC PreP Boot
42 SFS
4d QNX4.x
4e QNX4.x 3rd part
50 OnTrack IM
51 OnTrack DM6 Aux
52 OS/2
53 OnTrack DM6 Aux
54 OnTrack DM6
55 EZ-Drive
56 Golden Bow
5c Priam Edisk
61 SpeedStor
63 GNU HURD or Sys
64 Novell Netware
65 Novell Netware
70 DiskSecure Mult
75 PC/IX
80 Old Minix
81 Minix / old Lin
82 Linux swap
83 Linux
84 OS/2 hidden C:
85 Linux extended
86 NTFS volume set
87 NTFS volume set
93 Amoeba
94 Amoeba BBT
a0 IBM Thinkpad hi
a5 BSD/386
a6 OpenBSD
a7 NextSTEP
b7 BSDI fs
b8 BSDI swap
c1 DRDOS/secFAT-32
c4 DRDOS/secFAT-32
c6 DRDOS/secFAT-32
c7 Syrtex
db CP/M / CTOS /
e1 DOS access
e3 DOS R/O
e4 SpeedStor
eb BeOS fs
ef SpeedStor
f2 DOS secondary
fe LANstep
ff BBT

Hex code (type L to list codes): 82

Changed system type of partition 2 to 82 (Linux swap)

Command (m for help):
```

The first question is, of course, what partition number do you want to change to? Since you want the second partition to be the swap, you entered **2**. The next prompt is a bit more cryptic: the hexadecimal code for the correct partition. Since people don’t remember hex codes very well, the L command lists all available partition types. You spot 82 for Linux Swap, so enter that, and you’re done.

### NOTE

> It used to be that Linux’s swap partition was limited to 128M. This is no longer the case. You can create a single swap partition as large as 2GB. You can create multiple swap partitions if you like.

Now to create /usr. Make it 100MB in size:

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
p
Partition number (1-4): 3
First cylinder (85-665, default 85): 85
Last cylinder or +size or +sizeM or +sizeK (85-665, default 665): +100M
Command (m for help):
```

So at this point, you have three partitions: **root**, **swap**, and **usr**. You can see them by entering the **p** command:

```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hdb1 | | 1 | 51 | 25672+ | 83 | Linux |
| /dev/hdb2 | | 52 | 84 | 16632 | 82 | Linux swap |
| /dev/hdb3 | | 85 | 288 | 102816 | 83 | Linux |

Command (m for help):
```

Now you need to create the extended partition to accommodate /tmp, /var, and /home. Do so using the **n** command, just as for any other new partition:

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
e
Partition number (1-4): 4
First cylinder (289-665, default 289): 289
Last cylinder or +size or +sizeM or +sizeK (289-665, default 665): 665
Command (m for help):
```

Instead of designating a megabyte value for the size of this partition, you enter the last cylinder number, thus taking up the remainder of the disk. Let’s see what this looks like:

```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hdb1 | | 1 | 51 | 25672+ | 83 | Linux |
| /dev/hdb2 | | 52 | 84 | 16632 | 82 | Linux swap |
| /dev/hdb3 | | 85 | 288 | 102816 | 83 | Linux |
| /dev/hdb4 | | 289 | 665 | 190008 | 5 | Extended |

Command (m for help):
```

Now you’re ready to create the last three partitions:

```
Command (m for help): n
First cylinder (289-665, default 289): 289
Last cylinder or +size or +sizeM or +sizeK (289-665, default 665): +100M
Command (m for help): n
First cylinder (493-665, default 493): 493
Last cylinder or +size or +sizeM or +sizeK (493-665, default 665): +45M
Command (m for help): n
First cylinder (585-665, default 585): 585
Last cylinder or +size or +sizeM or +sizeK (585-665, default 665): 665
Command (m for help):
```

Note that for the very last partition, you again specified the last cylinder instead of a megabyte value, so that you are sure that you have allocated the entire disk. One last p command shows you what your partitions now look like:

```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

Device Boot Start End Blocks Id System
/dev/hdb1 1 51 25672+ 83 Linux
/dev/hdb2 52 84 16632 82 Linux swap
/dev/hdb3 85 288 102816 83 Linux
/dev/hdb4 289 665 190008 5 Extended
/dev/hdb5 289 492 102784+ 83 Linux
/dev/hdb6 493 584 46336+ 83 Linux
/dev/hdb7 585 665 40792+ 83 Linux
Command (m for help):
```

Perfect. Commit the changes to disk and quit the fdisk utility by using the w (write table to disk and exit) command:

```
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks.
WARNING: If you have created or modified any DOS 6.x
partitions, please see the fdisk manual page for additional
information.
[root@tedford /root]#
```

If you needed to write an /etc/fstab file yourself for this configuration, it would look something like this:
