# Task 10.2: Making a Filesystem with mke2fs

A filesystem is created on the hard disk with mkfs, and because different filesystems are so different in their underlying characteristics, most modern Unix systems have specific versions of mkfs for each supported filesystem.

+   1. Linux includes a number of applications for building a new filesystem on a disk:

```
# man -k mkfs
mkdosfs [mkfs] (8) - create an MS-DOS file system under Linux
mkfs (8) - build a Linux file system
mkfs.bfs [mkfs] (8) - make an SCO bfs filesystem
mkfs.minix [mkfs] (8) - make a Linux MINIX filesystem
# man -k mke2fs
mke2fs (8) - create a Linux second extended file system
```

> Notice that mke2fs didn't match the man -k mkfs. A classic example of why you have to dig around a bit when you're searching for specific commands in Unix. Someday that'll be fixed, but for now...

By contrast, Mac OS X Darwin offers nothing that even matches mkfs, but if you try the variation newfs you find:

```
$ man -k newfs
newfs(8), mount_mfs(8) - construct a new file system
newfs_msdos(8) - construct a new MS-DOS (FAT) file system
```

Notice that you can create Windows-format hard disk images from within the Macintosh environment, even on the command line.

> Solaris spans the gap, offering both newfs and mkfs, and they're completely different commands. You'll want to check the man page and the AnswerBook material (Sun's great online documentation suite at http://docs.sun.com) to find out the specifics of your own version of Solaris.

+   2. Building a "second extended" filesystem requires the mke2fs command:

```
# mke2fs /dev/hdb
mke2fs 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
/dev/hdb is entire device, not just one partition!
Proceed anyway? (y,n) y
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
```