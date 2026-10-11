+   □ **View all mount points, not just the current volume group.** When you select this option, all partitions and volumes that have entries in `/etc/fstab` are displayed. Otherwise, only the volumes in the selected volume group are displayed.

+   □ **Add.** Adds a new logical volume to the volume group. When you select **Add**, the following appears:

**Figure 4-10**

![](bbox=[0.36, 0.28, 0.62, 0.55])

This dialog lets you configure a logical volume using the same options available for creating a file system (see “Create a File System with YaST” on page 4-21).

In addition, you can enter a logical volume name, the maximum amount of space available (by selecting **max**), the number of stripes (equal or less than the number of disks), and the stripe size (if you configure more than one stripe).

Striping is only useful if you have two or more disks. It can increase performance by allowing parallel file system read and writes, but it also increases the risk of data loss. One failed disk can lead to data corruption in the whole volume group.

+   □ **Edit.** Allows you to change the parameters of a selected volume.