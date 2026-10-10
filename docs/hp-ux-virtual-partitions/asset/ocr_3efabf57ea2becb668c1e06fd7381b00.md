# Devices and Virtual Partitions

+   - Kernel Device info
+     ```
+     dump lvol
+     ```

+   - Tunable parameters

```
```
STRMSGSZ              65535
chlc_hash_locks       512
maxdsiz_64bit         0x40000000
maxssiz_              0x800000
maxssiz_64bit         0x8000000
maxswapChunks          2048
maxtsiz               0x4000000
maxtsiz_64bit         0x40000000
nstrply               64
shmmax                0x4000000
cvhdcnc3:/ #
```
```

We could now use the tape drive to perform a backup of `cable`. There is detailed information on backup in Chapter 7, including performing a backup using a remote tape drive. The following example shows the **fbbackup** command issued:

```
```
fbbackup -0u -f /dev/rmt/0m -g /tmp/backupgraph -I
	/tmp/backupindex.date '+%Y%m%d_%H:%M' 2>
	/tmp/backup.date '+%Y%m%d_%H:%M'
```
```

This produces an *index* file of the backup of `/var` on `cable` that contains the following entries:

```
```
1024                  1 / 
1024                  1 /var
1024                  1 /var/tmp/.fmd
200                   1 /var/tmp/aaaa01664
0                     1 /var/tmp/aaaa01745
0                     1 /var/tmp/aaaa01806
0                     1 /var/tmp/aaaa02391
0                     1 /var/tmp/cmd_res3036
0                     1 /var/tmp/cmd_res4403
1560                  1 /var/tmp/disk_em.fmt
324                   1 /var/tmp/dm_TL_adapter.fmt
1392                  1 /var/tmp/dm_stage.fmt
1241                  1 /var/tmp/ems_inittab.old
28                    1 /var/tmp/envd.action2
28                    1 /var/tmp/envd.action5
200                   1 /var/tmp/fc0mon.fmt
4106                  1 /var/tmp/inetd.conf.old
```
```