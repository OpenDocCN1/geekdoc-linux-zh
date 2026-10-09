You can now resize your ZFS partition to use that space. How you resize a partition varies with the partitioning scheme.

# Scheming Disks

No, not the sort of scheming where the disk deliberately lies to you. We’re talking about the disk’s partitioning scheme. Destruction is easier than creation, in both meatspace and with storage. Before you can partition a disk, you need to assign it a partitioning scheme.

# Removing the Disk Partitioning Scheme

You could go through and painstakingly delete every partition on the disk and then obliterate the partitioning scheme. That’s a bunch of work, though. It’s much simpler to just trash the entire disk partition table.

You can’t erase a disk with mounted partitions. Unmount those partitions first, and remove them from any ZFS pools. Once the disk is truly unused, erase any existing partitioning table with gpart destroy.

```
# gpart destroy da3
da3 destroyed
```

If the command returns immediately, the disk had no partitions. It might have had a partition scheme, but no partitions. If you get a “device busy” error, either the disk is still in use or the disk has partitions. You could methodically delete all existing partitions with gpart delete and then destroy the partitioning scheme, but it’s easier to burn the existing scheme to the ground by adding -f.

```
# gpart destroy -f da3
```

This forcibly erases all partitions and the partitioning scheme. Running gpart show da3 will show that there’s no partition table. You can now create new disk partitions.