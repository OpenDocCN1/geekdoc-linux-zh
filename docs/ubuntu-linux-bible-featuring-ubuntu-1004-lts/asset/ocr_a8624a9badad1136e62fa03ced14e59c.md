# Part II: Ubuntu for Desktop Users

The panes display information about the storage device that is currently selected. The dropdown list in the upper-right corner lists all the storage devices that are currently detected on your system, and provides information about the storage capacity of each device and the Linux device node through which device can be accessed. Once a device is selected from the list, the pane at the bottom displays a summary of how storage device is currently partitioned, as shown in Figure 20-16. The top pane shows a graphical view of the partitions on the selected disk, while the bottom pane identifies each partition, the device node through which it can be accessed, its format, and so on. For example, the partition list for the disk that is selected is mounted as / and, therefore, contains the current system's root filesystem.

After adding a new disk to your system, select each device in the dropdown list to examine its current partitioning until you find the device that is associated with the new drive. Figure 20-17 shows the entry for a new disk that has not been partitioned.

![](bbox=[0.078, 0.3995, 0.706, 0.7555])

When working with a new, unformatted disk, you will first need to create a partition table so that you can subsequently create one or more partitions on the disk. To do this, select Device -> Create Partition Table. A dialog appears, warning you that creating a partition table on the device will erase all data on the disk (because doing so deletes any existing partitioning information that may currently be present on this disk).