```
File system type? [ext2]?
Start? 1000MB
End? 2038MB
(parted)
```

In this example, the print command displayed the current partition table to verify that the correct disk was being used. Upon issuing the mkpartfs command without extra options, GNU Parted prompted for values: the partition type, the file system type (giving no response caused the default value of ext2 to be used), and the start and end points. Unlike fdisk, which deals in cylinders by default, GNU Parted expects values in other units—megabytes in this example, although kilobytes or gigabytes could have been used. Although the display was eventually replaced by the final (parted) prompt, the program briefly displayed a summary of what it did as it created the partition and then the filesystem within it.

# ## Creating New Filesystems

Just creating partitions isn’t enough to make them useful in Linux. To make them useful, you must create a filesystem on the partition (a task that’s also sometimes called “formatting” a partition). If you use GNU Parted, you may be able to create a filesystem when you create a partition. If GNU Parted doesn’t support your filesystem type, if you prefer to do it manually, or if you use fdisk to create partitions, you can use the mkfs program to do the job. This tool has the following syntax:

```
mkfs [-V] [-t fstype] [options] device [blocks]
```

![](bbox=[0.15, 0.56, 0.25, 0.61])

mkfs is actually just a front-end to tools that do the real work for specific filesystems, such as mke2fs (also known as mkfs.ext2). You can call these tools directly if you prefer, although their syntax may vary from that of mkfs.

The mkfs parameters can be used to perform several tasks, as summarized in Table 6.4.

Table 6.4 mkfs Options

| Option | Description |
| --- | --- |
| -V | This option causes mkfs to generate verbose output, displaying additional information on the filesystem-creation process. |
| -t fstype | You specify the filesystem type with the -t fstype option. Common values for fstype include ext2 (for ext2fs), ext3 (for ext3fs), ext4 (for ext4fs), reiserfs (for ReiserFS), xfs (for XFS), jfs (for JFS), and msdos (for FAT). Some other options are available as well. |