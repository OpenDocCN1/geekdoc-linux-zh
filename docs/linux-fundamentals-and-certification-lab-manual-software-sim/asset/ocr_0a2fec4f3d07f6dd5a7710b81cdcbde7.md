# CHAPTER 1

12

![](bbox=[0.25, 0.08, 0.8, 0.34])

PKG packages do not provide for signing, but do provide for checksums and dependency checking. PKG files cannot be viewed or manipulated by standard Linux tools.

Some Linux distributions provide for automatic updates to packages. For example, Red Hat Linux offers the Red Hat Network. The Red Hat Network is a complete systems management platform for Unix. It provides updates to software, increased management capabilities, and monitoring of the entire infrastructure. Automatic updating of RPM packages on Red Hat Linux is done with the up2date program.

# SYSTEM FEATURES

Linux supports most of the features found in Unix installations. It's a multitasking, multi-user operating system, meaning that it can run more than one program at a time and supports multiple users connected at the same time.

Linux is mostly compatible with Unix. Linux was developed with portability in mind. Most of the free software available online can be compiled under Linux and runs easily.

Linux supports multiprocessors on Intel, AMD, IBM, Sun, and other platforms (depending on the distribution). Symmetric Multi-Processor (SMP) support was introduced with kernel version 2.0. With SMP, processes and kernel-threads are distributed among processors. This means that while you are multitasking, each program can be controlled by its own processor. Using more than one processor is almost like having more than one computer to do the jobs you are running.

Linux supports multiple virtual consoles. A console is used by the user to enter commands. Up to 63 consoles can be used at one time.

Linux supports several file systems including minix, Xenix, and all the common system V file systems. It also has an advanced file system of its own, ext3, which offers file systems of up to 4 TB and names up to 255 characters long. The ext3 file system is a journalizing file system. Journalizing file systems can be checked for consistency far more quickly than non-journalizing file systems. Today's file system sizes often exceed several hundred gigabytes, and so the difference in recovery time after an ungraceful shutdown can run into several hours.

Linux also supports MS-DOS partitions. You don't need any special commands to use the MS-DOS partition, since it looks similar to a normal Unix file system.

Most Linux distributions provide support for TCP/IP, AppleTalk, NetWare, and LAN Manager/Windows Native (SMB or Server Message Block) client and server. These are protocols for sharing files, printers, serial ports, and communications between computers.