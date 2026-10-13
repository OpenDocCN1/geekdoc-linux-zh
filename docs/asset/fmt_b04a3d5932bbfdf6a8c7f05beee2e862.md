
点击“继续”按钮。然后你可以在“设备”页面中选择打印机访问类型（本地、远程、串行端口或 Internet），如图 21.14 所示。例如，要配置打印到本地打印机，请选择“并行端口 #1”；对于远程打印机，请选择“LPD/LPR 主机或打印机”条目。

![](img/774d40fd20903495c5cd00e2efad3f33_643_0.png)

**图 21.13** 使用 CUPS 创建新的打印队列。

再次点击“继续”，并按照图 21.15 所示的对话框要求选择打印机制造商。

![](img/774d40fd20903495c5cd00e2efad3f33_644_0.png)

**管理**

- DYMO

- EPSON

- Gnutext

- HP LaserJet 1010

- OLIVETTI

- Pictorica

- Zebra

- System...

图 21.14 在 CUPS 管理页面中选择打印机设备。

![](img/774d40fd20903495c5cd00e2efad3f33_644_1.png)

**打印机**

- `/usr/bin/lpd/10501-Local-Spooler/accepting/newspaper`

    - 使用 `system-configuration` 编辑此项

    - 位置：Local: 2160

    - 打印机全双工；接受任务；设备 URI（spooler:/dev/lp）

    - Fast-Text-Queue Default-Queue Default-Size Default-Pitch Copy-Options Duplex-Printing Job-Attributes Set-Up-Options

- `/usr/bin/lpd/10501-Remote/accepting/brother-2040`

    - 使用 `system-configuration` 编辑此项

    - 位置：

    - 打印机名称：bdc-accepting jobs;

    - 设备 URI：socket://brother:

    - Fast-Text-Queue Default-Queue Default-Size Default-Pitch Copy-Options Duplex-Printing Job-Attributes Set-Up-Options

图 21.15 在创建新队列时选择打印机制造商。

点击“继续”后，你将选择驱动程序。创建打印机后，你可以使用“打印机”页面（如图 21.16 所示）来打印测试页、停止打印服务、管理本地打印队列、修改打印机条目或添加另一台打印机。

![](img/774d40fd20903495c5cd00e2efad3f33_645_0.png)

**图 21.16** 使用 CUPS 打印机页面轻松管理打印机。

CUPS 提供许多其他功能，一旦安装、配置并运行，就可以为 Fedora 提供透明的传统 Unix 打印支持。

> **注意**
>
> 要了解有关 CUPS 的更多信息并获取系统的基本概述，请访问 http://www.cups.org/。

## 避免打印机支持问题

排查打印机问题可能会令人沮丧，尤其是当你发现新打印机无法在 Linux 上正常工作时。首先，请记住目前市场上几乎所有打印机都能与 Linux 协同工作。然而，某些厂商在支持 Linux 方面表现更好。如果你想知道评分表，请访问 http://www.linuxprinting.org/vendors.html。

### 多功能一体机（打印/传真/扫描设备）

有问题的打印机，或者可能也可能无法与 Fedora 协同工作的打印设备，包括多功能（或*一体式*）打印机，这些打印机结合了扫描、传真和打印服务。你应该调查任何计划购买的设备，并避免任何不愿通过驱动程序或开发信息支持 Linux 的厂商。

在 Linux 对多功能打印机的支持领域中，HP 对 HP OfficeJet Linux 驱动程序项目的支持是一个亮点，请访问 http://hpoj.sourceforge.net/。许多型号支持打印和扫描，传真支持正在开发中。

## 使用 USB 和传统打印机

由于缺乏打印机的 USB 厂商和设备 ID 信息，还可能会引发其他问题——这在 Linux 下的一些 USB 扫描仪中也存在同样的问题。关于 USB 打印机支持的信息，你可以查阅 Linux 打印团队（本节开头的 URL）或位于 http://www.linux-usb.org 的 Linux USB 项目。

