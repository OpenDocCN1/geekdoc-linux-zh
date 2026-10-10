
computer. In the following output, you see that /dev/fd0 and /dev/fd1 share the same major number of 2, yet the minor number for /dev/fd0 is 0 and the minor number for /dev/fd1 is 1, which differentiates them from each other.

```
[root@server1 ~]# ls -1/dev/fd0 /dev/fd1
brw-rw---- 1 root floppy 2, 0 Feb 23 16:02 /dev/fd0
brw-rw---- 1 root floppy 2, 1 Feb 23 16:02 /dev/fd1
[root@server1 ~]#
```

Together, the device file type (block or character), the major number (device driver), and the minor number (specific device) make up the unique characteristics of each device file. To create a device file, you simply need to know these three pieces of information.

If a device file becomes corrupted, it is usually listed as a regular file instead of a block or character special file. Recall from Chapter 4 that the `find /dev -type f` command can be used to search for regular files underneath the /dev directory to identify whether corruption has taken place. If you find a corrupted device file or accidentally delete a device file, the `mknod` command can be used to re-create the device file if you know the type, major, and minor numbers. An example of re-creating the /dev/fd0 block device file used earlier with a major number of 2 and a minor number of 0 is shown in the following example:

```
[root@server1 ~]# ls -1/dev/fd0
brw-rw---- 1 root floppy 2, 0 Feb 23 16:02 /dev/fd0
[root@server1 ~]# rm -f /dev/fd0
[root@server1 ~]# ls -1/dev/fd0
[root@server1 ~]# mknod /dev/fd0 b 2 0
[root@server1 ~]# ls -1/dev/fd0
brw-r-r-- 1 root root 2, 0 May 8 13:26 /dev/fd0
[root@server1 ~]#
```

To see a list of devices that are currently used on the system and their major numbers, you can view the contents of the /proc/devices file, as shown here:

```
[root@server1 ~]# cat /proc/devices
Character devices:
1 mem
4 /dev/vc/0
4 tty
4 ttyS
5 /dev/tty
5 /dev/console
5 /dev/ptmx
7 vcs
10 misc
13 input
14 sound
21 sg
29 fb
116 alsa
128 ptp
136 pts
162 raw
180 usb
189 usb_device
202 cpu/msr
203 cpu/cpuid
226 drm
250 hidraw
251 usbmon
252 bsg
253 pcmcia
254 rtc

Block devices:
1 ramdisk
2 fd
7 loop
8 sd
9 md
11 sr
65 sd
69 sd
70 sd
71 sd
128 sd
134 sd
135 sd
253 device-mapper
254 mdp
[root@server1 ~]#
```

## Filesystems

Recall from Chapter 2 that files must be stored on the hard disk in a defined format called a **filesystem** so that the operating system can work with them. The type of filesystem used determines how files are managed on the physical hard disk. Each filesystem can have different methods for storing files and features that make the filesystem robust against errors. Although many different types of filesystems are available, all filesystems share three common components, as discussed in Chapter 4: the superblock, the inode table, and the data blocks. On a structural level, these three components work together to organize files and allow rapid access to and retrieval of data. All storage media, such as floppy disks, hard disks, and DVDs, need to contain a filesystem before they can be used.

![](img/c27875544958897d817484d558c208c8_220_0.png)

Creating a filesystem on a device is commonly referred to as **formatting**.

## Filesystem Types

As mentioned, many filesystems are available for use in the Linux operating system. Each has its own strengths and weaknesses, thus some are better suited to some tasks and not as well suited to others. One benefit of Linux is that you need not use only one type of filesystem on the system; you can use several different devices formatted with different filesystems under the same directory tree. In addition, files and directories appear the same throughout the directory tree regardless of whether there is one filesystem or 20 different filesystems in use by the Linux system. Table 5-2 lists some common filesystems available for use in Linux. For a full listing of filesystem types and their features, you can refer to the Filesystem HOWTO at www.lfd.org/HOWTO/Filesystems-HOWTO.html.

![](img/c27875544958897d817484d558c208c8_221_0.png)

Filesystem support is typically built into the Linux kernel or added as a package on most distributions. Fedora 20 has native support for btrfs, cramfs, ext2, ext3, ext4, hfs, hfsplus, iso9660, ntfs, reiserfs, vfat, and xfs by default.

## Mounting

