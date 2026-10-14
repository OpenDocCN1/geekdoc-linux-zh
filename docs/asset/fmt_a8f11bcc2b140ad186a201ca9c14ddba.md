
# nohup nice -9 gcc hello.c & Run gcc uninterrupted and higher priority

使用 `nohup` 与单独使用 `&` 符号运行命令不同，因为 `nohup` 的命令即使在你退出了启动命令的 Shell 后也会继续运行。
`nohup` 命令在进程处理缓慢和拨号连接的时代非常常用（这样你就不需要在长时间编译完成时留在昂贵的连接上）。此外，今天使用如 `screen`（在第 14 章描述）等工具，你即使在断开与该 Shell 的网络连接后也可以保持会话活跃。

## 调度进程运行

与 `cron` 设施相关的命令可设置在特定时间（包括现在）运行命令，这样它就不会与当前 Shell 连接。`at` 命令可以在你指定的时间运行命令：

```
$ at +1 min Start command running in one minute

at> updatedb <Ctrl+d> 

job 5 at Mon Aug 20 20:37:00 2007

$ at teatime Start command at 4pm today

$ at +5 days Start a command in five days

$ at 06/25/08 Start a command at current time on June 25, 2008
```

另一种不与当前 Shell 连接的运行命令的方法是使用 `batch` 命令。通过 `batch`，你可以设置命令在处理器准备就绪（负载平均低于 8）时立即启动：

```
$ batch

Start command running immediately

at> find /mnt/isos | grep jpg$ > /tmp/mypics

at> <Ctrl+d> <EOT>
```

在执行 `at` 或 `batch` 命令后，你将看到一个次级 `at>` 提示符。在该提示符处输入你想运行的命令并按回车。之后，你可以继续输入命令。完成后，在单独的一行上按 `Ctrl+d`，将你输入的命令排队队列运行。
输入命令后，你可以通过输入 `atq` 命令检查设置运行的作业队列：

```
$ atq

Wed Sep 5 20:37:00 2007 5

Wed Sep 5 16:00:00 2007 6

Wed Sep 10 06:00:00 2007 7

Wed Sep 10 00:00:00 2007 8
```

# 10
# 系统管理

如果不进行仔细管理，Linux 系统的需求有时会超过你可用的资源。能够随时间监控你的系统活动（内存、CPU 和设备使用情况），有助于确保你的机器有足够的资源来完成你。同样，管理系统的其他方面，例如它使用的设备驱动程序以及启动过程的工作原理，可以帮助避免性能问题和系统故障。
本章分为几个部分，与管理你的 SUSE或其他 Linux 系统的方法有关。第一部分可以帮助监控你 Linux 系统上的资源（处理能力、设备和内存）。下一部分描述了如何检查和设置系统时钟。启动过程以及后续运行级别（`run levels`）的描述。最后部分描述了如何与内核及相关的设备驱动工作，以及如何查看计算机硬件组件的信息。

## 本章内容

- 使用 `free`、`top`、`vmstat` 和 `slabtop` 检查内存使用
- 使用 `iostat`、`dstat` 和 `top` 查看 CPU 使用情况
- 使用 `iostat`、`vmstat` 和 `isof` 监控存储设备
- 使用 `date`、`hwclock`、`cal` 和 `NTP` 处理日期/时间
- 更改 `GRUB` 引导加载器的行为
- 重建内存磁盘 (`ramdisk`)
- 使用 `runlevel` 和 `init` 处理运行级别
- 使用 `chkconfig` 和 `service` 添加、删除和列出服务
- 使用 `reboot`、`halt` 和 `shutdown` 关闭系统
- 使用 `ismod`、`modinfo` 和 `modprobe` 检查并更改内核驱动设置
- 使用 `lci`、`dmidecode` 和 `hdparam` 观察硬件设置

### 监控资源

SUSE、openSUSE 以及 Linux 系统在跟踪自身活动方面做得非常出色。如果你感兴趣，可以找到大量关于你的 CPU、硬盘、虚拟内存和其他计算机资源如何被使用的信息。
你可以通过直接查看 `/proc` 文件系统中的文件内容（附录 C），进入内核存储系统信息的地方。然而，另一种方法是使用命令查看系统上使用的计算机虚拟内存、处理器、存储设备和网络接口的信息。

# 第 10 章：系统管理

有一些命令可以监控系统资源的几个不同方面。然而，这本书不仅仅是一个帮助页（`man page`），我们按照主题（监控内存、CPU 和存储设备）而不是它们所执行的命令（`top`、`vmstat` 和 `iostat`）进行了划分。

> 注意：本节描述的许多应用程序在 SUSE 中默认安装，位于 `procps` 等软件包中。要使用 `iostat` 或 `sar`，你需要安装 `sysstat` 包。

## 监控内存使用

没有什么比内存耗尽更快地杀死系统性能了。`free` 和 `top` 等命令让你看到 RAM 和交换分区（`swap`）的使用信息。`vmstat` 命令提供有关内存使用的详细信息并可以持续运行。`slabtop` 命令显示内核（`slab` 缓存）消耗了多少内存。
`free` 命令提供了查看系统使用多少内存的最快方法。它显示了 RAM 的总量（`Mem:`）和交换空间（`Swap:`），以及当前使用的量。以下是该命令的一些示例：

```
$ free List memory usage in kilobytes (-k default)

| total free shared buffers cached |

| Mem: 742476 725108 17368 0 153388 342544 |

| -/+ buffers/cache: 229176 513300 |
```

```
Swap:

 free -m List memory usage in megabytes

| total free shared buffers cached |

| Mem: 725 706 18 0 148 333 |

| -/+ buffers/cache: 223 501 |
```

```
Swap:

 996 $ free -b List memory usage in blocks

| total free shared buffers cached |

| Mem: 760295424 72510952 17884832 0 15714368 350765056 |

| -/+ buffers/cache: 234631668 526652456 |
```

```
Swap: 104598784 73728 1045525056

$ free -g List memory usage in gigabytes

| total free shared buffers cached |

| Mem: 708 16 0 144 339 |

| -/+ buffers/cache: 223 501 |

| Swap: 996 0 996 |

Total: 1721 708 1013 |
```

```
$ free -s 5 Continuously display memory usage every 5 seconds
```

为了避免 RAM 交换并加快应用程序，Linux 会尽可能使用未使用的空闲 RAM 作为磁盘缓存。因此，`free` 输出中空闲 RAM 少的第一行具有误导性。我们建议关注输出的第二行，它显示了实际供应用程序使用的 RAM 数量。在这个例子中是 501MB：
`-/+ buffers/cache: 223 501`
猜测系统需要多少内存的一种方法是去另一个运行中的 SUSE 系统，然后你可能会认为你正在同时运行所有程序。运行带有总计选项的 `free -t` 来查看使用了多少内存。然后确保你的新系统至少有那么多总内存（最好都在 RAM 中）。
`top` 命令提供了一种监控系统资源几个不同方面的方法，并按 CPU 使用率或内存排序（关于运行进程的描述请参见第 9 章）。然而，你也可以使用 `top` 在全屏视图中查看内存使用情况。这是一个示例：

```
$ top

top - 14:15:39 3 days, 18:26, 1 user, load average: 0.11, 0.04, 0.01

Tasks: 114, 111 sleeping, 0 zombie

CPU(s): 0.0%us, 0.0%sy, 0.0%id, 0.0%wa, 0.0%hi, 0.0%si

Mem: 742476 725108 17368 0 153388 342544

-/+ buffers/cache: 229176 513300
```
