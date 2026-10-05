# FILE SYSTEMS AND PARTITIONS 101

You can carry out modifications to the file system only if you are logged in root. If this is not the case, you must change to a free console and root when logging in there.

The device names in this section represent the author's system. Each Linux installation is different! For this reason, it is highly likely that you will have to specify a different name to access drive c: on your computer.

Let us assume you have a text file in DOS drive c: which you want to process under Linux. Currently, this hard partition is not accessible under Linux. When executing the mount command, you must in principle specify three items: the device name for drive c;, the name of a directory into which the hard disk should be linked and the name of the file system.

The device name depends on whether you work with IDE or SCSI disks. Naming conventions for hard disks have already been described on page 37. In case of doubt, disk -l can help.

The following table summarizes the naming conventions for IDE and SCSI hard disks and partitions. Please note the noting of a 'normally' partitioned hard disk shows gaps: an IDE hard disk with one primary data partition, one extended partition (which, internally, is equally handled as a primary partition), and two logical partitions, will have the device name /dev/sda1, -2 and -6.

# Device names of hard disk(s) (partitions)

+   /dev/sda to /dev/hdf 8 IDE hard disks
/dev/sda to /dev/sdp 16 SCSI hard disks

+   /dev/...1 to /dev/...4 max 4 primary partitions
/dev/hd.5 to /dev/hd.63 max 59 logical partitions (IDE)
/dev/sd.5 to /dev/sd.15 max 11 logical partitions (SCSI)

In principle, it does not matter which directory you specify with. If you do not possess a created directory for this purpose easier disk accesses, create a new one with mkdir. A common location would be a subdirectory under /mnt.

The file system type depends on how the partition or hard disk has been formatted. The most frequent types are ext2 (Linux file system), msdos (MS-DOS, file names with 8+3 characters), vfat (Windows 9, up to 255 characters for file names, from kernel 1.3 onwards), and hfs (OS/2, read only).

```
root mkdir /dos
root mount -r t mdos /dev/sda3 /dos
root df
Filesystem 1024-blocks Available Capacity Mounted
/dev/sdc7 308223 168887 123925 58% /
/dev/sdc5 204564 79304 125260 39% /mnt/dosi
/dev/sda3 45860 44096 1764 96% /mnt/dosc
```