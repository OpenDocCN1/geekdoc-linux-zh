The **auto** option in the file system column for the floppy probes the superblock for the device to attempt identification of the file system type. This works for nearly any other file system type, including `ext2`, `ext3`, `iso9660`, `vfat`, and `ntfs` to name a few.

Notice also the mutually exclusive `user` and `users` options in the floppy and CD-ROM entries' options column. These enable either exclusive or nonexclusive mounting for users on that device.

For example, if the `user` option is present for the system's CD-ROM and the daytime user Sally mounts her favorite Spice Girls release into the drive and plays it, only user Sally (and the root user) can unmount that CD-ROM.

This is unacceptable to Steven the night shift operator, who simply must have his *Tenacious D* CD-ROM to help the night pass. Steven should request that the root user switch that option with the `users` option, which allows any user to mount the device and any other user to unmount it.

# # Manually Mounting File Systems

If a file system isn't configured in the `/etc/fstab` file, it can be mounted manually following this convention:

```
mount -t type -o option device mountpoint
```

The following example of a manual mount includes the type, the option, the device, and a mount point:

```
mount -t iso9660 -o exec /dev/cdrom /mnt/cdrom
```

With this `mount` command, the system's CD-ROM is mounted, allowing user access.

Mounting options that are important include

+   - `—a`—Mounts all file systems listed in `/etc/fstab`
+   - `—f`—Fakes the mounting of file systems
+   - `—r`—Mounts the file system read-only
+   - `—w`—Mounts the file system in write mode
+   - `—n`—Mounts without updating `/etc/mtab`
+   - `—L`—Mounts a file system with a given label, instead of using the device filename