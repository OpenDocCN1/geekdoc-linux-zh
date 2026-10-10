It includes additional advanced features such as built-in snapshots for backup, improved fault tolerance, and data compression on the fly.

+   - *eCryptfs:* The Enterprise Cryptographic File System (eCryptfs) applies a POSIX-compliant encryption protocol to data before storing it on the device. This provides a layer of protection for data stored on the device. Only the operating system that created the filesystem can read data from it.

+   - *ext3:* Also called ext3fs, this is a descendant of the original Linux ext filesystem. It supports files up to 2 tebibytes (TiB), with a total filesystem size of 16 TiB. It supports journaling as well as faster startup and recovery.

+   - *ext4:* Also called ext4fs, it’s the current version of the original Linux filesystem. It supports files up to 16 TiB, with a total filesystem size of 1 EiB. It also supports journaling and utilizes improved performance features.

+   - XFS: A 64-bit high-performance journaling filesystem created by SIlicon Graphics in 1993 and ported to Linux in 2001. It supports filesystems up to 8 exabytes.

+   - *swap:* The swap filesystem allows you to create virtual memory for your system using space on a physical drive. The system can then swap data out of normal memory into the swap space, providing a method of adding additional memory to your system. This is not intended for storing persistent data.

Most Linux distributions these days use the ext4fs filesystem as the default, although Red Hat has recently chosen the XFS filesystem as the default. Both filesystems provide *journaling*, which is a method of tracking data not yet written to the drive in a log file, called the journal. If the system fails before the data can be written to the drive, the journal data can be recovered and stored upon the next system boot.

# Non-Linux Filesystems

One of the great features of Linux that makes it so versatile is its ability to read data stored on devices formatted for other operating systems, such as Apple and Microsoft. This feature makes it a breeze to share data between different systems running different operating systems.

Here’s a list of common non-Linux filesystems that Linux can handle:

+   - *CIFS:* The Common Internet File System (CIFS) is a filesystem protocol created by Microsoft for reading and writing data across a network using a network storage device. It was released to the public for use on all operating systems.

+   - *HFS:* The Hierarchical File System (HFS) was developed by Apple for its macOS systems. Linux can also interact with the more advanced HFS+ filesystem.

+   - *ISO-9660:* The *ISO-9660* standard is used for creating filesystems on CD-ROM devices.

+   - NFS: The Network File System (NFS) is an open source standard for reading and writing data across a network using a network storage device.

+   - NTFS: The New Technology File System (NTFS) is the filesystem used by the Microsoft NT operating system and subsequent versions of Windows. Linux can read and write data on an NTFS partition as of kernel *2,6,x*.