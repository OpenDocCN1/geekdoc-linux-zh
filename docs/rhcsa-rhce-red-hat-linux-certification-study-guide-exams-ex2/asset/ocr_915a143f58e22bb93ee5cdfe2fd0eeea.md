that appears at the bottom of the window, which opens the window shown in Figure 6-7.

10. In the Create New Logical Volume window, you can configure the amount of space assigned to the LV, the format, and the mount point. In Figure 6-7, I've allocated half the space to NewLV, formatted it to ext4, and set it to be mounted on the previously created /test directory. If you were to also select the Mount When Rebooted option, the tool would also configure the LV in the /etc/fstab file.

This new LV is now ready for a new filesystem; you can copy desired files to the /test directory, unmount it, and change /etc/fstab to mount it on a different directory. But for the purpose of this section, complete Step 10, but don't make any further changes to the /test directory or the /etc/fstab file. If you want to see the changes reflected in the Logical Volume Management tool, click View | Reload.

# FIGURE 6-7

Create a New Logical Volume

![](bbox=[0.35, 0.55, 0.75, 0.85])