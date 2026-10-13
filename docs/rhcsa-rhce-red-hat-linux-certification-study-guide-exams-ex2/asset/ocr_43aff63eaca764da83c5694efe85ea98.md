# FIGURE 6-14

Sample /etc/fstab

```
[root@server1 ~]# mount
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw,rootcontext="system_u:object_r:tmpfs_t:s0")
/dev/vdal on /boot type ext4 (rw)
/dev/vda3 on /home type ext4 (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/tmp on /tmp type none (rw,bind)
/var/tmp on /var/tmp type none (rw,bind)
/home on /home type none (rw,bind)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
[root@server1 ~]#
```

When adding a new partition, you could just add the device file associated with the partition, LV, or LUKS volume to the first column. The last four lines include virtual filesystems, and are discussed later in this chapter.

# TABLE 6-8

Description of /etc/fstab by Column, Left to Right

| Field Name | Description |
|---|---|
| Device | Lists the device to be mounted; you may substitute the UUID or LABEL. |
| Mount Point | Notes the directory where the filesystem will be mounted. |
| Filesystem Format | Describes the filesystem type. Valid filesystem types include ext, ext2, ext3, ext4, msdos, vfat, devpts, proc, tmpfs, udf, iso9660, nfs, smb, and swap. |
| Mount Options | Covered in the following section. |
| Dump Value | Either 0 or 1. A value of 1 means that data is automatically saved to disk by the dump command when you exit Linux. |
| Filesystem Check Order | Determines the order that filesystems are checked by the fsck command during the boot process. The root directory (/) filesystem should be set to 1, and other local filesystems should be set to 2. Removable filesystems such as those associated with CD/DVD drives should be set to 0, which means that they are not checked during the Linux boot process. |