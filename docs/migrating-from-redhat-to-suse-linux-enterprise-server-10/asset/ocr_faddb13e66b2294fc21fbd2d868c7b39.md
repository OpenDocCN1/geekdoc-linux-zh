# ## Objective 4

# ## Configure Logical Volume Manager (LVM) and Software RAID

Logical volume manager (LVM) provides a higher-level view of the disk storage on a computer system than the traditional view of disks and partitions. This gives you much more flexibility in allocating storage space to applications and users.

After creating logical volumes with LVM, you can (within certain limits) resize and move logical volumes while they are still mounted and running.

You can also use LVM to manage logical volumes with names that make sense (such as “development” and “sales”) instead of physical disk names such as “sda” and “sdb.”

To configure a file system with LVM, you need to know the following:

+   *   Use LVM Components
+   *   Use LVM Features
+   *   Configure Logical Volumes with YaST
+   *   Configure LVM with Command Line Tools

The Linux Kernel is capable of combining hard disks to arrays with the RAID levels 0, 1, 5, and 6. Software RAID is covered in

+   *   Manage Software RAID

# **Use LVM Components**

Conventional partitioning of hard disks on a Linux file system is basically inflexible. When a partition is full, you usually have to move data to another medium before you can resize the partition, create a new file system, and copy the files back.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**