

![](img/c0a399aca0d18f8822d714ad0a173123_654_0.png)

如果您发现系统中未安装 `iostat` 实用程序，请安装 `sysstat` 软件包以获取它。软件包安装在第 13 章中已进行过介绍。

`iostat` 命令的语法如下：

```
iostat  [OPTION]  [INTERVAL]  [COUNT]
```

如果您直接在命令行输入 `iostat` 并按下回车键，您将看到系统自启动以来 CPU、文件系统和分区统计信息的静态摘要。然而，在故障排除情况下，这样做并没有太大价值。有几个有用的 `iostat` 选项可用于故障排除：

- `-y`: 不包含初始的“自系统启动以来”统计信息。
- `-N`: 显示逻辑卷的已注册设备映射名称。
- `-z`: 不显示没有活动的设备。
- `-p device`: 仅显示有关此设备的信息。

`iostat` 命令的两个参数允许随时间查看统计数据。[INTERVAL] 参数指定每次显示之间的间隔秒数，[COUNT] 设置显示次数。请记住，如果使用 `-y` 选项，在设定的间隔之后您才会看到第一批统计数据。

图 20.14 中的片段展示了一个使用 `iostat` 及适用于故障排除情况的适当选项的示例。在这种情况下，仅显示两个间隔 5 秒的统计数据。您可以看到 I/O 等待（`%iowait` 列）百分比相当高，这表明存在潜在问题。

### **图 20.14：** 使用 `iostat` 实用程序排查 I/O 等待问题

```
$ iostat -ynz 5 2
[...]
avg-cpu:  %user   %nice  %system  %iowait  %steal  %idle
          26.80     0.00     42.27     30.93     0.00     0.00

Device:            tps     kB_read/s     kB_wrtn/s     kB_read     kB_wrtn
sda               409.90          3.30       9720.72         16       47145
[...]
avg-cpu:  %user   %nice  %system  %iowait  %steal  %idle
          22.67     0.00     65.79     11.54     0.00     0.00

Device:            tps     kB_read/s     kB_wrtn/s     kB_read     kB_wrtn
sda               535.83          0.00       9772.77          0       48277
[...]
```

![](img/c0a399aca0d18f8822d714ad0a173123_655_0.png)

要定位导致高 I/O 的应用程序或进程，请使用 `iostat` 实用程序。它通常不会默认安装，但包含在 `sysstat` 软件包中。

对于高 I/O 问题，除了采用不同的磁盘技术外，您还需要审查 Linux 内核定义的*I/O 调度*。I/O 调度是一系列处理 I/O 请求及其相关活动的内核操作。这些操作如何执行取决于在配置文件中选择特定的 I/O 调度器，如图 20.7 所示。

### 图 20.7 I/O 调度器

| 名称 | 描述 |
| --- | --- |
| cfq | 为每个进程创建队列，并在循环中处理各个队列，同时为读请求提供比写请求更高的优先级。当需要更平衡的 I/O 处理和/或系统具有多处理器时，此调度器效果很好。 |
| deadline | 批量处理磁盘 I/O 请求，并尝试在指定时间内处理每个请求。当需要增加数据库 I/O 并降低整体 I/O 延迟时，和/或使用了 SSD 时，和/或正在使用实时应用程序时，此调度器效果很好。 |
| noop | 将所有 I/O 请求放入单个 FIFO 队列并按顺序处理。当需要更低的 CPU 使用率和/或使用了 SSD 时，此调度器效果很好。 |

用于确定使用哪个 I/O 调度器的配置文件位于与每个磁盘关联的目录中。图 20.15 展示了如何在 Rocky Linux 发行版中找到各个磁盘目录及其关联的调度器文件。

### 图 20.15：定位磁盘的调度器文件

```bash
# ls /sys/block
dm-0 dm-1 sda sdb sdc sdd sr0
#
# cat /sys/block/sda/queue/scheduler
[mq-deadline] kyber bfq none
#
```

用于 sda 磁盘的调度器 mq-deadline 显示在方括号中。要更改当前的 I/O 调度器，只需使用超级用户权限和 `echo` 命令，如图 20.16 所示。

![](img/c0a399aca0d18f8822d714ad0a173123_655_0.png)

### 图 20.16：临时更改磁盘的调度器文件

