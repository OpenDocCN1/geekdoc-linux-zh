Free space and inodes within each AG are managed so that multiple processes can allocate free space throughout the file system simultaneously, thus reducing the bottleneck that can occur on large, active file systems.

XFS was merged into the 2.4.25 release of the kernel.org source tree.

# ## Kernel Configuration Support for XFS

You can set XFS options through the File Systems section of the configuration menu by enabling the following option:

```
`XFS filesystem support (CONFIG_XFS_FS=y,m,n)`
```

Click y next to the xfs entry if you want to build XFS into the kernel. Click m next to the xfs entry if you want to build XFS as a module.

Other options are available in the XFS section for XFS configuration. If you need any of these options, select them there.

# ## Working with XFS File Systems

There are two ways to tune an XFS file system:

+   1. When the file system is created, which is the most efficient way
+   2. Through options that can be used when the file system is mounted

Both of these tuning options are discussed in the following sections.

# ## Creating an XFS File System

The program that creates XFS file systems is called xfs_mkfs. This program can also be invoked by using the name mkfs.xfs. For a list of all the options of the mkfs utility, see the mkfs.xfs man page.

The next example shows how to create an XFS file system using a spare partition (/dev/hda1).

To create the XFS file system with the log inside the XFS partition, issue the following command:

```
`# mkfs.xfs /dev/hda1`
```