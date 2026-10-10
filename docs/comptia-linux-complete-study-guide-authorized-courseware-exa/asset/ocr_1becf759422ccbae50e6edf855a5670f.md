# 104 Devices, Linux Filesystems, Filesystem Hierarchy Standard

# 104.1 Create partitions and filesystems

+   *   Use various mkfs commands to set up partitions and create various filesystems such as:
+       *   ext2
+       *   ext3
+       *   xfs
+       *   reiserfs v3
+       *   vfat
+   *   The following is a partial list of the used files, terms and utilities:
+       *   fdisk
+       *   mkfs
+       *   mkswap

# 104.2 Maintain the integrity of filesystems

+   *   Verify the integrity of filesystems
+   *   Monitor free space and inodes
+   *   Repair simple filesystem problems
+   *   The following is a partial list of the used files, terms and utilities:
+       *   du
+       *   df
+       *   fsck
+       *   e2fsck
+       *   mke2fs
+       *   debugfs
+       *   dumpe2fs
+       *   tune2fs
+       *   xfs tools (such as xfs_metadump and xfs_info)

# 104.3 Control mounting and unmounting of filesystems

+   *   Manually mount and unmount filesystems
+   *   Configure filesystem mounting on bootup
+   *   Configure user mountable removableable filesystems