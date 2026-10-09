![](bbox=[0.3, 0.08, 0.75, 0.42])

**Figure 3-36** The finished partition tables

Highlight **Finish** on the next screen (the one that asks if you want to create an MD device again) and press RETURN. Now you need to tell the installer where to mount the RAID array. Highlight the **RAID** array. In the example, this line contains **\#1 100.0 GB** (this line is highlighted in Figure 3-36, but is shown after the partition is created). Press RETURN. **Highlight Use as:** do not use and press RETURN. The installer displays the HOW to use this partition screen (Figure 3-31, page 89). Highlight the type of filesystem you want to create on the RAID array (typically ext4) and press RETURN. Continue to set up the RAID array as you would any other partition by following the instructions under “Creating a partition” on page 88. In the example, the full 100 gigabytes is used for an ext4 filesystem mounted on /home.

To complete this example, create a bootable / (root) partition using the rest of the free space on the first drive and a 4-gigabyte swap partition on the second drive. Figure 3-36 shows the Partition overview screen that includes these changes. Highlight **Finish partitioning and write changes to disk** (you may have to scroll down to expose this line) and press RETURN.

# # CHAPTER SUMMARY

Most installations of Ubuntu Linux begin by booting from the live/install DVD or the live/install Desktop CD and running a live session that displays a GNOME desktop. To start the installation, double-click the object on the desktop labeled **Install**.