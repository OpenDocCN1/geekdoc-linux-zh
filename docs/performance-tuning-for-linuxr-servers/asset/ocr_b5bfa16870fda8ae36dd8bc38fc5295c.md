```
```
sdp    0.00    0.01    0.00    378     24
sdo   59.49 2883.87  0.90 158937034 49520
```
```

`iostat` reports CPU utilization similar to how it is provided by the `top` tool. It splits the CPU time into user, nice, system, I/O wait, and system idle. It is followed by the disk utilization report. The disk header is followed by lines of disk statistics, where each line reports the activities of one logical disk that is configured. The `tps` column represents the number of I/O requests that are issued to the logical disk. However, the size of the I/O requests is not given. `Blk read/s` and `Blk wrtn/s` represent the amount of data read from and written to the logical drive in a number of blocks per second. Again, the block size is not given. Finally, `Blk read` and `Blk writn` correspond to the amount of data read from and written to the logical drive in a number of blocks per second, without specifying the block’s size.

The `-k` option displays statistics in kilobytes, the `-p` option gets per-partition statistics, and the `-x` option gets information such as average wait time and average service time. In the data, the count on `Blk read` of `sdo` is very close to the count of `Blk writn` of `sda`, as data is copied from `sda7` to `sdo1`. In addition, the rate of reads is slightly higher than the rate of writes. This report can highlight disk I/O bottlenecks, if any, and helps database designers lay out data to achieve higher access parallelism.

# ## sar

`sar` is included in the `sysstat` package. `sar` collects and reports a wide range of system activities in the operating system. Activities include I/O operations, CPU utilization, the rate of context switches and interrupts, the rate of paging in and paging out, and the use of shared memory, buffer, and network. Based on the values in the count and interval parameters, `sar` writes information the specified number of times spaced at the specified intervals in seconds. For example, the command `sar b 3 12` reports disk usage every 3 seconds for a total of 12 seconds. In addition, at the end of data collection, average statistics are given. `sar` is a very option-rich tool. The remainder of this section discusses a few features of the tool:

+   *   `sar` displays I/O statistics similar to `iostat`. `sar` provides the total number of I/O operations (`tps`), which is further split into read operations (`rtps`) and write operations (`wtps`). `sar` also provides the rates of read and write operations under `bread/s` and `bwrtn/s`. The following data is collected every 2 seconds for a total of 18 seconds. At the end of the data collection, the averages of five fields are given. However, operations for individual logical drives are not given.

```
```
12:59:15       tps     rtps     wtps    bread/s    bwrtn/s
12:59:17     37.50    0.00    396.00      0.00      0.00
12:59:19     66.50    66.50   0.00   16140.00      0.00
12:59:21    268.50   268.50   0.00   66560.00      0.00
12:59:23    333.50   261.50  72.00   64548.00    9620.00
12:59:25    153.50    40.50 113.00   9728.00   27984.00
12:59:27    133.00     5.00 128.00   1024.00   31744.00
12:59:29    119.50     7.50 112.00   1536.00   27776.00
12:59:31    133.00     5.00 128.00   1024.00   31744.00
Average:     155.63    86.50  69.13   20119.50  16108.50
```
```

+   *   `sar` provides data on CPU utilization for individual processors as well as for the whole system. This particular feature is especially useful in multiprocessor environments. If some processors do more work than others, the display clearly shows. You can then check