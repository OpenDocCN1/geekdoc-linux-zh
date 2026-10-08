
# 在 Linux 中设置多端口串口卡

如果你计划使用运行 Linux 的 PC 和哑终端来支持一家小型企业（哑终端比完整的 PC 便宜，你也可以使用旧 PC 当作终端），并且你需要的串口多于两个。那么通过增加另一块串口卡，PC 就可以支持四个串口。如果你需要多于四个串口，则必须购买名为多端口串口卡的特殊 I/O 板。这些板卡通常支持 4 到 32 个不等的任意串口。这些端口共享一个 IRQ，但每个端口都有唯一的 I/O 地址。

许多多端口串口卡使用 `16450` 或 `16550A`。当你购买板卡时，你可能想确认 UART 是否兼容 `16550A`。

为了支持特定的多端口串口卡，你需要在 `/etc/rc.rc.serial` 文件中添加相应的行。有关特定信息，请查阅多端口板卡的文档或联系供应商。Linux 内核串口驱动程序支持以下基于 `16450` 或 `16550A` 的多端口串口卡：

- AST FourPort 及其克隆版本（4 端口）
- Accent Async-c4（4 端口）
- Arnet Multiport-8（8 端口）
- Bell Technologies HUB6（6 端口）
- Boca BB-1004（4 端口），BB-1008（8 端口），BB-2016（16 端口）
- Boca IOAT66（6 端口）
- Boca 2by4（4 个串口和 2 个并行端口）
- Computone ValuePort V4-ISA（兼容 AST FourPort）
- Digi PC/8（8 端口）
- GTEK BBS-550（8 端口）
- Longshine LCS-8880, Longshine LCS-8880+（兼容 AST FourPort）
- Moxa C104, Moxa C104+（兼容 AST FourPort）
- PC-COMM（4 端口）
- Sealevel Systems COMM-2（2 端口），COMM-4（4 端口）以及 COMM-8（8 端口）
- SIIG I/O Expander 2S IO10112（4 端口）
- STB-4COM（4 端口）
- Twincom ACI/550
- Usenet Serial Board II（4 端口）

Boca BB-1004 和 BB-1008 板卡不支持使拨号调制调器工作的载波检测（CD）和铃指示（RI）信号。因此，你无法配合拨号调制调器使用 BB-1004 和 BB-1008 板卡。

某些多端口串口卡使用特殊处理器代替 `16450` 或 `16550` UART。表 E-5 列出了 Red Hat Linux 支持的一些智能多端口串口卡。它还显示了为了支持特定类型多端口串口卡而必须加载的驱动模块。这些驱动模块位于你 Red Hat Linux 系统的 `/lib/modules/VERSION/kernel/drivers/char` 目录下，`VERSION` 为 Linux 内核版本。因此，对于内核版本 `2.4.7-10`，这些驱动模块位于 `/lib/modules/2.4.7-10/kernel/drivers/char` 目录。

## 表 E-5 智能多端口串口卡的 Linux 驱动

| 多端口串口卡 | Linux 驱动模块 |
|---|---|
| SDL RISCom/8 | `riscom8` |
| Comtrol RocketPort | `rocket` |
| Stallion 多端口串口驱动 | `stallion` |
| Microgate Synclink ISA 和 PCI 高速多端口串口适配器 | `synclink` |
| 华硕 W83977af I/o芯片多端口板 | `w83977af_ir` |
| Cyclades Cyblom-Y 和 Cyclades-Z 系列多端口串口卡 | `cyclades` |
| Digi International PC/Xe, PC/XI, PC/Xr 和 PC/Xem | `epca` |
| Hayes ESP 串口卡 | `esp` |
| MultiTech 的 ISI 系列卡 | `isicom` |
| Stallion 智能多端口串口卡 | `istallion` |
| COSA 或 SRP 同步串口卡 | `costa` |

要了解更多关于设置多端口串口卡的知识，你可能想阅读最新的 Serial-HOWTO 文档。要阅读 Serial-HOWTO 文档，请使用浏览器访问 URL `http://www.ibiblio.org/pub/Linux/docs/HOWTO/Serial-HOWTO`。

# 附录 F

## PC 卡

