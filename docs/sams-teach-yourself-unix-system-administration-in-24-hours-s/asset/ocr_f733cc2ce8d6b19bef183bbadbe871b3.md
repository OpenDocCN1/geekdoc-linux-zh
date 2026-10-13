Notice that the volume has a label now, and that the number of inodes has jumped up considerably, as desired.

A quick fsck demonstrates that all is as expected:

```
```
# fsck /dev/hdb
Parallelizing fsck version 1.23 (15-Aug-2001)
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
Little Guy: clean, 11/128000 files, 16094/255528 blocks
```
```

Most of the work of adding a new disk to the filesystem is done by the mke2fs (or one of its brethren), and there are a number of different options to the command.

# Mounting the New Disk

After the disk is formatted and has a filesystem skeleton added by newfs (or mkfs), it can be hooked into the filesystem. This is where Unix proves slightly different than other computer systems, because rather than add new drive images, Unix requires you to hook the new disk into the existing filesystem. That's why the mount output shows specific directories. Consider the following line from the mount output:

```
```
/dev/hda1 on /boot type ext3 (rw)
```
```

What this implies is that there's a /boot directory on the root (/) filesystem, and that its contents are hidden by the newly mounted /dev/hda1 drive.

This idea that newly mounted disks hide existing file content is critical to understand so you can best plan how to add your new disk space to your system.

# Task 10.3: Adding New Drives to Your System

Imagine that we can stop the system partway through the boot sequence, after things have started running, but before any nonboot disks are mounted. At this point, there'll be a /boot directory, but nothing in it. The job of the mount command is to attach filesystems to a specific directory.

+   1. Before the new drive hdb is added to the system, let's have a look at the directory /home/taylor:

```
```
/home/taylor:
# cd /home/
# ls -a taylor
.               .first_start_kde   .MOOP-random-seed
..              .gconf            .mcoprc
.autorun.lck    .gconfd           .nautilus
.bash_history   .gnome            .sawfish
```
```