![](bbox=[0.14, 0.105, 0.24, 0.16])

If your Linux system uses specialized storage devices, there are often additional command tools available other than the standard Linux tools. For example, if your Linux system uses SCSI controllers you can use the `lsscsi` command to display information about the hard drives connected to the SCSI controllers, or for systems that use fiber-channel networks to connect a storage area network (SAN) to your Linux system, the `fcstat` command is very useful.

![](bbox=[0.14, 0.26, 0.24, 0.315])

Some filesystems, such as ext3 and ext4, allocate a specific number of inodes when created. An *inode* is an entry in the index table that tracks files stored on the filesystem. If the filesystem runs out of inode entries in the table, you can’t create any more files, even if there’s available space on the drive. Using the `-i` option with the `df` command will show you the percentage of inodes used on a filesystem and can be a lifesaver.

# Filesystem Tools

Linux uses the `e2fsprogs` package of tools to provide utilities for working with ext filesystems (such as ext3 and ext4). The most popular tools in the `e2fsprogs` package are as follows:

+   - `blkid` displays information about block devices, such as storage drives.
+   - `chattr` changes file attributes on the filesystem.
+   - `debugfs` manually views and modifies the filesystem structure, such as undeleting a file or extracting a corrupted file.
+   - `dumpe2fs` displays block and superblock group information.
+   - `e2label` changes the label on the filesystem.
+   - `resize2fs` expands or shrinks a filesystem.
+   - `tune2fs` modifies filesystem parameters.

These tools help you fine-tune parameters on an ext filesystem, but if corruption occurs on the filesystem, you’ll need the `fsck` program.

The XFS filesystem also has a set of tools available for tuning the filesystem. Here are the two that you’ll most likely run across:

+   - `xfs_admin` displays or changes filesystem parameters such as the label or UUID assigned.
+   - `xfs_info` displays information about a mounted filesystem, including the block sizes and sector sizes as well as label and UUID information.

If you’re using a btrfs filesystem, the `btrfs` command provides access to several utilities for managing the filesystem:

+   - `balance` balances filesystem chunks across multiple devices
+   - `check` performs an offline check of a btrfs filesystem