笔记本电脑通常包含用于连接外围设备的 PCMCIA 插槽。`PCMCIA` 是个人内存卡国际（Personal Computer Memory Card International）的非营利组织，它为笔记本电脑添加内存卡的接口进行了标准化。虽然最初是为内存卡设计的，但 PCMCIA 设备因笔记本电脑的各种扩展而流行。今天，笔记本电脑使用许多 PCMCIA 设备，如调制调器、网卡、SCSI 控制器和声卡。使用 Linux 作为笔记本意味着必须处理 PCMCIA 设备，或者说大众媒体所称的 PC Cards。在 David Hinds 的努力下，我们现在可以通过他的 Linux PCMCIA 服务在 Linux 下使用 PCMCIA 设备。我将实际的卡称为 PC Cards，因为这是设备的正式名称。然而，我使用 PCMCIA 术语是因为……

## PC 卡基础知识

多功能能力（Multunction Capability）允许 PC 卡支持多种功能。例如，3Com 的 3C562 是一个 Type II 规格的 PC 卡 10Base-T 以太网卡和 28,800-bps 调制解调器。插插即用（Plug-and-Play）允许你在系统开启时插入或移除 PC 卡（这被称为热插拔）。你可以通过使电源连接引脚最长，来实现 PC 卡的热插拔，这样信号线就会在电源线之前断开。

电源管理（Power Management）是指 PC 卡通过卡服务规范（Card Services Specification）与笔记本电脑的高级电源管理（APM）功能交互。

缩放视频（ZVO）是指 PC 卡与系统视频控制器之间的连接，它允许显卡直接将视频数据写入视频控制器。

## Linux 下的 PCIA 卡服务

PC 卡的标准化意味着 Linux 开发者可以获取为 PC 卡编写设备驱动程序所需的编程信息。特别是，卡服务规范提供了一个应用程序编程接口（API），它独立于控制 PC 卡插槽（即 PC 卡的插座或插槽）的硬件。

相关的插槽服务规范（Socket Services Specification）也提供了一个 API，允许软件应用程序访问控制 PC 卡插槽的硬件。

你不需要学习 PC 卡和插槽服务的 API。David Hinds 已经在他的 `PCIA Card Services for Linux` 中完成了这项工作，这是一个你可以用来在 Linux 下访问 PC 设备的软件包。你所做的只是在需要时开启 PCIA 支持即可。

## 激活卡服务

如果你在安装 Red Hat Linux 时，按照第 2 章概述的步骤操作并选择了“笔记本电脑支持”（Laptop Support）软件包，那么 PCIA 卡软件将安装在你的系统上。如果你没有安装“笔记本电脑”组，可以通过安装第一张光盘上的 `kernel-pcmcia-cs` RPM 来安装 PCIA 软件。

假设支持 PCIA，以下文件控制卡服务的激活：

- `/etc/init.d/pcmcia` 是启动 PCIA 卡服务的 shell 脚本。基本上，`/etc/init.d/pcmcia` 命令在系统启动时激活卡服务。该脚本使用 `/sbin/insmod` 命令加载相应的 PCIA 驱动模块，该模块处理所有的卡片插入和移除事件。运行 `cardmgr` 程序允许你热插拔 PC 卡，以便你可以随时插入或拔出卡。要停止卡服务，输入 `/etc/init.d/pcmia`
- `/etc/sysconfig/pcmia` 包含了 `/etc/init.d/pcmia` 脚本使用的若干变量。特别是，如果 `/etc/sysconfig/pcmia` 文件中出现 `PCIA=no` 这一行，卡服务就不会被激活。如果你的系统没有 PCIA 设备，你会发现这一行 `PCIA=no`。

你可以通过确保 `/etc/sysconfig/pcmia` 文件中出现 `PCIA=yes` 这一行来在启动时激活卡服务。当然，只有当你的电脑具有 PCIA 插槽时（大多数笔记本电脑），你才需要这样做。

## 使用 cardctl 程序

如果你正在运行 PCIA 卡服务，可以使用 `/sbin/cardctl` 程序来监控和控制 PCIA 插槽。要查看 PCIA 插槽的状态，输入：

```
/sbin/cardctl status
```

输出应显示当前的插槽状态标志。

