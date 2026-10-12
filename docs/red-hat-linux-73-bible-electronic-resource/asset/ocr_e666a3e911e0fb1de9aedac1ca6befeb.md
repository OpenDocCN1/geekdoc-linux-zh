+   • A part of the Linux file system,
+   • Swap space for Linux, or
+   • Other file system types (perhaps containing other bootable operating systems.)

For our purposes, I want to focus on partitions that are used for the Linux file system. To see what partitions are currently set up on your hard disk, you can use the fdisk command as follows:

```
# fdisk -1
Disk /dev/hda: 255 heads, 63 sectors, 554 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Start End Id System
/dev/hda1 * 1 83 666666 b Win95 FAT32
/dev/hda2 84 89 48195 83 Linux
/dev/hda3 90 522 3478072+ 83 Linux
/dev/hda4 523 554 257040 5 Extended
/dev/hda5 523 554 257008+ 82 Linux swap
```

This output shows the disk partitioning for a computer running both Red Hat Linux and Microsoft Windows. You can see that the Linux partition on /dev/hda3 has most of the space available for data. There is a Windows partition (/dev/hda1) and a Linux swap partition (/dev/hda5). There is also a small /boot partition (46MB) on /dev/hda2. In this case, the root partition for Linux has 3.3GB of disk space and resides on /dev/hda3.

Next, to see what partitions are actually being used for your Linux system, you can use the mount command (with no options). The mount command can show you which of the available disk partitions are actually mounted and where they are mounted.

```
# mount
/dev/hda3 on / type ext3 (rw)
/dev/hda2 on /boot type ext3 (rw)
/dev/hda1 on /mnt/win type vfat (rw)
none on /proc type proc (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/cdrom on /mnt/cdrom type iso9660 (ro,nosuid,nodev)
```

> NOTE: You may notice that /proc, /dev/pts, and other entries not relating to a partition are shown as file systems. This is because they represent different file system types (proc and devpts, respectively). The word “none,” however, indicates that they are not associated with a separate partition.

The mounted Linux partitions in this case are /dev/hda2, which provides space for the /boot directory (which contains data for booting Linux), and /dev/hda3, which provides space for the rest of the Linux file system beginning from the root directory (/). This particular system also contains a Windows partition that was mounted in the /mnt/win