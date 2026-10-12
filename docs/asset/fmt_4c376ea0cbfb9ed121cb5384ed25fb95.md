
此测试使用了采用 RAID 10 配置的 EMC SAN。如表所示，性能差异非常巨大。该测试已多次执行且结果可复现。

使用 `O_DIRECT` 标志对 OCFS 进行调优可以显著改善备份和恢复操作，以及作为常规 DBA 职责的一部分所需的其他文件操作。请大胆尝试并充分利用 `O_DIRECT` 功能。

## Linux 上的网络调优

网络对系统整体性能非常重要。对于 Oracle RAC 集群尤其如此。由于互连流量和全局缓冲缓存的数量，互连的性能对集群的性能可能至关重要。有一些方法可以改善网络性能。

> **核心工具 (Coreutils)**
> 
> Oracle 针对 OCFS 的核心工具可在 www.ocfs.org 上获取。

## 选择合适的网络

为系统配置最佳网络性能的第一步是正确配置网络。确保网络性能符合规格非常重要。在配置以千兆速度运行的网络时，通常有必要配置适配器进行自动协商（取决于控制器）。如果网络交换机配置不正确，适配器可能无法以适当的速度运行。

Linux 工具 `ethtool` 将显示适配器的配置方式。运行 `ethtool adapter` 命令以查看适配器设置，如下所示：

```
ptc:~ # ethtool eth0
Settings for eth0:
  Supported ports: [ TP ]
  Supported link modes: 10baseT/Half 10baseT/Full
                          100baseT/Half 100baseT/Full
                          1000baseT/Full
  Supports auto-negotiation: Yes
  Advertised link modes:  10baseT/Half 10baseT/Full
                          100baseT/Half 100baseT/Full
                          1000baseT/Full
  Advertised auto-negotiation: Yes
  Speed: 1000Mb/s
  Duplex: Full
  Port: Twisted Pair
  PHYAD: 0
  Transceiver: internal
  Auto-negotiation: on
  Supports Wake-on: pumbg
  Wake-on: g
  Link detected: yes
```

如果适配器没有以正确的速度和双工设置运行，必须找出问题的根源并加以纠正，以便适配器正确运行。

## 为网络性能调优 Linux

调优 UDP 发送和接收缓冲区通常有利于实现更高的 UDP 性能。如果在 Oracle RAC 集群中运行，这一点尤为重要。这些参数如下：

| 参数 | 说明 |
| :--- | :--- |
| `/proc/sys/net/core/rmem_default` | 默认接收窗口 |
| `/proc/sys/net/core/mem_max` | 最大接收窗口 |
| `/proc/sys/net/core/wmem_default` | 默认发送窗口 |
| `/proc/sys/net/core/wmem_max` | 最大发送窗口 |
| `/proc/sys/net/ipv4/tcp_rmem` | 为 TCP 接收缓冲区保留的内存 |
| `/proc/sys/net/ipv4/tcp_wmem` | 为 TCP 发送缓冲区保留的内存 |

要设置这些参数，你可以将值回显到上述文件名中，如下所示：

```
echo 262144 > /proc/sys/net/core/rmem_default
echo 262144 > /proc/sys/net/core/rmem_max
echo 262144 > /proc/sys/net/core/wmem_default
echo 262144 > /proc/sys/net/core/wmem_max
echo "4096 65536 4194304" > /proc/sys/net/ipv4/tcp_rmem
echo "4096 65536 4194304" > /proc/sys/net/ipv4/tcp_wmem
```

或者，你可以在 `/etc/sysctl.conf` 文件中设置它们，如下所示：

```
net.core.rmem_default = 262144
net.core.rmem_max = 262144
net.core.wmem_default = 262144
net.core.wmem_max = 262144
net.ipv4.tcp_rmem = 4096 65536 4194304
net.ipv4.tcp_wmem = 4096 65536 4194304
```

此外，以下 `/etc/sysctl.conf` 网络参数有助于改善 RAC 集群中的故障转移性能：

```
net.ipv4.tcp_keepalive_time = 3000
net.ipv4.tcp_keepalive_intvl = 30
net.ipv4.tcp_retries2 = 3
net.ipv4.tcp_syn_retries = 2
```

正确配置网络可以极大改善系统性能。如前所述，互连性能对 Oracle RAC 集群的性能至关重要。

## 总结

在本章中，你看到了许多通过修改驱动程序参数和固件配置来调优系统硬件本身的不同方法。需要更改的配置参数取决于硬件类型以及系统和应用的运行方式。对于 OLTP 系统有效的设置可能不适用于批处理或决策支持系统。硬件调优和规格定型的区别在于：规格定型是选择满足需求的正确硬件的行为，而硬件调优是修改该硬件以使其在你的配置中表现最优的行为。

![](img/9479df2d00f5e62b87366b125224950f_398_0.png)

# 第 16 章 SQL 调优

本章重点介绍对实际 SQL 语句进行调优。下一节将向你介绍 Oracle 执行计划，这是一种可视化 Oracle 处理 SQL 语句请求数据时所走路径的方法。有许多方法可以识别性能不佳的 SQL，这些方法将在本章后续部分讨论，从“查找性能不佳的 SQL”一节开始。然后，本章将介绍 Oracle 提供的几种用于捕获性能不佳 SQL 的实用工具作为结束。

## 检查执行计划

执行计划是 Oracle 处理 SQL 语句请求数据时使用的路径。Oracle 提供了一个 `Plan_Table`，用于存储执行计划。该计划表被许多 Oracle 工具使用，例如 `TKProf`，以及非字符模式工具 `SQL*Plus`。

### 计划表回顾

Oracle 在要求时会将执行计划信息填充到 `Plan_Table` 中。计划表为每个 SQL 语句持有一个执行计划。清单 16-1 展示了 Oracle 10 版本 1 的计划表。`uxtplan.sql` 脚本用于在你的模式创建计划表。该脚本总是位于你的 `ORACLE_HOME/rdbms/admin` 目录中。

### 清单 16-1: Oracle 10.1 计划表
