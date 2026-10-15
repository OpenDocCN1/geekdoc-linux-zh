# File System Tuning

Never content to leave things alone, Linux provides several tools to adjust and customize the file system settings. The belief is that hardware manufacturers and distribution creators tend to select conservation settings that will work well all the time, leaving some of the potential of your system leashed—that’s why you have chosen Ubuntu Unleashed to help you.

The Linux file system designers have done an excellent job of selecting default values used for file system creation and the 2.6 version of the Linux kernel now contains new code for the IDE subsystem that significantly improves I/O(input/output) transfer speeds over older versions, obviating much of the need for special tweaking of the file system and drive parameters if you use IDE disks. Although these values work well for most users, some server applications of Linux benefit from file system tuning. As always, observe and benchmark your changes.

# Synchronizing the File System with sync

Because Linux uses buffers when writing to devices, the write will not occur until the buffer is full, until the kernel tells it to, or if you tell it to by using the sync command. Traditionally, the command is given twice, as in the following:

```
# sync ; sync
```

It is really overkill to do it twice. Still, it can be helpful prior to the unmounting of certain types of media with slow write speeds (such as some USB hard drives or PCMCIA storage media), but only because it delays the user from attempting to remove the media too soon, not because two syncs are better than one.

# The tune2fs Command

With tune2fs, you can adjust the tunable file system parameters on an ext2 or ext3 file system. A few performance-related items of note are as follows:

+   To disable file system checking, the -c 0 option sets the maximal mount count to zero.

+   The interval between forced checks can be adjusted with the -i option.

+   The -m option will set the reserved blocks percentage with a lower value, freeing more space at the expense of fsck having less space to write any recovered files.

+   Decrease the number of superblocks to save space with the -O sparse_super option. (Modern file systems use this by default.) Always run e2fsck after you change this value.

+   More space can be freed with the -r option that sets the number of reserved (for root) blocks.

Note that most of these uses of tune2fs free up space on the drive at the expense of the capability of fsck to recover data. Unless you really need the space and can deal with the consequences, just accept the defaults; large drives are now relatively inexpensive.