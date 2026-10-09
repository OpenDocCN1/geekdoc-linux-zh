P
Selected partition 3
First cylinder (828-1310, default 828):
Using default value 828
Last cylinder or +size or +sizeM or +sizeK (828-1224, default 1224):
Using default value 1224

Command (m for help): p


Disk /dev/hda: 10.1 GB, 10141286400 bytes
240 heads, 63 sectors/track, 1310 cylinders
Units = cylinders of 15120 * 512 = 7741440 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 14 | 105808+ | 83 | Linux |
| /dev/hda2 |  | 15 | 827 | 6146280 | 83 | Linux |
| /dev/hda3 |  | 828 | 1224 | 3001320 | 83 | Linux |
| /dev/hda4 |  | 1225 | 1310 | 650160 | f | Win95 Ext'd (LBA) |
| /dev/hda5 |  | 125 | 1310 | 650128+ | 82 | Linux swap |

+   3. After the partition is created, it must be assigned a file system type. Use the **t** command to enter the file system type menu.
4. Type **3** to indicate the third partition.
5. Type **L** to display a list of the possible file system types. Select **83** for a **Linux** type partition.

Command (m for help): t
Partition number (1-5): 3
Hex code (type L to list codes): L

|  |  |  |  |
|---|---|---|---|
| 0 Empty1 | 1c Hidden Win95 FA | 70 DiskSecure Mult | bb Boot Wizard hid |
| 1 FAT12 | 1e Hidden Win95 FA | 75 PC/IX | be Solaris boot |
| 2 XENIX root | 24 NEC DOS | 80 Old Minix | c1 DRDOS/sec (FAT- |
| 3 XENIX usr | 39 Plan 9 | 81 Minix / old Lin | c4 DRDOS/sec (FAT- |
| 4 FAT16 <32M | 3c PartitionMagic | 82 Linux swap | c6 DRDOS/sec (FAT- |
| 5 Extended | 40 Venix 80286 | 83 Linux | c7 Syrinx |
| 6 FAT16 | 41 PPC PreP Boot | 84 OS/2 hidden C: | da Non-FS data |
| 7 HPFS/NTFS | 42 SFS | 85 Linux extended | db CP/M / CTOS / |
| 8 AIX | 4d QNX4.x | 86 NFS volume set | de Dell Utility |
| 9 AIX bootable | 4e QNX4.x 2nd part | 87 NTFS volume set | df BootIt |
| a OS/2 Boot Manag | 4f QNX4.x 3rd part | 8e Linux LVM | e1 DOS access |
| b Win95 FAT32 | 50 OnTrack DM | 93 Amoeba | e3 DOS R/O |
| c Win95 FAT32 (LB | 51 OnTrack DM6 Aux | 94 Amoeba BBT | e4 SpeedStor |
| e Win95 FAT16 (LB | 52 CP/M | 9f BSD/OS | eb BeOS fs |
| f Win95 Ext'd (LB | 53 OnTrack DM6 Aux | a0 IBM Thinkpad hi | ee EFI GPT |
| 10 OPUS | 54 OnTrackDM6 | a5 FreeBSD | ef EFI (FAT-12/16/ |
| 11 Hidden FAT12 | 55 EZ-Drive | a6 OpenBSD | f0 Linux/PA-RISC b |
| 12 Compaq diagnos | 56 Golden Bow | a7 NextStep | f1 Linux swaps |
| 14 Hidden FAT16 <3 | 5c Priam Edisk | a8 Darwin UFS | f4 Speedstor |
| 16 Hidden FAT16 | 61 SpeedStor | a9 NetBSD | f2 DOS secondary |
| 17 Hidden HPFS/NTF | 63 GNU HURD or Sys | ab Darwin boot | fd Linux raid au |
| 18 AST SmartSleep | 64 Novell Netware | b7 BSDI fs | fe LANstep |
| 1b Hidden Win95 FA | 65 Novell Netware | b8 BSDI swap | ff BBT |

Hex code (type L to list codes): 83
Changed system type of partition 3 to b (Win95 FAT32)


The partition is created with a file system type of Linux.

Command (m for help): p