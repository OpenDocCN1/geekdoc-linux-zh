
## 9.2 系统性能

Fedora Core (2.6.16np)
`root (hd1,0)`
`kernel /vmlinuz-2.6.16np root=/dev/VolGroup00/LogVol00 rhgb quiet`
`initrd/initrd-2.6.16.np`

启用 APIC 可以提高中断延迟，这在实时应用中可能是一个问题。它提供的中断数量也比传统的 PIC 多得多。因此，启用 APIC 意味着卡不需要共享中断，我稍后会讨论这一点。

APIC 曾被指责导致驱动程序崩溃。如果你的 BIOS 启用了 APIC 而你想禁用它，可以使用 `nolapic` 选项。SMP 系统需要一个 I/O APIC，默认情况下，当你运行 SMP 内核时它会启用它，BIOS 也会启用。

### 9.2.3.4 设备与插槽

如果你在主板上安装了适配器，你应该注意以下几点。正如我早之前提到的，插槽通常决定了卡将使用哪种中断。如果你的卡与另一个设备共享中断，移动到不同的插槽可能会防止这种共享。共享可能不是问题，但对性能来说是最优的。

PCI 和 PCI-X 等并行总线必须在安装的卡之间分配可用的总线周期。慢卡和快卡并用会减慢两块卡。PCI-X 允许 66MHz 的卡和支持 133MHz 的卡位于同一个 PCI-X 总线上，但总线的运行速度仅取决于最慢的卡。同样，支持 133MHz PCI-X 卡的主板将根据安装的卡数调整时钟频率。主板可能提供两个支持 133MHz 的 PCI-X 插槽，但由于信号质量问题，如果你插满了两个插槽，你可能会降低时钟频率。这完全取决于主板的设计和 BIOS；每一个都是不一样的。

PCIe 的独特之处在于它使用点对点连接，消除了许多与并行总线相关的信号质量问题。PCIe 带宽以通道带宽表示（每通道 2.5GB/s）。插槽尺寸决定了安装卡可以拥有的最大通道数。因此，一个 x8 插槽可以支持多达 8 通道的卡（20 GB/s）。PCIe 规范允许制造商提供物理上比主板支持的宽宽插槽。例如，插槽物理上可能是 x8，但主板只提供四个通道。在这种情况下，卡仍然工作，但速度减半。

只需记住，并非所有插槽都是同等的。特定的配置对于每块主板都是唯一的，而对于高质量的主板，这些配置会为相关用户记录。阅读说明书总是是值得的。

### 9.2.3.5 处理插槽和设备的工具

确定插槽配置的一个非常有用的工具是 `lspci` 实用程序，它可以显示由多个设备共享的常用总线段。有时，你会发现某个特定插槽与焊接在主板上的设备共享一个公共总线段。在这种情况下，你可能在在不知情的情况下降低了自己的带宽。

通过选项，`lspci` 会列出 PCI 总线上的设备。每个 PCI 设备都有一个厂商 ID（`vendor ID`）和一个设备 ID（`device ID`）。厂商 ID 是一个识别制造商的 16 位数字。该 ID 由负责维护 PCI 规范的 PCI-SIG 分配。每个制造商为其出货的部件分配其自己的设备 ID，这些 ID 与厂商 ID 一起唯一地标识了设备。`lspci` 包含厂商和设备表，以便以人类可读的格式报告准确的设备信息。例如：

