# Mount point

The **mount point** for the filesystem/directory hierarchy that you are mounting is a directory in the local filesystem. This directory must exist before you can mount a filesystem; its contents disappear as long as a filesystem is mounted on it and reappear when you unmount the filesystem. See page 38 for a discussion of mount points.

Without any arguments, **mount** lists the mounted filesystems, showing the physical device holding each filesystem, the mount point, the type of filesystem, and any options set when each filesystem was mounted. The **mount** utility gets this information from the /etc/mtab file (page 508), which is a link to the /proc/self/mounts. On a system running systemd page 438, **mount** lists so many virtual filesystems it can be difficult to find the physical filesystems. Instead you can use findmnt with the -t (--types) option to display one type of filesystem such as ext4:

```
$ findmnt -t ext4
TARGET        SOURCE                      FSTYPE OPTIONS
/dev/mapper/fedora-root  ext4      rw,relatime,seclabel,data=ordered
/boot           /dev/sda1                   ext4      rw,relatime,seclabel,data=ordered
```

The first entry in the preceding example shows an LV mounted by the LVM (page 44) device mapper on / (root). As explained on page 40, the /boot partition cannot reside on an LV; it is mounted on /dev/sda1.

# Do not mount anything on root (/)

# caution

Always mount network directory hierarchies and removable devices at least one level below the root level of the filesystem. The root filesystem is mounted on /; you cannot mount two filesystems in the same place. If you were to try to mount something on /, all files, directories, and filesystems that were under the root directory would no longer be available, and the system would crash.

# optional

An easy way to know when a filesystem is not mounted is to create a file named **NOTMOUNTED** in the directory that is the mount point. That way, ls shows **NOTMOUNTED** when the filesystem is not mounted, making it clear the filesystem is not mounted. When the filesystem is mounted, the **NOTMOUNTED** file is hidden and ls does not display its name.

Give the following **touch** command (you will probably need to work with **root** privileges) to create a file named **NOTMOUNTED** in the /p02 directory. You must give the command while the filesystem that gets mounted on /p02 is not mounted. Otherwise the file appears when the filesystem is mounted. The subsequent commands show ls displaying **NOTMOUNTED** while the filesystem is not mounted and displaying the files on the mounted filesystem.

```
$ su -c ' touch /p02/NOTMOUNTED'
$ ls /p02
NOTMOUNTED
$ su -c ' mount /p02'
$ ls /p02
memo1.
...
```