
## DELETING A PARTITION

Before you delete a partition, make sure it does not contain any data you need. To use *gparted* to delete a partition, highlight the partition you want to delete, click the circle with a line through it, and then click the green check mark on the toolbar.

### palimpsest: The GNOME Disk Utility

The *palimpsest* graphical disk utility can create, remove, and modify partitions and filesystems on many types of media, including internal and external hard disks, CD/DVDs, and USB flash drives. It can encrypt partitions and change passwords on already encrypted partitions.

Open the Palimpsest Disk Utility window by selecting **Main menu: System → Administration → Disk Utility** (just above **GParted** in Figure 3-10 on page 64). To display information about a hard disk, click a hard disk under Storage Devices/Peripheral Devices on the left side of the window.

With a hard disk selected, the palimpsest Disk Utility window is divided into three sections (Figure 3-13): Storage Devices holds a list of CD/DVD drives, hard disks, and other devices; Drive holds information about the hard disk that is highlighted in the list of storage devices; and Volumes displays information about the partition that is highlighted in the graphical representation of the hard drive.

When you select a hard disk in the Storage Devices section, palimpsest displays information about that disk in the Drive section of the window. Click one of the partitions in the graphical representation of the hard disk and palimpsest displays information about that partition in the Volumes section.

From this window you can view, create, and delete partitions. Although you can create partitions using palimpsest, you cannot specify the mount point (page 35) for a partition—this step must wait until you are installing Ubuntu and using the ubiquity partition editor. You can save time if you use palimpsest to examine a hard disk and ubiquity to set up the partitions you install Ubuntu on.

### DISPLAYING THE CONTENTS OF A FILESYSTEM

To display the contents of a filesystem, select the partition holding the filesystem as described above and click Mount Volume in the Volumes section of the Disk Utility window. Figure 3-13 shows Unmount Volume because the partition is already mounted. When palimpsest mounts the highlighted filesystem, the mounted filesystem appears as a directory (folder) on the desktop. When you click the mount point (the link following Mount Point: mounted at) in the Volumes section or double-click the directory icon on the desktop, Nautilus displays the filesystem in a file browser window (page 107). When you have finished examining the contents of the filesystem, click Unmount Volume to unmount the filesystem.

![](img/2344fc4a798f29dca9e8b5ed7288171a_118_0.png)

The palimpsest Disk Utility showing a disk without a partition table

### WRITING A PARTITION TABLE

A new disk does not have a partition table (page 33) and looks similar to the disk highlighted in Figure 3-14. In the Drive section of a Disk Utility window, **Not Partitioned** follows the Partitioning label, the graphical representation of the disk is marked Unknown, and Usage is blank. If the disk you are working with already has a partition table, skip to the next section.

To partition a hard disk, click Format Drive in the Drive section of the Disk Utility window: palimpsest opens a Format window showing a drop-down list labeled Scheme. Select a scheme. In most cases you will want to accept the default scheme of Master Boot Record. Click Format. After checking that you really want to format the drive, palimpsest creates the partition table. Now Master Boot Record follows the Partitioning label, the graphical representation of the disk is marked Free (free space; page 33), and Unallocated Space follows the Usage label.

If you want to create a single filesystem that occupies the entire disk drive, instead of following the instructions in the preceding paragraph, click Format Volume in the Volumes section of the Disk Utility window: palimpsest opens a Format whole-disk volume window. To create a filesystem, follow the instructions for the Create partition window in the next section.

### CREATING A PARTITION AND A FILESYSTEM

Once you have created a partition table, you will be able to create a partition that holds a filesystem in the free space. When you click Create Partition, palimpsest opens a Create partition window (Figure 3-15).

![](img/2344fc4a798f29dca9e8b5ed7288171a_119_0.png)

Figure 3-15 The *palimpsest* Create partition window

In this window, use the slider labeled *Size*, or the adjacent *spin* box, to specify the size of the new partition. Next specify a filesystem type; **ext4** filesystems are the most common. You can optionally enter a disk label in the text box labeled *Name*. This name is not the mount point for the disk. Typically you will want to own the filesystem, so allow the tick to remain in the check box labeled *Take ownership of file system*. If you want the filesystem to be encrypted, put a tick in the check box labeled *Encrypt underlying device*. Click **Create**. After checking with you, *palimpsest* creates the filesystem. Now the graphical representation of the disk is divided to represent the division of the hard disk and *Usage* corresponds to the highlighted section of the graphical representation (Filesystem or Unallocated Space). If you did not use all the free space, you can create additional partitions and filesystems in the same manner.

### Deleting a Partition

Before deleting a partition, make sure it does not contain any data you need. To use the *palimpsest* utility to delete a partition, highlight the partition you want to delete in the graphical representation of the hard disk and click **Delete Partition**. After checking with you, *palimpsest* deletes the partition.

### Using SMART to Display Disk Performance Information

SMART (Self-Monitoring, Analysis, and Reporting Technology) monitors hard disks and attempts to predict hard disk failures. To see a SMART report for a disk on the system, highlight the disk in the *Storage Devices* section and click **Smart Data** in the Drive section; *palimpsest* displays a window similar to the one shown in Figure 3-16.

![](img/2344fc4a798f29dca9e8b5ed7288171a_120_0.png)

Figure 3-16.  SMART data as displayed by *palimpsest*

From this window you can run various self-tests and scroll through the information at the bottom of the window.

### ubiquity: SETTING UP PARTITIONS

While you are installing Ubuntu, *ubiquity* offers two ways to partition a disk: guided and manual. Guided partitioning sets up two partitions—one for swap space (page 37) and one for / (root, where the entire Ubuntu filesystem gets mounted; page 37). The amount of space occupied by root depends on which guided option you select. Manual partitioning enables you to set up partitions of any type and size; you can also specify the mount point for each partition.

### ADVANCED GUIDED PARTITIONING

“Prepare Disk Space” on page 60 explained how to use guided partitioning to partition an empty disk. This section explains how guided partitioning works on a disk that is already partitioned.

Depending on the contents of the hard disk you are installing Ubuntu on, the ubiquity partition editor presents different choices. Figure 3-17 shows the Prepare disk space screen for a hard disk with one partition that occupies the entire disk. That partition holds a Windows system. This screen shows all possible choices. In some cases, not all of these choices appear. Click the radio button adjacent to a choice to select it. The choices possible are outlined here:

- **Install them side by side, choosing between them each startup**—Allows you to shrink a partition and use the space freed up by this operation to install Ubuntu. You can use this choice to set up a dual-boot system
