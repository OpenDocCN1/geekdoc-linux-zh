
## OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| `-A` | Check all filesystems listed in /etc/fstab if possible. |
| `-C` | Display progress bars if possible. |
| `-N` | Show the actions that would be performed without actually executing them. |
| `-r` | Repair the filesystem interactively. |
| `-R` | Skip the root filesystem, which may be mounted as read and write. |
| `-t type` | Specify the type of filesystem. Available types are listed in /proc/filesystems. |
| `-V` | Display messages. |

## EXIT CODES

| This Code | Indicates the Following |
| :--- | :--- |
| 0 | No errors. |
| 1 | Errors encountered but they were all corrected. |
| 2 | Errors encountered but they were all corrected. Reboot the system if the filesystem was mounted. |
| 4 | Errors encountered but left uncorrected. |
| 8 | Program error. |
| 16 | Usage or syntax error. |
| 128 | Shared library error. |

## EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| `fsck -a /dev/sda1` | Automatically repairs errors on the specified filesystem (/dev/sda1). |

## hformat

```
hformat [ option | device ]
```

Creates a Macintosh Hierarchical File System (HFS) on the specified device (/dev/fd0 or /dev/fd1). You must first perform a low-level format using fdformat. This command is part of the HFS Utilities package (hfstis), which is not distributed with most versions of Linux. To obtain a copy, visit the HFS Utilities home page at http://www.mars.org/home/rob/proj/hfs.

See also hmount.

## OPTIONS

| **Use This Option** | **To Do This** |
| :--- | :--- |
| `-l string` | Create a volume label using the specified string |

## hmount

```
hmount device
```

Mounts a Macintosh floppy disk in the specified device (/dev/fd0 or /dev/fd1). This command is part of the HFS Utilities package (hfstis), which is not distributed with most versions of Linux. To obtain a copy, visit the HFS Utilities home page at http://www.mars.org/home/rob/proj/hfs.

See also hformat, humount.

## humount

```
humount device
```

Unmounts a Macintosh floppy disk in the specified device (/dev/fd0 or /dev/fd1). This command is part of the HFS Utilities package (hfstis), which is not distributed with most versions of Linux. To obtain a copy, visit the HFS Utilities home page at http://www.mars.org/home/rob/proj/hfs.

## mke2fs

```
mke2fs [ option ] device
```

Creates a Linux e2fs filesystem on the specified device, such as a disk partition or a floppy disk.

> **WARNING** This command erases all the data on the specified device.

## OPTIONS

| **Use This Option** | **To Do This** |
| :--- | :--- |
| `-b size` | Specify the size of blocks in bytes. The default is 512. |
| `-c` | Check the device for bad blocks before creating the filesystem. |
| `-f size` | Specify the size of fragments in bytes. |
| `-i size` | Specify the number of bytes used for each inode. |
| `-N n` | Manually set the number of inodes reserved for the filesystem. |
| `-l filename` | Read the list of bad blocks from the specified filename. |
| `-m n` | Set the percentage of blocks reserved for the superuser to the integer n. The default is 5. |
| `-o type` | Manually set the name of the creator operation system. |
| `-q` | Hide all messages. |
| `-s setting` | Set the sparse superblock flag, which saves space on large filesystems. Do not use on kernels earlier than version 2.2. Available settings are 0 (off) and 1 (on). |

## OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| `-F` | Force `mke2fs` to run. |
| `-L string`, `-volume-label string` | Set the filesystem’s volume label using a string of no more than 16 characters. |
| `-M`, `-last-mounted-directory` | Manually set the last mounted directory. |
| `-r` | Set the filesystem revision. |
| `-R stride=n` | Set the number (n, an integer) of blocks in a RAID stripe. |
| `-T type` | Set the intended usage type so that `mke2fs` can optimize the filesystem. The only available type is `news`. |
| `-V` | Display the version number. |

## EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `mke2fs -c /dev/fd0` | Checks the formatted floppy disk in drive `fd0` for bad blocks and creates the Linux filesystem on the disk. |

## mlabel

