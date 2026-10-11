34 CHAPTER 2 INSTALLATION OVERVIEW

# DEFAULT PARTITIONING

It can be difficult to plan partition sizes appropriately if you are not familiar with Linux. During installation, Fedora/RHEL provides *default partitioning*. Without asking any questions, default partitioning divides the portion of the disk allotted to Fedora/RHEL into three partitions. One partition is the boot partition (*boot*), which is generally 200–500 megabytes (page 35). The rest of the disk is set up as a volume group that you can control with LVM (Logical Volume Manager; page 38). Default partitioning divides the volume group into two logical volumes (partitions). The first logical volume, which holds swap space, can be any size from 512 megabytes to 2 or more gigabytes. The other logical volume is designated as / (root) and contains the remainder of the disk space. See the next section for a discussion of the advantages of manual partitioning.

# MANUAL PARTITIONING: PLANNING PARTITIONS

This section discusses additional partitions you may want to create. Consider setting up LVM (page 38) *before* you create partitions (LVs); LVM allows you to change partition sizes easily after the system is installed. Default partitioning uses LVM.

If you decide to manually partition the hard disk and set up partitions other than a root partition (/) and a swap partition, first consider which kinds of activities will occur under each top-level subdirectory. Then decide whether it is appropriate to isolate that subdirectory by creating a filesystem and mounting it on its own partition. Advantages of creating additional filesystems include these points:

+   * Separating data that changes frequently (e.g., *\ /var* and *\ /home*) from data that rarely changes (e.g., *\ /usr* and *\ /boot*) can reduce fragmentation on the less frequently changing filesystems, helping to maintain optimal system performance.
+   * Isolating filesystems (e.g., *\ /home*) can preserve data when you upgrade or reinstall Linux.
+   * Additional filesystems can simplify backing up data on a system.
+   * If all directories are part of a single filesystem, and if a program runs amok or the system is the target of a *DoS attack* (page 1080), the entire disk can fill up. System accounting and logging information, which may contain data that can tell you what went wrong, may be lost. On a system with multiple filesystems, such problems typically fill a single filesystem and do not affect other filesystems. Data that may help determine what went wrong will likely be preserved and the system is less likely to crash.

The following paragraphs discuss the advantages of making each of the major top-level subdirectories a separate, mountable filesystem. Any directories you do not create filesystems for automatically become part of the root (/) filesystem. For example, if you do not create a *\ /home* filesystem, /home is part of the root (/) filesystem.

Linux temporarily stores programs and data on a swap partition when it does not have enough RAM to hold all the information it is processing. The swap partition is also used when you hibernate (suspend to disk) a system. The size of the swap partition should be between one and two times the size of the RAM in the system, with