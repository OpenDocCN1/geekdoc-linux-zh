# **SETTING UP A RAID DEVICE**

To set up a RAID array (page 42), click the mount point/partition you want to change to a RAID device, select RAID from the drop-down list labeled **Device Type**, and click Update Settings. Anaconda changes the partition to a RAID device. You can then select the type of RAID device you want from the drop-down list labeled **RAID Level**.

# **RECLAIMING DISK SPACE**

There are several situations in which you might want to reclaim disk space by shrinking or deleting a partition. Assuming you are not installing on a clean disk, any partitions on the disk that are not full are candidates for reclaiming space. A typical example occurs when you are working with a hard disk with a single partition that occupies the entire disk, such as when you are setting up a dual-boot system by adding Fedora/RHEL to a Windows system (page 84). In this case you might be able to reclaim space from the Windows partition to install Fedora/RHEL. According to the *ntfsresize man* page, you do not need to defragment a Windows partition before resizing. The process of resizing a partition is the same regardless of the type of partition: You can use the Reclaim Space window to resize Windows, Linux, and other types of partitions.

To reclaim disk space, click **Reclaim space** on the Installation Options window; Anaconda displays the Reclaim Disk Space window (Figure 3-14). This window displays a table listing the partitions on each of the disks you selected in the Installation Destination window (page 67). The table shows the mount point, device name, type of filesystem, amount of reclaimable space, and action to be taken for each partition. Below the table are three buttons: **Preserve**, **Delete**, and **Shrink to**. The default action is to preserve a partition.

![](bbox=[0.33, 0.49, 0.83, 0.9])

**Figure 3-14** The Reclaim Disk Space window showing the slider