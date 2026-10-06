# TABLE 3.5 Important filesystem options for the mount command

| Option | Supported filesystems | Description |
| --- | --- | --- |
| defaults | All | Causes the default options for this filesystem to be used. It's used primarily in the /etc/fstab file to ensure that the file includes an options column. |
| loop | All | Causes the loopback device for this mount to be used. Allows you to mount a file as if it were a disk partition. For instance, mount -t vfat image.img /mnt/ mounts the file image .img as if it were a disk. |
| auto or noauto | All | Doesn't mount the filesystem at boot time or when root issues the mount -a command. The default is auto, but noauto is appropriate for removable media. Used in /etc/fstab. |
| user or nouser | All | Allows or disallows users to mount the filesystem. The default is user, but user is often appropriate for removable media. Used in /etc/fstab. When included in this file, allow users to type mount /mountpoint (where /mountpoint is the assigned mount point) to mount a disk. Only the user who mounted the filesystem may unmount it. |
| users | All | Similar to user, except that any user may unmount a filesystem once it's mounted. |
| owner | All | Similar to user, except that the user must own the device file. Some distributions, such as Red Hat, assign ownership of some device files (such as /dev/fd0) to the console user, which can be a helpful option. |
| remount | All | Changes one or more mount options without explicitly mounting a partition. To issue a mount command on an already-mounted filesystem use remount along with any options you want to change. This feature can be used to enable or disable access to a partition, for example. |
| ro | All | Specifies a read-only mount of the filesystem. This is the default for filesystems that include no write access and for some with particularly unreliable write support. |
| rw | All read/write file systems | Specifies a read/write mount of the filesystem. This is the default for most read/write filesystems. |