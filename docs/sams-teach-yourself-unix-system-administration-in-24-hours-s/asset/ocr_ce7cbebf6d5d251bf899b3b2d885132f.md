```
Disk /dev/sda: 255 heads, 63 sectors, 522 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Start End Blocks Id System
/dev/sda1 * 1 6 48163+ 83 Linux
/dev/sda2 7 490 3887730 83 Linux
/dev/sda3 491 522 257040 82 Linux swap
```

To add an additional operating system, we would need to have a configuration that included additional partitions—they're all in use already in the above output, as you can see by comparing the disk statistics with the start and end values of the specific devices.

Given that we've consumed the entire disk with this set of partitions, the bad news is that we need to repartition the disk, destroying the /dev/sda2 partition, then reinstall Linux. Or we need to buy, format, and install a new disk.

2. The resultant partition table for a reorganized disk might look like this:

```
Disk /dev/sda: 255 heads, 63 sectors, 522 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Start End Blocks Id System
/dev/sda1 * 1 6 48163+ 83 Linux
/dev/sda2 7 245 1943865 83 Linux
/dev/sda3 246 490 1943865 b Win95 FAT32
/dev/sda4 491 522 257040 82 Linux swap
```

There are other ways to partition your disk too, and many Linux experts recommend that you start with Windows, using the Windows installer to partition the disk into the four partitions needed.

If you're going to dual-boot, it's wise to read this section before you begin any installation on your disk. You could also opt for another solution that's less destructive, such as VMware, covered later in this hour.

# Dual-Boot Configurations with LILO

When you have more than one operating system installed on your system, you can select your favorite at boot-time by using either LILO or GRUB. LILO is the Linux Loader, and it's surprisingly straightforward to configure.