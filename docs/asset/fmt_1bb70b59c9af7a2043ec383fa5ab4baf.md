
### 监控 CPU 使用率，每 5 秒一次，持续 10 次：`sar -u 5 10`

### 监控内存使用：`sar -r 5 10`

### 分析结果以识别趋势和潜在瓶颈。

```
Linux 5.14.0-362.8.1.el9_3.x86_64 (localhost) 07/01/2025 _x86_64_ (a CPU)
10:55:16 %user %nice %system %iowait %steal %idle
10:55:16 2.50 0.00 1.25 0.50 0.00 95.75
Average: 2.50 0.00 1.25 0.50 0.00 95.75
```

列表 15.2：`sar` CPU 使用示例输出

` sar ` 命令用于历史性能分析的强大工具，允许管理员随时间监控 CPU 使用率和其他系统指标。通过通过定期间隔收集长期性能数据，它可以帮助识别长期趋势，例如反复出现的 CPU 峰值、内存泄漏或低利用率期间。这种历史视角支持主动的性能管理、准确的容量规划，并为扩展或优化系统资源提供明智的决策。

## 实验 3：使用 iostat 进行磁盘 I/O 监控

目标：使用 `iostat` 监控磁盘性能。

步骤：

- 1. 确保已安装 `sysstat`。
- 2. 运行以下命令查看磁盘利用率和响应时间：

  `iostat -x 5 10`
- 3. 识别利用率高或响应时间长的磁盘，这些可能意味着瓶颈。

```
Linux 5.14.0-362.8.el9_3.x86_64 (localhost) 07/01/2025
avg-cpu: %user %nice %system %owait %steal Idle
2.50 0.00 1.25 0.00 95.75
Device r/s w/s kB/s MB/s rr/s wrqm/s wrrq %wrqm r_await
  u_wait aqu-s rareq-s wareq-s svctm util
vme0n1 10.0 5.0 400.0 200.0 0.0 0.0 0.0 0.0 1.50 2.0 0.1 40.0
  40.0 0.5 3.6
```

列表 15.3：磁盘利用率 `iostat` 示例

磁盘 I/O 性能是数据密集型应用效率的关键因素。`iostat` 命令提供了有关磁盘活动的详细统计信息，包括读写速率、队列长度和响应时间。这些指标帮助管理员诊断现有硬件的有效性，并确定是否需要优化或升级。通过监控磁盘利用率趋势，`iostat` 为容量规划提供了科学的依据，并确保系统能够在不同的负载下维持应用性能。

系统监控和分析对于 Rocky Linux 的性能调优至关重要。通过使用 `top`、`sar` 和 `iostat` 等工具，管理员可以维护系统健康。

资源利用率以及跨不同环境的可预测的系统行为。

接下来，我们将使用以下命令安装软件包：

- `sudo dnf install fio -y`

# fio: 磁盘 I/O 基准测试

## 命令：

```
fio --name=test --rw=randread --bs=4k --size=512M --numjobs=1-
time_based --runtime=10s --group_reporting
```

```
test: (gid=0) /rw=randread; bs(R)=4096K, (W)=4096K, (T) 4096K-4096K; engine=inesync;iodep=1
fio:3.20
  1 process
  Writing out file (id 0 file 512M)
  job 1: (id=0) (time=10.00s, size=512.00M) [4096 IOPS] [lat 12.21 us/24.41 us/20.44 us]
  test: (groupid=0) job: (time=10.00s) [4096 IOPS] [lat 12.21 us/24.41 us/20.44 us]
  clat (use): min=96, max=1038, avg=254.09, stdev=104.08
  clat (use): min=96, max=1032, avg=252.32, stdev=102.64
  percentiles (use):
    10.00=98, 50.00=117, 90.00=147, 95.00=183, 99.00=267,
    30.00=99, 40.00=108, 60.00=126, 70.00=135, 80.00=161,
    85.00=176, 92.00=198, 94.00=231, 96.00=258, 97.00=301,
    98.00=444, 99.90=694, 99.99=1038
  test: (id=0) (time=10.00s, size=512.00M) [4096 IOPS] [lat 12.21 us/24.41 us/20.44 us]
  clat (use): min=96, max=1038, avg=254.09, stdev=104.08
  clat (use): min=96, max=1032, avg=252.32, stdev=102.64
  percentiles (use):
    10.00=98, 50.00=117, 90.00=147, 95.00=183, 99.00=267,
    30.00=99, 40.00=108, 60.00=126, 70.00=135, 80.00=161,
    85.00=176, 92.00=198, 94.00=231, 96.00=258, 97.00=301,
    98.00=444, 99.90=694, 99.99=1038
  cl: (use): min=0, max=0, avg=0, stdev=0
  sl: (use): min=0, max=0, avg=0, stdev=0
  10 depths
    0=0.00, 2=0.00, 4=0.00, 6=0.00, 8=0.00, 10=0.00, >=640=0.00
  complete:
    0=0.00, 50=0.00, 100=0.00, 150=0.00, 200=0.00, 250=0.00, >=640=0.00
  latency:
    target=0.00, percentile=0.00, max=00us
```

Running test with 1 job

READ: 15.2GB(15.9MB/s), WRITE: 15.2GB(15.9MB/s), IOPS=1599(1000-100sec)

Disk stats (read/write)

dev=nvme0n1 read=76953, in_queue=7952, util=11.7%, aggrios=38922/9, aggmerge=0/1, aggricks=7887/4,

write=780, in_queue=7890, util=99.02%

You have new files in /var/lib/aio/context

> 图 15.5：`fio` 随机性能测试输出

此图显示了使用 `fio`、`4K` 块大小、`512MB` 文件执行的 10 秒随机读取测试的结果。输出突出了性能指标：带宽 `15.2 MB/s`，平均 IOPS 为 `3912`，延迟显示大多数读取操作在 `500 微秒`内完成，表明延迟较低。磁盘利用率数据进一步证实了设备在测试期间接近饱和，反映了持续的高 I/O 负载。这些指标共同为随机负载下的存储行为提供了宝贵的见解，对于容量规划和性能调优至关重要。

# iostat: CPU 和磁盘利用率

```
Command: Linux 5.14.0-427.421.11_x86_64 (local)

CPU:
%user     %nice   %system   %iowait  %idle     %steal
0.00      0.00    0.00      0.00     99.02     0.00

Device:
             read_s     write_s     read_kB/s     write_kB/s  util%  avg-sz
nvme0n1      769.53       7.80      769.53        7.80   11.70  0.00
```

- • 保存更改并重启虚拟机。

## 验证 CPU 型号和频率配置

在进行高级配置之前，验证处理器架构至关重要，以确保与所需的优化具有兼容性。验证 CPU 型号和频率配置有助于管理员理解硬件能力和局限性，确保任何调优都符合系统规范。通过使用 `lspcu` 和 `cat /proc/cpuinfo` 等命令，管理员可以收集有关 CPU 型号、核心数和频率设置的必要细节。这些信息对于确定最有效的性能调优策略至关重要，无论是调整 CPU 缩放、启用特定功能，还是配置电源管理选项以增强系统性能。
