# mdadm: Linux software RAID

The following example scenario configures a RAID 5 array composed of identical 500GB hard disks. Although md can use raw disks as components, we prefer to give each disk a partition table for consistency, so we start by running parted (gpart refers to this the "msdos" style of partition table, and assigning all the disk's space to a single partition of type "unformatted" (which is unfortunately about close as you get to the actual). It is not strictly necessary to set the partition type, but it is a useful reminder to anyone who might inspect the table later. There is also a "raid" flag you can set on a partition, although ged doesn't make this easy: you must create the partition, execute the pending operations, and then go back to the new partition and edit its flags.

The following command builds a RAID 5 array from our three SCSI partitions:

```
linux$ mdadm --create /dev/md0 --level=5 --devices=3 /dev/sdb1
/dev/sdc1 /dev/vdd1
mdadm /dev/md0 started.
```

The virtual /proc/mdstat always contains a status of mdadm and the status of the system of the RAID arrays. It is especially useful to keep an eye on the /proc/mdstat after adding a new disk or replacing a faulty drive. (Watch cat /proc/mdstat is a handy idiom.)

```
linux$ cat /proc/mdstat
Personalities: [linear] [multipath] [raid0] [raid1] [raid6] [raid5] [raid4] [raid10]
md0 : active sdb1 sdd1 sdc1 sdb1
102304544 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_] -
recovery = 0.1% (672640/51702272) finish=75.99min
speed=112106K/sec
```

unused devices: 

The md system does not keep track of blocks in have been used, so it must manually synchronize all the parity blocks with their corresponding data blocks. md calls the operation "recovery" since it's the same procedure used when you swap out a bad disk. It can take hours on a large array.

Some helpful notifications appear in the /var/log/messages file, too

```
md0:RAID5 config:
--- rd.3 wd:2
disk 0, o:1, dev:sdb1
disk 1, o:1, dev:sdc
disk 2, o:1, dev:vdd
md: recovery of RAID array md0
md: minimum guaranteed_, speed: 1000 KB/sec/
md: using max available IO bandwidth (but not more than 200000 KB/sec) for recovery.
md: using 128k write, over a total of 51702272 blocks.
```

The initial creation command also serves to "activate" the array (make it available for use), but on subsequent reboots it may be necessary to activate the array as