```
$ lspci

00:0.0 Host bridge: Intel Corporation E7501 Memory Controller Hub (rev 01)

Subsystem: Intel Corporation Unknown device 341a

  Flags: bus master, fast devsel, latency 0

  Capabilities: <access denied>

00:03.1 Class ff00: Intel Corporation E7500/E7501 Host Interface RASUM Controller (rev 01)

Subsystem: Intel Corporation Unknown device 341a

  Flags: fast devsel

00:0.3 PCI bridge: Intel Corporation E7500/E7501 Hub Interface C PCI-to-PCI

Bridge (rev 01) [Normal decode]

  Flags: bus master, 66MHz, fast devsel, latency 64

  Bus: primary=00, secondary=02, subordinate=04, sec-latency=0

  I/O behind bridge: 00002000-00005ff5

  Memory behind bridge: eff00000feafffff

  Prefetchable memory behind bridge: edda00000-edcffffff

00:03.1 Class ff00: Intel Corporation E7500/E7501 Hub Interface C RASUM

Controller (rev 01)

Subsystem: Intel Corporation Unknown device 341a

  Flags: fast devsel

..
```

- 5. www.pcisig.com

列表中的每个设备都包含一个标识该设备在总线上的逻辑位置的数字。上面列出的默认格式是：

```
bus : slot : function
```

PCI 是并行总线，这意味着卡必须共享一组公共信号。`bus` 字段标识总线号。PCI 允许使用多个总线。这里是 `lspci` 的输出：

```
bus : slot : function

00:00.0 00:03.1 00:00.3

00:02.0 00:03.1 00:03.1

00:04.0 00:07.0 00:07.1

00:06.0 00:09.0 00:09.1

00:08.0 00:0a.0 00:0a.1

00:0a.0 00:0d.0 00:0d.1

00:0c.0 00:0e.0 00:0e.1

00:0e.0 00:1f.0 00:1f.1
```

## 9.2 系统性能

设备: 错误: 可修正+ 非致命+ 致命+ 不支持
设备: RxdOrd-ExtTag-PhantFunc-Afxwr-NoSnoop-
设备: 最大负载 128 bytes, 最大读取请求 128 bytes
链接: 支持速度 2.5Gb/s, 宽度 x8, ASPM L0s, 端口 8
链接: 延迟 L0s 无限制, 输入无限
链接: ASPM 已禁用 RCB 64 bytes CommClk-ExtSync-
链接: 支持速度 2.5Gb/s, 宽度 x8

速度代表显卡的能力。实际速度是第二个高亮行，它代表显卡所在插槽的速度。

## 9.2.4 查找系统性能问题的工具

你有多种工具可用，用于追踪导致系统运行缓慢的进程。在之前的一个章节中，我使用了 `top` 命令并提供了一些详细示例。在本节中，我将向你展示其他可以帮助说明系统正在运行内容的工具。这些工具的大多数功能是重叠的。工具工具比另一个更有用取决于应用场景。

### 9.2.4.1 使用 vmstat 查看虚拟内存状态和噪声

我在之前的章节中使用 `vmstat` 来阐明系统如何使用磁盘缓存。这是一个已经存在已的熟悉工具。`vmstat` 的魅力之一在于它的简单性；你只需就能获得一行密集但实用的信息。输入 `vmstat` 可以获取从每个事件中打印的信息。

```
$ vmstat 1

procs --memory-- --swap-- --io-- --system-- --cpu

r swpd free buff cache si so bo in cs us id wa

1 1 3940 14740 147440 0 0 51 15 26 91 1 8 90

0 1 3764 15236 145516 0 0 2952 0 53 606 3 10 87

0 1 12368 13220 128084 0 0 1576 0 565 644 0 9 91

0 1 8216 17628 135116 0 0 2768 0 402 354 1 0 5 9

0 1 14452 17624 128484 0 0 3596 1020 438 397 1 5 94

0 1 11236 17796 129696 0 0 2196 0 588 695 2 9 89

0 0 8028 17824 130944 0 0 2220 0 556 610 2 7 91

0 0 4040 18524 132240 0 0 2180 0 532 601 5 6 87

0 1 4140 19744 137424 0 0 2964 0 491 506 1 5 94

0 1 4368 20024 131004 0 0 3488 932 481 488 1 6 93

0 1 9748 20212 124968 0 0 3840 0 502 535 1 8 91
```
