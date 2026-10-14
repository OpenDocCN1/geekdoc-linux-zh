
# 第 10 章 命令行快速上手

按下回车键后，`less` 命令（一种称为分页器的 Linux 命令）会显示帮助页。`less` 命令是一个文本浏览器，你可以用它向前或向后（甚至是横向）滚动文档，以了解更多命令信息。输入字母 `h` 获取帮助，使用斜杠 (`/`) 输入搜索字符串，或按 `q` 退出。

没有人能记住所有内容。最优秀、经验丰富的管理员经常使用帮助页。查询复杂信息很容易的，因为这让你无需回想所有内容，使你专注于任务，而不是因为没有记住语法而惩罚自己。

> 注意

Linux 包含的几乎所有命令都有对应的帮助页；然而，某些命令没有，或者可能只有简单的页面。你也可以使用 `info` 读取关于某些命令更详细的信息，或作为其他命令的替代。例如，要了解更多关于 `info`（它有一个非常广泛的手册页），可以这样使用 `info` 命令：

```
info info
```

使用方向键浏览文档，按 `q` 退出阅读。

## 使用 apropos

Linux 与 UNIX 一样是一个自文档化系统，可以通过 `man` 命令访问帮助页。Linux 还提供了许多访问其文档的有用命令。你可以使用 `apropos` 命令（例如使用 `partition` 等关键字）来查找与分区相关的命令，如下：

```
matthew::seymour:- apropos partition
addpart (8) - 对 "add partition" ioctl 的简单封装
all-swaps (7) - 表示所有交换分区已完成的事件信号
fdisk () - Curses/俚语磁盘分区表操纵器
delpart (8) - 对 "del partition" ioctl 的简单封装
fdisk (8) - Linux 分区表操纵器
gparted () - 用于管理磁盘分区的 Gnome 分区编辑器。
Mpartition (1) - 分区 MSDS 硬盘
Partprobe (8) - 通知操作系统分区表更改
Partx (8) - 通知内核关于位于...分区的存在和编号
Pcreate (8) - 为 LVM 使用初始化磁盘或分区
Presize (8) - 调整 LVM2 使用的磁盘或分区的大小
sfdisk (8) - Linux 分区表操纵器
```

## 使用 whereis

要找到一个命令及其文档，你可以使用 `whereis` 命令。例如，如果你正在寻找 `fdisk` 命令，可以这样做：

```
matthew::seymour:- whereis fdisk
fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.8.gz
```

## 理解 Linux 系统层次结构

Linux 继承了 UNIX 这种规划良好的用于组织内容的层次结构。它并不完美，但通常是逻辑化且一致的，尽管发行版在例如 Fedora、Slackware 和 Ubuntu 之间切换时往往会进行一些修改，导致某些部分的精简和适配。表 10.1 显示了标准 Linux 发行版的某些顶层目录。

### 表 10.1 基础 Linux 目录

| 名称 | 说明 |
|---|---|
| `/` | 根目录 |
| `/bin` | 基本命令 |
| `/boot` | 引导加载器文件、Linux 内核 |
| `/dev` | 设备文件 |
| `/etc` | 系统配置文件 |
| `/home` | 用户家目录 |
| `/lib` | 共享库、内核模块 |
| `/lost+found` | 恢复文件的目录（如果在文件系统检查后找到） |
| `/media` | 可移动介质（如 DVD 和软盘）的挂载点 |
| `/mnt` | 本地、远程文件系统的常用挂载点 |
| `/opt` | 附加软件包 |
| `/proc` | 内核信息、进程控制 |
| `/root` | 超级用户 (root) 家目录 |
| `/sbin` | 系统命令（主要仅限 root 使用） |
| `/srv` | 存储与系统上运行的服务相关的信息 |
| `/sys` | 内核所用设备的实时信息 |
| `/tmp` | 临时文件 |
| `/usr` | 系统运行并非必需的软件，如应用程序 |
| `/var` | 变量数据（如日志）；暂存文件 |

这些目录可以帮助你在需要时找到文件。当在你安装新系统时，这些知识可以帮助你划分硬盘，让你选择将某些目录放在它们独立的分区上，这对于隔离目录与其他非常有用，例如在服务器安全案例中，将不经常更改的 `/boot` 目录放在其分区上，并在超级用户未进行特定操作期间设置为只读且不可更改。桌面用户可能不需要考虑这些，但当你想要查找特定程序的配置文件并设置某些系统范围选项以影响所有用户时，了解目录树仍然非常有帮助。

> 注意

有很多内容要记，尤其是刚开始时。作为参考，有一个 Linux 文件系统层次结构的帮助页：

```
matthew@semour:-$ man hier
```

这会返回一个详细的列表，并带有每个部分的描述。

表 10.1 中的一些重要目录（如包含用户和 root 命令或系统配置文件的目录）将在后续章节中讨论。在使用 Ubuntu 时，你可以使用并编辑这些目录下的文件。

## `/bin` 和 `/sbin` 中的基本命令

`/bin` 目录包含了系统运行和启动系统所需的各种命令。通常情况下，root 用户使用 `/bin` 目录中的命令。

即使操作系统被升级、损坏或重新安装，`/home` 也能完好无损地不受这些事件的影响。

## 使用 `/proc` 目录的内容与内核交互

`/proc` 目录的内容是从内存创建的，仅在 Linux 运行期间存在。该目录包含特殊文件，可以从中提取信息或向内核发送信息。许多 Linux 工具会从此目录下的动态创建的目录和文件中提取信息，该目录也被称为虚拟文件系统。例如，`free` 命令从名为 `meminfo` 的文件中获取信息：

```bash
matthew@semour:~$ free
```

| | total | used | shared | buffers | cached |
|---|---|---|---|---|---|
| Mem: | 4055680 | 2725684 | 1329996 | 188996 | 1551464 |
| -/+ buffers/cache: | 985224 | | 3070456 | | |
| Swap: | 8787512 | 0 | | 8787512 | |

这些信息随着系统的使用而不断变化。你可以使用 `cat` 命令查看 `meminfo` 内容来获取相同的信息：

```bash
matthew@semour:~$ cat /proc/meminfo
```

```
MemTotal: 4055680 KB
MemFree: 1329996 KB
Buffers: 189208 KB
Cached: 1551488 KB
SwapCached: 0 KB
Active: 1222172 KB
Inactive: 1192244 KB
Active (anon): 684092 KB
Inactive (anon): 16 KB
Active (file): 538080 KB
Inactive (file): 1192228 KB
Unevictable: 48 KB
Mlocked: 48 KB
SwapTotal: 8787512 KB
SwapFree: 8787512 KB
Dirty: 136 KB
Writeback: 0 KB
AnonPages: 673760 KB
Mapped: 202308 KB
Shmem: 10396 KB
Slab: 129248 KB
SReclaimable: 107356 KB
Sreclaim: 21892 KB
KernelStack: 2592 KB
PageTables: 30108 KB
NFS_Unstable: 0 KB
Bounce: 0 KB
WritebackTmp: 0 KB
CommitLimit: 10815352 KB
Committed_AS: 1553172 KB
VmallocTotal: 3435973836 KB
VmallocUsed: 342300 KB
VmallocChunk: 34359387644 KB
HardwareCorrupted: 0 KB
HugePages_Total: 0
HugePages_Free: 0
HugePages_Rsvd: 0
HugePages_Surp: 0
Hugepagesize: 2048 KB
DirectMap4: 38912 KB
DirectMap2M: 4153344 KB
```