```
mlabel [ option ] drive: string
```

Used on a mounted MS-DOS filesystem, sets the volume label of the specified drive (A or B) to the specified string.

## OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-c` | Clear the existing label without replacing it |
| `-s` | Show the existing label without replacing it |

## mount

**mount** [ *option* ] *device* | *directory*

Attaches the device to the specified directory, which will serve as the filesystem's mount point. The directory must exist for this command to succeed. Superuser status (see su in Chapter 1) is required to mount all devices except those for which the user option is specified in /etc/fstab.

*See also umount.*

## OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-a` | Mount all the filesystems listed in /etc/fstab, except those set to **noauto**. |
| `-f` | Run through the **mount** procedure and generate all relevant messages but do not actually mount the device. |
| `-r` | Mount the device as read only. |
| `-w` | Mount the device as read and write. This is the default. |
| `-L *label*` | Mount the device that has the specified label. |
| `-t *type*` | Mount the device with the specified *type* of filesystem (see the Filesystem Types table). |
| `-h` | Display the available options. |
| `-v` | Display the version number. |

## EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `mount -a` | Mounts all the devices listed in /etc/fstab. |
| `mount -t iso9660 /dev/cdrom /mnt/cdrom` | Mounts the disk in the CD-ROM drive to the specified mount point (/mnt/cdrom). To mount this device to the specified mount point, the directory /mnt/cdrom must exist. |

| This Command | Does the Following |
| :--- | :--- |
| `mount -t msdos /dev/fd0 /mnt/fd0` | Mounts the MS-DOS floppy disk in drive fd0 to the specified mount point (/mnt/fd0). To mount this device to the specified mount point, the directory /mnt/fd0 must exist. |
| `mount /dev/cdrom` | Mounts the disk in the CD-ROM drive to the mount point given in /etc/fstab. |
| `mount /dev/fd0` | Mounts the disk in the floppy disk drive to the mount point given in /etc/fstab. |

## mt

`mt [ option ] operation`

Instructs the tape drive to carry out the specified operation. Operations that change device defaults require superuser status (see su in Chapter 1).

## OPERATIONS

| Use This Operation | To Do This |
| :--- | :--- |
| `asf n` | Position the tape at the beginning of the nth file. |
| `bsfm n` | Go back n files and position the tape on the first block of the next file. |
| `bsf n` | Go back n files and position the tape on the last block of the previous file. |
| `bsr n` | Go backward n records. |
| `bss n` | Go backward n setmarks. This operation is for SCSI tapes only. |
| `compression` | Enable data compression if the drive supports it. |
| `datacompression n` | Set the compression status specified by n. |

## OPERATIONS (CONT.)

| Use This Operation | To Do This |
| :--- | :--- |
| `defblksize n` | Set the block size to n bytes. This operation is for SCSI drives only. |
| `defcompression compression` | Set the default compression specified by compression. This operation is for SCSI drives only. |
| `defdensity n` | Set the density specified by n. This operation is for SCSI drives only. |
| `defdrvbugger n` | Set the drive buffer code specified by n. This operation is for SCSI drives only. |
| `densities` | Display some common density codes. |
| `drvbuffer n` | Set the tape drive buffer to the value specified by n. |
| `eod`, `seed` | Go to end of valid data. |
| `erase` | Erase the tape. |
| `fsfm n` | Go forward n files and position the tape on the last block of the previous file. |
| `fsf n` | Go forward n files and position the tape on the first block of the next file. |
| `fsr n` | Go forward n records. |
| `fss n` | Go forward n setmarks. This operation is for SCSI tapes only. |
| `load` | Load the tape. This operation is for SCSI drives only. |
| `lock` | Lock the tape drive door. This operation is for SCSI drives only. |
| `mkpartition [ size ]` | When used without an argument, formats the tape with one partition. When you specify a size in megabytes, formats the tape with two partitions and makes the second partition the specified size. |
| `offline`, `rewofl` | Rewind the tape and unload. |
| `partseek n` | Set the position to the nth block in the specified partition. |
