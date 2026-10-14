| Table 4.2 Overview of FAT, HPFS, and NTFS |
|---|---|---|
| Filesystem | Maximum File and Volume Sizes | Performance Characteristics |
| FAT | 4 gigabytes | Best for partitions smaller than 500 megabytes. |
| HPFS | 4 gigabytes | Better than FAT, but worse than NTFS. |
| NTFS | 16 exabytes (theoretical)
2 terabytes (realistic) | Best for partitions larger than 500 megabytes. |

# Large Disk Support

NTFS supports very large disks, theoretically up to 16 exabytes. Current physical limitations place the actual limit at 2 terabytes. While it is not possible to have such a large disk volume or logical partition today, we must remember that it was nearly inconceivable to have 1-gigabyte disks in personal computers just 10 years ago. Since we cannot predict the future, Microsoft designed NTFS as a 64-bit filesystem capable of adapting to whatever the future may bring. Another notable and related feature is that NTFS also supports a maximum theoretical file size of 16 exabytes, so it is possible to have a single file occupying the maximum volume size in NTFS. This may prove to be very useful in the future, as databases continue to grow in size.

# Security

NTFS supports file-level security; that is, access permissions can be set on individual files, directories, and volumes. This feature gives system administrators nearly unlimited control over access permissions. The amount of control is really only limited by the amount of time the administrator wants to spend configuring the system (and by the imagination, of course).

The security structure is stored as an Access Control List (ACL), along with the other file attributes in the file record. Access Control Lists will be discussed in greater detail in Chapter 11. Access permissions can be both granted and denied in NTFS on both user and group levels. Permissions can be adjusted by system administrators, the designated owner of a file or directory, and those users or groups granted permission to change the access permissions by the administrator or owner. It should be clear by now that NTFS provides a high level of access control.