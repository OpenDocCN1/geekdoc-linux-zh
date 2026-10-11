
现在，你已经准备好从上次离开的地方继续 KNOPPIX 会话，并且可以使用相同的配置和数据文件。

## 总结

KNOPPIX 提供了许多人认为今天最好的可启动 Linux 发行版。它让你在几乎任何可以找到可启动 PC 的地方都能获得完全配置好的 Linux 桌面系统。

除了桌面功能外，KNOPPIX 还包含了使用 Linux 许多服务器、编程和故障排除功能所需的软件。尽管 KNOPPIX 作为内存启动系统在 RAM 中，但默认情况下，有方法可以配置它以跨启动会话保存数据和配置信息。

KNOPPIX 可以在每次启动时都处于一致的状态，这是使用 KNOPPIX 的另一个优势。如果你认为保存的自定义设置已损坏，你可以随时重新启动 KNOPPIX 而不加载它们，以便从干净的 KNOPPIX 系统重新开始。

KNOPPIX 作为访问损坏计算机以进行故障排除的工具特别有价值。在安装了 Microsoft Windows 或其他操作系统的电脑上启动 KNOPPIX 磁盘时，你可以使用 KNOPPIX 访问并处理该电脑硬盘上的数据。

# 第 22 章 运行 Yellow Dog Linux

Yellow Dog Linux 是 PowerPC (PPC) 平台领先的 Linux 发行版之一。Yellow Dog Linux 由 Terra Soft Solutions (`www.terrasoftsolutions.com`) 提供，对 PowerPC 用户的需求提供了无与伦比的关注。

由于大多数 Linux 发行版集中在 Intel/AMD (x86) 平台，因此发现 PowerPC 世界中有一个拥有自己热情社区的主流 Linux 发行版，有时会令人惊讶。像 Fedora 这样的发行版在 PowerPC 世界中也有活跃的社区。然而，Yellow Dog 专注于 PowerPC 的发布。Yellow Dog 不仅运行在 Apple G4/G5 电脑上，还支持 PlayStation 3 和 IBM。Terra Soft Solutions 致力于让 Yellow Dog 适用于 Apple 产品。

本章介绍了 Yellow Dog Linux，并解释了它如何吸引喜爱 Apple 的用户。你可以从 Terra Soft Solutions (`www.terrasoftsolutions.com/store`) 购买 Yellow Dog Linux，或者从书中附带的 DVD 下载。Linux 镜像站：`www.terrasoftsolutions.com/resources/ftp_mirrors`

| 本章内容 |
| 深入 Yellow Dog Linux |
| 安装 Yellow Dog Linux |
| 在 Mac 上运行 Linux |

## 选择和安装不同的 Linux 发行版

## 理解 Yellow Dog Linux

Terra Soft Solutions 致力于让 Yellow Dog 适用于各种 Apple 产品，这减少了硬件不兼容的问题。另一个令人安心的是 Terra Soft Solutions 是 Apple 授权 OEM 增值供应商，可以在 Apple 上安装 Linux。最新的 x86 芯片无法在这些系统上运行。更多信息请参见“迈向 Yellow Dog”章节。

Mac OS X 以 Aqua 的形式被认为是最先进的图形界面之一。尽管 Apple 平台提供了复杂的界面，用户可能会质疑在 Apple 设备上使用 Linux，但有很多合理的理由。

- 应用程序成本——商业应用程序的价格通常比其开源版本更高。例如，Mac 平台上的最新文字处理器可能花费数百美元，而开源替代品通常是免费的。Linux 的可用软件超过了 Mac OS 平台。

虽然一些流行的开源软件适用于 Mac OS X，但它们可能需要进行移植，而不是重新编译。移植应用程序是一个复杂的过程，通常需要操作系统编程专业知识。移植超本书的范围。

- 延长硬件寿命——Linux 以低运行要求闻名。你可以在不支持最新 Mac OS X 的机器上运行 Yellow Dog Linux 并运行 Linux 程序。

- 一致性——Linux 广泛用于后台功能。通过 Yellow Dog Linux（通常被称为 YDL），你可以在同一个生产环境中混合 PowerPC 硬件和 Intel 硬件，实现应用程序和操作系统的一致性，减少支持两种不同操作系统的成本。由于 Linux 是开源且广泛提供的，你可以减少对单一实体的依赖。

- 安全性——Yellow Dog Linux 有数千名程序员的支持，他们不断为软件开发补丁和更新，而不是依赖商业实体或自己动手）。

- Yellow Dog Linux 6.0 带 YDL.net——支持 PlayStation 3；Apple G4 和 G5；IBM 510、520、540、JS20 和 JS21 电脑。该产品还提供对 YDL.net 的访问。通过 YDL.net，你可以获得软件库、支持功能、安全的 Web 邮箱帐户以及个人日历和博客。

## 运行 Yellow Dog Linux

- 适用于 PlayStation 3 的 Yellow Dog Linux 6.0 DVD —— 此版本的 Yellow Dog Linux 包含适用于 PS3 的纸质指南、一张 Yellow Dog Linux 纸以及可选的 6 个月安装支持。

- 适用于 Apple PowerPC 和 IBM System p 的 Yellow Dog Linux 6.0 DVD —— 该 Yellow Dog Linux 软件包包含安装 DVD 和源代码。纸质指南描述了如何在 Apple PowerPC (G4 和 G5) 以及 IBM System p 上安装 Yellow Dog。在线指南涵盖了如何在 OpenPower、510/520/540 系统以及 JS20/21 系统上安装。提供可选的 6 个月支持合同。

### 展望 Yellow Dog 的未来

