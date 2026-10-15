

## 在 /etc 目录中使用和编辑文件

如果按照本书包含的软件进行默认安装，则在 /etc 目录下将有超过 2300 个系统配置文件和目录。一些主要软件包，例如 Apache、OpenSSH 和 xinetd，在 /etc 下有配置文件的目录。/etc 中其他重要的系统相关配置文件有

- fstab—系统文件系统表是一个文本文件，列出了连接到你的 PC 的每个硬盘、CD-ROM、软盘或其他存储设备。该表为每个设备的分区信息与 Linux 文件系统（目录布局）中的位置建立索引，并列出使用 Linux 时每个设备的其他选项。fstab 中的几乎所有条目都可由 root 使用 mount 命令进行操作。

- inittab—系统初始化表定义了默认运行级别，也称为运行控制级别或系统状态。对此文件的更改可以决定你的系统启动时进入图形登录还是文本登录，以及是否启用拨号远程访问。（你将在第 15 章“自动化任务”中“系统服务和运行级别”部分了解默认运行级别。）

- modprobe.conf—此配置文件包含在加载内核模块以启用各种类型的硬件（例如声音、USB、网络等）时使用的指令和选项（在第 35 章“管理模块”部分中讨论）。此文件的内容在启动时使用，并且文件可以手动编辑或由 Ubuntu 自动更新。

- passwd—系统的用户列表以及用户账户信息。此文件的内容可由各种程序更改，例如 useradd 或 chsh。

- printcap—系统的打印机功能数据库（在第 12 章“使用 Ubuntu 打印”中“Ubuntu 打印概述”部分讨论）。

- shells—已批准的 shell（命令行界面）列表。

## 保护用户目录 /home 的内容

Linux 系统上最重要的数据位于用户目录中，这些目录位于 /home 目录下。将系统数据和用户数据分开有助于防止数据丢失并使备份过程更轻松。例如，让用户数据驻留在单独的文件系统或从网络上的远程计算机挂载，可能会在系统硬件故障的情况下帮助用户免受数据丢失的影响。

## 使用 /proc 目录的内容与内核交互

/proc 目录的内容是从内存创建的，仅在 Linux 运行期间存在。此目录包含特殊的“文件”，它们要么从内核提取信息，要么向内核发送信息。许多 Linux 实用程序从此目录下的动态创建的目录和文件（也称为虚拟文件系统）中提取信息。例如，free 命令从名为 meminfo 的文件获取其信息：

```
$ free
          total       used       free     shared    buffers     cached
Mem:       256116     246208      9908          0      42964      50140
-/+ buffers/cache:     153104     103012
Swap:      409616      25820     383796
```

此信息会随着系统使用而不断变化。你可以使用 cat 命令查看 meminfo 文件的内容来获取相同的信息：

```
$ cat /proc/meminfo
MemTotal:       256116 kB
MemFree:         8920 kB
Buffers:        43080 kB
Cached:         50700 kB
SwapCached:         0 kB
Active:        140448 kB
Inactive:       34456 kB
HighTotal:         0 kB
HighFree:          0 kB
LowTotal:      256116 kB
LowFree:         8920 kB
SwapTotal:      409616 kB
SwapFree:       383796 kB
Dirty:             52 kB
Writeback:          0 kB
AnonPages:      81132 kB
Mapped:         41380 kB
Slab:           66416 kB
SReclaimable:    59152 kB
SUnreclaim:     7264 kB
PageTables:      1380 kB
NFS_Unstable:       0 kB
Bounce:             0 kB
CommitLimit:    537672 kB
Committed_AS:   281252 kB
VmallocTotal:   770040 kB
VmallocUsed:     3572 kB
VmallocChunk:   766268 kB
```
