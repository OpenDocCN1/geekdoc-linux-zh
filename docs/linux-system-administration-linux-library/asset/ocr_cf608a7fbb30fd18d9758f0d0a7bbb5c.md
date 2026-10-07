# Selecting Hardware 29

simultaneously from both drives. Read-balancing had some problems in Linux kernels, although this has been iron out in the 2.4 kernels. If you wish to take advantage of this, you should probably consider a kernel upgrade. Writes tend to be slower since two copies of the data must be written. RAID1 may mirror data between two local drives or between two different hosts.

RAID2 Not supported in Linux, RAID2 uses error correction to compensate for drives that do not have built-in error detection. Since most drives include correction now, RAID2 is seldom used.

RAID3 Not supported in Linux, RAID3 strips the data across all drives at the byte level. Parity information is stored on one of the disks in the array to protect against data loss in the event of a single disk failure.

RAID4 Similar to RAID3, except that the data is striped at the block level. Parity is maintained on one disk as in RAID3. This causes the parity disk to be the bottleneck.

RAID5 Similar to RAID4, except that parity is split between all the disks in the array. RAID5 array can withstand a single disk failure. Write performance is significantly slower since a single write operation requires old data and parity to be read from each disk, the new parity to be calculated, and the new data and parity to be written to each disk in the array. The improvement in reading from striping across multiple spindles goes a long way offsetting the overhead of performing the write parity calculations. It is not unusual for a well-configured RAID5 software array to perform as or better than the individual disks.

RAID can be implemented in hardware or software. The hardware implementations are extremely fast and relatively costly. The software implementations, on the other hand, are relatively inexpensive. As of kernel 2.2.16-22, which is standard for Red Hat 7.0, RAID0, RAID1, and RAID4/RA5 can be configured in the kernel. There is also an option to auto-detect RAID partitions; this works by detecting any partitions created with a partition ID of 0xfd, as opposed to the usual Linux partition type code of 0x83. (You can check or change a partition type code with the Linux disk utility, as described in Chapter 10.)

To see what RAID support you have already installed, look at the /proc/mdstat file. If you are not running any of the RAID modules that exist in /lib/modules/2.2.16-22/block, the file will not exist or will contain the following:

+   Personalities : []
read_ahead not set
unused devices: <none>

![](bbox=[0.915, 0.13, 0.975, 0.245])