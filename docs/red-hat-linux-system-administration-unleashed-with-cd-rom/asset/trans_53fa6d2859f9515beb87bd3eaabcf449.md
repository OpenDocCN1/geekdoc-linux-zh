
[root@qhtest18 /root]# ls /raid1
lost+found

[root@qhtest18 /root]# ls /raid2
lost+found

[root@qhtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
md1 : active raid1 sde1[0] sdd1[0] 8883840 blocks [2/2] [UU]
resync=9% finish=20.8min
md0 : active raid0 sdc1[1] sdb1[0] 17767680 blocks 32k chunks
unused devices: <none>

[root@qhtest18 /root]# umount /raid2
[root@qhtest18 /root]# umount /raid1
[root@qhtest18 /root]# raidstop /dev/md0
[root@qhtest18 /root]# raidstop /dev/md1
[root@qhtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
unused devices: <none>

在我们卸载文件系统并使用 raidstop 停用阵列后，我们就可以创建更复杂的镜像。在本例中，我们将创建一个由两个 RAID 0 级阵列组成的镜像。这需要在 /etc/raidtab 中使用三个段落，并且在这种情况下，条目的顺序至关重要。/etc/raidtab 文件是顺序解析的，因此我们必须先定义两个 RAID 0 级阵列，然后再定义镜像。下面是其外观：

# 由两个条带阵列组成的镜像
raiddev    /dev/md0
raid-level 0
persistent-superblock 0
chunk-size 32
nr-raid-disks 2
nr-spare-disks 0
device     /dev/sdb1
raid-disk  0
device     /dev/sdc1
raid-disk  1

raiddev    /dev/md1
raid-level 0
persistent-superblock 0
chunk-size 32
nr-raid-disks 2
nr-spare-disks 0
device     /dev/sdd1
raid-disk  0
device     /dev/sde1
raid-disk  1

raiddev /dev/md2
raid-level 1
persistent-superblock 0
chunk-size 32
nr-raid-disks 2
nr-spare-disks 0
device /dev/md0
raid-disk 0
device /dev/md1
raid-disk 1

这种设置的一个优点是，对镜像组件的写入可以获得 RAID 0 级的性能优势，同时镜像在读操作上也有性能优势。这种组合在网络上一些 Linux RAID 文档中被错误地称为 RAID 10。实际上它与 RAID 10 正好相反，RAID 10 是由两个 RAID 1 级阵列组成的 RAID 0 级阵列。下面是创建此配置的外观：

[root@qtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
unused devices: <none>

[root@qtest18 /root]# mkraid /dev/md0
handling MD device /dev/md0
analyzing super-block
disk 0: /dev/sdb1, 8889313kB, raid superblock at 8883640kB
disk 1: /dev/sdc1, 8889313kB, raid superblock at 8883640kB

[root@qtest18 /root]# mkraid /dev/md1
handling MD device /dev/md1
analyzing super-block
disk 0: /dev/sdd1, 8889313kB, raid superblock at 8883640kB
disk 1: /dev/sde1, 8889313kB, raid superblock at 8883640kB

[root@hqtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
md1 : active raid0 sde1[1] sdd1[0] 17767808 blocks 32k chunks
md0 : active raid0 sdc1[1] sdb1[0] 17767808 blocks 32k chunks
unused devices: <none>

[root@hqtest18 /root]# mkraid /dev/md2
handling MD device /dev/md2
analyzing super-block
disk 0: /dev/md0, 17767808KB, raid superblock at 17767744KB
disk 1: /dev/md1, 17767808KB, raid superblock at 17767744KB

[root@hqtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
md2 : active raid1 md1[1] md0[0] 17767808 blocks [2/2] [UU]
resync=0% finish=38.6min
md1 : active raid0 sde1[1] sdd1[0] 17767808 blocks 32k chunks
md0 : active raid0 sdc1[1] sdb1[0] 17767808 blocks 32k chunks
unused devices: <none>

[root@hqtest18 /root]# mke2fs -b 4096 -i 262144 /dev/md2
mke2fs 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
69632 inodes, 4441952 blocks
222097 blocks (5.00%) reserved for the super user
First data block=0
Block size=4096 (log=2)
Fragment size=4096 (log=2)
136 block groups
32768 blocks per group, 32768 fragments per group
512 inodes per group
Superblock backups stored on blocks:
32768, 65536, 98304, 131072, 163840, 196608, 229376, 262144, 294912,
327680, 368448, 393216, 425984, 458752, 491520, 524288, 557056,
589824
622592, 655360, 688128, 720896, 753664, 786432, 819200, 851968,
884736,
917504, 958272, 983040, 1015808, 1048576, 1081344, 1114112, 1146880,
1179648, 1212416, 1245184, 1277952, 1310720, 1343488, 1376256,
1409824,
1441792, 1474560, 1507328, 1540096, 1572864, 1605632, 1638400,
1671168,
1703936, 1736704, 1769472, 1802240, 1835008, 1867776, 1900544,
1933312,
1966080, 1998848, 2031616, 2064384, 2097152, 2129920, 2162688,
2228224, 2260992, 2293760, 2326528, 2359296, 2392064, 2424832,
2457600,
2490368, 2523136, 2555904, 2588672, 2621440, 2654208, 2686976,
2719744,
2752512, 2785280, 2818048, 2850816, 2883584, 2916352, 2949120,
2981888,
3014656, 3047424, 3080192, 3112960, 3145728, 3178496, 3211264,
3244032,
3276800, 3309568, 3342336, 3375104, 3407872, 3440640, 3473408,
3506176,
3538944, 3571712, 3604480, 3637248, 3670016, 3702784, 3735552,
3768320,
3801088, 3833856, 3866624, 3899392, 3932160, 3964928, 3997696,
4030464,
4063232, 4096000, 4128768, 4161536, 4194304, 4227072, 4259840,
4292608,
4325376, 4358144, 4390912, 4423680

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

[root@hqtest18 /root]# mount /dev/md2 /raid

[root@hqtest18 /root]# df

| 文件系统 | 1K 块 | 已用 | 可用 | 使用% | 挂载点 |
|---|---|---|---|---|---|
| /dev/sda2 | 2085638 | 81745 | 1846668 | 4% | / |
| /dev/sda7 | 6172033 | 974808 | 4877534 | 17% | /usr |
| /dev/md2 | 17756384 | 52 | 16867944 | 0% | /raid |

[root@hqtest18 /root]# ls /raid
lost+found

[root@hqtest18 /root]# umount /raid

[root@hqtest18 /root]# raidstop /dev/md2

[root@hqtest8 /root]# raidstop /dev/md1

[root@hqtest8 /root]# raidstop /dev/md0

[root@hqtest8 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
unused devices: <none>

再次，让我们卸载我们创建的文件系统并使用 raidstop 停用阵列。我们现在准备创建下一个类型的 RAID 阵列，即 RAID 4 级阵列。对于此阵列，我们将使用三块磁盘作为数据盘，第四块磁盘作为奇偶校验盘，且不使用热备。下面是为此示例创建的 /etc/raidtab 条目：

# RAID-4 阵列示例
raiddev	/dev/md0
raid-level	4
persistent-superblock	0
chunk-size	32
nr-raid-disks	4
nr-spare-disks	0
device	/dev/sdb1
raid-disk	0
device	/dev/sdc1
raid-disk	1
device	/dev/sdd1
raid-disk	2
device	/dev/sde1
parity-disk	0

以下会话记录显示了阵列的创建、阵列上文件系统的创建以及 /proc 中 md 状态文件的内容。如您所见，即使阵列尚未完全初始化，在其向内核注册后也可以立即开始使用。虽然这是可能的，但建议您在初始化完成之前不要开始向阵列写入数据。您可以通过查看进程表并检查 /proc/mdstat 来确定何时完成。

[root@hqtest8 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
unused devices: <none>

[root@hqtest8 /root]# mkraid /dev/md0
handling MD device /dev/md0
analyzing super-block
disk 0: /dev/sdb1, 8889313KB, raid superblock at 8883840KB
disk 1: /dev/sdc1, 8889313KB, raid superblock at 8883840KB
disk 2: /dev/sdd1, 8889313KB, raid superblock at 8883840KB
disk 3: /dev/sde1, 8889313KB, raid superblock at 8883840KB

[root@qtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1] [raid5]
read_ahead 1024 sectors
md0 : active raid5 sde1[3] sdd1[2] sdc1[1] sdb1[0] 2665712 blocks
level 4, 32k chunk, algorithm 0 [4/4] [UUUU] resync=0% finish=47.8min
unused devices: <none>

[root@qtest18 /root]# mke2fs -b 4096 -i 262144 /dev/md0
mke2fs 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
104448 inodes, 6662928 blocks
333146 blocks (5.00%) reserved for the super user
First data block=0
Block size=4096 (log=2)
Fragment size=4096 (log=2)
204 block groups
32768 blocks per group, 32768 fragments per group
512 inodes per group
Superblock backups stored on blocks:
32768, 65536, 98304, 131072, 163840, 196608, 229376, 262144, 294912,
327680, 360448, 393216, 425984, 458752, 491520, 524288, 557056,
589824,
622592, 655360, 688128, 720896, 753664, 786432, 819200, 851968,
884736,
917504, 950272, 983040, 1015808, 1048576, 1081344, 1114112, 1146880,
1179648, 1212416, 1245184, 1277952, 1310720, 1343488, 1376256,
1409024,
1441792, 1474560, 1507328, 1540096, 1572864, 1605632, 1638400,
1671168,
1703936, 1736704, 1769472, 1802240, 1835008, 1867776, 1900544,
1933312,
1966080, 1998848, 2031616, 2064384, 2097152, 2129920, 2162688,
2195456,
2228224, 2260992, 2293760, 2326528, 2359296, 2392064, 2424832,
2457600,
2490368, 2523136, 2555904, 2588672, 2621440, 2654208, 2686976,
