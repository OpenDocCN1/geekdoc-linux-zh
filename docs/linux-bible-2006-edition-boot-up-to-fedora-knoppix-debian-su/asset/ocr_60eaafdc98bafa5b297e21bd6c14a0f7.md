# Chapter 7 \ Installing Linux 253

Although some of these options are distribution-specific, others are simply options that can be passed to an installer environment that works from a Linux kernel. Chapter 11 includes a list of many boot options that can be used with KNOPPIX and other Linux systems.

# Partitioning Hard Drives

The hard disk (or disks) on your computer provides the permanent storage area for your data files, applications programs, and the operating system itself. Partitioning is the act of dividing a disk into logical areas that can be worked with separately. In Windows, you typically have one partition that consumes the whole hard disk. However, with Linux there are several reasons you might want to have multiple partitions:

+   Multiple operating systems If you install Linux on a PC that already has a Windows operating system, you may want to keep both operating systems on the computer. For all practical purposes, each operating system must exist on a completely separate partition. When your computer boots, you can choose to run

+   Multiple partitions within an operating system To prevent from having your entire operating system run out of disk space, people often separate partitions to areas of the Linux system. For example, if /home and /var were assigned to separate partitions, then a gluttonous user who fills up the /home partition wouldn't prevent logging daemons from continuing to write files in the /var/log directory.

Multiple partitions also make it easier to obtain certain kinds of backups (such as an image backup). For example, image backup of /home would be much faster (and probably more useful) than an image backup of the root file system (/).

+   Different file system types Kind of file systems have different structures. File systems of different types must be on their own partitions. In most Linux systems, you need at least one file system type for / (typically ext3 or reiserfs) and one for your swap area. File systems on CD-ROM using the iso9660 file system.

When you create partitions for Linux, you will usually assign the file system type as Linux native (using the ext2 or ext3 type on some Linux systems, and reiserfs on others). Reasons to use other types needing a file system that allows particularly long filenames or many inmates (each consumes an inode).

For example, if you set up a news server, it can use many inodes for news articles. Another reason for using a different file system type is to copy an image backup tape from another operating system to your local disk (such as one from OS/2 or Minix operating system).

![](bbox=[0.135, 0.717, 0.183, 0.765])