`cardctl` 程序接受许多参数。通过不同的参数，你可以挂起卡、恢复它或查看配置参数（如中断和配置寄存器）。要从在线手册学习更多关于 `cardctl` 的信息，请输入 `man cardctl` 查看手册页。

## 使用支持的 PC 卡

在 PCIA 卡服务的文档目录下，你会找到一个 `SUPPORTED.CARDS` 文件。（你可以通过 `cd /usr/share/kernel/pcmia*` 进入该目录）。该文件列出了所有已知可以在至少一个系统中运行的 PCIA 卡。

支持的卡片列表已过多，无法在此处列出。卡服务支持的卡片分类如下：

- 以太网卡——支持近百种不同型号以太网卡，包括流行型号 3c 3589、3c589B、3c589C 和 3c589D；Megahertz XJ10BT 和 CC10BT；以及 Xircom Credit CE2。
- 快速以太网 (100BASECAR)—支持超过 20 种卡，包括 3c 5747X、3c 5575TX、3CCE575B 和 3CXFE575B；Linksys EtherFast 100/100；以及 Xircom CreditCard CE3。
- 令牌环卡—支持 IBM Token Ring Adapter 和 3Com 3689 TokenLink III 卡。
- 无线网卡 —支持 AT&T/NCR/Lucent WaveLAN version 2.0、DEC RoamAbout/DS 和 Xicom CreditCard Netwave。
- 调制解调器和串口卡：所有的调制解调器卡和串口卡都应该可以工作。唯一的例外是如 Compaq 192、New Media WinSurfer、Megahertz XJ/CC2550、3Com CXM356/3CCM356 和 3CXM656。
- 内存卡——所有静态内存 (SRAM) 均可用。
- SCSI 卡——支持 30 多种不同的适配器。
- ATA/IDE 硬盘—支持许多 ATA/IDE 适配器。
- 多功能——支持多功能卡。

# 附录 G：Linux 资源

本附录列出了你可以获取更多信息的资源。大多数资源都在互联网上，因为那里可以获取有关 Linux 的最新信息。

## 网页

如果你浏览互联网，你可能会发现相当多与 Linux 相关的网页。寻找 Linux 信息的良好起点是 Linux 在线主页：

```
http://www.linux.org/
```

你可以点击按钮来访问该按钮标签所标识的主题的更多信息。在该页面，你还可以找到一个组织良好的 Linux 相关网站链接合集。

要浏览有关 Linux 的最新新闻，请访问 Linux 资源页面：

```
http://www.linuxresources.com/
```

《Linux Journal》的出版社 Specialized Systems Consultants (SSC), Inc. 维护此页面。你可以扫描《Linux Journal》最新一期的文章并找到其他信息，例如最新版本的内核以及指向其他 Linux 资源的链接。

另一个流行且权威的 Linux 信息来源是 Linux 文档项目 (LDP) 的主页，URL 为：

```
http://www.linuxdoc.org/
```

在该网站上，你可以找到许多指向其他 Linux 资源的指针。特别是，你可以从 `http://www.ibiblio.org/pub/Linux/docs/HOWTO/` 浏览并下载最新的 HOWTO 文档。

有关 Red Hat Linux 的特定问题，您可以访问 Red Hat 支持网站：

`http://www.redhat.com/apps/support/`

该网站提供了产品更新（Product-Updates）、错误列表（Errata）、硬件兼容列表（Hardware Compatibility List）以及安装指南和手册等链接。特别是，您可以在 `http://www.redhat.com/apps/support/resources/` 找到手册和常见问题（FAQs）。

如果您对开源开发（包括 Linux）感兴趣，一个很好的资源是 SourceForge.net 网站：`http://sourceforge.net/`

## 新闻组

为了跟上Linux的发展，您需要访问互联网，特别是新闻组。您可以在表 G-1 中找到特定 Linux 相关主题的讨论。

| 新闻组 | 提供以下内容 |
|---|---|
| `comp.os.linux.admin` | 关于 Linux 系统管理的信息 |
| `comp.os.linux.advocacy` | 关于推广 Linux 的讨论 |
| `comp.os.linux.announce` | 关于 Linux 的重要公告。（这是一个受制的新闻组，这意味着您必须向管理员发送文章，然后由管理员将其发布到新闻组。） |
