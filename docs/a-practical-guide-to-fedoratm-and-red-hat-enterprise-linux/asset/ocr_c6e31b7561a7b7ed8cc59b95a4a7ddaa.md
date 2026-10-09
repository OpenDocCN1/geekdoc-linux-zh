![](bbox=[0.33, 0.1, 0.83, 0.36])

# Figure 3-18  A disk without a partition table

follows the **Contents** label and the graphical representation of the disk is marked **Unknown**. If the disk you are working with already has a partition table, skip to the next section.

To partition a hard disk, click the gears icon at the upper-right of the Disks window (not the one below the graphical image of the disk) and select **Format** from the pop-up menu: `gnome-disks` opens a Format Volume window. Unless you want to explicitly erase the data on the disk, accept the default of **Don't overwrite existing data** from the drop-down list labeled **Erase**. In the drop-down list labeled **Partitioning**, accept the default of **Compatible with modern systems** .... You can enter a name in the text box labeled **Name** if you like. Click **Format**; `gnome-disks` displays another window to confirm you want to format the disk. Click **Format** again. The `gnome-disks` utility takes a moment to format the disk, quickly displaying some information while it is working. When it is done, **GUID Partition Table** follows the **Partitioning** label, the graphical representation of the disk is marked **Free Space** (page 36), and **Unallocated Space** follows the **Contents** label.

If you want to create a single filesystem that occupies the entire disk drive, instead of following the instructions in the preceding paragraph, click the gears icon in the graphical representation of the disk and select Format from the drop-down menu; `gnome-disks` opens a Format Volume window. To create a filesystem, make a selection from the Type drop-down menu and click **Format**.

# CREATING A PARTITION AND A FILESYSTEM

Once you have created a partition table, you will be able to create a partition that holds a filesystem in the free space. Highlight the area marked **Free Space** and click