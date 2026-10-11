Table 5-12 
Options Used with umount 
| Option | Use |
| :----- | :--- |
| -V | Displays version information. |
| -h | Displays help information. |
| -v | Unmounts the file system verbosely. |
| -n | Unmounts without writing to the /etc/mtab file. |
| -r | If unmounting fails, attempts to remount in read-only mode. |
| -a | Unmounts all file systems listed in the /etc/mtab file. |
| -f | Forces unmounting of the file system. |
| -V | Displays version information. |

Following is an example of the correct use of the *umount* command.

```
# umount /mnt/cdrom
```

This command will umount the device currently mounted to /mnt/cdrom so that it can be ejected.

There are two files you need to know about when mounting and umounting files: /etc/fstab and /etc/mtab.

# ## Checking available file systems with /etc/fstab

The /etc/fstab file contains the file systems mounted when a Linux system starts. This file also contains file systems that are mounted manually. If a file system is listed in this file and the proper rights are set, it can be mounted simply by issuing the *mount* command and the directory, as in the following:

```
# mount /mnt/floppy
```

An example of the /etc/fstab file is shown below. As you can see from this file, device names are listed followed by the mount point. Next is the file system type and whether the file system is mounted automatically by the operating system or manually by the user. Umask information is also stored here. The umask information is used to set the default permissions on newly created files and directories. This example shows devices mounted using the supermount option available as an option in some Linux kernels. Supermount is designed to prevent the manual mounting and umounting currently required when changing removable media such as floppy and CD-ROM disks. When working with the mount commands and