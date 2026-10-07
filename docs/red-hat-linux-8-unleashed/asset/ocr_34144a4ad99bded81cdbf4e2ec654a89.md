# CHAPTER 10 Managing the Filesystem

The default setting provided by Red Hat is adequate for most needs. The optimal choice depends on many factors (computer usage, hardware used, and testing and evaluation methods) that a meaningful discussion is beyond the scope of this chapter. You learn in this chapter what the choices are and how they differ, but whether a choice is right for you can only be determined on an individual basis.

Like journaling filesystems, the traditional filesystem check (fsck) is not necessary on an ext3 filesystem. Although only mildly annoying on a 20GB drive on your machine at home, imagining the seemingly endless hours that a fsck would take to run on a terabyte of data. This feature is shared in common with the other journaling filesystems

When choosing journaling options, you can trade off data integrity (keeping your data current and valid) for data transfer speed in your filesystem's operation; you can't have both because of the nature of the filesystem design. You can choose to expose some of your data to potential damage in the case of an improper shutdown in exchange for faster data handling; or, you can sacrifice speed to keep the state of the filesystem consistent with the state of the operating system.

Three modes available as ext3 are as follows:

+   - Writeback—Allow data to stay in the filesystem, attaining the fastest speed possible. It doesn't schedule any data writes; it just allows the kernel's 30-second writeback code to flush the buffer.
- Ordered—keeps the data consistent, but with some sacrifice in speed (the default mode for Red Hat).
- Journal—Requires more disk space to journal more data. You might see slower performance because data is written twice, but there are some speed benefits if you are doing synchronous data writes in database operations.

For most of us, the default selection represents a good trade-off. Red Hat supports booting from an ext3 formatted root filesystem with the proper drivers loaded in the initrd image.
The mode is selected by using the appropriate mount point in /etc/fstab.

# Verifying File Integrity in ext3 with the fsck Utility

The filesystem integrity is assured through the use of the fsck, or filesystem check, program—one of five commands in the library that are used to maintain and modify the ext3 filesystem.

When fsck is run, it performs a sequential analysis of the filesystem information available in the filesystem if it detects a directory that cannot be traced back to the root or an undeleted file with a zero link count. It places these directories and files in the /lost+found directory that is created on each physical partition by the filesystem formatting process. Some blocks are reserved for this and other uses of the superuser. It is possible to reduce this allocation to free regular users by special arguments to the formatting program mke2fs.