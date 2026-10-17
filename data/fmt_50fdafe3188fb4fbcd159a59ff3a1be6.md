
![](img/1dca8e8a8784dadffa032dcfe0460e55_77_0.png)

OES Linux 包括两种安装选项，两者都在《OES for Linux 安装指南》中有记录：

- CD 安装。您可以使用从 Novell 授权经销商处获得的 CD 进行安装，也可以从下载的 ISO 镜像文件创建 CD。
- **网络安装。** 如果网络上可以使用剩余的 ISO 文件，则仅需第一张 CD 进行安装。

此选项可以避免您在安装过程中在服务器上更换 CD。

有关详细的说明说明，请参阅《OES Linux 安装指南》(install_linux.pdf) 第 23 页的“安装 Open Enterprise Server (OES Linux)”。

## OES NetWare 安装概述

下文概述了安装 OES NetWare 所需的软件和网络准备过程：

### 图 1-8

![](img/1dca8e8a8784dadffa032dcfe0460e55_79_0.png)

OES NetWare 包含两种安装方式，这两种方式在《OES for NetWare 安装指南》中均有介绍：

- **CD 安装。** 您可以使用从 Novell 授权经销商处获取的 CD 进行安装，也可以从下载的 ISO 镜像文件创建 CD。
- **网络安装。** 如果您已经准备好带有 Novell 客户端的 DOS 分区并将 CD 文件复制到网络，则可以从网络进行安装。

此选项可以避免您在安装过程中在服务器上更换 CD。

![](img/1dca8e8a8784dadffa032dcfe0460e55_80_0.png)

有关详细的安装说明，请参阅*OES NetWare 安装指南* (`install_nw.pdf`) 第 27 页的“安装 OES NetWare”。

## 尽可能使用预定义的服务器类型（模式）

两个 OES 平台都包含预定义的服务器安装选项，这些选项仅会安装提供特定组网络服务所需的组件。

在 OES Linux 安装中，这些安装选项被称为*服务器类型* (`server types`)；在 OES NetWare 安装中，这些安装选项被称为*模式* (`patterns`)。

例如，如果您想安装一个支持基于 Web 的、用户可配置的协作环境的 OES 服务器，应该在 OES 安装期间选择 Virtual Office 服务器类型。

如果某个预定义的服务器类型符合您的服务器预期用途，您应始终选择该预定义类型。如果不符合，您可以选择安装带有您所需服务组件的自定义 OES 服务器。

OES Linux 安装中提供以下服务器类型：

### 表 1-7 预定义服务器类型描述及安装包

| 预定义服务器类型 | 描述及安装的包 |
| :--- | :--- |
| Novell QuickFinder Server | 安装一个允许用户在 Web 站点和附加文件系统中查找所需信息的服务器。不安装 KDE。 |
| Novell iFolder2 Server | 安装一个允许移动用户随时随地（在线、离线）访问其本地文件的服务器。不安装 KDE。 |
| Novell Virtual Office Server | 安装一种协作解决方案，让用户在 IT 需求上自给自足。不安装 KDE。 |
| Novell Management Server | 安装 iManager、YaST（文本界面）和基础运行时系统。不安装 KDE 和图形基础系统。 |
| Novell Print Server | 安装打印系统，安装工作站打印机驱动程序并提供对本地打印机和具有连接连接远程打印机的访问。不安装 KDE。 |
| Novell Open Enterprise Server | 默认服务器模式安装 SLES 9 默认安装和大多数 OES 服务。安装 KDE。 |

OES NetWare 安装中提供以下模式：

### 表 1-8

