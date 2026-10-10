
## restore

用途：从转储归档中恢复文件。

用法语法：`restore [OPTIONS] [FILE]`

```bash
# restore -if backup.dump
restore > pwd
/
restore > cd etc
restore > add hosts
restore > extract
…
```
从转储归档中恢复文件

`restore` 命令用于从由 `dump` 命令创建的归档中恢复文件。上述示例演示了启动交互式 `restore` shell 以从 `dump` 归档中提取文件。

下表介绍了基本的 `restore` shell 命令。

| 命令 | 功能 |
| :--- | :--- |
| `ls [PATH]` | 列出当前目录或指定目录的内容 |
| `cd [PATH]` | 在转储归档中导航 |
| `pwd` | 显示当前工作目录 |
| `add [PATH]` | 将当前目录（或指定项）添加到恢复列表 |
| `delete [PATH]` | 从恢复列表中删除当前目录（或指定项） |
| `extract` | 提取恢复列表中的所有文件 |
| `help` | 显示帮助菜单 |
| `quit` | 退出恢复 shell |

恢复 shell 命令

常用用法示例：
- `restore -if [FILE]`：在恢复 shell 中打开指定归档
- `restore -rf [FILE]`：从转储归档中恢复整个文件系统
- `restore -tf [FILE]`：列出指定转储归档中的所有项目

## dd

**用途：** 创建数据设备的原始副本。

**用法语法：** `dd if=[SOURCE] of=[TARGET] [OPTIONS]`

```bash
# dd if=/dev/sdb of=/dev/sdc
使用 dd 命令创建磁盘副本
```

`dd` 命令执行数据设备的原始（逐位）复制。`if` 参数指定要读取的输入文件或设备。`of` 参数指定输出位置。在上述示例中，整个硬盘 `/dev/sdb` 被复制到 `/dev/sdc`。

`dd` 也可用于创建磁盘映像文件。下一个示例演示如何使用 `dd` 从 CD-ROM 创建 ISO 映像文件。

```bash
# dd if=/dev/cdrom of=/tmp/image.iso
使用 dd 命令将 CD-ROM 转换为 ISO 文件
```

> **警告**
> 由于如果误用 `dd` 命令可能会造成严重破坏，因此它常被称为“数据毁灭者”。在尝试使用 `dd` 时请务必谨慎。

**常用用法示例：**
- `dd if=[SOURCE] of=[TARGET]` 创建指定设备的原始副本

## cpio

**用途：** 创建或提取 cpio 归档。

**用法语法：** `[INPUT] | cpio [OPTIONS] > [OUTPUT]`

```bash
# cd /etc
# ls | cpio -ov > /tmp/backup.cpio
adduser.conf
adjtime
aliases
alternatives
...
使用 cpio 命令创建备份
```

`cpio` 实用工具用于创建简单的备份。在上述示例中，`-ov` 选项创建 `/etc` 目录的 `cpio` 备份。

下一个示例演示如何使用 `-idv` 选项从 `backup.cpio` 归档中恢复文件。

```bash
# cd /etc
# cpio -idv < /tmp/backup.cpio
adduser.conf
adjtime
aliases
alternatives
...
从 cpio 归档中提取文件
```

> **注意**
> - `cpio` 是一个遗留程序，在现代系统中很少用于备份。
> - 使用 `tar` 和 `dump` 代替 `cpio`，因为它们提供了更完整且用户友好的备份解决方案。

常用用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `ls | cpio -ov > backup.cpio` | 备份指定的项目 |
| `cpio -idv < backup.cpio` | 恢复指定的项目 |
| `cpio --list < backup.cpio` | 列出指定归档中的所有项目 |

## mt

用途：控制磁带设备。

用法语法：`mt -f [DEVICE] [OPERATION]`

```bash
# mt -f /dev/rmt0 rewind
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_197_0.png)

**mt** 命令用于控制可移动磁带设备。它可以用来显示驱动器状态并管理其可移动介质。上述示例演示了如何使用 **mt** 命令将 `/dev/rmt0` 驱动器中的磁带倒带。

下表列出了与 **mt** 实用工具一起使用的常见操作。

| 操作 | 功能 |
| :---: | :--- |
| rewind | 磁带设备倒带 |
| retension | 重新张紧磁带 |
| erase | 擦除磁带 |
| status | 显示磁带设备状态 |
| offline | 倒带并弹出磁带 |

![](img/8f33496304c637dbf51ff6ddc3c7ff29_197_1.png)

常用用法示例：

```bash
mt -f [DEVICE] [OPERATION]
```

在磁带驱动器上执行指定操作

## mksysb

**用途：** 创建 AIX 系统的备份映像。

**用法语法：** `mksysb [OPTIONS] [DEVICE/FILE]`

```bash
# mksysb -i /dev/rmt0
Creating information file (/image.data) for rootvg.

Creating list of files to back up.

Backing up 64981 files.................................. 
51767 of 64981 files (79%).. 

64981 of 64981 files (100%)
0512-038 mksysb: Backup Completed Successfully.
      在 AIX 上创建 mksysb 备份
