
| `pProcessSize(3)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| `pProcessCPU Time(4)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| `pProcessTTY(7)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| `pProcessWaitChannel(6)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| `pProcessID(1)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

| `pParentProcessID(2)` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

**图 7.12** 进程状态 MIB 映射。

进程表包含以下对象：

**Object Name:** `psProcessID`

**OID:** `psEntry.1`

Object Type: Counter

Access Mode: read-only

Description: 显示进程 ID

Object Name: `psParentProcessID`

OID: `psEntry.2`

Object Type: Counter

Access Mode: read-only

Description: 显示进程 ID 的父进程

Object Name: `psProcessSize`

OID: `psEntry.3`

Object Type: Counter

Access Mode: read-only

Description: 显示进程使用的内存大小，包括栈和数据段

Object Name: `psProcessCpuTime`

OID: `psEntry.4`

Object Type: Counter

Access Mode: read-only

Description: 显示在检索该值时，该进程已消耗的 CPU 时间，包括用户时间和系统时间

**Object Name:** `psProcessState`

**OID:** `psEntry.5`

**Object Type:** Display String [4]

**Access Mode:** read-only

**Description:** 显示进程的当前运行状态。这包括以下标志的使用：R: 可运行 T: 已停止 P: 分页等待 0: 不可中断等待 S: 睡眠（少于 20 秒）I: 空闲（超过 20 秒）Z: 僵尸

**Object Name:** `psProcessWaitChannel`

**OID:** `psEntry.6`

**Object Type:** Display String [16]

**Access Mode:** read-only

**Description:** 显示进程处于等待模式的原因

**Object Name:** `psProcessTTY`

**OID:** `psEntry.7`

**Object Type:** Display String [16]

**Access Mode:** read-only

**Description:** 显示该进程的控制终端（如果有）

对象名称: `psProcessUserName`

OID: `psEntry.8`

对象类型: Display String [16]

访问模式: read-only

描述: 显示与此进程关联的用户名

对象名称: `psProcessUserID`

OID: `psEntry.9`

对象类型: counter

访问模式: read-only

描述: 显示与 `psProcessUserName` 字符串关联的数值用户 ID

对象名称: `psProcessName`

OID: `psEntry.10`

对象类型: Display String [64]

访问模式: read-only

描述: 显示此进程的命令字符串名称

对象名称: `psProcessStatus`

OID: `psEntry.11`

对象类型: Counter

访问模式: read-write

描述: 指示要发送到此进程的信号

## Sun SNMP 代理

407

## Sun 主机性能组

`sunHostPerf` 组包含一系列系统性能相关对象，从进程使用的总时间滴答数到总网络冲突数不等。由于这些对象的数量相当多，只会描述最有用的对象。如果您正在寻找该组中所有可用对象的完整列表，请查阅 Sun MIB 文件 `/var/snmp/mib/sun.mib` 以获取更多信息。

`sunHostPerf` 组中更有用的对象包括与系统交换、设备中断和网络流量相关的对象。图 7.13 以层级形式展示了这些对象与主 `sun` 分支的关系。流量对象是计数器，表示整个系统的总数，不受网络连接数量的影响，与 `netstat` 命令的输出类似。例如，`rsIfInPackets` 对象提供系统上所有网络接口从网络获得的总输入数据包数。

`sunHostPerf` 组包含以下对象：

对象名称: `rsVpagesIn`

OID: `sunHostPerf.9`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来从磁盘读入的总页数

对象名称: `rsVpagesOut`

OID: `sunHostPerf.10`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来写入磁盘的总页数

![](img/f265c9d1f2610aca197c430cbfcd51f5_439_0.png)

**图 7.13** *sunHostPerf* 视图。

对象名称: `rsVSwapIn`

OID: `sunHostPerf.11`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来换入的总页数

对象名称: `rsVSwapOut`

OID: `sunHostPerf.12`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来换出的总页数

对象名称: `rsVIntr`

OID: `sunHostPerf.13`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来设备中断的总次数；包括磁盘和其他外围设备等所有设备的中断。

对象名称: `rsIfInPackets`

OID: `sunHostPerf.14`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来从网络获得的总输入数据包数

对象名称: `rsIfOutPackets`

OID: `sunHostPerf.15`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来传输到网络的总输出数据包数

对象名称: `rsIfInErrors`

OID: `sunHostPerf.16`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来从网络产生的总输入错误数

对象名称: `rsIfOutErrors`

OID: `sunHostPerf.17`

对象类型: Counter

访问模式: read-only

描述: 尝试传输到网络时遇到的总输出错误数，自上次重启以来

对象名称: `rsIfCollisions`

OID: `sunHostPerf.18`

对象类型: Counter

访问模式: read-only

描述: 自上次重启以来在网络上记录的总输出冲突数

## SNMP 工具

第 4 章“核心系统实用程序和工具”以及第 5 章“其他系统实用程序和工具”讨论了操作系统工具和实用程序。本章更侧重于网络工具，这些工具可以帮助管理系统和网络元素，例如交换机、路由器、探针、集线器和其他设备。它们都基于 SNMP，可用于查询任何 SNMP 兼容代理以获取大量信息。

本章涵盖以下工具：

| 命令 | 页码 |
|---|---|
| `snmpdelta` | 422 |
| `snmpget` | 425 |
| `snmpgetnext` | 427 |
| `snmpnetstat` | 429 |
| `snmpset` | 434 |
| `snmpstatus` | 437 |
| `snmptable` | 440 |
| `snmptest` | 443 |
| `snmptranslate` | 443 |
| `snmptrap` | 445 |
| `snmptrapd` | 446 |
| `snmpwalk` | 450 |
| `snmpbulkwalk` | 451 |
| `snmpconf` | 454 |
| `tkmib` | 458 |

### 监控/管理功能

本节介绍的工具可访问各种代理信息，在监控和管理方面特别有用。可以从设备收集的最重要信息包括以下内容：

- SNMP 系统心跳
