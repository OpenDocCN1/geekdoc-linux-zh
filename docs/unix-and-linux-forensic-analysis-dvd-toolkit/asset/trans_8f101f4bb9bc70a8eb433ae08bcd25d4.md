

# /Proc 文件系统 • 第6章

这些子目录中存储了海量信息，但大部分与我们的调查无关。不过，我们可以在不使用任何额外的系统命令的情况下，确认我们正准备镜像的设备的大小。

```
root@localhost block]# ls -1 sda/

drwxr-xr-x 3 root root 0 2008-04-09 17:40 sda
drwxr-xr-x 3 root root 0 2008-04-09 17:39 sda2
-r--r--r-- 1 root root 4096 2008-04-09 17:40 size
```

我们看到了两个值得注意的子目录和一个文件 sda：sda1、sda2 和 size。
root@localhost]# cat size
16777216

这对应于我们物理磁盘的完整大小（8 gigabytes）。现在，我们可以确定这 8 GB 磁盘上的分区位于何处。首先是 sda1 (/boot)：
root@localhost]# cat sda1/start
63

接下来是 sda2（包含我们所有非启动分区的 LVM）：
root@localhost]# cat sda2/start
4016562
root@localhost]# cat sda2/size
163702335

我们可以使用 Sleuthkit 中的 “mmls” 来确认这些数字。
root@localhost tmp]# mmls /dev/sda
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

| Slot | Start | Length | Description |
| :--- | :--- | :--- | :--- |
| 00: | ----- | 000000000 | 000000000 | 000000001 Primary Table (#0) |
| 01: | ----- | 000000001 | 000000062 | 000000062 Unallocated |
| 02: | 00:00 | 0000000063 | 0000401624 | 0000401624 Linux (0x83) |
| 03: | 00:01 | 0000401625 | 0016717859 | 0163702335 Linux Logical Volume Manager (0xe8) |
| 04: | ----- | 0016771860 | 0016772175 | 000005356 Unallocated |

> sleuthkit.org

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_174_0.png)

# 第7章

# 文件分析

本章解决方案涉及：

- Linux 启动过程
- 系统与安全配置文件
- 日志文件
- 识别其他感兴趣的文件

# Linux 启动过程

Linux 启动过程的第一步是加载内核。内核通常位于 /boot 目录，并由引导加载程序引用。现代 Linux 发行版将使用统一引导加载程序 (GRUB)，而某些发行版（如 Slackware）仍将使用 Linux 加载器 (LILO)。它们的作用相同：加载内核并启动系统。让我们查看示例 grub.conf 文件中的一些相关条目：

```
default=0
timeout=5
```
这表示在延迟 5 秒后启动的默认 grub 条目是第一个（在我们的案例中也是唯一的）。

```
title Fedora (2.6.23-fc8)
```
这是在该特定 GRUB 条目（也称为 stanza）处显示的标题。它告诉 GRUB 在哪个物理设备查找后续数据；hd0 是第一个硬盘和第一个分区。双启动或多硬盘系统可能有不同的值，但这是标准：

```
kernel /vmlinuz-2.6.23-fc8 root=/dev/VolGroup0 quiet
```
该行提供了如果选择此条目将加载的内核可以通过 /proc/cmdline 识别启动选项。如果运行系统的 /proc/cmdline 输出与此处列出的，说明有人手动编辑过启动选项。

```
initrd /initrd-2.6.23-fc8.img
```
这提供了启动时将使用的初始内存磁盘 (initrd) 的位置。内存磁盘通常包含启动所需的模块（设备驱动程序、文件系统模块、逻辑卷模块等），但并非直接构建在内核中。一旦引导加载程序加载内核，内核将初始化 /sbin/init。

# init 与运行级别

Init 是 Linux 系统上的第一个进程。你可能记得 /proc 文件中的条目——它是如何工作的？类 Unix 系统有两种通用处理方式：System V 和 BSD 样式。Linux 发行版大多数情况下（包括 init 的任务和运行级别处理）遵循 System V。init 读取 /etc/initab 并执行其中的指令。这是一个相当标准的 Fedora 8 initab。使用的运行级别如下：

```
# Default runlevel
# 0 halt (不要将 initdefault 设置为此)
# 1 Single user mode
# 2 Multiuser, without NFS (如果没有网络则与3 相同)
# 3 Full multiuser mode
# 4 unused
# 5 X11
# 6 reboot (不要将 initdefault 设置为此)
```

```
id:5:initdefault:
```
此节定义了系统将启动到的默认运行级别。运行级别描述了系统的运行状态。在运行级别 1，一组服务将运行；在运行级别 2，运行另一组，依此类推。上面描述了七个运行级别，但通常默认是两者之一：3（带网络的文本模式多用户）或 5（带网络的图形模式多用户）。

```
# System initialization.
::sysinit:/etc/rc.d/rc.sysinit
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
```

> ¹ http://en.wikipedia.org/wiki/System_V
² http://en.wikipedia.org/wiki/BSD

```
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

然后，根据我们的默认运行级别 5，init 会在运行 /etc/rc.d/rc 5 之前运行 /etc/rc.d/rc.sysinit。随后 /etc/rc.d/rc 将根据脚本遍历 /etc/rc.d/ 并杀死进程。（见图 7.1。）

# 图 7.1 rc5.d 的内容

![](img/fd8e85097b37559dbc07dc22fd8cb1fe)

> 注意，目录中的每个条目都是 /etc/init.d/ 中脚本的符号链接，根据符号链接的名字启动或停止。每个脚本都包含了大量的变量和用于优雅启动或停止服务的操作。

```
# Run getty in standard runlevels
1:2345:respawn:/sbin/getty tty1
2:2345:respawn:/sbin/getty tty2
3:2345:respawn:/sbin/getty tty3
4:2345:respawn:/sbin/getty tty4
5:2345:respawn:/sbin/getty tty5
6:2345:respawn:/sbin/getty tty6
# Run getty in standard runlevels
5:initdefault: 
```
最后，init 派生六个虚拟终端并启用图形显示。(img/fd8e85097b37559dbc07dc22fd8cb1fe_174_0.png)

如你所见，入侵者可以在许多地方设置对受损系统的访问权限。即使在精简的系统中，仔细审查所有配置文件也是强制性要求的；然而，我们将详细介绍一些更相关且重要的系统和安全文件的位置和功能。

# 用户、组与权限

对于嫌疑人，你可能想知道的首要信息是“谁有权访问这台机器？”/etc/passwd 会告诉你：
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin/nologin
admin:x:3:4:admin:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/bin/sync
down:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/etc/news:/sbin/nologin
uuc:x:10:14:uuc:/var/spool/uuc:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/user/games:/sbin/nologin
