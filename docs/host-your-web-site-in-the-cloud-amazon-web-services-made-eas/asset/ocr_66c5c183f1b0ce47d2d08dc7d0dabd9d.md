```
Block size=4096 (log=2)
:
5242880 inodes, 10485696 blocks
```

Multiplying the block size (4096) by the block count (10,485,696) results in the value 42,949,410,816. We've created a 40 gigabyte RAID volume. As is the case with any file system, we wrap up by creating a mount point and mounting the volume on it:

```
<dev>: mkdir /data
<dev>: mount /dev/md0 /data
```

When using RAID volumes in production-level systems, you should keep a few things in mind:

+   1. An ext3 file system on a 32-bit Linux system is limited to a maximum size of eight terabytes (if the default 4K block size is used). You can use the xfs file system if you need to create larger file systems.
+   2. The larger the file system, the more time the `fsck` command will need to check and repair the disk after a crash or an unclean reboot.
+   3. Take extreme care when creating snapshots of the volumes used to create a RAID array. Be sure to defer all write activity, run the `sync` command, and initiate all the snapshots in succession. Track the snapshot IDs with care in case you need to put the volume back together later. If you do find that you have to put the volume back together, be sure that the ordering of the volumes within the RAID is preserved across the entire operation.
+   4. The `mdadm` command has many options. Spend some time studying it to learn even more about what you can do with RAID volumes. For example, you can add additional devices to a RAID 0 volume in order to increase its capacity. If you do this, you also need to do a logical resize on the file system.