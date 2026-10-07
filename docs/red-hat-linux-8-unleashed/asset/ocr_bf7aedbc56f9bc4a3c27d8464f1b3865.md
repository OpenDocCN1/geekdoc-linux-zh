# CHAPTER 3 Installing Red Hat Linux

![](bbox=[0.213, 0.098, 0.786, 0.353])

FIGURE 3.8 You can use Disk Froid to partition your drive before installing Red Hat Linux.

![](bbox=[0.213, 0.41, 0.786, 0.655])

FIGURE 3.9 Set partition information about a selected or new partition on a hard drive.

Use the Add Partition box to assign a mount point (such as /boot or /), assign a filesystem (such as ext2, ext3, RAID, swap, or vfat), assign the size of the partition, and assign a filesystem check. Remember that, at a minimum, your Red Hat system should have a root (/) and swap partition. The ext3 filesystem is the best choice for your partitions because it is the default for Red Hat, but you can also use ext2 (convert to ext3 later-on—see Chapter 10). The size of the partition can be fixed by entering a number (megabytes), or if you press the spacebar when selecting the Fill All Available Space field, will use all remaining free space.

Use the Check for Bad Blocks item to verify low-level formatting and check the integrity of your hard drive. (This will take a long time on a hard drive with a capacity larger than 10GB.) You can also check your hard drive after installing Red Hat by using various Linux software tools, as shown in Chapter 10. Use the OK button when finished.