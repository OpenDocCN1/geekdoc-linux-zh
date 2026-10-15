Names of Disks Actually Installed on Your System" from Section 24.2.1. The complete logical device names, including the appropriate partitions on those disks, of our original hard disk (the boot disk with the operating system and all your files on it) and the second hard disk drive we want to mirror it to are /dev/ada0s1 and /dev/ada1p3. On your system they may not be exactly the same, but they will be very similar.

5. The size in bytes of tank (the name of the default system pool for our PC-BSD) is smaller than or equal to the size of the partition on the second hard disk drive you will mirror tank to.

Procedure: Do the following steps in the order shown to meet the objectives.

+   1. Become the superuser.

```
[bob@pcbsd-5867] ~# su
Password: xxx
[bob@pcbsd-5867] ~#
```

+   2. Having previously determined the logical device name to the new hard disk to be ada1, you should delete the ZFS metadata associated with all partitions that may have previously existed on it. This also clears the partitions on ada1.

```
[bob@pcbsd-5867] ~# zpool labelclear -f ada1
```

In the next steps, we will prepare partitions on the new hard disk to accommodate the mirroring process. If the new disk does not have a GPT partition table on it, you can use the following gpart command:

```
bob@pcbsd-5867]# gpart create -s gpt ada1
```

+   3. You then have to add a boot partition to the new hard disk, using the gpart command, so that you will be able to boot to it in the event of a failure of the original system disk.

```
[bob@pcbsd-5867] ~# gpart add -b 40 -l gptboot -s 512k -t freebsd-boot ada1
ada1p1 added
```

+   4. You then have to add a swap space partition to the new hard disk.

```
[bob@pcbsd-5867] ~# gpart add -s 1G -l swap1 -t freebsd-swap ada1
ada1p2 added
```

+   5. You then have to add the primary partition that will contain the tank1 zpool and all file systems attached to it.

```
[bob@pcbsd-5867] ~# gpart add -t freebsd-zfs -l zfs1 ada1
ada1p3 added
```