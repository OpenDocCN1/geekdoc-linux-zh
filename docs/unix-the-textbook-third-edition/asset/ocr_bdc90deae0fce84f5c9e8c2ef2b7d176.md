![](bbox=[0.35, 0.09, 0.65, 0.38])

FIGURE 24.1 ZFS component relationships.

Working with ZFS in UNIX is a matter of efficiently and easily managing zpools, vdevs, file systems, and files.

Figure 24.1 shows this relationship between files, datasets (file systems), pools, and disks. Pool 1 has two disks mapped to it, and a dataset with a number of files in it. Pool 2 has a single disk mapped to it, and has a dataset in it. This layering of files and datasets, pools, and disks is the basic structure of ZFS.

# 24.1.4 Important ZFS Concepts

Some very important points have to be made here:

+   1. Only one zpool can be mapped or associated with any vdev. So if you want to create a zpool on a physical hard disk or one of its slices, no other existing active zpool can be mapped to that vdev!

+   2. There are seven types of vdev in ZFS:

+   - Disk (default): The physical hard drives in your system, usually the whole drive or primary slice

+   - File: The absolute path of preallocated files/images, similar to the Section 24.2.2, Example 24.1

+   - Mirror: Standard software RAID1 mirror

+   - Raidz1/2/3: Nonstandard distributed parity-based software RAID levels

+   - Spare: Hard drives marked as a hot spare for ZFS software RAID

+   - Cache: Device used for a level-2 adaptive read cache (L2ARC)

+   - Log: A separate log (SLOG) called the ZFS intent log (ZIL)