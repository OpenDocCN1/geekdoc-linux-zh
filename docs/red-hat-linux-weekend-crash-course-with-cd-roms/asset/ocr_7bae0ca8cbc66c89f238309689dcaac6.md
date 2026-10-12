# Mounting a file system on a device

In Red Hat Linux, you use a physical disk partition by associating it with a specific part of the file system. This is a hierarchical arrangement of directories — a directory tree. If you have more than one disk partition (you may have a second disk with a Linux partition), you can use all of them in Red Hat Linux under a single directory tree. All you have to do is decide which part of the Linux directory tree should be located on each partition — a process known in Linux as mounting a file system on a device. (The disk partition is a device.)

![](bbox=[0.17, 0.33, 0.28, 0.4])

The term mount point refers to the directory you associate with a disk partition or any other device.

Suppose that you have two disks on your PC, and you have created Linux partitions on both disks. Figure 2-3 illustrates how you can mount different parts of the Linux directory tree (the file system) on these two partitions.

![](bbox=[0.22, 0.51, 0.66, 0.74])

Figure 2-3
An example of mounting the Red Hat Linux file system on two disk partitions

# Understanding swap partition

Most advanced operating systems support the concept of virtual memory, in which part of your system’s hard disk functions as an extension of the physical memory (RAM). When the operating system runs out of physical memory, it can move (or swap out) the contents of currently unneeded parts of RAM to make