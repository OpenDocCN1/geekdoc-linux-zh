
```bash
[root@server ~]# ps aux -q 282441
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
qemu 282441 89.1 25.5 74079692 67366884 ? Sl Jun03 91484:59 /usr/libexec/qemu-kvm -name
```

图 6.27：`ps` 命令的输出示例

命令 `pmap`，加上进程 ID 参数，显示关于保留内存和共享内存的高级输出。

### 内存不足管理

当应用程序在 Linux 中执行时，它会预留内存空间，但通常不会使用全部空间。这使得 Linux 能够执行比可用内存更多的应用程序，预期应用程序使用的内存将少于可用内存。Linux 包含一个管理器，用于检测系统使用的内存是否超过应有的量，并自动终止正在使用内存的非关键进程。

每个进程都有一个关联的`score`；分数越高，表明该进程被终止的可能性越大。进程的分数存储在 `/proc/<pid>/oom_score` 文件中。

## 监控磁盘使用和可用空间

存储是导致系统瓶颈的输入/输出元素之一，这是由于在同一个存储设备上执行了大量操作或由于物理问题造成的。Linux 提供了工具来检查使用和可用空间、输入/输出操作的磁盘统计信息以及存储设备的物理状态。

命令 `lshw` 可用于列出系统中的物理存储组件，例如 `RAID` 控制器或 `SATA` 控制器。图 6.28 显示了物理服务器信息的示例：

```bash
[root@server ~]# lshw -c storage -short
H/W path Device Class Description
/==========================================
/0/100/11.4 storage C610/X99 series chipset 5SATA Contro
/0/100/14/0/e/2 storage Mass storage device
/0/100/1f.2 storage C610/X99 series chipset 4-port SATA
/0/100/1f.5 storage C610/X99 series chipset 2-port SATA
/0/2/0 scsi1 storage MegaRAID SAS-3 3108 [Invader]
/0/8f scsi0 storage
```

图 6.28：`lshw` 命令的输出示例

同一命令可用于列出连接到服务器的存储设备，例如物理磁盘（可以是配置为 `RAID` 的虚拟磁盘）或虚拟磁盘（例如，用于远程 CD/软盘的`模拟磁盘`）。图 6.29 显示了之前说明的同一服务器的示例：

```bash
[root@server ~]# lshw -c disk -short
H/W path Device Class Description
/==========================================
/0/2/0/2.0.0 /dev/sda disk 799GB MR9361-8i
/0/8f/0.0.0 /dev/sdb disk 1474KB Virtual Floppy
```

![](img/863afa537de4eed7deb11978bfbfa90e_200_0.png)

一些新的现代系统使用称为`非易失性内存快速存储（Non-volatile Memory Express，NVMe）`的新接口协议，该协议改进了之前名为`高级主控制器接口（Advanced Host Controller Interface，AHCI）`的协议，提供了降低延迟和改进并行任务处理的特性。图 6.30 显示了使用 `NVMe` 的系统上命令 `lshw` 的输出：

```bash
[root@server2 ~]# lshw -c disk -short
H/W path      Device             Class          Description
==========================================================
/0/100/1d.2/0/0  /dev/ng0n1       disk           NVMe disk
/0/100/1d.2/0/1  /dev/nvme0n1     disk           512GB NVMe disk
/0/0/0.0.0       /dev/sda         disk           SD/MMC
/0/0/0.0.0/0     /dev/sda         disk
```

![](img/863afa537de4eed7deb11978bfbfa90e_200_1.png)

命令 `lsblk` 显示关于磁盘和分区的信息。图 6.31 显示了之前使用的物理服务器的输出示例：

```bash
[root@server ~]# lsblk -a
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0  744,7G  0 disk
├─sda1   8:1    0  744,6G  0 part /
└─sda2   8:2    0   64M   0 part
sdb      8:16   1   1,4M   0 disk
```

![](img/863afa537de4eed7deb11978bfbfa90e_200_2.png)

在使用`逻辑卷管理器（Logical Volume Manager，LVM）`或使用`Linux 统一密钥设置（Linux Unified Key Setup，LUKS）`加密磁盘的系统中，命令 `lsblk` 将提供有关配置的有用信息，如图 6.32 所示：

![](img/863afa537de4eed7deb11978bfbfa90e_201_0.png)

图 6.32：`lsblk` 命令的输出示例

### 命令 iostat

此命令是 `sysstat` 软件包的一部分，该软件包之前已针对 CPU 使用率进行了描述，通常用于输入/输出统计信息。统计信息显示物理存储设备、每秒传输次数（`tps`）、每秒读取和写入的数据，以及观察期间读取和写入的数据。图 6.33 显示了输出示例；选项 `-y` 排除与系统启动以来平均值相关的第一条目：

![](img/863afa537de4eed7deb11978bfbfa90e_201_1.png)

图 6.33：`iostat` 命令的输出示例

### 命令 iotop

此实用程序类似于 `top` 命令，但仅与输入/输出相关。应该安装此工具（`iotop` 软件包）。图 6.34 显示了应用程序的外观：

### 命令 iotop

```
总磁盘读取 : 22.31 K/s | 总磁盘写入 : 11.15 M/s

实际磁盘读取 : 22.31 K/s | 实际磁盘写入: 11.15 M/s

TID PRIO 用户 磁盘读取 磁盘写入 换入 IO% 命令

2137334 be/4 qemu 0.00 B/s 52.05 K/s 0.00 % 1.50 % qemu-kvm -na-p=on [worker]

2137341 be/4 qemu 0.00 B/s 11.15 K/s 0.00 % 0.84 % qemu-kvm -na-output [worker]

2137325 be/4 qemu 0.00 B/s 26.02 K/s 0.00 % 0.73 % qemu-kvm -na-p=on [worker]

2137313 be/4 qemu 0.00 B/s 156.14 K/s 0.00 % 0.41 % qemu-kvm -na-p=on [worker]

2137359 be/4 qemu 0.00 B/s 0.00 B/s 0.00 % 0.14 % qemu-kvm -na-output [worker]
```

图 6.34: `iotop` 命令的输出示例

显示的信息对于检测哪个应用程序正在执行更多的输入/输出操作以及读写任务的速度非常重要。

### 命令 atop

此命令之前已用于描述 `CPU` 使用率，它提供了有关系统中本地和远程存储使用的详细概述。图 6.35 说明了显示的信息如下：

```
SWP | 总计 32.0G | 可用 32.0G | swcac 0.0M | vmcom 17.5G | vmlim 47.5G |

LVM | 4ab0-a3eb-6a | 繁忙 6% | 读取 0 | 写入 232 | 平均IO 2.70 ms |

LVM | RHELC5B-Home | 繁忙 6% | 读取 0 | 写入 175 | 平均IO 3.19 ms |

LVM | RHELC5B-Root | 繁忙 1% | 读取 0 | 写入 3 | 平均IO 22.7 ms |

DSK | nvme0n1 | 繁忙 6% | 读取 0 | 写入 220 | 平均IO 2.85 ms |
```

图 6.35: `atop` 命令中的磁盘信息示例
