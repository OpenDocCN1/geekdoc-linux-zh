

# 138 | Linux命令大师

```
top - 08:39:30 1:23, 2 users, load average: 0.15, 0.12, 0.14
Tasks: 331, 2 running, 129 sleeping, 0 stopped, 0 zombie
Cpu(s): 14.5 us, 16.9 sy, 0.0 ni, 65.3, 5.3 wa, 0.0 hi, 0.0 si, 0.0 st
KIB Mem: 502812 total, 18852 free, 24584 cached
KIB Swap: 198908 total, 186476 used, 211032 cached Mem
```

| PID | USER | PR | NI | VIRT | RES | SHR | SMEM | TIME | COMMAND |
|---|---|---|---|---|---|---|---|---|---|
| 921 | 20 | 0 | 486600 | 94908 | 30172 | S | 14,6 18,9 | 02:26:42 | gnome-shell |
| 610 | 20 | 0 | 120866 | 24712 | 19832 | S | 9,6 4,9 | 01:22:04 | gnome-screen |
| 2172 | 7 | 0 | 57826 | 23604 | 28296 | S | 5,7 5,5 | 00:02:20 | gnome-screen |
| 7 | 20 | 0 | 0 | 0 | R | 1,3 8,0 | 00:02:20 | rcu_sched |
| 2169 | 20 | 0 | 49964 | 2740 | 2368 | R | 0,3 0,5 | 00:08:18 | top |

## Pgrep

使用 **pgrep** 命令可以根据某些标准列出内存运行的进程。要对运行中的进程进行更改，我们必须先找到该进程。例如，要查找关于 **apache** 的进程，我们可以使用 **pgrep apache2**（必须有一个 apache 服务才能使用）。

```
root@kemal:~# pgrep apache2
2293
2297
2298
2299
2300
2301
2302
```

通过此命令，我们可以看到 apache 服务的进程号 (pid)。如果我们想查看带有进程名称的数字，必须使用 **-l** 参数。我们的命令可能是 **pgrep -l apache2**。

```
root@kemal:~# pgrep -l apache2
2293 apache2
2297 apache2
2298 apache2
2299 apache2
2300 apache2
2301 apache2
2302 apache2
```

要查找任何用户的进程，可以使用 `pgrep -lu <user>` 命令。

```
root@kemal:-# pgrep -lu root
1 systemd
2 kthread
3 ksoftirqd/0
5 kworker/0:0H
7 rcu_sched
8 rcu_bh
9 migration/0
10 watchdog/0
11 helper
12 kdevtmpfs
13 netns
```

## Kill-Killall

使用 kill 和 killall 命令来结束进程。这些命令的工作如下：

- kill <pid> : 终止带有 pid 的进程
- kill -9 <pid> : 强制杀死无法终止的进程
- killall <process_name> : 终止所有名为该名称进程
- kill -9 <process_name> : 强制杀死坚持不退的服务
- killall -i <process_name> : 交互式地终止进程

例如，要终止所有带有 apache 服务，让我们使用 killall apache2。

# 140 | Linux命令大师

```
root@kemal:-# pgrep -l apache2
2293 apache2
2297 apache2
2298 apache2
2299 apache2
2300 apache2
2301 apache2
2302 apache2
root@kemal:-# killall apache2
root@kemal:-# pgrep -l apache2
root@kemal:-#
```

现在让我们尝试 killall -i apache2 来交互式地终止与服务相关的进程。

```
root@kemal:-# pgrep -l apache2
2681 apache2
2685 apache2
2687 apache2
2688 apache2
2689 apache2
2690 apache2
root@kemal:-# killall -i apache2
Kill apache2(2681) ? (y/N)
Kill apache2(2685) ? (y/N)
```

## Xkill

在 X 会话中，如果应用程序响应可以使用 xkill 命令。鼠标指针变成骷形状，我们可以点击想要终止的应用程序窗口。

## F-Bg

最后，让我们谈谈在后台执行进程。当进程运行时，终端无法输入新命令直到进程完成。但如果我们把运行中的进程发送到后台，可以使用另一个命令。有两种方法将命令或运行中的进程发送到后台：使用 ctrl+Z 切断进程并使用 bg 命令发送到后台；或者使用 fg 命令将其带回。

