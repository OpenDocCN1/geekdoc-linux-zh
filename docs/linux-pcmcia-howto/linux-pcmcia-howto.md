
# Linux PCMCIA 入门指南

本文描述了如何在 Linux 下安装和使用 PCMCIA 卡片服务，并回答了一些常见问题。本文档的最新版本始终可以在 `http://pcmcia-cs.sourceforge.net` 找到。

## 1. 一般信息与硬件要求

### 1.1 引言

Card Services for Linux 是一个完整的 PCMCIA 或“PC 卡”支持包。它包含了一组可加载的内核模块，实现了一个版本的 Card Services 应用程序接口（API）、一组用于服务卡的客户端驱动程序，以及一个可以响应插入和移除事件、加载和卸载驱动程序的管理器守护进程（`daemon`）。它支持大多数卡类型的“热插拔”，因此可以随时安全地插入和拔出卡。

该软件尚处于开发阶段。它包含某些错误，应谨慎使用。我会尽力修复报告给我的问题，但如果你不告诉我，我可能永远无法得知。如果你使用了这些代码，我希望你能看到我的经验，无论好坏！

如果你对如何改进本文档有任何建议，请联系我（`dahinds@users.sourceforge.net`）。

未经我事先同意，本文档可以包含在商业发行版中。虽然不是强制要求的，但我希望获知此类使用。如果您打算将本文档纳入出版物，请联系我以确保您已拥有它。

### 1.3 最新版本是什么，在哪里可以获取？

Card Services 的当前版本是 3.2，可以在 `http://www.sourceforge.net/projects/linuxcardservices` 获取。本文档版本为 3.2，您可以在网上找到更多信息。Card Services 的当前版本是 3.2，且本文档“按现状”提供，风险自担。

### 1.4 支持哪些卡？

其他注册为与 Intel i2365s 兼容的控制器通常运行良好，由于笔记本电脑硬件技术变化速度快，新控制器频繁出现，当新型号上市市场与驱动程序可用之间可能会存在延迟。

PCMCIA 支持热插拔。以下已知控制器可以工作：

- `Cirrus Logic`（现为 `Basis`）`6210`, `6270`, `6272`
- `ENE Technology` `6211`, `6225`
- `Intel` `6729`, `6730`, `6812`, `6833`, `6836`, `6912`
- `Omega Micro` `6922`, `6933`
- `Ricoh` `5296`, `5396`
- `RC45`, `RC46`, `RLC47`, `RLC48`
- `SMC` `3490`
- `Texas Instruments` `1031`, `1130`, `1131`, `1210`, `1211`, `1220`, `1221`, `1225`, `1250A`, `1251A`, `1251B`, `1410`, `1410A`, `1420`, `1450`, `1451A`, `1510`, `1520`, `1620`, `4451`, `4451`, `4510`, `4520`, `7410`, `7510`, `7610`
- `Toshiba` `ToPIC95`, `ToPIC97`, `ToPIC100`（实验性，不完整）
- `Vadem` `465`, `468`, `469`
- `VLSI Technologies` `146`
- `VIA` `83C469`
- `Database` `8602`, `8602A`, `8604`, `8604A`, `8672`, `8602B`

现代笔记本电脑中使用的 `Motorola` `6AHC05GA` 控制器不支持。`HP Omnibook 600` 中的自定义主机控制器也不支持。

## 2. 编译与安装

卡是否能工作取决于网卡的类型。基本上所有的调制解调器都应该可以使用随附的驱动程序工作。某些网卡如果是受支持网卡的 OEM 版本，也可以正常工作。其他类型的 IO（帧缓冲区、声卡等）在有人编写相应的驱动程序之前将无法工作。

### 1.6 我最喜欢的（不支持的）卡何时能被支持？

遗憾的是，他们通常不会付钱让我写驱动程序，所以如果你想为你你最喜欢的卡获取一个驱动程序，你可能需要自己完成其中的至少一项工作。理想情况下，我希望建立类似于 Linux 内核的模式，由我负责“核心”驱动代码，而其他作者则贡献并维护针对特定卡的客户端驱动程序。这目前正在进行中。我会尽力提供帮助，但单人独立调试内核设备驱动程序的效率并不高。

### 1.7 邮件列表和其他信息源

Linux PCIA 信息页位于 `http://pcmia-cs.sourceforge.net`，其中包含错误跟踪、支持和功能请求，以及各种与 PCIA 相关的消息论坛。用户可以请求对特定问题的新回复进行通知，或对某个类别下的所有新消息进行通知。我希望这将成为一个非常有用的信息库，用于超出 HOWTO 范围的问题。

位于 `http://www.linux-on-laptops.com` 的 Linux 笔记本电脑页面链接了大量网站，这些网站提供了关于为 Linux 配置特定类型笔记本的信息。这里还有一个可查询的系统配置信息数据库，以及指向各种笔记本相关邮件列表的指针。

## 2. 编译与安装

### 2.1 前提条件和内核设置

在开始之前，你应该考虑一下是否真的需要自己编译 PCMCIA 软件包。所有的 Linux 发行版都带有预编译的驱动程序包。通常情况下，只有当你需要当前驱动程序的新功能，或者你更新和/或重新配置了内核且与 Linux 发行版自带的驱动不兼容时，才需要从头安装驱动程序。虽然编译软件包在技术上并不困难，但它需要一些通用的 Linux 知识。

在你开始之前，你的系统中已安装以下内容：

- 一个 2.0、2.2、2.4 或 2.6 内核源码树。
- （可选）“XForms” X11 用户界面。

你需要一个完整的内核 Linux 源码树，而不仅仅是一个过更新的内核镜像。驱动模块包含对内核源文件的引用。虽然你可能想构建一个新内核以移除不必要的驱动程序，但安装 PCMCIA 并不要求你这样做。

“stable”内核源码和补丁可以从 `ftp://ftp.kernel.org/pub/linux/kernel/v2.4` 获取。当前的模块工具可以在相同的位置找到。

在 Linux 源码树中，`Documentation/Changes` 文件描述了该内核发布版本所需的各种系统组件的版本。你可能需要检查此文件并验证你的系统是最新的，特别是如果你更新了内核。如果你正在使用开发版内核，请确保你使用的是正确的共享库和模块工具的组合。

在 x86 系统上，如果你正在使用 16 位的 PC 设备，对于较新的内核，还应该开启 `CONFIG_ISA`。这些卡的行为既像 ISA 设备，PCMCIA 驱动程序也会用来判断平台是否支持 ISA 中断。

在配置内核时，如果你正在使用 PCMCIA 以太网卡，你应该开启网络支持，但关闭 Linux 网卡驱动程序，包括“口袋和便携式适配器”。PCMCIA 网卡驱动程序都实现为可加载模块。编译进内核的驱动程序只会浪费空间。

如果你想使用 `SLIP`、`PPP` 或 `PLIP`，你需要在配置内核时启用它们，或者使用这些驱动程序的可加载模块版本。

为了使用 PCMCIA 令牌适配器（token adapter），你的内核应该配置启用 `TRB`。

如果你使用的是 PCMCIA IDE 适配器，你的内核应该配置启用 `BLK_DEV`。

如果你使用的是 PCMCIA SCSI 适配器，那么在配置内核时启用 `CONFIG_SCSI`。对于你预期使用的顶级驱动（`SCSI`、磁带、光驱），应禁用其他驱动程序。

该软件包包含一个基于 `XForms` 的状态工具 `cardinfo`。该工具作为独立包在大多数 Linux 发行版中提供。该库在大多数 Linux 发行版中提供。如果你想使用 `cardinfo`，你应该在配置 PCMCIA 软件包之前安装 `XForms` 库。此工具是完全可选的。

### 2.2 PCMCIA 支持

PCMCIA 驱动支持包含在 2.4 及之后的内核中。虽然它与独立的 PCMCIA 程序包共享大部分代码，但存在一些差异。内核 PCMCIA 支持也在演进。

内核 PCMCIA 的功能与 `pcmcia-cs` 程序包相同。它并不需要安装 `pcmcia-cs` 程序包，因为它需要一些用户工具（`cardsmgr`, `cardctl1`, `/etc/pcmia/*`）。

要使用 PCMCIA，配置内核时启用 `CONFIG_HOTPLUG`，并在 x86 系统上也应启用 `ISA`。内核 PCMCIA 支持也在演进。

内核 PCMCIA 的功能与 `pcmcia-cs` 程序包相同。它并不需要安装 `pcmcia-cs` 程序包，因为它需要一些用户工具（`cardsmgr`, `cardctl1`, `/etc/pcmia/*`）。

### 2.3 安装

以下是安装过程的概述：

- 在 `/usr/src` 中解压 `pcmia-cs-3.2.tar.gz`。
- 在 `pcmia-cs-3.2` 目录下运行 `make config`。
- 运行 `make all`，然后运行 `make install`。
- 根据需要自定义 `/etc/pcmia` 中的启动脚本和选项文件。

运行 `make config` 会提示一些配置选项，并检查你的系统以验证其是否满足 PC 的所有先决条件。在大多数情况下，你可以接受所有默认配置选项。务必仔细检查此命令的输出以防是否存在问题。



如果你计划安装未包含在核心 PCMCIA 发行版中的贡献驱动，请将每一个解压到 PCMCIA 源码树的根目录下。按照标准的构建说明操作。这些额外的驱动程序将自动编译并安装。

构建卡工具的“信任”版本

某些支持工具（`cardctl` 和 `cardinfo`）可以以“安全”或“信任”形式编译。“安全”形式防止非 root 用户修改卡配置。“信任”形式允许普通用户颁发命令来挂起和恢复卡、重置卡以及更改当前配置方案。默认构建安全形式。

# 2. 编译与安装

### 包含 32 位 (CardBus) 卡支持吗？

如果你希望使用 32 位 CardBus 卡，则必须选择此选项。如果你仅计划使用 16 位 PC 卡，则不需要 CardBus 桥接支持。

### 包含 PnP BIOS 资源检查吗？

这会将额外的代码构建到 PCMCIA 核心模块中，用于与系统的 BIOS 通信，以获取板载“主板”设备（串口和并行口、声卡等）的资源信息，从而帮助避免资源冲突。如果启用，将在 `/proc/bus/pcard` 处创建一些资源文件，并可以使用 `lmsp` 和 `setp` 池来管理 PnP BIOS 设备。然而，此设置在某些笔记本电脑上会导致问题，因此默认未开启。

### 模块安装目录？

新内核模块将安装的目录。通常，这应该是与你的内核版本匹配的 `/lib/modules` 的子目录。

### 如何设置内核特定选项？

有几个配置选项会影响 PCMCIA 系统。配置脚本可以从运行的内核中推导出这些选项（默认且最常见的情况）。或者，如果你是为了在另一台机器上安装而进行编译，可以从内核源码树读取配置，也可以设置每个选项。

`Configure` 脚本也可以以非活动模式执行，用于自动构建或在内核更新后快速重新配置。某些其他不常使用的选项只能从命令行设置。运行 `Configure --help` 会列出所有可用选项。

运行 `make install` 然后将构建并安装内核模块和程序。内核模块安装在 `/lib/modules/<version>/pcmcia` 下。`cardmgr` 和 `cardctl1` 程序安装在 `/sbin/pcmcia`。如果启用了 Cardbus，它将安装在 `/usr/bin/X11`。

配置文件将安装在 `/etc/pcmcia` 中。如果你在旧版本上安装，你的配置脚本将在替换之前进行备份。保存的脚本将赋予 `~.old` 后缀。

如果你不知道使用的是哪种控制器，请使用 `cardmgr/` 子目录下的 `pcmcia probe` 来确定。这里有几种主要类型：Databook TCIC-2 类型和 Intel I2365SL 兼容类型。在内核 PCMCIA 子系统中，Intel 控制器进一步细分为 ISA-总线 16 位总线和基于 PCI 的 CardBus 设备。

