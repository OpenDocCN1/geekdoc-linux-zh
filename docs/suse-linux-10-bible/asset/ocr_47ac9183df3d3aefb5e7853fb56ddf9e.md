# Chapter 14 ◆ Working with the System

# 377

![](bbox=[0.183, 0.121, 0.816, 0.502])

**Figure-14-2:** The YaST Repair mode Expert Tools screen

In order to see all of these options, you will have to use the scroll bar at the right of the screen to scroll down. SUSE's Repair mode assumes a fixed screen height/width ratio and thus can't show all of them at once.

The boot loader tool enables you to create a new boot loader configuration from scratch and install it to the Master Boot Record. The partitioning tool is YaST's standard partitioning module (clearly a dangerous tool; see the next section of this chapter).

The File System and Verified Installed Software options have the same function as the equivalent items discussed in the previous section.

Recover Lost Partitions scans the disk and attempts to restore any partitions that might have been deleted from the partition table (possibly by reckless use of the partitioning tool or `fdisk`).

Finally, Save System Settings to Floppy Disk backs up important system files and the Master Boot Record to a floppy disk.