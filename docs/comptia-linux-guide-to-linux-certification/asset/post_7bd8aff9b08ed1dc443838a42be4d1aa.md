
```
[root@server1 ~]# df
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/sda1 30237648 7227280 21474368 26% /
devtmpfs 422820 80 422760 1% /dev
tmpfs 480640 272 480368 1% /dev/shm
/dev/mapper/vg00-data 15481840 169456 14525952 2% /data
/dev/mapper/vg00-extras 16513960 176108 15498992 2% /extras
[root@server1 ~]#
```

If a filesystem is approaching full capacity, it might be useful to examine which directories on that filesystem are taking up the most disk space such that you can remove or move files from that directory to another filesystem that has sufficient space. To view the size of a directory and its contents in kilobytes, you can use the `du (directory usage)` command. If the directory is large, you should use either the `more` or `less` command to view the output page-by-page, as shown with the following `/usr` directory:

```
[root@server1 ~]# du /usr | more
56048 /usr/sbin
4 /usr/include/telepathy-1.0
48 /usr/include/python3.3m
40 /usr/include/python2.7
156 /usr/include
8 /usr/libexec/gedit
24 /usr/libexec/spice-gtk-x86_64
20 /usr/libexec/awk
2720 /usr/libexec/ipsec
28 /usr/libexec/pymouth
32 /usr/libexec/shotwell
8 /usr/libexec/totem
12 /usr/libexec/gstreamer-1.0
16 /usr/libexec/utempter
8 /usr/libexec/paccct
12 /usr/libexec/coreutils
1592 /usr/libexec/sssd
20 /usr/libexec/file-roller
36 /usr/libexec/man-db
12 /usr/libexec/gstreamer-0.10
432 /usr/libexec/sudo
1168 /usr/libexec/bluetooth
528 /usr/libexec/cpnnssh
--More--
```

To view only a summary of the total size of a directory, simply use the `-s` switch to the `du` command, as shown in the following example with the `/usr` directory:

```
[root@server1 ~]# du -s /usr
5719324 /usr
[root@server1 ~]# _
```

As with the df command, the du command also accepts the `-h` option to make the view more human readable; the following indicates that the total size of the /usr directory is 5.5GB:

```
[root@server1 ~]# du -hs /usr
5.5G   /usr
[root@server1 ~]# _
```

Recall that every filesystem has an inode table that contains the inodes for the files and directories on the filesystem; this inode table is made during filesystem creation and is usually proportionate to the size of the filesystem. Each file and directory uses one inode; thus, a filesystem with several small files might use up all of the inodes in the inode table and prevent new files from being created on the filesystem. To view the total number of inodes and free inodes for an ext2, ext3, or ext4 filesystem, you can use the dumpe2fs command with the `-h` switch, as shown in the following output:

```
[root@server1 ~]# df
Filesystem     1K-blocks     Used Available Use% Mounted on
/dev/sda1      30237648 7227280  21474368  26% /
devtmpfs        422820      80    422760   1% /dev
tmpfs            480640    272    480368   1% /dev/shm
/dev/mapper/vg00-data  15481840 169456 14525952  2% /data
/dev/mapper/vg00-extra  16513960 176108 15498992  2% /extras
[root@server1 ~]# dumpe2fs -h /dev/sda1
dumpe2fs 1.42.8 (20-Jun-2013)
Filesystem volume name:   <none>
Last mounted on:           /
Filesystem UUID:           db545f1d-c1ee-4b70-acbe-3dc61b41db20
Filesystem magic number:   0xEF53
Filesystem revision#:      1 (dynamic)
Filesystem features:       has_journal ext_attr resize_inode dir_index filetype needs_recovery extent flex_bg sparse_super large_file huge_file uninit_bg dir_inlink extra_isize
Filesystem flags:         signed_directory_hash
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              1921360
Block count:              7680000
Reserved block count:     384000
Free blocks:              5752659
Free inodes:              1663809
First block:              0
Block size:               4096
Fragment size:            4096
Reserved GDT blocks:      1022
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8176
Inode blocks per group:  511
Flex block group size:    16
Filesystem created:       Mon Aug 2 09:27:13 2015
Last mount time:          Thu Aug 12 10:55:03 2015
Last write time:          Mon Aug 2 10:24:23 2015
Mount count:              20
Maximum mount count:      -1
Last checked:             Mon Aug 2 09:27:13 2015
Check interval:           0 (<none>)
Lifetime writes:          13 GB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:               256
Required extra isize:     28
Desired extra isize:     28
Journal inode:            8
First orphan inode:       1705241
Default directory hash:   half_md4
Directory Hash Seed:     cab24941-82b1-43a5-83ff-18a93adbfd94
Journal backup:          inode blocks
Journal features:        journal_incompat_revoke
Journal size:             128M
Journal length:           32768
Journal sequence:         0x000031fe
Journal start:            1
[root@server1 ~]# _
```

