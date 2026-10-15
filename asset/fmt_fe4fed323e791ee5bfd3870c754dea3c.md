
其他文件是二进制文件或布尔开关。例如，如果你输入 `cat /proc/sys/net/ipv4/forward`，你将看到 0 或 1。0 表示内核没有转发网络包。通过使用命令将 `ip_forward` 文件的值改为 1，你可以立即开启数据包转发。

## /proc/ 中的目录

关于内核的常见信息组被在 `/proc/` 目录内的目录和子目录。

## /proc 目录

每个 `/proc/` 目录都包含许多以数字命名的目录。它们的列表可能如下所示：

| 权限 | 链接 | 所有者 | 组 | 大小 | 日期 | 名字 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| dr-xr-xr-x | 3 | root | root | 0 | Feb 13 01:28 | 1 |
| dr-xr-xr-x | 3 | root | root | 0 | Feb 13 01:28 | 1010 |
| dr-xr-xr-x | 3 | xfs | xfs | 0 | Feb 13 01:28 | 1087 |
| dr-xr-xr-x | 3 | daemon | daemon | 0 | Feb 13 01:28 | 1123 |
| dr-xr-xr-x | 3 | root | root | 0 | Feb 13 01:28 | 11307 |
| dr-xr-xr-x | 3 | apache | apache | 0 | Feb 13 01:28 | 13660 |
| dr-xr-xr-x | 3 | root | root | 0 | Feb 13 01:28 | 1337 |
| dr-xr-xr-x | 3 | rpcuser | rpcuser | 0 | Feb 13 01:28 | 667 |

这些目录被称为进程目录，因为它们以程序的进程 ID（PID）命名，并包含与该进程特定的信息。每个进程目录的所有者和组都设置为运行该进程的用户。当进程终止时，其 `/proc/` 进程就会消失。

除了进程的名称和 ID 之外，状态（例如 S（睡眠）或 R（运行））以及运行该进程的用户/组 ID 是可用的，还有更多关于内存使用的详细数据。

## /proc/self/

`/proc/self/` 目录是指向当前运行进程的链接。这允许进程查看自己而无需知道其进程 ID。在 shell 环境中，列出 `/proc/self/` 目录产生与列出该进程的目录相同的内容。

## /proc/bus/

此目录包含有关系统中可用各种总线的特定信息。例如，在标准的 ISA、PCI 和 USB 总线上，这些每个总线的当前数据可以在其目录 `/proc/bus/` 中可用。

子目录和文件的内容根据你系统的精确配置而大异。然而，每种类型的总线目录至少包含一个该类型总线的目录。单个总线目录（通常用数字 00 标记）包含指向该总线上可用各种设备的二进制文件。

例如，一个拥有 USB 总线但未连接 USB 设备的系统，有一个连接多个文件的 `/proc/bus/usb/` 目录。

`/proc/bus/usb/` 目录包含跟踪任何 USB 总线上各种设备的文件，以及使用它们所需的驱动程序。`/proc/bus/usb/001/` 目录包含第一个 USB 总线上的所有设备。通过查看设备文件的内容，你可以识别主板上的 USB 根总线。

## /proc/driver/

此目录包含内核使用的特定驱动程序的信息。在这里找到的一个常见文件是 `rtc`，它提供系统实时时钟（RTC）驱动程序的输出，该设备在系统关机时保持计时。有关更多信息请参阅 `/usr/src/linux-2.4/Documentation/rtc.txt`。

## /proc/fs

此目录显示导出了哪些文件系统。如果你正在运行 NFS 服务器，可以 `cat /proc/fs/nfs/exports` 来查看正在共享的文件系统以及授予这些文件系统的权限。

## /proc/ide/

此目录持有系统上 IDE 设备的信息。每个 IDE 通道都表示为一个单独目录，例如 `/proc/ide/ide0` 和 `/proc/ide/ide1`。

## /proc/sys/net/

此目录包含有关各种网络主题的各种目录。内核编译时的各种配置会产生不同的目录，此处有 `appletalk`、`ethernet`、`ipv4`、`ipx`、`ipv6`。在这些目录中，你可以调整运行中的系统以调整各种配置值。关于这些目录及其配置文件的可能取值的更多信息，可以在 `/usr/src/linux-2.4/Documentation/filesystems/proc.txt` 中找到。

