# Partitioning Tips

Are Linux and its file systems completely new to you? Then you probably ask yourself questions like: How much space should I assign to Linux? What’s the minimum I need? What’s best for my needs? How should I divide up the available space?

# Partition Types on a PC

Every hard disk contains a partition table that has space for up to four entries. Each entry may be either a primary or an extended partition. Only one extended partition may be assigned.

Primary partitions are a continuous section of cylinders assigned to one operating system. Using primary partitions, you would only be able to create four partitions. More will not fit into the partition table.

An extended partition itself is also a continuous section of cylinders, but you can divide an extended partition into multiple logical partitions, which do not need a separate entry in the partition table. The extended partition is like a container for logical partitions.

If you need more than four partitions, make one an extended partition in which to assign logical partitions. The maximum is fifteen partitions for SCSI systems and sixty-three for (E)IDE systems.

Linux does not care on what kind of partition it is installed. It can be primary or logical.

# Time to Decide

Let’s start with the minimum SuSE Linux install: 180 MB. This only works if you use the machine for a simple purpose, for example, you only work on a text console (no X Window System). If you want to take a look at X and start a few applications, you will need 500 MB. Both values include swap.

What is a reasonable size for an installation? 1 GB — in this world of several gigabyte hard disks, this is quite a modest requirement. There is no upper limit.

What’s the best for your needs? That depends on what you want to do:

+   - Working in X and using applications such as **Applixware** and **Netscape** will require 1.2 GB.
+   - To create your own applications in X, you also need 1.2 GB.
+   - Both of the above items: 2 GB.
+   - To compile your own X servers and write your own CDs together with the items mentioned above: 4 GB.