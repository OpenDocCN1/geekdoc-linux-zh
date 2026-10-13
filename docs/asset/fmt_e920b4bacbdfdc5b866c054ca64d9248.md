
vmstat 输出中标题行之后的第一行显示了自上次重启以来的平均值。之后，`vmstat` 在接下来的 35 秒内多次显示 5 秒的平均数据。在 `vmstat` 的输出中，`si` 和 `so` 字段的高值表示内存交换过多。`bi` 和 `bo` 字段的高数值表示磁盘活动过于频繁。

# 检查磁盘性能和磁盘使用

Linux 带有 `/sbin/hdparm` 程序，你可以用它控制大多数 PC 上的 IDE 或 ATAPI 硬盘。`hdparm` 程序的一个功能是 `t` 选项允许你确定数据从磁盘读取到内存缓冲区中的速率。例如，以下是该命令在系统上执行的结果：

```
/sbin/hdparm -t /dev/hda
```

`/dev/hda`:

Timing disk reads: 130 MB in 3.01 seconds = 43.24 MB/sec

可以看出，该命令需要 IDE 驱动器的设备名称（`/dev/sda`）作为参数。如果你有一个 IDE 硬盘，可以使用此命令。

## 第 20 章：高级系统管理

你可以像访问任何其他目录一样访问 `/proc` 文件系统，但你必须了解文件的含义才能解读这些信息。通常，你可以使用 `cat` 命令来查看 `/proc` 中文件的内容；这些文件的内容提供了系统各个方面的信息。

对于任何目录，你都可能想开始查看 `/proc` 的详细列表。为此，请使用 `ls -l /proc`。在输出中，第一组目录（以字母 `d` 开头）代表当前系统上运行的进程。每个对应进程的目录都以 id（一个数字）作为名称。

此外，注意一个大文件 `/proc/kcore`，它代表系统的整个内存。虽然 `/proc/kcore` 在列表中显示为一个巨大的文件，但并没有物理文件占用你硬盘上的大量大量空间。你不应尝试删除此文件来回收磁盘空间。

`/proc/cpuinfo` 中的几个文件和目录包含有关你 Linux 系统的信息。例如，`/proc/cpuinfo` 列出了你系统的关键特性，例如处理器类型和浮点处理器信息。你可以通过 `cat /proc/cpuinfo` 来查看进程信息。例如，以下是我在我的机器上运行该命令得到的结果：

```bash
cat /proc/cpuinfo
processor : 0
vendor_id : GenuineInt
cpu family : 15
model : 3
model name : Intel(R) Celeron(R) CPU 2.53GHz
stepping : 3
cpu MHz : 2533.114
cache size : 256 KB
fdiv_bug : no
hlt_bug : no
f00f_bug : no
coma_bug : no
fpu : 
fpu_exception : yes
cpuid_level : 5
wp : yes
flags : fpu vme de pse tsc mde cx8 apic mittr pga cmov
pat pse356 clflush dts acpi mxx fxsr sse sse2 ss ht tm pbi sni monitor
ds_cpl cid : 4997.12
```

此输出源自一个 2.53 GHz 的 Intel Celeron 系统。列表显示了处理器的许多有趣特性。注意以 `fdiv_bug` 开头的列表。记住臭臭昭著的 Pentium 浮点除法错误：`fdiv` 是一个导致 `fdiv`（浮点除法）的指令。因此，`fdiv_bug` 行表示此 Pentium 是否存在该错误（幸运的是，我的系统处理器没有）。

表 20-1 总结了 `/proc` 文件系统中的某些文件，你可以从中获取有关你 Linux 系统的信息。你可以在系统上查看其中一些文件以了解它们的内容。请注意，表 20-1 中显示的所有文件并不存在于你的系统中——`/proc` 文件系统的内容取决于内核配置和加载的驱动模块（而这些反过来取决于你 PC 的硬件配置）。

你可以像在 Linux 中导航任何其他目录和文件一样导航 `/proc` 文件系统。使用 `more` 或 `cat` 命令查看文件内容。

### 表 20-1：/proc 中的典型文件和目录

