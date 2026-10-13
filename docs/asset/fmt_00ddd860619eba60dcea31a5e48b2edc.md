
Linux 系统上最重要的数据位于用户目录中，这些目录位于 `/home` 目录下。将系统数据和用户数据隔离有助于防止数据丢失，并使备份过程更加容易。例如，将用户数据放置在单独的文件系统上，或从网络上的远程计算机挂载，可能有助于在系统硬件故障时保护用户免受数据丢失的影响。

## 使用 `/proc` 目录的内容与内核交互

`/proc` 目录的内容是从内存中创建的，仅在 Linux 运行时存在。该目录包含特殊的“文件”，这些文件要么从内核提取信息，要么向内核发送信息。许多 Linux 工具从这个目录（也称为虚拟文件系统）下动态创建的目录和文件中提取信息。例如，`free` 命令从名为 `meminfo` 的文件中获取其信息：

```bash
$ free
        total         used       free     shared      buffers     cached
Mem:      255040      250752       4288          0         1716       90964
-/+ buffers/cache:    158072       96968
Swap:       524280        760      523520
```

随着系统的使用，这些信息不断变化。您可以使用 `cat` 命令查看 `meminfo` 文件的内容来获得相同的信息：

```bash
$ cat /proc/meminfo
MemTotal:     255040 kB
MemFree:       4412 kB
Buffers:       2164 kB
Cached:        90580 kB
SwapCached:     0 kB
Active:        208884 kB
Inactive:       8976 kB
HighTotal:      0 kB
HighFree:       0 kB
LowTotal:     255040 kB
LowFree:        4412 kB
SwapTotal:    524280 kB
SwapFree:     523520 kB
Dirty:          40 kB
Writeback:      0 kB
Mapped:        201520 kB
Slab:          24772 kB
CommitLimit:   651800 kB
Committed_AS:  341544 kB
PageTables:    2880 kB
VmallocTotal:  770040 kB
VmallocUsed:   3432 kB
VmallocChunk:       762312 kB
HugePages_Total:     0
HugePages_Free:      0
Hugepagesize:        4096 kB
```

`/proc` 目录还可用于通过向 `/proc/sys` 目录下的特定文件回显数值来动态改变运行中的 Linux 内核的行为。例如，要开启针对一种称为 SYN 泛洪的拒绝服务（DOS）攻击的内核保护，请使用 `echo` 命令将数字 1（一）发送到以下 `/proc` 路径：

```bash
# echo 1 >/proc/sys/net/ipv4/tcp_syncookies
```

> **注**
>
> Linux 内核内置了多种保护机制，但良好的系统管理安全策略以及保护您的网关、路由器或互联网连接系统的安全防火墙，是您能使用的最佳保护。有关防火墙配置及随 Fedora 提供的 Red Hat 网络安全工具实施示例的概述，请参见第 18 章中的“保护您的网络”部分。

使用 `/proc` 目录的其他方法包括

- 获取 CPU 信息，例如从 `/proc/cpuinfo` 获取系列、类型和速度。
- 查看 `/proc/net` 下的重要网络信息，例如 `/proc/net/dev` 下的活动接口信息、`/proc/net/route` 中的路由信息以及 `/proc/net/netstat` 中的网络统计数据。
- 检索文件系统信息。
- 通过 USB 报告媒体挂载点信息；例如，如果系统检测到 USB 摄像头或硬盘，Linux 内核会报告用于访问文件（如 `/dev/sda`）的设备。您可以使用 `dmesg` 命令查看此信息，或在设备文件系统目录 `/proc/devfs` 下查找有关这些设备的信息（如果安装了 Linux 内核源代码，请参阅 http://www.atnf.csiro.au/~rgooch/linux/docs/devfs.html 上的 Linux Devfs 常见问题解答）。文件 `/usr/src/linux-2.6/Documentation/usb/proc_usb_info.txt` 包含关于 USB 和 `/proc` 目录的一般信息，以及此目录下文件的预期内容。请注意，`devfs` 可能受支持，但在 2.6 内核中通常将过时，因为 `/proc/udev` 取代它成为管理系统中热插拔设备的方式。
- 获取 `/proc/version` 中的内核版本，`/proc/uptime` 中的性能信息（如正常运行时间），或 `/proc/stat` 中的其他统计信息，如 CPU 负载、交换文件使用情况和进程。

## 在 `/usr` 目录中处理共享数据

`/usr` 目录（如果执行完全安装，大小约为 5GB）包含软件应用程序、库和其他类型的共享数据，可供系统中的任何用户使用。许多 Linux 系统管理员会为 `/usr` 分配一个独立的分区。`/usr` 下的若干子目录包含 X 窗口系统（`/usr/X11R6`）、手册页（`/usr/share/man`）、软件包的共享文件（`/usr/share/软件包名称`，例如 `/usr/share/emacs`）、额外的应用程序或软件包文档（`/usr/share/doc`），以及一个完整的本地构建和安装软件的子目录树 `/usr/local`。

## 在 `/tmp` 目录中存储临时文件

顾名思义，`/tmp` 目录用于临时文件存储；在使用 Linux 时，各种程序会在此目录中创建文件。`/tmp` 目录中的陈旧文件每天由 `tmpwatch` 命令清理。（陈旧文件是指在 10 天内未被使用的任何文件。）Fedora 默认配置使用 `tmpwatch` 每天检查 `/tmp`，这是通过系统中调度表 `/etc/crontab` 的设置实现的。

## 访问 `/var` 目录中的可变数据文件

`/var` 目录包含由各种系统服务用于暂存和日志记录的子目录。许多这些可变数据文件，如打印暂存队列，是临时的；而另一些，如系统和内核日志，则在使用中进行重命名和轮转。

传入的电子邮件通常被定向到 `/var/spool/mail` 下的文件。

Linux 还使用 `/var` 来管理其他重要的系统服务。这些包括位于 `/var/ftp` 下的最顶层文件传输协议（FTP）目录（参见第 24 章“使用 FTP 进行远程文件服务”），以及系统 Apache Web 服务器的初始主页目录 `/var/www/html`。（有关使用 Apache 的更多信息，请参见第 21 章“Apache Web 服务器管理”。）

## 登录和使用 Linux

你可以通过多种方式访问和使用 Linux 系统。一种方式是使用连接到 PC 的显示器、键盘和鼠标在控制台处。另一种方式是通过串行控制台，要么通过电话调制解调器拨号，要么通过运行终端模拟器的 PC 并通过空 modem 线连接到 Linux PC。你还可以使用 `telnet` 或 `ssh` 命令通过有线或无线网络连接到你的系统。本节中的信息展示了如何使用物理和远程基于文本的登录来访问和使用 Linux 系统。

> **注意**
>
> 本章侧重于基于文本的登录和 Linux 的使用。图形登录和使用图形桌面在第 6 章的“启动 X”一节中描述。

### 基于文本的控制台登录

如果你坐在 PC 前并登录到一个没有启动图形登录的 Linux 系统，你会看到类似这样的提示：

> Fedora Core 发行版 4 (Stentza)
>
> 内核 2.6.13-1.1532_FC4 运行在 i686 上
>
> 登录：

你的提示可能因你使用的 Fedora 版本而异。无论如何，在此提示下，输入你的用户名并按下 Enter。当提示你输入密码时，输入它并按下 Enter。

> **注意**
>
> 请注意，你的密码不会回显给你，这是一个好主意。为什么这是一个好主意？好吧，这样可以防止别人从你的肩膀旁看到你的屏幕输入。不难猜测，五个字母的密码可能对应用户配偶的名字！

### 使用虚拟控制台
