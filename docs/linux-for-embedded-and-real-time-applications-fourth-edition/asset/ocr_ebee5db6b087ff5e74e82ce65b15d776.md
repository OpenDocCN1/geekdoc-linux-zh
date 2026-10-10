# 22 Chapter 2

much contiguous free space. You can use the Windows defragmentation tool to put all free space at the “end” of the disk.

Windows 7 has a slick disk management tool that handles partitioning. From the Start menu, select Control Panel > Administrative Tools > Computer Management. In the Computer Management dialog, select Storage > Disk Management. That displays the menu shown in Fig. 2.2. This shows five partitions, the largest of which is identified as drive C:.

A little background on disk partitioning is in order here. In the DOS/Windows/PC world, a disk can have up to four primary partitions. Any of these primary partitions can be designated an extended partition, which in turn can hold several logical partitions. There’s no fixed upper limit on the number of logical partitions an extended partition can hold, but owing to the way in which Linux accesses partitions, 12 is the practical upper limit on a single disk drive.

Take a look at the partition list in Fig. 2.2, and compare it with the list in Listing 2.1 derived from the Linux fdisk command on the same disk. This particular machine is already configured for dual booting. Note that fdisk reports six partitions, whereas the Windows Disk Manager only shows five. /dev/sda4 is identified as an extended partition.

![](bbox=[0.15, 0.47, 0.85, 0.86])

**Figure 2.2**
Windows 7 Disk Manager.