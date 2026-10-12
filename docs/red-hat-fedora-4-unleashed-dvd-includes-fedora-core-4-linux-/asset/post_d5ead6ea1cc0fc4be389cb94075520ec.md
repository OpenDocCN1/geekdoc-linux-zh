
> The latter two options in the arguments list are mutually exclusive.

To select the ext3 journaling mode, you must add the appropriate entry in `/etc/fstab`. Because the ext3 file system is a new version of the ext2 file system with journaling added, it supports the same options as ext2, as well as the following additions:

- **no`load`**—This option disables the ext3 file system’s journal when mounting; it becomes an ext2 file system.
- **`data=journal / data=ordered / data=writeback`**—This option specifies the journaling mode; “ordered” is the default. Metadata is always journaled.
  - **`journal`**—The slowest, but most secure mode because all the data is written to the journal before it is written to the regular file system.
  - **`ordered`**—This is the default mode in which all data is written to the main file system prior to its metadata being committed to the journal.
  - **`writeback`**—With this option, data can be written into the main file system after its metadata has been committed to the journal. This option enables old data to appear in files after a crash and journal recovery, but it is the fastest option.

## Using `mkreiserfs`

The Reiser file system journals file data and handles smaller files more efficiently than the ext3 file system. Although it is suitable for use as the root file system, Fedora Core does not officially support its use in that way. You use the `mkreiserfs` command to create a Reiser file system. The default values for `mkreiserfs` work well. To create a Reiser file system, use

```bash
# mkreiserfs device
```

## Creating a DOS File System with `mkdosfs`

It is possible to create DOS file systems without owning any Microsoft software using the `mkdosfs` command. To create a DOS file system in an image file, use the `-C` option. The `-n` option allows you to specify a volume label. To create a 1.4M DOS file system as an image file with the label `dosfloppy`, the sector size (`-S`) should be 512 and the block count should be 1440. Use the `-v` option to provide verbose output so that we can observe what happens.

```bash
# mkdosfs -n dosfloppy -v -C floppy.img -S 512 1440
```

> To create a DOS file system on a floppy disk drive, use `# fdformat device`.

A complete review of all the argument options and syntax for creating a DOS file system can be found in man mkdosfs. The new file system must be mounted (as described in the following section) and then formatted with the mformat command.

## Mounting File Systems

File Systems in Unix are very flexible in that they need not be physically present on your computer; you can have network access to other file systems on other machines. The Linux file system structure (the Virtual File System we spoke of at the beginning of the chapter) makes it appear as if all the file systems, regardless of type and location, are local and mounted somewhere under the root file system. As the system administrator, you decide what file systems are to be made available and where they will be attached, or mounted, to the root file system. The standard arrangement of the file system tree is that installed by default by Fedora Core Linux. The source of that standard arrangement is found in the File System Hierarchy Standards. Although a detailed discussion of those standards is beyond the scope of this section, they can be examined at http://www.pathname.com/fhs/. In this section, you learn how to mount file systems to the root file system and add file systems to the system, and you learn the traditional mount points of commonly used file systems as well.

In Linux (and its Unix cousins), all file systems—whether local, remote, images on a disk, or in memory—are mounted on a single point known as root (which is not the same as the root operator, also known as the superuser). This mount point is written as a forward slash, /, which is read and pronounced "root." The resulting file directory hierarchy all starts from / . Once mounted, the physical location of the files is unimportant because they all appear to be local.

Even if the file systems are different (FAT, ext2, HPFS, ntfs, and so on), the Linux kernel modules and the VFS make them all appear as part of the directory tree as native files. Listing the file systems as native files obviates the need for any applications to be aware of the physical location of the file or the true nature of the native file system. As a result, programming these applications is simplified because the applications only have to work with what they think are local, native files.

Any file system can be mounted anywhere, but some places are more traditional than others. Removable media devices are traditionally mounted under the /mnt directory (for example, floppy drives on /mnt/floppy and CD-ROM drives on /mnt/cdrom). The /mnt directory is the traditional place to mount removable or remote file systems that are unrelated to the local system directories that branch from the root mount point.

