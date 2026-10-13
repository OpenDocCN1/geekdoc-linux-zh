
![](img/9139201cfcaf4292284a0eed074928e5_822_0.png)

## 15

## Samba 文件服务器

## 认证目标

- 15.01 Samba 服务
- 15.02 Samba 作为客户端
- 15.03 Samba 故障排除

- ✓ 两分钟速览
- 问答自测

Samba 是用于连接 Microsoft 操作系统的网络协议在 Linux 上的实现。Microsoft 网络基于通用 Internet 文件系统 (CIFS)，它源自服务器消息块 (SMB) 协议。Samba 最初作为适用于所有 Unix 相关操作系统（包括 Linux）的自由可用的 SMB 服务器开发，并已升级以支持 CIFS。

Samba 与 CIFS 的交互如此透明，以至于 Microsoft 客户端无法区分您的 Linux 服务器和真正的 Windows Server，而且在 Linux 上使用 Samba 无需购买服务器、客户端或客户端访问许可证。如果您能学会从命令行界面编辑 Samba 的主配置文件，就能快速配置 Samba。在其可选存储库中，RHEL 6 包含一个 GUI 配置工具——Samba Web 管理工具。

学习测试 Samba 等网络服务。这些是在 Red Hat 考试中您可能需要配置和/或排除故障的服务。花一些时间了解与这些服务相关的配置文件，并在不同的 Linux 系统上练习使其正常工作。在某些情况下，使用两个或多个运行 Linux 的系统来练习本章所学内容会很有用。

## 考试内部

本章直接涉及与 Samba 文件系统服务相关的两个 RHCE 目标。完成本章后，您将知道如何

- 为特定客户端提供网络共享
- 提供适合组协作的网络共享

使用 Samba，与 Microsoft 客户端的通信是无缝的。但由于在 Red Hat 考试期间您无法使用 Microsoft Windows，您将看到 Samba 与其他 Linux 客户端的通信也是无缝的。

Samba 可以与其他安全选项一起将共享限制为特定客户端。

Samba 还提供组协作支持，正如第 14 章中的 Apache 所做的一样。其原理与第 8 章中 Linux 上组目录的配置方式相同。

当然，您不能忘记第 10 章和第 11 章中讨论的所有网络服务的标准要求。回顾一下，您需要安装服务，使其与 SELinux 协同工作，确保它在启动时启动，配置服务以实现基本操作，并设置基于用户和基于主机的安全。

## 认证目标 15.01

## Samba 服务

Microsoft 的 CIFS 建立在服务器消息块 (SMB) 协议之上。SMB 由 IBM、Microsoft 和 Intel 在 1980 年代开发，用于在网络上共享文件和打印机。

随着 Microsoft 将 SMB 发展为 CIFS，Samba 开发者也相应升级了 Samba。Samba 服务提供稳定、可靠、快速且高度兼容的文件和打印共享服务，使您的计算机能够充当 Microsoft 网络上的客户端、成员服务器、主域控制器 (PDC) 或 Active Directory (AD) 服务的成员。虽然 Samba 不包含最新 Microsoft 网络构建的每个功能，但我相信在不久的将来会实现。

> 我期待 Samba 4.0 的最终发布，这将使 Linux 能够充当基于 Microsoft 的网络上的 AD 控制器。RHEL 6 包含 Samba 4.0 的初步版本，并在 RHEL 6 的生命周期内可能包含它。

在基于 Microsoft 的网络上，SMB 网络通信也称为通过 TCP/IP 的网络基本输入/输出系统 (NetBIOS)。通过 Andrew Tridgell 和 Samba 团队的集体工作，Linux 系统通过名为 Samba 的软件包在 TCP/IP 上提供透明可靠的 SMB 支持。

Samba 通过 SMB 协议模拟与各种 Microsoft 操作系统相关的许多高级网络特性和功能。完整信息可在官方 Samba 网站 www.samba.org 上找到。配置 Samba 在基于 Microsoft 的网络上执行多项操作很容易。以下是一些示例：

- 以客户端、成员服务器甚至 PDC 的身份参与 Microsoft Windows 工作组或域。
- 共享用户主目录。
- 充当 Windows Internet 名称服务 (WINS) 客户端或服务器。
- 链接或管理工作组浏览服务。
- 充当主浏览服务器。