对这些文件进行错误更改可能会影响你对系统的远程连接。

## /proc/sys/vm/

此目录便于 Linux 内核虚拟内存（VM）子系统的配置。内核广泛且智能地使用虚拟内存，虚拟内存通常称为交换空间（`swap space`）。`/usr/src/linux-2.4/Documentation/sysctl/vm.txt` 文件包含关于这些各种文件的额外信息。

## /proc/sysipc/

此目录包含关于 System V IPC 资源的信息。该目录中的文件与消息 (`msg`)、信号量 (`sem`) 和共享内存 (`shm`) 的 System V IPC 调用有关。

## /proc/tty/

此目录包含关于可用和当前使用的 tty 设备的信息。最初称为电打字设备（teletype device），任何基于字符的数据终端都称为 tty 设备。在 Linux 中，有三种 tty 设备：

- 串口设备 — 这些设备使用串行连接，例如通过调制解调器或使用串口线。
- 虚拟终端 — 这些设备创建公共控制台连接，例如通过在系统控制台上按 Alt-Function 键提供的虚拟控制台。
- 伪终端 — 这些设备创建供某些高级别应用程序（如 X11）使用的双向通信。设备文件是当前正在使用的 tty 设备列表。

### 最佳 /proc/ 资源

大部分 `/proc/` 文档在你的系统中可用：

- `/usr/src/linux-2.4/Documentation/filesystems/proc.txt` — 包含关于 `/proc/` 目录各方面的各种限制性信息。
- `/usr/src/linux-2.4/Documentation/sysrg.txt` — 系统请求（System Request）选项的概述。
- `/usr/src/linux-2.4/Documentation/sysctl` — 包含各种 sysctl 提示的目录，包括修改与内核相关（`kernel.txt`）、访问文件系统相关（`fs.txt`）以及虚拟内存使用（`vm.txt`）的值。
- `/usr/src/linux-2.4/Documentation/networking/ip-sysctl.txt` — 各种 IP 网络选项介绍。
- `/usr/src/linux-2.4` — 读取内核源码可以找到关于 `/proc/` 的最权威的信息。确保你的系统安装了 kernel-source RPM，并在 `/usr/src/linux-2.4` 目录中查看源码。
- `http://www.linuxuxhq.com` — 该网站维护了各种版本 Linux 内核源码、补丁和文档的完整数据库。

## 第 24 章
常用 MS-DOS 和 Linux 命令比较

在 shell 提示符下输入的许多 Linux 命令与你在 MS-DOS 中输入的命令相似。事实上，某些某些命令是完全相同的。

本章提供了 Windows 中 MS-DOS 提示符下使用的常用命令及其在 Linux 中的对应命令。还提供了这些命令在 Linux shell 提示符下使用的基本示例。注意，这些命令通常有许多选项。要了解更多关于每个命令的信息：

表 24-1：MS-DOS 和 Linux 命令比较

| 命令用途 | MS-DOS | Linux | Linux 示例 |
|---|---|---|---|
| 复制文件 | copy | Cp | `cp datafile.txt /home/directory` |
| 移动文件 | move | Mv | `mv datafile.txt /home/directory` |
| 列出文件 | dir | ls | `ls` |
| 清除屏幕 | cls | clear | `clear` |
| 关闭提示符窗口 | exit | exit | `exit` |
| 显示或设置日期 | date | date | `date` |
| 删除文件 | del | rm | `rm file.txt` |
| 在屏幕上“回显”输出 | echo | echo | `echo message` |
| 使用简单文本编辑器编辑文件 | edit | pico | `pico file.txt` |
| 比较文件内容 | fc | diff | `diff file1 file2` |
| 在文件中查找文本字符串 | find | grep | `grep word_or_phrase file.txt` |
| 格式化磁盘 | format a: (如果磁盘在 A: 中) | mke2fs or mformat | `/sbin/mke2fs /dev/fd0` (Linux 中的 A:) 等价物) |
| 显示命令帮助 | command /? | man | `man command` |
| 创建目录 | mkdir | mkdir | `mkdir directory` |
| 查看文件 | more | less | `less file.txt` |
| 重命名文件 | ren | mv | `mv this_file.txt that_file.txt` |
| 显示在文件系统中的位置 | chdir | pwd | `pwd` |
| 使用指定路径（绝对路径）切换目录 | cd pathname | cd pathname | `cd /directory/directory` |
| 使用相对路径切换目录 | cd .. | cd .. | `cd ..` |
| 显示时间 | time | date | `date` |
| 显示 RAM 数量和使用情况 | mem | free | `free` |