在某些情况下，`pcmcia_probe` 将无法自动确定你的控制器。如果你有一台 Halikan NBD 186 系统，它在未知位置具有一个 TCIC-2 控制器：你需要编辑 `rc.pcmcia` 来加载 `tcic` 模块，并将 `PCIC_OPTS` 参数设置为 `tcic_base=0x02c0`。

在使用 Cirrus 控制器的旧版非 PCI 系统上（包括 NEC Vers M），BIOS 在系统启动时会将控制器置挂起状态。此时 `pcmcia_probe` 将无法找到任何已知的主机控制器。如果发生这种情况，请编辑 `rc.pcmcia` 并将 `PCIC` 设置为 `i28365`，将 `PCIC_OPTS` 设置为 `wakeup=1`。

## 2.4 启动选项

PCMCIA 启动脚本通过环境变量识别一组启动选项。多个选项之间应用空格分隔并用引号括起来。启动选项的位置取决于所使用的 Linux 发行版。它们可能直接放置在启动脚本中，也可能保留在单独的选项文件中。具体细节请参见 2.6（关于特定 Linux 发行版的说明）。可以设置以下变量：

`PCMCIA`

此变量指定是否启动 PCMCIA 支持。如果设置为“yes”以外的任何值，则启动脚本将被禁用。

`PCIC:`

这用于标识 PC 卡接口控制器驱动程序模块。有几个选项：“tcic”、“i82365”以及（对于内核 PCMCIA 子系统）“yenta_socket”。几乎所有当前控制器在独立驱动程序中属于“i82365”组，在内核驱动程序中属于“yenta_socket”。这是唯一的强制性选项。

`PCIC_OPS:`

此指定用于 PCIC 模块的选项。某些主机控制器具有可选功能，这些功能在特定系统中可能实现也可能不实现。在某些情况下，驱动程序无法检测这些功能是否已实现。请查看相应的 man 页以获取可用选项的完整说明。

`CORE_OPS:`

此指定用于 `pcmcia_core` 模块的选项，该模块实现了核心 PC 卡驱动服务。更多信息请参见“man pcmcia_core”。

`CARDMGR_OPS:`

此指定要传递给 `cardmgr` 守护进程的选项。更多信息请参见“man cardmgr”。

`SCHEME:`

如果设置，则 PC 卡配置方案将在驱动程序启动时初始化为此方案。请参阅 4.2（PCMCIA 配置脚本概述）关于方案的讨论。

底层驱动程序 `tic` 和 `i82365` 具有各种定时参数，可能需要针对系统进行调整。定时问题包括识别问题、高负载下的死机、高错误率或性能不良。只有某些主机桥具有可调定时参数：请检查相应的 man 页查看控制器的可用选项。以下是总结：

- ISA-总线控制器具有许多定时参数。最重要的似乎是 `cmd_time` 标志，它决定了 PCMCIA 总线周期。486 系统（例如 DX-100）似乎从增加该值中受益。
- 对于 PCI-to-PCMCIA 桥，`fast_pci=1`。
- 对于 PCI-to-PCMCIA 桥，`i12365` 驱动需要参数 `p2cclk=1`。

# 2. 编译与安装

- PLX Technologies PCI9052（也作为 Linksys WDT11 销售）并非通用的 PCMCIA 读器；它是一个用于无线适配器的 PCI 接口卡，这使其看起来像是一个普通的 PCI 设备。本系统不支持此类设备。

## 2.5 系统资源设置

Card Services 理想情况下应避免锁定其他标准设备正在使用的 IO 端口和中断。它还会尝试检测与未知设备的冲突，但这种方法并不完全可靠。在某些情况下，你可能需要在 `/etc/pcmsia/config.opts` 中显式排除某个设备的资源。

以下是针对特定笔记本电脑类型的资源设置。查看此列表时请保持谨慎：它可能为解决问题提供有用提示，但不可避免地已经过时并包含错误。欢迎修正。

- 在 AMS SoundPro 上，排除 irq 10。
- 在某些 AMS TravelPro 5300 型上，使用内存 0xc8000-0xffcf。
- 在 BMX 486DX-66 上，排除 irq 5, irq 9。
- 在 Chicony NBS 上，使用内存 0xa000-0xdffff。
- 在 Compaq Presario 900 上，排除端口 0x3b0-03bb。
- 在 Compaq Presario 2010 上，排除端口 0x2f8-0x2ff, irq 3, irq 5。
- 在 Compaq Presario 2120EA 上，排除 irq 10。
- 在 Dell Inspiron 7000 上，排除 irq 3, irq 5。
- 在 Dell Inspiron 8000 上，排除端口 0x800-0x8ff。
- 在 Fujitsu C 系列上，排除端口 0x200-0x27f。
- 在 HP Omnibook 4000c 上，排除端口 0x300-0x30f。
- 在 HP Omnibook 4100 上，排除端口 0x220-0x22ff。
- 在 IBM ThinkPad 380 上，可能可能的 385 和 600 系列上，排除端口 0x230-0x233 以及 irq 5。
- 在带有内置调制解器的 IBM ThinkPad 600 和 770 型上，排除端口 0x2f8-0x2ff。
- 在 IBM ThinkPad 600E 和 770z 上，将高内存窗口排除到 0x60000000-0x6ffffff。
- 在 Micron Millennium Transport 上，排除 irq 5, irq 9。
- 在 NEC Versa M 上，排除 irq 9, 端口 0x2e0-02ff。
- 在 NEC Versa P / 75 上，排除 irq 5, irq 9。
- 在 NEC Versa S 上，排除 irq 9, irq 12。
- 在 NEC Versa 6000 系列上，排除端口 0x2f8-0x33ff, irq 9, irq 10。
- 在 NEC Versa SX 上，排除端口 0x300-0x31f。



- 在`ProStar 9200`、`Altima Virage`和`Aquiline Hurricane DX-400`上，排除`irq 5`，端口`0x330-0x35f`。可能某些内存`0xd8000-0xffff`。

- 在`Siemens Nixdorf SIMATIC PG 720C`上，使用内存`0xc0000-0xcfff`，端口`0x300-0x3bf`。

- 在`TI TravelMate 5000`上，使用内存`0xd4000-0xdfff`。

- 在`Toshiba 4030CDS`上，排除`irq 9`。

- 在`Toshiba T4900 CT`上，排除`irq 5`，端口`0x2e0-0x2e8`，端口`0x330-0x338`。

- 在`Toshiba Tecra 8000`上，排除`irq 3`、`irq 5`、`irq 9`。

- 在`Twinhead 5100`、`HP 4000`、`Sharp 8700`和`8900`上，排除`irq 9`（声音）、`irq 12`。

- 在`MPC 800`系列上，为`CD-ROM`排除`irq 5`，端口`0x300-0x30f`。

## 2.5.1 Powerbook 设置

对于基于`Powerbook`的系统，`/etc/pcmia/config.opts`文件中的默认资源完全不可用。将`IO`端口和窗口定义替换为如下内容：

```
include port 0x1000-0x7ff
include memory 0x80000-0xffffff
```

## 关于 Linux 发行版的说明

在某些情况下，你可能需要在`/etc/pcmia/config.opts`中显式地排除某个设备的资源。

- 在`AMS SoundPro`上，排除`irq 10`。

- 在某些`AMS TravelPro 5300`型上，使用内存`0xc8000-0xffcf`。

- 在`BMX 486DX-66`上，排除`irq 5`、`irq 9`。

- 在`Chicony NBS`上，使用内存`0xa000-0xdffff`。

- 在`Compaq Presario 900`上，排除端口`0x3b0-0x3bb`。

- 在`Compaq Presario 2010`上，排除端口`0x2f8-0x2ff`、`irq 3`、`irq 5`。

- 在`Compaq Presario 2120EA`上，排除`irq 10`。

- 在`Dell Inspiron 7000`上，排除`irq 3`、`irq 5`。

- 在`Dell Inspiron 8000`上，排除端口`0x800-0x8ff`。

- 在`Fujitsu C`系列上，排除端口`0x200-0x27f`。

- 在`HP Omnibook 4000c`上，排除端口`0x300-0x30f`。

- 在`HP Omnibook 4100`上，排除端口`0x220-0x22ff`。

- 在`IBM ThinkPad 380`上，可能`385`和`600`系列上，排除端口`0x230-0x233`以及`irq 5`。

- 在带有内置调制解器的`IBM ThinkPad 600`和`770`型上，排除端口`0x2f8-0x2ff`。

- 在`IBM ThinkPad 600E`和`770z`上，将高内存窗口排除到`0x60000000-0x6ffffff`。

- 在`Micron Millennium Transport`上，排除`irq 5`、`irq 9`。

- 在`NEC Versa M`上，排除`irq 9`、端口`0x2e0-0x2ff`。

- 在`NEC Versa P / 75`上，排除`irq 5`、`irq 9`。

- 在`NEC Versa S`上，排除`irq 9`、`irq 12`。

- 在`NEC Versa 6000`系列上，排除端口`0x2f8-0x33ff`、`irq 9`、`irq 10`。

- 在`NEC Versa SX`上，排除端口`0x300-0x31f`。

- 在`ProStar 9200`、`Altima Virage`和`Aquiline Hurricane DX-400`上，排除`irq 5`、端口`0x330-0x35f`。可能某些内存`0xd8000-0xffff`。

- 在`Siemens Nixdorf SIMATIC PG 720C`上，使用内存`0xc0000-0xcfff`、端口`0x300-0x3bf`。

- 在`TI TravelMate 5000`上，使用内存`0xd4000-0xdfff`。

- 在`Toshiba 4030CDS`上，排除`irq 9`。

- 在`Toshiba T4900 CT`上，排除`irq 5`、端口`0x2e0-0x2e8`、端口`0x330-0x338`。

- 在`Toshiba Tecra 8000`上，排除`irq 3`、`irq 5`、`irq 9`。

- 在`Twinhead 5100`、`HP 4000`、`Sharp 8700`和`8900`上，排除`irq 9`（声音）、`irq 12`。

- 在`MPC 800`系列上，为`CD-ROM`排除`irq 5`、端口`0x300-0x30f`。

### 2.6.1 Debian

对于基于`Powerbook`的系统，`/etc/pcmia/config.opts`文件中的默认资源完全不可用。将`IO`端口和窗口定义替换为如下内容：

```
include port 0x1000-0x7ff
include memory 0x80000-0xffffff
```

### 2.6.2 Red Hat

`Card Services`理想情况下应避免锁定其他标准设备正在使用的端口和中断。它还会尝试检测与未知设备的冲突，但这种方法并不完全可靠。在某些情况下，你可能需要在`/etc/pcmia/config.opts`中显式地排除某个设备的资源。

以下是针对特定笔记本电脑类型的资源设置。查看此列表时请保持谨慎：它可能为解决问题提供有用提示，但不可避免地已经过时并包含错误。欢迎修正。

`Debian`使用启动脚本安排。

### 2.6.3 Slackware

`Slackware`使用`BSD`启动安排。

### 2.6.4 SuSE

`SuSE`使用`System V init`脚本安排，脚本存储在`/etc/init.d`。

## 解决安装与配置问题

- 系统日志中`cardmgr`报告`"no pcmia driver in /proc/devices"`。

内核模块包含版本信息，在加载模块时会与当前内核进行检查。检查类型取决于`CONFIG_MODVERSIONS`内核选项的设置。如果该项为`false`，内核版本号会被编译到每个模块中，`insmod`会检查其与运行内核是否匹配。如果`CONFIG_MODVERSIONS`为`true`，内核导出的每个符号都会赋予一个校验和。这些代码将全部与每个模块中编译的相应代码进行比较。此意图是使模块依赖于版本：只有当接口发生变化时，校验和才会改变，并且通常在微版本内核更新中保持不变。在实践中，校验和的限制性较小，因为许多内核接口依赖于编译时的内核选项设置。事实证明，校验和是对兼容性一种过于悲观的判断。

实际的影响是，内核模块与内核版本以及许多内核配置选项的设置紧密绑定。通常，为一个`2.2.19`内核编译的一组模块不会加载到其他内核上，除非采取特殊措施来确保两者是用相似的配置构建的。这种预编译内核模块的分布使得问题变得很棘手。