![](img/9139201cfcaf4292284a0eed074928e5_824_0.png)

- 在本地、另一台 Samba 服务器或 Microsoft NT 4 PDC 上提供用户/密码和共享安全数据库。
- 将本地目录配置为共享 SMB 文件系统。
- 在 Windows 和 Linux 系统之间同步密码。
- 支持 Microsoft 访问控制列表。

Samba 还能做更多，但你明白了。Samba 功能通过 /etc/samba 目录中的一个非常大的文件 smb.conf 进行配置。由于该文件可能令一些用户望而生畏，Samba Web 管理工具 (SWAT) 提供了 GUI 界面。

> **考试提示**
> 研究 /etc/samba/smb.conf 配置文件。它包含许多有用的注释和建议的指令。
> 
> 如果使用 SWAT，请先备份 Samba 配置文件，因为它会覆盖默认注释和指令。

## 安装 Samba 服务

Samba 服务和软件包的安装与其他服务器有所不同。Samba 软件包未组织在单个软件包组中。虽然存在“CIFS 文件服务器”软件包组，但该组仅包含 samba RPM 软件包。虽然这是设置 Samba 服务器所需的唯一软件包，但您可能会发现其他 Samba 软件包有用。重要的 Samba 软件包在表 15-1 中描述。

## Samba 背景简介

Samba 服务在 Microsoft Windows 与 Linux/Unix 计算机之间提供互操作性。在配置 Samba 之前，您需要基本了解 Microsoft Windows 网络如何与 TCP/IP 协同工作。

最初的 Microsoft Windows 网络使用计算机主机名进行配置，称为 NetBIOS 名称，限制为 15 个字符。这些唯一的主机名为局域网上的计算机提供了一个简单、扁平的主机名系统。所有计算机识别请求都通过广播进行。这种整体网络传输系统称为 NetBIOS 扩展用户界面 (NetBEUI)，它不可“路由”。换句话说，它不允许两个不同的局域网之间通信。因此，最初基于 Microsoft 的 PC 网络规模限制为 255 个节点。

**表 15-1 Samba 软件包**

| RPM Package | Description |
|---|---|
| samba | 包含用于共享文件和打印机的基本 SMB 服务器软件。 |
| samba-client | 提供从 Samba 和 Microsoft 服务器连接共享所需的实用程序。 |
| samba-common | 包含客户端和服务器都使用的通用 Samba 命令。 |
| samba-doc | 包含 HTML 和 PDF 格式的 Samba 文档。 |
| samba-domainjoin-gui | 支持连接到网络工作组和域。 |
| samba-swat | 提供 Samba 配置的基于 Web 的界面。 |
| samba-winbind | 支持 Samba 作为基于 Microsoft 的域上的成员服务器，并支持 Linux 服务器上的 Windows 用户。 |
| samba-winbind-nss | 通过 PAM 和网络切换服务 (NSS) 提供到 Winbind 的客户端连接。 |

虽然 Microsoft 网络可以使用 Novell IPX/SPX 协议栈在网络之间路由消息，但这还不够好。随着互联网的增长，TCP/IP 的主导地位也随之增强。Microsoft 将其 NetBIOS 系统通过 SMB 适配到 TCP/IP。由于 Microsoft 将 SMB 发布为行业标准，任何人都可以设置自己的服务来与 SMB 协同工作。随着 Microsoft 转向 CIFS，Samba 开发者也很好地适应了。但一些相当近期的变化影响了配置文件以及主要的命令行客户端挂载命令。

Windows 网络的一个不错特性是浏览器服务。所有计算机都将其 NetBIOS 名称注册到一个“选举产生”的主浏览服务器，该服务器保存网络范围服务的数据库。事实上，对于网络上运行的每个协议，都会由某个选举产生的主机维护一个浏览数据库。例如，如果在主机上安装了 NetBEUI、IPX/SPX 和 TCP/IP 协议，则需要三个重复的浏览数据库——每个协议一个——因为不同协议可用的服务可能不同。

## 端口、防火墙与 Samba

Samba 作为服务和客户端需要通过多个网络协议访问。当通过以下方式启用 Samba 客户端和服务器之间的通信时
