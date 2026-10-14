
`/bin` 和 `/sbin` 中的命令被保留是为了维护基础系统的完整性，不需要经常更新，或者根本不需要更新。通常情况下，这些目录中的命令是静态链接的，这意味着命令不依赖于使用 `/lib` 或 `/usr/lib` 目录的软件库。你系统中所有其他应用程序都是动态链接的，这意味着它们需要使用外部软件库（也称为共享库）来运行。这是这两类软件的特性。

# 第 10 章 命令行入门课程

| Mlocked | 48 KB |
| SwapTotal | 8787512 KB |
| SwapFree | 8787512 KB |
| Dirty | 136 KB |
| Writeback | 0 KB |
| AnonPages | 673760 KB |
| Mapped | 202308 KB |
| Shmem | 10396 KB |
| Slab | 129248 KB |
| SReclaimable | 107356 KB |
| SUnreclaim | 21892 KB |
| KernelStack | 2592 KB |
| PageTables | 30108 KB |
| NFS_Unstable | 0 KB |
| Bounce | 0 KB |
| WritebackTmp | 0 KB |
| CommitLimit | 10815352 KB |
| Committed_AS | 1553172 KB |
| VmallocTotal | 3435973837 KB |
| VmallocUsed | 342300 KB |
| VmallocChunk | 3435938764 KB |
| HardwareCorrupted | 0 KB |
| HugePages_Total | 0 |
| HugePages_Free | 0 |
| HugePages_Rsvd | 0 |
| HugePages_Surp | 0 |
| Hugepagesize | 2048 KB |
| DirectMap4 | 38912 KB |
| DirectMap2M | 4153344 KB |

可以通过向 `/proc/sys` 目录下的特定文件“回声”数值值，来动态更改运行中的 Linux 内核的行为。要“关闭”针对名为 SYN 洪的拒绝服务（DoS）攻击的内核保护，请使用 `echo` 命令将数字 1 写入以下 `/proc` 路径：

```
matthew@semour:-$ sudo echo 1 >/proc/sys/net/ipv4/tcp_syncookies
```

使用 `/proc` 目录的其他方式还包括：

- 从 `/proc/cpuinfo` 获取 CPU 信息，例如系列、类型和速度。
- 在 `/proc/net` 下查看重要的网络信息，例如 `/proc/net/dev` 中的活动接口信息、`/proc/net/route` 中的路由信息以及 `/proc/net/netstat` 中的网络统计数据。

## 导航 Linux 文件系统 117

- 取回文件系统挂载信息。
- 通过 USB 报告媒体挂点信息；例如，如果系统检测到 USB 摄像头或硬盘，Linux 内核会将设备访问文件指定为 `/dev/sda`。你可以使用 `dmesg` 命令查看此信息。
- 在 `/proc/version` 中获取内核版本，在 `/proc/uptime` 获取性能信息（如运行时间），或在 `/proc/stat` 获取其他统计数据（如 CPU 负载、交换文件使用情况和进程）。

## 在 `/usr` 目录中处理共享数据

`/usr` 目录包含了系统上任何用户都可以使用的软件应用程序、库和其他类型的共享数据。许多 Linux 系统管理员会为 `/usr` 分配独立的分区。`/usr` 下的若干子目录包含了帮助页（manual pages，位于 `/usr/share/man`）、软件共享文件（`/usr/share/name_of_package`，如 `/usr/share/emacs`）、额外的应用程序或软件包文档（`/usr/share/doc`）以及整个用于本地构建和安装软件的子目录树 `/local`。

## `/tmp` 目录中的临时文件存储

顾其名，`/tmp` 目录用于临时文件存储。在使用 Linux 时，各种程序会在此目录下创建文件。此目录中的文件会由 `cron` 任务每天清理并在每次系统启动时清理。

## 访问 `/var` 目录中的可变数据文件

`/var` 目录包含各种系统服务用于打印和日志的子目录。许多可变数据文件（如打印队列）是临时的，而其他文件（如系统和内核日志）在使用过程中会被重命名和轮换。输入的数据通常重定向到 `/var/spool/mail` 下的文件。

> 注意：Linux 还将 `/var` 用于其他重要的系统服务，例如 Apache 服务器的初始主页目录 `/var/www/html`。（有关使用 Apache 的更多信息，请参见第 25 章“Apache 服务器管理”）。

## 导航 Linux 文件系统

在 Linux 文件系统中，与它的前身 UNIX 一样，一切皆文件：数据文件、可执行程序，甚至是输入输出设备。这些文件被放置在系列类似于文件夹的目录中。目录无非特殊类型的文件，包含其他文件/目录的列表。这些文件和目录

![](img/3d6f0094eea43cca43a26f4e063dddf0_155_0.png)

用于创建一个层次结构，以便对特定类型的文件进行逻辑放置。本章稍后将讨论 Linux 文件系统的标准层次结构。首先，你将学习如何导航并与文件系统交互。

包含内容的目录被称为父

### 使用 ls 列出目录内容

`ls` 命令列出当前目录的内容。它通常单独使用，但 `ls` 也有许多选项（也称为开关），可以为你提供更多信息。如果你像之前描述的那样刚登录目录，`ls` 命令会列出家目录的文件和目录：

```
matthew@seymour:-$ ls
Documents      file.txt
```

本章中所有的目录列表为了节省空间都是简写的。`ls` 命令本身显示名称列表。有些是文件，有些是目录。如果你知道要找什么但记不起确名称，这很有用。然而，使用 `ls` 不显示隐藏文件。隐藏文件以点（.）开头，通常用于配置且不频繁访问。因此，它们不在基础目录列表中。你可以通过向命令添加开关来查看隐藏文件：

```
matthew@seymour:-$ ls -a
.bashlogout .bashrc .bash_history
```

```
matthew@seymour:-$ ls -al
total 608
drwxr-xr-x 38 matthew 4096 2015-05-04 08 .
drwxr-xr-x 2 root 4096 2015-05-16 20 ..
-rw-r--r-- 1 matthew 421 2015-06-04 27 .bash_history
```

```
-rw-r--r-- 1 matthew 220 2015-05-16 48 .bashlogout
-rw-r--r-- 1 matthew 335 2015-05-16 48 .bashrc
drwx-xr-x 1 matthew 4096 2015-05-21 42 .config
drwx-xr-x 1 matthew 4096 2015-05-16 07 Documents
-rw-r--r-- 1 matthew 335 2015-05-16 48 file.txt
drwx-xr-x 1 matthew 4096 2015-05-16 07 .local
drwx-xr-x 1 matthew 4096 2015-05-16 07 Music
drwx-xr-x 1 matthew 4096 2015-05-16 07 Pictures
-rw-r--r-- 1 matthew 675 2015-05-16 48 .profile
```
