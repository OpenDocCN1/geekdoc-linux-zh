# Naming conventions for partitions

DOS partitions are indicated by letters, such as C:, D:, and so on. Under Linux, device names are used instead. With fdisk -l you can obtain a listing of all existing partitions on the first two IDE and the first eight SCSI hard disks. The program displays all partitions (DOS, OS/2, Linux, and so on). On a computer with three disks, this might look as follows:

```
root# fdisk -l
Disk/sda: 64 bytes, 32 sectors, 116 cylinders
Units = cylinders of 2048 * 512 bytes
Device  Boot  Start  End Blocks Id System
/dev/sda1 *       1      1    1 118768 6 DOS 16-bit  >=32M
```

```
Disk/sdb: 64 heads, 32 sectors, 116 cylinders
Units = cylinders of 2048 * 512 bytes
Device  Boot  Start  End Blocks Id System
/dev/db1       1      1   116 118768 6 DOS 16-bit  >=32M
The number of cylinders for this disk is set to 1029,
This is larger than 1024, and may cause problems with some software.
```

```
Disk/sdc: 64 heads, 32 sectors, 1029 cylinders
Units = cylinders of 2048 * 512 bytes
Device  Boot  Start  End Blocks Id System
/dev/sdc1       1      1   200 204784 6 DOS 16-bit  >=32M
```

The first two (116 Mbytes) are completely filled with one DOS partition. Each on the first hard disk (1.03 Gbytes). has only the first 200 Mbytes which are reserved for DOS, and the remaining hard disk space is free for Linux partitions.
The above print indicates the naming conventions for hard disk partitions; normal hard partitions (AT or IDE bus) are named dev/hdx, where x is a letter for the hard disk (a for the first disk, b for the second disk, and so on). SCSI hard disks are named analogously, that is, dev/sdy.

The rule for numbering partitions is that 1 to 4 are reserved for primary or extended partitions. figures from 5 onwards for logical partitions within the extended partitions. For this reason, there are frequently 'holes' in the numbering (such as hda1 for a primary, hda2 for an extended and hda5 for the first logical partition).

# Device names of hard disk partitions

+   - dev/hda  the first IDE disk
- dev/hda1 the first primary partition of the first IDE disk
- dev/hda2 the second primary partition of the first IDE disk
- dev/hda5 the first logical partition of the first IDE disk
- dev/hda8 the fourth logical partition of the first IDE disk
- dev/hdb  the second IDE disk
- dev/hdb1 the first primary partition of the second IDE disk