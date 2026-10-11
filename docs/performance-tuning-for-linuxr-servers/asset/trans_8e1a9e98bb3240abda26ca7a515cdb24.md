

## 摘要

本章主要关注商业工作负载的性能分析与调优。我们提供了该领域的一些背景信息以及执行此类任务的一些指导原则。我们还简要提到了业界在应用服务器标准化性能测量方面所付出的努力。

本章的大部分篇幅都用于一个示例，该示例逐步说明了调优商业工作负载的过程。以下是本章的一些要点：

- 性能调优是一项通过不断接触不同问题情境而获得的技能。
- 性能调优应按照明确定义的方法论来执行。
- 如果没有明显的嫌疑人，通过排除法缩小问题范围。
- 始终选择更简单、更快捷的方式来获取所需结果。
- 始终关注您的 Linux 安装的 kernel 层面。这样，您将知道是否缺少补丁等。
- 不要期望一个补丁、内核级参数或调优参数在所有情况下都对您有效。
- 始终意识到开源社区对 Linux 操作系统所做的更改和改进。
- 并非所有新的硬件功能都有帮助；例如，超线程。很多仍取决于您的应用程序和中间件的性质和使用模式。

## 参考文献

[1] Gunther, Harvey. "WebSphere Application Server: Best practices for developing high performance Web and enterprise applications," http://www-306.ibm.com/software/webservers/appserv/ws_bestpractices.pdf, Sept. 7, 2000.

[2] Comer, Douglas E. Internetworking with TCP/IP Volume I: Principles, Protocols, and Architecture, Second Edition, Prentice Hall, New Jersey, 1991.

[3] Jamison, Wilfred C. "Improving Performance of J2EE Applications," WebSphere Journal, May 20, 2003.

## 附录 A. 调整内核参数

*作者：Badari Pulavarti 和 Narasimha Sharoff*

### 简介

本附录列出并描述了许多通过 `sysctl`、`/proc` 和 `sysfs` 接口可用的内核可调参数。它提供了如何通过使用这些接口来调整 Linux 内核及系统其他关键组件的概述。本附录涵盖的主题包括：

- `sysctl` 的使用概述和描述
- `/proc` 的使用概述和描述
- `sysfs` 的使用概述和描述
- 对各种类型可调参数的讨论，包括：
  - 通用内核参数
  - 虚拟内存参数
  - 文件系统参数
  - 网络参数

### sysctl 接口

sysctl 接口允许您在运行时配置内核参数。sysctl 列出了内核参数，通过命令行界面临时修改参数，从文件加载设置，或者通过在启动时加载的配置文件中添加设置来永久修改内核参数。

参数按照层次结构或树状结构组织。例如，与设备相关的所有参数都以 `dev` 开头。特定设备（如 `cdrom`）的参数位于 `dev.cdrom` 之下。

默认情况下，已启用对 sysctl 的内核支持。在新内核构建时启用 sysctl 支持时，请使用 `menuconfig`，从主菜单中选择 General Setup，并选择 sysctl support。或者，您可以编辑配置文件以设置 CONFIG_`SYSCTL` 选项。

### 使用 sysctl

`sysctl` 命令通常位于 `/sbin` 目录中。您可以通过执行 `sysctl a` 命令来查看完整的可调参数及其设置列表。要设置特定参数，请使用 `w` 选项。例如，以下命令将消息队列标识符设置为 32：

```bash
$ sysctl w kernel.shmmax=32
```

请注意，此更改是暂时的，不会在系统重启后保留。

要进行在重启后仍能保留的更改，请使用 `p` 选项从配置文件加载一组值。在下面的示例中，从配置文件 `/etc/sysctl.conf` 加载值：

```bash
$ sysctl p /etc/sysctl.conf
```

有关不同使用选项的更多信息，请参阅 `sysctl(8)` man 页。

### procfs 接口

修改内核参数的另一种方法是使用通过 procfs 的文件系统接口。/proc 文件系统（procfs）是一个特殊的文件系统。它是一个虚拟文件系统；它与块设备不关联，仅存在于内存中。/proc/ 目录以层次结构显示参数。您可以通过查看文件内容来查看参数。可以通过将值回显到文件中来修改参数。但是，以这种方式进行的更改不会在机器重启后保留。

