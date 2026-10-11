
# 第 8 章：学习系统管理

```
$ dmesg less

[ 000000 ] Linux version 3.1.0-fc16.i686

mockbuild@x86-11.phx2.fedoraproject.org.

(gcc version 4.6.2 20111107 (Red Hat 4.6.2-1) ))

# SMP Tue Nov 01 22:16:00 UTC 2011

[ 000000 ] DMI: Dell Precision Workstation 490

/D083, BIOS A08/20/2007

[000000] Kernel command line: initrd=0

root=cdrom:Linux-Fedora-i686-Live-Device.iso

rootfsype=auto live quiet quiet rh rd.lsuks=0

rd.md=rd.dm=0

[ 005694 ] CPU: Intel(R) Xeon(R) E5320 @ 1.86GHz stepping on

[ 027025 ] Brought up 4 CPUs

[ 032068 ] serial8250 driver, 4 ports, IRQ sharing enabled

[ 0341185 ] serial8250:ttyS0 at I/O 0xf8 (irq 4) is a 1650A

[ 0361880 ] serial8250:ttySI at I/O 0xf2 (irq 3) is a 1650A

[ 0354982 ] mousedev scsi 6:0:0: CD-ROM

TSTcorp DVD-ROM TS-H352C DEQ002: Q ANSI: 5

[ 3870128 ] input: ImPs/2 Generic Wheel Mouse

as /devices/platform/18042/seriol1/input/input3
```

[ 26.964764 ] e1000: Intel (R) PRO/1000 Network Driver - version 7.32.1-k8-NAPI

[ 26.964767 ] e1000: Copyright (c) 1999-2006 Intel Corporation.

[ 26.964813] e1000 0000:0c:02: PCI INT A -> GSI 18 (level, low) -> IRQ 18

[ 27.089103] parport_pc 00:08: reported by Play and Play ACPI

[ 27.089169] parport_pc: Style at 0x37 (0xf78), irq 7 (PCSPP,TRISTATE)

[24179.176319] scsi ctrl#1:0:0: Host-Controller

S3IB1102 Intel scsi 1100 PCI: 0 ANSI: 0 CCS

[24179.177466] sd 0:0:0: Attached scsi generic sg2 type 0

[24179.177584] sd 0:0:0: (sd)

8345512 512-byte logical blocks: (4.27 GB/3.97 GIB)

[24179.178593] scsi 0:0:0: (sd) Write Protect is off
```

从这些输出中，你可以看到 Linux 内核版本，接着是关于计算机的信息（Dell 工作站）以及内核命令行选项。接下来，你可以看到处理器类型（Intel Xeon）和 CPU 数量。之后，你缩小到了连接到计算机的硬件信息：串口、鼠标端口、以太网控制器 (`e1000`) 和并行端口。最后几行提到了插入计算机的 4 GB USB 驱动器。

如果在在检测硬件或加载驱动程序时出现问题，你可以参考这些信息来查看未正常工作硬件的名称和编号。然后你可以搜索 Linux 论坛或文档来解决问题。

一旦你的系统启动运行，还有其他命令可以查看关于计算机硬件的详细信息。`lspci` 命令列出了计算机上的 PCI 总线以及连接到总线上的设备。这里是一个片段：

```
$ lspci
00:00: Host bridge: Intel Corporation 5000 Chipset Memory Controller
00:02: PCI bridge: Intel Corporation 5000 Series Chipset PCI Express x4
00:1b: Audio controller: Intel Corporation 631ESB/632B High Definition Audio Controller (rev 09)
00:1d: USB controller: Intel Corporation 631ESB/632B/3100 UHCI Controller (rev 09)
07:00: VGA controller: Nvidia Quadro NV4 (285)
0c:02: Ethernet controller: Intel Corporation 8254 Gigabit Controller (rev 05)
```

主机将本地总线连接到 PCI 总线上的组件。输出显示了系统的不同设备具有各种功能：（音频设备）、闪存驱动和其他 USB 设备（USB 控制器）、显示器（VGA）以及有网卡（以太网控制器）。要从 `lspci` 获取更多详细信息，可以添加一个或多个 `-v` 选项。例如，使用 `lspci -vv`，你收到了关于你的以太网控制器的信息，包括延迟、控制器功能以及用于设备的 Linux 驱动 (`e1000`)。

如果你对 USB 设备感兴趣，请尝试 `lsusb` 命令。默认情况下，`lsusb` 列出计算机 USB Hub 以及连接到计算机端口的 USB 设备：

```
$ lsusb
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 4d13:5109 Dell Computer Corp. L100 Keyboard
Bus 002 Device 004: ID 4d13:3012 Dell Computer Corp. Optical Mouse
Bus 001 Device 005: ID 090c:0100 Silicon Mos, Inc. - Taiwan 64MB USB
```

从前面的输出中，你可以看到连接到计算机的键盘和 USB 闪存器的型号。通过 `lspci`，你可以添加 `-v` 选项查看更多细节。要查看处理器的详情，请使用 `lscpu` 命令。它提供了关于处理器的基本信息。

```
$ lscpu
x86_64
Architecture: 
CPU op(s): 32-bit, 64-bit
CPU(s): 4
CPU(s) list: 0
Thread(s) per core: 1
Core(s) per socket: 4
```
