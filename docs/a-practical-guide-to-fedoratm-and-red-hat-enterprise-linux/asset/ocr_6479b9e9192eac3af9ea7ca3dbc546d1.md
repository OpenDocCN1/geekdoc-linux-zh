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

# LPI MOUNT OPTIONS

The **mount** utility takes many options, which you can specify either on the command line or in the **/etc/fstab** file (page 524). For a complete list of **mount** options for local filesystems, see the **mount** man page; for remote directory hierarchies, see page 807 and the **nfs** man page.

The system mounts most filesystems specified in **fstab** when it boots. You can specify the **noauto** option to cause Linux not to mount a filesystem automatically.

# Mount removable devices with the nosuid option

security Always mount removable devices with the **nosuid** option so a malicious user cannot, for example, put a setup copy of **bash** on a disk and have a shell with **root** privileges. By default, Fedora/RHEL uses the **nosuid** option when mounting removable media. See page 806 for more information.

Unless you specify the **user**, **users**, or **owner** option, only a user running with **root** privileges can mount and unmount a filesystem. The **user** option allows any user to mount the filesystem, but the filesystem can be unmounted only by the user who mounted it; the **users** option allows any user to mount and unmount the filesystem. These options are frequently specified for CD, DVD, and USB flash drives. The **owner** option, which is used only under special circumstances, is similar to the **user** option except that the user mounting the device must own the device.

Three options can help ensure the security of the system when you allow nonprivileged users to mount filesystems. The **noexec** option prevents a user from running an executable file on the mounted filesystem, **nosuid** forces mounted setuid and setgid executable files to run with regular permissions (no effective user or group ID change) on the mounted filesystem (page 806), and **nodev** prevents the system from recognizing a device special file on the mounted filesystem (page 806). The **user** and **users** option imply all three of these options; **owner** implies **nosuid** and **nodev**.