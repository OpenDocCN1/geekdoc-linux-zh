This chapter covers the *Disk Management* test objectives. The first section of this chapter reviews basic disk management commands. The second section introduces and describes features of virtual file systems and defines some of the basic terminology.

The last two sections briefly describe the features and capabilities of two disk management software products that are available for the Solaris 8 operating system: Solstice DiskSuite and Sun StorEdge Volume Manager.

# Basic Disk Management

This section provides a brief review of the basic disk management commands provided with the Solaris 8 operating system. These commands are covered in more detail in Chapter 9, “File System Administration.”

> NOTE: Reviewing Chapter 9 should be considered part of your preparation for the Part II exam.

Before you create a file system on a disk, the disk must be formatted by using the **format** command. Next, you must define the volume table of contents (VTOC) using the **fmthard** or **format** command. The VTOC includes the partition table that determines the number and size of partitions or disk slices. The **prtvtoc** command can be used to display the VTOC. For x86 platforms, the **fdisk** command is used to create or modify the partition table.

You can use the **mkfs** or **newfs** command to create a Unix File System (UFS) on the partition. The file system must fit within a partition, and only one file system can reside within a partition.

The **fsck** command checks and repairs file systems. Typically, a file system should be checked before it is made available for use.

You can use the **mount** or **mountall** command to mount the file system and make it available for use.

# Virtual File Systems

Virtual disk management systems let you use physical disks in different ways that are not supported by the standard Solaris file systems. The following sections summarize these advantages and describe several techniques to provide virtual file systems.