尽管许多较新的打印机需要通用串行总线（USB），但 Linux 仍然对传统的并行端口（IEEE-1284）打印机提供了极佳的支持，使网站能够继续使用旧硬件。即使主机计算机没有传统的并行打印机端口，或者你想在较旧的计算机上使用较新的 USB 打印机，你也可以利用 Linux 的变通办法来设置打印。

例如，要在仅支持 USB 的计算机上托管基于并行端口的打印机，可以使用廉价的 USB 转并行转换器将打印机连接到计算机。USB 转并行转换器通常提供 Centronics 连接器；该连接器的一端插入旧打印机，另一端插入 USB 连接器。然后，该 USB 连接器插入你的集线器、台式机或笔记本电脑的 USB 端口。另一方面，如果旧计算机没有内置 USB，你可以使用附加 PCI 卡来添加 USB 支持，用于打印（以及其他设备）。大多数 PCI USB 接口卡至少添加两个端口，并且可以通过集线器链式连接设备。

### 相关的 Fedora 和 Linux 命令

以下命令帮助你管理打印服务：

- `accept`—通过命令行控制对 CUPS 服务器的打印任务访问

- `cancel`—从命令行取消打印任务

- `disable`—从命令行控制打印

- `enable`—控制 CUPS 打印机

- `lp`—将指定文件发送到打印机并允许控制打印服务

- `lpc`—在控制台显示打印机和打印服务状态

- `lpq`—在控制台查看打印队列（待处理的打印任务）

- `lprm`—通过命令行从打印队列中移除打印任务

- `lpstat`—显示打印机和服务器状态

- `system-config-printer`—显示 Fedora 的图形化打印机配置工具

- `system-config-printer-tui`—显示 Fedora 的文本对话框打印机配置工具

## 参考资料

- http://www.linuxprinting.org/—在此处浏览特定驱动程序以及有关 USB 和其他类型打印机的信息。

- http://www.hp.com/wwsolutions/linux/products/printing_imaging/index.html—来自 HP 的简短但权威的信息，关于在 Linux 下的打印产品支持。

- http://www.linuxdoc.org/HOWTO/Printing-HOWTO/—Grant Taylor 的打印 HOWTO，包含有关在 Linux 下使用各种打印服务的信息。

- http://www.cups.org/—CUPS 软件的综合存储库，包括 Red Hat Linux 的版本。

- http://www.pwg.org/ipp/—Internet 打印协议标准的首页。

- http://www.linuxprinting.org/cups-doc.html—有关 CUPS 的信息。

- http://www.cs.wisc.edu/~ghost/—Ghostscript 解释器的首页。

- http://www.samba.org/—获取有关 Samba 的更多信息以及在 Linux、Unix、Mac OS 和其他操作系统上使用 SMB 协议的基本入口点。

此外，一本优秀的关于 Samba 的书籍可以帮助你了解更多信息，即 *Samba Unleashed*（Sams Publishing，ISBN: 0-672-31862-8）。

# 第 22 章

# 使用 FTP 提供远程文件服务

文件传输协议（FTP）曾被视为通过网络在计算机之间传输文件的主要方法。尽管现在许多图形化 FTP 客户端都补充了原始的基于文本的界面命令，但 FTP 今天仍被广泛使用。随着计算机的发展，FTP 也随之演进，Fedora Core 提供了许多使用图形界面通过 FTP 传输文件的方式。

本章概述了 Fedora 包含的可用 FTP 软件，并简要介绍了初始设置、配置以及使用特定于 FTP 的客户端的细节。Fedora 还包含一个名为 `vsftpd`（非常安全的 FTP 守护进程）的 FTP 服务器软件包，以及一系列你可以用来提供和传输文件的 FTP 协议相关程序。

以下各节概述了如何使用 FTP 客户端，以及 how to install and configure the `vsftpd` FTP server（如何安装和配置 `vsftpd` FTP 服务器）。

## 本章内容

- 使用 FTP 客户端

- FTP 服务器

- 安装 FTP 软件

- FTP 用户

- `wu-ftpd` 的 `xinetd` 配置

- 配置非常安全的 FTP 服务器
