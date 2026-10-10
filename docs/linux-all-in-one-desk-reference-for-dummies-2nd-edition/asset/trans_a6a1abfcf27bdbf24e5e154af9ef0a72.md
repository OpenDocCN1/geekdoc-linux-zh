
然而。如果你正在启动 SCSI 磁盘且未将 SCSI 驱动程序编译到内核中，那么 RAM 磁盘是必需的。

## ATA/ATAPI/MFM/RLL 支持

下一组问题涉及 IDE 设备，例如硬盘和 ATAPI CD-ROM 驱动器。

- ATA/ATAPI/MFM/RLL 支持

ATA/ATAPI/MFM/RLM/RLL 支持 (IDE) [M/n/y/?]
增强型 IDE/MFM/RLL 磁盘/CD-ROM/磁带/软驱支持 (BLK_DEV_IDE) [M/n/y/?]

在配置操作系统时，你必须习惯大量的缩略词——这里就有四个：ATA、ATAPI、MFM 和 RLL。它们都涉及硬盘或连接磁盘驱动器与 PC 的接口。以下是它们的含义：

- ATA 代表 AT Attachment（AT 附加），指连接硬盘和 CD-ROM 驱动器到 PC 主板的 PC-AT 风格接口。

- ATAPI 代表 AT Attachment Packet Interface（AT 附加数据包接口），指最初将磁盘控制器集成在硬盘驱动器本身上的 PC 硬盘。这种接口过去被称为 Integrated Drive Electronics（集成驱动器电子学），即 IDE。你通常会看到 IDE、ATA 和 ATAPI 这些术语互换使用。

- MFM 代表 Modified Frequency Modulation（调制频率调制），这是旧式硬盘上数据编码的方式。这些硬盘可以通过 IDE 接口工作。

- RLL 代表 Run Length Limited（游程有限），是 PC 早期在硬盘上存储数据的一种旧技术。RLL 磁盘可以通过 IDE 接口工作。

第一个问题询问你是否希望内核支持 IDE 设备。第二个问题询问你是否希望使用功能齐全的 IDE 设备，该设备可控制多达十个 IDE 接口。由于每个 IDE 接口可以有一个主设备和一个从设备，这使得 Linux 可以访问总共多达 20 个 IDE 设备，如磁盘或 CD-ROM 驱动器。你可以按 Enter 键接受这两个选项的默认选择，即作为模块。

下一组选项涉及各种 IDE 驱动程序。你可以接受这些选项的默认答案。请注意，IDE/ATAPI FLOPPY 指的是 IDE 软驱，如 Iomega Zip 驱动器或 IOMEGA Superdisk LS-120 驱动器。关于 CMD640 和 RZ1000 错误修复的问题涉及用于 IDE 接口的特定芯片组的一些已知问题。

## SCSI 设备支持

这组选项与 SCSI 设备有关。SCSI 代表 Small Computer Systems Interface（小型计算机系统接口）——这是一种可以连接多个设备（如硬盘和扫描仪）到 PC 的接口类型。如果你的系统有 SCSI 适配器，你应该首先对 *SCSI* 选项回答 *Yes*（是）。之后，你需要回答关于连接到 SCSI 适配器的设备类型（磁盘、磁带、CD-ROM）的问题。最后，你必须启用系统中特定 SCSI 适配器型号的支持。

## IEEE 1394 (FireWire) 支持

下一组选项用于启用 IEEE 1394 支持，无论是作为模块还是链接到内核。IEEE 1394 是一种连接外设到 PC 的高速串行总线。苹果称此总线为 FireWire；索尼称其为 iLink。IEEE 1394 类似于 USB，但它可以以高达 400 Mbps 的速率传输数据，这比旧版 USB 1.1 的数据传输速率快 30 多倍。（请注意 USB 2.0 快得多；它可以以高达 480 Mbps 的速率传输数据。）由于其高速数据传输率，IEEE 1394 非常适合将高速外设（如数字音频和视频设备以及外部硬盘）连接到 PC。

目前，Linux 支持与 Texas Instruments PCI/lynx/PCILynx2 兼容的 IEEE 1394 芯片组以及 OHCI 芯片组。如果你的 PC 有 IEEE 1394 适配器，你可以通过这些选项构建必要的驱动程序。

- IEEE 1394 (*Firewire*) 支持
- IEEE 1394 (*Firewire*) 支持 (*IEEE1394*) `[M/n/y/?]`

![](img/792720823146d68f19fd50c99ebfce4b_509_0.png)

要了解有关在 Linux 中使用 IEEE 1394 外设的更多信息，请访问 `www.linux1394.org` 上的 IEEE 1394 for Linux 项目网站。

## I2O 设备支持

