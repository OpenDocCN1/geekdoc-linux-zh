# HP-UX logical volume management

will “see” the additional 10GB of allocated space, but since the filesystem contains only 100GB in size, the snapshot will still be usable.

We can resize the filesize with resize2fs. (The 2 comes from the original ext2 filesystem, the command supports all versions of ext.) Since resize2fs can determine the size of the new filesystem from the volume, we do not need to specify the new size explicitly. We would have to do so when shrinking the filesystem.

```
$ sudo resize2fs /dev/DEMO/web1
resize2fs 1.41.9 (22-Aug-2009)
Please run ‘efsck -f /dev/DEMO/web1’ first.
```

Oops! resize2fs forces you to double-check the consistency of the filesystem resizing.

```
$ sudo efsck -f /dev/DEMO/web1
efsck 1.41.9 (22-Aug-2009)
Pass 1: Checking inodes, blocks, and sizes
```

/dev/DEMO/web1: 6432/6553600 blocks (0.1% non-contiguous), 473045/2621400 blocks

```
$ sudo resize2fs /dev/DEMO/web1
resize2fs 1.41.9 (22-Aug-2009)
Resizing the filesystem of /dev/DEMO/web1 (4k) blocks.
The filesystem on /dev/DEMO/web1 is now 28835840 blocks long.
```

That’s it! Examining the output of df which shows the changes:

```
$ sudo mount /dev/DEMO/web1 /mnt/web1
$ df -h /mnt/web1
```

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| /dev/mapper/DEMO-web | 109G | 188M | 103G | 1% | /mnt/web1 |

# HP-UX logical volume management

![](bbox=[0.175, 0.648, 0.235, 0.685])

As of HP-UX 10.2, HP provides a full logical volume manager. especially when you consider that HP-UX formerly did not support the notion of disk partitions. The volume manager is LVM, just as on Linux, although the HP-UX version is in the original. (Really, it Veritas…)

As a simple example of LVM wrangling, here’s how you would configure 75GB hard disk for use with the logical volume manager. If you have read through the Linux example, the following procedure will seem familiar. There are a few differences, but the overall process is essentially the same.

The pvcreate identifies physical volumes.

If you will be using the disk as a block disk, the -B option to pvcreate to reserve space for a block disk, run mkboot to install it.