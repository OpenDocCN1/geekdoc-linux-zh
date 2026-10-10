| Resource | Linux | FreeBSD |
| :--- | :--- | :--- |
| System startup scripts | `/etc/rc.d` | `/etc/rc.*` |
| User-installed startup scripts | `/etc/rc.d` | `/usr/local/etc/rc.d` |
| User-installed executables | `/usr/bin` | `/usr/local/bin` |
| User-installed libraries | `/usr/lib` | `/usr/local/lib` |
| User-installed shared files | `/usr/share` | `/usr/local/share` |
| System documentation | `/usr/doc` | `/usr/share/doc` |
| Documentation for user-installed software | `/usr/doc` | `/usr/local/share/doc` |

Some of these resource locations differ because of the differences between the RPM method (the widely used Linux package manager) and the FreeBSD ports/packages method of software installation. Other location differences exist because of differences in the core system layout. Linux typically has more of a "System V" structure, whereas FreeBSD is, well, BSD-like. Refer to Chapter 14 for a fuller discussion of how ports and packages work under FreeBSD.

# Partitions and Filesystem Types

The Ext2FS filesystem used by Linux takes a very DOS-like approach to disk partitioning: There are four primary BIOS partitions, one of which can be made into an "extended partition" with multiple "logical" partitions inside it. These partitions all appear on the same "level" to the user, even though the structure is, in fact, hierarchical. The system can be booted only from a nonextended partition, thus leading to a lot of potential confusion.

FreeBSD's hierarchical partition structure is much more overt. BIOS partitions are called *slices*, subpartitions are called *partitions* or *BSD partitions*, and the boot process handles the different levels explicitly in order to remove the mystery associated with extended and primary partitions. Setting up a disk involves first slicing and then partitioning the disk. This process is described in detail in Chapter 18, "Understanding Hard Disks and Filesystems."

FreeBSD's native filesystem is UFS/FS. You can use your Linux disks under FreeBSD without modification, but you will need to recompile the FreeBSD kernel to support Ext2FS. See Chapter 16, "Kernel Configuration," for instructions on how to enable this option and build yourself a new kernel.

# Ports and Packages

Coming from a Linux background, you may be used to installing software through the RPM utility. This is not widely used or recommended in FreeBSD. In fact, you can seriously damage your system by installing incompatible libraries into places such as /usr/lib, although it is possible to do if you really need to. The preferred method of installing and maintaining software in FreeBSD is through the package tools (pkg_*) or the ports. Chapter 14 offers a full explanation of ports and packages, but some aspects of how they