The term **mounting** originated in the 1960s when information was stored on large tape reels that had to be mounted on computers to make the data available. Today, mounting still refers to making data available. More specifically, it refers to the process whereby a device is made accessible to users via the logical directory tree. This device is attached to a certain directory on the directory tree called a **mount point**. Users can then create files and subdirectories in this mount point directory, which are then stored on the filesystem that was mounted to that particular directory.

Remember that directories are merely files that do not contain data; instead, they contain a list of files and subdirectories organized within them. Thus, it is easy for the Linux system to cover up directories to prevent user access to that data. This is essentially what happens when a device is mounted to a certain directory; the mount point directory is temporarily covered up by that device while the device remains mounted. Any file contents that were present in the mount point directory prior to mounting are not lost; when the device is unmounted, the mount point directory is uncovered, and the previous file contents are revealed. Suppose, for example, that you mount a floppy disk device that contains a filesystem to the /mnt directory. The /mnt directory is an empty directory that is commonly used as a temporary mount point for mounting removable media devices. Before mounting, the directory structure would resemble that depicted in Figure 5-1. After the floppy is mounted to the /mnt directory, the contents of the /mnt directory would be covered up by the floppy filesystem, as illustrated in Figure 5-2.

If a user then stores a file in the /mnt directory, as shown in Figure 5-2, that file will be stored on the floppy disk device. Similarly, if a user creates a subdirectory under the /mnt directory depicted in Figure 5-2, that subdirectory will be made on the floppy disk.

It is important to note that any existing directory can be used as a mount point. If a user mounts a floppy device to the /bin directory, all files in the /bin directory are covered up during the time the floppy disk is mounted, including the command used to unmount the floppy. Thus, it is safe practice to create empty directories used specifically for mounting devices to avoid making existing files inaccessible to users.

| Filesystem | Description |
|---|---|
| bfs | Boot File System—A small, bootable filesystem used to hold the files necessary for system startup; it is commonly used on UNIX systems. |
| btrfs | B-tree File System—A new filesystem for Linux systems that includes many features that are geared towards large-scale storage. Although still in development, it is envisioned to be a replacement for the ext4 and reiserfs filesystems in the long term. Its name is commonly pronounced as “Butter FS.” |
| cramfs | Compressed ROM Filesystem—A read-only filesystem typically used on embedded Linux systems to host system files in a small amount of storage space. |
| ext2 | Second extended filesystem—The traditional filesystem used on Linux, it supports access control lists (individual user permissions). In addition, it retains its name from being the new version of the original extended filesystem, based on the Minix filesystem. |
| ext3 | Third extended filesystem—A variation on ext2 that allows for journaling and, thus, has a faster startup and recovery time. |
| ext4 | Fourth extended filesystem—A variation on ext3 that has larger filesystem support and speed enhancements. |
| hfs, hfsplus | Hierarchical File System—A filesystem native to Apple Macintosh computers. |
| hpfs | High Performance File System—An IBM proprietary OS/2 filesystem that provides long filename support and is optimized to manipulate data on large disk volumes. |
| iso9660 | ISO 9660 filesystem—A filesystem that originated from the International Standards Organization Recommendation 9660 and is used to access data stored on CDs and DVDs. |
| minix | MINIX filesystem—The filesystem used by Linus Torvalds in the early days of Linux development. |
| msdos | DOS FAT filesystem. |
| ntfs | New Technology File System—A Microsoft proprietary filesystem developed for its Windows operating systems. |
| reiserfs | Reiser File System—A journalizing filesystem similar to ext3, and more suited for use with databases. |
| udf | Universal Disk Format filesystem—A filesystem used by software programs that write to a CD-RW or DVD-RW drive. |
| vfat | DOS FAT filesystem with long filename support. |
| vxfs | Veritas File System—A journalizing filesystem that offers large file support and supports access control lists (individual user permissions) and is commonly used by major versions of UNIX. |
| xfs | X File System—A high-performance filesystem created by Silicon Graphics for use on their IRIX UNIX systems. Many Linux administrators prefer to use xfs on systems that need to quickly write large numbers of files to the hard disk. |
| zfs | Zettabyte File System—A very high-performance filesystem and volume manager originally created by Sun Microsystems that protects against data corruption and has features that support very large distributed storage systems. Many large-scale Linux server systems in industry use the zfs filesystem to store and manage large amounts of data. You will learn how to configure zfs in Chapter 6. |

Table 5-2 Common Linux filesystems
