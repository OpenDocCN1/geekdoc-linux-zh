special /proc filesystem (page 497), which maps useful Linux kernel information to a pseudodirectory. This section covers mounting local filesystems; refer to page 773 for information using NFS to mount remote directory hierarchies. /dev on page 488 for information on device names.

The mount point for the filesystem/directory hierarchy that you are mounting is a directory in the local filesystem. This directory must exist before you mount a filesystem; its contents disappear as long as a filesystem is mounted on and it reappear when you unmount the filesystem. See page 35 for a discussion of mount points.

Without any arguments, mount lists the currently mounted filesystems, showing the physical device holding each filesystem, the mount point, the type of filesystem, and any options when each filesystem was mounted. The mount utility gets this information from the /etc/mtstab file (page 494).

# $ mount

```
/dev/sda1 /dev type ext4 (rw,errors=remount-ro)
proc /proc type proc (rw,noexec,nosuisid,nodev)
...
/dev/sda2 /home type ext4 (rw)
/dev/sda5 /p15 type ext4 (rw)
/dev/sda6 /p16 type ext4 (rw)
/dev/sda1 /p01 type ext4 (rw)
/jam/c on /jam/c type cifs (rw,mand)
dp/pg04 /p04 type nfs (rw,addr=192.168.0.12)
/dev/hdb /media/cdrom0 type iso9660 (rw,noexec,nosuisid,nodev,user=sam)
```

The first entry in the example shows the root filesystem, which is mounted on /. The second entry shows the /proc pseudofsystem (page 497). The next four entries identify disk partitions standard Linux ext4 filesystems. The directory /jam/c has a cifs (Windows) filesystem mounted on it using Samba. You can use Linux utilities and applications to access the Windows files and directories. The line starting with dog shows a mounted, remote NFS filesystem. The last line shows the CD at /dev/hdb mounted on /media/cdrom0.

If the list of filesystems in /etc/mtstab is not correct, see the tip on page 494.

# Do not mount anything on root (/)

caution Always mount root directory hierarchy and removable devices at one level below the root level of the filesystem. The root filesystem is mounted on /. you cannot mount two filesystems in the same place. If you were to try to mount something on /, all files, directories, and filesystems that were under the root directory no longer be available, and the system would crash.

When you add a line for a filesystem to the /etc/fstab file (page 492), you can mount that filesystem by giving the associated point point or device name as argument to mount. For example, the CD earlier was mounted using the following command:

```
$ mount /media/cdrom0
```