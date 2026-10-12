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

```
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