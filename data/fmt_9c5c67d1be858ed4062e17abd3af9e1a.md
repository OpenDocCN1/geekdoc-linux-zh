
# Linux 业务桌面迁移

> 作为安全措施，Knoppix 可启动 CD-ROM 以只读模式挂载主机上的硬盘。要访问这些硬盘，你必须让它们变得可读。你可以通过两种方式实现这一点。第一方法是右键点击硬盘，选择“属性”，并点击“权限”选项卡。另一种方法是在命令行界面使用 `chmod` 命令设置权限。`chmod` 命令可用于使硬盘可读。

你可以通过点击桌面上的硬盘图标并选择“属性”，然后是“权限”选项卡（如图 4.16 所示），将硬盘设置为可读和可写。

![](img/72e1c6125676a623b5032cfdab8d797c_108_0.png)

![](img/72e1c6125676a623b5032cfdab8d797c_109_0.png)

图 4.16 通过右键点击并选择“属性”更改硬盘属性

一旦硬盘被设置为可读可写，用户就可以在 Microsoft Office 的替代程序 OpenOffice 中编辑文档了。OpenOffice 套件提供了 Word (Writer)、Excel (Calc) 和 PowerPoint (Impress) 的对等软件。多种浏览器选择和磁盘工具可可用。使用 Knoppix 自带的分区工具，可以对硬盘进行重新分区，以适应原生 Linux 安装或仅隔离 Linux 数据存储。

## Windows PC 的重新利用或双用途

到此为止，关于使用 Knoppix 的讨论大多是在 Windows PC 双重用途或使用它来帮助修复特定的操作系统故障的背景下。以下方案设计不仅提供了双重用途场景，还提供了重新利用场景，允许 PC 回收利用或创建有助于学习企业级场景的项目。

## 为 Linux 优化现有 PC

如果你正在运行 Knoppix CD-ROM，你显然无法将该驱动器用于其他用途，如浏览数据 CD 或刻录 CD-R 媒体。然而，Knoppix 有一种变通方法允许你直接从硬盘运行 Knoppix，而不会干扰你现有的 Windows 安装。Knoppix 社区将这种方法戏称为“穷人的安装法”。如果你目前拥有有至少 700 MB 空闲磁盘空间的 PC，可以将 Knoppix CD-ROM 的镜像复制到你的硬盘上，提供一种启动 Knoppix 而不占用 CD 驱动器的方法。这种方法有几个考虑因素。

你安装 Knoppix 镜像的硬盘不应为 NTFS。它应该是 FAT32 或 Linux 可读可写的格式之一（ext2, ext3, ReiserFS）。如果你有一台 NTFS PC 且有可用空间，可以使用之前 GParted 工具修复硬盘，并创建一个有足够空间用于 Linux 启动镜像和额外设置的兼容分区。如果你在 PC 的其他部分使用 NTFS，可以为要保存的文档添加额外空间。

## 创建便携式桌面

设置持久性目录（home）涉及几个简单的步骤。在启动 Knoppix CD-ROM 时，你可以在启动提示符传递参数。在 USB 密钥的情况下，最可能的 USB 设备位置是 `/dev/sda1`。因此在启动提示符处，你应该输入 `knnoppix home=/dev/sda1`。如果失败，你可以选择启动你创建的持久性目录，尽管这可能需要更长的时间。现在，当你从 PC 移动到 PC 时，可以带上你需要的文件。这种设置也是在你知道将访问 PC 但不想干扰另一个用户的安装时的选择。

![](img/72e1c6125676a623b5032cfdab8d797c_112_0.png)

图 4.17 Knoppix 持久主目录对话框。

## 访问远程桌面和终端服务器

KDE 提供了一个名为远程桌面共享的工具，它也包含在 Knopp CD-ROM 中。使用此软件可以使用不同的显示协议连接到其他桌面。要启动远程桌面，进入 K 菜单 -> Internet -> 远程桌面。这将启动如图 4.18 所示的远程桌面软件。

![](img/72e1c6125676a623b5032cfdab8d797c_112_1.png)

图 4.18 KDE 远程桌面共享程序。

## 访问 Windows 终端服务器或 Windows 2000/2003 终端服务

