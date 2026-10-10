# Partition Basics

Linux requires at least one partition for the *root filesystem*, which will hold the Linux kernel itself.

You can think of a *filesystem* as a partition formatted for Linux. Filesystems are used to hold files. Every system must have a root filesystem, at least. However, many users prefer to use multiple filesystems—one for each major part of the directory tree. For example, you may wish to create a separate filesystem to hold all files under the `/usr` directory. (Note that on Unix systems, forward slashes are used to delimit directories, not backslashes as with MS-DOS.) In this case you have both a root filesystem and a `/usr` filesystem.

Each filesystem requires its own partition. Therefore, if you're using both root and `/usr` filesystems, you'll need to create two Linux partitions.

In addition, most users create a *swap partition*, which is used for virtual RAM. If you have, say, 4 megabytes of memory on your machine and a 10-megabyte swap partition, you have 14 megabytes of virtual memory as far as Linux is concerned.

When using swap space, Linux moves unused pages of memory out to disk, allowing you to run more applications at once on your system. However, because swapping is often slow, it's no replacement for physical RAM. But applications that require a great deal of memory (such as the X Window System) often rely on swap space if you don't have enough physical RAM.

Nearly all Linux users employ a swap partition. If you have 4 megabytes of RAM or less, a swap partition is required to install the software. It is strongly recommended that you have a swap partition anyway, unless you have a great amount of physical RAM.

The size of your swap partition depends on how much virtual memory you need. It's often suggested that you have at least 16 megabytes of virtual memory total. Therefore, if you have 8 megs of physical RAM, you might want to create an 8-megabyte swap partition. Note that swap partitions can be no larger than 128 megabytes in size. Therefore, if you need more than 128 megs of swap, you must create multiple swap partitions. You may have up to 16 swap partitions in all.

You can find more on the theory of swap space layout and disk partitioning in the *Linux Partition mini-HOWTO* (<http://MetaLab.unc.edu/LDP/HOWTO/mini/Partition.html>).