
```
Sat Jun 28 02:57:08 PDT 2003
....+..*......+...*......+...*..+....+*..+...+****
+30 clients started
Throughput 18.9072 MB/sec (NB=23.634 MB/sec
189.072 MBit/sec)
Sat Jun 28 03:00:38 PDT 2003
```

当添加 `logbufsize` 和 `logbsize` 挂载选项时，吞吐量从 1.45512 MBps 增加到 1.97025 MBps。当日志被移动到外部设备时，吞吐量增加到 18.9072 MBps。显然，在一个具有大量元数据活动的测试程序中，外部日志提高了文件系统的性能。

### 测量 I/O

`systat` 软件包包含 `sar` 和 `iostat` 命令。`sar` 命令收集和报告系统活动信息。`iostat` 命令报告磁盘的 CPU 利用率和 I/O 统计信息。

以下小节详细讨论 `iostat` 命令，并描述如何使用 `iostat` 和 `sar` 来分析和报告 I/O 及 CPU 的利用率和分配情况。

### iostat

`iostat` 命令通过观察设备处于活动状态的时间与其平均传输速率的关系，来监控系统输入输出设备的负载。该命令生成的报告可用于更改系统配置，以更好地平衡物理磁盘之间的输入输出负载。

与大多数监控命令一样，`iostat` 输出的第一行反映的是自启动以来统计信息的汇总。为了查看有意义的实时数据，请在运行 `iostat` 时指定时间戳，并查看报告时间段间隔汇总的行。通过查看读取或写入驱动的字节统计信息，`iostat` 可以提供一种在物理硬盘之间平衡负载的方法。

当字节被读取或写入时，`iostat` 报告以下信息：

- `tps`。每秒传输次数。
- `device`。磁盘设备名称。
- `Blk_read/s`。从设备读取的数据量，以每秒块数表示。
- `Blk_wrtm/s`。写入设备的数据量，以每秒块数表示。
- `Blk_read`。读取的总块数。
- `Blk_wrtm`。写入的总块数。
- `kB_read/s`。从设备读取的数据量，以每秒千字节数表示。
- `kB_wrtm/s`。写入设备的数据量，以每秒千字节数表示。
- `kB_read`。读取的总千字节数。
- `kB_wrtm`。写入的总千字节数。
- `rrqm/s`。每秒合并并发送到设备的读取请求数。
- `wrrm/s`。每秒合并并发送到设备的写入请求数。
- `r/s`。每秒发送到设备的读取请求数。
- `w/s`。每秒发送到设备的写入请求数。
- `rsec/s`。每秒从设备读取的扇区数。
- `wsec/s`。每秒写入设备的扇区数。
- `rkB/s`。每秒从设备读取的千字节数。
- `wkB/s`。每秒写入设备的千字节数。
- `avgrq-sz`。发送到设备的请求的平均大小（以扇区计）。
- `avgqu-sz`。平均队列长度。

### 使用 iostat 和 sar 实用程序

Linux 的 `iostat` 和 `sar` 实用程序通过分析磁盘和 CPU 使用情况的同步逐间隔配置，来分析并报告 I/O 和 CPU 的利用率和分配情况。如果在高负载或系统性能不足的期间使用这些实用程序，它们可以指示哪个系统资源可能限制了整体系统性能。在识别出系统瓶颈后，可以采取针对性的措施来提高系统性能。

以下示例演示了在 `/dev/hda1` 设备上执行 `iostat` 的过程并展示了输出结果。

```
##### iostat -x /dev/hda1
Linux 2.4.20-4GB
avg-cpu:  %user   %nice   %sys  %idle
           0.67    0.00   0.18  99.15
Device:      rrqm/s wrqm/s r/s  w/s rsec/s  wsec/s  rkB/s  wkB/s avgrq-sz avgqu-sz
             await  svctm   %util
/dev/hda1    0.00   0.00  0.00 0.00   0.03    0.01   0.01   0.00    8.71    0.01
            199.71  199.41  0.08
```

此示例说明了执行 `tiobench` 以在 `/dev/hda1` 设备上产生文件系统活动的过程。

```
##### date && ./tiobench.pl --size 500 --numruns 5 --threads 32 && date
Fri Jun 27 05:41:03 PDT 2003
Run #1: ./tiotest -t 32 -f 15 -r 125 -r 4096 -d . -T
Run #2: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #3: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #4: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #5: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Unit information
====================
File size = megabytes
Blk Size = bytes
Rate = megabytes per second
CPU% = percentage of CPU used during the test
Latency = milliseconds
Lat% = percent of requests that took longer than
X seconds
CPU Eff = Rate divided by CPU% - throughput per cpu load

Sequential Reads
File  Blk  Num        Avg     Maximum   Lat%
      CPU  Size  Size Thr  Rate  (CPU%) Latency Latency  >2s
Identifier  Eff
>10s   Eff
---  - -
---  - -
2,4,20-4GB 500 4096 32 10.46 4.810% 22,227 20407.44 0.11800 
 0.00000 217

Random Reads
File  Blk  Num        Avg     Maximum   Lat%
      CPU  Size  Size Thr  Rate  (CPU%) Latency Latency  >2s
Identifier  Eff
>10s   Eff
---  - -
---  - -
2,4,20-4GB 500 4096 32 0.75 0.715% 438.919 1926.01 0.00000 
 0.00000 104

Sequential Writes
File  Blk  Num        Avg     Maximum   Lat%
      CPU  Size  Size Thr  Rate  (CPU%) Latency Latency  >2s
Identifier  Eff
>10s   Eff
---  - -
---  - -
2,4,20-4GB 500 4096 32 2.94 3.460% 1.798 9288.13 0.02279 0
 0.00000 85

Random Writes
File  Blk  Num        Avg     Maximum   Lat%
      CPU  Size  Size Thr  Rate  (CPU%) Latency Latency  >2s
Identifier  Eff
>10s   Eff
---  - -
---  - -
2,4,20-4GB 500 4096 32 0.50 1.081% 0.198 206.05 0.00000 0
 0.00000 46
```

`tiobench` 完成后，再次运行 `iostat` 以查看该程序产生的磁盘活动。此处展示了 `iostat` 输出的示例：