尽管 Apple 已将其产品线从 PowerPC 转移到 x86 架构，但 Terra Soft Solutions 仍继续为 Power 架构开发 Yellow Dog Linux。虽然 Terra Soft 仍然是苹果顶级的增值合作伙伴，但它也在其他硬件上销售预装的 Linux 系统。

简单来说，Yellow Dog 的使命是支持最新的 Power 架构系统（例如 Sony Playstation 3，以及来自 IBM 和 Mercury Computer 等供应商的基于单元和高端 PowerPC 的系统），并继续为像我这样的 1000 万 万拥有基于 PowerPC 的 Mac 但希望利用 Linux 系统力量的人们提供专注于 PowerPC 的 Linux。

对于高端服务器系统，Terra Soft 在 IBM 970 BladeCenter 4U 服务器和 Mercury Computer 64 位扩展 ATX 10 和 4U 机架式服务器上提供其 Y-HPC 操作系统。在这些机器上使用 Y-HPC 配有 Y-IManager 集群管理软件套件，因此你可以集中管理多个基于 Power 的 Y-HPC 服务器。

在工作站方面，Terra Soft 是 Sony PlayStation 3 的理想供应商。在与 Sony 密切合作以确保完全支持和互操作性后，Terra Soft 于 2006 年 11 月底为 PS3 推出了 Yellow Dog Linux 5.0，现在提供 6.0 版本。同样，Terra Soft 还与 Generis USA (`www.generesi.com`) 合作，推出了预装 Yellow Dog Linux 的开放式桌面工作站。该开放桌面工作站采用微 ATX 规格，配备千兆以太网端口。

底线是，你可以期待 Yellow Dog 满足你的需求。

### 深入了解 Yellow Dog

Yellow Dog Linux 提供了许多功能，但最重要的是以下：

## 硬件支持

过去，Linux 操作系统的硬件支持是一个大问题，但随着 Linux 流行程度的提高，许多设备制造商已经提供了其硬件驱动程序的访问，或者在某些情况下为 Linux 创建了硬件驱动程序。虽然这对于 x86 社区的全新硬件仍然是一个问题，但在 PowerPC 平台上，这种影响被减轻了，因为所有硬件通常都是按照 Apple 严苛的标准制造的。Terra Soft Solutions 专注于 Apple 硬件，通常硬件变体较少，这使得 PowerPC 平台的支持工作要快得多。

Yellow Dog Linux 的伟大之处之一在于于，当你深入研究时，会发现 x86 用户所面临的一些硬件兼容性问题（例如使用 Winmods、众多的硬件配置选项等）被降至最低或消除了。作为获得授权的 Apple 增值值销商，Terra Soft Solutions 可以确保你正在使用的硬件将获得支持。

在在您自己的 PowerPC 硬件上安装 Yellow Dog Linux 之外，你还可以从 Terra Soft Solutions 购买预装了 Yellow Dog Linux 的 PowerPC 硬件。

Terra Soft Solutions 为 Yellow Dog Linux 开发了支持硬件的官方列表（`http://terrasoftsolutions.com/support/hardware`）。从 Yellow Dog Linux 6.0 开始，官方取消了对许多旧硬件配置的支持，包括：

- Apple Mac G4（Power Mac G4 PCI 350–400 MHz G4 及以上）
- Apple Power Mac G5（1.6 GHz G5 及以上）
- YDL PowerStation
- Sony PlayStation 3
- Apple Xserve（ga G4 和 G5）
- Apple iMac（Rev A, B, C 233 MHz G3），eMac G4 以及 iMac G5
- Apple iBook（800 MHz 1.2 GHz G4）

> 注意：你可以使用较早版本的 Yellow Dog 用于旧款电脑。对于旧款电脑，Yellow Dog 5.0.2 应该运行在 2006 年 1 月之前发布的任何基于 PPC 的 Mac 上，但 Old World ROM 或更早的硬件（如 8500s、7200s 和 Performa PowerPC）。YDL 3.0.1 支持此类硬件以及 Yellow Dog Linux 4.1 目前支持的大部分硬件（任何在 2003 年 9 月即 3.0 发布之前由 Apple 制造的硬件）。Yellow Dog Linux 3.0.1 支持并测试的硬件包括：Power Mac 4400–9600、Power Mac G3 型号和蓝白 G3 型，以及 Yellow Dog Linux 4.0 和 4.1 支持的大多数硬件。

如果你有不受官方支持的 PPC 硬件，你仍然应该可以使用 Yellow Dog Linux 4.1，但如果你在不支持的配置下运行，请自担风险（emptor）。Terra Soft Solutions 取消了对许多旧硬件配置的支持，以便专注于最可能的配置。此外，尝试支持过时的计算机架构（这在 Old World ROM 系统上特别为棘手）对于商业性 Linux 创业来说没有太大回报。

## 运行 Yellow Dog Linux

本节其余部分的描述侧重于在 Terra Soft PowerStation（`www.terrasoftsolutions.com/products/powerstation`）上安装 Yellow Dog Linux。

### 在 PowerStation 上安装 Yellow Dog Linux

为了启动 PowerStation，Yellow Dog Linux 安装了 Yet Another Bootloader (`yaboot`) 引导程序。首先，你需要获取本章前面介绍的最新 Yellow Dog Linux 安装 DVD。拿到 DVD 后，在你的 PowerStation 面前，按照以下步骤操作：

- 1. 将 Yellow Dog Linux DVD 插入你的电脑。
- 2. 重启。
- 3. 按指示输入 `s` 进入 Open Firmware。
- 4. 在固件提示符处输入：

```
