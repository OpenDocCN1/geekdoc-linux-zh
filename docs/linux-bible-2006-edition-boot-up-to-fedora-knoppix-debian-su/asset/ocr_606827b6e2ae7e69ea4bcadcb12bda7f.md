# 166 Part II Running the Show

Filesystem too small for a journal
Writing superblocks and filesystem accounting information:
done

The filesystem will be automatically checked every 32 mounts
or180 days, whichever comes first. Use tune2fs -c -i to
override.

You can see the statistics that are output with the formatting done by mkfs
command. The number of inodes and blocks are created, as are the number
of blocks and fragments per format. You could now make this file system
(mount /mnt/floppy), change to it your current directory (cd /mnt/floppy),
and create files on it as you please.

# Adding a Hard Disk

Adding new hard disk to your computer so that it can be used by Linux requires
combination of steps described in previous sections. Here's the general procedure:

+   1. Install the new hard hardware.
2. Identify the partitions on the new disk.
3. Create the file systems on the new disk.
4. Mount the file systems.

The easiest way to add a hard disk to Linux is to have the entire disk devoted to a
single Linux partition. You can have multiple partitions, however, and assign them
to different types of file systems and different mount points, if you like. The\following process takes you adding a hard disk containing a single Linux
partition. Along the way, it also notes which steps you need to repeat to have multiple
file systems with multiple mount points.

![](bbox=[0.128, 0.676, 0.193, 0.715])

This procedure assumes that Linux is already installed and working on the com-\puter. If it is not the case, follow the instructions for adding a hard disk on your
current operating system. Later, when you install Linux, you can identify this disk
when you are asked to partition your hard disk(s).

+   1. Follow the manufacturer's instructions for physically installing and connect-
ing new hard disk in your computer. If, presumably, this is a second hard
disk, you may need to change jumpers on the hard unit itself to have it
operate as a slave hard disk (if it's on the same cable as your first hard disk).
You may also need to change the BIOS settings.

+   2. Boot your computer to Linux.
3. Determine the device name for the hard disk. As root user from a shell, type:

```
# dmesg | less
```