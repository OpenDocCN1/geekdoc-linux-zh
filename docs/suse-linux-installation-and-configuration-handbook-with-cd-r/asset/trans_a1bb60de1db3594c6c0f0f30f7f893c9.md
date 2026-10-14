

kerneld   kerneld   kerneld
serial    serial    serial
pcmcia    p1a_hardware  p1a1_hardware
dummy     pcmcia    pcmcia
syslog    dummy     dummy
boot.setup dhclient  dhclient
random    l41       l41
svgatext  network   network
apmd      route     route
gpm       rpc       rpc
kbd       argus     argus
-         nfs       nfs
-         scanlogd  scanlogd
-         syslog    syslog
-         boot.setup boot.setup
-         nisplus   nisplus
-         routed    routed
-         named     named
-         quota     quota
-         quotad    quotad
-         random    random
-         yppasswdd yppasswdd
-         ypserv    ypserv
-         ypxfrd    ypxfrd
-         ypclient  ypclient
-         autofs    autofs

+   12. 你的文件可能看起来有点不同，但应该具有相同的格式。要将你的新服务添加到运行级别，只需在它下面写下其名称。例如，要将脚本添加到运行级别 3，请在标题为 Runlevel 3 的列下添加其名称。
+   13. 完成后，只需退出编辑器。rc.tab 将处理你的更改并相应地更新运行级别。

就这样。只要确保你的脚本包含所有正确的命令且没有多余的内容。如果需要帮助，你可以随时查看其他脚本的工作方式。你可以从阅读其他脚本中获得很多想法。

## 故障排除

*我向运行级别添加了一个新服务，但它不起作用。*

你确定它具有可执行权限吗？如果没有，运行 chmod +x script 命令来修复它。

## 声卡配置

## 本章内容

+   Linux 与声音：简史 202
+   SuSE Linux 提供的内容 202
+   软件需求 203
+   硬件设置 204
+   OSS/Lite 配置 210
+   OSS/Lite 故障排除 214
+   OSS 配置 215
+   OSS 故障排除 218
+   ALSA 配置 218
+   ALSA 故障排除 222
+   Enlightenment Sound Daemon (ESD) 222

## Linux 与声音：简史

正如我们所知，在 Linux 开发的早期阶段，大多数用户都是程序员。这些用户并不像内存管理和进程调度那样关心多媒体。因此，Linux 很长一段时间都存在而没有声音或声音应用程序的支持。直到一家专门从事 UNIX 多媒体实现的公司决定这个操作系统需要一些声音方面的帮助。该公司的名字是 4Front，项目是 Linux 的 Open Sound System。Open Sound System (OSS) 被认为是第一个在所有 UNIX 架构上统一 UNIX 声音系统标准的项目。

Linux 对 OSS 的支持对 Linux 和 OSS 来说都很重要。Linux 找到了一个存在已久、可靠且包含使用 OSS 的声音应用程序的标准声音系统。OSS 也因支持 Linux 而获得了很大好处。凭借大量 Linux 开发者和他们使用 OSS API 编写的众多应用程序，OSS 确保了其作为 UNIX 声音系统标准的存在，并将声卡支持扩展到了标准 PC 声卡。

OSS 有两个版本：

+   - 支持大量声卡的完整商业版
+   - 支持少量标准卡的 lite GPL 版

直到最近，一组 Linux 程序员才决定开始一个新的声音驱动项目：Advanced Linux Sound Architecture (ALSA)。该项目旨在建立一个新标准和完整的支持声卡列表，同时保持与 OSS 标准的向后兼容。这一举措将确保目前完全依赖 OSS 的现有声音程序能够运行，同时也提供了一个具有新 API 的新标准。

只有几个月前，制造商才开始意识到 Linux 已成为操作系统市场的一股力量，并开始为 Linux 编写驱动程序。4Front 提供了一个可完全运行的 OSS 版本试用期为七天；本章中将此称为 OSS demo。完整的注册版 OSS 将被称为 OSS，而随内核提供的 GPL 版将被称为 OSS/lite。

