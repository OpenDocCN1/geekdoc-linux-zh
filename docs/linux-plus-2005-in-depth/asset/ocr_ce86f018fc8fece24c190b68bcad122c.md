If there are several users on a Linux system, there must be enough hard disk space to support the files that each user is expected to store on the hard disk. However, if hard disk space is limited or company policy limits disk usage, you should impose limits on filesystem usage. These restrictions are called **hard disk quotas**, and can be applied to users or groups of users. Furthermore, **quotas** can restrict how many files and directories a user can create (that is, restrict the number of inodes created) on a particular filesystem, or the total size of all files that a user can own on a filesystem. Two types of quota limits are available: soft limits and hard limits. **Soft limits** allow the user to extend them for a certain period of time (seven days by default), whereas **hard limits** are rigid and prevent the user from going past them. Quotas are typically enabled at boot time if there are quota entries in `/etc/fstab`, but can also be turned on and off afterward by using the `quotaon` and `quotaoﬀ` commands, respectively.

To set up quotas for the `/` filesystem and restrict the user user1, you can carry out the following steps:

+   1.  Edit the `/etc/fstab` file to add the `usrquota` and `grpquota` mount options for the `/` filesystem. The resulting `/etc/fstab` file should look like the following:

```
```
[root@server1 root]# cat /etc/fstab
LABEL=/              /                 ext3    defaults,usrquota,grpquota 1 1
none                 /dev/pts          devpts  gid=5,mode=620             0 0
none                 /proc             proc    defaults                   0 0
none                 /sys              sysfs   defaults                   0 0
none                 /dev/shm          tmpfs   defaults                   0 0
/dev/hdc2            swap              swap    defaults                   0 0
/dev/cdrom           /mnt/cdrom        iso9660 noauto,owner,kudzu,ro      0 0
/dev/fd0             /mnt/floppy       auto    noauto,owner,kudzu         0 0
[root@server1 root]# _
```
```

+   2.  Remount the root filesystem as read-write to update the system with the new options from `/etc/fstab`. The command to do this is:

```
```
[root@server1 root]# mount / -o remount, rw
[root@server1 root]#
```
```

+   3.  Create two files in the root of the filesystem called `aquota.user` and `aquota.group`. For the `/` filesystem, you should create the files `/aquota.user` and `/aquota.group`. Following this, run the `quota check` `-mavug` command, which looks on the system for file ownership and updates the quota database for all filesystems with quota options listed in `/etc/fstab` (`-a`), giving verbose output (`-v`) for all users and groups (`-u` and `-g`) even if