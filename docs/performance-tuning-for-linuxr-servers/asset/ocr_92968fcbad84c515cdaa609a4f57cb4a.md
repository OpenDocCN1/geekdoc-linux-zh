# AS Sequential Read Performance

In the single disk setup, the AS implementation can approach the capacity of the hardware and therefore provides optimal throughput performance. Under the same workload conditions, the CFQ scheduler substantially hampers throughput performance and does not allow the system to fully utilize the capacity of the I/O subsystem. The described behavior holds true for the Ext3 and the XFS file systems. Hence, in the case of sequential read operations and CFQ, the I/O scheduler, not the file system per se, reflects the actual I/O bottleneck. This picture is reversed as the capacity of the I/O subsystem is increased.

As depicted in Table 19-5, the CFQ scheduler approaches the throughput of the AS implementation in the benchmarked RAID-5 environment, and can approach the capacity of the hardware in the large RAID-0 setup; the AS scheduler approaches only approximately 17% of the hardware capacity (180 MBps) in the RAID-0 environment. To reiterate, the discussed I/O behavior is reflected in the Ext3 and XFS benchmark results. From any file system perspective, performance should not degrade if the size of the file system, the number of files stored in the file system, or the size of the individual files stored in the file system increases. Further, the performance of a file system is supposed to approach the capacity of the hardware. This study clearly outlines that in the discussed workload scenario, the two benchmarked file systems can achieve these goals, but only in the case where the I/O schedulers are exchanged depending on the physical hardware setup. The read-ahead code in Linux 2.6 has to operate as efficiently as possible in conjunction with the I/O scheduler, and the file system has to be considered as well.

# Table 19-5. AS Versus CFQ Sequential Read Performance

| Hardware Setup | AS Throughput | CFQ Throughput |
|---|---|---|
| Single Disk | 52 MBps | 23 MBps |
| RAID-5 | 46 MBps | 39.2 MBps |
| RAID-0 | 31 MBps | 158 MBps |

Based on the benchmarked profiles and hardware setups, the AS scheduler provides, in most circumstances, the least-efficient I/O solution. Because the AS framework represents an extension to the deadline implementation, the next section explores the possibility of tuning AS to approach deadline behavior.