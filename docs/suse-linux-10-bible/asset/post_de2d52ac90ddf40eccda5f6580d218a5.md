
## Chapter 3 ✦ Partitions, Filesystems, and Files 87

To provide access to a wide range of different types of filesystems, Linux provides a general method that is easily extended. Linux provides a virtual filesystem (VFS) layer that a filesystem driver hooks into to provide file-based access to information. Whether it is listing the files in a directory, the data from a file, or providing other functionality as direct file access (not using the filesystem buffers), VFS and the filesystem driver provide a uniform application interface (API) to deal with different types of filesystems. This is nothing new, and Unix and all operating systems that support multiple filesystems provide this virtual interface in one way or another.

When you have created partitions, you must usually create a filesystem in partition to make use of the newly allocated space. Many different types of filesystems are available for this purpose, but this section focuses on types of filesystems that are available out of the box with SUSE Linux.

The most common and preferred filesystem used by SUSE is the Reiser filesystem (ReiserFS). ReiserFS was the first incarnation of a journaling filesystem on Linux. The development of ReiserFS was partly fueled by SUSE as they realized enterprise class storage (at least large storage pools) needed a journaling filesystem.

## What Is a Journaling Filesystem?

A journal, with respect to filesystems, is an area of the disk that is used to store information about changes to that filesystem. Filesystems contain two types of information: the actual files and directories where your data is stored, and filesystem metadata, which is information about the filesystem itself (where the data for each file is physically stored, directories which contain files, and so on). When you write to a journaling filesystem, the changes that you want to make are written directly to the journal. The filesystem then asynchronously applies those changes to the specified files and updates the metadata only when the modified file has been successfully written to the file. Journal helps guarantee that a filesystem is always in a consistent state. When you reboot a system, Linux checks the consistency of each filesystem (using a program called fsck, for system consistency check) before it. If a filesystem requires repair because its consistency cannot be verified, the fsck process can take a long time, especially on large disks. Enterprise systems need to require journaling filesystems to minimize the time it takes to restart the system because downtime is generally frowned upon.

Historically, the most popular Linux filesystem is EXT2, which is a fast, simple filesystem that does not have a journaling feature. When a system uses EXT2 filesystems crashes, the EXT2 metadata must be scanned thoroughly and compared to the data that is actually on the disk to correct any of data corruption. On a large system, this consistency check can take at best minutes and at worst an hour or two. Journaling filesystems introduce a small overhead for all write operations, but the greater assurances of data consistency and the fact that modern drives are very fast make them an attractive choice for use on most modern Linux systems.

There are certain situations where the use of a journaling filesystem can be a bad idea — notably with databases that store their data in a standard Linux filesystem but keep their log of changes to those files and are able to recover data using their internal methods. Oracle is a good example of a database that provides its own methods to guarantee the consistency of its data files.

## EXT2

EXT2 has been the facto Linux filesystem for many years and is still used for initial randoms and most non-journaling filesystems. Because of its age, EXT2 is considered extremely stable and quite lightweight in terms of overhead. The downside is that it does not use any journaling to maintain integrity of data and metadata.

## EXT3

EXT3 is a journaling version of the EXT2 filesystem discussed in the previous section. It adds a journal to the EXT2 filesystem, which can be done to an existing EXT2 filesystem, enabling easy upgrades. This is not possible with other journaling filesystems because they are internally very different from other filesystems.

EXT3 provides three journaling modes, each of which has different advantages and disadvantages:

- **journal**: Logs all filesystem data and metadata changes. The slowest of the three EXT3 journaling modes, this journaling mode minimizes the chance of losing the changes you have made to any file in an EXT3 filesystem.
- **ordered**: Logs only changes to filesystem metadata, but relates file data updates before making changes to associated filesystem metadata. This is the default EXT3 journaling mode.
- **writeback**: Logs only changes to filesystem metadata but relies on the filesystem write process to write file data to disk. This is the fastest EXT3 journaling mode.

Beyond its flexibility and the ease with which EXT2 filesystems can be converted to EXT3 filesystems, another advantage of the EXT3 filesystem is that it is also backward compatible, meaning you can mount an EXT3 filesystem as an EXT2 system because the layout on the disk is exactly the same. This enables you to take advantage of all the existing filesystem repair, tuning, and optimization software that you have always used with EXT2 filesystems should you ever need to repair an EXT3 filesystem.

JFS is similar to ReiserFS in that it uses binary trees to store information about files. JFS is heavily based on transactions, in much the same way that databases are, using these as the basis for the records that it maintains in its journal. An extent is a contiguous series of data blocks that can be allocated, read, written and managed at one time.

JFS also makes clear that XFS is associated with each single file or directory in the filesystem (information node) data structure that at least one inode exists for every file in the filesystem, JFS creates them only when files and directories are created. In traditional filesystems, the number of inodes (and the number of files) on a filesystem was dictated by filesystem creation time. This could lead to a situation in which no more files could be created because there was nowhere to store information. JFS can create virtually unlimited number of files and XFS is scalable. As JFS is a 64-bit filesystem, it is also able to allocate space for extremely large files, unlike 32-bit filesystems that can create files only up to 4GB in size.

## XFS

XFS is SGI's high-performance 64-bit filesystem, originally developed for use with its IRIX operating system. SGI machines have traditionally had to work with large sets on machines with many processors, which is reflected in the way XFS works. One of the best features of XFS is that independent domains of data across the filesystem allows a multiprocessor system to access data independently of each other. This means that instead of a single write happening at one time, multiple reads and writes can take place at the same time. This provides a significant performance boost for enterprise level data storage. This might not sound like something that would work in the traditional sense of a single disk on a home PC, but if you have a storage area network in which multiple data are processed by many disks, the data works very well.

Like ReFS, XFS uses its journal to store information about metadata and employs binary trees to handle allocation of data. An added feature of XFS is that it also uses a binary tree to store information about free space. This helps up block allocation for new information. As you would expect from a filesystem originally developed for processes that handle amounts of metadata data, XFS is especially good at allocating and managing files.

XFS is truly an enterprise filesystem and may not prove overwhelmingly attractive for a home user, but for large amounts of data and high-end machines, it is really an excellent choice.

## VFAT/NTFS

Virtual File Allocation Table (VFAT) and New Technology File System (NTFS) are the Microsoft filesystems that are found in Windows 98/95, NT, and 200x operating systems. NTFS filesystems are readable by Linux systems, although writing NTFS filesystems is a recent addition to the Linux kernel that is being developed and debugged. Support for the VFAT filesystem is quite stable in Linux and enables a
