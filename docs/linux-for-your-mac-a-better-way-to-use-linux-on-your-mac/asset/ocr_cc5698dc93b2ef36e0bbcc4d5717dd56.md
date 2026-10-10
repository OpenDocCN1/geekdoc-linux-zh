| Table 16.3 | Linux Disk Tools |
|---|---|
| **Name** | **Description** |
| badblocks | Search an IDE or other device for bad blocks |
| cksum | Create checksum based on byte count of file |
| df | Display free space on designated device or all devices |
| dosfsck | Check and repair DOS filesystems |
| dump | Archive an entire ext2 filesystem |
| e2fsck | Check and fix an ext2 filesystem |
| fdisk | Create and create a drive's partitions |
| hdparm | Set and configure IDE drive parameters |
| mkswap | Set up a Linux swap area |
| pdisk | Edit Apple partition table editor |
| scsi_info | Display info about specified SCSI device |
| sum | Create checksum based on block count of file |
| swapon | Mount swap file and start process |

# Using fsck

One of the first utilities you may run into when using PowerPC Linux (especially distributions with current 2.2-series Linux kernels) is the fsck command (more properly termed e2fsck). This command is used to check and repair ext2 filesystems on designated partitions.

Although designed for speed, e2fsck can still take quite a bit of time to check today's large hard drives, especially when you have partitions that are 5, 10, or 20GB (the limitation in 2.2-series Intel-based kernels is 27GB for an individual partition and 8 terabytes for the filesystem).

When e2fsck is run, it performs five passes over the specified filesystem, which is unmounted. The passes check file block locations, directories, links, the integrity of the filesystem (directory structure), and summary information about the partition. For example, to check a spare partition while running Linux, you can use e2fsck with its -t or force check option (as root), along with the partition's device name, like this:

```
```
# e2
Filesystem 1k-blocks Used Available Use% Mounted on
```
```