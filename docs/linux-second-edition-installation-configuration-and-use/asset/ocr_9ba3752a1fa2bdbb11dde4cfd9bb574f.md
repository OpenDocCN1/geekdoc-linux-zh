# CREATING LINUX PARTITIONS 41

2048 × 512 Bytes ≈ 1 Mbyte. The size can also be specified using the syntax +nM
to make a partition nMbytes big.

After the definition of a new partition, the whole partition table can be dis-
played with [P] (print). After this, further partitions can be defined, existing ones
deleted, and so on.

+   Memorize the names of your newly created partitions, or write them down.
During the installation process, you will need to remember these device names
(for example, /dev/sdc) more than once.

To create a swap partition, the type of a newly created partition must be
changed, using ① (type), from 'Linux native' (83) to 'Linux swap' (82).
The following printout shows on the third SCSI disk, which contained only
e primary DOS partition, two further partitions were created (250 Mbytes
to the system and 150 Mbytes for data), plus an extended partition occupying the
entiring storage area, and within the latter, a logical partition as a small swap\partition (16 Mbytes).

```
root# fdisk /dev/sdc
The number of cylinders for this disk is set to 1029.
This is larger than 1024, and may cause problems with some software.
```

```
Command (m for help): p
Disk /sdc: 64 sectors, 32 sectors, 1029 cylinders
Units = 2048 * 512 bytes
```

| Device Boot Begin Start End Blocks Id System |
|---|---|---|---|---|---|---|
| /dev/sdc1 1 | 1 | 20478 | 6 DOS 16-bit >=32M |

```
Command (m for help): m
Command action
a toggle a bootable flag
toggle the dos compatibility flag
de delete a partition
l list known partition types
mp print this menu
a add a new partition
np print the partition table
q without saving changes
t change a partition's system id
u change display/entry units
v verify the partition table
ww write table to disk and exit
extra functionality (experts only)
```

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
p
```