
```
npx0:[FAST]
px0:<math processor> on motherboard
px0: INT 16 interface
cpu0 on motherboard
pci0:<Intel 82443BX (44 BX) host to PCI bridge pibus 0 on motherboard
prio0:<Interrupt Routing Table: 7 Entries> on motherboard
pci0:<PCI bus> on pci0
apg0:<Intel 82443BX (44 BX) host to PCI bridge mem 0xe0000000-0xe3ffffff
-at device 0.0 on pci0
pcib1:<PCI-PCI bridge> at device 1.0 on pci0
pci1:<PCI bus> on pci1
spir0:ROUTE_INTERRUPT failed.
pci1:<display, VGA> at device 0.0 (no driver attached)
isa b0:<PCI-ISA bridge> at device 7.0 on pci0
isa0:<ISA bus> on isa0
atapci0:<Intel PIX4 UDMA33 controller> port 0x1f0-0x1f7,0x3f6,0x170-0177,
-0x376,0xf00-0xf00 at device 7.1 on pci0
ata0:<ATA channel 0> on atci0
ata1:<ATA channel 1> on atci0
hci0:<Intel 82371AB/EB (PIIX4) USB controller> port 0xe000-0xe01f irq 10 at
-device 7.2 on pci0
h0:[GIANT-LOCKED]
```

![](img/77bd66253135c18493b7c99c3f112b77_124_0.png)

# 第 4 章 FreeBSD 的启动与关闭

```
usb0: <Intel 82371AB/EB (PIIX4) USB controller on uhci0
usb0: USB revision 1.0
hub0: Intel UHCI root hub, class 9/0, rev 1.00/1.00, addr 1
hub0: 2 ports with removable, self powered
pci0: <bridge> at device 7.3 (no driver attached)
fxp0: <Intel 82557 Pro/100 Ethernet> port oxe400-0xe41f mem oxe9200000-09200000,
-0xe9100000-0xe91fffff irq 9 at device 11.0 on pci0
miub0::MII bus on fxp0
inphy: <182555 10/100 media interface> on miub
inphy: 10base-T, 100base-FTX, 100baseTX, 100baseTX-FX
fxp0: Ethernet address: 00a0:c966:7b32
```

在这里，内核找到了鼠标并检测到它是 PS/2 类型的鼠标。它分配了设备 `psm0` 来指代这个鼠标供以后参考：

- `psm0`: <PS/2 Mouse> irq 12 at tkbcd0

`psm0`: [GIANT-LOCKED]

`psm0`: model Generic PS/2 mouse, device ID 0

`fdc`: <Enhanced floppy controller> at port 0x3f0-0x3f5,0x3f7 irq 6 drive 2 on isa

`fdc`: [FAST]

`fd0`: <1440-KB 3.5' drive> at `fdc0`

内核还找到了软盘控制器和软盘驱动器。`fdc` 是软盘控制器的设备名称，`fd0` 是软盘驱动器的设备名称（类似于 Windows/DOS 当你想访问该设备时的设备名称）。下一条消息显示内核发现了 SoundBlast AWE64 声卡，并提供了关于该卡正在使用的资源信息：

```
sb0: <Creative AWE6> at port 0x220-0x22f,0x330-0x331,0x388-0x38b-irq 5 drq 5 on isa
pcm1: <SB16 DSP> on sb0
```

在这种情况下，`sb0` 实际上是声卡相关设备组。声卡根据你想访问的功能使用多个设备，例如控制音频级别的 DSP 和 mixer。你可能还会看到以下行：

- unknown: <PNP003> can't assign resources (port)

- unknown: <Pc1> can't assign resources (memory)

- unknown: <Pa3> can't assign resources (port)

- unknown: <Pf13> can't assign resources (irq)

- unknown: <PNP051> can't assign resources (port)

- unknown: <PNP070> can't assign resources (port)

这些行表示内核在系统中发现了一些即插即用（通常缩写为 PNP）设备，但它对它们并不了解，且无法为其分配资源。这些是无害的。如果你没有看到它们，正如 FAQ 所说，“FreeBSD 项目将乐意接受驱动程序的贡献”。下一条消息显示内核发现了硬盘和 CD-ROM 驱动器；它提供了关于每个驱动器的各种信息，包括设备名称、制造商和型号、几何结构以及驱动器所在：

```
ad0: 19473MB<Maxtor 920409 [39566/16/63]> at ata0-master UDMA33
ad1: 14664MB<IBM-DNA35120 [29975/16/63]> at ata1-master UDMA33
acd0: CDROM <ATAPI 44X CDROM> at ata1-slave UDMA33
```

（这将在第 20 章“添加磁盘存储”中详细介绍）。

最后一条消息显示内核已挂载根文件系统：

Trying to mount root from ufs:/dev/ad0

系统的这一事实表示操作成功。根文件系统挂载后，内核将控制权交给一个名为 `init` 的进程。浅色的消息是由 init 阶段发生的事件触发的。你可以通过颜色区分内核消息和非内核消息。内核消息显示白色；非内核消息显示浅灰色。

## init

`init` 程序是操作系统下运行的第一个进程，其 ID 为 1。Init 负责启动构成完整操作系统的其余进程；为了实现这一点，它必须确定磁盘状态良好。当 FreeBSD 系统正常关闭时，它会在每个磁盘上运行名为 `sync` 的进程以确保所有数据写入，卸载文件系统，然后在文件系统上设置“clean”标志。这类似于 Windows 关闭时的过程。如果 FreeBSD 系统没有正常关闭，clean 标志就不会被设置。

## 文件系统一致性检查

`init` 执行的操作之一是检查 clean 标志是否已设置。如果没有设置，`init` 会挂载文件系统以供使用。它首先在文件系统上运行 `fsck` 程序以确保其没有损坏。该程序会修复它认为可以修复的任何损坏。`fsck` 类似于 Windows 中的 Scandisk 程序，这又类似于 Windows 在不正常关闭后重启时看到的“系统未正常关闭”程序。

![](img/77bd66253135c18493b7c99c3f112b77_126_0.png)

如果 `fsck` 在此时遇到无法修复的错误，它会将系统置于单用户模式（如果你正在读这本书，可能就是你），手动进行必要的修复。

假设 clean 标志已设置，并且在未设置时 `fsck` 能够修复损坏，`init` 继续挂载 `/etc/fstab` 文件列出的每个设置了 `mount at boot` 的文件系统（参见第 12 章“FreeBSD 启动”中的“理解 /etc/fstab 文件”）。

> 提示
如果需要，你也可以手动运行 `fsck`。

## 系统配置脚本

文件系统挂载后，`init` 读取位于 `/etc` 和 `/etc/defaults` 的系统配置脚本（称为运行控制或资源配置脚本，简称 rc 脚本）。此外，它还会检查 `/usr/local/etc/rc.d` 目录，查找启动时应运行的任何额外脚本（这些可能是 Web 服务器、数据库服务器或任何你想要自动运行的程序）。如果你熟悉 Windows 或 DOS，那么启动过程的一部分类似于控制 Windows 启动的 `config.sys`、`autexec.bat`、`ini` 以及 Windows 注册表部分。

> 注意
