![](bbox=[0.18, 0.07, 0.96, 0.37])

display information about a hard disk, click a hard disk under Storage Devices/Peripheral Devices on the left side of the window.

With a hard disk selected, the palimpsest Disk Utility window is divided into three sections (Figure 3-13): Storage Devices holds a list of CD/DVD drives, hard disks, and other devices; Drive holds information about the hard disk that is highlighted in the list of storage devices; and Volumes displays information about the partition that is highlighted in the graphical representation of the hard drive.

When you select a hard disk in the Storage Devices section, palimpsest displays information about that disk in the Drive section of the window. Click one of the partitions in the graphical representation of the hard disk and palimpsest displays information about that partition in the Volumes section.

From this window you can view, create, and delete partitions. Although you can create partitions using palimpsest, you cannot specify the mount point (page 35) for a partition—this step must wait until you are installing Ubuntu and using the ubiquity partition editor. You can save time if you use palimpsest to examine a hard disk and ubiquity to set up the partitions you install Ubuntu on.

# DISPLAYING THE CONTENTS OF A FILESYSTEM

To display the contents of a filesystem, select the partition holding the filesystem as described above and click Mount Volume in the Volumes section of the Disk Utility window. Figure 3-13 shows Unmount Volume because the partition is already mounted. When palimpsest mounts the highlighted filesystem, the mounted filesystem appears as a directory (folder) on the desktop. When you click the mount point (the link following Mount Point: mounted at) in the Volumes section or double-click the directory icon on the desktop, Nautilus displays the filesystem in a file browser window (page 107). When you have finished examining the contents of the filesystem, click Unmount Volume to unmount the filesystem.