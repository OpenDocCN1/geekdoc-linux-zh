# Tuning the System 289

Make adjustments and rerun the hdparm test command until you've found the optimal settings. If you want to make these changes permanent, use the -k option with hdparm as shown:

```
# /sbin/hdparm -k 1 /dev/hda
```

Changing the number of sectors transferred on each interrupt by setting the -m option may buy you a minor performance gain, but we haven't seen a real change when we've used it.

# mke2fs

The mke2fs command creates a new filesystem on a disk partition or other device. If your Linux system typically works with very large files, you may be able to obtain a noticeable filesystem improvement by formatting your drives with larger block sizes. By default, the Linux filesystem uses 1024-byte blocks. If you're going to manipulate files that are bigger than a gigabyte in size, you might try setting the block size to 4K with the mke2fs command:

```
# mke2fs -b 4096 /dev/hda3
```

The mke2fs command creates a new filesystem on the partition specified. This operation destroys any data that has been on that partition, so it won't except on an empty partition.

# defrag

When you write a file to disk, it can't always be written in consecutive blocks. A file that is not stored in consecutive blocks is said to be fragmented. It takes longer to read a fragmented file because the disk's read-write head is required to move more. You want to avoid disk fragmentation, even though a good buffer cache with read-ahead ability makes it less of an issue. Luckily the ext2 filesystem is very careful in its block selection so as to minimize fragmentation.

The Debian distribution comes with a utility called defrag, which is released under the GPL and is available for public consumption. You can download it from ftp://metalab.unc.pub/Linux/system/filesystems.

# chattr

Linux keeps track of the last time a file was modified and updates the timestamp appropriately. This process involves the use of the find and fsck commands, and it can be resource-intensive for systems that contain large amounts of constantly changing data, such as a newsfeed or mail server. In order to save the time and resources involved, you might choose to turn off the last-access-time modification as superuser with the chattr command:

```
# chattr +A filename
```

![](bbox=[0.903, 0.535, 0.963, 0.633])