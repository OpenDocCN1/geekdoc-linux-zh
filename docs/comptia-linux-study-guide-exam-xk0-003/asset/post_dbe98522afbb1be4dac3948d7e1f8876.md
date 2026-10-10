
## TABLE 6.6 mount Options (continued)

- **-t fstype**: Use this parameter to specify the filesystem type. Common filesystem types are ext2 (for ext2fs), ext3 (for ext3fs), ext4 (for ext4fs), reiserfs (for ReiserFS), jfs (for JFS), xfs (for XFS), vfat (for FAT with VFAT long filenames), msdos (for FAT using only short DOS filenames), iso9660 (for most CD-ROM filesystems), udf (for the newer UDF CD-ROM/DVD-ROM filesystem), nfs (for NFS network mounts), smbfs (for SMB/CIFS network shares), and cifs (a newer driver for SMB/CIFS network shares). Linux supports many others. If this parameter is omitted, Linux will attempt to autodetect the filesystem type.
- **-O**: You can add filesystem-specific options using the -O parameter. See Table 6.7.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_306_0.png)

> Linux requires support in the kernel or as a kernel module to mount a filesystem of a given type. If this support is missing, Linux will refuse to mount the filesystem in question.

Table 6.6 isn't comprehensive; consult the man page for some of the more obscure options. The most common applications of mount use few parameters, because Linux generally does a good job of detecting the filesystem type, and the default parameters work reasonably well. For instance, consider this example:

```
# mount /dev/sdb7 /mnt/shared
```

This command mounts the contents of /dev/sdb7 on /mnt/shared, autodetecting the filesystem type and using the default options. Ordinarily, only root may issue a mount command; however, if /etc/fstab specifies the user, users, or owner option, an ordinary user may mount a filesystem using a simplified syntax in which only the device or mount point is specified, but not both. For instance, a user might type `mount /mnt/cdrom` to mount a CD-ROM, if /etc/fstab specifies /mnt/cdrom as its mount point and uses the user, users, or owner option.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_306_1.png)

> Many Linux distributions ship with automounter support, which causes the OS to automatically mount removable media when they're inserted. In GUI environments, a file browser may also open on the inserted disk. In order to eject the disk, the user will need to unmount the filesystem by using umount, as described in the upcoming section “Using umount,” or by selecting an option in the desktop environment.

When Linux mounts a filesystem, it ordinarily records this fact in `/etc/mtab`. This file has a format similar to that of `/etc/fstab` and is stored in `/etc`, but it’s not a configuration file that you should edit. You might examine this file to determine what filesystems are mounted, though. (The `df` command, described in more detail in the section “Using df,” is another way to learn what filesystems are mounted.)

### Using mount Options

When you need to use special parameters, it’s usually to add filesystem-specific options. Table 6.7 summarizes the most important filesystem options. Some of these are meaningful only in the `/etc/fstab` file.

**TABLE 6.7** Important Filesystem Options for the `mount` Command

| Option | Supported Filesystems | Description |
| --- | --- | --- |
| `defaults` | All | Uses the default options for this filesystem. It’s used primarily in the `/etc/fstab` file to ensure that there’s an options column in the file. |
| `loop` | All | Uses the loopback device for this mount. Enables you to mount a file as if it were a disk partition. For instance, `mount -t vfat -o loop image.img /mnt/image` mounts the file `image.img` as if it were a disk. |
| `auto` or `noauto` | All | Mounts or does not mount the filesystem at boot time or when root issues the `mount` command. The default is auto, but noauto is appropriate for removable media. Used in `/etc/fstab`. |
| `user` or `nouser` | All | Allows or disallows ordinary users to mount the filesystem. The default is `nouser`, but user is often appropriate for removable media. Used in `/etc/fstab`. When included in this file, user allows users to type `mount /mountpoint`, where `/mountpoint` is the assigned mount point, to mount a disk. Only the user who mounted the filesystem may unmount it. |
| `users` | All | Similar to user, except that any user may unmount a filesystem once it’s been mounted. |
| `owner` | All | Similar to user, except that the user must own the device file. Some distributions, such as Red Hat, assign ownership of some device files (such as /dev/fd0, for the floppy disk) to the console user, so this can be a helpful option. |
| `remount` | All | Changes one or more mount options without explicitly unmounting a partition. To use this option, you issue a mount command on an already-mounted filesystem, but with remount along with any options you want to change. Can be used to enable or disable write access to a partition, for example. |
| `ro` | All | Specifies a read-only mount of the filesystem. This is the default for filesystems that include no write access and for some with particularly unreliable write support. |
| `rw` | All read/write filesystems | Specifies a read/write mount of the filesystem. This is the default for most read/write filesystems. |
| `uid=value` | Most filesystems that don’t support Unix-style permissions, such as vfat, hfs, ntfs, and hfs | Sets the owner of all files. For instance, uid=500 sets the owner to whoever has Linux user ID 500. (Check Linux user IDs in the /etc/passwd file.) |
| `gid=value` | Most filesystems that don’t support Unix-style permissions, such as vfat, hfs, ntfs, and hfs | Works like uid=value but sets the group of all files on the filesystem. You can find group IDs in the /etc/group file. |
| `umask=value` | Most filesystems that don’t support Unix-style permissions, such as vfat, hfs, ntfs, and hfs | Sets the umask for the permissions on files. value is interpreted in binary as bits to be removed from permissions on files. For instance, umask=027 yields permissions of 750, or rwxr-x--. Used in conjunction with uid=value and gid=value, this option lets you control who can access files on many foreign filesystems. |
| `conv=code` | Most filesystems used on Microsoft and Apple OSs: msdos, umsdos, vfat, hpfs, and hfs | If *code* is *b* or *binary*, Linux doesn’t modify the files’ contents. If *code* is *t* or *text*, Linux autoconverts files between Linux-style and DOS- or Macintosh-style end-of-line characters. If *code* is *a* or *auto*, Linux applies the conversion unless the file is a known binary file format. It’s usually best to leave this at its default value of *binary* because file conversions can cause serious problems for some applications and file types. |
| `norock` | iso9660 | Disables Rock Ridge extensions for ISO-9660 CD-ROMs. |
| `nojoliet` | iso9660 | Disables Joliet extensions for ISO-9660 CD-ROMs. |

Some filesystems support additional options that aren’t described here. The *mount man* page covers some of these, but you may need to look to the filesystem’s documentation for some filesystems and options. This documentation may appear in `/usr/src/linux/Documentation/filesystems` or `/usr/src/linux/fs/fname`, where *fname* is the name of the filesystem.

### Using umount

The *umount* command is simpler than *mount*. The basic *umount* syntax is as follows:

```
umount [-afnrV] [-t fstype] [device | mountpoint]
```

Most of these parameters have similar meanings to their meanings in *mount*, but some differences deserve mention, as summarized in Table 6.8.

**TABLE 6.8** umount Options That Differ from mount Options

| Option | Description |
| --- | --- |
| `-a` | Rather than unmount partitions listed in `/etc/fstab`, this parameter causes the system to attempt to unmount all the partitions listed in `/etc/mtab`, the file that holds information on mounted filesystems. On a normally running system, this operation is likely to succeed only partly because it won’t be able to unmount some key filesystems, such as the root partition. |
