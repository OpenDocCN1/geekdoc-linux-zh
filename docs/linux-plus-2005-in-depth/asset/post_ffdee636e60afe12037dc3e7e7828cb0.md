
## Linux Filesystem Quotas

If there are several users on a Linux system, there must be enough hard disk space to support the files that each user is expected to store on the hard disk. However, if hard disk space is limited or company policy limits disk usage, you should impose limits on filesystem usage. These restrictions are called **hard disk quotas**, and can be applied to users or groups of users. Furthermore, **quotas** can restrict how many files and directories a user can create (that is, restrict the number of inodes created) on a particular filesystem, or the total size of all files that a user can own on a filesystem. Two types of quota limits are available: soft limits and hard limits. **Soft limits** allow the user to extend them for a certain period of time (seven days by default), whereas **hard limits** are rigid and prevent the user from going past them. Quotas are typically enabled at boot time if there are quota entries in `/etc/fstab`, but can also be turned on and off afterward by using the `quotaon` and `quotaoﬀ` commands, respectively.

To set up quotas for the `/` filesystem and restrict the user user1, you can carry out the following steps:

- 1. Edit the `/etc/fstab` file to add the `usrquota` and `grpquota` mount options for the `/` filesystem. The resulting `/etc/fstab` file should look like the following:

```bash
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

- 2. Remount the root filesystem as read-write to update the system with the new options from `/etc/fstab`. The command to do this is:

```bash
[root@server1 root]# mount / -o remount, rw
[root@server1 root]# _
```

- 3. Create two files in the root of the filesystem called `aquota.user` and `aquota.group`. For the `/` filesystem, you should create the files `/aquota.user` and `/aquota.group`. Following this, run the `quotacheck -mavug` command, which looks on the system for file ownership and updates the quota database for all filesystems with quota options listed in `/etc/fstab` (`-a`), giving verbose output (`-v`) for all users and groups (`-u` and `-g`) even if the filesystem is used by other processes (`-m`). This places information in the `aquota.user` and `aquota.group` files.

```bash
[root@server1 root]# touch /aquota.user
[root@server1 root]# touch /aquota.group
[root@server1 root]# quotacheck -mavug
quotacheck: Scanning /dev/hda1 [/] done
quotacheck: Checked 22249 directories and 337809 files
[root@server1 root]# _
```

- 4. Turn quotas on for the `/` filesystem using the `quotaon /` command:

```bash
[root@server1 root]# quotaon /
[root@server1 root]# _
```

Alternatively, you can use the `quotaoff /` command to turn them off.

- 5. Edit the quotas for certain users by using the `edquota` command as follows: `edquota -u <username>`. This brings up the vi editor and allows you to set soft and hard quotas for the number of blocks a user can own on the filesystem (typically, 1 block = 1 Kilobyte) and the total number of inodes (files and directories) that a user can own on the filesystem. A soft limit (and hard limit of zero (0)) indicates that there is no limit. To set a hard limit of 20Mb (≈20480Kb) and 1000 inodes, as well as a soft limit of 18Mb (≈18432Kb) and 900 inodes, you can do the following:

```bash
[root@server1 root]# edquota -u user1
Disk quotas for user user1 (uid 500):
  Filesystem    blocks      soft     hard     inodes     soft    hard
  /dev/hda1       1188        0       0       326        0      0
~
~
~
~
"/tmp//EdP.aclps1v" 3L, 216C
```

Next place the appropriate values in the columns provided, and then save and quit the vi editor:

```bash
Disk quotas for user user1 (uid 500):
  Filesystem    blocks      soft     hard     inodes     soft    hard
  /dev/hda1       1188     18432   20480     326       900    1000
~
```

- 6. Edit the time limit for which users can go beyond soft quotas by using the `edquota -u -t` command. The default time limit for soft quotas is seven days, but can be changed as follows:

```bash
[root@server1 root]# edquota -u -t
Grace period before enforcing soft limits for users:
Time units may be: days, hours, minutes, or seconds

| Filesystem | Block grace period | Inode grace period |
| :--- | :--- | :--- |
| /dev/hda1 | 7days | 7days |
```

- 7. Ensure that quotas were updated properly by gathering a report for quotas by user on the `/` filesystem using the `repquota` command, as shown in the following output:

```bash
[root@server1 root]# repquota /
*** Report for user quotas on device /dev/hdc1
Block grace time: 7days; Inode grace time: 7days

