# **Chapter 4: More Bash Shell Commands**

> **NOTE**
> Most USB memory sticks are formatted using the vfat filesystem. If you need to mount a data CD or DVD, you'll have to use the iso9660 filesystem type.

The next two parameters define the location of the device file for the media device and the location in the virtual directory for the mount point. For example, to manually mount the USB memory stick at device `/dev/sdb1` at location `/media/disk`, you'd use the following command:

```
mount -t vfat /dev/sdb1 /media/disk
```

Once a media device is mounted in the virtual directory, the root user will have full access to the device, but access by other users will be restricted. You can control who has access to the device using directory permissions (discussed in Chapter 7, "Understanding Linux File Permissions").

In case you need to use some of the more exotic features of the mount command, the available parameters are shown in Table 4.5.

TABLE 4.5 **The mount Command Parameters**
| Parameter | Description |
| :-------- | :---------- |
| `-a` | Mount all filesystems specified in the `/etc/fstab` file. |
| `-f` | Causes the mount command to simulate mounting a device but not actually mount it. |
| `-F` | When used with the `-a` parameter, mount all filesystems at the same time. |
| `-v` | Verbose mode; explains all the steps required to mount the device. |
| `-i` | Don't use any filesystem helper files under `/sbin/mount.\*filesystem`. |
| `-l` | Add the filesystem labels automatically for ext2, ext3, ext4, or XFS filesystems. |
| `-n` | Mount the device without registering it in the `/etc/mtab` mounted device file. |
| `-p num` | For encrypted mounting, reads the passphrase from the file descriptor num. |
| `-s` | Ignore any mount options not supported by the filesystem. |
| `-r` | Mount the device as read-only. |
| `-w` | Mount the device as read-write (the default). |
| `-L label` | Mount the device with the specified label. |
| `-U uuid` | Mount the device with the specified uuid. |
| `-O` | When used with the `-a` parameter, limit the set of filesystems applied. |
| `-o` | Add specific options to the filesystem. |