| 文件名 | 内容 |
| --- | --- |
| `/proc/apm` | 关于高级电源管理 (APM) 的信息。 |
| `/proc/bus` | 包含每个总线（如 PCI）的特定总线信息的目录。 |
| `/proc/cmdline` | 用于启动 Linux 内核的命令行（例如，root=LABEL=/1 acpi-off rhgb quiet）。 |
| `/proc/cpuinfo` | 关于 CPU（微处理器）的信息。 |
| `/proc/devices` | 系统中可用的块设备和字符设备。 |
| `/proc/dma` | 关于已使用的 DMA（直接存储器访问）通道的信息。 |
| `/proc/driver` | 包含各种驱动程序信息的目录（例如，你可以在此目录下找到关于 PC 实时时钟 rtc 的信息）。 |
| `/proc/fb` | 关于任何帧缓冲区的信息。 |
| `/proc/filesystems` | 支持的文件系统列表。 |
| `/proc/fs` | 文件系统参数的目录。 |
| `/proc/ide` | 包含 IDE 设备信息的目录。 |
| `/proc/interrupts` | 关于中断请求 (IRQ) 编号、其使用方式以及每个 IRQ 生成了多少中断的信息。 |
| `/proc/meminfo` | 显示正在使用的物理内存地址范围的内存映射。 |
| `/proc/ioports` | 关于输入/输出 (I/O) 端口地址及其使用方式的信息。 |
| `/proc/irq` | 包含每个中断请求 (IRQ) 编号子目录的目录，其中 `smp_affinity` 文件指示多个 CPU 中的哪一个处理中断（仅适用于多 CPU 系统）。 |
| `/proc/kcore` | 物理内存映像。 |
| `/proc/kmsg` | 内核消息。 |
| `/proc/kallsyms` | 内核符号表。 |
| `/proc/loadavg` | 负载平均（过去 1、5 和 15 分钟内等待运行的进程平均数）。 |
| `/proc/locks` | 当前内核锁（用于确保多个进程不会同时写入文件）。 |
| `/proc/meminfo` | 关于物理内存和交换分区的信息。 |
| `/proc/misc` | 杂项信息。 |
| `/proc/modules` | 已加载模块的列表。 |
| `/proc/mounts` | 已挂载的文件系统列表。 |
| `/proc/net` | 包含网络目录。 |
| `/proc/partitions` | 分区列表。 |
| `/proc/pci` | 关于 PCI 的信息。 |
| `/proc/scsi` | 关于 SCSI 的信息。 |
| `/proc/stat` | 总体统计。 |
| `/proc/swaps` | 关于交换分区的信息。 |
| `/proc/tty` | 关于 tty 的信息。 |
| `/proc/uptime` | 关于系统运行时间的信息。 |
| `/proc/version` | 内核版本。 |

## 第 20 章：高级系统管理

在我的 Linux 系统上，`/etc/sysctl.conf` 文件包含以下行：

```
# 对于二进制值，0 表示禁用，1 表示启用。更多信息请参见 sysctl(8) 和
# sysctl.conf(5)。
```

```
# 控制 IP 数据包转发
net.ipv4.ip_forward = 0
```

```
# 控制源路由验证
net.ipv4.default.rp_filter = 1
```

```
# 不接受源路由
net.ipv4.default.accept_source-route = 0
```

```
# 控制内核的系统请求（System Request）调试功能
kernel.sysrq = 0
```

```
# 控制核心转储是否会在核心文件名中追加 PID。
# 有于调试多线程应用程序。
kernel.core_uses_pid = 1
```

```
# 控制 TCP syncookies 的使用
net.ipv4.tcp_syncookies = 1
```

表 20-12 描述了 `/proc/sys` 目录中一些有趣的内核参数以及这些参数的含义。

### 表 20-12：/proc/sys 目录中的某些内核参数

| 名称 | 含义 |
| --- | --- |
| `fs.file-max` | Linux 内核可以分配的文件句柄的最大数量。 |
| `fs.file-nr` | 三个值，分别代表已分配句柄数、使用的句柄数和最大可用句柄数。 |
| `kernel.acct` | 三个值（高阈、低阈和频率），控制进程计数信息的日志。当文件系统空闲空间低于低阈（百分比）时，挂计数；当空闲空间高于高阈（百分比）时恢复；频率指定空闲空间有效的秒数（默认值为高阈 4%、低阈 2%、频率 30 秒）。 |
