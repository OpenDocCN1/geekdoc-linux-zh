# fsck

Checks and repairs a filesystem

fsck [options] [filesystem-list]

The fsck verifies the integrity of a filesystem and reports on problems it finds. This utility is a front end for filesystem checkers specific to a filesystem type (each checker is named fsck.type), where type is the filesystem type.

# Arguments

The filesystem-list is required unless the -A option, in which case fsck checks all the filesystems listed in the /etc/fstab file.
On the command line there are two ways to list the filesystems you want fsck to check. use the name of the device that holds the filesystem (for example, /dev/hda2) or, if the filesystem appears in /etc/fstab, specify the mount point (for example, /usr2) for the filesystem.

# Options

Without the -A option fsck checks the filesystems in the filesystem-list. When a filesystem is consistent, you may see a report such as the following:

```
# /sbin/fsck -f /dev/hda8
sck 1.27 (8-Mar-2002)
efsck 1.27 (8-Mar-2002)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/hda8: 26/128768 files (7.7% non-contiguous) blocks
```

If fsck finds problems with a filesystem, it reports on each problem, allowing you to choose whether to repair it or ignore it.
When you run fsck, you specify both fsck options and options specific to the filesystem type that fsck is checking (for example, ext2, ext3, mdos, reiserfs). The fsck options precede the type-specific options.

+   5. The fsck utility does not check these entries in fstab that have a zero in the fifth (next-to-last) column.