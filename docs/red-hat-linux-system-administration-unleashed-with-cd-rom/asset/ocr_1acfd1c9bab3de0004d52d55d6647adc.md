This entry will create a RAID level 0 array using /dev/sdb1 and /dev/sdc1, making the size of the array equal to the combined size of these two partitions. In our example, they are the same size. Again, to instantiate this RAID array, you simply run the mkraid command. Here is what this might look like:

```
[root@qtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0]
read_ahead 1024 sectors
unused devices: <none>
```

```
[root@qtest18 /root]# mkraid /dev/md0
handling MD device /dev/md0
analyzing super-block
disk 0: /dev/sdb1, 8883913kB, raid superblock at 8883840kB
disk 1: /dev/sdc1, 8883913kB, raid superblock at 8883840kB
```

```
[root@qtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0]
read_ahead 1024 sectors
md0 : active raid0 sdc1[1] sdb1[0] 17767680 blocks 32k chunks
unused devices: <none>
```

```
[root@qtest18 /root]# mkraid /dev/md1
handling MD device /dev/md1
analyzing super-block
disk 0: /dev/sdd1, 8883913kB, raid superblock at 8883840kB
disk 1: /dev/sde1, 8883913kB, raid superblock at 8883840kB
```

```
[root@qtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
md1 : active raid1 sde1[0] 8883840 blocks [2/2] [UU]
resync=0% finish=21.6min
md0 : active raid0 sdc1[1] sdb1[0] 17767680 blocks 32k chunks
unused devices: <none>
```

```
[root@qtest18 /root]# mkdir -p /raid1
[root@qtest18 /root]# mkdir -p /raid2
```

```
[root@qtest18 /root]# mke2fs -b 4096 -i 262144 /dev/md0
mke2fs 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
```