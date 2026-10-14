# Figure 10-4 Completed RAID partitioning

assume you simply want to add a RAID array to an existing server. For this example I will assume I have added three new drives, /dev/sdb, /dev/sdc, and /dev/sdd, and I want to partition the drives and create a RAID 5 array across all three partitions that I then mount at /mnt/storage.

Software RAID arrays are created and managed under Ubuntu with the mdadm tool. This tool might not be installed by default; if it isn’t, run sudo apt-get install mdadm to install the package. The next step is to partition each of these drives. In my case I just create a single partition that spans the full drive. Use whichever partitioning tool you prefer (like fdisk or cfdisk) as though you were creating any other partition. The only difference here is to change the partition type from the default of 82 to fd. The fd partition type is set aside for Linux RAID autodetect. If a partition is set to that type, it tells Linux that it is part of a software RAID array.

Once your partitions are set up, you can use mdadm on the command line to create the MD device. In the case of a RAID 1 array you would type

```
$ sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
mdadm: array /dev/md0 started.
```