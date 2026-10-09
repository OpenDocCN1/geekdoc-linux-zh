# EXT

The standard Linux filesystems—EXT2, EXT3, and EXT4—support many of the same features as UFS. FreeBSD can safely read from and write to EXT2 and EXT3 filesystems without any problems but can mount EXT4 filesystems only as read-only.

Mounting Linux filesystems is most useful for disaster recovery, dual-boot systems, or system migrations. Despite the name, `mount -t ext2fs` supports mounting all versions of EXT.

Linux filesystem users might find the tools in `/usr/ports/sysutils/e2fsprogs` useful. They let you `fsck(8)` and assess Linux filesystems, among other things.

# Permissions and Foreign Filesystems

Permissions of a filesystem depend on the filesystem features and the person who mounts it. FreeBSD tries to support features that aren’t too different from those in UFS or ZFS.

Consider the Linux filesystem, EXT. EXT stores permissions in the filesystem and lets the kernel map them to UIDs. Since EXT permissions behave much like UFS permissions and all the necessary permissions information is available within the filesystem, FreeBSD respects the permissions on these filesystems. EXT doesn’t support BSD file flags, however, so you can’t assign those flags to a file on EXT.

FAT has no permissions system. Even if you mount your FAT32 thumb drive in your FreeBSD host, you can’t apply permissions to files.

By default, only root can mount filesystems, and root owns all non-Unix filesystems. If that’s not your preference, you can use the `-u` and `-g` flags to set the user ID and group ID of the owner when you’re mounting a FAT32, ISO 9660, or UDF filesystem. For example, if you’re mounting a FAT32 USB device for the user *xistence* and want him to be able to edit the contents, use this command:

```
# mount -t msdosfs -u xistence -g xistence /dev/da5 /mnt
```

The user *xistence* now owns the files on the device.