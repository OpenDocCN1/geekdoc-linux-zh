> If you are using RAID or a volume management system, as discussed in Chapter 8, "Installing Linux," you may be interested in additional formatting options beyond those mentioned here. See the man pages as well for information about using these specialized file systems.

When you format a file system, you see many lines of output on the screen as the program lists all of the structure information that is being written to the device. In any case, formatting even a large hard disk is quite fast. On a fast Pentium system, using mke2fs to create a 40 GB file system takes only a couple of minutes.

You can use the fdformat command to format 3.5-inch disks. The format includes the device name of the floppy drive:

```
# fdformat /dev/fd0
```

In addition, a graphical removable disk formatter, gfloppy, can be started by choosing System Tools, then Floppy Formatter on the GNOME main menu. (See Figure 10-9.)

![](bbox=[0.18, 0.58, 0.62, 0.85])

# Figure 10-9 The gfloppy Floppy Formatter

After formatting an ext3 file system using mke2fs, you can use the tune2fs utility to examine the superblock of the file system and make minor changes to the file system parameters. Not all file system parameters can be altered using tune2fs. For example, you cannot change the block size used by the file system without reformatting the file system.

Use tune2fs with the -l option (for "list") to show the superblock of a file system:

```
# tune2fs -l /dev/hda1 | less
```

Although the default settings are sufficient for most system administrators, understanding how file systems are constructed and how you can view and alter their characteristics can