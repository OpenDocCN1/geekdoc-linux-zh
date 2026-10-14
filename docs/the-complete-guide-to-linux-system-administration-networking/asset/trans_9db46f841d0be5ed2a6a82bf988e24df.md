

| 命令 | 描述 | 示例 |
|---|---|---|
| syslogd | 管理所有对 syslog 函数的调用的守护进程，根据 syslog.conf 配置写入日志消息；由启动脚本在启动时启动。 | syslogd |
| whatis | 显示有关查询项的任何手册页的一行描述。 | whatis lvm |
| xconfig | 使用图形实用程序配置 Linux 内核的选项（在 Red Hat 和 Fedora 中称为 qconf）；必须在适当的 Linux 内核源代码目录中（如 /usr/src/Linux-2.6.5-1.358）与 make 命令一起使用。 | make xconfig |

## 关键术语

/etc/ntp.conf — Network Time Protocol (NTP) 服务器使用的配置文件。
action — syslog.conf 配置文件中的一个字段，用于确定对与该行选择器匹配的消息应执行什么操作。
backup — 计算机系统上数据的副本。
backup level — 描述备份操作中存储了多少数据的描述。备份级别只有在与其他备份级别进行比较时才相关。在给定级别执行备份操作时，会记录自上次执行前一级别备份以来发生更改的所有数据。
backup media — 可以存储数据的设备，例如磁带盒、可写 CD 或 DVD，或软盘。
backup plan — 一份书面文件，概述何时、如何以及为何备份、存储各种文件和文件系统，并在必要时将其恢复，以防止永久数据丢失。
differential backup — 一种备份过程，存储自上次完整备份以来更改过的所有文件。
duplexing — 一种冗余技术，其中硬盘通过不同的硬盘控制器进行访问。与“mirroring”相比，后者提供两个文件系统上的相同信息，但没有冗余磁盘控制器。
epoch backup — 完整备份，包含系统上的所有数据。
facility — 分配给系统消息的类别，用于标识提供消息的程序类型。设施在 syslog.conf 中使用。
fault tolerance — 在发生意外硬件或软件故障时优雅响应的能力，以防止系统完全关闭。
file handle — Linux 中允许单个文件被打开并使用的内部存储机制。
hardware-based RAID — 包含在单独硬件设备（RAID 子系统）中的 RAID 阵列，并由与 Linux 系统的 CPU 分开的 CPU 和其他组件控制。

**hardware clock** — 每台基于 Intel 的 PC 硬件中的时钟。Linux 内核在启动时使用它来初始化系统时钟。

**hot-swapping** — 在不关闭设备电源的情况下移除和更换故障硬盘或其他组件。

**incremental backup** — 一种备份过程，存储自上次增量或差异备份以来更改过的所有文件。

**kernel modules** — 包含可根据需要加载到内核或从内核中移除的计算机代码的文件。

**log file** — 包含 Linux 系统活动详细记录的文件。

**logical volume group** — 物理卷（实际硬盘分区）的集合，这些卷被组合在一起供逻辑卷管理器实用程序使用，以提供抽象层，便于以后向文件系统添加空间。

**Logical Volume Manager (LVM)** — Red Hat Linux 和 Fedora 的一项功能，提供一组实用程序，允许将多个物理存储设备作为单个存储卷进行管理，按需将其划分为文件系统，并在无需重新格式化硬盘的情况下向这些文件系统添加空间。

**message** — 程序中正在发生情况的描述。

**messages file** — Linux 中主要的系统日志文件，通常存储在 /var/log 目录中。

**mirroring** — 一种冗余技术，其中两个文件系统的内容包含相同的信息。镜像可提高数据访问速度，并在其中一个文件系统发生故障时提供容错能力。

**module parameters** — 模块所需的信息，用于定位系统资源。使用 insmod 或 modprobe 命令时，参数在模块名称之后添加。

**Network Time Protocol (NTP)** — 用于在网络或互联网上的服务器之间协调高度精确的时间保持的协议。

**network time server** — 依靠无线电钟、原子钟或类似设备来保持准确时间的计算机，并可使用 Network Time Protocol (NTP) 为其他联网服务器提供准确时间。

**parity** — 一种冗余技术，允许使用存储数据时创建的额外信息（奇偶校验信息）重建损坏的数据。

**parity stripe** — 作为 RAID-3 或 RAID-5 系统的一部分存储的奇偶校验信息。

**patch file** — 包含对一个或多个源代码文件的更新以及应如何更新这些源代码文件的说明的文本文件。patch 命令用于将补丁文件应用于现有源代码文件。

**physical volumes** — 逻辑卷管理器使用的底层物理分区。多个物理卷一起构成逻辑卷组，该组被划分为标准分区数据存储。

**priority** — 指示提交用于记录的消息严重性的标签。优先级在 syslog.conf 中使用。

**RAID (redundant arrays of inexpensive disks)** — 使用多个廉价硬盘按预定义模式（阵列）排列的存储技术，以提高性能、增加容错能力或两者兼而有之。

## 复习问题

- 1. 备份计划通常不包括以下内容：
  - a. 磁带驱动器价格清单
  - b. 执行备份的时间
  - c. 系统上关键文件的位置
  - d. 建议何时用新磁带盒替换旧磁带盒的时间

RAID-0 — 使用条带化提高磁盘性能但不提供任何容错能力的 RAID 级别。

RAID-1 — 使用磁盘镜像显著提高容错能力的 RAID 级别。磁盘读取性能也得到改善，但磁盘写入性能下降。

RAID-3 — 使用带奇偶校验信息的条带化来提高性能并增加容错能力的 RAID 级别。

RAID-5 — 条带化与奇偶校验分布在 RAID 阵列中的所有磁盘上的 RAID 级别（与 RAID-3 相比，后者将奇偶校验信息存储在单个硬盘上）。

RAID-Linear — 将多个物理设备组合成单个逻辑设备的存储技术。

RAID subsystem — 包含 CPU 和其他组件来控制硬盘阵列的硬件控制 RAID 设备。

redundant arrays of inexpensive disks — 参见 RAID。

restore — 将数据从备份位置（例如磁带盒）复制到文件系统上，该数据通常在该文件系统上使用，并且从中意外丢失。

rotating log files — 将现有日志文件移动到另一个文件名和位置以进行归档或审查的过程。

selector — syslog.conf 文件中的一个字段，用于确定正在记录哪些事件。选择器由设施和优先级组成。

SIGHUP — 发送给日志守护进程的信号，指示守护进程重新读取其配置文件和写入的日志文件。有时称为 HUP。

striping — 一种数据存储技术，将文件的一部分写入多个磁盘以提高性能。参见 RAID-3 和 RAID-5。

syslog.conf — 用于控制 syslogd 和 klogd 如何以及在何处记录消息的配置文件。

system clock — Linux 内核在系统打开时维护的内部时钟。基于硬件时钟初始化。在大型网络上，通过依赖使用 Network Time Protocol (NTP) 的网络时间服务器来保持准确。

timestamp — 正在记录的事件发生的日期和时间。

write caching — 一些存储系统的功能，其中要写入文件系统（特别是 RAID 文件系统）的信息暂时存储在内存中，以提高文件系统的整体读写性能。

