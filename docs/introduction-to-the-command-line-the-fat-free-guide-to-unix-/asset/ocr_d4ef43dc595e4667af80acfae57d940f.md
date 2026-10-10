# iostat

**Purpose**: Display I/O utilization statistics.

**Usage syntax**: `iostat [OPTIONS] [DELAY] [COUNT]`

```
# iostat -d 2 5
Linux 2.6,24-19-server (vmware-02)    05/03/2010

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda            56.65        3.44         756.95      9462264    2080033488

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda             3.50        0.00          64.00            0           128

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda             6.97        0.00          59.70            0           120

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda             0.00        0.00           0.00            0             0

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda            61.50        0.00         524.00            0          1048

Displaying I/O utilization using the iostat command
```

The **iostat** command displays I/O utilization statistics for disk drives and network file systems. It is helpful in monitoring disk drives as they can be a significant bottleneck in system performance. In the above example, five lines of I/O statistics are displayed. The first line displays the statistics since the system was last booted. Subsequent lines display the totals since the previous line was printed.

+   **Common usage examples:**
+   `iostat` Display I/O utilization once and exit
+   `iostat [DELAY]` Update I/O utilization at the specified interval
+   `iostat [DELAY] [COUNT]` End after reaching the specified count
+   `iostat -k` Display statistics in kilobytes per second
+   `iostat -m` Display statistics in megabytes per second
+   `iostat -d` Only display I/O devices
+   `iostat -P` Display each partition individually
+   `iostat -n` Display NFS I/O utilization