
## File System Types

| Type | Description |
| :--- | :--- |
| *swap* | Linux swap partition or swap file. |
| *sysv* | Unix System V file systems. |
| *iso9660* | File system for mounting CD-ROM. |
| *proc* | Used by operating system for processes (kernel support file system). |
| *sysfs* | Used by operating system for devices (kernel support file system). |
| *usbfs* | Used by operating system for USB devices (kernel support file system). |
| *devpts* | Unix 98 Pseudo Terminals (ttys, kernel interface file system). |
| *shmfs* and *tmpfs* | Linux Virtual Memory, POSIX shared memory maintenance access (kernel interface file system). |
| *adfs* | Apple DOS file systems. |
| *affs* | Amiga fast file systems. |
| *ramfs* | RAM-based file systems. |
| *udf* | Universal Disk Format used on CD/DVD-ROMs. |
| *ufs* | Unix File System, found on Unix system (older format). |

**TABLE 30-7** File System Types

The next example shows an entry for the main Linux hard disk partition. This entry is mounted at the root directory, /, and has a file type of ext3:

```
/dev/sda3 / ext3 defaults 0 1
```

The following example shows a **LABEL** entry for the hard disk partition, where the label name is /:

```
LABEL=/ / ext3 defaults 0 1
```

## Auto Mounts

The file system type for a floppy may differ depending on the disk you are trying to mount. For example, you may want to read a Windows-formatted floppy disk at one time and a Linux-formatted floppy disk at another time. For this reason, the file system type specified for the floppy device is **auto**. With this option, the type of file system formatted on the floppy disk is detected automatically, and the appropriate file system type is used.

```
/dev/fd0 /media/floppy auto defaults,noauto 0 0
```

## mount Options

The field after the file system type lists the different options for mounting the file system. The default set of options is specified by **defaults**, and specific options are listed next to each other separated by a comma (no spaces). The **defaults** option specifies that a device is read/ write (**rw**), that it is asynchronous (**async**), that it is a block device (**dev**), that it cannot be mounted by ordinary users (**nous**), and that programs can be executed on it (**exec**).

Removable devices like your CD-ROMS and floppy disks are now managed by **HAL**, the Hardware Abstraction Layer. HAL uses its own configuration files to set the options for these devices. You can place your own entries in the `/etc/fstab` file for CD-ROMs to bypass HAL. This will, however, no longer let your CD-ROMs and DVD-ROMs be automatically detected.

In a manual configuration, a CD-ROM should have **ro** and **noauto** options. **ro** specifies that the device is read-only, and **noauto** specifies it is not automatically mounted. The **noauto** option is used with both CD-ROMs and floppy drives, so they won't automatically mount, because you don't know if you have anything in them when you start up. At the same time, the HAL entries for both the CD-ROM and the floppy drive can specify where they are to be mounted when you decide to mount them. The **owner** option is a more secure option used in place of the user option. The **owner** option will only allow the owner of the device to mount or unmount the device, instead of just any user, as the user option does. The **fscontext** option is used by SELinux as discussed in Chapter 17. Table 30-8 lists the options for mounting a file system. An example of a hard drive entry follows:

```
/dev/VolGroup0/LogVol00 / ext3 defaults 1 1
```

## Boot and Disk Check

The last two fields of an **fstab** entry consist of integer values. The first one is used by the **dump** command to determine if a file system needs to be dumped, backing up the file system. The second value is used by **fsck** to see if a file system should be checked at reboot, and in what order with other file systems. If the field has a value of 1, it indicates a boot partition, and 2 indicates other partitions. The 0 value means **fsck** needn't check the file system.

## fstab Sample

A copy of an `/etc/fstab` file is shown here. Notice the first line is a comment. All comment lines begin with a #. The entries for `/proc` and `/sys` file systems are special entries used by your Linux operating system for managing its processes and devices; they are not actual devices. To make an entry in the `/etc/fstab` file, you can edit the `/etc/fstab` file directly. You can use the example `/etc/fstab` file shown here as a guide to show how your entries should look. The `/proc` and `swap` partition entries are particularly critical.

**/etc/fstab**

| File System | Mount Point | Type | Options | Dump | Pass |
|---|---|---|---|---|---|
| /dev/sda3 | / | ext3 | defaults | 1 | 1 |
| LABEL=/boot | /boot | ext3 | defaults | 1 | 2 |
| tmpfs | /dev/shm | tmpfs | defaults | 0 | 0 |
| devpts | /dev/pts | devpts | gid=5, mode=620 | 0 | 0 |
| sysfs | /sys | sysfs | defaults | 0 | 0 |
| proc | /proc | proc | defaults | 0 | 0 |
| /dev/sda3 | swap | swap | defaults | 0 | 0 |
| /dev/sda1 | /media/win | ntfs-3g | defaults,ro,locale=en_US.UTF-8 | 0 | 0 |

## Mount Options for File Systems

