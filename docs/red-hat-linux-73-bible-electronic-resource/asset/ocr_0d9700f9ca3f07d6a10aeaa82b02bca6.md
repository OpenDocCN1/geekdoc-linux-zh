- **parted command** — A fairly new Red Hat Linux utility called parted can be used to resize NTFS file systems. Because it runs in Linux, you need to be able to run it from a boot disk if you currently have a Windows-only system. You can download a boot disk image from the following location and create a boot disk with that image using the boot-disk-creation descriptions in this chapter:

```
ftp://ftp.gnu.org/gnu/parted/bootdisk/partboot.img
```

Documentation of this utility is available from gnu.org at:
`www.gnu.org/software/parted/USER`. The USER file is also available on the partboot.img boot disk to refer to while you use the utility.

+   - **Partition Magic** — I’ve heard of good reports from people using Partition Magic (www.partitionmagic.com/partitionmagic) to resize NTFS partitions. Partition Magic also helps you create new partitions and manage them. The cost is currently $69.
+   
+   - **Acronis OS Selector** — This is another well-regarded product for managing, creating and resizing partitions. It supports a variety of file system types, including FAT12, FAT16, FAT32, NTFS, and Linux partition types (ext2, ext3 and Linux ReiserFS). The cost is currently $44.

As I mentioned earlier, if your Windows partition is FAT or VFAT you can continue with the procedure in the next session to resize your hard disk.

# Backing up and repartitioning

One way to divide a disk that is currently totally used for DOS (DOS, Windows 9x/2000, and so on) is not very complicated, but it can take some time. The method is to do a full system backup of your data, erase the whole disk, repartition the disk, restore your Windows 9x/2000 operating system to the hard disk (on a smaller partition), and add Red Hat Linux to the hard disk (using new partitions). Whew!

The problem with the backup/repartition approach is that it can be a pain. If your backup device is a 1.44MB floppy disk and your hard disk holds a gigabyte or more, a full backup is not a pleasant prospect. Alternatively, there is a DOS utility called FIPS.

# Using the FIPS utility

The FIPS utility came about to solve the problem of a would-be Linux user with a monolithic DOS/Windows hard disk. With FIPS, you can change the size of your DOS partition without erasing it. Though this process is risky, and nobody recommends it without major "buyer beware" warnings, many use it safely and save a lot of time and effort.

FIPS works by changing the values in the partition table and boot sector. Space is gained by changing the partition table that is used to create a new primary DOS partition. After that, the new DOS partition can be converted to a Linux partition.