读作 *eye-two-OH*，I2O 指的是 Intelligent Input/Output（智能输入/输出）——一种独立于操作系统和被控设备的新设备驱动程序架构。I2O 通过逻辑上分离负责管理设备的部分和包含操作系统特定细节的部分来工作。（驱动程序功能的逻辑分离称为 *I2O Split Driver model*（I2O 分拆驱动器模型）。）I2O 驱动程序的这两个部分是 OS Services Module（OSM，操作系统服务模块），它与操作系统协同工作，以及 Hardware Device Module（HDM，硬件设备模块），它与驱动程序管理的特定接口设备交互。OSM 和 HDM 通过相互传递消息进行通信。

Linux 附带了一些用于 SCSI 和 PCI 设备的 I2O 驱动程序。你可以通过以下配置选项构建 I2O 驱动程序：

I2O 设备支持

- I2O 支持 (I2O) [M/n/y/?]
- I2O 配置支持 (I2O_CONFIG) [M/n/?]
- I2O 块 OSM (I2O_BLOCK) [M/n/?]
- I2O SCSI OSM (I2O_SCSI) [M/n/?]
- I2O /proc 支持 (I2O_PROC) [M/n/?]

## 网络支持

这组选项涉及网络。如何设置这些选项取决于你希望在网络中使用 Linux 系统的方式。由于 X Window System 使用 TCP/IP 网络（即使你的 PC 未连接任何网络），因此请始终对 TCP/IP Networking 选项回答 Yes（是）。你还可以启用对 IPv6 的实验性支持——下一代互联网协议。

如果你希望将 Linux 系统用作 *firewall*（防火墙）——一个控制局域网（LAN）和互联网之间信息流动的中间系统，请对 Network packet filtering 选项回答 Yes（是）。

网络支持选项中的其他类别包括无线局域网、以太网（10/100 Mbps 以及千兆）、ATM（异步传输模式）、令牌环、ARCnet、AppleTalk、广域网（WAN）、PCMCIA 网络设备、业余无线电、红外线和蓝牙。对于以太网，你可以为你的系统安装的以太网卡构建支持。此类还包括无线网络的驱动和无线以太网卡的驱动。你还可以启用对 SCTP（流控制传输协议）的实验性支持——旨在通过 IP 网络传输公共交换电话网络信令消息（RFC 3758 描述了 SCTP）。

红外线支持用于使用 Infrared Data Association（IrDA，红外数据协会）指定的协议进行红外通信。IrDA 通信被许多笔记本电脑和个人数字助理（PDA）（如 Palm 和 Handspring）使用。许多红外接口形式为 *dongles*（小型适配器），通常连接在 PC 的串行端口上。你可以使用本节的选项来启用对几种常见类型 dongles 的支持。

蓝牙是一种低功耗、短距离无线技术，用于在 2.4 GHz 频段连接设备。使用蓝牙的设备通常可以在彼此 10 米范围内连接。要了解有关蓝牙的更多信息，请访问 www.bluetooth.com。Linux 通过核心驱动器和几个其他模块支持蓝牙。你可以回答 y 以启用蓝牙支持，然后选择特定于你的蓝牙设备的其他选项。

### ISDN 子系统

这组选项允许你包含对 *ISDN*（综合业务数字网）的支持——这是一种你可以用来将 Linux 系统连接到互联网的数字电话线。这些与 ISDN 相关的选项包括特定 ISDN 适配器的配置。

只有当你的 PC 有 ISDN 卡时才构建 ISDN 驱动程序。如果你预计将添加 ISDN 卡并从电话公司购买 ISDN 服务，你可以将驱动程序构建为模块。

### 电话支持

使用正确的硬件和软件，电话支持选项使你可以使用 Linux 系统进行互联网电话呼叫（也称为 *voice over Internet Protocol* 或 *VoIP*，即网络电话）。如果你有电话卡，例如由 Quicknet Technologies, Inc. 制造的 Internet PhoneJACK 或 Internet LineJACK，你可以选择构建电话支持的驱动程序模块。如果你没有电话卡，你可以安全地关闭这些选项。

### 输入设备和字符设备

接下来的几个选项涉及配置键盘、鼠标、游戏杆和触摸屏等输入设备，以及连接到串行和并行端口的设备。这些选项还包括多端口串行接口卡的配置，这些卡使你可以将多个终端或其他设备连接到你的 Linux 系统。如果你的系统没有此类设备，请回答 *No*（否）。在列表的末尾，你会看到一个关于并行打印机支持（*PRINTER*）的问题。如果你计划将打印机连接到并行端口，请对此选项回答 *Yes*（是）。

### 看门狗定时器

这些配置选项允许你开启对看门狗定时器的支持。基本上，这会导致内核创建一个特殊文件；如果不能每分钟打开该文件并写入它，系统就会重启。一些看门狗板可以监控 PC 的状态（包括温度）。你还可以从这组选项中启用对特定看门狗卡的支持。

如果你希望访问 PC 的实时时钟中的非易失性（电池备份）内存——*NVRAM*——请对 *NVRAM* 选项回答 *Yes*（是）。你可以通过启用 *RTC* 选项来访问实时时钟。

### 软盘磁带驱动器

如果你的软盘控制器连接了磁带驱动器，请对下一个选项回答 *y* 或 *m* 并适当选择其他参数（或接受默认选择）：

