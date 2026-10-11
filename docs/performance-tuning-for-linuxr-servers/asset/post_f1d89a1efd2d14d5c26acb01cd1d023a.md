
*   `jfs_fsscklog`. Extracts a JFS fsck service log into a file or format and displays the extracted file.
*   `jfs_debugfs`. A shell-type JFS file system editor.

For more information, see the man pages for the JFS utilities.

# Next-Generation File System (XFS)

SGI has released a version of its high-end XFS file system for Linux. Based on the SGI Irix XFS file system technology, XFS supports metadata journaling and extremely large disk farms. A single XFS file system is designed to be 18,000 petabytes and a single file can be 9,000 petabytes.

In addition, XFS is designed to scale and have high performance. XFS uses many of the same techniques available in JFS.

XFS is a 64-bit file system. All the file system counters in the system are 64 bits in length, as are the addresses used for each disk block and the unique number assigned to each file inode number. Currently, Linux supports only 32-bit inode numbers, so this limits XFS to a 32-bit inode number. A single file system can in theory be as large as 18 million terabytes. Currently, Linux has a 2TB limit for the 2.4.x kernel and a 16TB limit for the 2.6.x kernel.

XFS partitions the file system into regions called allocation groups (AGs). Each AG manages its own free space and inodes, as shown in Figure 11-7. In addition, AGs provide scalability and parallelism for the file system. AGs range in size from 0.5GB to 4GB. Files and directories are not limited to a single AG.

![](img/08b574e80eed8279bfda286dbd25d40d_329_0.png)

Free space and inodes within each AG are managed so that multiple processes can allocate free space throughout the file system simultaneously, thus reducing the bottleneck that can occur on large, active file systems.

XFS was merged into the 2.4.25 release of the kernel.org source tree.

## Kernel Configuration Support for XFS

You can set XFS options through the File Systems section of the configuration menu by enabling the following option:

```
XFS filesystem support (CONFIG_XFS_FS=y,m,n)
```

Click y next to the xfs entry if you want to build XFS into the kernel. Click m next to the xfs entry if you want to build XFS as a module.

Other options are available in the XFS section for XFS configuration. If you need any of these options, select them there.

## Working with XFS File Systems

There are two ways to tune an XFS file system:

1. When the file system is created, which is the most efficient way
2. Through options that can be used when the file system is mounted

Both of these tuning options are discussed in the following sections.

## Creating an XFS File System

The program that creates XFS file systems is called `xfs_mkfs`. This program can also be invoked by using the name `mkfs.xfs`. For a list of all the options of the `mkfs` utility, see the `mkfs.xfs` man page.

The next example shows how to create an XFS file system using a spare partition (`/dev/hda1`).

To create the XFS file system with the log inside the XFS partition, issue the following command:

```
# mkfs.xfs /dev/hda1
```

One option that can make a difference in the file system is the `-i size=xxx` option. The default inode size is 256 bytes. The inode size can be increased (up to 4KB). Doing so means that more directories keep their contents in the inode and need less disk I/O to read and write. However, inodes conversely need more I/O to read; because they are read and written in clusters, this is not a straightforward calculation. Because extents are also held in the inode if there is room, the number of files with out-of-inode metadata is reduced.

Another option that makes a difference in the file system's performance is the log size: `-l size=xxx`. A larger log means that when there is a large amount of metadata activity, more time elapses before modified metadata is flushed to the disk. However, a larger log also slows down recovery.

Finally, for very large file systems, keep the `agcount` as low as possible (specified with the `-d agcount=` option). An allocation group can be up to 4GB in size; more allocation groups means more of them to scan in low free-space conditions. The allocation group size also governs the maximum extent size you can have in a file.

After the file system has been created, mount it using the `mount` command. Determine a mount point and create a new empty directory, such as `/xfs`, to mount the file system:

```
# mount -t xfs /dev/hda1 /xfs
```

After the file system is mounted, you can try out XFS.

To unmount the XFS file system, use the `umount` command with the same mount point as the argument:

```
# umount /xfs
```

## Full File System

An XFS file system performs allocations more slowly when the file system is very full/nearly 99%. Basically, XFS composes the file system into allocation groups (1 to 4 GB each), and free space is managed independently in each of these. The slowdown occurs when the system has to scan through a large number of allocation groups, looking for space to extend a file. An in-memory summary structure tells you if it is worth the effort to look in an allocation group, so a major slowdown does not usually occur, unless a significant number of parallel actions occur.

## Increasing Speed with an External Log for XFS

An external log improves performance because the log updates are saved to a different partition than their corresponding file system.

To create an XFS file system with the log on an external device, your system needs to have two unused partitions. In the following example, `/dev/hda1` and `/dev/hdb1` are spare partitions. The `/dev/hda1` partition is used as the external log.

```
# mkfs.xfs -l logdev=/dev/hda1 /dev/hdb1
```

### Mounting the File System

To mount the file system, use the following mount command:

```
# mount -t xfs /dev/hdb1 /xfs
```

To avoid having to mount the file system every time the system boots, add the file system to the `/etc/fstab` file. Make a backup of `/etc/fstab` and edit it with your favorite editor to add the `/dev/hdb1` device. For example:

```
/dev/hdb1 /xfs xfs defaults 1 2
```

### Mount Options

At mount time, three XFS options are related to performance:

*   `osyncsada sync`. Indicates that `O_SYNC` is treated as `O_DSYNC`, which is the behavior Ext2 gives you by default. Without this option, `O_SYNC` file I/O syncs more metadata for the file.
*   `logbufsize=size`. Sets the number of log buffers that are held in memory. This means you can have more active transactions at once and can still perform metadata changes while the log is synced to disk. The flip side of this is that the number of metadata changes that might be lost due to a system crash is greater. Valid values are 2 through 8. The default value is eight buffers for file systems created with a 64KB block size, four buffers for file systems created with a 32KB block size, three buffers for file systems created with a 16KB block size, and two buffers for the other block sizes.
*   `logbsize=size`. Sets the size of the log buffers held in memory.

Linux records an `atime`, or access time, whenever a file is read. However, this information is not very useful and can be costly to track. To get a quick performance boost, simply disable access time updates with the mount option `noatime`.

## Tuning XFS

For a metadata-intensive workload, the default log size could be the limiting factor that reduces the file system's performance. Better results are achieved by creating file systems with a larger log size. The following `mkfs` command creates a log size of 32768b:

```
# mkfs -t xfs -l size=32768b -f /dev/hdb1
```

Currently, to resize a log, you need to remake the file system.

Also, it is a good idea to mount metadata-intensive file systems with the following:

```
# mount -t xfs -o logbufs=8,logsize=32768b /dev/device /mntpoint
```

## XFS Utilities

The XFS utilities are available in two packages: `xfsprogs` and `xfsdump`. The `xfsprogs` package contains the following utilities:

*   `xfs_growfs`. Expands an XFS file system.
*   `xfs_admin`. Changes the parameters of an XFS file system.
*   `xfs_freeze`. Suspends access to an XFS file system.
*   `xfs_mkfile`. Creates an XFS file, padded with zeroes by default.
*   `xfs_check`. Checks XFS file system consistency.
*   `xfs_bmap`. Prints block mapping for an XFS file.
*   `xfs_rtcp`. Copies a file to the real-time partition on an XFS file system.
*   `xfs_repair`. Repairs corrupt or damaged XFS file systems.
*   `xfs_db`. Used to debug an XFS file system.
