# TABLE 5.1 Common Non-Linux Filesystems (continued)

| Filesystem Name | Linux Filesystem Type Code | Native OS or Use |
|---|---|---|
| ISO-9660 | iso9660 | CD-ROMs and similar media; Linux includes Joliet and Rock Ridge support for long file-names and Unix-style permissions and ownership. |
| Universal Disc Format (UDF) | udf | DVDs and read/write optical media. |

![](bbox=[0.14, 0.36, 0.24, 0.45])

> Linux can create many, but not all, of the filesystems described in Table 5.1. To create an ISO-9660 or UDF filesystem, you'd ordinarily use the `mkiso fs` utility, which creates a disk file that holds an image of the filesystem and all the files it's to contain. You can then write that image file to a CD-R or similar disc using `cdrecord`. Various GUI tools, such as X-CD-Roast and ERoaster, provide point-and-click interfaces to this process.

In addition to disk-based filesystems, Linux supports various filesystems that provide access to files on other computers. The most important of these are the Network File System (NFS) and the Server Message Block/Common Internet File System (SMB/CIFS). NFS is most often used between Linux and Unix systems, whereas SMB/CIFS is used on DOS and Windows networks. You don't create an NFS or SMB/CIFS filesystem on your disk, though; instead, these filesystems are network protocols that give remote access to ext2s, ReiserFS, FAT, ISO-9660, or any other disk filesystem. You can use the nfs filesystem type code with a `mount` command to mount an NFS export or use the smbfs or cifs type code to mount an SMB/CIFS share.

# Creating a Filesystem

To create a filesystem, you use the `mksfs` tool, to which you pass the filesystem type code using the `-t` option and the device file for the partition or disk that should hold the filesystem:

```
`# mksfs -t ext3 /dev/sda1`
```

![](bbox=[0.14, 0.82, 0.24, 0.91])

> Remember to check, double-check, and triple-check your command! You do not want to enter the wrong device filename! If you accidentally omit the partition number (as in `/dev/sda` rather than `/dev/sda1`), you'll create a filesystem on the entire disk, wiping out all the disk's partitions.