| 服务器模式 | 描述 |
| :--- | :--- |
| Customized NetWare Server | 允许您在服务器上选择所需的可选产品。 |
| Basic NetWare File Server | 仅安装基础 NetWare，不含额外产品。 |
| Pre-Migration Server | 创建一个可以使用 NetWare 迁移向导在以后迁移的服务器。 |
| DNS/DHCP Server | 为目录启用 DNS/DHCP 服务设置 Novell eDirectory 树。 |
| extND J2EE Web Application Server | 安装优化的 Novell extND Web 服务器。 |
| LDAP Server | 为 Novell eDirectory 安装轻量级目录访问协议 (LDAP)。 |
| NetWare AMP (Apache, MySQL, PHP, and Perl) | 允许在 NetWare 6.5 服务器上托管开源 Web 应用程序。 |
| NetWare Backup Server | 在 NetWare 平台上安装备份和恢复服务的基础设施。 |
| QuickFinder Server | 安装搜索服务器，允许用户在 Web 站点和附加文件系统中查找所需信息。 |
| Network Attached Storage (NAS) Server | 为您的网络安装多文件协议存储。 |
| Novell iPrint Server | 安装打印系统，安装工作站打印机驱动程序并提供对本地打印机和具有连接连接远程打印机的访问。 |
| **服务器模式** | **描述** |
| :--- | :--- |
| Apache/Tomcat Server | 安装 Apache Web 服务器和 Jakarta-Tomcat Servlet 容器，用于托管动态的应用驱动型 Web 站点。 |
| Novell Nsure Audit Starter Pack Server | 安装内置于 OES NetWare 的集中审计服务。 |
| iSCSI SAN Storage Server | 将您的 OES NetWare 服务器转换为 iSCSI 存储服务器（也称为 iSCSI Target）。 |
| Novell iFolder Storage Services | 安装一个允许移动用户随时随地（在线）访问本地文件的服务器。 |
| Management Server | 安装 Novell iManager 2.5 和 Novell ConsoleOne 1.3.6 网络管理软件。 |
| Virtual Office Server | 安装一种协作解决方案，让用户在 IT 需求上自给自足。 |

## 如果您想在单分区上安装 NSS

许多管理员对在 Linux 上运行的 Novell Storage Services (NSS) 感感兴趣。

如果您计划在单分区上使用 NSS，请务必参考《OES Linux 安装指南》第 17 页的“安装 Linux”。

## 购买并许可 OES

作为实施 OES 计划的一部分，您需要了解有关购买和许可 OES 的信息：

- 如何通过升级保护获取 OES
- 如何购买 OES
- Novell 许可

### 如何通过升级保护获取 OES

如果您拥有升级保护，可以免费升级到 OES 及最新支持包。

要获取更多信息并启动升级过程，请执行以下操作：

1. 使用您的 Novell 账户登录 Novell 网站 (`http://www.novell.com/nps`)。
2. 选择 Care 图标进入 Customer Care 页面。
3. 按照 Customer Care 页面上的说明获取升级。

### 如何购买 OES

如果您决定购买 OES，请访问 Novell 购买 OES 页面 `http://www.novell.com/products/openentererver/howbuy.html`。

购买 OES 后将获得：

- 用于启用 OES 服务器接收在线更新（包括最新支持包）的激活码。
- 用于安装 OES NetWare 的许可证文件。

购买 OES 后，可以在 Novell 支持网站 `http://support.novell.com/filefinder` 上免费获取 OES NetWare 支持包。

作为购买过程的一部分，了解 1-48 页“Novell OES 许可”下的内容非常重要。

## Novell OES 许可

要了解 OES 许可，您需要知道以下：

- OES 许可模型
- OES NetWare 许可
- OES Linux 许可

联系您的 Novell 客户经理或合作伙伴，或访问 `www.novell.com/oes` 获取详细定价信息。适用某些限制和条款。

### OES 许可模型

所有 OES 许可都是基于用户连接购买的。每个平台授权安装的服务器数量不同如下：

- **OES NetWare 服务器。** 唯一的许可限制是网络上的用户连接数。

您可以安装任意数量的 OES NetWare 服务器为这些用户提供服务。