你有几种选择：

- 如果你将预编译模块作为`Linux`发行版的一部分，请验证你使用的是该发行版提供的未修改的内核。如果你打算使用预编译模块，通常必须坚持使用相应的内核。

- 如果你重新配置或升级了内核，你可能需要从头编译并安装`PCMIA`包。如果你已经安装了内核源码树，这很容易完成。详细说明请参阅（编译与安装）。

- 在某些情况下，其他系统组件的不兼容性可能会阻止内核模块的正确加载。如果你升级了自己的内核，请注意内核源码树`Documentation/Changes`文件中列出的模块工具和`binutils`的“最低要求”。

### 3.2 部分客户端驱动模块未加载

症状：

- 基础模块（`pcmia_core`、`ds`、`182365`）加载正常。

- 插入卡片时发出高音 + 低音的组合蜂声。

- `cardmgr`在系统中报告版本不匹配错误。

某些驱动模块需要内核服务，这些服务取决于内核配置可能存在也可能不存在。例如，`SCSI`卡驱动程序要求内核编译时带有`SCSI`支持，而网络驱动程序需要支持网络的内核。如果内核缺少必要的功能，`insmod`可能会报告未定义符号并拒绝加载特定模块。注意，`insmod`的错误信息不区分版本不匹配错误和符号缺失错误。

具体来说：

- 串口客户端驱动`serial_cs`需要内核驱动通过`CONFIG_SERIAL`启用。该驱动可以作为模块构建。

- 支持多口串口卡或包含串口或调制调器设备的多功能卡需要启用`CONFIG_SERIAL_SHARE_IRQ`。



## 配置要求

- SCSI 客户端驱动程序需要启用 `CONFIG_SCSI` 以及适当的高级驱动选项（对于 2.2 及后续内核的 `CONFIG_BLK_DEV_SD`, `CONFIG_BLK_DEV_SR` 等）。这些可以作为模块构建。
- 网络客户端驱动程序需要启用 `CONFIG_INET`。内核网络支持可以编译为模块。
- 令牌环客户端要求内核编译时启用了 `CONFIG_TR`。

有两种处理方法：

- 启用必要的功能重新编译你的内核。
- 如果这些功能已编译为模块，请修改 `/etc/pcmia/config` 以预先加载它们。

`/etc/pcmia/config` 文件可以指定为特定客户端加载额外的模块。例如，对于串口驱动程序，应使用：

```
device "serial_cs"
class "serial" module "misc/serial", "serial_cs"
```

模块路径是相对于当前内核版本的顶层模块目录指定的；如果没有给出相对路径，则默认为 `pcmia` 子目录。

### 3.3 ISA 中断扫描失败

症状：

- 当加载 PCMIA 驱动时即使没有卡片，系统也会死机。
- 系统日志显示主机探测成功，但没有显示中断结果。

在识别主机后，驱动程序会对空闲的 ISA 中断进行扫描。扫描涉及为每个空闲中断设置一个“软”中断，以查看是否可以检测。在某些情况下，探测特定中断可能会干扰另一个设备。

探测的目的是识别那些看起来空闲（即未被任何 Linux 驱动程序占用）、物理上连接到主机，或连接到了没有驱动程序的设备。

在系统日志中，成功的探测可能如下：

```
Intel probe:
TI 1130 CardBus at mem 0x10211000...
ISA irqs (scanned) = 5,7,9,10 status on irq 10
```

有两种处理方法：

- 使用 `irq_list` 参数为驱动程序限制 ISA 中断列表。例如，`irq_list=5,9,10` 将扫描限制为三个中断。16 位设备将受到限制。
- 通过 `do_scan=0` 禁用探测。

在任何情况下，你可能需要指定，例如：

```
PCIC_OPTS=irq_list=5,9,10
```

默认窗口很大，因此可能有助于 `/etc/pcmia/config` 中的扫描。

### 3.4 IO 扫描失败

症状：

- 加载 PCMIA 驱动时即使没有卡片，系统也会死机。
- 系统日志显示主机探测成功，但没有显示中断结果。
- 基础模块（`pcmia_core`, `ds`, `182365`）加载正常。
- 插入卡片时发出高音 + 低音的组合蜂声。
- `cardmgr` 在系统中报告版本不匹配错误。

处理方法：

- 使用 `irq_list` 参数为驱动程序限制 ISA 中断列表。例如，`irq_list=5,9,10` 将扫描限制为三个中断。16 位设备将受到限制。
- 通过 `do_scan=0` 禁用探测。

### 3.5 内存探测失败

症状：

- 当没有卡片时，核心驱动加载正常，系统日志中没有错误。
- 一只要插入任何卡片，系统就会冻机并或重启。
- 所有卡片插入都会产生一个高音紧接着是一个低音。
- 所有卡片都被识别为“匿名卡片”。
- 系统日志报告某些内存范围已被排除。

### 3.6 无法检测到卡片的插入和拔出

症状：

- 卡片在启动时能被正确检测并配置。
- 驱动程序对插入和移除事件没有响应，既没有在系统日志中记录事件，也没有通过蜂鸣响应。

## 3. 解决安装和配置问题

在大多数情况下，插槽驱动程序（`i82365` 和 `tcic`）会自动探测并选择合适的中断来信号显卡状态的变化。自动中断探测在 Intel 兼容控制器上将无法工作，包括 Cirrus 芯片以及在某些 IBM ThinkPads 中使用的芯片。如果设备在探测期间处于非活动状态，其中断可能可能显示为可用。在这些情况下，插槽驱动程序可能会选取一个正被另一个设备使用的中断。

对于 `i82365` 和 `tcic`，可以使用 `irq_list` 选项来限制测试的中断。此列表限制了 PCMCIA 卡可以使用以及用于监控状态变化的中断集。`cs_irq` 选项也可以用于显式设置用于监控状态变化的中断。

如果你无法找到可用的中断，还有一种轮询模式：`i82365` 和 `tcic` 均接受 `poll_interval=100` 选项，每秒轮询一次卡状态。如果你的系统可用供 PCMCIA 使用的中断短缺，也应该使用此选项。特别是对于具有多个控制器的系统，专门分配中断用于监控卡状态变化的意义不大。

所有这些选项都应该在 `/etc/rc.d/pcmia` 或 `/etc/sysconfig/pcmia` 的 `PCIC_OPTS` 行中设置，取决于你的站点设置。

### 3.7 中断交付问题

症状：

- 卡显示配置成功，但无法工作。
- 串口卡和调制解器卡响应非常缓慢。
- 网卡可能报告“中断丢失 (interrupt(s) dropped)”或传输超时。

最简单的中断交付问题是由于与其他系统设备的冲突引起的。这些通常可以通过在 `/etc/pcmia/config.opts` 中排除故障中断来解决。测试时，逐个排除中断，直到问题解决或用完所有中断。如果没有中断可以工作，那么设备冲突可能不是问题所在。

对于 CardBus 桥器，可能会出现各种其他中断交付问题。欲详细讨论，请参见 5.2.3（PCI 中断交付问题）。

### 3.8 系统资源饥饿

症状：

- 当插入卡时，它被正确识别但无法配置（高/低蜂鸣声模式）。
- 系统日志中将出现以下消息之一：

```
RequestIO: Resource in use
RequestIRQ: Resource in use
RequestWindow: Resource in use
GetNextTuple: No more items
could not allocate mn IO ports for CardBus socket n
could not allocate nn memory for CardBus socket n
could not allocate interrupt for CardBus socket n
```

中断饥饿通常表明中断探测存在问题（参见 3.3 中断扫描失败）。在某些情况下，探测似乎有效，但只报告了一个或两个可用中断。检查你的系统日志以查看扫描是否合理。禁用探测并手动选择中断应该有所帮助。



如果中断探测工作不正常，插槽驱动程序可能会为插入操作分配中断，即使中断极其稀缺以至于这样做并不理想。你可以通过将`PCI_OPTS`设置为`"poll_interval=100"`将控制器切换到轮询模式。或者，如果你有一个`CardBus`控制器和旧版本的`PCMCIA`驱动程序，使用`"pci_cse=1"`选择一个`PCI`中断（如果可用）用于卡状态变化。

在某些情况下，内核配置错误也会导致表面的中断短缺。在 2.4 及更新后的内核中，如果没有启用`CONFIG_ISA`，那么`PCMCIA`总线中断是可用的。

IO 端口共享并不常见见，但有时发生在需要大对齐 IO 端口空间区域的卡上，或者可能只能识别少数特定的 IO 端口位置。`/etc/pcmia/config.opts`中的默认 IO 端口范围通常是足够的，但可以扩展。如果这是问题所在，可以在`config.opts`中使用`include 0x1000-0x1fff`行。在少数情况下，饥饿可能表示 IO 探测失败（参见 3.4 IO 端口失败）。

在`config.opts`的默认内存窗口中，内存饥饿也不常见见。`CardBus`卡可能比典型的 16 位卡需要更大的内存区域。由于`CardBus`内存窗口可以映射到主机的`PCI`地址空间的任何位置（而不仅仅是`PC`系统中 640K-1MB 的“空洞”），在高内存中指定大型内存窗口（例如`0xa0000000-0xa0fffff`）是有帮助的。

### 3.9 仅在插入两个卡时发生资源冲突

症状：

- 两张卡在单独使用时均工作正常。

- 当两张卡都插入时，只有一张工作。

这通常表示与`Linux`不知道的系统设备存在资源冲突。`PCMCIA`设备是动态配置的，例如，中断是按需分配的而不是而不是分配给特定的卡或插槽。给定一个可用资源列表，卡按照它们配置的顺序分配资源。在这种情况下，最后被分配到资源的卡的资源实际上并不是空闲的。

检查系统日志以查看未工作的卡使用了哪些资源。从`/etc/pcmia/config.opts`中排除这些资源，并重启`configmgr`守护进程以重新加载资源数据库。

### 3.10 设备配置未完成

症状：

- 当插入卡时，恰好听到一声高音蜂鸣声。

- 后续的卡插入可能会被忽略。

这表明卡已被识别，但`cardmgr`无法完成配置。最可能的原因是设置脚本阻塞了。要确定问题，你可以手动运行设置脚本以查看阻塞在何处。`cardmgr`守护进程还显示网络状态。例如，网络命令的输出可能如下：

```
poll_interval=100
```

# 4. 使用与功能

## 4.1 配置工具

当插入卡时，恰好听到一声高音蜂鸣声。后续的卡插入可能会被忽略。这表明卡已被识别，但`cardmgr`无法完成配置。最可能的原因是设置脚本阻塞了。要确定问题，你可以手动运行设置脚本以查看阻塞在何处。`cardmgr`守护进程还显示网络状态。例如，网络命令的输出可能如下：

```
poll_interval=100
```

| 模块 | 大小 | 使用者 |
| :--- | :--- | :--- |
| i82365 | 2 | |
| linksYS | 2 | |
| pcmia_core | 3 | |

### 4.1.1 卡状态守护进程

`cardmgr`守护进程负责监控`PCMCIA`插槽、加载驱动程序以及响应卡变化的运行脚本。它还显示系统日志中的状态。高蜂鸣表示成功，低蜂鸣表示卡未识别。更多信息请参见手册页。

### 4.1.2 stab 文件

`cardmgr`在`/var/lib/pcmia/stab`中记录每个插槽的设备信息。这是一个示例列表：

| 插槽 | 类 | 驱动程序 | 名称 | 主/次号 |
| :--- | :--- | :--- | :--- | :--- |
| 0 | scsi | Adapatec-1460 | sda | 8 |
| 0 | scsi | aha152 | scd0 | 11 |
| 1 | serial | ttyS1 | | |

对于描述设备的行，第一行是插槽，第二行是设备类，第三行是设备驱动程序，第四行是具有相同驱动程序的多个设备，第五行是设备名称，最后两个是设备的主次号（如果适用）。

