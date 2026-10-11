+   10. To create the data logical partition, issue the following keystrokes:
+   
+       n
+       (Press Enter)
+       +1024MB

+   11. Lastly, set the 750MB partition to the type 82, which is used for Linux swap partitions with the following:
+   
+       t
+       2
+       L
+       82

+   12. Check your partition layout with the p command:

| Device | Boot | Start | End | Blocks | Id | System |
|:-------|:-----|:------|:----|:-------|:---|:-------|
| /dev/hda1 | 1 | 25 | 200781 | 83 | Linux |
| /dev/hda2 | 26 | 117 | 730990 | 82 | Linux swap |
| /dev/hda3 | 118 | 847 | 5863725 | 83 | Linux |
| /dev/hda4 | 848 | 2088 | 9968332+ | 5 | Extended |
| /dev/hda5 | 848 | 972 | 1004031 | 83 | Linux |

+   13. Write the changes to the disk with the w command and press Enter.

> **NOTE**
> The system might require a reboot at this point because you've altered the drive on which the system's root (/) partition exists.
> 
> Also note how the first logical partition becomes /dev/hda5 for IDE drives.

# # Disk Druid

Red Hat's Disk Druid partitioning tool comes in two modes or styles. The text-mode, or TUI, tool is present during a text-mode installation of Red Hat and is visually similar to the true GUI-mode tool. The X GUI Disk Druid tool is just that—it runs in X and is present in the GUI install of Red Hat. Disk Druid offers a one-stop shop of partitioning, formatting, and choosing the mount points for the various partitions. It also has some advanced features, such as software RAID, that can be configured with multiple disks.

# ## cfdisk

The cfdisk menu options are context-sensitive, so when you've highlighted the free space, only the create, quit, and write options are selectable. When focused on an existing partition, the appropriate options, such as delete, type, and bootable, are available.