## SuSE Linux 提供的内容

SuSE Linux 是一个非常有帮助的发行版。如果你拥有完整版的 SuSE Linux，你也拥有完整的 OSS 版本（3.8.1）和 OSS 的演示版（最新版本在 4Front FTP 上）。这两个版本之间的区别在于商业版不包括对某些 ISA 声卡的支持。另一方面，演示版支持一些 PCI 卡。SuSE 假设你不会重新分发注册的 OSS 版本。你应该阅读位于 /usr/lib/oss 的许可协议文件。该软件包位于 series pay/oss。

许多声卡都由三个声卡驱动程序支持——OSS/lite、OSS（商业版）和 ALSA。在这种情况下，我们建议使用 ALSA 驱动程序。这是因为 ALSA 保持与 OSS API 的向后兼容性，从而使你能够运行需要 OSS 的应用程序，同时也能运行使用 ALSA 的应用程序。

## 软件需求

本章的软件需求在风格上是独特的。以下是声音运行所需的一般软件需求。如果你要使用 OSS/Lite、OSS 或 ALSA，你将必须使用以下列表中的软件以及你将要使用的驱动程序部分中指定的软件：

### 软件包需求：

### 系列 a：

+   - `isapnp`（用于即插即用卡）
+   - `pciutils`（用于即插即用卡的自动配置）

### 系列 snd：

> TIP 从这里列出的软件包中，你可以挑选你喜欢的。它们对于配置声卡并非必不可少，但我们推荐以下内容。

+   - `audiofil`
+   - `esound`
+   - `sox`
+   - `xmix`

### 系列 pay：

> TIP 只有当你计划使用 OSS 时才应仅选择以下其中一个。这些软件包不包含在 SuSE Linux 的快照版本中。

### 内核需求：

### 声音：

+   - 声音核心支持（作为模块）

## 硬件设置

这个过程相当漫长，所以请耐心。在此过程中，你将检查你的声卡是通过 DIP 开关/跳线配置还是通过 PnP 配置。大多数新声卡都是 PnP，因此，如果你有一块新声卡，它很可能是 PnP。Linux 对 PnP 设备的支持不由内核（2.2.x 系列）执行。这并不意味着你将无法使用你的声卡。得益于 isapnptools 软件包，你可以配置你的 PnP 设备并毫无问题地使用它们。

### 搜索适当的资源

在所有情况下，你都必须为声卡搜索适当的资源。在这部分，你将查找可用的 IRQ、DMA 和端口。要列出可用的资源，你应该使用 proc 文件系统中的 /proc/interrupts、/proc/dma 和 /proc/ioports 虚拟文件的信息。

发出以下命令以列出可用的空闲中断：

```
bash#cat /proc/interrupts
CPU0
0: 9780712      XT-PIC  timer
1: 61964        XT-PIC  keyboard
2: 0            XT-PIC  cascade
4: 710344       XT-PIC  serial
6: 562          XT-PIC  floppy
7: 0            XT-PIC  fdc
10: 9682        XT-PIC  eth0
13: 1           XT-PIC  fpu
14: 6119932      XT-PIC  ide0
15: 74241        XT-PIC  ide1
NMI:
```

正如命令输出所示，以下 IRQ 可用：3、5、7、10、11 和 12。你可以使用其中任何一个用于声卡。请注意 IRQ 9 和 IRQ 2 是相同的中断，不是声卡的合适 IRQ。你不应使用命令输出中列出的任何 IRQ；它们已经被占用。你应该首先尝试 5、7 和 10 中断。这并不意味着其他 IRQ 不能使用。但通常首选声卡使用这些中断。

> CAUTION

> 一些 IRQ 不应使用，因为它们属于主板资源。如果你使用其中任何一个，你将减慢 Linux 机的性能或使其死锁。这些中断是 1、6、8、13 和 14。IRQ 共享是好的，但不要与这些中断共享。