```

**mksysb** 命令创建 AIX 系统的备份映像。该映像可用于在系统故障时恢复基础操作系统。

在上述示例中，**mksysb** 系统映像被写入 `/dev/rmt0` 磁带设备。

> 注意 **mksysb** 不是传统备份的替代品，因为它不包含基础操作系统之外的文件。数据库、第三方软件等都不会在 **mksysb** 映像中进行备份。这些文件应使用其他方法（如 **tar** 命令）单独进行备份。

**常用用法示例：**
`mksysb -i [DEVICE/FILE]` | 创建系统映像备份

## 第 12 节：监控与故障排除

### 概述

本节介绍用于监控和排除 Unix、Linux 和 BSD 系统故障的命令。这些命令可用于诊断问题或解决性能问题。

**本节涵盖的命令：**

| 命令 | 用途 |
| :--- | :--- |
| top | 监控系统性能和运行中的进程。 |
| htop | Linux 的高级系统监视器。 |
| topas | AIX 系统的性能监视器。 |
| iotop | 监控磁盘输入和输出操作。 |
| mpstat | 显示处理器利用率信息。 |
| vmstat | 显示虚拟内存使用情况信息。 |
| iostat | 显示 I/O 利用率统计信息。 |
| dstat | 监控 CPU、磁盘、网络和交换分区利用率。 |
| nfsstat | 显示 NFS 统计信息。 |
| free | 显示系统内存和交换空间使用情况信息。 |
| df | 显示文件系统使用情况信息。 |
| du | 显示磁盘使用情况。 |
| uname | 显示有关操作系统信息。 |
| uptime | 显示系统在线运行了多久。 |
| dmesg | 显示内核日志消息。 |
| errpt | 在 AIX 系统上显示系统错误消息。 |
| strace | 跟踪系统调用和信号。 |
| ltrace | 跟踪库调用。 |
| lsmod | 显示 Linux 内核模块信息。 |
| insmod | 安装/移除内核模块。 |
| rmmod | 安装/移除内核模块。 |
| modinfo | 显示有关 Linux 内核模块的信息。 |
| **sysctl** | 在 Linux 和 BSD 系统上显示和编辑内核参数。 |

### 本节中使用的术语表：

- **I/O**
  （输入/输出）读取或写入磁盘驱动器的过程。

- **内核模块**
  内核的扩展，提供驱动程序、功能或服务。

- **库**
  应用程序使用的子例程集合。

- **负载平均值**
  一段时间内系统负载的平均值。

- **系统调用**
  程序请求访问系统资源（如内核设施或系统硬件）的过程。

- **跟踪**
  监控程序内部功能（如系统调用和库调用）的过程。

- **虚拟内存**
  物理内存和交换存储的逻辑组合。

## top

用途：监控系统性能和运行中的进程。

用法语法：`top [OPTIONS]`

```bash
$ top

top - 18:56:55 up 21 min, 2 users, load average: 0.22, 0.35, 0.31
Tasks: 140 total, 2 running, 138 sleeping, 0 stopped, 0 zombie
Cpu(s): 9.0%us, 2.0%sy, 0.1%ni, 85.1%id, 3.5%wa, 0.1%hi, 0.2%si, 0.0%st
Mem: 3988516k total, 1089196k used, 2899320k free, 35832b buffers
Swap: 3951948k total, 0k used, 3951948k free, 66484k cached

  PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
 5297 nick 20 0 19112 1224 892 R 4 0.0 0:00.02 top
  1 root 20 0 4100 920 632 S 0 0.0 0:01.16 init
  2 root 15 -5 0 0 0 S 0 0.0 0:00.00 kthread
  3 root RT -5 0 0 0 S 0 0.0 0:00.00 migration/0
  4 root 15 -5 0 0 0 S 0 0.0 0:00.82 ksoftirqd/0
  5 root RT -5 0 0 0 S 0 0.0 0:00.00 watchdog/0
  6 root RT -5 0 0 0 S 0 0.0 0:00.00 migration/1
  7 root 15 -5 0 0 0 S 0 0.0 0:00.00 ksoftirqd/1
  8 root RT -5 0 0 0 S 0 0.0 0:00.00 watchdog/1
  9 root 15 -5 0 0 0 S 0 0.0 0:00.01 events/0
 10 root 15 -5 0 0 0 S 0 0.0 0:00.04 events/1
 11 root 15 -5 0 0 0 S 0 0.0 0:00.00 khelper
```
使用 top 命令监控系统活动

top 是 Unix、Linux 和 BSD 系统的进程和性能监视器。top 输出的前几行显示关于处理器、内存和交换分区利用率的信息。屏幕的其余部分用于显示有关运行中进程的信息。进程列表每隔几秒钟更新一次，以显示资源消耗最大的进程。

> **提示** 有几个交互式命令可用于控制 top 命令的输出。在 top 中按 ? 键可获取这些命令的完整列表。

常用用法示例：

| 命令 | 描述 |
| :--- | :--- |
| top | 监控系统性能和进程 |
| top -u [USER] | 仅显示由指定用户拥有的进程 |
| top -d [SECONDS] | 按指定间隔（以秒为单位）更新 |
| top -i | 不显示空闲进程 |
