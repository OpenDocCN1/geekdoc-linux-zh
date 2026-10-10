
## iotop

**Purpose:** Monitor disk input and output operations.

**Usage syntax:** `iotop [OPTIONS]`

```
$ iotop
Total DISK READ: 52.68 M/s | Total DISK WRITE: 0.00 B/s
TID  PRIO USER  DISK READ DISK WRITE  SWAPIN     IO>  COMMAND
4310 be/4 root  9.33 M/s  0.00 B/s  0.00 %   0.00 %  hdparm -Tt
4311 be/4 root  4.84 M/s  0.00 B/s  0.00 %   0.00 %  hdparm -Tt
4312 be/4 root  9.46 M/s  0.00 B/s  0.00 %   0.00 %  hdparm -Tt
4313 be/4 root  13.68 M/s 0.00 B/s  0.00 %   0.00 %  hdparm
1 be/4 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  init
2 be/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [kthread]
3 rt/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [migration/0]
4 be/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [ksoftirqd/0]
5 rt/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [watchdog/0]
6 be/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [events/0]
7 be/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [cpuset]
8 be/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [khelper]
9 be/3 root    0.00 B/s  0.00 B/s  0.00 %   0.00 %  [netns]
10 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [async/mgr]
11 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [blkcg_mgd/0]
12 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [kblockd/0]
13 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [kapci]
14 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [kacpi_notify]
15 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [kacpi_hotplug]
16 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [ata/0]
17 be/3 root   0.00 B/s  0.00 B/s  0.00 %   0.00 %  [ata_aux]
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_204_0.png)

`iotop` is a utility for monitoring disk I/O operations on Linux systems. It can be useful for monitoring disk performance and tracking down resource-intensive applications. The example above displays the default `iotop` interface.

> **Tip** Press the Q key to exit the `iotop` utility.

**Common usage examples:**

- `iotop`: Monitor system I/O statistics
- `iotop -o`: Only display processes performing I/O
- `iotop -u [USER]`: Only display I/O activity from the specified user
- `iotop -d [SECONDS]`: Update at the specified interval (in seconds)

## mpstat

**Purpose:** Display processor utilization information.

**Usage syntax:** `mpstat [OPTIONS] [DELAY] [COUNT]`

```
$ mpstat 2 10
Linux 2.6.24-19-server (vmware-02)    05/03/2010

10:46:53 AM  CPU  %user  %nice  %sys  %iowait  %irq  %soft  %idle  intr/s
10:46:55 AM  all  0.00   0.00    2.22  0.00      0.00  0.00   0.00  97.78  82.50
10:46:57 AM  all  0.62   0.00    2.49  0.00      0.00  0.00   0.00  96.89  126.50
10:46:59 AM  all  0.12   0.00    2.21  0.00      0.00  0.12   0.00  97.54  84.00
10:47:01 AM  all  0.25   0.00    5.29  0.00      0.00  0.12   0.00  93.73  403.00
10:47:03 AM  all  0.00   0.00    2.55  0.00      0.00  0.00   0.00  97.45  106.50
10:47:05 AM  all  0.25   0.00    2.84  0.00      0.00  0.00   0.00  96.91  101.50
10:47:07 AM  all  0.00   0.00    3.28  0.00      0.00  0.00   0.00  96.72  118.00
10:47:09 AM  all  0.24   0.00    3.40  0.00      0.00  0.00   0.00  96.36  126.00
10:47:11 AM  all  0.00   0.00    3.91  0.00      0.00  0.00   0.00  96.09  97.50
10:47:13 AM  all  0.00   0.00    3.27  0.00      0.00  0.00   0.00  96.61  107.00
Average:      all  0.15   0.00    3.15  0.06      0.02  0.01   0.00  96.61  135.25

          Output of the mpstat command
```

`mpstat` displays processor utilization information on Linux systems. In the above example, executing `mpstat 2 10` instructs the program to display results in two-second intervals and exit after displaying 10 lines. If the delay and count options are omitted, `mpstat` will display one line of results and then terminate.

**Common usage examples:**

- `mpstat`: Display processor utilization once and exit
- `mpstat [DELAY]`: Update display at the specified interval
- `mpstat [DELAY] [COUNT]`: End monitoring after reaching the specified count

## vmstat

**Purpose:** Display virtual memory usage information.

**Usage syntax:** `vmstat [OPTIONS] [DELAY] [COUNT]`

```
# vmstat 2 10
    r b swpd     free    buff       cache  si so bi bo   in cs us sy id wa
    0 0  88  79260  149184     7400704  0  0  0  93    1  4  0  97  0
    0 1  88  78996  149184     7400704  0  0  0 2  119 2933  0  90  6
    2 0  88  78996  149184     7400704  0  0  0 12  115 3083  0  94  3
    0 0  88  78872  149184     7400704  0  0  0 1828  259 3275  0  97  0
    0 0  88  78872  149184     7400704  0  0  0 62  145 3031  0  96  0
    0 0  88  78748  149184     7400704  0  0  0 0  114 2965  0  98  0
    0 0  88  78452  149184     7400704  0  0  0 438  150 3170  0  97  0
    0 0  88  78004  149184     7400704  0  0  0 0  114 3073  0  97  0
    0 0  88  77762  149184     7400704  0  0  0 130  306 4469  0  95  0
    0 0  88  77260  149184     7400708  0  0  0 52  130 2864  0  97  0
