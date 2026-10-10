of the partitions in the RAID array. Once the new partition is ready, use the --add command to add it to the array:

```
`$ sudo mdadm /dev/md0 --add /dev/sddl`
```

Now mdadm will start the process of resyncing data. This can take some time, depending on the speed and size of your disks. You can monitor the progress from /proc/mdstat:

```
```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md0 : active raid5 sdd1[3] sdb1[0] sdc1[1]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/2] [UL_]
[>....................] recovery = 2.8% (170112/6385792)
finish=1.6min speed=85056K/sec
unused devices: <none>
```
```

> **NOTE**  
> If you get tired of running cat /proc/mdstat over and over, you can use the watch command to update it every few seconds. For instance, to run that command every 5 seconds you could type
> `$ watch -n 5 "cat /proc/mdstat"`
> Just hit Ctrl-C to exit out of the watch command when you are done.