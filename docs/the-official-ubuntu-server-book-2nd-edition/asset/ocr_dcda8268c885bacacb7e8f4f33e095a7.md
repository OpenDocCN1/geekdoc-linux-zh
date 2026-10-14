arrays that are ready to use after the install completes, so if you are installing a new machine, it makes sense to set up the RAID from the installer.

RAID configuration is done during the partitioning section of the install process. Once you see the main partition screen, select “Manual partitioning.” In my example I set up RAID on a three-disk machine. I have a three-partition RAID 1 array for /boot, a three-partition RAID 5 array for /, and a three-partition RAID 5 array for swap.

The first step is to partition each of the disks so they have a /boot, /, and swap partition. When you size the partitions, keep in mind that RAID 1 arrays are only as big as one of the partitions, whereas RAID 5 arrays are as big as all of the partitions combined, minus the size of one partition. While it’s not required that each partition be equal in size, the arrays base everything on the smallest partition, so if you can make each partition in an array the same size, you will have an easier time.

When you get to the partition settings for each new partition, the section where you can choose the file system and mount point, change the “Use as” option so that it says “physical volume for RAID,” as shown in Figure 10-1.

![](bbox=[0.236, 0.587, 0.744, 0.884])

**Figure 10-1** Partition settings for software RAID