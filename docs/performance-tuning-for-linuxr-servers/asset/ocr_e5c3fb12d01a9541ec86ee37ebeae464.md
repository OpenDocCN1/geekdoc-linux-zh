operations that could be completed over a period of time. Further, such a bizarre access pattern would likely reduce not just the number of devices per logical drive, but also the overall I/O transfer rate.

Another solution to multitasking is to ensure that the data requests from the applications and operating system are well distributed among the disks connected to the system. Distributing the I/O requests to multiple disks effects a level of parallelism that further reduces the performance impacts of the individual latencies of disk drives. Redistributing the application data among a number of disk devices often requires a solid understanding of the workload as well as an understanding of the data access patterns of that workload.

Although system monitoring tools do not provide the capability to track each I/O that a particular application issues, there are tools that allow a performance analyst to monitor the total number of I/Os processed by the system, the number of I/O operations per logical disk drive, and the overall I/O transfer rate. The two primary tools discussed in the next sections are `iostat(1)` and `iostat(1)`. You can use these tools to understand what the I/O bottlenecks are, what disks or interconnects are underutilized, and what the latencies are from a system perspective (as opposed to an application perspective).

Before exploring the specific tools, keep in mind that there are many techniques for increasing I/O performance. These techniques include purely hardware-related solutions (such as using disk drives that have higher revolutions per minute, thereby providing lower I/O latencies, larger disk cache sizes, or I/O controller cache sizes). They also include improved data transfer rates for both reads and writes, and/ increases in I/O bus speeds or I/O fabric speeds, which both increase data transfer rates and reduce I/O latencies. Also, some disk drives and disk storage subsystems provide multiported logical or physical disks, allowing parallel I/O from a single disk, which again increases potential I/O throughput. Additionally, hardware and software RAID (Redundant Array of Independent Disks) were designed to increase access parallelism by striping data across multiple disk drives.

The tools discussed in the following sections provide data that can be useful in considering hardware and software solutions as well as improvements in data layout.

# iostat

The `iostat` command monitors system I/O activities by observing how long the physical disks are active in relation to their average transfer rates. The `iostat` command generates reports that can be used to change system configuration to better balance the I/O load among physical disks. `iostat(1)` also provides CPU utilization that can sometimes be useful in comparing directly against the I/O activities. If no display interval is given, `iostat` gives out I/O information since the system was last booted. If a display interval is given, the first set of output represents total activity since boot time, and subsequent displays only show the delta activities. The following display corresponds to copying files from /dev/sd0 to /dev/sd5, /dev/sd7 to /dev/sd7, and /dev/sd7 to /dev/sd7:

```
avg-cpu:  %user   %nice   %sys  %iowait   %idle
0.21      0.00    0.80    2.07   96.92

Device:    tps Blk_read/s  Blk_wrt/s   Blk_read   Blk_wrt
sd          0.00    0.00      0.00        32       0
sdw         0.00    0.00      0.00        32       0
sdv         0.00    0.00      0.00        32       0
sdu         2.49    0.05   1443.46     2778  79552392
sdt         4.94    0.10   2871.73     5322 158268008
sds         4.95    0.10   2860.91     5330 157671720
sdr        30.20  1518.55    0.42  83690898    23288
sdq        60.25  2902.76    0.92 159978258    50896
```