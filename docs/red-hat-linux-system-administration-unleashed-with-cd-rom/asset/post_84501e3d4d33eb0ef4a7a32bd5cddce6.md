
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
4325376, 4358144, 4390912, 4423680, 4456448, 4489216, 4521984,
4554752,
4587520, 4620288, 4653056, 4685824, 4718592, 4751360, 4784128,
4816896,
4849664, 4882432, 4915200, 4947968, 4980736, 5013504, 5046272,
5079040,
5111808, 5144576, 5177344, 5210112, 5242880, 5275648, 5308416,
5341184,
5373952, 5406720, 5439488, 5472256, 5505024, 5537792, 5570560,
5603328,
5636096, 5668864, 5701632, 5734400, 5767168, 5799936, 5832704,
5865472,
5898240, 5931008, 5963776, 5996544, 6029312, 6062080, 6094848,
6127616,
6160384, 6193152, 6225920, 6258688, 6291456, 6324224, 6356992,
6389760,
6422528, 6455296, 6488064, 6520832, 6553600, 6586368, 6619136,
6651904

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

```
[root@hqtest8 /root]# mount /dev/md0 /raid
```

```
[root@hqtest8 /root]# df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/sda2 | 2035638 | 81769 | 1848644 | 4% | / |
| /dev/sda7 | 6172033 | 974008 | 4877534 | 17% | /usr |
| /dev/md0 | 26634576 | 52 | 25301940 | 0% | /raid |

```
[root@qtest18 /root]# ls /raid
lost+found

[root@qtest18 /root]# umount /raid

[root@qtest18 /root]# raidstop /dev/md0

[root@qtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1] [raid5]
read_ahead 1024 sectors
unused devices: <none>
```

Our final example is the one that is most commonly used, a RAID level 5 array. This RAID level is often selected because it offers the redundancy advantages of RAID levels 1 and 4 without the write penalty of mirroring, and without the parity checking bottleneck of RAID level 4. Let's look at the /etc/raidtab entry for this example.

```
# RAID-5 array example with one spare
raiddev		/dev/md0
raid-level		5
persistent-superblock	0
chunk-size		32
parity-algorithm	left-symmetric
nr-raid-disks		3
# nr-spare-disks	1
device		/dev/sdb1
raid-disk	0
device		/dev/sdc1
raid-disk	1
device		/dev/sdd1
raid-disk	2
# device	/dev/sde1
# spare-disk	0
```

You will note in the entry above the addition of a keyword, parity-algorithm. This entry controls the algorithm used to determine which disk in each slice will be used to store the parity data. You will also note that the entries for nr-spare-disks and the definition of /dev/sde1 as a spare are commented out, so that for the following session, this definition results in the creation of a filesystem that is 16Gb in size.

The formula for calculating the size of a RAID level 5 array is (N - 1) * S, where N is the value of nr-raid-disks and S is the size of the smallest device used in the creation of the array. In this example, using four identical disks of 9 Gb each, this is (3 - 1) * 9Gb or 18Gb of space for the filesystem created on the array.

```
[root@hqtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1] [raid5]
read_ahead 1024 sectors
unused devices: <none>
```

```
[root@hqtest18 /root]# mkraid /dev/md0
handling MD device /dev/md0
analyzing super-block
disk 0: /dev/sdb1, 8883913kB, raid superblock at 8883840kB
disk 1: /dev/sdc1, 8883913kB, raid superblock at 8883840kB
disk 2: /dev/sdd1, 8883913kB, raid superblock at 8883840kB
```

```
[root@hqtest18 /root]# mke2fs -b 4096 -i 262144 /dev/md0
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

Writing inode tables:  done
Writing superblocks and filesystem accounting information:  done

[root@hqtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1] [raid5]
read_ahead 1024 sectors
md0 : active raid5 sdd[2] sdc[1] sdb[0] 17767808 blocks level 5, 32k chunk, algorithm 2 [3/3] [UUU] resync=0% finish=80.0min
unused devices: <none>
```

```
[root@hqtest18 /root]# mount /dev/md0 /raid
```

```
[root@hqtest18 /root]# df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/sda2 | 2635638 | 81777 | 1848636 | 4% | / |
| /dev/sda7 | 6172833 | 974808 | 4877534 | 17% | /usr |
| /dev/md0 | 17756384 | 52 | 16867944 | 0% | /raid |

```
[root@hqtest18 /root]# ls /raid
lost+found
```

Now that we have a working RAID level 5 array, let's make it a little more robust by adding a spare disk that can be used for hot reconstruction in the event of a disk failure. To do this, we must modify our /etc/raidtab entry by uncommenting the nr-spare-disks entry and the definition of /dev/sde1 as a spare disk, resulting in a raidtab entry that looks like this:

```
# RAID-5 array example with one spare
raiddev		/dev/md0
```

```
raid-level      5
persistent-superblock  0
chunk-size      32
parity-algorithm        left-symmetric
nr-raid-disks   3
nr-spare-disks  1
device  /dev/sdb1
raid-disk       0
device  /dev/sdc1
raid-disk       1
device  /dev/sdd1
raid-disk       2
device  /dev/sde1
spare-disk      0
```

Once these changes have been made, we run the raidhotadd command as shown here to add this spare disk to the array:

```
[root@hqtest18 /root]# raidhotadd /dev/md0 /dev/sde1
```

```
[root@hqtest18 /root]# cat /proc/mdstat
Personalities : [linear] [raid0] [raid1] [raid5]
read_ahead 1024 sectors
md0 : active raid5 sde1[3] sdd1[2] sdc1[1] sdb1[0] 17767808 blocks
level 5, 32K chunk, algorithm 2 [3/3] [UUU] resync=3% finish=48.8min
unused devices: <none>
```

As you can see, the sde1 device is now part of the RAID array and construction of the array is proceeding. This is an important new feature of software RAID for Linux that was lacking in previous releases.

One final topic concerning Linux software RAID is booting from a RAID device. With Red Hat 6.0, this procedure has become much easier, with the exception of installation. Red Hat boot images do not currently support installing to a RAID device, which means that you must first install on a normal partition and then copy the installation to the RAID array that you create.

There are actually multiple methods for booting from a RAID array. The original method is documented in a HOWTO document called the “Root RAID HOWTO cookbook,” by Michael A. Robinton. This document can be found in the /usr/doc/HOWTO directory of your Red Hat installation, provided that you included this when you set up your system, in a file named Root - RAID - HOWTO. This method is very complex and with the 2.2 series kernels, totally unnecessary. Another method for booting from a RAID is documented very briefly in the kernel source tree, in the Documentation directory in md.txt. This method
