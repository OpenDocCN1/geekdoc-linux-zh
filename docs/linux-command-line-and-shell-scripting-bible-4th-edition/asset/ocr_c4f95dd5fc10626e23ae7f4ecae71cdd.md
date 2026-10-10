```
[...]
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 1
First sector  (2048-4194303, default 2048):
Last sector, +sectors or +size{K,M,G,T,P} (2048-4194303,
default 4194303):

Created a new partition 1 of type 'Linux' and of size 2 GiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

$ 

```

Now a new disk partition, /dev/sdb1, is ready for formatting. Be aware when creating a new disk partition with fdisk, you don't have to type in any information. Instead, just press Enter to accept the displayed defaults.

# Working with gdisk

If you're working with drives that use the GUID Partition Table (GPT) indexing method, you can use the gdisk program:

```
$ sudo gdisk /dev/sda
[sudo] password for christine:
GPT fdisk (gdisk) version 1.0.3

Partition table scan:
 MBR: MBR only
 BSD: not present
 APM: not present
 GPT: not present

*******************************************************

Found invalid GPT and valid MBR; converting MBR to GPT format
in memory. THIS OPERATION IS POTENTIALLY DESTRUCTIVE! Exit by
typing 'q' if you don't want to convert your MBR partitions
to GPT format!

```