```
root@kemal:-# tail -f
tail: 警告: 跟踪标准输入无效
[1]+ Stopped tail -f
root@kemal:-# bg
[1]+ tail &
root@kemal:-# jobs
[1]+ tail -f
root@kemal:-# fg
tail -f
~
root@kemal:-# _
```

# 第12 章 磁盘操作

磁盘相关过程：分区、坏块测试、根据任何系统格式化、备份。有很多用的命令可以完成这些操作。

## Fdisk

磁盘分区时可以使用 fdisk 工具。你的数据可能会丢失。首先，要查看磁盘分区必须使用类似 fdisk -l 或 fdisk -l /dev/sda 的命令。

```
root@kemal:~# fdisk -l
/dev/sda: 31.3 GiB, 336876120 bytes, 6580160 sectors
扇区单位 * 512 = 512 
扇区大小 (逻辑/物理): 512 字节 / 512 字节
I/O 大小 (最小/最优): 512 字节 / 512 字节
磁盘标签: dos 0x73f44
```

| 设备 | 引导 | 起始 | 结束 | 扇区 | 大小 | Id | 类型 |
|---|---|---|---|---|---|---|
| /dev/sda | * | 2948 | 70681151 | 76079164 | 36.6G | 83 | Linux |
| /dev/sdb | | 70681152 | 71399391 | 71823994 | 350.194M | 5 | 扩展 |
| /dev/sdc | | 71399392 | 73455207 | 2056192 | 1024M | 82 | Linux Solaris |

如果我们不带任何参数使用 fdisk /dev/sda 命令，我们将看到等待命令的屏幕。

```
root@kemal:~# fdisk /dev/sda
欢迎使用 fdisk (util-linux 2.25.2)。更改将仅留在内存中，由你决定是否写入。在使用命令前请小心。
命令 (m 获得帮助):

帮助:
- m 菜单
- p 分区表
- n 创建新分区
- a 创建引导分区
- d 删除分区
- l 列出磁盘分区
- q 退出
- w 保存并退出
```

## Cfdisk

再次，分区磁盘 cfdisk 命令是 fdisk 的简单界面版本。当你输入 cfdisk 命令时，你会看到类似这样的屏幕：

![](img/aa6ce54dbb8ffe5bd7befb8c6764064_144_0.png)

## Badblocks

使用 badblocks 命令来确定磁盘上的块。如果有坏块，将尝试通过 fsck 命令修复这些块。我想从 USB 闪盘创建一个示例。首先使用 fdisk -l 列出我们系统中的分区。

```
root@local:~# fdisk -l
/dev/sda: 37.3 GiB, 400877120 bytes, 7814016 sectors
扇区单位 * 512 = 512 字节
扇区大小 (逻辑/物理): 512 字节 / 512 字节
I/O 大小 (最小/最优): 512 字节 / 512 字节
磁盘类型: dos
磁盘标识符: 0x73afd5
```

| 设备 | 引导 | 起始 | 结束 | 扇区 | 大小 | Id | 类型 |
|---|---|---|---|---|---|---|
| /dev/sda | * | 2948 | 70681151 | 76079164 | 36.6G | 83 | Linux |
| /dev/sdb | | 70681152 | 71399391 | 71823994 | 350.194M | 5 | 扩展 |
| /dev/sdc | | 71399392 | 73455207 | 2056192 | 1024M | 82 | Linux Solaris |

如果我们不带任何参数使用 fdisk /dev/sda 命令，我们将看到等待命令的屏幕。

在此输出中，/dev/sdb 显示了 USB 闪盘。为了测试我的闪盘，我使用 badblocks -v /dev/sdb 命令。

```
root@kemal:-# badblocks -v /dev/sdb
正在检查 0 到 978431 之间的块
正在检查坏块 (只读测试): 完成

测试完成，找到 0 个坏块。(0/0/0) 错误

## Fsck

磁盘上的坏块区域将尝试通过 fsck 工具修复。当我们的系统首次启动时，该工具会在后台运行并自动检查磁盘。例如，要修复 USB 内存棒中的错误，可以使用 fdisk -p /dev/sdb 命令。我们将在后续问题中看到，在使用此类工具时必须先将磁盘从系统中卸载。

```
root@kemal:-# fsck -p /dev/sdb
fsck from util-linux 2.25.2
fsck.fat 3.0.27 (2014-11-12)
/dev/sdb: 506 files, 175330/244127 clusters
```

