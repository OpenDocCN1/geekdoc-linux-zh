a small /boot partition, if you choose to use one, and for small (sub-gigabyte) removable disks. On such small partitions, the size of the journal used by more advanced filesystems can be a real problem, so the non-journaling ext2fs is a better choice. (Journaling is described in more detail shortly.) The ext2 filesystem type code is ext2.

**Ext3fs** The Third Extended File System (ext3fs or ext3) is basically ext2fs with a journal added. The result is a file system that’s as reliable as ext2fs but that recovers from power outages and system crashes much more quickly. The ext3 filesystem type code is ext3.

**Ext4fs** The Fourth Extended File System (ext4fs or ext4) is the next-generation version of this filesystem family. It adds the ability to work with very large disks (those over 32 terabytes) or very large files (those over 2 terabytes), as well as extensions intended to improve performance. Its filesystem type code is ext4.

**ReiserFS** This filesystem was designed from scratch as a journaling filesystem for Linux and is a popular choice in its role. It’s particularly good at handling filesystems with large numbers of small files (say, smaller than about 32KB) because ReiserFS uses various tricks to squeeze the ends of files into each other’s unused spaces. This small savings can add up to a large percentage of file sizes when files are small. You can use reiserfs as the type code for this filesystem.

![](bbox=[0.11, 0.6, 0.25, 0.66])

> As of Linux kernel version 2.6.34, ReiserFS version 3.x is current. A from-scratch rewrite of ReiserFS, known as Reiser4, is being developed but has not yet been integrated into the mainstream kernel.

**JFS** IBM developed the Journaled File System (JFS) for its AIX OS and later re-implemented it on OS/2. The OS/2 version was subsequently donated to Linux. JFS is a technically sophisticated journaling filesystem that may be of particular interest if you’re familiar with AIX or OS/2 or want an advanced filesystem to use on a dual-boot system with one of these OSs. As you might expect, this filesystem’s type code is jfs.

**XFS** Silicon Graphics (SGI) created its Extents File System (XFS) for its IRIX OS and, like IBM, later donated the code to Linux. Like JFS, XFS is a very technically sophisticated filesystem. XFS has gained a reputation for robustness, speed, and flexibility on IRIX, but some of the XFS features that make it so flexible on IRIX aren’t supported well under Linux. Use xfs as the type code for this filesystem.

**Btrfs** This filesystem (pronounced “butter eff ess” or “bee tree eff ess”) is an advanced filesystem with features inspired by those of Sun’s Zettabyte File System (ZFS). Like ext4fs, JFS, and XFS, Btrfs is a fast performer and is able to handle very large disks and files. As of the 2.6.34 kernel, Btrfs is considered experimental; however, its advanced features make it a likely successor to the current popular filesystems.