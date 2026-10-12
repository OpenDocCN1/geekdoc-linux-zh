# Part III: Administering Fedora

For our purposes, I want to focus on partitions that are used for the Linux file system. To see what partitions are currently set up on your hard disk, use the `fdisk` command as follows:

```
```
# fdisk -1
Disk /dev/hda: 40.0 GB, 40020644320
255 heads, 63 sectors/track, 4825 cylinders
Units = cylinders of 16065 * 512 bytes = 8225280 bytes

Device Boot Start End Blocks Id System
/dev/hda1 * 1 13 104 b Win95 FAT32
/dev/hda2 84 69 48195 83 Linux
/dev/hda3 90 522 3478072+ 83 Linux
/dev/hda4 523 554 257040 5 Extended
/dev/hda5 523 554 257008+ 82 Linux swap
```
```

This output shows the disk partitioning for a computer able to run both Linux and Microsoft Windows. You can see that the Linux partition on `/dev/hda3` has most of the space available for data. There is a Windows partition (`/dev/hda1`) and a Linux swap partition (`/dev/hda5`). There is also a small `/boot` partition (46MB) on `/dev/hda2`. In this case, the root partition for Linux has 3.3GB of disk space and resides on `/dev/hda3`.

Next, to see what partitions are actually being used for your Linux system, you can use the `mount` command (with no options). The `mount` command can show you which of the available disk partitions are actually mounted and where they are mounted.

```
```
# mount
/dev/hda3 on / type ext3 (rw)
/dev/hda2 on /boot type ext3 (rw)
/dev/hda1 on /mnt/win type vfat (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/dev/hdc on /media/cdrom type iso9660 (ro,nosuid,nodev)
```
```

> **NOTE:** You may notice that `/proc`, `/sys`, `/dev/pts`, `/proc/sys/fs/binfmt_misc`, `/dev/shm`, and other entities not relating to a partition are shown as file systems. This is because they represent different file system types (`proc` and `devpts`, and so on). The word `none`, however, indicates that they are not associated with a separate physical partition.

The mounted Linux partitions in this case are `/dev/hda2`, which provides space for the `/boot` directory (which contains data for booting Linux) and `/dev/hda3`, which provides space for the rest of the Linux file system beginning from the root directory (`/`). This particular system also contains a Windows partition that was mounted in the `/mnt/win` directory.