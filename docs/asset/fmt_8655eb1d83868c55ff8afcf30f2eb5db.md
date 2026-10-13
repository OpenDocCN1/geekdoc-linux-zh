
![](img/a5afb9ccf4a412511e9fcfa4280141e3_354_0.png)

# 第三部分：在 Linux 中利用你的硬件

```
dr-xr-xr-x 3 nobody nobody      May 03 06:13 1791
dr-xr-xr-x 3 nobody nobody      May 03 06:13 1792
dr-xr-xr-x 3 root root        May 03 06:13 187
dr-xr-xr-x 3 root root      May 03 06:13 196
dr-xr-xr-x 3 root root      May 03 06:13 192
dr-xr-xr-x 3 root root      May 03 06:13 2000
dr-xr-xr-x 3 daemon root     May 03 06:13 207
dr-xr-xr-x 3 root root      May 03 06:13 218
dr-xr-xr-x 3 root root      May 03 06:13 22
dr-xr-xr-x 3 root root      May 03 06:13 230
dr-xr-xr-x 3 root root      May 03 06:13 241
dr-xr-xr-x 3 root root      May 03 06:13 252
dr-xr-xr-x 3 root root      May 03 06:13 267
dr-xr-xr-x 3 root nobody    May 03 06:13 279
dr-xr-xr-x 3 root root      May 03 06:13 290
dr-xr-xr-x 3 root postgres  May 03 06:13 316
dr-xr-xr-x 3 root root      May 03 06:13 332
dr-xr-xr-x 3 root root      May 03 06:13 341
dr-xr-xr-x 3 root root      May 03 06:13 382
dr-xr-xr-x 3 root root      May 03 06:13 383
dr-xr-xr-x 3 root root      May 03 06:13 384
dr-xr-xr-x 3 root root      May 03 06:13 385
dr-xr-xr-x 3 root root      May 03 06:13 386
dr-xr-xr-x 3 root root      May 03 06:13 387
dr-xr-xr-x 3 root root      May 03 06:13 389
dr-r--r-- 1 root root      May 03 06:13 cmdline
dr-r--r-- 1 root root      May 03 06:13 spuinfo
dr-r--r-- 1 root root      May 03 06:13 devices
dr-r--r-- 1 root root      May 03 06:13 dma
dr-r--r-- 1 root root      May 03 06:13 filesystems
dr-r--r-- 1 root root      May 03 06:13 interrupts
dr-r--r-- 1 root root      May 03 06:13 ioports
dr-r--r-- 1 root root      Apr 28 167
dr-r--r-- 1 root root      May 03 06:13 kmore
dr-r--r-- 1 root root      May 03 06:13 kysm
dr-r--r-- 1 root root      May 03 06:13 loadavg
dr-r--r-- 1 root root      May 03 06:13 locks
dr-r--r-- 1 root root      May 03 06:13 mdstat
dr-r--r-- 1 root root      May 03 06:13 meminfo
dr-r--r-- 1 root root      May 03 06:13 modules
dr-r--r-- 1 root root      May 03 06:13 mounts
dr-xr-xr-x 2 root root      May 03 06:13 net
dr-xr-xr-x 2 root root      May 04 06:13 pci
dr-xr-xr-x 3 root root      May 03 06:13 rtc
dr-xr-xr-x 3 root root      May 03 06:13 scsi
lrw-rw 1 root root      64 May 06:13 self
dr-r--r-- 1 root root      May 03 06:13 stat
dr-xr-xr-x 5 root root      May 03 06:13 sys
dr-xr-xr-x 5 root root      May 03 06:13 uptime
dr-xr-xr-x 5 root root      May 03 06:13 version
```

等待，我需要重新检查页面流。根据提供的文本进行重构。

## /proc/cpuinfo 文件

`/proc` 中的几个文件包含了关于你系统硬件的信息。例如，`/proc/cpuinfo` 文件列出了你系统的关键特性，例如处理器类型和浮点信息。

当我想要检查 `/proc/cpuinfo` 文件时，输入 `cat /proc/cpuinfo` 并得到以下输出：

```
cat /proc/cpuinfo
processor : 0
cpu        : 586
model      : Pentium 75
vendor_id : GenuineIntel
stepping  : 5
fdiv_bug : no
hlt_bug   : no
fpu       : yes
fpu_exception : yes
cuid      : yes
wp        : 
flags      : fpu vme tsc mce
bogomips : 30.00
```

此输出来自 Dell 公司的 P75 (75MHz Pentium) 系统。列表显示了处理器的许多有趣特性。注意以 `fdiv_bug` 开头的行。该 bug 是一个名为 `fdiv`（浮点除法）的指令。因此，`fdiv_bug` 行指示此特定的 Pentium 是否具有该 bug（幸运的是，我的系统没有）。

## CPU 命名规范

`CPU` 术语代表中央处理单元。在大型机和微机时代，CPU 是一个单元——就像柜子一样。对于 PC，CPU 是微处理器——486 或 Pentium 芯片。因此，包含处理器（CPU）信息的文件的名为 `cpuinfo`——这是一个由 `cpu` 和 `info` 拼接而成的名称。我解释这个想法是因为程序员通常会创建简短的名字。当你看到这些名称后，将更容易猜出它们的含义。

`/proc/cpuinfo` 文件的最后一行显示了关于 `Bogoips` 的信息，请参见第 1 章中的“什么是 Bogoips?”侧边栏。`Bogoips` 是 Linux 内核在启动时用于时间循环的数值。

## /proc/pci 文件

如果你有一个 PCI 系统（大多数新的 Pentium 系统都是），你可以检查 `/proc/pci` 文件以获取关于系统中 PCI 设备的信息。按照习惯，输入 `cat /proc/pci` 查看信息。以下是我在带有 PCI 主板的 Pentium 系统上发现的：

发现 PCI 设备：

```
Bus 0. device 13, function 0:
IDE interface: CMO 640 (buggy) (rev 2)
Medium devsel. IRQ 14
Bus 0. device 0:
VGA compatible controller: S3 Inc. Trio32/Trio64 (rev 0)
Medium devsel. IRQ 255.
nonprefetch 32 memory at 0xfe0000
Bus 0. device 1, function 0:
ISA bridge: VLSI B2C93-FCI (rev 1)
Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0. device 0, function 0:
Host bridge: VLSI B2C92-FCI (rev 1)
Medium devsel. Fast back-to-back capable. Master Capable. Latency=16.
```
