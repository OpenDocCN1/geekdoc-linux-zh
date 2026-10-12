
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

After we have unmounted the filesystem and have created and used raidstop to deactivate the array, we are ready to create a more complex mirror. In this example, we will create a mirror consisting of two RAID level 0 arrays. This will require three stanzas in /etc/raidtab and in this case, ordering of the entries is crucial. The /etc/raidtab file is parsed sequentially and therefore we must define the two RAID level 0 arrays first and then define the mirror. Here is what this looks like:

# Mirror consisting of two striped arrays
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
device /dev/sdd1
raid-disk 0
device /dev/sde1
raid-disk 1

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

One of the advantages of this setup is that writes to the components of the mirror get the performance advantage of RAID level 0 in addition to the performance advantage of mirrors on read operations. This combination is mistakenly called RAID level 10 in some of the Linux RAID documentation found on the Web. It is in fact the exact opposite of RAID level 10, which is the creation of a RAID level 0 array consisting of two RAID level 1 arrays. Here is what creation of this configuration would look like:

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

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
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

Again, let us unmount the filesystem we created and use raidstop to deactivate the array. We are ready now to create the next type of RAID array, the RAID level 4 array. For this array, we will use three of the disks as data disks and the fourth disk as the parity disk with no spares. Here is the /etc/raidtab entry created for this example:

# RAID-4 array example
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

The following session transcript shows the creation of the array, the creation of a filesystem on the array, and the contents of the md status file in /proc. As you can see, it is possible to start using the array immediately after it is registered with the kernel, even though the array is not completely initialized. Although this is possible, it is recommended that you do not begin writing data to the array until the initialization is completed. You can determine when this happens by watching the process table and by checking /proc/mdstat.

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