`CardBus`卡的热插拔`PCI`驱动程序不由`cardmgr`管理；它们由热插拔内核管理。有关此信息请参见`http://linux-hotplug.sourceforge.net`。当`cardmgr`看到由`PCI`驱动的卡时，它将忽略该卡。插入或弹出卡时会报警，但在系统日志和`stab`文件中仅会被识别为“`CardBus`热插拔设备”。

### 4.1.3 cardctl 和 cardinfo 工具

`cardctl`命令可检查插槽状态或查看其如何配置。它也用于更改卡的配置状态。以下是`cardctl config`命令输出的示例：

```
Socket 0:
not configured
Socket 1:
Vcc = 5.0, Vpp1 = 0.0, Vpp2 = 0.0
Card type is memory and I/O
IRQ 3 is dynamic shared, level mode, enabled
Speaker output is enabled
Function 0:
Config register base = 0x0800
Option = 0x063, status = 0x008
I/O window 1: 0x0280 to 0x2bf, auto sized
I/O window 2: 0x02f8 to 0x2ff, 8 bit
```

或者使用`cardctl ident`获取识别信息：

```
Socket 0:
no product info available
Socket 1:
product info: "LINKSYS", "PCMLM336", "A", "0040052d6400"
manif: 0x0143, 0x0cab
function: 0 (multifunction)
```

# 4. 使用特性

`"cardctl suspend"`和`"cardctl resume"`命令用于在不加载驱动程序的情况下关闭卡设备。`"cardctl reset"`命令尝试重置并配置卡设备。`"cardctl insert"`和`"cardctl eject"`模拟物理插入或拔出卡片时执行的操作，包括加载或卸载驱动程序，以及配置或关闭设备。

如果你正在运行`X`，`cardinfo`工具除了`"cardctl config"`外，还提供了显示`PCMCIA`插槽当前状态的图形化显示。它还提供了一个监控`cardctl`功能的图形界面。

## 4.1. 插入和拔出卡片

理论上讲，你可以随时插入和移除`PCMCIA`卡。然而，不拔出当前正被应用程序使用的卡片是一个好习惯。比 1.1.77 旧的内核在串口串口/现代卡片时会死锁，但这个问题现在应该已经修复了。

某些类型的卡片无法安全地进行热拔出。具体而言，`ATA/IDE`和`SCSI`接口卡不是热插拔安全的。这不太可能实现，因为完整的解决方案需要对`Linux`内核驱动模型进行重大更改。此外，通常不建议热拔出任何类型的`CardBus`驱动程序。这正在针对各种卡类型（`IDE`, `SCSI`, `CardBus`）逐步改进，建议在物理拔出之前使用`"cardctl eject"`。

### 4.1.5 卡片服务与高级电源管理

如果你在配置内核时启用了`APM`支持，则可以在编译`Card Services`时带有`APM`（高级电源管理）。`APM`内核驱动由 Stephen Rothwell (`Stephen.Rothwell@ann.aug.org.au`) 维护。`apmd`守护进程由 Avery Pennurun (`apennarr@worldvisions.ca`) 维护，更多信息请参阅`http://www.worldvisions.ca/apennarr/apmd/`。如果在系统上检测到兼容版本，`PCMCIA`模块将自动配置`APM`。

无论是否配置了`APM`，你可以在笔记本电脑睡眠前使用`"cardctl suspend"`，并在恢复后使用`"cardctl resume"`，从而干净地关闭和恢复你的`PCMCIA`卡。这对于正在使用的调制调器无效，因为串口驱动程序无法保存和恢复现代操作参数。

`APM`在某些系统上似乎不稳定。如果你在系统上遇到`APM`和`PCMCIA`的问题，请尝试缩小范围，确定是哪一个包报告了错误。

某些驱动程序（`PCMCIA SCSI`驱动程序）无法从挂起/恢复周期恢复。使用`PCMCIA SCSI`卡时，请务必在系统睡眠之前使用`"cardctl eject"`。

### 4.1.6 关闭 PCMCIA 系统

要卸载整个`PCMCIA`包，请调用`rc.pcmcia`：

```
/etc/rc/rc.pcmcia stop
```

此脚本将运行几秒钟，为所有卡驱动程序留出优雅关闭的时间。如果设备当前正在使用，关闭将不完整，某些内核模块可能不会加载。



为了避免这种情况，请在调用 `rc.pcmcia` 之前使用 `"cardctl eject"` 关闭所有插槽。`cardctl` 命令的退出状态将指示是否有任何插槽已成功关闭。

## 4.2 PCMCIA 配置脚本概述

以下信息适用于由 `cardmgr` 管理的卡片。在 2.4 及更高内核中，内核 PCMCIA 子系统是激活的，此时 CardBus 由热插拔子系统管理，不再使用 PCMCIA 脚本。

每个 PCMCIA 设备都有一个关联的“类”（class），描述如何对其进行配置和管理。类与 `/etc/pcmcia/config` 中的驱动程序关联。目前有五种 IO 设备（网络、SCSI、光驱、固定磁盘和两个内存设备（内存和 FTL））。对于每个类，`etc/pcmcia/` 下有两个脚本（例如 `/etc/pcmcia/scsi` 用于 SCSI 设备）和一个选项脚本（例如 `/etc/pcmcia/scsi.opts`）。在设备插入时调用主脚本进行配置，在移除时关闭设备。对于具有多个关联设备的卡，将为每个设备调用脚本。

所有地址的第一部分是当前的 PCMCIA “方案”（scheme）。该参数用于根据用户指定的变量支持多组设备配置。一种用法是设置“家庭”方案和“工作”方案，它们包含不同的网络配置参数。使用 `"cardctl scheme"` 选择当前方案。如果没有指定方案，默认为 `"default"`。

除了 `ADDRESS` 之外，`*.opts` 文件中还可以使用几个附加变量：

`SOCKET, CLASS, DRIVER, DEVICE, MAJOR, MINOR`

这些对应于 stab 文件中的行中的字段。详情请参见相关页面。

`PROID_1, PROID_2, PROID_3, PROID_4, MANID, FUNCID`

这些等同于 `"cardctl info"` 的输出，并提供更详细的识别信息。

由于 `*.opts` 文件只是 shell 脚本，并不要求它们遵循基于 `ADDRESS` 返回设置的示例。

作为通用规则，为笔记本电脑配置 Linux 时，PCMCIA 设备应仅通过 PCMCIA 设备脚本进行配置。不要尝试以配置固定设备的方式配置 PCMCIA 设备。然而，某些发行版提供了集成到其自带设备配置工具中的 PCMCIA 包。在某些情况下，以下章节可能不适用。

## 4.3 使用与特性

PCMCIA 设备可以通过多种方法配置，最常见的方法是通过 `.opts` 文件。

PCMCIA 设备可以通过多种方法配置，最常见的方法是通过 `.opts` 文件。

PCMCIA 设备可以通过多种方法配置，最常见的方法是通过 `.opts` 文件。

PCMCIA 设备可以通过多种方法配置，最常见的方法是通过 `.opts` 文件。

### 4.3.1 网络设备

以下参数可以在 `network.opts` 中定义：

`IF_PORT`

- 为某些设备指定以以太网类型。更多信息请参阅“man ifport”。

`BOOTP`

- 布尔值（y/n）：指示是否应使用 BOOTP 协议获取主机 IP 地址和路由信息。

### 4. 使用与特性

```
DOMAIN="domain.org"
DNS_1="dns1.domain.org"
nesac
```

为了自动挂载和卸载 NFS 文件系统，首先将所有文件系统添加到 `/etc/fstab`，包含 `network.opts`，并在 `MOUNTS` 变量中列出文件系统的挂载点。当 NFS 挂载激活时，使用 `cardctl` 或 `cardinfo` 关闭网络尤为重要。在不弹出（eject）的情况下插入新网卡，是无法干净地卸载 NFS 文件系统的。

除了常规的网络配置参数外，`network.opts` 脚本还可以指定在接口配置后或接口关闭前采取的额外操作。如果 `network.opts` 定义了一个名为 `start_fn` 的 shell 函数，网络脚本将在接口配置后调用它，并将接口名称作为其第一个（也是唯一的）参数传递给该函数。如果定义了 `stop_fn`，则会在关闭之前调用它。

某些（大多数旧型号）卡的收发器类型必须使用 `IF_PORT` 设置手动选择。这可以是一个数值，也可以是识别收发器类型的关键字。所有网络驱动程序默认会尽可能自动检测接口，否则默认为 `10base`。可以使用 `ifport` 命令来检查或设置当前的收发器类型。例如：

```
# ifport eth0 10base2
#
ifport eth0
eth0 2 (10base2)
```

大多数现代 10/10baseT 卡使用“介质独立接口”（MII）收发器，该收发器可自动选择速度和双工设置。可以使用 `mii-tool` 命令监控和控制 MII 接口的行为。

### 4.3.2 关于特定网卡的注释

- 对于 IBM CCAE 和 Socket E 卡，在配置网络设备时需要设置收发器（`10base2`、`10baseT`、`AUI`）。确保系统日志中报告的收发器与你的连接相匹配。

- Farallon EtherWave 实际上基于 3Com 3c589，并带有特殊的收发器。尽管 EtherWave 使用 10baseT 风格的连接，但它要求将 3c589 配置为 10base 模式。

- 如果你在 IBM CCAE、NE4100、Thomas Conrad 或 Kingston 适配器上遇到问题，可以通过 `mem_speed=#` 增加 `pcnet_cs` 模块的内存访问速度。具体方法示例见标准的 `config.opts` 文件。尝试速度最高可 1000（纳秒）。

- 对于 New Media Ethernet 适配器，在某些系统中，可能需要在加载 `pcmcia_core` 模块时通过 `io_speed=#` 选项增加 IO 访问时间。编辑启动脚本中的 `CORE_OPTS` 来设置此选项。

- New Media Ethernet 驱动程序的多播支持是不完整的。最新的驱动程序可以在多播内核上运行，但会忽略多播包。混杂模式（Promiscuous mode）应该可以正常工作。

### 4. 使用特性

IBM 和 3Com 环形适配器使用的驱动程序在卡在通电前连接且未连接环路时，表现似乎非常糟糕。如果 `ifconfig` 报告硬件地址为全 0，可能是由于内存配置问题。

- 某些 Linksys、D-Link 和 IC-Card 10baseT/10base2 卡具有独特的收发器选择方式，由 Linux 驱动程序处理。一种变方法是启动 DOS 并使用供应商提供的工具选择收发器，然后启动 Linux。或者，执行此功能的实现可以在 <http://pcmia-source-sourceforge.net/ftp/extras/dlport.c> 中找到。

- 16 位 PCMC 卡的最大性能为 1.5-2 MB/sec。这意味着任何 16 位 bitbaseT 卡（即任何 16 位卡）性能受限。对于 New Media Ethernet 适配器，在加载 `pcmcia_core` 模块时，可能需要通过 `io_speed=#` 选项增加 IO 访问时间。...

- 对于 New Media Ethernet 适配器，在某些系统中，可能需要在加载 `pcmcia_core` 模块时通过 `io_speed=#` 选项增加 IO 访问时间。

- New Media Ethernet 驱动器的多播支持是不完整的。最新的驱动程序可以在多播内核上运行，但会忽略多播包。混杂模式应该可以正常工作。

### 4. 使用特性

- IBM 和 3Com 环形适配器使用的驱动程序在卡在通电前连接且未连接环路时，表现似乎非常糟糕。如果 `ifconfig` 报告硬件地址为全 0，可能是由于内存配置问题。

- 某些 Linksys、D-Link 和 IC-Card 10baseT/10base2 卡具有独特的收发器选择方式，由 Linux 驱动程序处理。一种变方法是启动 DOS 并使用供应商提供的工具选择收发器，然后启动 Linux。或者，执行此功能的实现可以在 <http://pcmia-source.sourceforge.net/ftp/extras/dlport.c> 中找到。

- 16 位 PCMC 卡的最大性能为 1.5-2 MB/sec。这意味着任何 16 位 bitbaseT 卡（即任何 16 位卡）性能受限。...

