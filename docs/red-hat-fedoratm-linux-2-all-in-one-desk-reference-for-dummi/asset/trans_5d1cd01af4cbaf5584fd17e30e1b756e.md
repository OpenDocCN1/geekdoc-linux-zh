

## 504 重建内核

![](img/9f89727199836b0f871f1745838aa8b2_530_0.png)

如果向下滚动图 6-3 右上角窗格中的选项列表，你会发现更多关于块设备的选项。开启 **Loopback Device Support**（回环设备支持）选项后，Linux 内核可以操纵存储在单个大文件中的整个文件系统映像。如果你想要挂载 CD 映像（例如 Fedora Core ISO 文件）并在实际刻录 CD 之前进行检查，此选项非常有用。

**RAM Disk Support**（RAM 磁盘支持）选项允许内核使用系统内存的一部分作为可以存储文件系统的磁盘。**The initial RAM Disk Support**（初始 RAM 磁盘支持）选项创建一个 RAM 磁盘，在系统启动之前由引导加载程序使用。初始 RAM 磁盘仅在系统启动期间发挥作用，此时硬盘可能尚未可用。初始 RAM 磁盘对于在从硬盘分区启动内核之前加载访问硬盘所需的驱动程序模块至关重要。

### ATA/ATAPI/MFM/RLL 支持

当你配置操作系统时，必须做好接受大量缩略词的准备——这一项就包含四个缩略词：ATA、ATAPI、MFM 和 RLL。这些都与硬盘或连接磁盘驱动器与 PC 的接口有关。它们的含义如下：

- **ATA** 代表 *AT Attachment*（AT 附加），指的是将硬盘和 CD-ROM 驱动器连接到 PC 主板的 PC-AT 风格接口。
- **ATAPI** 代表 *AT Attachment Packet Interface*（AT 附加包接口），指的是将磁盘控制器集成到硬盘本身的早期 PC 硬盘。这种接口过去被称为 *Integrated Drive Electronics*（集成驱动器电子设备）或 IDE。你通常看到 IDE、ATA 和 ATAPI 这些术语被互换使用。
- **MFM** 代表 *Modified Frequency Modulation*（调频制），这是旧硬盘上编码数据的方式。这些硬盘可以通过 IDE 接口工作。
- **RLL** 代表 *Run Length Limited*（有限长度运行），这是 PC 早期在硬盘上存储数据的一种技术。RLL 磁盘可以通过 IDE 接口工作。

点击 **ATA/ATAPI/MFM/RLL Support** 选项直到出现复选框，从而启用该选项。启用此支持后，你会获得许多涉及 IDE 设备（如硬盘和 ATAPI CD-ROM 驱动器）的更多配置选项（见图 6-4）。

第一个选项是 **enhanced IDE support**（增强型 IDE 支持），它指的是可以控制多达 10 个 IDE 接口的全功能 IDE 控制器。由于每个 IDE 接口可以有一个主设备和一个从设备，Linux 总共可以访问多达 20 个 IDE 设备（如磁盘或 CD-ROM 驱动器）。请确保此选项带有复选框。

![](img/9f89727199836b0f871f1745838aa8b2_531_0.png)

![](img/9f89727199836b0f871f1745838aa8b2_532_0.png)

图 6-4 右上角窗格中的第二项是一个注释，引导你参阅文件 `Documentation/ide.txt` 以获取有关 IDE 设备的帮助。要阅读这些帮助文件（它们都是文本文件），请输入以下命令以更改目录：

```
cd /usr/src/linux*/Documentation
```

现在你可以浏览与特定设备相关的文本文件。你还可以使用 GNOME 或 KDE 文件管理器来浏览文档。

> 注意：IDE/ATAPI FLOPPY Support 选项指的是 IDE 软驱，例如 Iomega Zip 驱动器或 Imation SuperDisk LS-120 驱动器。如果你有一个 IDE ZIP 驱动器，请启用此选项以显示复选框或圆点。

### SCSI 设备支持

SCSI 代表 Small Computer Systems Interface（小型计算机系统接口）——这是一种可以通过其将多个设备（如硬盘和扫描仪）连接到 PC 的接口类型。这组选项与 SCSI 设备有关。如果你的系统有 SCSI 适配器，请首先点击 **SCSI Support** 选项以显示一个圆点（这意味着构建了一个模块）。之后，你可以设置与连接到 SCSI 适配器的设备类型（磁盘、磁带、CD-ROM）相关的选项。最后，你必须查看 SCSI 低级驱动程序类别，并启用系统上特定 SCSI 适配器型号的支持。

### IEEE 1394 (FireWire) 支持

