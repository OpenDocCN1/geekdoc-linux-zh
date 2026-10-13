versions offer a "serialize" flag that forces the program to check disks one at a time rather than all at once. On Linux, for example, the -s flag does just that.

# Workshop

# Quiz

+   1. What’s the most common Linux filesystem? Mac OS filesystem? Commercial Unix filesystem?
+   2. Superstition or not, most Unix sysadmins do what after they run fsck and find errors?
+   3. On a filesystem with 512-byte blocks, what’s the minimum actual disk space used by a file that’s 1025 bytes in size?
+   4. The Unix equivalent of the PC “File Allocation Table” (that’s what “FAT” stands for on those FAT* filesystems) is called?
+   5. When the fsck program doesn’t think that a check is required of the filesystem, it refers to that disk as being in what state?
+   6. Though it’s called single-user mode, can you really use a computer in that state?

# Answers

+   1. The most common Linux filesystem is ext2 with ext3 continuing to grow in popularity; on the Mac it’s HFS+ (Hierarchical File System Plus), and on commercial Unix systems it’s the FFS (Berkeley Fast File System).
+   2. Run fsck again.
+   3. If the file is 1025 bytes in size and it gets stored in 512-byte blocks, the minimum size possible is three 512-byte blocks, or 1536 bytes.
+   4. The superblock.
+   5. Disks that don’t need checking are “clean.”
+   6. No. On almost all Unix systems, networking, a windowing environment, and other necessities of modern Unix interaction, aren’t started yet. It’s an unfortunate name because it’s really administrative mode.

In the next hour, we’ll format and mount a new disk on the system, exploring partition tables, fdisk, newfs and other helpful tools.