*(注：由于提供的待文本存在部分重复和截断，以上翻译已根据提供的逻辑片段进行了完整处理，并确保格式符合 Markdown 要求。)*

---

**注意：由于您提供的“需要翻译的文本”部分包含多处段落重复和部分不连续的描述，我将严格按照您提供的文本内容进行首次精准翻译：**

### 4. 使用与特性

```
DOMAIN="domain.org"
DNS_1="dns1.domain.org"
nesac
```



为了自动挂载和卸载 NFS 文件系统，首先将所有文件系统添加到 `/etc/fstab`，包含 `network.opts`，并在 `MOUNTS` 变量中列出文件系统的挂载点。当 NFS 挂载激活时，使用 `cardctl` 或 `cardinfo` 关闭网络尤为重要。在不弹出（eject）的情况下插入新网卡，是无法干净地卸载 NFS 文件系统的。

除了常规的网络配置参数外，`network.opts` 脚本还可以指定在接口配置后或接口关闭前采取的额外操作。如果 `network.opts` 定义了一个名为 `start_fn` 的 shell 函数，网络脚本将在接口配置后调用它，并将接口名称作为其第一个（也是唯一的）参数传递给该函数。如果定义了 `stop_fn`，则会在关闭之前调用它。

某些（大多数旧型号）卡的收发器类型必须使用 `IF_PORT` 设置手动选择。这可以是一个数值，也可以是识别收发器类型的关键字。所有网络驱动程序默认会尽可能自动检测接口，否则默认为 `10base`。可以使用 `ifport` 命令来检查或设置当前的收发器类型。例如：

```
# ifport eth0 10base2
#
ifport eth0
eth0 2 (10base2)
```

大多数现代 `10/10baseT` 卡使用“介质独立接口”（MII）收发器，该收发器可自动选择速度和双工设置。可以使用 `mii-tool` 命令监控和控制 MII 接口的行为。

### 4.3.2 关于特定网卡的注释

- 对于 IBM CCAE 和 Socket E 卡，在配置网络设备时需要设置收发器（`10base2`、`10baseT`、`AUI`）。确保系统日志中报告的收发器与你的连接相匹配。

- Farallon EtherWave 实际上基于 3Com `3c589`，并带有特殊的收发器。尽管 EtherWave 使用 `10baseT` 风格的连接，但它要求将 `3c589` 配置为 `10base` 模式。

- 如果你在 IBM CCAE、NE4100、Thomas Conrad 或 Kingston 适配器上遇到问题，可以通过 `mem_speed=#` 增加 `pcnet_cs` 模块的内存访问速度。具体方法示例见标准的 `config.opts` 文件。尝试速度最高可 `1000`（纳秒）。

- 对于 New Media Ethernet 适配器，在某些系统中，可能需要在加载 `pcmcia_core` 模块时通过 `io_speed=#` 选项增加 IO 访问时间。编辑启动脚本中的 `CORE_OPTS` 来设置此选项。

- New Media Ethernet 驱动程序的多播支持是不完整的。最新的驱动程序可以在多播内核上运行，但会忽略多播包。混杂模式应该可以正常工作。

### 4. 使用特性

- IBM 和 3Com 环形适配器使用的驱动程序在卡在通电前连接且未连接环路时，表现似乎非常糟糕。如果 `ifconfig` 报告硬件地址为全 0，可能是由于内存配置问题。

- 某些 Linksys、D-Link 和 IC-Card `10baseT/10base2` 卡具有独特的收发器选择方式，由 Linux 驱动程序处理。一种变方法是启动 DOS 并使用供应商提供的工具选择收发器，然后启动 Linux。或者，执行此功能的实现可以在 `<http://pcmia-source.sourceforge.net/ftp/extras/dlport.c>` 中找到。

- 16 位 PCMC 卡的最大性能为 `1.5-2 MB/sec`。这意味着任何 16 位 `bitbaseT` 卡（即任何 16 位卡）性能受限。... *(此处根据原文截断处理，已翻译至原文结束处)*

*(注：由于您提供的待翻译文本存在大量段落重复，以上内容仅针对您提供的原始文本块进行了翻译。)*

# 4. 使用与特性

## 4.4.1 串口设备参数

在 `serial.opts` 中可以定义以下参数。

### LINK

指定用于为“呼出”（callout）设备创建符号链接的路径（例如，对于 2.2 之前的内核使用 `/dev/cua*`，对于 2.2 内内核使用 `/dev/ttyS*`）。

### SERIAL_OPTS

指定传递给 `setserial` 命令的选项。

### INITTAB

如果指定，这将用于为该设备构建 `inittab` 条目。

### NO_CHECK, NO_FUSER

卡弹出策略的布尔（y/n）设置。如果 `NO_CHECK` 为真，即使设备正在忙，`cardctl eject` 也会关闭该设备。如果 `NO_FUSER` 为真，脚本将不会尝试杀死使用已弹出设备的进程。

例如：

```
case "$ADDRESS" in
*,*)
LINK="/dev/modem"
SERIAL_OPTS=""
INITTAB="sbin/getty
```

## 4.4.2 关于特定卡的注释

- Uniden Data 2000 无线 CDPD 卡具有一些特殊的拨号字符串用于启动 SLIP 和 PPP 模式。对于 SLIP，使用 `"ATDTD2"`；对于 PPP，使用 `"ATDTD0"`。

- Socket II 串口卡的 UART 具有高于标准的时钟。卡的实际波特率比串口驱动程序快四倍。为了解决这个问题，请在 `/etc/pcmia/serial.opts` 中指定 `SERIAL_OPTS="baud_base 460800"`。

## 4.4.3 诊断串口设备问题

- 在 3.1.5 及更高版本的 PCMCIA 中，PCMIA 源码树 `debug-tools` 子目录下的 `test_modem` 脚本将显示一些常见问题。

- 你的设备被识别为调制解调器了吗？检查系统日志并查找 `cardpcmia` 识别该卡并正确启动 `serial_cs` 驱动的消息。如果没有，你可能需要向 `/etc/pcmia/config` 文件添加新条目，以便能够正确识别。详情请见第 6.1（配置未识别的卡）节。

- `serial_cs` 是否成功配置了调制解调器？再次检查系统日志并查找来自 `serial_cs` 驱动的消息。如果 `register_serial()` 失败，你可能与其他设备存在 I/O 端口冲突。该卡的另一个提示是设备被报告为 `8250`；大多数现代调制解调器应被识别为 `16550` UART。如果你认为看到了端口冲突，请编辑 `/etc/pcmia/config.opts` 并排除分配给调制解调器的端口。

- 是否存在中断冲突？如果系统正常但调制解调器似乎无法工作，尝试使用 `setserial` 将 irq 改为 `0`，看调制解调器是否工作。这会导致串口驱动使用较慢模式而不是中断。如果系统看起来正常但调制解调器似乎无法工作，这通常是中断冲突的指示。你应该在 `/etc/pcmia/config` 中排除分配给调制解调器的中断。

- 调制解调器运行非常慢，这几乎是中断冲突的。

- 你的问题很可能是 SLIP 的，而不是 PCMIA 的。

 如果 如果你将串口驱动编译为模块，这意味着你的内核不支持串口设备。你必须修改 `/etc/pcmia/config` 以指示在加载串口模块之前加载串口模块。

## 4.5 PCMIA 并口设备

Linux 并口驱动是分层的，使得多个高层设备类型可以共享同一个端口驱动。打印设备通过 `/dev/lp*` 特殊设备访问。打印机的配置可以通过 `junto` 命令检查和修改。

`purport_cs` 模块依赖于 `purport` 和 `purport_re` 驱动，这些可以编译进内核。这种结构意味着任何高层并行设备（如 `plip` 驱动、打印机驱动等）必须编译为模块。这些驱动在启动时识别并行口设备，因此它们需要在配置 PC并行设备后加载。

传递给 `purport.opts` 的设备地址具有三个逗号分隔的字段：第一个是方案，第二个是插槽号，第三个是设备实例。对于支持并行口的卡，设备实例可能有多个值，但对于单端口卡，它总是 `0`。如果你经常使用多个卡，可能需要根据插槽位置指定设置：

```
case "ADDRESS" in
  ,*)
    # 插槽 0 的选项
    LINK=/dev/printer0
    ;;
  *1,*)
    # 插槽 1 的选项
    LINK=/dev/printer1
    ;;
esac
```

## 4.5.1 并口设备参数

在 `parport.opts` 中可以定义以下参数。

### LINK

指定用于为“呼出”设备创建符号链接的路径。

### SERIAL_OPTS

指定传递给 `setserial` 命令的选项。

### NO_CHECK, NO_FUSER

卡弹出策略的布尔（y/n）设置。如果 `NO_CHECK` 为真，`cardctl eject` 即使设备正在忙也会关闭该设备。如果 `NO_FUSER` 为真，脚本将不会尝试杀死使用已弹出设备的进程。

例如：

```
case "$ADDRESS" in
  *,*)
LINK="/dev/modem"
SERIAL_OPTS=""
```

## 4.5.2 诊断串口设备问题

## 4.6 PCMIA 适配器

# 4. 用法与特性



指定用于为此设备创建符号链接的路径。

- `DO_FSTAB`

  布尔值 (y/n) 设置：指定是否应为此设备在 `/etc/fstab` 中添加条目。

- `DO_FSCK`

  布尔值 (y/n) 设置：指定在挂载前是否应该检查文件系统，命令为 `fsck -Ta`。

- `DO_MOUNT`

  布尔值 (y/n) 设置：指定是否在插入卡片时自动挂载此设备。

- `FSTYPE`, `OPTIONS`, `MOUNTPT`

  用于 `fstab` 条目和/或挂载设备的文件系统类型、挂载选项和挂载点。

- `NO_CHECK`, `NO_FUSER`

  卡弹出策略的布尔值 (y/n) 设置。如果 `NO_CHECK` 为 `true`，当设备正忙时 `cardctl eject` 将关闭设备。如果 `NO_FUSER` 为 `true`，脚本将不会杀死使用已弹出设备的进程。

例如，这里是一个配置 SCSI ID 为 3 的磁盘设备（带有两个分区）以及 SCSI ID 为 6 的光驱的脚本：

```bash
case "$ADDRESS" in
*.sd,.*0,3,0)
  # 此设备有两个分区...
  PARTS="1 2"
  ;
  *.sd,.*0,0,1)
  # 分区 1 的选项：
  # 更新 /etc/fstab，并在 /usr1 上挂载 ext2 文件系统
  DO_FSTAB="y" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
  MOUNTPT="usr1"
  ;
*.sd,.*0,3,2)
  # 分区 2 的选项：
  # 更新 /etc/fstab，并在 /usr2 上挂载 MS-DOS 文件系统
  DO_FSTAB="y" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="mddos"
  OPTS=""
  MOUNTPT="usr2"
  ;
*.sr,.*0,6,0)
  # SCSI ID 6 光驱的选项
  PARTS=""
  DO_FSTAB="y" ; DO_FSCK="n" ; DO_MOUNT="y"
FSTYPE="iso9660"
OPTS="ro"
MOUNTPT="/cdrom"
::
esac
```

## 4.6.2 关于特定卡片的说明

- `Adaptec APA-1480` CardBus 卡需要一个较大的 IO 端口窗口（在 256 端口主体上对齐的 256 个连续端口）。可能需要扩展 `/etc/pcmcia/config.opts` 中的 IO 端口区域，以确保能找到如此大的窗口。

- 不支持 `Adaptec APA-460` SlimSSI 适配器。此卡最初以 `Tranter` 为名销售，当 `Adaptec` 与 `Tranter` 合并后，他们继续带有 `Adaptec` 标签销售 `Tranter` 卡。`APA-460` 与任何现有的 Linux 驱动都不兼容。

- 我收到过一个关于 `New Media Bus Toaster` 和 `UMAX Astra 1200` 扫描仪之间发生不良交互的报告。由于 SCSI 协议的复杂性，诊断 SCSI 设备的问题非常困难，值得考虑可能存在此类未记录的冲突组合。

