user will not be able to add more files till they delete the files to be below the limit.

+   2. **Hard limit:** The user will not be able, in any case, to have more than the limit specified.

Before quotas are used in a system, the user or the group quotas have to be enabled in the filesystem, which is required to be configured for quotas. This is not enabled by default. For that, it is needed to open the file `/etc/fstab` and, in the fourth column, add the words `usrquota` and/or `grpquota`, as is shown in figure 6.50:

```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/ubuntu-vg/ubuntu-lv during curtin installation
/dev/disk/by-iddm-uuid-LVM-BZrwBMRT0nAcI1QcZonwGQRHUKMzm1pJGLbA2z6NSilzWCGpNy88g55A5G5Eq1fi / ext4 defaults,usrquota,grpquota 0 1
```

Figure 6.50: File /etc/fstab content example

After this, the filesystem is required to be remounted to apply the new configuration. In this case, it is configured in the filesystem mounted in **root** (/): `mount -o remount,rw /`. It is possible to run the command `mount` without any option to ensure the quotas are enabled, as shown in figure 6.51:

```
root@ubuntu:~# mount -o remount,rw /
root@ubuntu:~# mount |grep quota
/dev/mapper/ubuntu--vg-ubuntu--1v on / type ext4 (rw,relatime,quota,usrquota,grpquota)
```

Figure 6.51: Using command mount to remount and check status

After enabling the quotas to attribute to the filesystem, it is required to create the files `aquota.user` and/or `aquota.group` to keep track of configuration and usage for users and groups. The way to create these files is through the command `quotacheck` with the options -u (for users), -g (for groups), and -m (do not remount as read-only for this task). After installing the `quota` package, the command `quotacheck` would be available, as shown in figure 6.52:

```
root@ubuntu:~# quotacheck -ugm /
root@ubuntu:~# ls -l /aquota*
-rw------- 1 root root 9216 Aug 14 14:46 /aquota.group
-rw------- 1 root root 8192 Aug 14 14:46 /aquota.user
```