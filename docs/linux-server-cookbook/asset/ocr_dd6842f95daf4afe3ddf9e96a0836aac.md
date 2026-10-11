```
```
[root@server2 ~]# fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test.fio
--bs=4k --iodepth=64 --size=4G --readwrite=randrw --numjobs=4
test: (g=0): rw=randrw, bs=(R) 4096b-4096b, (W) 4096b-4096b, (T) 4096b-4096b, ioengine=libaio, iodepth=64
...
fio-3.19
Starting 4 processes
test: Laying out IO file (1 file / 4096MiB)
Jobs: 4 (f=4): [m(4)][96.2%] r=384MiB/s,w=383MiB/s [r=98.2K,w=98.2K iops] [eta 00m:02s]

Run status group 0 (all jobs):
  READ: bw=164MiB/s (171MB/s), 40.8MiB/s-41.0MiB/s (42.8MB/s-42.9MB/s), io=8192MiB (8590MB), run=49990-50089msec
 WRITE: bw=164MiB/s (171MB/s), 40.9MiB/s-40.9MiB/s (42.9MB/s-42.9MB/s), io=8192MiB (8590MB), run=49990-50089msec

Disk stats (read/write):
 dm-1: ios=207688/2076846, merge=0/0, ticks=703954/4020718, in_queue=11051672, util=99.53%, aggrios=2097185/
 2100015, aggmerge=0/0, aggticks=7047507/4054918, aggrin_queue=11102425, aggrutil=98.54%
 dm-0: ios=2097185/2100015, merge=0/0, ticks=7047507/4054918, in_queue=11102425, util=98.54%, aggrios=2097185/
 2098583, aggmerge=0/1459, aggticks=6444743/3063238, aggrin_queue=9507982, agrutil=98.31%
 nvme0n1: ios=2097185/2098583, merge=0/1459, ticks=6444743/3063238, in_queue=9507982, util=98.31%
```
```

*Figure 6.39: Output example for command fio*

# ## Commands df and LVM commands

Command **df** described in *Chapter 3, Using the Command Line Interface*, shows the disk free and usage. If the system is using LVM (Logical Volume Manager), the commands to check the status are as follows:

+   *   **vgdisplay**: Display volume group information as shown in *figure 6.40*:

```
```
[root@server2 ~]# vgdisplay   2>/dev/null
 --- Volume group ---
  VG Name       RHELC5B
  System ID
  Format        lvm2
  Metadata Areas   1
  Metadata Sequence No 11
  VG Access   read/write
  VG Status   resizable
  MAX LV      0
  Cur LV      3
  Open LV     3
  Max PV      0
  Cur PV      1
  Act PV      1
  VG Size     499,98 TiB
  PE Size     4,00 MiB
  Total PE    131067903
  Alloc PE / Size 59392 / 232,00 GiB
  Free PE / Size 131008511 / <499,76 TiB
  VG UUID     wNqZcz-C2xE-xtfV-fFJn-Oe6n-QA5W-3Q13oz
```
```

*Figure 6.40: Output example for command vgdisplay*