
## 第二章：安装 Red Hat Linux

### 本章内容

- 列出你的 PC 硬件清单
- 创建 Red Hat 安装启动盘
- 为 Red Hat Linux 预留磁盘空间
- 开始 Red Hat Linux 安装
- 为 Red Hat Linux 创建硬盘分区
- 设置关键系统参数
- 选择要安装的软件包

PCs 预装了 Microsoft Windows。如果您想使用 Red Hat Linux，首先必须安装它。本书附带 Red Hat Linux DVD — 您要做的就是按照本章中解释的步骤进行安装。

您可能会担心在 PC 上安装新的操作系统。您可能会觉得这就像脑外科手术——或者更确切地说，更像是移植一个新大脑，因为您可以除了 Microsoft Windows 之外再安装 Red Hat Linux。像这样安装两个操作系统时，您可以在开机时选择启动其中一个。将 Red Hat Linux 添加到装有 Windows 的 PC 上最大的麻烦是创建新的磁盘分区——基本上是为 Red Hat Linux 预留磁盘的一部分。剩下的安装过程相当常规，只需按照说明进行即可。我在本章中解释了所有内容。

## 按照安装步骤操作

安装 Red Hat Linux 涉及多个步骤——我希望在不涉及细节的情况下简要带您了解它们。然后您可以按照详细步骤，从本书的附带 DVD 安装 Red Hat Linux。

第一步是快速盘点 PC 中的一些关键硬件组件，并确保它们在 Red Hat Linux 中都能正常工作。

如果您正在购买新 PC，请在购买前确保其组件对 Linux 友好。如果您计划在旧 PC 上安装 Red Hat Linux，请收集有关硬件的信息（制造商、型号等），并将其与 Red Hat Linux 支持的硬件列表进行核对（该列表可在网页 `hardware.redhat.com/hcl` 上获取）。如果旧 PC 的某些组件在 Red Hat Linux 中无法工作——而没有它们就无法运行——那么就不要在该 PC 上安装 Red Hat Linux。

第二步——如果您的 PC 无法从 DVD-ROM 驱动器启动——是准备一个 Red Hat *安装启动盘*——一张软盘，您可以在开始安装时用它来启动 PC。您可以在 Windows 中使用专门为此目的设计的程序（包含在附带 DVD-ROM 上）来准备启动盘。

第三步是在 PC 的硬盘上为 Red Hat Linux 腾出空间。如果您正在运行 Microsoft Windows，此步骤可能容易也可能困难，这取决于您是想用 Red Hat Linux *替换* Windows 还是保留 *两者* Windows 和 Red Hat Linux。

如果您想在不删除（或干扰）Windows 的情况下安装 Red Hat Linux，请记住您现有的操作系统——我假设是 Windows 95、98、Me、NT、2000 或 XP——目前正在使用整个硬盘。这意味着您必须 *分区*（划分）硬盘，以便 Windows 位于其一部分，Red Hat Linux 位于另一部分。这样做可能令人害怕，因为您有损坏硬盘并抹去其上所有内容的风险。

在创建 Red Hat Linux 安装程序可用的硬盘新位置之前，您可能希望使用程序来帮助您创建分区，以保持安心。如果您的 Windows 版本是 NT、2000 或 XP，请考虑投资购买 PartitionMagic 等商业硬盘分区产品。对于 Windows 95/98/Me 系统，您可以使用名为 `FIPS` 的程序（包含在本書 DVD 上）。

在为 Red Hat Linux 预留硬盘分区后，您可以开始最后一步——从 Red Hat 安装启动盘启动 PC 并开始 Red Hat Linux 安装。安装过程中有相当多的步骤，但到目前为止，应该会顺利进行。只需浏览安装屏幕，您应该在一两个小时内完成。Red Hat 安装程序会启动图形用户界面（GUI）并引导您完成所有步骤。其中一个关键步骤再次涉及分区硬盘，但这次您只需分割之前创建的额外分区。完成一些配置步骤后，例如设置网络和时区，您选择要安装的软件包，然后让安装程序完成剩余的安装任务。

## 检查 PC 硬件

