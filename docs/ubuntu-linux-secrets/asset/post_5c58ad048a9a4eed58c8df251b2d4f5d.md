
## Examining the Current Hard Drive Setup

Before diving into partitioning your existing hard drive, it's a good idea to know what you have to work with. If you already have Microsoft Windows running on the existing hard drive, you can use the utilities included in Windows to examine your system.

The Windows Computer Management console provides a graphical tool for looking at the hard drives installed on your workstation. This tool is available in Windows 2000 Workstation, XP, and Vista. You can get to it by following these steps:

1. Right-click on the My Computer desktop icon or the My Computer entry in the Start menu.
2. Select Manage from the resulting menu. This starts the Computer Management tool window.
3. From the Computer Management tool window, select the Disk Management entry.

The Disk Management tool, shown in Figure 3-3, appears, showing the current hard drives installed on the PC.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_84_0.png)

The Disk Management tool displays all of the hard drives recognized by Windows and shows whether they are formatted and used. Each hard drive appears as a separate line in the list and is shown with the partitions and format types identified.

Many newer workstations utilize a hidden partition to store important recovery information. A hidden partition is a section of the hard drive that’s partitioned, but not assigned a drive letter, by the operating system. Even if you see only a C: drive on your Windows setup, your hard drive may still contain two partitions, as shown in the example in Figure 3-3. The hidden partition can’t be used for Ubuntu, or you’ll lose the ability to restore your Windows system if it crashes.

If you see an area on the hard drive marked unallocated, that means the hard drive has free space that’s not part of the Windows partition. You can use this as part of the Ubuntu partition. If it’s 4 GB or larger, then you don’t have to do anything to your existing Windows partition. You can install Ubuntu directly into the unallocated hard drive areas without having to alter the existing Windows partition.

If you see only a single partition that’s allocated for Windows on your hard drive, you’ll need to continue with the partitioning process to free up space for Ubuntu.

### Determining Free Space

The next step in the partition process is to determine how much free space you have on your existing hard drive. Remember, you’ll need at least 4 GB of free space for Ubuntu, plus you’ll probably want to keep some extra free space for the original operating system.

To find out how much free space is available on your Windows partition, you can turn again to the Windows Computer Management tool. The top portion of the Disk Management window shows detailed statistics for each hard drive partition.

The statistics shown include the total size of the partition and the amount of free space available. Make note of the free space available on the partition. That’s the amount of space you’ll have available to divvy up between the existing Windows partition and the new Ubuntu partition.

> A common mistake is to assign all of the free space on a hard drive to the new Ubuntu partition. You’ll want to keep some free space assigned to the Windows partition; otherwise, the Windows operating system installed might not boot properly. It’s always a good idea to have at least 1 GB of free space available on the Windows partition, even if you’re not planning on adding any new software or data.

Once you’ve determined the amount of space you have available for Ubuntu, the next step is to ensure that the space on the disk is really empty.

### Defragmenting Files

During the normal course of using your workstation, Windows tends to write files at random places on the hard drive. This can spread data over the entire disk space area. When you split the hard drive into partitions, you’ll want to ensure that you don’t lose any of the data used in the Windows system, including system and data files.

To make a clean partition of the hard drive, you’ll need to make sure that all of the Windows data are moved toward one end of the hard drive. This process is commonly done with a defragmenting tool.
