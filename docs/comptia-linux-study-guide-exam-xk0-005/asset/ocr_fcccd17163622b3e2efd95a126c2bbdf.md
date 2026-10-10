+   *   *device* provides device management for btrfs filesystems by adding or deleting a physical device.
+   *   *filesystem* provides filesystem management utilities for an existing btrfs filesystem, such as displaying information and resizing filesystems.
+   *   *quota* allows you to set quotas on btrfs filesystems.
+   *   *restore* allows you to restore files from a damaged btrfs filesystem.

While these ext, XFS, and btrfs tools are useful, they can't help fix things if the filesystem itself has errors. For that, the *fsck* program is the tool to use:

```
$ sudo fsck -f /dev/sdb1
fsck from util-linux 2.31.1
e2fsck 1.44.1 (24-Mar-2018)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/sdb1: 11/655360 files (0.0% non-contiguous), 66753/2621440 blocks
$
```

> **NOTE**
> 
> As of this writing the XFS module for *fsck* does not repair XFS filesystems. For now you’ll need to use the *xfs_repair* tool.

The *fsck* program is a front end to several different programs that check the various filesystems to match the index against the actual files stored in the filesystem. If any discrepancies occur, run the *fsck* program in repair mode, and it will attempt to reconcile the discrepancies and fix the filesystem.

# ## Storage Alternatives

Standard partition layouts on storage devices do have their limitations. Once you create and format a partition, it’s not easy making it larger or smaller. Individual partitions are also susceptible to disk failures, in which case all of the data stored in the partition will be lost.

To accommodate more dynamic storage options, as well as fault-tolerance features, Linux has incorporated a few advanced storage management techniques. The following sections cover three popular techniques.