在做任何其他事情之前，您首先需要检查 PC 的硬件是否与 Red Hat Linux 兼容。您可以直接开始安装，但如果 Red Hat Linux 无法识别 PC 中的某些硬件，安装可能不会成功。因此，在开始安装 *之前* 请先检查硬件与 Red Hat Linux 的兼容性。

*注意：并非每件硬件都必须与 Red Hat Linux 兼容——只有您想与之一起使用的硬件。例如，您可以在带有不受支持的声卡的 PC 上安装 Red Hat Linux——只要您不在 Red Hat Linux 中关心播放任何音频 CD 即可。*

那么，这里有一份简短的 PC 硬件清单，这些硬件在 Red Hat Linux 中 *必须* 正常工作，否则您无法继续：

- 处理器（也称为中央处理器，或 CPU）
- 硬盘
- DVD-ROM 驱动器（如果您只有 CD-ROM 驱动器，则必须使用本书背面的优惠券订购 CD-ROM 版 Red Hat Linux）
- 键盘

所有这些都必须与 Red Hat Linux 兼容。要使 GNOME 和 KDE 等 GUI 桌面正常工作，PC 还必须具有兼容的鼠标、显卡和显示器。

### 列出清单，再检查一遍

在您能够检查 Red Hat Linux 是否支持 PC 中的硬件之前，您必须先了解 PC 中有什么。要列出 PC 的硬件清单，请按照以下步骤操作：

1. 从 Windows（任何版本）打开控制面板并双击系统图标。

系统属性窗口出现。初始窗口显示一些重要信息，例如 Windows 版本、处理器类型（例如 GenuineIntel Pentium II Processor）和内存容量（例如 128.0MB RAM）。记下这些信息。

2. 在 Windows 95/98/Me 中，单击设备管理器选项卡。在 Windows NT/2000/XP 中，单击硬件选项卡，然后单击设备管理器按钮。

PC 所有设备的信息出现。

3. 浏览按类型显示设备的树状分层组织中的信息。

例如，您会看到 *CDROM, Disk drives, Display adapters* 等标签。单击标签旁边的加号（⊕）可查看该设备类型的详细信息。例如，当我单击 *Display adapters* 旁边的加号时，我会看到 *ATI Xpert98 AGP 2X*，这是我 PC 上显示适配器（显卡）的型号名称。

4. 写下以下设备的制造商、型号以及其他任何信息，以创建您的硬件清单：

- DVD/CD-ROM 驱动器
- 磁盘驱动器
- 显卡
- 显示器
- 键盘
- 鼠标
- 任何网卡、SCSI 控制器、声卡和调制解调器

完成这些步骤后，您需要安装 Red Hat Linux。总结一下，在开始 Red Hat 安装之前，您通常需要收集 PC 中以下一些或全部关键组件的信息：

- **处理器：** 400 MHz Pentium II 或更好为最佳。处理器速度以 *MHz（兆赫）* 或 *GHz（吉赫）* 表示，只要超过 400 MHz 就不是那么重要，但越快越好。Red Hat Linux 也可运行在其他 Intel 兼容处理器上，如 AMD K5、K6 和 Cyrix 以及 IBM 处理器。

- **RAM：** 这是系统拥有的内存量。与处理速度一样，RAM 越多越好。您至少需要 128MB 来安装 Red Hat Linux 并运行 GUI 桌面。（好吧，我承认。我曾在 233 MHz Pentium II、64MB RAM 的 PC 上安装过 Red Hat Linux，它运行良好，但一切——从安装到日常使用——都痛苦地缓慢。至少它能工作！）

- **DVD/CD-ROM：** 具体型号无关紧要。重要的是 DVD/CD-ROM 驱动器如何连接到 PC。大多数新 PC 的 DVD/CD-ROM 驱动器都连接到硬盘控制器（称为 *IDE 即集成驱动电子设备*）。任何 IDE DVD/CD-ROM 在 Red Hat Linux 中都能工作。

- **硬盘：** 如果在磁盘驱动器名称中看到 *IDE* 这个词，那么它就是 IDE 驱动器，应该能在 Red Hat Linux 中工作。另一种硬盘控制器类型是 SCSI（*小型计算机系统接口*），Red Hat Linux 也支持它。您还需要知道硬盘的大小。要查找磁盘大小，请双击 *我的电脑* 图标 on the