## 第 25 章 收集系统信息

有时你可能需要收集基本信息。例如，你应该知道如何找到空闲内存、可用驱动器空间、你的驱动器是如何划分的以及正在运行哪些进程。本章讨论了如何从 Red Hat 获取此类信息。

### 进程

有时你可能需要收集基本信息。例如，你应该知道如何查出正在运行的进程列表。

`/proc/sysipc/` 此目录包含关于 System V IPC 资源的信息。

`/proc/tty/` 此目录包含关于可用和当前使用的 tty 设备的信息。

`/proc/sys/vm/` 此目录便于 Linux 内核虚拟内存（VM）子系统的配置。

`/proc/sys/net/` 此目录包含有关各种网络主题的各种目录。

- 这些设备创建供某些高级别应用程序（如 X11）使用的双向通信。设备文件是当前正在使用的 tty 设备列表。

### 最佳 /proc/ 资源

大部分 `/proc/` 文档在你的系统中可用：

`/proc/sys/vm/` 此目录便于 Linux 内核虚拟内存（VM）子系统的配置。

`/proc/ipc/`

`/proc/tty/` 此目录包含关于可用和当前使用的 tty 设备的信息。

`/proc/sys/net/`

```
10:14 up 2 days, 19:28, 5 users, load: 0.10, 0.06
CPU: 2.7% user, 0.5% system, 0.0% nice, 96.6% idle
Mem: 256812k, 252016k used, 4796k free, 97280k shared, 43300k buff
Swap: 30532k, 1328k used, 26370k free, 86180k cached
```

Processes:
```
PID  PR  NI  VIRT    RES    SH %CPU %MEM COMMAND
17372  20  0     5.9M   319M   480K   0.5   1.2 emacs
14461  20  0     5.4M   210M   324K   0.1   1.3 gnome-terminal
17356  20  0     5.1M   105M   288K   0.5   0.4 top
15775  20  0     4.3M   102M   256K   0.0   0.2 sawfish
 4476  20  0     5.6M   544M   476K   0.0   0.1 update
 3476  20  0     5.5M   556M   460K   0.0   0.2 syslog
 3572  20  0     7.1M   712M   360K   0.0   0.2 logd
 3724  20  0     6.9M   692M   584K   0.0   0.5 lockd
 3888  20  0     3.8M   388M   500K   0.0   0.0 rpcid
 3891  20  0     3.8M   388M   500K   0.0   0.0 rpid
4144  20  0     4.3M   436M   372K   0.0   0.5 apmd
4764  20  0     5.9M   592M   496K   0.0   0.5 automount
```

要退出，按 q 键。

表 25-1：交互式命令

| 命令 |  |
|---|---|
| 空格 | 立即刷新显示。 |
| h | 显示帮助屏幕。 |
| k | 杀死进程。系统将提示进程 ID 和发送给它的信号。 |
| n | 更改显示的进程数量。系统将提示输入数字。 |
| u | 按用户排序。 |
| M | 按内存使用量排序。 |
| P | 按 CPU 使用率排序。 |

如果你更喜欢使用图形界面查看 top，可以使用桌面上的 GNOME System Monitor，点击 Main 按钮并选择 System Tools System Monitor（或者在 X Window 系统内的 shell 提示符中输入 `gnome-system-monitor`）。然后选择 Process Listing 标签。

GNOME System Monitor 允许你在运行进程列表中搜索所有进程、你的进程或活动进程。

要了解更多关于进程的信息，请选择它并点击 More Info 按钮。进程的详细信息将在窗口底部显示。

## 第 25 章：收集系统信息

要停止一个进程，选择它并点击“结束进程”（End Process）。此功能对于停止响应用户输入的进程非常有用。

要按特定列中的信息进行排序，请点击列名。用于对信息排序的列将以深灰色显示。

![](img/70f8904e8a1105c5df33b26207132b97_348_0.png)

图 25-1. GNOME 系统监器 — 进程列表标签

