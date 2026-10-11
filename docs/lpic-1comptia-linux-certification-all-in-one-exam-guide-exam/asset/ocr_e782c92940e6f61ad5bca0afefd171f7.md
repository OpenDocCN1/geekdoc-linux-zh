On some distributions, it's also the default location for mounting removable devices as well. Other distributions, such as OpenSUSE and newer versions of Fedora, use /media as the default location for mounting removable media.

You can also use the -o option with the mount command to include a variety of mounting options with the command. For example, you could use -ro to mount the partition as read-only. See the man page for mount for a complete listing of all the available options.

![](bbox=[0.05, 0.22, 0.12, 0.31])

> **TIP** One of the things I love about the mount command is the fact that it can be used to mount an ISO image in the file system, allowing you to access the files within it without burning it to an optical disc first. The syntax is mount -o loop filename.iso mount_point.

After mounting the partition, you can use the mount command with no switches to view all mounted file systems, as shown here:

```
ws1:~ # mount
/dev/sda3 on / type ext4 (rw, acl, user xattr)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
debugfs on /sys/kernel/debug type debugfs (rw)
devtmpfs on /dev type devtmpfs (rw, mode=0755)
tmpfs on /dev/shm type tmpfs (rw, mode=1777)
devpts /dev/pts type devpts (rw, mode=0620, gid=5)
/dev/sda1 /boot type ext4 (rw, acl, user xattr)
/dev/sda4 /var type ext4 (rw, acl, user xattr)
securityfs /sys/kernel/security type securityfs (rw)
none on /proc/fs/vmblock/mountPoint type vmblck (rw)
fusectl on /sys/fs/fuse/connections type fusectl (rw)
gvfs -fuse-daemon /home/tux/.gvfs type fuse. gvfs =fuse-daemon
(rw, nosuid, nodev, user-tux)
/dev/sdb1 /mnt/extraspace type ext4 (rw)
ws1:~ #
```

If you look at the last line of the output from mount, you’ll see that /dev/sdb1 is mounted on /mnt/extraspace and uses the ext4 file system.

In addition, whenever you mount or unmount a partition, the /etc/mtab file is updated with a list of mounted file systems. You can view this file as well to see a list of mounted file systems, as you can see in this example:

```
ws1:~ $ cat /etc/mtab
/dev/sda3 / ext4 rw, acl, user_xattr 0 0
proc /proc proc rw 0 0
sysfs /sys sysfs rw 0 0
debugfs /sys/kernel/debug debugfs rw 0 0
devtmpfs /dev devtmpfs rw, mode=0755 0 0
tmpfs /dev/shm tmpfs rw, mode=1777 0 0
devpts /dev/pts devpts rw, mode=0620, gid=5 0 0
/dev/sda1 /boot ext4 rw, acl, user_xattr 0 0
/dev/sda4 /var ext4 rw, acl, user_xattr 0 0
securityfs /sys/kernel/security securityfs rw 0 0
none /proc/fs/vmblock/mountPoint vmblck rw 0 0
fusectl /sys/fs/fuse/connections fusectl rw 0 0
gvfs -fuse-daemon /home/tux/.gvfs fuse. gvfs =fuse-daemon
rw, nosuid, nodev, user-tux 0 0
/dev/sdb1 /mnt/extraspace ext4 rw 0 0
ws1:~ $
```