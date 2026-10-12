parenthesis is the total blocks available for partitioning. If this is the first partition, choose 1 as the starting block:

`First cylinder (1-1014): 1`

To create a 512MB partition, enter the size in bytes, kilobytes, or megabytes. Because a value in megabytes is easy to deal with, this example uses `+512MB` for the last cylinder:

`Last cylinder or +size or +sizeM or +sizeK (1-1014): +512M`

To see whether the partition has been created as requested, use the `p` command to see the partition information:

```
```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes

Device Boot     Start      End Blocks Id System
/dev/sda1           1       505  524916 83 Linux native
```
```

As the last two lines show, the first partition has been created as requested, and the default partition type is Linux native; if you want to change this, use the `t` command to toggle a partition's system ID flag. For example, to toggle a partition's system ID flag to Linux swap, use the following commands:

```
```
Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux swap)

Command (m for help): p
```
```

```
```
Disk /dev/sda: 33 heads, 63 sectors, 1014 cylinders
Units = cylinders of 2079 * 512 bytes

Device Boot     Start      End Blocks Id System
/dev/sda1           1       505  524916 82 Linux swap
```
```