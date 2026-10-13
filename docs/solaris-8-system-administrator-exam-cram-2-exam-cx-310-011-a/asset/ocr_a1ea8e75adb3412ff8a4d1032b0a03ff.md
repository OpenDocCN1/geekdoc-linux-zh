| Field | Description |
|---|---|
| FS Type | File system type |
| fsck Pass | Flag used to indicate whether the **fsck** command should be executed automatically (a nonzero numeric value indicates yes) |
| Mount At Boot | A “yes” indicates that the file system should be mounted at boot or when the **mountall** command is executed; otherwise, “no” |
| Mount Options | Any mount options appropriate for the file system |

The **umountall**(1M) command unmounts all the file systems listed in the /etc/mnttab file, except root, /proc, /var, and /usr.

![](bbox=[0.119, 0.357, 0.222, 0.426])

Keep in mind the purpose of the /etc/mnttab and /etc/vfstab files. The /etc/mnttab file lists currently mounted file systems (unless the **-m** command-line argument is used with the **mount** command). The /etc/vfstab file provides a list of file systems that should be mounted automatically at system boot or when the **mountall** command is used.

# Accessing Data on CD-ROMs and Floppy Disks

Properly formatted floppy disks and CD-ROMs can be mounted by using the **mount** command and accessed like any other file system. The **umount** command is also used to unmount a floppy disk or CD-ROM. However, in the Solaris environment, mounting these types of media has been made easier by use of *Volume Management*, which provides automatic mounting of removable volumes (floppy disks and CD-ROMs). This service is provided by the Volume Management daemon, vold(1M). By default, vold is enabled.

# Using CD-ROMs

When a CD-ROM is inserted into a CD-ROM drive, the **vold** program recognizes a properly formatted CD-ROM and automatically mounts it under the /cdrom directory. The first CD-ROM is mounted at /cdrom/cdrom0, the second at /cdrom/cdrom1, and so on. If the CD-ROM is partitioned (which it probably is), each slice or partition is mounted. For example, if the CD-ROM volume contains six slices (so through s5), then each is mounted (/cdrom/cdrom0/s0 through /cdrom/cdrom0/s5). Once mounted, the partitions can be used like any other read-only disk drive.

When the CD-ROM is no longer needed, you can use the **eject cdrom** command to automatically unmount all partitions associated with it and eject the