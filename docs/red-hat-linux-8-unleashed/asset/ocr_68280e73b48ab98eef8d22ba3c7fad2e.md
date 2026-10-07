# CHAPTER 10 Managing the Filesystem

> NOTE
If you are preparing to create a filesystem on any device other than a floppy disk, examine it with fdisk or any other utility of your choice and modify the partition table accordingly (following the instructions you were in the preceding sections of this chapter).

Zip disks are typically delivered with a single partition numbered 4. This has some arcane relevance to Apple computer users, but is of no importance to Linux users who are free to use any valid number you choose.

To create the filesystem structure, you need to do what is referred to as a high-level format. For FAT systems, this is accomplished by the format command. In Linux, you use the mke3fs command to create an ext3 filesystem.

> NOTE
If you are creating a Reiter filesystem, use the miserfs command. To create a DOS filesystem, use the mkdosfs command. Other commands for other filesystems include

+   * mkfs.bfs—The SCO filesystem
* mkfs.ext2—The ext2 filesystem
* mkfs.minix—The minix filesystem
* mkfs.msdos—The MS-DOS filesystem
* mkfs.vfat—The FAT32 filesystem

The special tools used to manipulate the FAT and MS-DOS filesystems are known as the Mtools and are covered in Chapter 27, "Using Emulators and Other Cross-Platform Tools in Red Linux," along with their counterparts for the Macintosh HFS filesystem.

# Using mke2fs to Create the Filesystem

The mke2fs command is used to create both the ext2 and ext3 filesystems. At its simplest, the command is used as

```
# mke2fs device
```

Here are some of the most useful options for mke2fs:

+   -c—This option checks for bad blocks during filesystem creation.
-N—This option overrides the default number of inodes created. (The default number is usually a good choice, but you might need to use this option to allow additional disk space.)
-m—This option frees up some space on the disk, but you do so at your peril. By default, the system allocates 5% of the blocks to the superuser—to be used in file recovery during fsck. You can lower that allocation, but you might not leave enough blocks for fsck to recover enough files.