# **Figure 3–10 Local Volume Screen**

![](bbox=[0.09, 0.19, 0.75, 0.54])

The fields, as shown in Figure 3–10, Local Volume Screen, are:

+   - **Source:** The physical hardware; hda indicates an IDE hard drive, fda indicates a diskette drive, and cdrom typically indicates a CD-ROM drive. If your system has a SCSl drive, you will see an sd instead. More than one drive of a type are listed by letters, so hda represents the first IDE drive, while hdb would be the second. In some cases, you’ll see numbers following these letters; on hard drives, the numbers represent the partitions on that drive, while for diskette drives, this number refers to the actual unit.

+   - **Mount point:** This is where in the system the drive is accessible from when mounted.

+   - **FsType:** The type of filesystem. A standard Linux partition uses the ext2 filesystem type. A filesystem type of vfat indicates a DOS filesystem with long filename support, while a fat filesystem type is for DOS filesystems supporting traditional 8.3 filenames. The iso9660 filesystem type indicates a CD-ROM drive.