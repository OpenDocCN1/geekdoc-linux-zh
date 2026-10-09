Relative mount point | The first column of a map file holds the absolute or relative autofs mount point. A pathname other than /— appearing in the first column of auto.master specifies a relative autofs mount point. A relative mount point is appended to the corresponding autofs mount point from column 1 of the auto.master. In this example, public (from auto.plum) is appended to /plum (from auto.master) to form /plum/public.

Absolute mount point | A /— appearing in the first column of auto.master specifies an absolute autofs mount point. In this example, auto.master specifies /— as the mount point for the auto.misc map file, so the mount points specified in this map file are absolute and are specified entirely in an auto.misc map file. The auto.misc file specifies the autofs mount points /music and /home/zach.

The second column holds autofs options, and the third column shows the server and directory hierarchy to be mounted.

The auto.misc file specifies a local filesystem (/dev/mapper/vg_guava-music; an LV (page 44)) and a remote NFS directory (plum/home/zach). You can identify a local directory hierarchy by the absence of a system name before the colon and usually the ext4 filesystem type. A system name appears before the colon of a remote directory hierarchy filesystem and the filesystem type is always nfs4.

Before the new setup can work, you must restart the autofs service (page 821). This process creates the directories that hold the mount points if necessary.

The following example starts with the automount daemon (autofs service) not running. The first ls command shows that the /music and /plum directories are empty. The next command, run with root privileges, starts the autofs service. Now when you list /music, autofs mounts it and ls displays its contents. The /plum listing shows nothing: It is not an autofs mount point.

```
```bash
$ ls /music /plum
/music:
/plum:
```
```bash
$ su -c 'systemctl start autofs.service'
```
```bash
$ ls /music /plum
/music:
lost+found mp3 ogg
/plum:
```
```bash
$ ls /plum/public
memos personal
$ ls /plum
public
```
```

When you give an ls command and specify the mount point (/plum/public), automount mounts it and ls displays its contents. Once public is mounted on /plum, ls /plum shows the public directory is in place.