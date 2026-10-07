# Using the *mount* Command

Linux uses the mount command to make a filesystem available. Here is the basic format of this command:

```
mount [-t fstype] [-o options] device dir
```

The *fstype* is the filesystem type, such as ext2, vfat, or jfs. You can often omit the –t parameter, and Linux will correctly detect the filesystem type. The preceding discussion of filesystems for Linux includes these type codes.

*device* is the Linux device file associated with the filesystem. For instance, /dev/sdb4 indicates the fourth partition on the second SCSI disk, and /dev/fd0 indicates the first floppy disk.

*dir* is the mount point, which should be an empty directory. (You can use a nonempty directory, but then you lose access to the files stored in that directory for as long as the filesystem is mounted.)

The *options* are special codes that give Linux instructions on how to treat filesystem features. Some options apply to most or all filesystems, but others are filesystem-specific. Type **man mount** for a discussion of the filesystem options that apply to most of the standard Linux filesystems, and consult the filesystem’s documentation for information on rarer filesystem options. Table 6.1 summarizes the most important filesystem options.

Table 6.1: Important Filesystem Options for the mount Command

| Option | Supported Filesystems | Description |
| :---- | :---- | :---- |
| default | All | Uses the default options for this filesystem. It's used primarily in the /etc/fstab file (described shortly) to ensure that there's an options column in the file. |
| loop | All | Uses the loopback device for this mount. Allows you to mount a file as if it were a disk partition. For instance, entering mount –t vfat –o loop image.img/mnt/image mounts the file image.img as if it were a disk. |
| auto or noauto | All | Mounts or does not mount the filesystem at boot time, or when root issues the mount –a command. Default is auto, but noauto is appropriate for removable media. Used in /etc/fstab. |
| user or nouser | All | Allows or disallows ordinary users to mount the filesystem. Default is nouser, but user is often appropriate for removable media. Used in /etc/fstab. When included in this file, user allows users to type mount /mountpoint, where /mountpoint is the assigned mount point, to mount a disk. |
| owner | All | Similar to user, except that the user must own the device file. Some distributions, such as Red Hat, assign ownership of some device files (such as /dev/fd0, for the floppy disk) to the console user, so this can be a helpful option. |


143