### The mount Command

File systems are mounted with the mount command and unmounted, curiously enough, with the umount command.

During the installation, you have the opportunity to decide where and how your partitions will be mounted. You indicate your choices, and Fedora Core automatically stores them in /etc/fstab, the File System Table, for you. The mount command looks at /etc/fstab and mounts the file system according to those set preferences. You learn more about the File System Table later in this section.

The syntax for mount is

```bash
mount -t type file_system_to_be_mounted mount_point
```

Here are the components of the mount command, and a brief explanation of each:

- **type**—Always preceded by the -t argument and followed by a space, and then the type of file system you are mounting. Typical file systems types are: ext2, ext3, vfat, iso9660, hpfs, hfs, ntfs, and others. For many file systems, mount can detect what type they are automatically, and the -t argument is superfluous (and is replaced with auto).
- **file system_to_be mounted** (as represented by the partition on which it resides)—This is the device name of the file system you want to mount, typically in the form of /dev/hdx, /dev/scx, or /dev/fdx.
- **mount_point**—The place in the directory tree where you want to mount the file system. Curiously, you can mount a file system over part of an existing file system. For example, if you have an existing directory at /foo with a single file named bar, and you mount a file system at /foo that includes a file named snafu, a listing of the directory /foo will not show the file bar, but only the file snafu. To show both files is a feature called transparency, which unfortunately is not in the current Linux repertoire.

The only real restriction to "mount anything anywhere" is that the critical system files in /bin, /etc, /lib, /dev, /proc, and /tmp need to be accessed at bootup, which typically means that they need to be on the same physical disk. If they cannot be accessed at bootup, Linux will not load and run.

Here are a few examples of using the mount command:

- Mounting a floppy:
  ```bash
  # mount -t vfat /dev/fd0 /mnt/floppy
  ```
- Mounting a CD-ROM:
  ```bash
  # mount -t iso9660 /dev/scd0 /mnt/cdrom
  ```
- Mounting a Network File System (NFS) volume:
  ```bash
  # mount -t nfs remote_host:/dir [options] mount_point
  ```

Numerous mount options exist. These options are used primarily in the /etc/fstab file. You can invoke a mount option by preceding it (or a comma-delimited string of options) with the -o switch. The mount options are listed in the fstab section of this chapter.

### The umount Command

To unmount a file system, use the umount command with the following syntax:

```bash
umount mount_point
```

You can also unmount by device name:

```bash
umount device_name
```

> **CAUTION**
>
> Do not use umount -a to unmount everything that the system does not require to run (or is not currently using). Unmounting *everything* is a particularly bad idea on a multiuser, networked system because your users will undoubtedly lose access to some or all their files. So, as any good sysadmin will tell you, do not do that.

### Mounting Automatically with /etc/fstab

A special file, /etc/fstab, exists to provide the system with predetermined options and mount points so that the file systems can be automatically or manually mounted with minimal typing and without having to recall arcane Linux syntax.

The /etc/fstab file can only be written to by the superuser. The commands fsk, mount, and umount all read information from /etc/fstab. Each file system gets its own line with the information separated by tabs.

On each line of fstab, the first field indicates the block device or remote file system that will be mounted. The second field identifies the mount point on the local system where the file system will be mounted. The third field is the file system type, and the fourth field is a comma-delimited list of mount options. Options include

- **exec**—If this option is specified, binaries can be executed from this file system.
- **noauto**—This means that the -a option will not cause the file system to be mounted and it will not be mounted at bootup.
- **noexec**—If this option is specified, binaries cannot be executed from this file system.
- **nosuid**—This option does not permit set-user-identifier or set-group-identifier bits to take effect.
- **ro**—This option mounts the file system as read-only.
- **rw**—This option mounts the file system as read/write.
- **sync**—Reading from and writing to the files are done synchronously.
- **user**—This option allows a regular (not just root) user to mount the file system, but it includes the options noexec, nosuid, and nodev by default unless they are overridden by exec, dev, and suid.
