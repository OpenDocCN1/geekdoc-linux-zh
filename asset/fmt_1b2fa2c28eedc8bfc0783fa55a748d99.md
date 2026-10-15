
交换空间的使用率对系统性能有显著影响。如果系统大量使用交换空间，应升级更多的内存以提高性能。此外，在专用的磁盘上创建交换空间存储是一种良好的做法，可以防止性能下降。

`mkswap` 是 Linux 命令。其他平台也存在类似的命令，详情参见以下交叉参考表。

| AIX | BSD | HP-UX | Linux | Solaris |
|---|---|---|---|---|
| mkfs | swaptc1 | lvcreate | mkswap | swap |

交换命令交叉参考

常见用法示例：

| 命令 | 描述 |
|---|---|
| `mkswap [DEVICE]` | 在指定设备上创建交换空间 |
| `mkswap -c [DEVICE]` | 在格式化之前检查设备的坏块 |

### swapon / swapoff

**用途**：激活/停用交换空间。

**用法语法**：`swapon [OPTIONS] [DEVICE]`

```
# swapon /dev/sdb1

Activating swap storage
```

`swapon` 命令用于激活交换空间存储。上面的示例演示了如何使用 `swapon` 激活新创建的交换空间。

> **注意**
>
> 新创建的交换空间在使用 `swapon` 命令激活之前无法被系统使用。大多数系统默认在启动时激活至少一个交换空间。安装后创建的额外交换设备必须添加到 `/etc/fstab` 文件中，以便在启动时自动激活。

`swapoff` 命令用于停用交换空间存储。下一个示例演示了如何使用 `swapoff` 停用 `/dev/sdb1` 交换设备。

**用法语法**：`swapoff [OPTIONS] [DEVICE]`

```
# swapoff /dev/sdb1

Deactivating swap storage
```

在修改或删除交换空间存储之前，必须使用 `swapoff` 命令将其停用。

> **注意**
>
> Solaris 系统使用 `swap` 命令代替 `swapon` 和 `swapoff`。

常见用法示例：

| 命令 | 描述 |
|------|------|
| `swapon -a` | 启用所有交换空间 |
| `swapon [DEVICE]` | 启用指定的交换空间 |
| `swapon -s` | 显示设备的交换空间使用情况 |
| `swapoff -a` | 禁用所有活动的交换空间 |
| `swapoff [DEVICE]` | 禁用指定的交换空间 |

### swapinfo

**用途**：显示交换空间信息。

**用法语法**：`swapinfo [OPTIONS]`

```
### swapinfo
                 Kb     Kb     Kb    PCT   START/        Kb
TYPE             AVAIL  USED   FREE  USED  LIMIT   RESERVE  PRI  NAME
dev           524288    0  524288    0%     0     -  /dev/vg00/lvol2
reserve      -111696 -111696
memory        389816 143784  246032   37%
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_189_0.png)

`swapinfo` 显示活动交换空间存储的详细信息。上面的示例显示了 `swapinfo` 命令在 HP-UX 系统上的输出。它包括关于交换空间存储的大小和位置以及内存和交换空间使用量的信息。

`swapinfo` 在 BSD 和 HP-UX 系统上可用。其他平台使用以下交叉参考中列出的命令来显示关于交换空间利用率的信息。

| AIX | BSD | HP-UX | Linux | Solaris |
| :--- | :--- | :--- | :--- | :--- |
| lps | swapinfo | swapinfo | free | swap |

![](img/8f33496304c637dbf51ff6ddc3c7ff29_189_1.png)

常见用法示例：

- `swapinfo`: 在 BSD 和 HP-UX 系统上显示交换空间利用率

### sync

**用途**：刷新文件系统缓冲区。

**用法语法**：`sync`

```
### sync
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_190_0.png)

