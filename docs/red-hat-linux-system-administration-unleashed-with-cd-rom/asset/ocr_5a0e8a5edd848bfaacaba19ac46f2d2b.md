Here is a sample entry in /etc/raidtab for a RAID level 0 array, using three disk partitions:

```
raiddev    /dev/md0
raid-level 0
nr-raid-disks 3
chunk-size 64
device     /dev/sdb1
raid-disk 0
device     /dev/sdc1
raid-disk 1
device     /dev/sdd1
raid-disk 2
```

# Note

> Due to the way in which striping is done, it is desirable to have the component parts of a RAID level 0 array be the same geometry. Failure to adhere to this rule can affect the performance of the array. Say, for example, that you create RAID level 0 array using a 100Mb partition on /dev/sda2 and a 150Mb partition on /dev/sdb1. In this case, all of the space would be would be divided up into the user specified stripe size and all access to the first 200Mb of the resulting 250Mb array would be interleaved across the two devices, thus increasing performance. Access to the final 50Mb of the array, which is physically located on a single disk, cannot ake advantage of multiple read/write heads of both devices and therefore is no faster than access to a single disk. It can even be slower due to the fact that access must now go through both the RAID code layer as well as the regular filesystem layer.

Linear devices and RAID level 0 arrays may be used for the root filesystem provided that support for this is compiled into your kernel.

RAID level 1 arrays are the lowest level of true RAID arrays supported by the Linux software RAID drivers. In order to create a mirrored array, or a RAID level 1 array, the entry is quite simple. In fact, it looks remarkably like the entry for a RAID level 0 device. The following is an example of a simple one-way mirror stanza from /etc/raidtab. In this example, there are two disks only. To create an N-way mirror, you could modify the entry and simply add to the number of raid disks and the number of device entries.