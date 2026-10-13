# ## Step 9

Write out new partition table information to the hard drive as follows:

```
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

After the new partition table is written to disk, reboot your system to ensure that the partition table is updated. The newly created partitions are now ready for a Linux filesystem.

> **Note**
> 
> You can examine the existing partition of any drive by running fdisk with the option -l. For example, `fdisk -l /dev/hda` displays the existing partitions on the first IDE drive on the primary controller. You can display the partitions for all hard drives by just supplying the `-l` option without specifying any particular hard drive.

# # Linux Filesystems

Even though the newly added drive is now recognized by the operating system, it’s not usable until it is partitioned and a filesystem is created on it. The default filesystem for Linux is the extended type-2 filesystem (ext2). Characteristics of an ext2 filesystem are listed in Table 9.3.

**Table 9.3. Second Extended (ext2) Filesystem Characteristics**

| Characteristic | Limit |
|---|---|
| Maximum filesystem size | 4 terabytes |
| Maximum file size | 2 gigabytes |
| Maximum filename length | 255 characters |
| Minimum block size | 1,024 bytes |
| Default inode allocation | 1 per 4,096 bytes of partition space |

The filesystem structure is built when the *make filesystem* utility (mkfs) is run. This utility is actually just a front-end program that calls subordinate routines for filesystem creation. When making an ext2 filesystem, the mkfs utility actually calls mke2fs to create the correct filesystem structure. After the filesystem structure is created, it cannot be modified without reformatting the partition, or—in other words—remaking a new filesystem with the mkfs utility.

> **Caution**
> 
> The mkfs utility completely erases all data. You are not prompted to continue. It runs without any user intervention. Use it with caution.