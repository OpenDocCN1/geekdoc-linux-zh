| Field | Contents | Description |
|---|---|---|
| 5 | Frequency | A single number that specifies if and when a file system is to be backed up with the dump command. |
| 6 | Order | A single number that specifies in what order file systems should be checked with the fsck command. |

# Viewing a List of Mounted File Systems

The mount command is used to mount file systems. Entering the command without arguments will display a list of the file systems currently mounted.

```
[me@linuxbox ~]$ mount
/dev/sda2 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda5 on /home type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
fusectl on /sys/fs/fuse/connections type fusectl (rw)
/dev/sdd1 on /media/disk type vfat (rw,nosuid,nodev,noatime,uhelper=hal,uid=500,utf8,shortname=lower)
twin4:/musicbox on /misc/musicbox type nfs4 (rw,addr=192.168.1.4)
```

The format of the listing is as follows: device on mount_point type filesystem_type (options). For example, the first line shows that device /dev/sda2 is mounted as the root file system, is of type ext4, and is both readable and writable (the option rw). This listing also has two interesting entries at the bottom of the list. The next-to-last entry shows a 2GB SD memory card in a card reader mounted at /media/disk, and the last entry is a network drive mounted at /misc/musicbox.

For our first experiment, we will work with a CD-ROM. First, let’s look at a system before a CD-ROM is inserted.

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext4 (rw)
```