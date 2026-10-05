# ADVANCED INSTALLATION 89

| !!| Partition disks |
|---||
| You are editing partition #1 of SCSI3 (0,0,0) (sda). No existing file | You are editing partition #1 of SCSI3 (0,0,0) (sda). No existing file
system was detected in this partition.

Partition settings:

Use as: Ext4 journaling file system
Mount point: defaults
Mount options: none
Label: S
Reserved blocks: 5
typical usage: standard
bootable flag: off

Copy data from another partition
Delete the partition
Done setting up the partition

<Go Back|>

Figure 3-30 The Partition settings screen

this line and press RETURN; the installer displays How to use this partition screen (Figure-3-31). You can select ext2 for /boot and /usr, swap area (page 37), RAID (page 91), LVM (page 41), or another type of filesystem. Table 12-1 on page 505 lists common types of filesystems. Move the highlight to the selection you want and press RETURN. The partition editor redisplays the Partition settings screen, which reflects the selection you made. For a swap area, there is nothing else to set up; skip to "Done setting up the partition" on the next page.

Specifying a mount point The mount point defaults to /(root). To change the mount point for the filesystem, point highlight the line labeled Mount point and press RETURN. The partition editor displays a

| !!| Partition disks |
|---||
| How to use this partition:
Ext4 journaling file system
Ext3 journaling file system
Ext2 file system
ReiserFS journaling file system
JFS journaling file system
XFS journaling file system
FAT16 file system
FAT32 file system
swap area
physical volume for encryption
physical volume for RAID
physical volume for LVM
do not use the partition

<Go Back>|

Figure 3-31 How to use this partition screen