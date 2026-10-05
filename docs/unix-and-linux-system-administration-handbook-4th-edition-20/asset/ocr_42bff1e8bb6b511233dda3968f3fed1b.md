# Setup for automatic mounting

By default, ZFS filesystems mount themselves automatically and do not require vstab entries. However, you can change this behavior by setting ZFS filesystem properties. Swap areas and nonfilesym mounts should still appear in vstab.

![](bbox=[0.173, 0.116, 0.251, 0.149])

mount, umount, swapon, and fsck read all the filesystem catalog, as it is helpful if the data presented there is correct and complete. mount and use the catalog to figure out what you want done if you specify only a partition name or mount point on the command line. For example, with the Linux vstab configuration on page 262, the command

```
$ sudo mount /media/cdrom0
```

would have the same effect as typing

```
$ sudo mount -t udf -o user,noauto,exec,utf8 /dev/scd0 /media/cdrom0
```

The command mount -a all regular filesystems listed in the filesystem catalog; it is usually executed from the startup scripts at boot time.20 The -t, -F, or -v flag (-F for Solaris and HP-UX, -v for AIX) with a f argument constraints the operation to filesystems of a certain type. For example,

```
$ sudo mount -ext4
```

mount all local ext4 filesystems. The mount command reads vstab sequentially. Therefore, filesystems that are mounted beneath other filesystems must follow their parent partitions in the vstab file. For example, for /var/log must follow the line for /var if /var is a separate filesystem.

The command for unmounting filesystems accepts a similar syntax. You cannot mount a filesystem that a process is using as its current directory or which files are open. There are commands to identify the processes that are interfering with your ummount attempt; see page 144.

![](bbox=[0.193, 0.638, 0.246, 0.672])

The HP UX vstab file is the most traditional of our examples. Here are entries for a system that has only one volume group:

| Device | Mount point | Type | Options | | |
|---|---|---|---|---||
| /dev/vg00/vol3/ | | vxfs | delayog | 0 1 |
| /dev/vg00/vol1/stand | | vxfs | tranflush | 0 1 |
| /dev/vg00/vol4/tmp | | vxfs | delayog | 0 2 |
| /dev/vg00/vol5/home | | vxfs | delayog | 0 2 |
| /dev/vg00/vol6/opt | | vxfs | delayog | 0 2 |
| /dev/vg00/vol7/usr | | vxfs | delayog | 0 2 |
| /dev/vg00/vol8/var | | vxfs | delayog | 0 2 |

There are six fields per line, separated by whitespace. Each line describes a filesystem. The fields are traditionally aligned for readability, but alignment is not required.

2. The noauto mount option excludes a given filesystem from automatic mounting by mount -a.