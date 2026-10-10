# CHAPTER 18
# Understanding Hard Disks and Filesystems

This chapter tries to make sense of what is surely one of the ugliest parts of dealing with a Unix system: disks. Compared to a Windows system (where a disk is automatically assigned a drive number by the BIOS) or a Macintosh (where a new disk simply appears on the desktop), Unix systems require a deeper knowledge of geometry, partitions, access modes, and other such esoterica. FreeBSD is, unfortunately, no exception.

As you learned in Chapter 8, "The FreeBSD Filesystem," the hierarchical filesystem structure of Unix does provide a more flexible way of dealing with files than is possible with traditional desktop operating systems. This flexibility comes at a price, however. To add a new disk to the FreeBSD system, it must first be installed in the proper physical position and then sliced, partitioned, labeled, and finally mounted at the selected mount point. This is a far cry from the two or three steps necessary to add a new disk in most desktop systems.

Times are changing, and the progress of hardware standards has eliminated the need for some of the really nasty underlying pencil-and-paper work that used to accompany the installation of a new disk. With the right knowledge (and the help of your good friend sysinstall), you can get the rest of the process under control.

# ## IDE/ATA Access Modes

The most common type of hard disk for PC hardware is the Integrated Drive Electronics (IDE) interface. The IDE interface is so named because the controller chips that manage the disk are integrated into the drive itself, rather than on a separate host adapter card (as with SCSI). The official name for this type of interface is Advanced Technology Attachment (ATA), and ATA and IDE are often used interchangeably.

# **IN THIS CHAPTER**

+   - IDE/ATA Access Modes
+   - SCSI Disks
+   - Understanding Hard Disk Geometry
+   - Partitioning a Hard Disk
+   - Creating the Disk Labels
+   - Making the Filesystem Available for Use