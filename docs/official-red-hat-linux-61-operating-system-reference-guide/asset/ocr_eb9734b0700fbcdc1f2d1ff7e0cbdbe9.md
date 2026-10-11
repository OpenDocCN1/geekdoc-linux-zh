> **Please Note**
> Red Hat Linux 6.2 can access FAT32 filesystems using the `vfat` filesystem type.

+   - **Size**: Size may indicate the size of the filesystem in megabytes (M), or it may not be filled in.

+   - **Partition type**: A description of the filesystem used on that partition (may not be filled in).

+   - **Status**: Whether the device is mounted or not.

Filesystems from other machines on a network may also be available. These can range from single small directories to entire volumes. No information on **Size** or **Partition type** is available for these partitions, either. Additional information on NFS filesystems (should you have any available) will be contained under:

Config => File systems => Access nfs volume