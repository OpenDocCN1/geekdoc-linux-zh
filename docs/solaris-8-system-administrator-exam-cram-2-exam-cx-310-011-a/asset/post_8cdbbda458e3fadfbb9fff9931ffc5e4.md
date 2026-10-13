
- nosuid—Disallow setuid execution on files.
- suid—Allow setuid execution on files (default).

The following (abbreviated) example shows the use of the **mount** command:

```
# mount
/proc on /proc read/write
/ on /dev/dsk/c0d0s0 read/write/largefiles
/usr on /dev/dsk/c0d0s0 read/write/largefiles
/var on /dev/dsk/c0d0s3 read/write/largefiles
/opt on /dev/dsk/c0d0s5 read/write/largefiles
/tmp on swap read/write
# mount -F ufs -o nolargefiles,noatime /dev/dsk/c0d1s7 /usr2
# mount
/proc on /proc read/write
/ on /dev/dsk/c0d0s0 read/write/largefiles
/usr on /dev/dsk/c0d0s0 read/write/largefiles
/var on /dev/dsk/c0d0s3 read/write/largefiles
/opt on /dev/dsk/c0d0s5 read/write/largefiles
/tmp on swap read/write
/usr2 on /dev/dsk/c0d1s7 read/write/nolargefiles/noatime
#
```

![](img/b957f979417d9f16274c2eb52c8f2c9f_225_0.png)

You can use the **mount** command to mount CacheFS, HSFS, NFS, PCFS, TMPFS, UDF, and UFS file systems. Unlike the other file system commands, the **mount** command expects a logical block device name of a partition in which the file system resides.

The **umount**(1M) command is used to unmount a file system. The file system cannot be unmounted if it is busy (for example, a program residing on the file system is being executed, or the current directory of a logged-in user account is within the file system). Either the logical block device name or the mount point can be specified as a command-line argument.

The **mountall**(1M) command mounts all file systems listed in the /etc/vfstab file. This file is also used to determine the file systems to automatically mount during system boot. You can add or remove file systems in the /etc/vfstab file with any standard text editor. Table 9.4 lists the (tab-separated) fields of an entry in the /etc/vfstab file. A hyphen indicates no entry in a field.

**Table 9.4 Fields of the /etc/vfstab File**

| Field | Description |
|---|---|
| Device To Mount | Logical block device name of the file system partition to mount |
| Device To fsck | Logical block device name used for the **fsck** command |
| Mount Point | Subdirectory where the file system should be mounted |
| FS Type | File system type |
| fsck Pass | Flag used to indicate whether the **fsck** command should be executed automatically (a nonzero numeric value indicates yes) |
| Mount At Boot | A “yes” indicates that the file system should be mounted at boot or when the **mountall** command is executed; otherwise, “no” |
| Mount Options | Any mount options appropriate for the file system |

The **umountall**(1M) command unmounts all the file systems listed in the /etc/mnttab file, except root, /proc, /var, and /usr.

![](img/b957f979417d9f16274c2eb52c8f2c9f_226_0.png)

Keep in mind the purpose of the /etc/mnttab and /etc/vfstab files. The /etc/mnttab file lists currently mounted file systems (unless the **-m** command-line argument is used with the **mount** command). The /etc/vfstab file provides a list of file systems that should be mounted automatically at system boot or when the **mountall** command is used.

## Accessing Data on CD-ROMs and Floppy Disks

Properly formatted floppy disks and CD-ROMs can be mounted by using the **mount** command and accessed like any other file system. The **umount** command is also used to unmount a floppy disk or CD-ROM. However, in the Solaris environment, mounting these types of media has been made easier by use of *Volume Management*, which provides automatic mounting of removable volumes (floppy disks and CD-ROMs). This service is provided by the Volume Management daemon, vold(1M). By default, vold is enabled.

### Using CD-ROMs

