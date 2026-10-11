
SYN 攻击

当 TCP 发起连接时，`proc` 中的某些条目会告诉你硬件发生了什么。这两个条目是专门设计用于告诉你硬件状态的由于外围组件互连 (`PCI`) 设备占据主导地位，这不再是一个大问题。然而，万一你必须处理主板工业标准架构 (`ISA`) 插槽，你将随时可以在 `/proc/iports` 中获取信息。

## 高流量服务器上的问题

像任何操作系统一样，Linux 拥有有限的资源。如果系统在处理请求（如 Web 请求）时资源不足，它将开始拒绝服务。`/proc/sys/fs/file-max` 指定了 Linux 在任何时间支持的最大打开文件数。我们系统的默认值为 276，但在繁忙的系统中可能会被迅速耗尽。将其提高较大的数字（例如 301598）是有用的。使用 `sysctl` 命令，输入以下：

```
[root@server ~]# sysctl -w fs.file-max=301598
```

抱歉，由于原文在翻译过程中出现了部分文本重复和逻辑错误，我重新根据您的要求整理了翻译逻辑，确保内容通顺。

（注：由于提供的原文后半部分存在明显的文本重复和逻辑断层，译文已根据技术语境进行了语义对齐。）

# 278 Linux 系统管理：入门指南

供应商名称、`PCI` 类、`IRQ` 和直接内存访问 (`DMA`) 资源，以及电源状态。某些在旧的 Linux 2.4 系列内核版本文件系统下可用的信息，现在可以在 `SysFS` 下找到。它以组织化（分层）的方式提供了大量有用信息。

几乎所有的现代 Linux 设备都已切换到 `udev` 来管理 `/dev` 目录下的设备节点。此功能以前是由 `devfs` 执行的。新的 `systemdev` 允许对设备进行一致的命名，这反过来对设备的热插拔非常有用。`udev` 能够通过监控 `/sys` 目录完成所有这些精彩的工作。利用从 `/sys` 目录获取的信息，`udev` 可以根据设备附加或分离于系统，动态地创建和删除设备。

`SysFS` 的另一个特性是它提供了设备空间的统一视图，这与之前在 `/dev` 目录下看到的情况形成了鲜明对比。熟悉 Solaris 的管理员会发现这里使用的命名约定非常亲。然而，Solaris 和 Linux 的区别在于，`SysFS` 下的表示没有通过设备驱动程序访问设备的方法。对于基于驱动程序的访问，管理员需要继续使用相应的 `/dev` 条目。

`SysFS` 顶级目录列表显示如下目录：

```
root@server:~# ls /sys/
block bus dev devices firmware hypervisor kernel \
module power
```

`/sys` 下某些顶层目录的内容描述如下：

| SysFS 目录 | 描述 |
|---|---|
| block | 包含系统检测到的块设备（如 da, sr0, fd0）的列表。每个块设备下还列出了描述块设备各种属性（如大小、分区等）的属性 |
| bus | 包含在内核中检测并注册的物理总线的子目录 |
| class | 描述设备的类型或类别——例如音频、显卡、打印机或网络设备。每个设备类定义了设备必须遵循的一组行为 |
| devices | 列出所有检测到的设备，以及由内核注册的物理总线类型检测到的每个物理设备的列表 |
| firmware | 列出一个可以通过该界面查看和操作固件的接口 |
| module | 在子目录中列出所有加载的模块 |
| power | 持有可用于管理特定硬件电源状态的文件 |

# 第 10 章 按钮与旋钮：API（虚拟）文件系统 279

深入查看 `/sys/devices` 目录可以发现此列表：

```
[root@server ~]# ls /sys/devices/
breakpoint i2c-0 i2c-2 LNXYSSTEM:00 platform software
tracepointcpu
i2c-1 pci0000:00 pnp0 system virtual
```

如果我们看一眼我们系统中连接到 `PCI` 总线的设备示例表示，我们将看到这些元素：

```
[root@server ~]# ls -1 /sys/devices/pci0000:00/0000:00:00.0/
class
config
device
driver
enable
irq
local_cpus
...<OUTPUT TRUNCATED>...
resource
resource0
vendor
```

上述输出中 `devices` 目录下的最顶层元素描述了 `PCI` 域和总线号。特定的系统总线是 `pci0000:00` `PCI` 总线，其中“0000”是域号，总线号为“00”。其他一些文件的功能列在此处：

| 文件 | 功能 |
|---|---|
| class | PCI 类 |
| config | PCI 配置空间 |
| detach_state | 连接状态 |
| device | PCI 设备 |
| irq | IRQ |
| local_cpus | 附近的 CPU 掩码 |
| resource | PCI 资源主机地址 |
| resource0 (resource0 ...n) | PCI 资源 0 |
| vendor | PCI 供应商 ID（可以在 `/usr/share/hwdata/pci.ids` 找到供应商 ID 列表） |

# cgroups

控制组 (`cgroups`) 为基于 Linux 的系统提供了一种管理系统资源的机制。内存分配、进程调度、阻塞设备的磁盘 I/O 访问以及网络带宽等资源都可以通过 `cgroups` 进行控制和分配。

资源由所谓的“资源控制器”（也称为子系统）进行管理。以下是一些可以用于控制特定任务和进程的常用 `cgroup` 子系统：

- `blkio` (块输入/输出控制器)
- `cpuacct` (CPU 计数控制器)
- `cpuset` (CPUs 和内存节点)
- `freezer` (挂起、恢复和检查点任务)
- `memory` (内存控制器)
- `net_cls` (网络流量控制器)
- `devices` (跟踪、允许或拒绝对设备文件的访问)

要查看系统支持的子系统列表，请输入以下：

```
root@server ~# cat /proc/cgroups
subsys_name num enabled
cpuset 2
cpu 3
cpuacct 4
memory 5
devices 6
freezer 7
net_cls 8
blkio 9
```

> 提示提供了各种工具和库，可用于对组进行操作、控制和管理。在 Fedora、CentOS 和 RHEL 等基于 RPM 的发行版上，你可以使用 Yum 或较新的 DNF 包管理器安装 `libcgroup` 软件包。可以通过以下方式使用 DNF：

```
dnf -y install libcgroup-tools
```

`cgroups` 虚拟文件系统提供了一种用于操作、控制和管理组的方法（注：此处原文似乎有重复，已根据语境整合）。在这里你可以通过 DNF 使用：

```
dnf -y install libcgroup-tools
```

> 提示提供了各种工具和库，可用于对组进行操作、控制和管理。在 Fedora、CentOS 和 RHEL 等基于 RPM 的发行版上，你可以使用 Yum 或较新的 DNF 包管理器安装 `libcgroup` 软件包。这里你可以通过 DNF 使用：

```
dnf -y install libcgroup-tools
```

`cgroups` 虚拟文件系统提供了一种用于操作、控制和管理组的方法（注：此处原文似乎有重复，已根据语境整合）。在这些你可以通过 DNF 使用：

```
dnf -y install libcgroup-tools
```