`sync` 命令刷新文件系统缓冲区。Unix、Linux 和 BSD 系统对磁盘活动进行批量处理以提高性能。当这种情况发生时，待处理的写入操作会在内存中缓存，并在适当的时间进行处理。`sync` 命令强制刷新缓冲区，从而完成所有待处理的写入操作。

虽然 `sync` 命令很少使用，但在系统必须以非正常方式重启的情况下，例如拔掉系统电源或按下重置按钮，它可能很有用。在这种方式下关闭系统电源之前执行 `sync` 可以通过确保所有磁盘缓冲区完全刷新来帮助防止文件系统损坏。

> **提示**
>
> 执行两次 `sync` 命令是确保所有文件系统缓冲区都已刷新的常见做法。可以通过在命令行执行 `sync; sync` 用一条命令完成。

常见用法示例：

- `sync`: 刷新文件系统缓冲区
- `sync ; sync`: 彻底刷新文件系统缓冲区

## 第 11 节：备份和恢复命令

### 概述

本节涵盖用于备份和恢复文件的实用工具。创建良好的备份对于从系统故障或自然灾害中恢复非常重要。大多数系统都包含许多内置的备份程序。这些程序可以创建完全备份、部分备份和增量备份，并且应纳入您的灾难恢复计划中。

**本节涵盖的命令：**

| 命令 | 用途 |
| --- | --- |
| `tar` | 创建/提取归档文件。 |
| `dump` | 创建增量备份。 |
| `restore` | 从 dump 归档中恢复文件。 |
| `dd` | 创建数据设备的原始副本。 |
| `cpio` | 创建/提取 cpio 归档。 |
| `mt` | 控制磁带设备。 |
| `mksysb` | 创建 AIX 系统的备份映像。 |

**本节使用的术语表：**

| 术语 | 定义 |
| --- | --- |
| `完全备份` | 包括本地系统上所有文件的备份。 |
| `增量备份` | 仅包括自上次完全备份以来已更改的文件的备份。 |

### tar

**用途**：创建/提取归档文件。

**用法语法**：`tar [OPTIONS] [OUTPUT] [INPUT]`

```
# tar -cvf backup.tar /etc/*
/etc/acpi/
/etc/acpi/stopbtn.sh
/etc/acpi/videobtn.sh
/etc/acpi/ibm-wireless.sh
/etc/acpi/hibernate.sh
/etc/acpi/resume.d/
/etc/acpi/resume.d/15-video-post.sh
/etc/acpi/resume.d/62-ifup.sh
/etc/acpi/resume.d/10-thinkpad-standby-led.sh
...
```

使用 `tar` 命令创建 `/etc` 目录的备份归档

`tar` 命令创建和提取 tar 归档。它是 Unix、Linux 和 BSD 系统上最常用的备份创建实用工具。在上面的示例中，使用 `-cvf` 选项创建名为 `backup.tar` 的 `/etc` 目录备份归档。

在下一个示例中，使用 `-xvf` 选项从第一个示例创建的归档中提取 `/etc/hosts` 文件。

```
# tar -xvf backup.tar etc/hosts
etc/hosts
```

从 tar 归档中提取文件

![](img/8f33496304c637dbf51ff6ddc3c7ff29_192_0.png)

> `tar` 命令的默认操作会去掉文件路径开头的 `/`。这意味着从 `tar` 归档中恢复的文件将放置在相对于当前目录的位置。可以指定 `-p` 选项来覆盖此行为。

常见用法示例：

- `tar -cvf [FILE] [ITEM]`: 备份指定项
- `tar -czvf [FILE] [ITEM]`: 压缩归档以节省空间
- `tar -xvf [FILE] [ITEM]`: 恢复指定项
- `tar -tf [FILE]`: 列出指定归档中的所有文件

### dump

**用途**：创建增量备份。

**用法语法**：`dump [OPTIONS] [OUTPUT] [INPUT]`

```
# dump -0 -uf backup.dump /
```

使用 dump 命令创建完全备份
