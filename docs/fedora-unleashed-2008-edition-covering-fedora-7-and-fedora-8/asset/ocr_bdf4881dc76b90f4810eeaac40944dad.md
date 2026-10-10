# The umount Command

To unmount a file system, use the `umount` command with the following syntax:

```
umount mount_point
```

You can also unmount by device name:

```
umount device_name
```

> **CAUTION**
> Do not use `umount -a` to unmount everything that the system does not require to run (or is not currently using). Unmounting *everything* is a particularly bad idea on a multi-user, networked system because your users are certain to lose access to some or all of their files. So, as any good sysadmin will tell you, do not do that.

# Mounting Automatically with `/etc/fstab`

A special file, `/etc/fstab`, exists to provide the system with predetermined options and mount points so that the file systems can be automatically or manually mounted with minimal typing and without having to recall arcane Linux syntax.

The `/etc/fstab` file can only be written to by the super-user. The commands `fsck`, `mount`, and `umount` all read information from `/etc/fstab`. Each file system gets its own line with the information separated by tabs.

On each line of `fstab`, the first field indicates the block device or remote file system that will be mounted. The second field identifies the mount point on the local system where the file system will be mounted. The third field is the file system type, and the fourth field is a comma-delimited list of mount options. Options include:

+   ► `exec`—If this option is specified, binaries can be executed from this file system.

+   ► `noauto`—This means that the `-a` option does not cause the file system to be mounted and it is not mounted at bootup.

+   ► `noexec`—If this option is specified, binaries cannot be executed from this file system.

+   ► `nosuid`—This option does not permit `set_user_identifier` or `set_group_identifier` bits to take effect.

+   ► `ro`—This option mounts the file system as read-only.

+   ► `rw`—This option mounts the file system as read/write.

+   ► `sync`—Reading from and writing to the files are done synchronously.

+   ► `user`—This option allows a regular (not just root) user to mount the file system, but it includes the options `noexec`, `nosuid`, and `nodev` by default unless they are overridden by `exec`, `dev`, and `suid`.