| User | used | Block limits | | | File limits | | | | |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| | | soft | hard | grace | soft | hard | grace | | |
| root | -- 6420573 | 0 | 0 | 376520 | 0 | 0 | | | |
| bin | -- 14912 | 0 | 0 | 47 | 0 | 0 | | | |
| daemon | -- 16 | 0 | 0 | 5 | 0 | 0 | | | |
| lp | -- 8 | 0 | 0 | 2 | 0 | 0 | | | |
| news | -- 4396 | 0 | 0 | 228 | 0 | 0 | | | |
| uucp | -- 9612 | 0 | 0 | 23 | 0 | 0 | | | |
| games | -- 0 | 0 | 0 | 65 | 0 | 0 | | | |
| rpm | -- 101056 | 0 | 0 | 120 | 0 | 0 | | | |
| vcsa | -- 8 | 0 | 0 | 143 | 0 | 0 | | | |
| rpcuser | -- 32 | 0 | 0 | 8 | 0 | 0 | | | |
```

The report continues with the following users:

| User | used | Block limits | | | File limits | | | | |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| | | soft | hard | grace | soft | hard | grace | | |
| pcap | -- 256 | 0 | 0 | 14 | 0 | 0 | | | |
| smsp | -- 12 | 0 | 0 | 3 | 0 | 0 | | | |
| apache | -- 48 | 0 | 0 | 12 | 0 | 0 | | | |
| squid | -- 16 | 0 | 0 | 4 | 0 | 0 | | | |
| webalizer | -- 24 | 0 | 0 | 6 | 0 | 0 | | | |
| xfs | -- 8 | 0 | 0 | 3 | 0 | 0 | | | |
| named | -- 36 | 0 | 0 | 9 | 0 | 0 | | | |
| ntp | -- 12 | 0 | 0 | 3 | 0 | 0 | | | |
| gdm | -- 28 | 0 | 0 | 1 | 0 | 0 | | | |
| pwm | -- 8 | 0 | 0 | 2 | 0 | 0 | | | |
| wmn | -- 4184 | 0 | 0 | 44 | 0 | 0 | | | |
| postfix | -- 88 | 0 | 0 | 22 | 0 | 0 | | | |
| mailman | -- 4 | 0 | 0 | 2 | 0 | 0 | | | |
| amanda | -- 1108 | 0 | 0 | 74 | 0 | 0 | | | |
| netdump | -- 32 | 0 | 0 | 9 | 0 | 0 | | | |
| quagga | -- 32 | 0 | 0 | 8 | 0 | 0 | | | |
| radvd | -- 8 | 0 | 0 | 2 | 0 | 0 | | | |
| radiusd | -- 24 | 0 | 0 | 9 | 0 | 0 | | | |
| ldap | -- 8 | 0 | 0 | 2 | 0 | 0 | | | |
| mysql | -- 16 | 0 | 0 | 5 | 0 | 0 | | | |
| postgres | -- 5352 | 0 | 0 | 279 | 0 | 0 | | | |
| fax | -- 60 | 0 | 0 | 5 | 0 | 0 | | | |
| mut | -- 28 | 0 | 0 | 5 | 0 | 0 | | | |
| privoxy | -- 624 | 0 | 0 | 48 | 0 | 0 | | | |
| tomcat | -- 24 | 0 | 0 | 6 | 0 | 0 | | | |
| cyrus | -- 16808 | 0 | 0 | 34 | 0 | 0 | | | |
| exim | -- 40 | 0 | 0 | 10 | 0 | 0 | | | |
| user1 | -- 1188 | 18432 | 20480 | 326 | 900 | 1000 | | | |

Note that most users in the preceding output are system users and do not have quotas applied to them. These users are discussed in Chapter 10, “Managing Linux Processes.”

The aforementioned commands must be performed by the root user; however, regular users can view their own quota using the `quota` command. The root user can also use the `quota` command but can also use it to view quotas of other users:

```bash
[root@server1 root]# quota
Disk quotas for user root (uid 0): none

[root@server1 root]# quota -u user1
Disk quotas for user user1 (uid 500):
Filesystem blocks    quota    limit    grace    files    quota    limit    grace
/dev/hdc1  1188    18432     20480                 326      900     1000

[root@server1 root]# _
```

## Chapter Summary

- Disk devices are represented by device files that reside in the `/dev` directory. These device files specify the type of data transfer, the major number of the device driver in the Linux kernel, and the minor number of the specific device.
- Each disk device must contain a filesystem, which is then mounted to the Linux directory tree for usage using the `mount` command. The filesystem can later be unmounted using the `umount` command. The directory used to mount the device must not be in use by any logged-in users for mounting and unmounting to take place.
- Hard disks must be partitioned into distinct sections before filesystems are created on those partitions. The `fdisk` command can be used to partition a hard disk.
- Many different filesystems are available to Linux; each filesystem is specialized for a certain purpose and several different filesystems can be mounted to different mount points on the directory tree. You can create a filesystem on a device using the `mksfs` command and its variants.
- It is important to monitor disk usage using the `df`, `du`, and `dumpe2fs` commands to avoid running out of storage space. Similarly, it is important to check disks for errors using the `fsck` command and its variants.
- If hard disk space is limited, you can use hard disk quotas to limit the space that each user has on filesystems.

### Key Terms

- **/dev directory** — The directory off the root where device files are typically stored.
- **/dev/MAKEDEV** — The command used to re-create a device file if one or more of the following pieces of device information is unknown: major number, minor number, or type (character or block).