Windows 终端服务使用名为远程桌面协议 (RDP) 的显示协议。你可以使用远程桌面软件来从 Linux 连接到你的 Windows 终端服务器。如果你已经或使用 Windows 终端服务（Terminal Services），这将非常有用；你可以继续在 Windows 服务器上托管你的应用程序，同时为自己提供一个安全的沙箱来尝试 Linux。

## 从 Knoppix 现场文件系统 CD-ROM 安装 Linux

Knoppix 安装脚本将尝试检测适用于安装 Linux 的分区。它将启动 QParted 来创建这些分区；然而，它可能不会以 root 用户身份启动 QParted 分区工具，因此它将没有创建分区的权限。如果是这种情况，你可以退出安装，进入终端窗口，并输入 `parted sudo qt <enter>` 开始安装。对于新安装，你将有选择 beginner（入门）、Knoppix 或 Debian 的选项。你可以选择安装带有硬件检测的多用户系统 beginner（入门）。

## 使用 NoMachine 和 Knoppix 构建薄客户端网络

NoMachine 是一个由 NoMachine 销售的开源软件包，NoMachine 是意大利系统集成商 Mediologic S.A. 的一个部门。NoMachine 使用 NX 分布式计算架构将 Unix 或在本例中为 Linux 计算机转换为终端服务器。NoMachine 架构通过三种方法的组合压缩 X 协议以使用更少的带宽：它使用算法来压缩网络流量；它缩短了往返传输的时间，并且能够根据任何时刻可用带宽进行适应。只有当 NoMachine 允许 Linux 会话被压缩和重放时，它可以作为 Windows 终端服务器和 Citrix MetaFrame® 的显示客户端。NoMachine 可以作为运行在你的 Windows PC 上的辅助桌面环境。

## 构建你自己的 LINUX 现场文件系统 CD-ROM 发行版

![](img/72e1c6125676a623b5032cfdab8d797c_113_0.png)

本章的解决方案侧重于使用随书提供的 Knoppix CD-ROM。不过，这应该激发你的创造力。构建你自己的 Linux 发行版对你可能是有利的，这样你可以选择包含用户所需的所有应用程序，并避免臃肿。以上述示例为切入点，你可以选择制作自己的工具 CD，其中包含针对你企业的特定文件。现场文件 CD-ROM 的重制并非易事，但其过程和方法在互联网上都有详细的记录。本章开头提到的 Morphix CD-ROM 设计用于想要创建发行版的终端用户能够构建自己的现场 Linux CD。

## 总结

正如本章示例所示，Linux 现场文件发行版提供了许多对你的 Windows 环境有影响的工具。它们还可以用于许多不同的项目，包括复活无法使用的 PC 或诊断问题。有许多不同类型的可启动发行版，旨在帮助特定人群解决某个特定问题或一组问题。受欢迎的 Linux Distrowatch 网站维护着一个关于桌面 Linux 发行版以及 Linux 现场文件 CD 发行版的动态新闻列表。

## 其他资源

- Distrowatch—www.distrowatch.com
- Morphix—www.morphix.org
- Gnoppix—www.gnoppix.org
- KDE—www.kde.org
- GNOME—www.gnome.org
- Linux Bootable Business Card—www.lnx-bcc.org
- Knoppix-STD—www.knoppix-std.org
- Knoppix—www.knoppix.org
- QtParted—http://qtparted.sourceforge.org
- Fresco—www.freesco.org
- LinNeighborhood—www.bnro.de/~schmidjo/
- Citrix—www.citrix.com
- NoMachine—www.nomachine.com
- rdesktop—www.rdesktop.org
- Distrowatch—www.distrowatch.com

## 参考文献

Windows 2000 Terminal Services. 在线地址：http://www.microsoft.com/windows2000/technologies/terminal/default.asp。

Windows 2003 Terminal Services. 在线地址：http://www.microsoft.com/windowserver2003/technologies/terminalservices/default.mspx。

# 5 Linux 桌面部署

在本章中

- 厚桌面或薄桌面部署
- 安装厚客户端 Linux 桌面
- 为你的硬盘一个快速启动
- 引导加载程序
- 登录
- 总结
- 其他资源
