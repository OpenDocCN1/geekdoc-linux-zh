HFS+ The follow-on to HFS borrows many features from Unix-style file systems, but it stops short of adding a journal. New Macintoshes invariably ship with their disks formatted for HFS+, but this file system is not used much on removable media. (The MacOS X installation CD-ROM is an exception; it uses HFS+.) Linux support for HFS+ is in the alpha stage and is not yet integrated into the kernel. The Linux HFS+ Web page is http://sourceforge.net/projects/linux-hfsplus/.

FFS MacOS X provides the option to use the Unix Fast Filesystem (FFS), which is described in the next section. Many MacOS X systems continue to use HFS+, though.

If you need to exchange removable media between Macintosh and Linux systems, you can do so. HFS is the best choice for a file system; and if you use a floppy disk, it has to be a 1.44MB floppy or a rare 720KB HFS floppy. Alternatively, you can use FAT, because modern Macintoshes support FAT. In theory, you can use FFS for exchanges with a Macintosh running MacOS X, but this option is tedious to implement.

If you run Linux on a Macintosh, you may want to create an HFS partition to be used for data exchange between Linux and MacOS. Because Linux can’t read HFS+ partitions, this data-exchange partition is a practical necessity when you want to share files across OSs.

# Miscellaneous Filesystems

In addition to Microsoft and Apple file systems, Linux supports a wide variety of other foreign file systems. Most are of extremely limited utility and interest. Here are some highlights:

BeFS BeOS uses its own journaling file system, known as BeFS. A read-only Linux driver for this file system is available from http://hp.vector.co.jp/authors/VA008030/bsf/. The author claims to be working on read/write support, but it does not yet exist. The driver also does not yet work with 2.4.x kernels, as of mid-2002. Although BeOS is a single-user OS, BeFS supports file ownership and permissions similar to those used in Linux. In theory, BeFS could become a contender for a native journaling file system, but the others have a commanding lead in 2002. BeFS also lacks support for file access time-stamps, which may hinder its abilities as a native Linux file system. BeFS’s file system type code is befs.

Note The 2.4.x kernels include support for another file system, known as BFS, that is completely unrelated to BeFS. BFS is used for storing critical system startup files on SCO’s UnixWare OS.

FFS/UFS The Fast Filesystem (FFS; aka Unix Filesystem or UFS) was developed early in the history of Unix. It’s still used by many Unix and derivative systems, including FreeBSD and Solaris. In principle, FFS/UFS could have been adopted as a native Linux file system, but Linux’s write support for this file system is still considered dangerous, much as is Linux’s support for writing to NTFS. FFS has been around long enough to spawn several minor variants, but one Linux driver handles them all. FFS’s file system type code is ufs.

UDF The Universal Disk Format (UDF) is a file system designed for recordable CD, DVD, and recordable DVD media. Linux includes UDF support in the 2.4.x kernel series, but the write support is marked "dangerous" and is very limited in terms of

![](bbox=[0.49, 0.94, 0.52, 0.96])