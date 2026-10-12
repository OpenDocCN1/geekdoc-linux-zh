
B: `MSC=10`

B: `LED=7`

```
I: Bus=0011 Vendor=0002 Product=0005 Version=0000
Name="ImPS/2 Generic Wheel Mouse"
P: Phys=isa0060/serial/input0
H: Handlers=mousel event2
B: EV-7
B: KEY=70000 0 0 0
B: REL=103
```

### `/proc/cpuinfo`

此文件包含有关系统 CPU 类型和状态的信息。在我一次使用 64 位处理器的系统测试中，该文件提供了如下信息：

```
# /proc/cpuinfo
processor : 0
vendor_id : AuthenticAMD
cpu family : 15
model : 12
model name : AMD Athlon(tm) 64 Processor 3200+
stepping : 0
cpu MHz : 2202.833
cache size : 512 KB
fpu : yes
fpu_exception : yes
cpuid level : 1
wp : 
flags : fpu vme de pse tsc msr pae mce cex apic mtr
pge cmov pat pse36 clflush fxsr sse
mse2 pni pysync nx
```

```
mmxext 1m 3dnext 3dn
bogomips : 4235.7
TLB size : 1024 4 pages
clflush size : 64
cache_alignment : 64
address sizes : 40 bits physical, 48 bits virtual
power management : ts fid vld tpp
```

### `/proc/devices`

此文件提供了系统中所有可用设备的高级概览。Linux（以及 Unix）系统将设备分为两类：字符设备（作为输入字符流进行访问）和块设备（使用较大的数据单元即“块”以结构化方式访问）。字符设备类似于你的键盘、鼠标以及如 FireWire 和 USB 等数据线。块设备则是磁盘驱动器和其他包含文件系统的设备。我其中一个测试系统中的该文件部分如下：

```
# cat devices
Character devices:
1 mem
2 pty
3 tty
4 /dev/vc/0
4 tty
4 ttyS
5 /dev/tty
5 /dev/console
5 /dev/ptmx
6 lp
7 vcs
10 st
10 misc
13 input
14 sound
...
171 ieee1394
180 usb
188 ttyUSB

Block devices:
1 ramdisk
2 fd
7 loop
8 sd
9 md
11 sr
33 ide2
34 ide3
65 sd
```

### `/proc/meminfo`

此文件包含有关系统可用内存以及系统如何使用内存的信息。示例系统上的该文件内容如下：

```
# cat /proc/meminfo
MemTotal: 1023660 kB
MemFree: 9420 kB
```

Buffers: 39300 kB

Cached: 305648 kB

SwapCached: 243568 kB

Active: 710216 kB

Inactive: 168280 kB

HighTotal: 0 kB

HighFree: 0 kB

LowTotal: 1023660 kB

LowFree: 9420 kB

SwapTotal: 6297472 kB

SwapFree: 5327564 kB

Dirty: 3328 kB

Writeback: 0 kB

Mapped: 592672 kB

Slab: 62180 kB

CommitLimit: 680930 kB

Committed_AS: 2045916 kB

PageTables: 24704 kB

VmallocTotal: 34359783 kB

VmallocUsed: 16256 kB

VmallocChunk: 343597216 kB

HugePages_Total: 0

HugePages_Free: 0

Hugepagesize: 2048 kB

### `/proc/version`

此文件列出了你的系统运行的 Linux 内核版本。在我其中一个系统中，该文件包含以下内容（内容通常在一行，但为了便于阅读分成了多行）：

```
# cat /proc/version
Linux version 2.6.11.4-21.9-default (geeko@buildhost)
(gcc) 3.3.3 release #1 Fri Aug 19 11:58 UTC 2005)
```

### `/proc/pci`

此文件列出了系统启动时发现的所有 PCI 设备。我的一个系统的 `/proc/pci` 文件部分如下：

```
PCI devices found:
Bus 0, device 0, function 0:
Host bridge: Silicon Integrated Systems [SiS] 620 (rev 2).
Master Capable. Latency=32.
Non-prefetchable 32 bit memory at Oxe000000 [0ffff].
Bus 0, device 0, function 1:
IDE interface: Silicon Integrated Systems [SiS] 5513 [IDE] (rev 208).
Master Capable. Latency=22.I/O at 0xff0 [xffaf].
Bus 0, device 1, function 0:
ISA bridge: Silicon Integrated Systems [SIS] 85C503/5513 (rev 179).
Bus 0, device 1, function 1:
Class ff00: Silicon Integrated Systems [SIS] ACPI (rev 0).
Bus 0, device 2, function 0:
PCI bridge: Silicon Integrated Systems [SIS] 5591/5592 AGP (rev 0).
Master Capable. No bursts. Min Gnt=12.
Bus 0, device 9, function 0:
Ethernet controller: Intel Corporation 82557 [Ethernet Pro 100] (rev 8).
IRQ 3.
Master Capable. Latency=64, Min Gnt=8.Max=56.
nonprefetch 32 bit memory at 0xeffb00 [0xffff].
I/O at 0xde00 [0xd3f].
nonprefetch 32 bit memory at 0efe000 [0xffff].
Bus 0, device 11, function 0:
Ethernet controller: Davicom Semiconductor, Inc. Ethernet 100/100 Mbit (rev 1 6).
IRQ 10.
Master Capable. Latency=64, Min Gnt=20.Max=44.
I/O at 0xd00 [0xc7f].
nonprefetch 32 bit memory at 0xeffaf80 [0xffff].
Bus 0, device 15, function 0:
Multimedia audio controller: C-Media Electronics Inc MB738 (rev 16).
IRQ 12.
Master Capable. Latency=64, Min Gnt=2.Max=24.
I/O at 0xd800 [0x8ff].
```

文件的第一个条目显示获取信息的系统使用了 SIS 主板，并描述了连接 PCI 和 ISA 总线到系统主数据线的桥，识别主板具有内置 IDE 接口，并开始识别系统中特定的控制器（如以太网控制器、多媒体、视频、通信等），以确保你构建的内核可以使用 Linux 所需驱动。

### `/proc/cpuinfo` 补充

此文件描述计算机中中央处理器（CPU）的特征。我其中一个系统的内容如下：
