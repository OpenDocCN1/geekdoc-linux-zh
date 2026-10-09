
When you add a line for a filesystem to the **/etc/fstab** file (page 506), you can mount that filesystem by giving the associated mount point or device name as the argument to **mount**. For example, the following command mounts a backup volume at **/backup**:

```
$ mount /backup
```

This command works because **/etc/fstab** contains the additional information needed to mount the file. A nonprivileged user is able to mount the file because of the **user** option.

```
/dev/sda7  /backup  ext4 user,noauto,rw 0 0
```

On the local system, the mount point and device name will differ from those in this example. You can specify a filesystem type of **auto** (in place of **ext4**) to cause the system to probe the filesystem to determine its type. You can also manually mount filesystems that do not appear in **/etc/fstab**. For example, you can mount a CD-ROM, filesystem type **ISO9660** (page 1256), at **/media/cd** using the following command:

```
# mount -t iso9660 /dev/cdrom /media/cd
```

## LPI MOUNT OPTIONS

The **mount** utility takes many options, which you can specify either on the command line or in the **/etc/fstab** file (page 524). For a complete list of **mount** options for local filesystems, see the **mount** man page; for remote directory hierarchies, see page 807 and the **nfs** man page.

The system mounts most filesystems specified in **fstab** when it boots. You can specify the **noauto** option to cause Linux not to mount a filesystem automatically.

### Mount removable devices with the nosuid option

- **Security**: Always mount removable devices with the **nosuid** option so a malicious user cannot, for example, put a setup copy of **bash** on a disk and have a shell with **root** privileges. By default, Fedora/RHEL uses the **nosuid** option when mounting removable media. See page 806 for more information.

Unless you specify the **user**, **users**, or **owner** option, only a user running with **root** privileges can mount and unmount a filesystem. The **user** option allows any user to mount the filesystem, but the filesystem can be unmounted only by the user who mounted it; the **users** option allows any user to mount and unmount the filesystem. These options are frequently specified for CD, DVD, and USB flash drives. The **owner** option, which is used only under special circumstances, is similar to the **user** option except that the user mounting the device must own the device.

Three options can help ensure the security of the system when you allow nonprivileged users to mount filesystems. The **noexec** option prevents a user from running an executable file on the mounted filesystem, **nosuid** forces mounted setuid and setgid executable files to run with regular permissions (no effective user or group ID change) on the mounted filesystem (page 806), and **nodev** prevents the system from recognizing a device special file on the mounted filesystem (page 806). The **user** and **users** option imply all three of these options; **owner** implies **nosuid** and **nodev**.

## mount: UNMOUNTS A FILESYSTEM

The `umount` utility unmounts a filesystem as long as it does not contain any files or directories that are in use (open). For example, a logged-in user's working directory cannot be on the filesystem you want to unmount. The next command unmounts the CD mounted earlier:

```
$ umount /media/cdrom
```

Unmount a USB flash drive or a remote (NFS) directory hierarchy the same way you would unmount a partition of a hard drive.

The `umount` utility consults `/etc/fstab` to get the necessary information and then unmounts the appropriate filesystem from its server. When a process has a file open on the filesystem you are trying to unmount, `umount` displays a message similar to the following:

```
mount: /home: device is busy
```

### When you cannot unmount a device because it is in use

When a process has a file open on a device you need to unmount, use `fuser` to determine which process has the file open and to kill it. For example, when you want to unmount a CD, give the command `fuser -ki /media/cdrom` (substitute the mount point for the diskette on the local system for `/media/cdrom`). After checking with you, this command kills the process(es) using the CD. You can also use `lsof` (page 624) to find open files.

Use the `-a` option to `umount` to unmount all mounted filesystems that are not in use. You can never unmount the filesystem mounted at `/`. You can combine `-a` with the `-t` option to unmount filesystems of a given type (e.g., `ext4` or `nfs`). For example, the following command unmounts all mounted `nfs` directory hierarchies that are not in use:

```
# umount -at nfs
```

## du: DISPLAYS DISK USAGE INFORMATION

The `du` (disk usage) utility displays estimates of file space usage. It is commonly called with the `-h` (`--human-readable`) option which causes `du` to display file sizes in kilobytes, megabytes, and gigabytes instead of blocks and with the `-s` (`--summarize`) option which causes `du` to display a total for each of its directory arguments instead of displaying the size of each file in the directory. The first of the following examples shows `du` listing the sizes of each file in the `/etc` directory (without the `-s` option); the second uses the `-s` option to cause `du` to list the size of the `/etc` directory itself. When run without `root` privileges, the examples display an error message for each file the user is not permitted to read.

```
# du -h /etc | head -4
76K     /etc/logrotate.d
12K     /etc/highlight
4.0K    /etc/terminfo
8.0K    /etc/wpa_supplicant
# du -sh /etc
37M     /etc
```

## LPI fstab: KEEPS TRACK OF FILESYSTEMS

The system administrator maintains the `/etc/fstab` file, which lists local and remote directory hierarchies, most of which the system mounts automatically when it boots. The `fstab` file has six columns; a hyphen is a placeholder for a column that has no value:

- **Name**: The name, label, or UUID number of a local block device (page 518) or a pointer to a remote directory hierarchy. When you install the system, Fedora/RHEL uses UUID numbers for fixed devices (but not for LVs). Using UUID numbers in `fstab` during installation circumvents the need for consistent device naming. Because `udev` (page 516) manages device naming dynamically, the installer might not be aware, for example, that the first disk is not named `/dev/hda1` but rather `/dev/sda1`, but it always knows the UUID number of a device. Using UUID numbers to identify devices also keeps partitions and mount points correctly correlated when you remove or exchange devices. When run with `root` privileges, `blkid` (page 464) displays device UUID numbers. See `/dev/disk/by-uuid` (page 503) for more information on UUID numbers. You can use the volume label of a local filesystem by using the form `LABEL=xx`, where `xx` is the volume label. For information on labeling devices, refer to `e2label` on page 465.
  - A remote directory hierarchy appears as `hostname:pathname`, where `hostname` is the name of the remote system that houses the filesystem, and `pathname` is the absolute pathname (on the remote system) of the directory that is to be mounted.
- **Mount point**: The name of the directory file that the filesystem/directory hierarchy is to be mounted on. If it does not already exist, create this directory using `mkdir`. See pages 38 and 521.
- **Type**: The type of filesystem/directory hierarchy that is to be mounted. Local filesystems are generally of type `ext2`, `ext4`, or `iso9660`, and remote directory hierarchies are of type `nfs` or `cifs`. Table 11-1 on page 519 lists filesystem types.
- **Mount options**: A comma-separated list of mount options, such as whether the filesystem is mounted for reading and writing (`rw`, the default) or read-only (`ro`). See pages 522 and 807 and refer to the `mount` and `nfs` man pages for lists of options.
- **Dump**: Previously used by `dump` to determine when to back up the filesystem.
- **Fck**: Specifies the order in which `fsck` checks filesystems. Root (`/`) should have a `1` in this column. Filesystems that are mounted to a directory just below the root directory should have a `2`. Filesystems that are mounted on another mounted filesystem (other than root) should have a `3`. For example,