IEEE 1394 是一种用于将外设连接到 PC 的高速串行总线。Apple 将这种总线称为 FireWire；Sony 将其称为 i.LINK。IEEE 1394 与 USB 类似，但它可以以高达 400Mbps 的速率传输数据，这是较旧的 USB 1.1 版本数据速率的 30 多倍（请注意，USB 2.0 甚至更快；它可以以高达 480Mbps 的速率传输数据）。由于数据传输速率高，IEEE 1394 非常适合将高速外设（如数字音频和视频设备以及外部硬盘）连接到 PC。

你可以为 IEEE 1394 总线构建一个模块。目前，Linux 支持兼容 Texas Instruments PCILynx/PCILynx2 和 OHCI 芯片组的 IEEE 1394 芯片组。如果你的 PC 有 IEEE 1394 适配器，你可以通过这些选项构建必要的驱动程序。

![](img/9f89727199836b0f871f1745838aa8b2_532_1.png)

要了解有关在 Linux 中使用 IEEE 1394 外设的更多信息，请访问 IEEE 1394 for Linux 项目的网站 www.linux1394.org。

### I2O 设备支持

读作 *eye-two-oh*，I2O 指的是 Intelligent Input/Output（智能输入/输出）——一种独立于操作系统和被控设备的新设备驱动程序架构。I2O 的基本概念是将负责管理设备的部分与包含操作系统特定细节的部分分离开来（这被称为 I2O Split Driver 模型）。I2O 驱动程序的这两个部分是 OS Services Module (OSM)（操作系统服务模块），它与操作系统协同工作；以及 Hardware Device Module (HDM)（硬件设备模块），它与驱动程序管理的特定设备进行接口交互。OSM 和 HDM 通过互相传递消息进行通信。Linux 附带一些用于 SCSI 和 PCI 设备的 I2O 驱动程序。你可以从此类选项中配置这些驱动程序。

### 网络支持

这组选项（如图 6-5 所示）涉及网络。你如何设置这些选项取决于你希望在网络中如何使用 Fedora Core 系统。始终启用 **TCP/IP Networking**（TCP/IP 网络）选项，因为 X 窗口系统使用 TCP/IP 网络（即使你的 PC 不在任何网络上也是如此）。

![](img/9f89727199836b0f871f1745838aa8b2_533_0.png)

**图 6-5：** 从此类选项中配置网络选项。

如果你想将 Fedora Core 系统用作防火墙——一个控制局域网 (LAN) 和 Internet 之间信息流的中介系统——请将 **Network Packet Filtering**（网络数据包过滤）选项设置为复选框。

网络支持选项中的其他类别包括无线局域网、令牌环、广域网 (WAN)、PCMCIA 网络设备、业余无线电、红外线和蓝牙。

红外线支持用于使用由红外数据协会 (IrDA) 规定的协议进行红外通信。IrDA 通信被许多笔记本电脑和个人数字助理 (PDA) 使用，例如 Palm 和 Handspring。

蓝牙是一种低功耗、短距离无线技术，用于在 2.4 GHz 频段连接设备。使用蓝牙的设备通常可以在彼此 10 米范围内连接。要了解有关蓝牙的更多信息，请访问 www.bluetooth.com。Linux 通过核心驱动程序和几个其他模块支持蓝牙。你可以点击选项启用蓝牙支持，然后选择特定于你蓝牙设备的其他选项。

### ISDN 子系统

这组选项使你能够包含对 ISDN (Integrated Services Digital Network，综合业务数字网) 的支持——这是一种数字电话线，你可以用它将 Linux 系统连接到 Internet。这些与 ISDN 相关的选项包括特定 ISDN 适配器的配置。

仅当你的 PC 有 ISDN 卡时才构建 ISDN 驱动程序。如果你打算添加 ISDN 卡并从电话公司购买 ISDN 服务，你可以将驱动程序构建为模块。阅读文件 `/usr/src/linux-*/Documentation/isdn/README` 以获取更多有关如何在 Linux 中设置和使用 ISDN 驱动程序的信息。

### 电话支持

借助正确的硬件和软件，电话支持选项使你能够在 Fedora Core 系统上通过电话线进行 Internet 通话（也称为语音 over IP 或 VoIP）。如果你有电话卡，如 Quicknet Technologies, Inc. 制造的 Internet PhoneJACK 或 Internet LineJACK，你可以选择构建用于电话支持的驱动程序模块。如果你没有 Quicknet 电话卡，可以安全地关闭这些选项。

### 字符设备

这些选项涉及配置字符设备，包括连接到串行端口和并行端口的设备。这些选项还

