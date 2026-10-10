This will also create a new ZFS volume called datastorage1 and mount it to /datastorage1, as shown here in the last line of the mount command output:

```
```
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw,errors=remount-ro)
proc on /proc type proc (rw,noexec,nosuid,nodev)
sysfs on /sys type sysfs (rw,noexec,nosuid,nodev)
tmpfs on /run type tmpfs (rw,noexec,nosuid,size=10%,mode=0755)
systemd on /sys/fs/cgroup/systemd type cgroup
(rw,noexec,nosuid,nodev,none,name=systemd)
datastorage1 on /datastorage1 type zfs (rw,xattr)
[root@server1 ~]# _
```
```

You can also use the zpool command to view the details for your datastorage1 volume:

```
```
[root@server1 ~]# zpool list
NAME     SIZE  ALLOC FREE  CAP  DEDUP  HEALTH ALTROOT
datastorage1  816M   114K   816M  0%  1.00x ONLINE -
[root@server1 ~]# _
```
```

![](bbox=[0.16, 0.42, 0.42, 0.52])

If you specify multiple devices when creating a simple ZFS volume, then both devices are automatically added to the ZFS pool and a ZFS volume created from their contents. For example, if you run the following command, the /dev/sdc and /dev/sdd hard disks would be added to the datastorage2 pool, and a ZFS volume called datastorage2 would be created (with a capacity of both hard disks combined) and mounted to the /datastorage2 directory. This would act as the equivalent of a RAID 0 volume, but with the file corruption prevention benefits of ZFS.

```
```
[root@server1 ~]# zpool create datastorage2 /dev/sdc /dev/sdd
[root@server1 ~]# _
```
```

To create a ZFS pool and mirrored ZFS volume called datastorage3 from the /dev/sde and /dev/sdf hard disks and mount the volume to /datastorage3, you simply need to specify the mirror keyword during creation, as shown here:

```
```
[root@server1 ~]# zpool create datastorage3 mirror /dev/sde /dev/sdf
[root@server1 ~]# _
```
```

The datastorage3 volume is the equivalent of RAID 1 but resize-able under ZFS, and the total size of the volume is identical to the size of one of the hard disks.

![](bbox=[0.16, 0.85, 0.33, 0.92])