## 4.6.3 诊断 SCSI 适配器问题

- 使用 `aha152x_cs` 驱动（`Adaptec`、`New Media` 及其他少数驱动使用），SCSI 断开/重置似乎是磁带驱动故障的频繁来源。要禁用此“功能”，请向 `/etc/pcmcia/config.opts` 中添加以下内容。

- 同样使用 `aha152x_cs` 驱动，某些设备似乎需要更长的启动延迟，通过 `reset_delay` 模块参数控制。`Yamaha 4416S CDR` 光驱就是其中一个设备。结果是设备识别成功，然后导致系统挂起。在这种情况下，请尝试调整该参数。

- 另一个 SCSI 设备探测的潜在源是针对多个 LUN 的探测。如果你看到设备检测成功，随后在探测该设备的 LUN 1 时出现 SCSI 超时，请禁用内核的 `CONFIG_SCSI_MULTI_LUN` 选项。

- 如果你将 SCSI 配置为模块（`CONFIG_SCSI="m"`），你可能需要修改 `/etc/pcmcia/config` 以将 SCSI 模块加载到相应的 scsi 驱动中。

- 如果在探测 SCSI 总线时因“timeout”消息导致中止命令，你几乎肯定存在中断冲突。

- 如果主机驱动程序报告“no SCSI devices”，请验证你的内核在编译时是否包含了适用于你设备的适当顶层驱动（即磁盘、磁带、光驱和通用驱动）。如果缺少顶层驱动，该类型的设备将被忽略。

## 4.7 PCMCIA 内存卡

`memory_cs` 驱动处理所有类型的内存卡，并为具有其他功能的卡片提供对 PCMCIA 内存空间的直接访问。加载时，它会创建一个字符设备和块设备的组合。请参阅主页获取设备命名方案的完整描述。块设备用于类似磁盘的访问（创建和挂载文件系统等）。字符设备用于对任意位置进行“原始”无缓冲读取。传递给内存的设备地址由两个字段组成：方案和插槽号。某些闪存卡和大多数 RAM 卡会加载“卡片信息”（`CIS`）。通常情况下，`cardmgr` 会假设任何带有 `CIS` 的卡都是简单模块并加载 `memory_cs` 驱动。因此，通用卡识别问题的常见副作用是，其他类型的卡可能被误识别为内存卡。在启动时，PCMCIA 使用第一个检测到的设备来确定哪些内存区域是使用的。`memory_cs` 驱动使用启发式方法猜测卡片的容量。这种启发式方法对于已写入的卡片无效，在其他情况下也可能出错。如果你计划经常使用内存卡，最好将 `/etc/pcmcia/config.opts` 中的窗口限制为已知的良好区域。如果卡片被误识别，则应使用 `dd` 或 `mkfs` 等命令显式指定其大小。`memory_cs` 模块还有一个用于覆盖大小检测的参数。

### 4.7.1 内存设备参数

可以在 `memory.opts` 中指定以下参数：

- `DO_FSTAB`：布尔值 (y/n) 设置：指定是否应为此设备在 `/etc/fstab` 中添加条目。

- `DO_FSCK`：布尔值 (y/n) 设置：指定在挂载前是否应该检查文件系统，命令为 `fsck -Ta`。

- `DO_MOUNT`：布尔值 (y/n) 设置：指定是否在插入卡片时自动挂载此设备。

- `FSTYPE`, `OPTIONS`, `MOUNTPT`：用于 `fstab` 条目和/或挂载设备的文件系统类型、挂载选项和挂载点。

- `NO_CHECK`, `NO_FUSER`：卡弹出策略的布尔值 (y/n) 设置。如果 `NO_CHECK` 为 `true`，当设备正忙时 `cardctl eject` 将关闭设备。如果 `NO_FUSER` 为 `true`，脚本将不会杀死使用已弹出设备的进程。

以下是一个根据插入插槽自动挂载内存的脚本示例：

```bash
case "$ADDRESS" in
*0,0)
  # 不在 /etc/fstab 中进行更新
  DO_FSTAB="n" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
  MOUNTPT="mem"
  ;;
*1,0)
  # 不在 /etc/fstab 中进行更新
  DO_FSTAB="n" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
  MOUNTPT="mem1"
esac
```

## 4.7.2 使用闪存卡

以下信息仅适用于所谓的“线性闪存”内存卡。许多闪存卡（包括 `SmartMedia` 和 `CompactFlash`）实际上包含了模拟 IDE 设备的电路。这些卡片被作为 IDE 设备处理，而不是内存卡。

闪存卡有两种主要格式：FTL（闪存转换层）风格和微软闪文件系统（FFS）。FTL 通常更灵活，因为它允许在闪存卡上像使用普通磁盘设备一样使用任何高级文件系统（`ext2`, `ms-dos` 等）。FFS 是一种完全不同的文件系统。Linux 原生无法处理格式化为 FFS 的卡片。要将内存卡作为普通磁盘设备使用，首先使用 `ftl_format` 命令在设备上创建 FTL。此层隐藏了闪存内存编程的设备细节，并使卡片看起来像简单的块设备。例如：

```bash
ftl_format -i /dev/mem0c0
```

注意，这是通过“原始”内存接口访问卡片。格式化后，可以通过 `ftl_cs` 驱动作为普通块设备访问。例如：

```bash
make2fs /dev/ftl0c0
mount -t ext2 /dev/ftl0c0 /mnt
```



FTL 设备的命名非常复杂。设备由三部分组成：卡号、该卡上的区域号，以及可选的区域内分区。一个区域可以被视为没有分区表的单个块设备（类似于软盘），也可以像硬盘设备一样进行分区。`ftl0c0` 设备是卡 `0`、通用内存区域 `0` 的整个区域。`ftl0c0p1` 到 `ftl0c0p4` 设备是如果区域已分区，主分区 `1` 到 `4`。

FTL 分区的配置选项可以在 `ftl.opts` 中给出，其结构与 `memory.opts` 相似。传递给 `ftl.opts` 的设备地址由三个或四个字段组成：方案，

# 4. 使用特性

插槽号（socket number）、区域号，以及可选的分区号。大多数闪卡只有一个内存区域，因此区域号通常为 `0`。

Intel 第 100 系列闪卡使用第一个 `128K` 闪存块来存储卡片的配置信息。为了防止这些信息被意外擦除，`ftl_format` 会自动检测此内容并在创建 FTL 分区时跳过该块。

## 4.8 PCMCIA ATA/IDE 卡驱动器

ATA/IDE 支持基于内核 IDE 驱动。这包括 SmartMedia 和 Compact-Flash 设备；这些内存卡的设置使其能够模拟 IDE 接口。驱动器中 PCMCIA 特有的部分是 `ide_cs`。在拔出卡片之前，务必使用 `cardctl` 或 `cardinfo` 关闭 ATA/IDE 卡片，因为该驱动器从未支持过“热插拔”。

传递给 `ide.opts` 的设备地址由三个或四个字段组成：当前方案、插槽号、设备序列号以及可选的分区号。可以使用 `ide_info` 命令获取 IDE 设备自身的编号。对于 SCSI 设备，`ide.opts` 在 `PARTS` 变量中返回分区列表，然后将为每个分区调用脚本。

## 4.8.1 ATA/IDE 固定式磁盘设备参数

可以在 `ide.opts:` 中指定以下参数：

- `DO_FSTAB`

  布尔值 (y/n) 设置：指定是否应为该设备在 `/etc/fstab` 中添加条目。

- `DO_FSCK`

  布尔值 (y/n) 设置：指定在挂载之前是否应该检查文件系统，命令为 `fsck -Ta`。

- `DO_MOUNT`

  布尔值 (y/n) 设置：指定在插入卡片时是否应自动挂载该设备。

- `FTYPE`, `TYPES`, `MOUNTOPT`

  用于 fstab 条目和挂载设备的文件系统类型、挂载选项和挂载点。

- `NO_CHECK`, `NO_USER`

  卡片拔出策略的布尔值 (y/n) 设置。如果 `NO_CHECK` 为 `true`，当设备忙时，`cardctl eject` 将关闭设备。如果 `NO_USER` 为 `true`，脚本将不会尝试杀死使用已拔出设备的进程。这里是一个 `ide.opts` 文件示例，将任何 ATA/IDE 卡的第一个分区挂载到 `/mnt`：

```
case "$ADDRESS" in
  *,.*1)
    DO_FSTAB="y" DO_FSCK="y" DO_MOUNT="y"
    FTYPE="msdos" OPTS="" MOUNT="mnt" ;;
  *,*)
    PARTS="1" ;;
esac
```

## 4.8.2 诊断 ATA/IDE 适配器问题

- IO 故障可能导致 IDE 驱动程序误判驱动器几何结构并报告“INVALID GEOMETRY: 0”。要修复此问题，尝试在 `/etc/pcmia/config.opts` 中排除选定的端口范围。

- 部分 IDE 驱动器违反了 PCMIA 规范，需要更多的时间来启动。这可能导致“timed out during reset”消息。调整 `pcimia_core` 的 `unset_delay` 和 `unset_limit` 参数以为驱动器留出更多启动时间；详情请参阅 `pcimia_core` 主页。

- 要使用 ATA/IDE CD-ROM 设备，你的内核在编译时必须启用 `CONFIG_BLK_IDE`。对于标准内核这通常是开启，但如果你编译了自定义内核，请注意这一点。

- 尝试挂载错误文件时的常见错误。通常情况下，你想挂载驱动器的分区，而不是整个设备（即 `/dev/ide1`, `/dev/ide2`）。

- 如果在插入时没有介质，Linux IDE 驱动程序可能会出现有问题的移除式介质驱动器。IBM Portable 就存在这个问题。

- 某些内核会在插入时报告“drive not ready”错误。这些错误可以被忽略；当可移动式 IDE 设备不接受命令时，它们会弹出。

```
CORE_OPTS="unset_delay=40"
```

## 4.9 多功能卡

单个中断可以被多个驱动程序共享，例如串行驱动程序和以太网驱动程序：事实上，PCMIA 规范要求所有卡片功能共享同一个中断。通常情况下，所有卡片功能都可以在无需共享驱动程序的情况下可用。

同时使用两个卡片功能是“棘手”的，不同的硬件供应商以各自不兼容的（有时是私有的）方式实现了中断共享。某些卡的驱动程序（Ositech Jack of、3Com 3c62 及相关卡、Linksys 卡）能够正确支持并发访问，但其他（旧卡）则不支持。如果你在激活两个功能的情况下使用卡片遇到困难，请尝试隔离地使用每个功能。这可能需要显式执行 `ifconfig down` 来关闭同一张卡片上的网络接口和调制解器。

# 5 高级主题

## 5.1 PCMCIA 设备的资源分配

理论上讲，将哪个中断分配给设备并不重要，只要没有两个设备被配置为使用同一个中断。在 `/etc/pcmia/config.opts` 中，你会找到一个用于排除非 PCMCIA 设备所用中断的地方。

同样，没有办法直接指定卡片使用的 I/O 地址充分`etc/pcmia/config.opts` 文件允许你指定适用于任何卡片的可用端口范围，或者排除与其他设备冲突的范围。

在修改 `/etc/pcmia/config.opts` 后，可以使用 `kill -HUP` 重启 `cardmgr`。用于监控卡片状态的中断由底层 socket 驱动模块（`i82365` 或 `tcicb`）选择；`cardmgr` 解析 `/etc/pcmia/config`，因此它不受该文件更改的影响。要设置此中断，当 socket 驱动程序是 `/etc/rc.d/rc` 中的 `PCIC_OPTS` 变量时，使用 `cs_irq_opts`。

所有客户端都有一个名为 `irq_list` 的参数，用于指定它们可能分配的中断。这些驱动选项应设置在你的 `/etc/pcmia/config` 中：

```
device "serial_cs"
module "serial_cs" opts "irq_list,8,12"
```

将指定驱动程序仅使用 irq 8 或 irq 12。无论 `irq_list` 如何设置，Card Services 都不会分配已被另一个设备占用的中断，或者文件中排除的中断。

