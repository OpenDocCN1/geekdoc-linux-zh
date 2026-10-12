| Device Boot | Start | End | Blocks | Id |
|---|---|---|---|---|
| System | | | | |
| /dev/sda1 | | 1 | 505 | 524916 | 83 |
| Linux native | | | | |

The last two lines show that the first partition has been created as requested, and that the default partition type is Linux native; if you want to change this, use the t command to toggle a partition's system ID flag. For example, to toggle a partition's system ID flag to Linux swap, use the following commands:

```
Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux swap)

Command (m for help): p
```

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes
```

| Device Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|
| /dev/sda1 | * | 1 | 505 | 524916 | 82 | Linux |
| swap | | | | | |

First, the t command is entered to toggle the system ID of a partition. Then, the partition is selected and 82 is entered as the swap partition type. The L command can be used to list all the available partition types.

Note that if you use fdisk to create partitions, you must make a Linux native partition bootable. For example, to turn on /dev/sda1 as a bootable partition, you need to toggle the boot flag by entering the following:

```
Command (m for help): a
Partition number (1-6): 1
```

Using the p command displays the existing partition table:

```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
```