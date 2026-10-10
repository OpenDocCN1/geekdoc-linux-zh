NVRAM is accessed through the /dev/nvram file. This file contains very precisely structured data, so you should *not* try to access it directly. Instead, you can use a utility, such as NVRAM Wakeup (http://sourceforge.net/projects/nvram-wakeup) or tpb (http://www.nongnu.org/tpb). These programs provide specialized functionality to read or write some or all of the NVRAM data.

> **WARNING**
> 
> *Never attempt to write a filesystem to /dev/nvram or otherwise write to it without the help of a program designed to do so. Even using such a program designed for a CPU or BIOS other than the one you’re using could render your system unbootable!*

# # Planning Disk Partitioning

Hard disks can be broken into logical chunks known as *partitions*. In Windows, partitions correspond to drive letters (C:, D:, and so on). In Linux, partitions are mounted as particular points in the Linux directory tree, so they’re accessible as subdirectories. Before installing Linux, it’s a good idea to give some thought to how you’ll partition your hard disk. A poor initial partitioning scheme can become awkward because you’ll run out of space in one partition when another has lots of available space or because the partition layout ties your hands in terms of achieving particular goals.

# ## Understanding Partitioning Systems

Partitions are defined by data structures that are written to specified parts of the hard disk. Several competing systems for defining these partitions exist. On x86 and x86-64 hardware, the most common method up until 2009 has been the *master boot record (MBR)* partitioning system, so called because it stores its data in the first sector of the disk, which is also known as the MBR. The MBR system, however, is limited to partitions and partition placement of 2 terabytes (TB), at least when using the nearly universal sector size of 512 bytes. The successor to MBR is the *GUID partition table (GPT)* partitioning system, which has much higher limits and certain other advantages. The tools and methods for manipulating MBR and GPT disks differ from each other, although there’s substantial overlap.

> **NOTE**
> 
> *Still more partitioning systems exist, and you may run into them from time to time. For instance, Macintoshes that use PowerPC CPUs generally employ the Apple Partition Map (APM), and many Unix variants employ Berkeley Standard Distribution (BSD) disk labels. You’re most likely to encounter MBR and GPT disks, so those are the partitioning systems covered in this book. Details for other systems differ, but the basic principles are the same.*