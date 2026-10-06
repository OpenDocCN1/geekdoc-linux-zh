# Linux Administration: A Beginner's Guide

![](bbox=[0.14, 0.09, 0.86, 0.415])

**Figure 7-2** Data structure on ext2 file systems

and it contains i-nodes and data. One group consists of 8192 blocks; thus, the first redundant superblock is at 8193, the second at 16,385, and so on. The designers of most Linux systems intelligently included this superblock redundancy into the file system design.

# ext3

The extended file system (ext3) is another popular Linux file system used by the major Linux distributions. The second extended file system (ext2) forms the base of ext3. The ext3 file system is an enhanced extension of the ext2 file system.

As of writing, the ext2 file system on which ext3 is built is more than 22 years old. This means two things for us system administrators: First and foremost, ext3 is rock-solid. It is a well-tested subsystem of Linux and has had the time to become optimized. Second, other file systems that were considered experimental ext2 was made mature and became available to Linux.

In addition to ext3, the other file systems are potential replacements for ext2 offer significant improvements in performance and stability, but their most important component is that they have moved to a new method of getting the data to the disk. This new method is called journaling. Traditional file systems (such as ext2) must search through the directory structure, find the right place to lay out the data, and then lay out the data. (Linux can also cache the whole process, including the directory updates, thereby making the process appear faster to the user.) Almost all new versions of Linux distributions now make use of one journaling file system or the other by default, including Fedora (and other Red Hat Enterprise Linux [RHEL] derivatives), openSUSE, and Ubuntu.