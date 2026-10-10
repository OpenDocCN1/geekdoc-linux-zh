+   c toggle the dos compatibility flag
+   d delete a partition
+   l list known partition types
+   m print this menu
+   n add a new partition
+   o create a new empty DOS partition table
+   p print the partition table
+   q quit without saving changes
+   s create a new empty Sun disklabel
+   t change a partition's system id
+   u change display/entry units
+   v verify the partition table
+   w write table to disk and exit
+   x extra functionality (experts only)

Command (m for help):

We begin by looking at the existing partition, using the p command (print the partition table):

```
```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

Device Boot Start End Blocks Id System
/dev/hdb1 * 1 664 334624+ 6 FAT16
Command (m for help): ```
```

We have a little legacy system here, don't you think? Time to upgrade this disk—we start by removing the existing partition using the d command (delete a partition):

```
```
Command (m for help): d
Partition number (1-4): 1
Command (m for help): ```
```

And we use the p (print the partition table) command to verify the results:

```
```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

Device Boot Start End Blocks Id System
Command (m for help): ```
```

No partition there. Time to start creating partitions. For the sake of discussion, we'll pretend this disk is large enough to accommodate a full workstation configuration. To set this up, we need to create the partitions shown in Table 9-5.