## 5.2 PCI 中断配置问题与解决方案

大部分讨论适用于 `2.2` 及更早的内核。对于 `2.4` 及更新的内核，PCI 子系统负责大部分中断管理。以下提示可能有助于诊断问题，尽管此处描述的某些工作负载可能无效。

### 5.2.1 PCI 中断路由概述

每个插槽都有四个 PCI 中断引脚（`INTA` 到 `INTD`）。单功能将仅使用 `INTA`。PCI 子系统负责大部分中断管理。以下提示可能有助于诊断问题，尽管此处描述的某些工作负载可能无效。

# 5. 高级主题

即使你不知道路由器是如何工作的，也要了解 PCI 中断是按某种方式设置的。

如果你遇到了你认为可能与 PCI 中断配置有关的问题，应该首先验证你是否拥有一个足够较的 PCMCIA 驱动程序包。仔细查看 PCMCIA 内核模块加载时的启动信息。你应该能看到类似的内容：

```
Linux PCMCIA Card Services 3.1.18
kernel build: [2.2.14-5] #1 May 9 10:44:42 PDT 2000
options: [pci] [cardbus] [apm] [pnp]
pci routing table version 1.0 at 0xfdf30
Intel PCI probe
TI 1126 rev 02 PCI-CardBus at slot 00:07, mem 0x20000000
host opts: [ring] [serial peri & irq] [pci irq 11] ...
host opts: [ring] [serial peri & irq] [pci irq 11] ...
ISA irqs (scanned) = 3,4 PCI status changes
```

“routing table”（路由表）消息表示找到了有效的路由表。“host opts”（主机选项）行指示了中断交付模式，以及是否能为每个插槽确定 PCI 中断。最后几行显示了可用中断的扫描结果。

## 5.2.2 PCI BIOS 未检测到 CardBus 桥器

症状：

- `Intel PCI probe`：未找到。

- 桥器未在 `lpci` 或 `/proc/pci` 中显示。



`Lucent/SCM` PCI 转 `CardBus` 适配器似乎在某些其他系统上让 PCI BIOS 产生了困惑。`Lucent` 表示，这仅支持符合 PCI 2.2 规范或 `PC99` 标准的系统。某些系统完全无法检测到 `Lucent` 卡，如果系统没有检测到它，Linux 驱动程序就无法使用它。唯一的可能解决方法是升级 BIOS，或者使用不同的主板或 `CardBus` 适配器。

### 5.2.3 PCI 中断交付问题

**症状：**

- 卡片配置正确，但无法工作。
- `/proc/interrupts` 显示 `PCMCIA` 驱动程序的中断计数为 0。

`CardBus` 桥器通常支持两种类型的中断：`PCI` 和 `ISA`。部分由于历史原因，习惯上是使用 `PCI` 中断来信号卡插入和拔出事件以及 `CardBus` 中断；而将 `ISA` 中断用于 16 位卡。从 3.1.9 版本开始，这是 Linux `PCMCIA` 系统默认使用的方案。大多数 `CardBus` 桥器支持多种向主机 CPU 交付中断的方法。方法包括：“并行”中断（每个支持的 `irq` 在桥器上都有专用引脚）；各种串行中断协议（使用一个或两个引脚与中断控制器通信）；以及混合模式（`PCI` 中断可能使用专用引脚信号，而 `ISA` 中断通过串行控制器交付）。

通常情况下，BIOS 负责为桥器编写适当的中断交付方法。然而，某些系统执行得不正确，在某些情况下，软件无法安全地检测到正确的方法。`i82365` 模块在启动时报告桥器，并有一个参数 `irq_mode` 可用于识别。并不是所有的桥器都支持此参数，且 `irq_mode` 的意义取决于桥器类型。请参阅 `i82365` 手页以获取支持的值描述。在某些情况下，桥器可能在多种中断模式下正常工作。

大多数适合 `PCI` 总线插槽的 `PCI` 读卡器提供 `PCI` 中断路由。Linux 驱动程序假设所有桥都有中断能力，这在笔记本电脑上通常是正确的。对于卡读卡器，通常需要使用 `irq_mode` 参数来指定“仅 `PCI`”的中断交付模式；该值取决于桥器类型，请检查 `i82365` 手页。少数 `PCI` 读卡器需要允许 `ISA` 中断的 `irq_mode`，但这些中断并未连接；在这种情况下，请使用 `irq_list=0`。

检查系统日志并验证 `CardBus` 是否有 `PCI` 中断分配。如果没有，请解决该问题，如果中断仍然存在，请返回此处。接下来，尝试对 `irq_mode` 参数的不同值进行实验。

### 5.2.4 无 PCI 中断分配；有效的路由表

**症状：**

- Intel `PCI` probe 对每个插槽报告“no pci irq”。
- 存在路由表，且路由器类型受支持。

当存在路由表时，`pcmia_core` 模块将尝试自动配置 `PCI` 中断分配。如果有多个有效选择，你必须使用 `pci_irq_list=...` 选项来指定分配哪个中断。最好的办法是选择分配给另一个设备的最常用的中断。移动到另一个插槽有时可以提供快速解决方案。如果该插槽与已配置的设备共享中断，那么 `PCMCIA` 驱动程序将能够顺利识别出来。

### 5.2.5 无 PCI 中断分配；未知中断路由器

**症状：**

- Intel `PCI` probe 对每个插槽报告“no pci irq”。
- 存在路由表，但路由器未知。

为新的中断路由器添加支持是棘手的，但并不是一项大任务。首先从数据表中确定你的路由器如何引导 `PCI` 中断。然后看看你是否可以从 `dump_irq` 的输出猜测链接值的含义。大多数路由器有四个中断引脚，链接值可能是 `1,2,3,4`。在某些情况下，桥器可能在多一个中断模式下正常工作。

### 5.4.1 pcinitrd 辅助脚本

`pcinitrd` 脚本创建一个用于带 `PCMCIA` 根分区启动的基本 `initrd` 镜像。该镜像包含最小的目录层次结构、一些设备文件、几个二进制文件、共享库以及一组 `PCMCIA` 驱动模块。在调用 `pcinitrd` 时，你指定要包含在镜像中的驱动模块。核心 `PCMCIA` 组件 `pcinitrd_core` 和 `ds` 会自动包含。

例如，如果你的笔记本电脑使用兼容 `i82365` 的主机控制器以及 `Adaptec` `SlimSCSI` 适配器。你可以使用连接到其上的硬盘上的根文件来创建一个镜像：

```
pcinitrd -v initrd pcmcia/i82365.o pcmcia/aha152x.cs.o
```

要自定义你的 `initrd` 序列，你必须使用类似下面的命令通过“回环”设备启动镜像：

```
mount -o loop -t ext2 initrd /mnt
```

然后编辑 `linuxrc` 脚本。配置文件将安装在镜像的 `/etc` 中，并且也可以进行自定义。查看 `pcinitrd` 的 man 页获取更多信息。

### 5.4.2 创建 initrd 启动软盘

使用 `pcinitrd` 创建镜像后，你可以通过将内核、压缩的 `initrd` 镜像和几个 `lilo` 支持文件拷贝到干净的软盘来创建一个启动软盘。在以下示例中，我们假设目标 `PCIA` 根设备是 `/dev/sda1`：



```
mk2fs /devfd0
mount /devfd0 /mnt
mkdir /mnt/etc /mnt/boot /mnt/dev
cp -a /dev/fd0 /dev/sda1 /mnt/dev
cp [kernel-image] /mnt/vmlinuz
cp /boot.b /mnt/boot.b
gzip < [initrd-image] > /mnt/initrd
```

创建内容如下的 `/mnt/lilo.conf`：

```
boot=/dev/fd0
compact
image=vmlinuz
label=linux
initrd=/initrd
read-only
root=/dev/sda
```

最后，调用 `lilo`：

```
lilo -r /mnt
```

当使用 `-r` 调用 `lilo` 时，它相对于指定的备用根目录执行所有操作。在 `/mnt/dev` 下创建设备文件的原因是 lilo 在此备用根模式运行时将无法使用 `/dev` 中的文件。

### 5.4.3 在非 Linux 驱动器上安装 initrd 镜像

使用 initrd 功能的一个后果是适用于内部硬盘专门用于另一个操作系统的系统。Linux 内核和 initrd 镜像可以放在非 Linux 分区中，并设置 lilo 或 LOADLIN 从这些镜像中启动 Linux。

假设你已经为适当的根设备配置了内核，并在另一个系统上创建了 initrd 镜像，最简单的方法是使用 `LOADLIN` 启动 Linux，如下：

```
LOADLIN <kernel> initrd-<image>
```

一旦在目标机器上启动 Linux，你可以安装 lilo 以允许直接启动 Linux。例如，`/dev/hd1` 是非 Linux 目标分区，而 `/mnt` 可以作为挂载点。在 Linux 文件上为目标创建一个子目录：

```
mount /dev/hd1 /mnt
mkdir /mnt/linux
cp [kernel-image] /mnt/linux/vmlinuz
cp [initrd-image] /mnt/linux/initrd
```

在此示例中，`/dev/sda1` 是所需的 Linux 根分区，通过 PCMCIA SCSI 适配器挂载的 SCSI 硬盘。要安装 lilo，创建一个内容如下的 `lilo.conf` 文件：

```
boot=/dev/hda
map=/mnt/linux/map
compact
image=/mnt/linux/vmlinuz
label=linux
root=/dev/sda1
initrd=/mnt/linux/initrd
read-only

other=/dev/hda1

table=/dev/hda
```

`other=` 行表示安装配置，并可能...

（注：此处原文存在大量重复，已过滤）

# 6. 处理不支持的卡

# 调试技巧与编程信息

编辑 `pcnet_cs` 后，编译并安装新模块。再次编辑 `/etc/pcmcia/config`，将卡绑定从 `memory_cs` 更改为 `pcnet_cs`。按照指令重新加载配置文件，然后就大功告成了。请向我发送你的 `hw_info` 和 `config` 条目的的副本。

如果你在十六进制转储（hex dump）中找不到显卡的地址，作为最后的手段，可以在 `pcnet_cs` 模块初始化时“硬接线”地址。编辑 `/etc/pcmcia/config.opts` 并添加一个 `hw_add=` 选项，如下所示：

```
module "pcnet_cs" opts "hw_add=0x00,0x80,0x8c,0x01,0x02,0x03"
```

当然，请在适当的位置将其替换为你显卡的硬件地址。请注意，如果你已经到了这一步，那么你的卡极可能不是真正兼容 NE200。事实上，我不确定是否还有哪些卡是无法前两种方法处理的。

### 6.3 PCMCIA 接口卡

Compaq Aero 以及其他笔记本电脑使用的 PCMCIA 软驱接口尚未被此软件包支持。支持 Aero 软驱的障碍在于，Aero 似乎使用了自定义的 PCMCIA 控制器来支持到软驱的 DMA。在不知道具体实现方式的情况下，无法在 Linux 下实现相关支持。

如果 Aero 启动时存在软驱卡，Aero BIOS 将配置该卡，Linux 将其识别为普通软驱。当加载 Linux PCMCIA 驱动程序时，它们会注意到该卡已经配置并附加到了 Linux 驱动程序，因此该插槽将被忽略。所以，如果驱动器在启动时存在，则可以使用它，但该卡不支持热插拔。

# 调试技巧与编程信息

## 7.1 提交有效的问题报告

提交报告的最佳方法是使用在线 pcmia-forums 或 SourceForge 上的错误跟踪器（bug tracker）。这样，其他人就可以看到当前的问题（如果有修复方案或变通方法）。所有错误报告都应该包含以下内容：

- 你的系统品牌和型号。

- 你使用的所有 PCMCIA 卡。

- 你的 Linux 内核版本（例如 `uname -rv`）以及 PCMCIA 驱动版本（例如 `cardctl -V`）。

- `lspci -v` 的输出。

- 你对 `/etc/pcmcia/config` 或 PCMCIA 启动脚本所做的任何更改。

