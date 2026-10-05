# GRAPHICAL PARTITION EDITORS 67

| 215 GB Hard Disk (VMware, VMware Virtual S5 [1]) - Disk Utility | Serial Number: |
|---|---|
| **Storage Devices section** | |
| **Local Storage** | Model: VMware Virtual S5
| Capacity: 1.0 | Volume Name: |
| Location: /dev/sda | |
| Capacity: 215 GB (214,364,808 bytes) | Connection: |
| SMART Status: Not Supported |
| **Peripheral Devices** | Boot Record: Not Found
| **Drive section** | Format Drive:
| 215 GB Hard Disk (VMware, VMware Virtual S5 [1]) | Volumes
| | Filesystem: /dev/sda1
| Partition Type: Linux (ext4) | Partition Label: |
| Capacity: 212 GB (211,667,698 bytes)|
| Type: ext4 (version 1.0) | Mounted: Not Mounted
| | Mount Volume
| Check Filesystem | Edit List Partitions
| Edit Partition | Delete Partition

Figure 3-13 The palimpsest Disk utility

display information about a hard disk, a hard disk under Storage Devices/Peripheral Devices on the left side of the window.

With a hard disk, the palimpsest Disk utility is divided into three sections (Figure 3-13): Storage Devices holds a list of CD/DVD drives, hard disks, and other devices; Drive section holds information about the hard disk that is highlighted in the list of storage devices; and Volumes displays information about the partition that is highlighted in the graphical representation of the hard drive.

When you select a hard disk in the Storage Devices sections, palimpsest displays information about that disk in the Drive section of the window. Click one of the partitions in the graphical representation of the hard disk and palimpsest displays information about that partition in the Volumes section.

From this window you can view, create, and delete partitions. Although you can create partitions using palimpsest, you cannot specify the mount point (page 35) for it—this step must wait until you are installing Ubuntu and using the ubiqu partition editor. You can save it if you use palimpsest to examine a hard disk and ubiqu to save the partitions onto Ubuntu.

# DISPLAYING THE CONTENTS OF A FILESYSTEM

To display the contents of a filesystem, select the partition holding the filesystem as described above and click Mount Volume in the Volumes section of the Disk Utility window. Figure 3-13 shows Unmount Volume because the partition is already mounted. When palimpsest displays the highlighted filesystem, the mounted filesystem appears as a directory (folder) on the desktop. When you click the mount point (the link following Mount Point: mounted at) in the Volumes section or double-click the directory icon on the desktop, Nautilus displays the files in a file browser window (page 107). When you have finished examining the contents of the filesystem, click Unmount Volume to unmount the filesystem.