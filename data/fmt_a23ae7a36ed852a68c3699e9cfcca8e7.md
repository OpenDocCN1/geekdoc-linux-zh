
`run-sz`（运行队列大小）表示在处理器队列上等待执行的进程数；对于 Intel 架构，该数字平均二或更小。

> 注意：`run-sz` 长时间远大于二，说明 CPU 响应系统请求太慢。

`plist-sz`（进程列表大小）值表示内存中运行的进程数量，`1davg-1`（1 分钟平均负载）、`1davg-5`（5 分钟平均负载）和 `1davg-15`（15 分钟平均负载）分别代表过去 1 分钟、5 分钟和 15 分钟的 CPU 负载。这四个统计数据提供了进程活动的整体情况。这些值的快速增加通常是由运行系统上的软件引起的。

记住，所有 Linux 系统都使用交换分区来存储无法放入物理内存的信息；这些信息以“页”为单位在交换分区之间传输。发送到交换分区的页（`pswin/s`）和从交换分区取的页（`psout/s`）可以使用 `sar` 命令的 `-W` 选项查看，如下所示：

```
[@server1]# sar -W 1 5

Linux 2.6.5-1.358 (server1)  07/14/2005

12:32:06  pswin/s  psout/s

12:32:07      0.00      0.54

12:32:08      1.32      1.93

12:32:09      0.38      0.00

12:32:10      0.00      0.00

12:32:11      0.00      0.00

Average: 0.00      0.00

[root]#
```

如果有大量页被发送到交换分区，系统性能将会变慢。为了解决这个问题，你可以添加更多的物理内存（RAM）。

## 其他监控工具

`sysstat` 软件包并不是 Red Hat Linux 中唯一的可用监控工具。第 10 章中讨论的 `top` 工具也在屏幕顶部显示 CPU 统计信息、内存使用情况、交换分区使用情况和 CPU 负载，如下：

```
top -12:33:49 1:00, load average: 0.04, 0.22, 0.17

Tasks: 77: 1 running, 76 sleeping, 0 zombie

Cpu(s): 0.0 us, 0.0 sy, 0.0 ni, 99.5 id, 0.0 wa, 0.0 si

Mem: 387172 total, 376432 used, 10740 free, 39092 buffers, 198140 cached

Swap: 614368 total, 0 used, 614368 free
```

# 第 13 章 故障排除与性能

Linux 内核为自身使用留留部分内存（缓存 `cached`），以存储来自硬件设备的请求（缓冲区 `buffers`）。前面的输出中的总内存是在包含和不包含这些值的情况下计算的，指示系统预留了多少内存。`free` 命令的输出表明系统中有足够的内存，因为没有使用交换分区（`swap`），并且有大量的空闲内存可用。

与 `free` 工具一样，可以使用 `vmstat` 工具通过测量交换性能来指示是否需要更多的物理内存：

```
[root@server1 root]# vmstat

procs --memory----swap--buffer--io--system----cpu-

r b swpd free cache si so bo in cs us id wa

2 0 10756 39128 19810 0 0 73 18 10230 186 10 2 87 2
```

`vmstat` 命令显示的信息比早之前使用的 `free` 命令更多，包括以下内容：

- 等待运行的进程数 (`r`)
- 处于睡眠状态的进程数 (`b`)
- 以 KB 为单位使用的交换内存量 (`swpd`)
- 空闲物理内存量 (`free`)
- 缓冲区使用的内存量（KB 为单位） (`buff`)
- 作为缓存使用的内存量 (`cache`)
- 每秒交换入磁盘的内存量（KB） (`si`)
- 每秒交换出磁盘的内存量（KB） (`so`)
- 每秒发送到块设备的块数 (`bi`)
- 每秒从块设备接收的块数 (`bo`)
- 每秒发送到 CPU 的中断数 (`in`)
- 每秒发送到 CPU 的上下文切换次数 (`cs`)
- CPU 用户时间 (`us`)
- CPU 系统内核时间 (`sy`)
- CPU 空闲时间 (`id`)
- 等待 I/O 的花费的时间 (`wa`)

因此，之前显示的 `vmstat` 输出表明没有使用交换内存，因为 `swpd`、`si` 和 `so` 均为 0；然而，它也表明出现这种现象的原因是系统当前没有运行许多进程（`r=2`, `id=87`）。

## 自定义内核

由于 Linux 内核与计算机硬件接口，你可以通过更改内核的工作方式来提供额外的硬件支持或更改现有的硬件支持。这可以通过向内核中插入模块或重新编译内核以包含不同的功能来实现。或者，可能需要下载并编译新内核以获取当前版本不可提供的硬件支持。此外，Linux 内核还会影响性能；重新编译内核以移除不必要的内核功能可以减小其体积并提高速度。

### 内核模块

许多设备和内核功能被编译到内核中；然而，这些也可以作为模块插入内核，以减小内核的大小。将标准设备支持编译到内核中，并将其他设备和功能的支持留为模块是一种良好的做法。由于存在大量的声卡和网卡（NIC）制造商，这些驱动程序通常由模块表示，可以作为模块插入内核；而对于 IDE 硬盘支持，它通常被编译到内核中，因为它是是需要的。

某些功能以模块的形式存在；这些模块必须手动插入内核。此外，如果内核未能正确检测新硬件，你需要将适当的模块加载到内核中提供必要的硬件支持。

模块通常存储在 `/lib/modules/<kernel-version>` 目录的子目录下。例如，你可以查看 2.6.5-1358 内核的网卡模块列表，你可以列出 `/lib/modules/2.6.5-1358/kernel/drivers/net` 目录的内容：

```
$root@server1# ls -F /lib/modules/2.6.5-1358/drivers/net/

c3c51.ko*               ppp_async.ko      starfire.ko*

b44.ko*                 fordceth.ko*

c3c53.ko*       bonding/             hamachi.ko*       ppp_deflate.ko    sundance.ko*

c3c55.ko*       cs89x0.ko*            hp100.ko*         ppp_generic.ko sumgeom.ko*

c3c57.ko*       de600.ko*             ppoe.ko*           sumgeom_phy*

c3c59.ko*       de620.ko*             ixgb/               ppox.ko*           sumhme.ko*

c3c15.ko*       depca.ko*            lance.ko*          ppp_synctly.ko  tg3.ko*

c3c9x.ko*       dgrs.ko*               r8189.ko           tlan.ko*

b819cp.ko*       d12k.ko*               natsemi.ko*        rcpi.ko*           tulip/

8139tu.ko*      dummy.ko*             ne2k-pci.ko*      s2io.ko*           tun.ko*

82596.ko*       1000/                netconsole.ko*    sb1000.ko*        typhoon.ko*

8390.ko*        el100.ko*             sis900.ko*        via-rhine.ko*

ac3200.ko*       eep100.ko*         ni900.ko* ... (此处内容省略)
```