- 你的系统日志文件中与 PCMCIA 相关的消息。

# 7. 调试技巧与编程信息

所有的 PCMCIA 模块都会将状态发送到系统日志。这些通常位于 `/var/log/messages` 或 `/var/log/syslog`。当你遇到问题时，这些文件应该是首选查找位置。在提交错误报告之前，请确保你使用的是最新的驱动程序版本。如果找不到你的系统消息，请检查 `/etc/syslog.conf`。阅读错误报告是非常有益的，如果你无法访问网络，可以将错误报告发送给我 `dahinds@sourceforge.net`。然而，我更倾向于让错误报告发布在 pcmia-cs 上以便他人看到。

## 7.2 解释错误报告

如果错误涉及内核故障（kernel fault），只有当将故障地址转换为有意义的符号时，寄存器转储（register dump）才有用。最近版本的 `klog` 可以翻译故障地址，但如果故障发生在模块中，或者问题严重到 `klog` 无法完成向系统日志的写入，这种方法可能无效。如果故障发生在内核中，可以在 `System.map` 中查找故障地址。这位于 `/System.map` 或 `/boot/System.map`。如果故障发生在模块中，`nm` 命令提供了相同的信息，故障地址已根据模块加载地址进行了调整。假设你有内核：

```
Unable to handle NULL pointer dereference
current->tss.cr3 = 014c9000, cr3 = 014c9000
pde = 00000000
ops: 0
CPU: 0
EIP: [0026081]
EFLAGS: 0010282
```

故障地址是 `0xc26081`。查看 `System.map` 我们可以看到这在内核末尾，即内核模块中。要确定是哪个模块，检查 `nm -m | sort` 的输出：

| Address | Symbol | Defined by |
| :--- | :--- | :--- |
| c200d00 (35k) | | [pcmia_core] |
| c200d10 | register_ss_entry | [pcmia_core] |
| c200d230 | register_ss_entry | [pcmia_core] |
| c202600 (9k) | | [3c574_cs] |
| c202a00 (4k) | | [serial_cs] |

所以，`0xc26081` 在 `3c574_cs` 模块中，它是模块开始处的偏移 `0x0081`。我们无法在 `ksym` 中查找此偏移：当内核加载模块时，它会在模块加载地址插入一个头部。头部的大小随内核版本变化：要找到你内核的大小，检查导出符号的模块（如 `pcmia_core`），并与 `nm` 输出进行比较。在本示例中，`register_ss_entry` 加载在 `0xc200d1c - 0xc200d00 = 0x01c` 偏移处，而 `nm pcmia_core.o` 显示偏移为 `0x00c`，因此头部大小为 `0x01c - 0x00c = 0xb4`。回到 `3c574_cs`，我们的故障偏移是 `0x0081`，头部 `0x04ac`。现在查看 `nm 3c574_cs.o | sort`，我们看到：

```
0000002 d if_names
0000002 t 3574_attach
0000040 d preamble_preamble
0000041 d dev_info
```



所以，故障位于 `3c574(attach)`。在本示例中，故障没有导致系统死机，因为故障发生后 `ksym` 还可以建立。在其他情况下，你可能需要以相同的顺序和相同的地址加载多个模块。如果在插入卡时发生故障，请在插入卡之前运行 `ksym`，或者在插入卡的情况下运行。你可以使用 `insmod` 手动加载卡驱动，并在插入卡之前运行 `kms`。更多背景信息请参见 `man inserted`、`man kms` 和 `man klog`。在内核源码树中，`Documentation/ops-tracing.txt` 也有帮助。以下是一些内核调试提示：

- 根据故障，翻译“调用栈（Call Trace）”中的地址可能有用，使用与主故障地址相同的步骤。

- 要诊断静默死机，需要在禁用的情况下触发问题，因为发送到控制台的内核消息将可见。

- 如果你杀死 `klog`，大多数内核消息将直接回显在控制台上，如果问题阻止了 `klog` 写入系统，这可能会有用。

- 为了允许内核消息发送到控制台，对于 2.2 及更高内核，如果 `/proc/sys/kernel/printk` 存在：

```
echo 8 > /proc/sys/kernel/printk
```

会在控制台上打印寄存器转储。即使系统完全没有响应，这可能仍然有效，且 `EIP` 地址可以解释为内核故障。

- 对于启用了 `CONFIG_STTY` 的 2.2 及更高内核，可以通过特殊的 `<Alt><SysRq>` 组合键可以使用应急函数，文档见内核源码树中的 `Documentation/sysrq.txt`。

## 7.3 低级 PCMCIA 调试辅助

PCMIA 模块包含一个条件编译的调试代码列表。这大部分由 `PCMIA_DEBUG` 预处理器定义控制。如果未定义此项，则不会编译调试代码。如果设置为 `0`，则代码被编译但未激活。数字越大，详细程度越高。每个使用 `PCMIA_DEBUG` 构建的模块都将有一个整数参数 `pc_debug`，用于控制输出的详细程度。这可以在模块加载时进行调整，无需重新编译。你的默认 `syslog` 可能会记录这些消息。为了确保它们被记录，请编辑 `syslog.conf`。PCMIA 分布的 `debug_tools` 子目录下有一些寄存器调试工具。用于 ISA 到 PCMCIA 控制器。

## 7.4 /proc/bus/pccard

在 2 及更高内核上，PCMIA 软件包会在 `/proc/bus/pccard` 下创建一个状态信息树。大部分信息只能使用主控制器的数据表来解释。其内容取决于驱动的配置方式，但可能包含全部或部分内容：

`/proc/bus/pccard/{irq,ioport,memory}`

如果存在，这些文件包含了补充内核资源表的资源信息。最近版本的 PCMIA 系统可能会根据配置从即插即用 BIOS 获取额外的资源信息。

`/proc/bus/pccard/drivers`

在最近的中，这列出了所有加载的 PCMCIA 客户端驱动。与 `/proc/modules` 不同，它还列出了可能静态链接到内核的驱动。

`/proc/bus/pccard/*info`

对于每个插槽，这描述了主机及其功能。

`/proc/bus/pccard/*/exca`

这包含了控制器的“ExCA”`Intel i82365sl` 兼容寄存器集。

`/proc/bus/pccard/*/{pci,cardbus}`

对于 CardBus 桥器，这是桥器 PCI 配置空间的转储，以及桥器 CardBus 配置寄存器的转储。

# 7. 调试技巧与编程信息

## 7.5 为新卡编写 Card Services

《Linux PCMCIA 程序员指南》是客户端驱动接口的最佳文档。最新版本可以在 `projects.sourceforge.net` 的 `/pub/pcmia-cs/doc` 中获取，或者在网页 <http://pcmia-cs.sourceforge.net> 上查看。

对于与普通 ISA 设备较相似的设备，你可能可以使用现有 Linux 驱动程序的部分。在某些情况下，最大的挑战将是修改现有的驱动程序，使其能够处理启动后的设备添加和删除。在当前的驱动中，内存卡驱动程序是“自包含”的驱动，它不依赖 Linux 内核的其他部分即可完成大部分的脏活工作。

在很多情况下，支持新卡最大的障碍是从制造商处获取技术信息。弄清楚应该问谁或解释需要哪些信息可能很困难。然而，除少数例外外，如果没有制造商提供的技术信息，为卡实现驱动程序是非常困难甚至是不可能的。

我写了一个带有大量注释的虚拟驱动，解释了驱动程序如何与 Card Services 通信；你可以在 PCMCIA 源码分发的 `clients/dummy_cs.cs` 中找到它。

## 7.6 PCMCIA 客户端驱动作者指南

我决定，将所有 PCMCIA 客户端驱动作为 PCMCIA 软件包的一部分进行分发并不可行。每个新驱动都会让主包的维护变得越来越困难，而且包含驱动程序不可避免地会将部分维护工作从作者转移给我。相反，我将根据用户需求和可维护性，具体决定是否包含贡献的驱动程序。对于未包含在核心包中的驱动，我建议作者采用以下方案对其驱动进行打包分发。

驱动程序文件应该按照 PCMCIA 源码分发相同的目录结构安排，这样驱动程序就可以解压到完整的 PCMCIA 源码树上。驱动程序应该包含源文件（位于 `/modules/`）、一个主页（位于 `/main/`）和文件（位于 `/etc/`）。顶目录还应该包含一个 `README` 文件。

顶目录应包含一个 `Makefile`，其设置应使得 `make -f all` 和 `make -f install` 编译驱动程序并安装所有适当的文件。如果此 `Makefile` 被赋予 `.mk` 扩展名，那么它将被顶层 `Makefile` 为所有的 `all` 和 `install` 目标调用。以下是此类 `Makefile` 的构建示例：

```
# Sample Makefile for contributed client driver
FILES = sample_cs.mk README.sample_cs \
modules/sample_cs.c modules/sample_cs.h \
etc/sample_cs.conf etc/sample_cs.opts \
man/sample_cs.4

all:
install:
	$(MAKE) -C modules MODULES=sample_cs.o
	$(MAKE) -C install-modules MODULES=sample_cs.o
	$(MAKE) -C etc install-clients CLIENTS=sample
	$(MAKE) -C man install-man-4 MAN4=sample_cs.4
```

`dist`:

```
tar czvf sample_cs.tar.gz $(FILES)
```

此 `Makefile` 使用 PCMCIA 软件包 `2.9.10` 及更高版本中的 `install` 目标。为了方便作者，此 `Makefile` 还包含了一个 `dist` 目标。你可能想为最终的包文件名添加版本号（例如 `sample_cs-1.5.tar.gz`）。一个完整的分发如下：

```
sample_cs.nk
README.sample_cs
modules/sample_cs.c
modules/sample_cs.h
etc/sample.conf
etc/sample
etc/sample.opts
man/sample_cs.4
```

通过这种安排，当贡献的驱动被解压时，它会成为 PCMCIA 源码树的一部分。它可以利用 PCMCIA 头文件以及检查用户系统配置的机制和自动依赖检查，就像“正常”的客户端驱动一样。

在这个示例中，`/etc/sample` 和 `/etc/sample.opts` 将是新驱动程序的配置脚本（如果需要），而 `/etc/sample.conf` 将包含对 PCMCIA 卡配置文件的任何添加。从 `3.1.6` 版本开始，`cmmgr` 将自动处理安装在 `/etc/pcmcia` 中的 `*.conf` 文件，因此安装贡献的驱动程序不再需要手动编辑配置文件。

我将接受按照此规范准备的客户端驱动，并将它们放置在 `projects.sourceforge.net` 的 `/pub/pcmia-cs` 目录下。该目录下的 `README` 将描述如何解压非贡献的驱动。

客户端驱动接口随时间推移变化不大，并且始终保持向后兼容。对于主包的微小修订，客户端驱动不需要更新。我将尝试通知贡献驱动的作者关于需要更新其驱动的更改。

## 7.7 Linux 发行版维护者指南

如果你有希望系统配置工具具备 PCMCIA 感知，请使用 `/etc/pcmcia` 中的 `*.opts` 文件，如果用户编译并安装 PCMCIA 软件包的新版本，这些文件不会被修改。如果你修改了配置脚本，全新的安装将静默地覆盖你的自定义脚本并破坏与你的配置工具的连接。如果你不确定如何编写适当的脚本，或者你需要额外的功能，请联系我。



如果你能记录你的发行版与本文描述的 `PCMCIA` 软件包之间的差异，对你（对我）来说是有帮助的。特别是记录对启动脚本和配置脚本的更改。如果你向我发送适当的信息，我将将其包含在 `2.6`（关于特定发行版的说明）中。

在为发行版构建 `PCMCIA` 时，考虑包含不是 `PCMCIA` 软件包一部分的贡献驱动。出于可维护性的考虑，我正尝试限制核心包的大小，只有当我认为某些驱动具有特别广泛的兴趣时才添加新驱动。其他驱动程序将按照上一节所述单独分发。集成驱动和独立驱动之间的划分在某种程度上是任意的，且部分出于历史原因，不应意味着质量上的差异。