```
# echo "bfq" > /sys/block/sda/queue/scheduler
# cat /sys/block/sda/queue/scheduler
mq-deadline kyber [bfq] none
#
```

如果您确定由于硬件限制，需要更换不同的新硬盘来处理所需的 I/O 级别，*ioping* 实用程序可以帮助您在测试过程中。*ioping* 实用程序通常不会默认安装，但通常可以在发行版的标准软件仓库中找到。

> *ioping* 实用程序可能会破坏磁盘上的数据！在使用该命令之前，请务必彻底理解其选项。如果您希望更安全的选择，请查看 *stress-ng* 工具。该实用程序允许您对磁盘、网络、系统 CPU 等进行压力测试。

使用 *ioping* 命令，您可以测试磁盘 I/O 延迟、寻道速率和顺序速度。您还可以尝试异步、缓存和直接 I/O 速率。图 20.17 中的片段示例展示了一个使用 *ioping* 命令从临时文件中读取随机数据块（非缓存）的简单测试。

### 图 20.17：使用 *ioping* 实用程序进行非缓存读取测试

```
# ioping -c 3 /dev/sda
4 KiB <<< /dev/sda [...]: request=1 time=20.7 ms (warmup)
4 KiB <<< /dev/sda [...]: request=2 time=32.9 ms
4 KiB <<< /dev/sda [...]: request=3 time=25.5 ms
--- /dev/sda (block device 15 GiB) ioping statistics ---
2 requests completed in 58.4 ms, 8 KiB read, 34 iops, 137.0 KiB/s
generated 3 requests in 2.03 s, 12 KiB, 1 iops, 5.92 KiB/s
min/avg/max/mdev = 25.5 ms / 29.2 ms / 32.9 ms / 3.72 ms
#
```

添加的 *-c 3* 选项指定了三次测试。更彻底的 *ioping* 测试有助于确定磁盘是否适合特定应用程序的需求。

## 测量磁盘性能

有助于确定磁盘驱动器整体 I/O 性能的一个基准测试是每秒输入/输出操作次数（IOPS）值。该值是存储设备每秒可以执行的输入或输出操作数量。IOPS 值不仅提供了一种评估磁盘驱动器性能的方法，还可以比较不同类型的存储，例如单个 SATA 或 SSD 驱动器与 RAID 或 LVM 设置。

在 Linux 环境中，用于确定 IOPS 值的流行工具是一个称为 fio 的灵活 I/O 工具。该工具在基于 Debian 和基于 Red Hat 的软件仓库中均可用作 `fio` 软件包，并且必须手动安装。

`fio` 工具对您指定的文件和目录执行多次读写操作，并指定您定义的文件大小和块大小。文件越大，获得的 IOPS 读数越准确。图 20.18 展示了在磁盘上执行 `fio` 测试的一个示例。

### **图 20.18：** 使用 `fio` 工具确定磁盘 I/O

```
# fio --randrepeat=1 --ioengine=libaio --direct=1
   --gtod_reduce=1 --name=fiotest --filename=fiotest --bs=4k
   --iodepth=64 --size=1G --readwrite=randrw --rwmxread=75

fiotest: (g=0): rw=randrw, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.19
Starting 1 process
fiotest: Laying out IO file (1 file / 1024MiB)
[...]
    read: IOPS=23.4k, BW=91.4MiB/s (95.9MB/s) (768MiB/8396msec)
      bw ( KiB/s): min=63425, max=101451, per=99.97%, avg=93588.81,
      stdev=9628.66, samples=16
    iops : min=15856, max=25362, avg=23396.88, stdev=2407.19, samples=16
   write: IOPS=7818, BW=30.5MiB/s (32.0MB/s) (256MiB/8396msec); 0 zone resets
      bw ( KiB/s): min=22658, max=33712, per=99.91%, avg=31245.31,
      stdev=2927.74, samples=16
    iops : min= 5664, max= 8428, avg=7811.06, stdev=732.05, samples=16
    cpu    : usr=2.80%, sys=34.02%, ctx=3045, majf=0, minf=7
    IO depths    : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
               submit: 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
               complete: 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
    issued rwt: total=196498,65646,0,0 short=0,0,0,0 dropped=0,0,0,0
    latency   : target=0, window=0, percentile=100.00%, depth=64
[...]
#
```

