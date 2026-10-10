+   4.  From the System Tools submenu of the Applications menu, search for the GParted Partition Editor application and select it. The GParted graphical partitioning tool opens, displaying your current disk partitions.

+   5.  Select the disk (probably /dev/sda) and partition (probably NTFS or VFAT for a Windows partition) you want to resize. The Resize/Move button should become available.

+   6.  Select the Resize/Move button to open a Resize/Move pop-up windows.

+   7.  Grab the slider bar from the right and move it to select how much you want to resize your partition. The New Size box shows the new size of your partition. The Free Space Following MiB box shows how much free space you will have after you are done. Figure 2-1 shows a number of partitions as managed from the GParted window.

+   8.  Click Resize/Move to begin resizing your partition. When it is done, you will see the resized partition and a new entry showing the free space.

> **CAUTION:** The resize is committed in the next step. You can quit now without making any changes if you are nervous. In any case, make sure that the partition you are resizing is not mounted. (In this example, I'd type `umount /dev/sda1` as root user from a shell before running the next step.)

+   9.  If the new partition sizes look alright, click Apply to commit the changes.

+   10. At this point, you can close the GParted window and begin the regular installation procedure for Fedora, using the disk space that you just freed up.

![](bbox=[0.16, 0.54, 0.81, 0.86])

**Figure 2-1:** Use GParted to resize your Windows NTFS partitions.