```

The `vmstat` command displays virtual memory statistics. In the above example, executing `vmstat 2 10` instructs the program to display results in two-second intervals and exit after displaying 10 lines. If the delay and count parameters are omitted, `vmstat` will display one line of results and then terminate.

> **Tip** The `-Sm` option can be used with the `vmstat` command on some systems to display the memory totals in megabytes instead of kilobytes.

**Common usage examples:**

- `vmstat`: Display memory utilization once and exit
- `vmstat [DELAY]`: Update results at the specified interval
- `vmstat [DELAY] [COUNT]`: End after reaching the specified count
- `vmstat -s`: Display a table of memory statistics
- `vmstat -Sm`: Display utilization in megabytes

## iostat

**Purpose:** Display I/O utilization statistics.

**Usage syntax:** `iostat [OPTIONS] [DELAY] [COUNT]`

```
# iostat -d 2 5
Linux 2.6.24-19-server (vmware-02) 05/03/2010
Device: tps Blk_read/s Blk_wtrn/s Blk_read Blk_wtrn
sda 56.65 3.44 756.95 9462264 2080033488
Device: tps Blk_read/s Blk_wtrn/s Blk_read Blk_wtrn
sda 3.50 0.00 64.00 0 128
Device: tps Blk_read/s Blk_wtrn/s Blk_read Blk_wtrn
sda 6.97 0.00 59.70 0 120
Device: tps Blk_read/s Blk_wtrn/s Blk_read Blk_wtrn
sda 0.00 0.00 0.00 0 0
Device: tps Blk_read/s Blk_wtrn/s Blk_read Blk_wtrn
sda 61.50 0.00 524.00 0 1048
Displaying I/O utilization using the iostat command
```

The `iostat` command displays I/O utilization statistics for disk drives and network file systems. It is helpful in monitoring disk drives as they can be a significant bottleneck in system performance. In the above example, five lines of I/O statistics are displayed. The first line displays the statistics since the system was last booted. Subsequent lines display the totals since the previous line was printed.

**Common usage examples:**

- `iostat`: Display I/O utilization once and exit
- `iostat [DELAY]`: Update I/O utilization at the specified interval
- `iostat [DELAY] [COUNT]`: End after reaching the specified count
- `iostat -k`: Display statistics in kilobytes per second
- `iostat -m`: Display statistics in megabytes per second
- `iostat -d`: Display only I/O devices
- `iostat -P`: Display each partition individually
- `iostat -n`: Display NFS I/O utilization

## dstat

**Purpose:** Monitor CPU, disk, network, and swap utilization.

**Usage syntax:** `dstat [OPTIONS] [DELAY] [COUNT]`

```
$ dstat 2 10

---total--- -cpu-usage---- -disk/total- -net/total- ---paging-- ---system---
usr sys idle wai hiq sirq read writx rcv send in out int csw
0 2 97 0 0 0 |1763B 379k| 0 0 | 0 | 131 2611
0 9 91 0 0 0 | 0 0 |346k 99k| 0 0 | 482 4748
0 3 97 0 0 0 | 0 410k| 141k 16k| 0 0 | 125 3189
0 3 97 0 0 0 | 0 0 | 55k 9090B| 0 0 | 114 3054
0 3 96 0 0 0 | 0 0 | 55k 9.9k| 0 0 | 100 2723
0 4 96 0 0 0 | 0 376k| 63k 11k| 0 0 | 115 2904
0 3 96 0 0 0 | 0 0 | 55k 9.8k| 0 0 | 127 3221
0 2 98 0 0 0 | 0 182k| 64k 13k| 0 0 | 135 3067
0 2 97 0 0 0 | 0 0 | 55k 10k| 0 0 | 115 2925
0 4 96 0 0 0 | 0 0 | 54k 9832B| 0 0 | 118 3129
0 13 87 0 0 0 | 0 94k| 37k 11k| 0 0 | 548 4950
```

`dstat` is an all-in-one performance monitoring utility for Linux systems. The above example demonstrates the default output of `dstat` which displays CPU, disk, network, and swap utilization in a single and easy-to-read display.

> **Tip** `dstat` output can be custom-tailored to your needs using a number of command line options. See man dstat for more information.

**Common usage examples:**

- `dstat`: Monitor system utilization
- `dstat [DELAY]`: Update results at the specified interval
- `dstat [DELAY] [COUNT]`: End monitoring after reaching the specified count
