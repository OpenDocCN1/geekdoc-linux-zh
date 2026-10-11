Linux 2.4 includes all of the file systems present in Linux 2.2, including FAT12 and FAT16 (for floppy drives and hard disks for the assorted DOS versions), NTFS (for Windows NT), VFAT and FAT32 (for Windows 9x), HFS (for MacOS), HPFS (for OS/2), UFS, and many more. However, in this chapter we have only treated the ever-present ext2 file system, as well as the new IBM journaling file system, JFS. It is clearly impossible to cover in a single chapter all, or even a significant part of, file systems available for Linux. For a detailed study on Linux 2.4 file systems, see my upcoming book *Linux File Systems*, to be published by McGraw-Hill.3

# IBM's JFS

JFS provides the superblock- and file-operation system calls required by the Linux Virtual File system layer. JFS, a log-based, byte-level file system, is both robust and scalable; although tailored primarily for the high throughput and reliability requirements of transaction-oriented, high-performance servers (from single processor systems to advanced multi-processor and clustered systems), JFS is also applicable to client configurations where performance and reliability are desired. In February 2000 IBM announced that JFS will be made available to the public. See **http://www-4.ibm.com/softwre/developer/library/jfs.html**.

# Main JFS Data Structures and Algorithms

# Superblocks: Primary Aggregate Superblock and Secondary Aggregate Superblock

The superblocks contain aggregate-wide information such as the size of the aggregate, size of allocation groups, aggregate block size, etc. The secondary aggregate superblock is a direct copy of the primary aggre-

3 In December 1999, I first proposed to IBM the idea of releasing the excellent JFS (Journaled File System) under the GPL license. In February 2000 IBM announced that JFS will be made available to the public. Other logging file systems have been announced, such as ext3fs, Veritas VxFS (port announced January 19, 2000, no availability date specified), and SGI's xfs. Very talented and bright Linux hacker Hans Reiser has also written his own journaling file system, reiserfs. As of this writing, the only readily available options are reiserfs and IBM's JFS; reiserfs is not yet available for the 2.4 kernel.

Although JFS is only in its 0.4 version, it is already quite a capable competitor to ext3fs and reiserfs, against which it shows improved reliability.