```
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information:done
[root@server1 ~]#
```

To mount this ext4 filesystem to a new mount point directory called /data and view the contents, you can use the following commands:

```
[root@server1 ~]# mkdir /data
[root@server1 ~]# mount -t ext4 /dev/sda5 /data
[root@server1 ~]# mount
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
/dev/sda2 on / type ext4 (rw,relatime,seclabel,data=ordered)
tmpfs on /tmp type tmpfs (rw,seclabel)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/sda5 on /data type ext4 (rw,relatime,seclabel,data=ordered)
[root@server1 ~]# ls -F /data
lost+found/
[root@server1 ~]#
```

To allow the system to mount this filesystem automatically at every boot, simply edit the /etc/fstab file, such that it has the following entry for /dev/sda5:

```
[root@server1 ~]# cat /etc/fstab


# /etc/fstab
# Created by anaconda on Wed Sep 24 15:33:17 2015
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for info
#
/dev/sda2       /             ext4    defaults            1 1
/dev/sda1       swap          swap    defaults            0 0
/dev/sda5       /data         ext4    defaults            0 0
[root@server1 ~]#
```

Although swap partitions do not contain a filesystem, you must still prepare swap partitions and activate them for use on the Linux system. To do this, you can use the mkswap command to prepare the swap partition and the swapon command to activate it. To prepare and activate the /dev/sda6 partition that we created earlier as virtual memory, you can use the following commands:

```
[root@server1 ~]# mkswap /dev/sda6
Setting up swapspace version 1, size = 2097148 KiB
no label, UUID=f7999b84-f9e4-48ff-879b-35b3c94c1fab
[root@server1 ~]# swapon /dev/sda6
[root@server1 ~]#
```