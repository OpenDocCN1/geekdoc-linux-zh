
The UNIX GNU/Linux systems have pipes for many generations. Without named pipes, only processes that were children of the same ancestor could use pipes to exchange information. Using named pipes, any processes on a single machine can exchange information. One program writes to a FIFO special file. Another program reads from the same file. The programs do not have to run at the same time or be aware of each other's activity. The operating system handles all buffering and information storage. The term asynchronous (async) applies to this type of communication because the programs on the ends of the pipe do not have to be synchronized.

# Sockets

Like a FIFO special file, a socket allows asynchronous processes that are not children of the same ancestor to exchange information. Sockets are the central mechanism of the interprocess communication that is the basis of the networking facility. When you use networking utilities, pairs of cooperating sockets manage the communication between the processes on your computer and the remote computer. Sockets form the basis of such utilities as ssh and sock.

# Major and Minor Device Numbers

A major device number represents a class of hardware devices: a terminal, printer, tape drive, hard disk, and so on. In the preceding listing of the /dev directory, all the hard disk partitions have a major device number of 3.

A minor device number represents a particular piece of hardware within a class. Although all the hard disk partitions are grouped together by their major device number, each has a different minor device number (hda1 is 1, hda2 is 2, and so on). This setup allows one piece of software (the device driver) to service all similar hardware and to be able to distinguish among different physical units.

# Block and Character Devices

This section describes typical device drivers. Because device drivers can be changed to suit a particular purpose, the descriptions in this section may not pertain to every system.

A device is an I/O (input/output) device that is characterized by

- Being able to perform random access reads.
- Having a specific block size.
- Handling only single blocks of data at a time.
- Accepting only transactions that involve whole blocks of data.
- Being able to have a filesystem mounted on it.
- Having the Linux kernel buffers its input and output.
- Appearing to the operating system as a series of blocks numbered from 0 through n - 1, where n is the number of blocks on the device.

The common block devices on a Linux system are hard and floppy disks and CD-ROMs.

A character device is any device that is not a block device. Some examples of character devices are printers, terminals, tape drives, and modems.

The device driver for a character device determines how a program reads from and writes to the device. For example, the device driver for a terminal allows a program to read the information you type in the terminal in two ways. A program can read single characters from a terminal in raw mode (that is, without doing any interpretation of the characters). This mode has nothing to do with the raw device described in the following section. Alternatively, a program can read a line at a time. When a program reads a line at a, the driver handles the erase and kill characters so that the program never sees typing mistakes. In this case the program reads everything from the beginning of a line to the RETURN that ends a line; the number of characters in a line can vary.

# Raw Devices

Device driver programs for block devices usually have two entry points so they can be used in two ways: as block devices or character devices. The character device form of a block device is called a raw device. A raw device is characterized by

- Direct I/O (no buffering through the Linux kernel).
- A one-to-one correspondence between system calls and hardware requests.
- Device-dependent restrictions on I/O.

An example of a utility that uses a raw device is fck. It is more efficient for fck to operate on the disk as a raw device, not restricted by the fixed size of blocks in the block device interface. Because it has full knowledge of the underlying filesystem structure, fck can operate on the raw device by using the largest possible units. When a filesystem is mounted, processes normally access the disk through the block device interface. This explains why it is important to allow fck to modify only an unmounted filesystem. On a mounted filesystem there is the danger that, while fck is rearranging the underlying structure through the raw device, another process would change a disk block using the block device, resulting in a corrupted filesystem.

# Filesystems

Table 17-8 lists some of the types of filesystems available under GNU/Linux.

# Filesystem

| | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| adfs | The Acorn Disc Filing System. | affs | The Amiga FFS filesystem. | autofs | Automounting filesystem. | coda | The CODA distributed filesystem (being developed at Carnegie-Mellon). | devpts | A pseudofystem for pseudoterminals (page 958). | ext2 | A standard filesystem for Red Hat systems, usually with the ext3 extension. | ext3 | A journaling (page 1475) extension to the ext2 filesystem; greatly improves recovery time from crashes (it takes a lot time to run fsck), promoting increased availability. As with any filesystem, a journaling filesystem can lose data during a system crash or hardware-failure. | hfs | Hierarchical Filesystem: used by all Macintoshes from the Mac Plus on. | hpfs | High Performance Filesystem: the native filesystem for IBM's OS/2. | iso9660 | The standard filesystem for CD-ROMs. | minix | Very similar to Linux, the filesystem of a small operating system that was written for educational purposes by Prof. Andrew S. Tanenberg (cs.cw.vu.nl/~/minix.html). | msdos | The filesystem used by DOS and subsequent Microsoft operating systems. | ncpfs | Novell NetWare NCP Protocol Filesystem: used to mount remote filesystems under NetWare. | nfs | Network Filesystem: Developed by Sun Microsystems, a protocol that allows a computer to access remote files over a network as they were local. | ntfs | NT Filesystem: the native filesystem of Windows NT. |

# Filesystem (Continued)

| | | |
| :--- | :--- |
| proc | An interface to several Linux kernel data structures (page 1463) that behaves like a filesystem (page 966). |
| qnx4 | The QNX 4 Operating System filesystem. |
| reiserfs | A journaling (page 1475) filesystem, based on balanced-tree-algorithms. See ext3 for more on journaling filesystems. |
| romfs | A dumb, readily filesystem used mainly for RAM disks (page 1488) during installation. |
| software RAID | RAID implemented in software (not hardware). Refer to "RAID File-system" on page 984. |
| smbfs | Samba Filesystem. Refer to "Samba/swat" on page 1025. |
| sysv | System V UNIX filesystem. |
| ufs | Default filesystem under Sun Solaris Operating System and other UNIXs. |
| umsdsf | A full-feature UNIX-like filesystem that runs on top of a DOS filesystem. |
| vfat | Developed by Microsoft, a standard that allows long file names on FAT partitions. |

mount: Mounts a Filesystem
The mount utility allows you to connect filesystems to your Linux file hierarchy. These filesystems can be on remote and local disk partitions, CD-ROMs, and floppy disks. Linux also allows you to mount virtual filesystem that have been built inside regular files, files built for other operating systems, and the special/proc filesystem (page 966), which maps useful kernel information into a directory-like structure.

The mount point for the filesystem that you are mounting is a directory in your local filesystem. The directory must exist before mounting; its contents disappear as long as a filesystem is mounted on it and reappear when you mount the file-system.

Without any arguments, mount lists all the currently mounted filesystems, showing the physical device holding the filesystem, the mount point, the type of filesystem, and any options set when each filesystem was mounted:
