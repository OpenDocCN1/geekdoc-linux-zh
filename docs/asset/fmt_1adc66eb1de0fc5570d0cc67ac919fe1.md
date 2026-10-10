
`bsdlabel ad0s` 显示 BSD 磁盘上的分区，分区 1

```
# bsdlabel ad0s          显示 BSD 磁盘上的分区，分区 1
# /dev/ad0s:
8 partitions:
# size    offset  fsize bps [cpg]
a 1048576      0       4.2BSD  2048 163844 8
b 975760               swap
c 4094962      0       # "raw" 部分，不要编辑
d 2584576    2024336  4.2BSD  2048 163844 28552
e 1048576    4608912  4.2BSD  2048 163844 8
f 3529134    5657448  4.2BSD  2048 163844 28552
```

`bsdlabel` 的输出显示了第一个 IDE 硬盘 (`ad0s1`) 第一个分区内的不同分区。你可以通过运行 `df` 命令显示已挂载的分区，更好地了解这些分区与你系统系统的关系：

```
# df -h          已挂载的分区
Filesystem      Size  Avail Capacity Mounted on
/dev/ad0s1      496M   39M  418M 8%        /
/devs           1.0K    0B  100%       /dev
/dev/ad0s11     496M   16K  456M 0%         /usr
/dev/ad0s11f    160     1.7G   13G  11%        /tmp
/dev/ad0s11d    1.2G    19M    2%         /var
```

如你所见，分区 `a`、`d`、`e` 和 `f` 分别挂载在根目录 (`/`)、`/var`、`/tmp` 和 `/usr` 上。分区 `b` 是交换分区。分区 `c` 是“原始”部分，不应修改。`devfs` 文件系统 `/dev` 提供了对计算机硬件设备的访问。

由于本章的讨论涉及启动过程，请参阅第 7 章有关 `bsdlabel` 和 `fdisk` 命令创建和修改磁盘分区及分用途的信息。

## 切换到 GRUB 引导程序

没有理由使用 `boot0` 引导程序来启动你的 BSD 系统。如今，许多人使用通用统一引导程序 (GRUB)，特别是在启动多个操作系统（如 Linux）的情况下。GRUB 具有一些功能，例如用于编辑启动选项的屏幕和菜单。

FreeBSD 提供了一个 `grub` 软件包。或者，如果需要，你可以从计算机上安装的其他系统之一来配置 GRUB。要在 FreeBSD 中安装 GRUB，请输入以下命令：

```
# pkg_add -r grub      安装 grub 软件包
```

接下来，你通过创建 `/boot/grub` 目录并将所需的 GRUB 文件复制到其中来设置 GRUB 文件。

```
# mkdir /boot/grub      创建 /boot/grub 目录
# cp -Rf /usr/local/share/grub/i386-freeBSD/ /boot/grub 将文件复制到 /boot/grub
```

接下来，你需要使用任何编辑器创建一个 `menu.list` 文件，告诉 GRUB 启动什么以及如何启动。在这个示例中，FreeBSD 系统和之前描述的 Debian GNU/Linux 系统设置为从 GRUB 启动屏幕启动。

```
default=0
timeout 15

title FreeBSD
root notify (hd0,0)
makeactive
chainloader +1

title Debian GNU/Linux
root (hd0,1)
chainloader +1
```

默认启动的操作系统是第一个 (`default=0`)，即 FreeBSD。GRUB 在启动操作系统之前会暂停 15 秒 (`timeout 15`)。由于引导程序同时安装在 FreeBSD 和 Debian 分区上，配置这两个系统的简单方法是使用链式加载器（`chainloader`）启动。这将让你看到这两个系统各自的二级启动屏幕。

现在你需要覆盖硬盘的主引导记录 (MBR)。由于默认情况下你可能无法写入硬盘的 MBR，请运行以下 `sysctl` 使覆盖 MBR 变得可行：

```
# sysctl kernel.geom.debugflags=16
```

一旦你创建了 `menu.list` 文件并能够写入主引导记录，就可以使用 `grub-install` 命令将其安装到主引导记录中。输入以下命令将 GRUB 安装到磁盘 `ad0` 的主引导记录中。

> 警告！你即将覆盖计算机的主引导记录。如果你在 `menu.list` 文件中执行了错误，`grub-install` 可能会失败。然而，如果写入完成的信息导致无法工作，你可以通过输入 `boot0cfg -B ad0` 随时恢复旧的 `boot0` 引导程序。

## 启动和停止你的系统

虽然你可以使用 `init` 命令启动和停止你的 BSD 系统，包括 `init 0`（关机）和 `init 6`（重启），但也有特定的停止 BSD 命令。`halt`、`reboot` 或 `shutdown` 等命令的优势在于它们允许你在关机发生之前让某些功能完成。例如：

```
# reboot
重启计算机
# halt -n
在关机前不运行 sync 同步硬盘
# halt -p
系统将关闭电源（如果可能）
# shutdown +10
在十分钟后关机并通知用户
# shutdown -r 06:08
在上午 06:08 重启
# shutdown +10 'Bye!'
在关机前向用户发送自定义消息
```

# 第 10 章：系统管理

用于查看有关内核如何启动的信息。此外，如果发生错误或你需要为内核添加某些额外支持，都有工具可以完成这些工作。

要确定你正在运行哪个版本的 BSD，请输入以下命令：

```
$ uname -r          显示当前发布版本的名称
6.3-RELEASE
$ uname -a          显示所有名称和发布信息
FreeBSD myhost.localdomain 6.3-RELEASE FreeBSD 6.3-RELEASE #0: Wed Aug 16 04:18:52 UTC 2008 root@desseller.c.buffalo:/usr/obj/usr/src/sys/GENERIC
1386
```

当内核启动时，关于发生情况的消息会被放置在系统消息缓冲区。你可以使用 `dmesg` 命令查找系统消息缓冲区的详情：

```
$ dmesg |less
Copyright (c) 1992-2008 The FreeBSD Project.
Copyright (c) 1979, 1980, 1983, 1986, 1988, 1989, 1991, 1992, 1993, 1994
The Regents of the University of California. All rights reserved.
FreeBSD is a registered trademark of the FreeBSD Foundation.
6.3-RELEASE #0: Wed Jan 16 04:18:52 UTC 2008
root@desseller.c.buffalo:/usr/obj/usr/src/sys
timecounter "18254" frequency 119312 Hz quality
CPU: Intel Pentium III Id = 0x683 Stepping = 3
Origin = "GenuineIntel* SSE"
>>
Features=0387f9ff-PFF,VME, DE, PSE, TSC, MSR, PAE, PGE, XEP, PTR, PTE, PCE, MCA, PAT,
P36, NX, PMX, MSR, SSE
real memory = 267142736 (254 MB)
avail memory = 251854848 (240 MB)
kbi at kdbdmux0
th_hal:0.920.3 (AR5210, AR5211, AR5212, RF5111, RF5112, RF2413, RF5413)
htpr: HTP RocketRadius kernel driver v1.1 (1 Jan 2008 04:16:19)
acpi0:CAMAN 8C1IAA0 on motherboard
acpi0:ACPI-fast* frequency 3579545 Hz quality 1000
acpi_timer0:<24-bit timer at 3579545MHz port 04x0-04xb0 on acpi0
...
```

如果缓冲区满了，它可能不再包含所记录信息的开头。在这种情况下，你可以使用 `less /var/log/dmesg`。

关于内核处理的其他信息可以在 `/var/log` 文件中找到，特别是 `messages` 文件。你可以按照以下方式查看这些文件：

```
# less /var/log/messages*
Aug 14 23:27:11 thompson syslog[557]: logfile first created
Aug 14 23:27:11 thompson syslog: kernel boot file is /boot/kernel/kernel
```

`Aug 14 23:27:11 thompson kernel: kbdl at kdbdmux0`

`Aug 14 23:27:11 thompson kernel: acpi0: <CAYAN 9C1A10A> on motherboard`

`Aug 14 23:27:11 thompson kernel: acpi0: Power Button (fixed)`

`Aug 14 23:27:11 thompson kernel: Timecounter <ACPI-fast frequency 357954 Hz quality 1000`

`Aug 14 23:27:11 thompson kernel: cpu0: <ACPI CPU> on acpi0`

`Aug 14 23:27:11 thompson kernel: pcib0: <ACPI Host-PICI bridge> port 0xcf8-0xcff acpi0`

`Aug 14 23:27:11 thompson kernel: fxp0: <Intel 82559 Pro/100 Ethernet> port 0xde80-0xdef6 mem 0xff8fd000-0xff8fdfff,0xff700000-0xffffff niq 1 device on 0.0 pci`

在理想情况下，连接到计算机的所有硬件都应该被检测并使用适当驱动程序进行配置。但在某些情况下，检测到了错误的驱动程序，或者系统中可能没有所需的驱动程序。对于这些情况，FreeBSD 提供了出可加载模块并向系统添加新模块的方法。

`kldstat` 命令允许查看已加载模块的名称、地址、大小和引用 ID。这是一个示例：

### kldstat

| ID | 引用 | 地址 | 名称 |
| :--- | :--- | :--- | :--- |
| 1 | 0xc040000 | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |

如果你想查找特定模块的详细信息，可以使用 `kldstat` 命令。这是一个示例：

| ID | 引用 | 地址 | 名称 |
| :--- | :--- | :--- | :--- |
| 1 | 0xc040000 | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