默认情况下，GNOME 系统监器不显示线程。要更改此偏好，选择“编辑”（Edit）⇨“选项”（Preferences），点击“进程列表”（Process Listing）标签，并选择“显示线程”（Show Threads）。该偏好还允许您配置间隔、默认显示每个进程的类型信息以及系统监器的颜色。

## 内存使用

`free` 命令显示系统的物理内存总量和交换空间总量，以及已、空闲、共享、内核缓冲区和缓存的内存量。以下是 `free` 命令的示例输出：

| total | used | free | shared | buffers | cached |
|---|---|---|---|---|---|
| Mem. | 256812 | 240668 | 16144 | 105176 | 50520 | 81848 |
| -+/buffers/cache: | 108300 | 148512 | | | | |
| Swap: | 265032 | 780 | 264252 | | | | |

使用 `free -m` 命令以兆字节为单位显示相同的信息，这样更容易读。

| | total | used | free | shared | buffers | cached |
|---|---|---|---|---|---|---|
| Mem: | 250 | 235 | 15 | 102 | 49 | 79 |
| -/+ buffers/cache: | | 105 | 145 | | | | |
| Swap: | 258 | 0 | | | | |

如果您更喜欢使用图形界面来查看内存情况，请使用 GNOME 系统监器。要从桌面启动系统监器，点击“主菜单”并选择“系统工具 -> 系统监器”（或在 X 窗口内的 shell 提示符处输入 `gnome-system-monitor`）。然后选择“系统监器”标签。

![](img/70f8904e8a1105c5df33b26207132b97_349_0.png)

图 25-2. GNOME 系统监器 — 系统监器标签

## 文件系统

`df` 命令报告系统的磁盘空间使用情况。如果您在 shell 提示符处输入命令 `df`，输出将类似于所示：

| Filesystem | Lk-blocks | Used Available Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/hda2 | 10325716 | 2902060 | 6899140 | 30% | / |
| /dev/hda1 | 15554 | 8656 | 6095 | 59% | /boot |
| /dev/hda3 | 2072264 | 2662456 | 1700573 | 14% | /home |
| none | | 256796 | 0 | 0% | /dev/shm |

默认情况下，`df` 以 1 千字节显示分区大小，并千字节显示已用和可用磁盘空间。要以兆字节和千字节查看信息，请对 `df` 使用 `-h` 选项。`-h` 选项表示“人类可读格式”（human-readable）。对于 `df -h` 命令，输出类似于所示：

| Filesystem | Size | Used | Available | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/hda2 | 9.8G | 2.8G | 6.5G | 30% | / |
| /dev/hda1 | 15M | 8.5M | 5.9M | 59% | /boot |
| /dev/hda3 | 20G | 2.6G | 16G | 14% | /home |
| none | 251M | | 250M | 0% | /dev/shm |

在分区列表（挂载点）中，你可以看到 `/dev/shm` 项。该条目代表系统的虚拟内存文件系统。

`du` 命令显示目录中文件估计占用的空间量。如果您在 shell 提示符处输入 `du`，每个子目录的磁盘使用情况将以列表形式显示。当前目录及其子目录的总计也将作为列表最后最后显示。如果您不想查看所有子目录的总计，请使用命令 `du -h` 仅以人类可读格式查看该目录的总计。

使用 `du --help` 命令查看更多选项。

要以图形格式查看系统分区和磁盘空间使用情况，请使用系统监器（如图 25-2 所示）。

## 硬件

如果您在配置硬件时遇到困难，或者只是想知道系统中有哪些硬件，可以使用“硬件浏览器”（Hardware Browser）应用程序显示可以探测的硬件。要从桌面启动该程序，点击“主菜单”并选择“系统工具 -> 硬件浏览器”（或在 shell 提示符处输入 `hwbrowser`），并在系统请求时输入 root 密码。硬件浏览器显示您的 CD-ROM 设备、软磁盘、硬盘（及其分区）、网络设备、系统设备和显卡。点击左侧菜单中所需的类别名称，即可显示信息。

### 2-3. 硬件

您也可以使用 `lspci` 命令（但仅限 root 用户）来列出所有 PCI 设备。**提示：使用 `lspci -v` 命令获取更多信息，或使用 `lspci -vv` 获取非常详细的输出。**例如，可以使用 `lspci` 来确定系统显卡的制造商、型号和内存大小，如下所示：
