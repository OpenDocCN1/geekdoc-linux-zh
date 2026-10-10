| Device | Boot | Start | End | Sectors | Size Id Type |

Then you delete partition 2 and check for free space:

```
Command (m for help): F
Unpartitioned space /dev/sdd: 881 MiB, 923841536 bytes, 1804378 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes

 Start End Sectors Size
1050624 2099199 1048576 512M
3147776 3903577 755802 369M
```

Adding up the size of the unallocated space, in theory we have 881 MB available. But see what happens when we try to create a 700 MB partition:

```
Command (m for help): n
Partition type
 p primary (2 primary, 0 extended, 2 free)
 e extended (container for logical partitions)
Select (default p): p
Partition number {2,4, default 2}: 2
First sector (1050624-3903577, default 2): 1050624)
Last sector, +/-sectors or +/-size{K,M,G,T,P} (1050624-2099199, default 2099199): +700M
Value out of range.
```

That happens because the largest contiguous unallocated space on the disk is the 512 MB block that belonged to partition 2. Your new partition cannot “reach over” partition 3 to use some of the unallocated space after it.

# Changing the Partition Type

Occasionally, you may need to change the partition type, especially when dealing with disks that will be used on other operating systems and platforms. This is done with the command t, followed by the number of the partition you wish to change.

The partition type must be specified by its corresponding hexadecimal code, and you can see a list