| Option | Description |
| --- | --- |
| async | Indicates that all I/O to the file system should be done asynchronously. |
| auto | Indicates that the file system can be mounted with the -a option. A mount -a command executed when the system boots, in effect, mounts file systems automatically. |
| defaults | Uses default options: rw, suid, dev, exec, auto, nouser, and async. |
| dev | Interprets character or block special devices on the file system. |
| fscontext | Sets SELinux file system context. |
| noauto | Indicates that the file system can only be mounted explicitly. The -a option does not cause the file system to be mounted. |
| exec | Permits execution of binaries. |
| managed | Removable device that is managed by HAL. Options for this device have to be specified in the HAL configuration files. |
| nouser | Forbids an ordinary (that is, nonroot) user to mount the file system. |
| owner | Allows only the owner to mount or unmount the device. |
| remount | Attempts to remount an already-mounted file system. This is commonly used to change the mount flags for a file system, especially to make a read-only file system wrtable. |
| ro | Mounts the file system as read-only. |
| rw | Mounts the file system as read/write. |
| suid | Allows set-user-identifier or set-group-identifier bits to take effect. |
| sync | Indicates that all I/O to the file system should be done synchronously. |
| user | Enables an ordinary user to mount the file system. Ordinary users always have the following options activated: noexec, nosuid, and nodev. |
| nodev | Does not interpret character or block special devices on the file system. |
| noexec | Does not allow execution of binaries on the mounted file systems. |
| nosuid | Does not allow set-user-identifier or set-group-identifier bits to take effect. |

**Table 30-8** Mount Options for File Systems

## Partition Labels: e2label

Red Hat Enterprise Linux and Fedora use file system labels for ext2 and ext3 file systems on hard disk partitions. Thus in the /etc/fstab file previously shown, the first entry would use a label for its device name, as shown here. In this case, the label is the slash, /, indicating the root partition. You could change this device's label with e2label, but be sure to also change the /etc/fstab entry for it.

```
LABEL=/ / ext3 defaults 0 1
```

For ext2 and ext3 partitions, you can change or add a label with the `e2label` tool or `tune2fs` with the `-L` option. Specify the device and the label name. If you change a label, be sure to change corresponding entries in the `/etc/fstab` file. Just use `e2label` with the device name to find out what the current label is. In the next example, the user changes the label of the `/dev/sda3` device to `TURTLE`:

```
e2label /dev/sda3 TURTLE
```

## Windows Partitions

You can mount MS-DOS; Windows 95/98/ME; or Windows XP, NT, and 2000 partitions used by your Windows operating system onto your Linux file structure, just as you would mount any Linux file system. You have to specify the file type of `vfat` for Windows 95/98/ME, and `msdos` for MS-DOS. Windows XP, NT, and 2000 use either the ntfs-3g or the `ntfs` file types. You may find it convenient to have your Windows partitions automatically mounted when you start up your Linux system. To do this, you need to put an entry for your Windows partitions in your `/etc/fstab` file and give it the `defaults` option, or be sure to include an `auto` option. You make an entry for each Windows partition you want to mount, and then specify the device name for that partition, followed by the directory in which you want to mount it. The `/mnt/windows` directory would be a logical choice (be sure the windows directory has already been created in `/mnt`). The next example shows a standard Windows partition entry for an `/etc/fstab` file. Notice the last entry in the `/etc/fstab` file example is an entry for mounting a Windows partition.

```
/dev/sda1 /mnt/windows vfat defaults 0 0
```

The `ntfs-3g` drivers will provide both write and read support for NTFS file systems used for Windows XP, NT, and 2000. You would specify the `ntfs-3g` type. Be sure to have already installed the ntfs-3g package from Fedora (see Chapter 3). If you use the `ntfs-3g` NTFS Configuration Tool to configure your NTFS access, then entries for your NTFS partitions will automatically be placed in the `/etc/fstab` file. Notice the example, the partition is mounted as read only (`ro`) with the locale specified as US (`locale`).

```
/dev/sda1 /mnt/win ntfs-3g defaults,ro,locale=en_US.UTF-8 0 0
```

For the original NTFS Linux drivers (Linux NTFS Project), you would specify the `ntfs` type. This has to be downloaded separately from `livna.org`. Be sure to have already downloaded and installed the NTFS kernel module (see Chapter 3). The `ntfs` kernel module from `ntfs.org` is read only.

```
/dev/sda2 /mnt/windows ntfs ro,umask=0222 0 0
```

## Linux Kernel Interfaces

Your `/etc/fstab` file may also have entries for two special kernel interface file systems, `devpts` and `tmpfs`. Both provide kernel interfaces that are not supported by standard devices. The `/dev/pts` entry mounts a `devpts` file system for pseudoterminals. The `/dev/shm` entry mounts the `tmpfs` file system (also known as `shmfs`) to implement Linux Virtual Memory, POSIX shared memory maintenance access. This is designed to overcome the 4 GB memory limitation on current systems, extending usable memory to 64 GB.