In the preceding output, you can see that there are 1921360 inodes in the inode table and that 1663809 of them are free to use when creating new files and directories.

## Checking Filesystems for Errors

Filesystems themselves can accumulate errors over time. These errors are often referred to as **filesystem corruption** and are common on most filesystems. Those filesystems that are accessed frequently are more prone to corruption than those that are not. As a result, such filesystems should be checked regularly for errors.

The most common filesystem corruption occurs because a system was not shut down properly using the shutdown, poweroff, halt, or reboot commands. Data is stored in memory for a short period of time before it is written to a file on the hard disk. This process of saving data to the hard disk is called *syncing*. If the computer’s power is turned off, data in memory might not be synced properly to the hard disk and corruption might occur.

Filesystem corruption can also occur if the hard disks are used frequently for time-intensive tasks such as database access. As the usage of any system increases, so does the possibility for operating system errors when writing to the hard disks. Along the same lines, the physical hard disks themselves are mechanical in nature and can wear during time. Some areas of the hard disk platter might become unusable if they cannot hold a magnetic charge; these areas are known as *bad blocks*. When the operating system finds a bad block, it puts a reference to that bad block in the bad blocks table on the file system. Any entries in the bad blocks table are not used for future disk storage.

To check a file system for errors, you can use the **fsck** (file system check) command, which can check file systems of many different types. The `fsck` command takes an option specifying the file system type and an argument specifying the device to check; if the file system type is not specified, the file system is automatically detected. It is also important to note that the file system being checked must be unmounted beforehand for the `fsck` command to work properly, as shown next:

```
[root@server1 ~]# fsck /dev/vg00/data
fsck from util-linux 2.24
e2fsck 1.42.8 (20-Jun-2013)
/dev/mapper/vg00-data is mounted.
e2fsck: Cannot continue, aborting.
[root@server1 ~]# umount /dev/vg00/data
[root@server1 ~]# fsck /dev/vg00/data
fsck from util-linux 2.24
e2fsck 1.42.8 (20-Jun-2013)
/dev/mapper/vg00-data: clean, 11/983040 files, 104064/3932160 blocks
[root@server1 ~]#
```

![](img/c27875544958897d817484d558c208c8_261_0.png)

> Because the / file system cannot be unmounted, you should only run the `fsck` command on the / file system from single-user mode (discussed in Chapter 8) or from live installation media (discussed in Chapter 6).

Notice from the preceding output that the `fsck` command does not give lengthy output on the terminal screen when checking the file system; this is because the `fsck` command only performs a quick check for errors unless the -f option is used to perform a full check, as shown in the following example:

```
[root@server1 ~]# fsck -f /dev/vg00/data
fsck from util-linux 2.24
e2fsck 1.42.8 (20-Jun-2013)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/mapper/vg00-data: 11/983040 files (0.0% non-contiguous),
104064/3932160 blocks
[root@server1 ~]#
```

Table 5-6 displays a list of common options used with the `fsck` command.

If the `fsck` command finds a corrupted file, it displays a message to the user asking whether to fix the error; to avoid these messages, you may use the -a or -y options listed in Table 5-6 to specify that the `fsck` command should automatically repair any corruption. If there are files that the `fsck` command cannot repair, it places them in the lost+found directory on that file system and renames the file to the inode number.
