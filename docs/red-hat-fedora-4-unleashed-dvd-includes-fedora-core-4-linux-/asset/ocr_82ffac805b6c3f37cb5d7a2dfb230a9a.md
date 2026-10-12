but you can also use ext2 (and convert to ext3 later on—see Chapter 37, “Managing the File System”). The size of the partition can be fixed by entering a number (in megabytes), or if you select the Fill All Available Space field, will use all remaining free space (but not yet, as you need to create a partition for swap. Click OK to save the new partition information.

> **TIP**
> 
> You can perform diagnostic checks on your storage media after installing Fedora by using various Linux software tools, as shown in Chapter 37.

Remember: Linux requires at least a root (/) and swap partition. The swap partition should be about twice as large as the amount of installed memory (or more) in order to get the most from your computer if you run a lot of programs or host many users. After you create an initial partition for the root filesystem, repeat the steps to create a new partition, but select swap as the filesystem type using the drop-down menu. Figure 3.10 shows a simple, completed partitioning scheme with a separate /home partition on a server using a 6GB hard drive.

![](bbox=[0.21, 0.45, 0.79, 0.77])

**FIGURE 3.10** Review your partitioning scheme for your hard drive.

Take a moment to review your partitioning scheme. If you are not satisfied with the partitioning, you can make changes by selecting a partition and then using the Edit button to change the partition’s information (such as mount point or type of filesystem). Use the Delete button to delete the partition entry and to free up partition space. You can then use the New button again to create partitions in the space that is now free. When satisfied, click Next to continue the install.