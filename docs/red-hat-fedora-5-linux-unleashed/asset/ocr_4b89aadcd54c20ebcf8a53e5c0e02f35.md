size=journal_size—This option creates a journal of journal_size megabytes. With a minimum size of 1,024 blocks, it cannot be more than 102,400 blocks. There must be enough free space in the file system to create a journal of that size.

dev=ext4journal_device—This option associates the file system with a journal not contained within the file system (one that must have already been created with the command mke2fs -O journal_device journal_name). In other words, the journal and the data files do not have to be on the same device.

> **NOTE**
> The latter two options in the arguments list are mutually exclusive.

To select the ext3 journaling mode, you must add the appropriate entry in /etc/fstab. Because the ext3 file system is a new version of the ext2 file system with journaling added, it supports the same options as ext2, as well as the following additions:

+   *   ro=1—This option disables the ext3 file system's journal when mounting; it becomes an ext2 file system.
+   *   data=journal | data=ordered | data=writeback—This option specifies the journaling mode; ordered is the default. Metadata is always journaled.
+   *   journal—The slowest, but most secure mode because all the data is written to the journal before it is written to the regular file system.
+   *   ordered—This is the default mode in which all data is written to the main file system prior to its metadata being committed to the journal.
+   *   writeback—With this option, data can be written into the main file system after its metadata has been committed to the journal. This option enables old data to appear in files after a crash and journal recovery, but it is the fastest option.

# ## Using mkreiserfs

The Reiser file system journals file data and handles smaller files more efficiently than the ext3 file system. Although it is suitable for use as the root file system, Fedora Core does not officially support its use in that way. You use the mkreiserfs command to create a Reiser file system. The default values for mkreiserfs work well. To create a Reiser file system, use

```
# mkreiserfs device
```

# ## Creating a DOS File System with mkdosfs

It is possible to create DOS file systems without owning any Microsoft software using the mkdosfs command. To create a DOS file system in an image file, use the -C option. The -n option allows you to specify a volume label. To create a 1.4MB DOS file system as an