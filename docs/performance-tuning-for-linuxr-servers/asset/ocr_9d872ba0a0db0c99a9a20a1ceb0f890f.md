|  | AS - Ext3 | DL - Ext3 | NO - Ext3 | CFQ - Ext3 | AS - XFS | DL - XFS | NO - XFS | CFQ - XFS |
|---|---|---|---|---|---|---|---|---|
| Web Server | 70.2 | 58.4 | 66.2 | 59.2 | 82.1 | 81.3 | 78.8 | 75.2 |
| Mail Server | 119.2 | 114.8 | 115.3 | 119.3 | 153.9 | 92.1 | 100.7 | 92.2 |
| Seq. Read | 517.5 | 631.1 | 654.1 | 583.5 | 515.8 | 624.4 | 628.7 | 604.5 |
| Seq. Write | 1033.2 | 843.7 | 969.5 | 840.5 | 426.6 | 422.3 | 462.6 | 400.4 |

In the second phase, all the I/O scheduler setups are tuned by adjusting the tunable $nr\_requests$ from its default value of 128 to 2,560. The results reveal that the CFQ scheduler reacts in a positive way to the adjustment and can provide an efficient solution on Ext3 as well as on XFS. The tuning results in decreasing the response time for CFQ in all the conducted benchmarks on both file systems. Although CFQ benefits from the tuning, the results for the other three implementations are inconclusive. Based on the profile, the tuning results in either a gain or loss in performance. Because CFQ is designed to operate on larger sets of I/O requests, the results reflect the scheduler's design goals. This is in contrast to the AS implementation, where by design, any read intensive workload cannot directly benefit from the change. On the other hand, for sequential write operations, AS can take advantage of the tuning as the response time decreases by 7% and 8% on Ext3 and XFS, respectively. The conducted benchmarks reveal another significant inefficiency behavior in the I/O subsystem, because the write performance for all the schedulers on Ext3 is significantly lower (by a factor of approximately 2.1) than on XFS. The issue here is the Ext3 reservation code. The Ext3 patches to resolve the issue are available at http://www.kernel.org .

Table 19-3 shows data from a RAID-5 8-way setup with $nr\_requests$ .

# Table 19-3. RAID-5 8-Way Setupnr_requests = 2,560Mean Response Time in Seconds (AS, Deadline, Noop, CFQ)