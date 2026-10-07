
## 3 Linux Files and Processes

A Linux system is made up of files of various types; essentially, everything on the system is a file. These files are organized hierarchically into directories, since having all files in one large directory would be far too chaotic. As development in Linux is often done individually or in small groups, it became obvious early on that the hierarchy needed some defined structure that all developers could work within so pieces developed by one group would fit with those developed by another. The basic characteristics of the hierarchy were defined first in the File System Standard (FSSTND), which was the consensus resulting from a lengthy discussion on a specially created Linux mailing list. The Filesystem Hierarchy Standard (FHS), a subsequent version of the FSSTND, was intended to standardize file systems between Linux and Unix for compatibility between different software packages, distributions, and networked systems.

This chapter discusses the history of these two standards and what they brought to Linux. It explains the file concept, including file types and file naming. It looks at the filesystem hierarchy as it has evolved and describes what an inode-based filesystem is. The chapter also discusses the components that form Linux. Finally, you'll learn about the processes that perform the actual work on a Linux system, how to track them, and how to administer them. As a system administrator, you must know the filesystem that you are working on and its restrictions and limitations in order to allocate system space efficiently and avoid pitfalls. Just as with city ordinances, you can sometimes get by without knowing them intimately, but you might find that your lack of knowledge gets you into trouble.

## The Filesystem Hierarchy Standard

The history of the Filesystem Hierarchy Standard encapsulates the open-source developing Linux as a whole. Even if you're not a history buff (or an open source "true believer"), understanding the issues that the developer set out to solve in defining the standard can help you understand the system you're working with today.

Linux Torvalds intended the Linux operating system compensate for the problems encountered when trying to use the Minix operating system. In its very early days, Linux was developed in tandem with the Minix operating system, allowing Linux to share between the Minix and Linux sides. At that point, the Linux filesystem was in fact the Minix filesystem. Soon thereafter, a Virtual Filesystem (VFS) layer was developed to handle the file-oriented system calls and pass the I/O functions to the physical filesystem code, allowing Linux to support multiple filesystems. Used for as an instructional tool, the Minix filesystem supported only 14-character file names and limited its support to smaller than 64 megabytes. In April 1992, after the integration of the VFS into the kernel, a new filesystem, the Extended File System or extfs, was implemented and added to Linux version 0.96c.

Although extfs was significantly more usable than the Minix filesystem, it still lacked some features that Linux wanted. Additionally, its practice of tracking blocks and nodes via a linked list did not allow for optimum performance, because as the filesystem used, the list became unsorted and the filesystem fragmented. Released in alpha version in January of 1993, the Second Extended File System (ext2fs) grew out of the desire to fix the problems of extfs and ensure a focus on excellent performance, robustness, and flexibility to allow users to use new features without having to reform their filesystems. Ext2fs supports filenames as long as 255 characters and filesystems as large as 4GB. Linux is still using this file system, as described in Chapter 10, several more advanced alternatives are starting to become replacements for ext2fs.

Although ext2 solved many technical problems, procedural problems remained; administrators did not always agree on how to use the filesystem. That is, administrators and distribution maintainers didn't put the same files in the same locations, leading to confusion. In August 1993, a programmer named Olaf Kirshitz posted a message to one of the most important Linux discussion groups, discussing the possibility of designing a common standard for filesystem layout. It turned out that many Linux users had some thing to say about this topic, and soon a new mailing list was created specifically to house the discussion. The goal was to form a consensus about creating a standard filesystem hierarchy that would support the needs of the Linux file and directory structure.

NOTE The word filesystem has two meanings. The first refers to the low-level layout of data on the disk, as defined by filesystems like the Minix system, extfs, and ext2fs. The second meaning refers to the placement of files and directories within the directory structure on the disk. Which meaning is intended to be clear from context.

A few of the problems that the Linux community sought to solve:

- The need to define which binaries belonged in /bin and which belonged in /usr/bin
- The disorder caused by having both binaries and configuration files in /etc
- The need to separate site-wide configuration files from local configuration files to facilitate the sharing of these files where appropriate
- The need to make changeable files of /usr so that partition could be mounted as read-only

The consensus for solving these and other problems was formalized into a filesystem hierarchy standard specific to the Linux operating system, called FSSTND. The first official version of the FSSTND was released in February 1994, and two subsequent revisions were released over the next year. The FSSTND defined a standard filesystem structure for Linux systems, mapped where specific types of files and directories were clarified and what was intended to be contained in specific system files. Linux FSSTND 1.2 is the final version of this standard. The major limitation of this standard was that it applied only to Linux and could not be used on networks with "mixed" operating systems. It didn't take long before the Linux specificity drove a push toward a new, open standard.

An effort to create a filesystem standard that would serve Unix operating systems in addition to Linux began in 1995. Many BSD supporters participated in this effort. The goal was to change the focus of the FSSTND, to generalize it that it applied across the board to any Unix-like system. The name of the standard was changed to Filesystem Hierarchy Standard (FHS) to emphasize that it was a new standard.

The FHS may be applied to any filesystem layout that:

- Conforms to a hierarchical structure
- Handles file data consistently
- Includes data-protection mechanisms

![](img/4fb617eb648f87def380ef5d92052d01_84_0.png)

The FHS begins by defining shareable data and unshareable data. Shareable data can be used by more than one host without alteration. Unshareable data is exclusive to one host and would require tailoring for another host. For example, it might be beneficial to share a text document across hosts, but sharing a configuration file that is tailored to the specific hardware on the host machine would not be beneficial.

FHS ensures that shareable files are not interspersed with unshareable files, so that a partition containing shareable data may be shared with another host without making an unshareable file available to that host. In the old Unix standard, shareable files and unshareable files existed together on the same partition. The /usr partition is a good example. It contained unable data until the /var system was created. Now, unshareable/usr files are stored in /var and linked into the /usr directory tree, leaving /usr perfectly shareable.

FHS further distinguishes between static and dynamic files. Static files are files that require superuser permission to change. Program files are a perfect example. Dynamic files are those that may be changed without the superuser's involvement, by some process that runs automatically on schedule or manually by a user without root privileges. Examples include user data and log files.

## The ext2 Filesystem

In order to understand what can be done with files, directories, and filesystems in the directory structure sense, it's helpful to understand some of the data structures that underlie a filesystem in the low-level partition data structure sense. Because ext2fs is the most common Linux filesystem, this section describes ext2fs and its data structures. Other Linux filesystems use similar structures, although some of the details differ. Non-Linux filesystems often differ in more details, but many of the basic principles still apply. (For a discussion of various Linux and non-Linux filesystems, see Chapter 10.)

## The Physical Structure

The ext2 filesystem is composed of block groups, which may or may not be sequential on the physical disk. Figure 3.1 shows the physical structure of an ext2 filesystem.

Each block group contains filesystem control data: a superblock and filesystem descriptors. It also contains filesystem data: a block bitmap, an inode bitmap, an inode table, and data blocks. Inodes are explained in the next section. Normally about 5 percent of these blocks are set aside to allow the superuser to recover a filesystem that has reached its maximum number of user processes and become unusable by ordinary users.
