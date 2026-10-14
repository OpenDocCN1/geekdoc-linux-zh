```
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 39 mounts or
180 days, whichever comes first. Use tune2fs -c or -i to override.
Athena:~#
```

# Step 6: Make a file system for the /srv directory structure.

```
Athena:~# mkfs.ext3 -L WEB -v /dev/sdb2
mke2fs 1.34 (25-Jul-2003)
Filesystem label=WEB
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
2632672 inodes, 5263295 blocks
263164 blocks (5.00%) reserved for the super user
First data block=0
161 block groups
32768 blocks per group, 32768 fragments per group
16352 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736,
        1605632, 2654208,
        4096000

Writing inode tables: done
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 29 mounts or
180 days, whichever comes first. Use tune2fs -c or -i to override.
Athena:~#
```

The final processes required to incorporate the new device and partitions into
a server demanded a significant amount of attention to detail. They also require
a significant amount of scheduled downtime. To minimize the service outage,
you can perform a number of steps before you take down the system.

First, you can create temporary mount points for the new partitions. They are
renamed /home and /srv while the system is in single user mode. In addition,
you can prepare a new version of fstab to mount the new partitions on their
proper mount points. This way, you can test the fstab file while the system is
in single user mode and not have any surprises when the system reboots.

# Step 7: Create temporary mount points and check permissions.

```
Athena:~#
Athena:~# cd /
```