When a CD-ROM is inserted into a CD-ROM drive, the **vold** program recognizes a properly formatted CD-ROM and automatically mounts it under the /cdrom directory. The first CD-ROM is mounted at /cdrom/cdrom0, the second at /cdrom/cdrom1, and so on. If the CD-ROM is partitioned (which it probably is), each slice or partition is mounted. For example, if the CD-ROM volume contains six slices (s0 through s5), then each is mounted (/cdrom/cdrom0/s0 through /cdrom/cdrom0/s5). Once mounted, the partitions can be used like any other read-only disk drive.

When the CD-ROM is no longer needed, you can use the **eject cdrom** command to automatically unmount all partitions associated with it and eject the CD-ROM from the CD-ROM drive. If more than one CD-ROM is mounted, you specify the mount point—for example, **eject cdrom0**. See the **eject(1)** manual page for more details.

### Using Floppy Disks

Unlike CD-ROMs, floppy disks are not automatically mounted by the **vold** program. Instead, you can use the **volcheck(1)** command to instruct **vold** to scan all floppy disk drives and mount any floppy disks under the /floppy directory. The first floppy disk is mounted at /floppy/floppy0, the second at /floppy/floppy1, and so on. Once mounted, the floppy disk can be used like any (small) read/write disk drive.

When the floppy disk is no longer needed, you can use the **eject** command without any command-line arguments to unmount it. Or, if more than one floppy disk is mounted, you supply the name of the mount point as a command-line argument—for example, **eject floppy0**.

## Monitoring File System Usage

Several commands can be used to monitor file system usage: **df(1)**, **du(1)**, and **quot(1M)**.

The **df** command (without command-line arguments) displays the mount point, logical block device name, number of free 512-byte blocks, and number of files that can be created for each file system. (The **-k** command-line argument lists sizes in 1,024-byte blocks or kilobytes instead of 512-byte blocks.) The command can also be used to display the disk space used by file systems. The following example shows the use of the df command:

```text
# df
/proc            (/proc          ):       0 blocks     948 files
/                (/dev/dsk/c0d0s0 ):    56098 blocks    35834 files
/usr              (/dev/dsk/c0d0s3 ):   181578 blocks    168053 files
/var              (/dev/dsk/c0d0s3 ):   307080 blocks    147835 files
/export/home      (/dev/dsk/c0d0s7 ):  1854626 blocks    488882 files
/opt              (/dev/dsk/c0d0s5 ):    15272 blocks    109653 files
/tmp              (swap           ):   311360 blocks       9985 files
/usr2             (/dev/dsk/c0d1s7 ):  2039566 blocks    256508 files
#
```

The **du** command lists the number of 512-byte blocks allocated to each subdirectory and the total for the current directory. Several frequently used command-line arguments include **-a** to list all nondirectory files, **-k** to list sizes in terms of 1,024-byte blocks (kilobytes) instead of 512-byte blocks, and **-s** to report only the total sum of the specified files. The following example uses the **du** command to determine the amount of storage space allocated to the /etc/openwin directory and its contents:

```text
# cd /etc/openwin
# du
4        ./etc/devdata/SUNWaccel/monitors/pnp
6        ./etc/devdata/SUNWaccel/monitors
8        ./etc/devdata/SUNWaccel
10       ./etc/devdata
12       ./etc
10       ./server/etc
12       ./server
2        ./devdata/profiles
4        ./devdata
30       .
#
```

The **quot** command lists the number of 1,024-byte blocks of a file system owned by each user. You must specify a file system (mount point) or **-a** (all mounted file systems) as a command-line argument. Another useful command-line argument is **-f**, which displays the number of files in addition to the amount of space available. The following example shows the **quot** command:

```text
# quot /export/home
/dev/rdsk/c0d0s7:
17627    root
  133    dla
    2    guest
    1    sys
#
```

## File and Directory Concepts

Data stored on file systems consists of directories and files. Directories serve as folders to arrange the files into some organized, user-defined structure. In reality, all the files and directories are stored more or less randomly on the disk. The files and (other) directories are then referenced or *linked* into directories to provide the organization. In addition, several types of special files are used.

Sometimes files and directories are not needed frequently or use up more space than desired. To address this issue, Solaris 8 provides several utilities to *compress* files and directories so that they take up less space; they can be *uncompressed* as needed.

The following sections provide an overview of these file/directory concepts and file/directory compression.
