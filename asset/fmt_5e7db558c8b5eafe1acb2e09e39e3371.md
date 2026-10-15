
以下字段显示在表 6.3 中（较大的终端尺寸会显示所有字段）：

| 字段 | 描述 |
| --- | --- |
| `busy` | 单元忙于处理请求的时间占比 |
| `read` | 发出的读取请求数量 |
| `write` | 发出的写入请求数量 |
| `discd` | 发出的释放（discard）请求数量 |
| `KiB/r` | 每次读取的千字节数（Kibbytes） |
| `KiB/w` | 每次写入的千字节数（Kibbytes） |
| `KiB/d` | 每次释放（discard）的千字节数（Kibbytes） |
| `MBr/s` | 读取吞吐量（每秒百万字节数，Mebibytes） |
| `MBw/s` | 写入吞吐量（每秒百万字节数，Mebibytes） |
| `avq` | 平均队列深度 |
| `avio` | 请求所需的寻道、延迟和数据传输的平均毫秒数。 |

**表 6.3: 命令 `atop` 的字段描述**

### 命令 `smartctl`

现代磁盘包含一个名为**自我监测、分析和报告技术（S.M.A.R.T）**的监控系统，其中包含不同的指标以预测硬件故障。主要命令是 `smartctl`，指定磁盘后会显示与磁盘相关的扩展信息。图 6.36 和 6.37 使用不同的选项来过滤显示的信息，以减少输出行数：

- 图 6.36 显示磁盘信息，包括型号/序列号和固件版本：

```
[root@server2 ~]# smartctl -i /dev/nvme0n1

smartctl 7.1 2020-04-05 r5049 [x86_64-linux-4.18.0-372.9.1.el8.x86_64] (local build)

Copyright (C) 2002-19, Bruce Allen, Christian Franke, www.smartmontools.org

=== 信息部分开始 ===

型号编号: INTEL SSDPEKKF512G8L

序列号: PHHH04800BY5512H

固件版本: L15P

PCI 供应商/子系统 ID: 0x8086

IEEE OUI 标识符: 0x5cd2e4

控制器 ID: 1

命名空间数量: 1

命名空间 1 大小/容量: 512.110.190.592 [512 GB]

命名空间 1 格式化 LBA 大小: 512

命名空间 1 IEEE EUI-64: 5cd2e4 259140262f

本地时间是: 2022 年 8 月 14 日 星期日 12:11:25 CEST
```

![](img/863afa537de4eed7deb11978bfbfa90e_203_0.png)

- 显示包含已写入和读取的数据、温度以及与其他使用空间相关的信息的 SMART 信息，如图 6.37 所示：

```
[root@server2 ~]# smartctl -A /dev/nvme0n1

smartctl 7.1 2020-04-05 r5049 [x86_64-linux-4.18.0-372.9.1.el8.x86_64] (local build)

Copyright (C) 2002-19, Bruce Allen, Christian Franke, www.smartmontools.org

=== SMART 数据部分开始 ===

SMART/健康信息 (NVMe Log 0x02)

关键警告: 0x00

温度: 33 摄氏度

可用备用空间: 100%

可用备用空间阈值: 12%

使用百分比: 8%

数据读取单元: 66.386.661 [33.9 TB]

数据写入单元: 58.888.607 [30.1 TB]

主机读取命令: 567.421.451

主机写入命令: 1.875.052.632

控制器忙碌时间: 68.306

电源循环次数: 2.921

通电小时数: 11.370

非安全关机次数: 161

媒体和数据完整性错误: 0

错误信息日志条目: 0

警告组件温度时间: 0

关键组件温度时间: 0
```

**图 6.37: 命令 `smartctl` 的输出示例**

使用选项 `-l error` 将显示由 SMART 监控系统检测到的错误。

### 命令 `fio` 和 `hdparm`

这些命令可用于查询存储设备的读/写速度，是检测磁盘问题的有用工具。命令 `hdparm` 带有选项 `-tT` 的输出显示在图 6.38 中：

```
[root@server2 ~]# hdparm -tT /dev/nvme0n1

/dev/nvme0n1:

测试缓存读取: 10064 MB 用时 1.99 秒 = 5047.98 MB/秒

测试缓冲磁盘读取: 3074 MB 用时 3.00 秒 = 1024.60 MB/秒
```

**图 6.38: 命令 `hdparm` 的输出示例**

命令 `fio` 是一个灵活的输入/输出测试器。它比 `hdparm` 更先进，因为它允许我们指定执行 I/O 操作的线程和进程数量。图 6.39（输出已截断）展示了该命令使用四个作业测试随机读写时的运行情况：

```
[root@server2 ~]# fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test.fio --bs=4k --iodepth=64 --size=4G --readwrite=randrw --numjobs=4

test: (g=0): rw=randrw, bs=(R) 4096b-4096b, (W) 4096b-4096b, (T) 4096b-4096b, ioengine=libaio, iodepth=64

...

fio-3.19

正在启动 4 个进程

test: 布局 IO 文件 (1 个文件 / 4096MiB)

作业: 4 (f=4): [m(4)][96.2%] r=384MiB/s,w=383MiB/s [r=98.2K,w=98.2K iops] [eta 00m:02s]

运行状态组 0 (所有作业):

  读取: bw=164MiB/s (171MB/s), 40.8MiB/s-41.0MiB/s (42.8MB/s-42.9MB/s), io=8192MiB (8590MB), run=49990-50089msec

 写入: bw=164MiB/s (171MB/s), 40.9MiB/s-40.9MiB/s (42.9MB/s-42.9MB/s), io=8192MiB (8590MB), run=49990-50089msec

磁盘统计 (读取/写入):

 dm-1: ios=207688/2076846, merge=0/0, ticks=703954/4020718, in_queue=11051672, util=99.53%, aggrios=2097185/

 2100015, aggmerge=0/0, aggticks=7047507/4054918, aggrin_queue=11102425, aggrutil=98.54%

 dm-0: ios=2097185/2100015, merge=0/0, ticks=7047507/4054918, in_queue=11102425, util=98.54%, aggrios=2097185/

 2098583, aggmerge=0/1459, aggticks=6444743/3063238, aggrin_queue=9507982, agrutil=98.31%

 nvme0n1: ios=2097185/2098583, merge=0/1459, ticks=6444743/3063238, in_queue=9507982, util=98.31%
```

**图 6.39: 命令 `fio` 的输出示例**

### 命令 `df` 和 LVM 命令

在第 3 章 使用命令行界面中描述的命令 `df` 显示磁盘空闲空间和使用情况。如果系统使用 LVM（逻辑卷管理器），检查状态的命令如下：

- `vgdisplay`: 如图 6.40 所示，显示卷组信息：

```
[root@server2 ~]# vgdisplay 2>/dev/null

 --- 卷组 ---

  VG 名称       RHELC5B

  系统 ID

  格式        lvm2

  元数据区域   1

  元数据序列号 11

  VG 访问   读/写

  VG 状态   可调整大小

  最大 LV      0

  当前 LV      3

  打开的 LV     3

  最大 PV      0

  当前 PV      1

  活动 PV      1

  VG 大小     499,98 TiB

  PE 大小     4,00 MiB

  总 PE    131067903

  已分配 PE / 大小 59392 / 232,00 GiB

  空闲 PE / 大小 131008511 / <499,76 TiB
```
