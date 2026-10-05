# CD-ROM and network file systems

+   * The iso9660 driver allows access to CD-ROMs. ISO 9660 has emerged as the standard for file management on CD-ROMs. Thanks to ISO 9660 it is possible to read the same CD-ROM on the most varied computers and operating systems.

Originally, ISO 9660 envisaged only short file names. Depending on the operating system, long file names are supported by different and mutually incompatible extensions. already in version 1. Linux was able to cope with the Rock-ridge extension commonly used under Unix. Since kernel 2.2 (more precisely, since more recent 2.0.11 versions), Linux also supports the Joliet extension used by Microsoft.

+   * File systems need not be located on the local hard disk – they can also be mounted through a network. Currently, the Linux kernel supports four file systems:

nfs (Network File System) is the most important variation over Unix.
coda is best compared with NFS. It provides a large number of additional functions, but is not very widely used.
cnp (Network Core Protocol) is the Novell variation.
smb (Server Message Buffer) is the network file system of Microsoft.

# Others

The proc file system is not really a file system. It is used for mapping of administrative information of the kernel or of process management. Details can be found on page 117.

Besides the file systems mentioned above, Linux supports a number of other file systems (such as those of the Commodore Amiga, the Apple Macintosh, the Arcon, and so on), which will not be discussed in the framework of this book.

# 5.4 File system internals

This is not a Unix textbook – thus, a long-winged explanation of how the Linux file system is structured and managed internally is really out of place. On the other hand, some further background knowledge will certainly provide a better understanding of typical Unix and Linux file system features – for example, links.

# Internals of the ext2 file system

# Group picture

The following subsections contain many simplifications. For example, for reasons of speed and security, some administration data is stored several times – a fact that, for the sake of simplicity, is ignored. You will find further details (including some very