
## 4.3.1 File Systems

![](img/bd9544b8c1ad3b1347c84630c5d698e1_103_0.png)

Figure 4.11: Improved file systems

operating systems today. Linux uses a variant form of this latter approach which also avoids any practical limit in the number of extents used by a file.

### Hierarchy—A Non-Flat File System

The systems described so far have only a single directory. The next level of enhancement is to build a hierarchical file system. This means that there are multiple directories, where a directory contains both ordinary files and subordinate directories.

### Access Control—Ownership and Permissions

Somewhere along the way, the idea of ownership of files appears. Some systems strictly limit file access to the owner, but others have added the idea that file access of another user’s files can be controlled by some permission mechanism.

### Structure—File Types

Some systems find utility in having files identified by type. This typing permits the system to manipulate different files in different ways. For instance, although Unix has only one kind of file which can hold data, other file-like entities exist. Besides ordinary files, directories, character devices, block devices, named pipes, and symbolic links exist in most Unix systems.

Other systems go so far as to have different file types for executable files, random access (text) files, indexed (database) files, sequential (printer output) files, etc.

## Support for Different File Systems

Some system kernels can support different file system structures at the same time. Linux is one such system kernel, perhaps more so than any other system.

Besides its native file system, ext2, and the /proc file system, which reports kernel data, Linux supports conventional file systems such as the ISO 9660 format for CD-ROMs, the FAT-16 file system used by MS-DOS, the Network File System developed by Sun Microsystems, and an encrypted file system. In addition, users are permitted to implement file systems outside of the kernel as user processes.

## /proc File System

The /proc file system grew out of the need to report kernel data to user programs. Before the /proc filesystem, programs had to peek into the kernel memory, which was mapped as a device /dev/kmem, and use the kernel symbol table to decode the contents. This has been superceded by access subroutines which mimic a file system to any user process. Although the data comes from the kernel structures instead of disk storage, the user program sees the data as structured text in a file. For instance, the command cat /proc/version reveals the version number and build time of the currently executing kernel.

This file is system undergoing constant upgrades. Recent changes have made it much easier to add new entries in this file system. One visible change is that it is now possible for the root user to write to some of these entries to cause internal changes to the kernel.

## Windows 95 File System

The file system used by Windows 95 is a modest extension to the FAT-16 file system used by MS-DOS. The most significant change is the addition of support for long file names. The vfat file system⁴ offers Linux the ability to access a partition holding a Windows 95 file system. (This may soon be incorporated into the standard kernel release.)

### Networked File System

Files need not be resident on the local system; they can be located elsewhere. Section 5.3.4 discusses issues and implementation of such extensions.

### Encrypted File System

Two distinct Linux projects have added support for an encrypted file system. Such a system preserves all files, and in some cases directories, in encrypted form. When the file system is mounted, an additional argument provides a password. This password provides protection against someone examining dump tapes or raw disk drives.

### User File Systems

The ultimate example of support for different file systems is the *user file system*. The Linux Software Map offers the following description:

> Userfs allows normal user processes to implement a Linux file system. Such file systems may be mounted by normal users and are indistinguishable from conventional file systems. Because they are normal processes they have access to all the normal system facilities, allowing them to have properties that a kernel resident file system cannot.

## 4.3.2 Virtual Machine

An unusual variation in file system design isolates the partitioning of the disk from the manipulation of the file system structure.

Imagine a system where all references to hardware registers, etc., are trapped and emulated by the system. All other instructions run as they normally would on the base hardware. This provides an execution environment in which a program cannot tell if it is running on the base hardware or in the emulated environment.

Each program which is running is said to be executing on a virtual machine. Thus a virtual machine is an emulation of a machine ... by that very machine!

In this way, it is possible to isolate the file system from the rest of the system kernel. The real disk is partitioned into sections, one for each virtual machine, and disk block addresses are translated for each read and write operation. Synchronization problems such as described in Figure 4.4 then become the major concern of the system kernel and disappear from the file system code. (Of course this method of partitioning and address mapping quickly evolves into a specialized file system itself.)

In this case it is reasonable to place the entire file system management in the hands of a run-time library. A user’s request to open a file is turned into commands to read some number of disk blocks which are then interpreted as directory information and references to data on the disk. Information about open files, character buffering, etc., is maintained in the process’ memory space. When a file is closed, the run-time library can update local information about the file and write it back to the disk. The system kernel is limited to reading and writing specific blocks of data on the disk.

A virtual machine also makes it possible to test and use a new system kernel while other users share the hardware as if they each had an entire machine to themselves.

Section 5.2.5 offers some other uses for a virtual machine.

## 4.4 Memory Management

When the system is little more than a program loader and run-time library, memory management is simple and requires no special hardware support. With multitasking, memory becomes yet another resource which must be managed by the system kernel. There are three major issues in memory management:

- memory allocation
- relocation
- protection

We’ll look at how these issues have been addressed as memory management techniques have developed over time.

## 4.4.1 Non-Mapped

Main memory is partitioned according to its use, such as for buffers, system kernel code, or user program. Programs are always loaded into a well-known location⁵ and they can access all of memory. Figure 4.12a shows how memory is split into various elements.

![](img/bd9544b8c1ad3b1347c84630c5d698e1_107_0.png)

Figure 4.12: Non-mapped memory

While this system is easy to implement, it has disadvantages—foremost are the difficulties in running multiple programs simultaneously. But if there is enough contiguous memory, a second, third, fourth, etc., program can be loaded into the remaining free memory as shown in Figure 4.12b.

Multiple processes can run in harmony provided the programs don’t need to grow (or sufficient memory was pre-allocated for each).

After a while, memory will become fragmented, i.e., the free space will no longer be all in one contiguous place. Figure 4.13 shows how, after a few steps, the free space is fragmented into four smaller chunks. Each time a process is started, it is placed in the lowest addressed space which will hold it. When it finishes, the space is reclaimed, but the other processes aren’t shifted. As a consequence, it is possible that a program which needs less memory than there is free on a system will not fit because the free space isn’t contiguous.

![](img/bd9544b8c1ad3b1347c84630c5d698e1_108_0.png)

Figure 4.13: Memory fragmentation

> ⁵ This location need not be known to the program because the loader may relocate all addresses in the program as the program is loaded. The format of the relocatable executable program is more complicated because it must contain pointers to all the places which must be relocated.
