continued

+   8. Press Enter to confirm your modified partition map. You'll see the following message displayed:
    `Enter table name (remember quotes):`
9. Name the modified partition table and press Enter:
    `Enter table name (remember quotes): c0t3d0.2gb`
10. After entering the name, the following message will be displayed:
    `Ready to label disk, continue?`
11. Type yes and press Enter to continue.
12. Type quit (or q) and press Enter to exit the partition menu. The main menu will be displayed.
13. Type quit and press Enter to exit the format utility.

# Recovering Disk Partition Information

It's always a good idea to save a disk's VTOC (Volume Table of Contents) to a file using the prtvtoc command described earlier. This information can then be used later to restore the disk label if your current VTOC becomes corrupted or accidentally changed or you need to replace the disk drive.

By saving the output from the prtvtoc command into a file on another disk, you can reference it when running the fmthard command. The fmthard command updates the VTOC on hard disks.

# STEP BY STEP

# 6.4 Recovering a VTOV (Volume Table of Contents)

To recover a VTOC, follow these steps:

+   1. Run the format utility on the disk, and label it with the default partition table.