/proc 组织为以下目录：

| 目录 | 描述 |
| --- | --- |
| /proc/bus | 总线特定信息 |
| /proc/driver | 驱动程序特定信息 |
| /proc/fs | 文件系统参数 |
| /proc/irq | IRQ 到 CPU 亲和性的掩码 |
| /proc/net | 网络信息 |
| /proc/scsi | SCSI 相关信息 |
| /proc/sys | 内核参数 |
| /proc/sys/fs | 通用文件系统数据 |
| /proc/sys/kernel | 通用内核参数 |
| /proc/sys/vm | 内存管理参数 |
| /proc/sys/dev | 设备特定信息 |
| /proc/sys/sunrpc | RPC 信息 |
| /proc/sys/net | 网络信息 |

参数可以通过写入 /proc/ 目录中的相应文件来查看或更改。

例如，要查看 `$shmmax` 的当前值，输入以下内容：

```bash
$ cat /proc/sys/kernel/shmmax
```

类似地，您可以通过输入以下命令来更改 `$shmmax` 的值：

```bash
$ echo "32" > /proc/sys/kernel/shmmax
```

请注意，此更改是暂时的，不会在重启后保留。

### sysfs (仅限 Linux 内核 2.6)

sysfs 是另一个虚拟文件系统，它为内核参数提供了易于使用的接口。目前，procfs 中所有的非进程信息都已移植到 sysfs。计划将 sysctl 和 /proc 接口合并为一个。sysfs 还设计用于替代 devfs，因为驱动程序预计将移植到新的接口。此文件系统由内核自动生成，并在设备添加或删除时更新。

### 使用 sysfs

参数可以通过写入 sysfs 文件系统中的相应文件来查看或更改。

### 通用内核参数

本节讨论通用内核参数，包括以下方面的参数：

- 共享内存
- 进程
- 信号
- 性能分析/调试
- 系统

#### 共享内存

**Sysctl 前缀：** kernel  
**/proc 前缀：** /proc/sys/kernel/

| 参数 | 描述 |
| --- | --- |
| `sem` | 信号量值 |
| `msgmnb` | 最大消息队列（以字节为单位） |
| `msgmni` | 最大允许的消息队列标识符 |
| `msgmax` | 最大消息大小（以字节为单位） |
| `shmmni` | 系统范围的共享段数 |
| `shmall` | 系统范围的共享内存（以页为单位） |
| `shmmax` | 共享段大小（以字节为单位） |

#### 进程

**Sysctl 前缀：** kernel  
**/proc 前缀：** /proc/sys/kernel/

| 参数 | 描述 |
| --- | --- |
| `thread_max` | 系统中允许的最大线程数 |

#### 信号

**Sysctl 前缀：** kernel  
**/proc 前缀：** /proc/sys/kernel/

| 参数 | 描述 |
| --- | --- |
| `rtsig-max` | 最大实时信号 |
| `rtsig-nr` | 当前排队中的实时信号数量 |

#### 性能分析/调试

**Sysctl 前缀：** kernel  
**/proc 前缀：** /proc/sys/kernel/

| 参数 | 描述 |
| --- | --- |
| `sysrq` | 系统跟踪请求 |
| `printk` | Printk 值 |

`printk` 参数有四个字段：`console_loglevel`、`default_message_loglevel`、`minimum_console_level` 和 `default_console_level`。优先级高于 `console_loglevel` 的消息会打印到控制台。没有明确优先级的消息会以 `default_message_loglevel` 优先级打印。`console_loglevel` 可以设置的最小（最高）值由 `minimum_console_level` 参数决定。`default_console_loglevel` 是 `console_loglevel` 的默认值。

#### 系统

**Sysctl 前缀：** kernel  
**/proc 前缀：** /proc/sys/kernel/

| 参数 | 描述 |
| --- | --- |
| `domainname` | 域名 |
| `hostname` | 主机名 |
| `ostype` | 操作系统类型 |
| `osrelease` | 操作系统发行版 |
| `version` | 内核版本 |
| `real-root-dev` | 实际根设备分区 |

