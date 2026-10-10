| User | used | Block limits |  |  | File limits |  |  |
|---|---|---|---|---|---|---|---|
|  |  | soft | hard | grace | used | soft | hard |
| root | 6420573 | 0 | 0 |  | 376520 | 0 | 0 |
| daemon | 8 | 0 | 0 |  | 3 | 0 | 0 |
| lp | 4 | 0 | 0 |  | 1 | 0 | 0 |
| polkitd | 8 | 0 | 0 |  | 2 | 0 | 0 |
| abrt | 24 | 0 | 0 |  | 4 | 0 | 0 |
| colord | 20 | 0 | 0 |  | 4 | 0 | 0 |
| geoclue | 4 | 0 | 0 |  | 1 | 0 | 0 |
| chrony | 12 | 0 | 0 |  | 3 | 0 | 0 |
| tss | 12 | 0 | 0 |  | 2 | 0 | 0 |
| unbound | 8 | 0 | 0 |  | 2 | 0 | 0 |
| pulse | 4 | 0 | 0 |  | 1 | 0 | 0 |
| gdm | 128 | 0 | 0 |  | 32 | 0 | 0 |
| user1 | 1188 | 18432 | 20480 |  | 326 | 900 | 1000 |

```
[root@server1 ~]# _
```

Note that most users in the preceding output are system users and do not have quotas applied to them. These users are discussed in Chapter 10.

The aforementioned commands are only available to the root user; however, regular users can view their own quota using the **quota** command. The root user can also use the quota command but can also use it to view quotas of other users:

```
[root@server1 ~]# **quota**
Disk quotas for user root (uid 0): none

[root@server1 ~]# **quota -u user1**
Disk quotas for user user1 (uid 500):
Filesystem blocks quota limit grace files quota limit grace
/dev/mapper/vg00-data
    1188 18432 20480
             326   900  1000

[root@server1 ~]# _
```

# ## Chapter Summary

+   ■ Disk devices are represented by device files that reside in the /dev directory. These device files specify the type of data transfer, the major number of the device driver in the Linux kernel, and the minor number of the specific device.
+   
+   ■ Each disk device must contain a filesystem, which is then mounted to the Linux directory tree for usage using the mount command. The filesystem can later be unmounted using the umount command. The directory used to mount the device must not be in use by any logged-in users for mounting and unmounting to take place.
+   
+   ■ Hard disks must be partitioned into distinct sections before filesystems are created on those partitions. To partition a hard disk with an MBR, you can use the fdisk, cfdisk, or parted command. To partition a hard disk with a GPT, you can use the fdisk or parted command.