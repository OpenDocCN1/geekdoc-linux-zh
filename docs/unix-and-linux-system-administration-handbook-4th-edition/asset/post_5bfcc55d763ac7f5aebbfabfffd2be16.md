
## Resizing filesystems

Filesystem overflows are more common than disk crashes, and one advantage of logical volumes is that they're much easier to juggle and resize than are hard partitions. We have experienced everything from servers used for personal MP3 storage to a department full of email pack rats.

The logical volume manager doesn't know anything about the contents of its volumes, so you must do your resizing at both the volume and filesystem levels. The order depends on the specific operation. Reductions must be filesystem-first, and enlargements must be volume-first. Don't memorize these rules; just think about what's actually happening and use common sense.

Suppose that in our example, /mnt/web1 has grown more than we predicted and needs another 10GB of space. We first check the volume group to be sure additional space is available.

```
$ sudo vgdisplay DEMO
--- Volume group ---
VG Name              DEMO
System ID
Format                lvm2
Metadata Areas        1
Metadata Sequence No  18
VG Access             read/write
VG Status             resizable
MAX LV                0
Cur LV                2
Open LV               1
Max PV                0
Cur PV                1
Act PV                1
VG Size               975.99 GB
PE Size               4.00 MB
Total PE              249854
Alloc PE / Size       51200 / 200.00 GB
Free PE / Size        198654 / 775.99 GB
VG UUID               NtBRLu-RqIQ-3Urt-iQZn-vEvJ-u0Th-FVYKWF
```

Plenty of space is available, so we unmount the filesystem and use lvresize to add space to the logical volume.

```
$ sudo umount /mnt/web1
$ sudo lvchange -an DEMO/web1
$ sudo lvresize -L +10G DEMO/web1
$ sudo lvchange -ay DEMO/web1
Extending logical volume web1 to 110.00 GB
Logical volume web1 successfully resized
```

The lvchange commands are needed to deactivate the volume for resizing and to reactivate it afterwards. This part is only needed because there is an existing snapshot of web1 from our previous example. After the resize operation, the snapshot will “see” the additional 10GB of allocated space, but since the filesystem it contains is only 100GB in size, the snapshot will still be usable.

We can now resize the filesystem with resize2fs. (The 2 comes from the original ext2 filesystem, but the command supports all versions of ext.) Since resize2fs can determine the size of the new filesystem from the volume, we don’t need to specify the new size explicitly. We would have to do so when shrinking the filesystem.

```
$ sudo resize2fs /dev/DEMO/web1
resize2fs 1.41.9 (22-Aug-2009)
Please run 'e2fsck -f /dev/DEMO/web1' first.
```

Oops! resize2fs forces you to double-check the consistency of the filesystem before resizing.

```
$ sudo e2fsck -f /dev/DEMO/web1
e2fsck 1.41.9 (22-Aug-2009)
Pass 1: Checking inodes, blocks, and sizes
...
/dev/DEMO/web1: 6432/6553600 files (0.1% non-contiguous), 473045/26214400 blocks
```

```
$ sudo resize2fs /dev/DEMO/web1
resize2fs 1.41.9 (22-Aug-2009)
Resizing the filesystem on /dev/DEMO/web1 to 28835840 (4k) blocks.
The filesystem on /dev/DEMO/web1 is now 28835840 blocks long.
```

That’s it! Examining the output of df again shows the changes:

```
$ sudo mount /dev/DEMO/web1 /mnt/web1
$ df -h /mnt/web1
Filesystem     Size  Used Avail Use% Mounted on
/dev/mapper/DEMO-web1 110G 188M 103G 1% /mnt/web1
```

## HP-UX logical volume management

![](img/14d78e3cecac4581d37024baf1e94cca_299_0.png)

As of HP-UX 10.20, HP provides a full logical volume manager. It’s a nice addition, especially when you consider that HP-UX formerly did not even support the notion of disk partitions. The volume manager is called LVM, just as on Linux, although the HP-UX version is in fact the original. (Really, it’s Veritas software…)

As a simple example of LVM wrangling, here’s how you would configure a 75GB hard disk for use with the logical volume manager. If you have read through the Linux example above, the following procedure will seem eerily familiar. There are a few minor differences, but the overall process is essentially the same.

The pvcreate command identifies physical volumes.

```
$ sudo pvcreate /dev/rdisk/disk4
Creating "etc/lvmtab.p".
Physical volume "/dev/rdisk/disk4" has been successfully created.
```

If you will be using the disk as a boot disk, add the -B option to pvcreate to reserve space for a boot block, then run mkboot to install it.
