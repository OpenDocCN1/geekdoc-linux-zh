| Types | Description |
|---|---|
| auto | Attempts to detect the file system type automatically. |
| minux | Minix file systems (filenames are limited to 30 characters). |
| ext | Earlier version of Linux file system, no longer in use. |
| ext3 | Standard Linux file system supporting long filenames and large file sizes. Includes journaling. |
| ext2 | Older standard Linux file system supporting long filenames and large file sizes. Does not have journaling. |
| xiaf | Xiaf file system. |
| msdos | File system for MS-DOS partitions (16-bit). |
| vfat | File system for Windows 95, 98, and Millennium partitions (32-bit). |
| reiserfs | A ReiserFS journaling file system. |
| xfs | A Silicon Graphics (SGI) file system. |
| ntfs | Windows NT, Windows XP, and Windows 2000 file systems (read-only access, write access is experimental and dangerous). |
| smbfs | Samba remote file systems, such as NFS. |
| hpfs | File system for OS/2 high-performance partitions. |
| nfs | NFS file system for mounting partitions from remote systems. |
| umsdos | UMS-DOS file system. |
| swap | Linux swap partition or swap file. |
| sysv | Unix System V file systems. |
| iso9660 | File system for mounting CD-ROM. |
| proc | Used by operating system for processes (kernel support file system). |
| devpts | Unix 98 Pseudo Terminals (ttys, kernel interface file system). |
| shmfs and tmpfs | Linux Virtual Memory, POSIX shared memory maintenance access (kernel interface file system). |

# mount Options

The field after the file system type lists the different options for mounting the file system. You can specify a default set of options by simply entering defaults, or you can list specific options next to each other separated by a comma (no spaces). The defaults option specifies that a device is read / write (rw), that it is asynchronous (async), that it is a block device (dev), that it cannot be mounted by ordinary users (nouser), and that programs can be executed on it (exec). By contrast, a CD-ROM has only two options listed for it: ro and noauto. ro specifies that the device is read-only, and noauto specifies it is not automatically