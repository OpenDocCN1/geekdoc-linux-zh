
你还需要 LDAP 服务器的名称或 IP 地址。除非你的网络中有可靠的 DNS 服务，否则你应该指定该服务器的 IP 地址。

此工具会自动对相应的配置文件进行所需的更改，正如本章介绍所示。

## 总结

网络信息服务 (NIS) 与 Linux 和 Unix 计算机共享配置文件。轻量级目录访问协议 (LDAP) 也可以做到这一点。

例如，你可以使用 NIS 将 `/etc/passwd` 和 `/etc/groups` 从服务器转换为单个共享数据库，从而创建一个用户名和密码的数据库。你需要在 `/var/yp/Makefile` 中定义 NIS 域名和共享文件。一旦你的 Makefile 准备就绪，可以使用 `ypint` 将其转换为数据库；可以在 `/var/yp` 目录下使用 `make` 命令处理更改。从服务器也可以通过 `ypbind` 配置并使用 `yresfresh` 进行刷新。

配置 NIS 客户端相对容易；只需使用 `ypbind` 将其绑定到相应的服务器即可。或者，一旦连接成功，NIS 客户端命令可以让你遍历可用数据库。最后，配置恰当的 `/etc/nsswitch.conf` 将你的 NIS 客户端计算机指向 NIS 服务器上适当的数据库。

配置 LDAP 服务器需要三个 openldap 和 nss_ldap RPM 包。你可以使用 `/etc/openldap/slapd.conf` 文件配置 LDAP 服务器。配置完成后，你可以启动 LDAP 服务器，然后以 LDIF 格式添加组织和用户数据。你还可以使用 `/usr/share/openldap/migration` 目录中的脚本将数据从 `/etc/passwd` 等标准配置文件传输到你的 LDAP 服务器数据库。除非数据库保持一致且你使用了适当的 `slap*` 命令，否则你可能会在此过程中遇到困难。

当你配置 LDAP 客户端时，你需要修改 `/etc/ldap.conf` 文件指向相应的 LDAP 服务器，并修改 `/etc/nsswitch.conf` 文件从 LDAP 查找基本信息。

最后，你可以使用 Red Hat 身份验证配置工具将你的 Linux 计算机设置为 NIS 或 LDAP 服务器的客户端。

在下一章中，我们将研究 Samba，它允许你与 Linux、Unix 和 Microsoft Windows 计算机共享文件和目录。

# 第 24 章 让 Samba 为你工作

## 通过 SAMBA，你可以

让你的 Linux 计算机成为微软网络的一部分。在本章中，你将学习如何在 Microsoft Windows 计算机网络上将 Samba 配置为客户端和服务器。

运行各种 Microsoft 操作系统的计算机可以使用服务器消息块 (SMB) 协议相互通信。当 Microsoft 操作系统在 TCP/IP 网络上共享文件或打印机时，Samba 就是一个与 SMB 和 CIFS 通信的 Linux 计算机。

Samba 是一种异构服务。一旦你配置了 Samba，其他 Windows 计算机将无法区分。就像第 20 章的 CUPS 一样，Samba 包含了自己的基于 Web 的配置工具 SWAT，即 Samba Web 管理工具。

你可以使用 Samba 包将你的 Linux 计算机配置为服务器，然后连接到共享目录和打印机，就像在一个类似于基于文本的 FTP 连接的终端中。

主要的 Samba 配置文件是 `/etc/samba/samba.conf`。许多 Linux 管理员直接在文本编辑器中配置它，你也可以学习如何在你的 Linux 计算机对目录和打印机进行相同的操作。测试和排错你对 `samba.conf` 所做的更改非常容易。

你可以配置 Samba 账户。如果 Windows 和 Linux 用户名相同，你可以在 `/etc/samba/smbpasswd` 中配置账户。如果用户的账户和 Windows 账户上的用户名不同，你可以在 `/etc/samba/smbsusers` 中建立关系。如果你正在设置 Microsoft 风格的域，还可以在 Samba 服务器上配置所需的计算机帐户。

Red Hat 有它自己的 Samba GUI 配置工具，被称为 Red Hat 服务器配置工具。虽然 Red Hat 没有在安装光盘中包含发行版的 SWAT，但可以通过 Red Hat Network 获取此包。Red Hat 的 Samba 服务器配置工具可以帮助你配置 Samba 和共享目录的基础设置。本章涵盖以下主题：

- 弥接 Linux 与 Microsoft Windows 之间的差距
- 将 Samba 配置为客户端

## 弥接 Linux 与 Microsoft Windows 之间的差距

- 理解 Samba 配置文件
- 管理 Samba 用户和计算机
- 使用 SWAT
- 使用 Red Hat Samba 服务器配置工具

作为一种异构服务，Samba 弥接了 Linux 和 Microsoft Windows 之间的差距——这本质意味着它可以与任何操作系统同等通信。事实上，你可以让 Samba 以像 Windows 网络中任何其他成员一样共享目录和打印机。

## 在 Microsoft 网络上运行

Samba 的优势之一是它允许你将 Linux 配置为微软网络的一部分。当你的配置完成后，它可以看起来像以下类型之一：

- Microsoft Windows 成员
- 域成员
- Microsoft Windows 2000/2003
- 主域控制器 (PDC)
- 备用域控制器 (BDC)

Samba 最初基于基于 TCP/IP 的 NetBIOS；有关 NetBIOS 和 WEBUI 的更多信息，请参阅第 15 章。

## 许可

不要让本节的标题让你恐慌。Samba 根据 GPL 许可并作为 Red Hat Enterprise Linux 的一部分免费提供。你不需要为使用任何 Microsoft 许可付费。

## 弥接 LINUX 与 MICROSOFT WINDOWS 之间的差距

注意 Samba 与下一个 Microsoft 操作系统发布版本（代号为 London）之间的兼容性可能会出现延迟。Microsoft 拥有了许多与 WinFS 相关的专利。然而，开源社区的人们根据定义，他们擅长进行“反向工程”。我不怀疑带有 Samba 的 Linux 很快就能与 WinFS 工作。

## 定义

本章包含了一些 Samba 专有的或与网络更密切相关的术语：

- **主域控制器 (PDC)**：拥有用户名和密码中心数据库的计算机。它还包含 Windows 登录配置的中心数据库。
- **备用域控制器 (BDC)**：此计算机从 PDC 获取信息。PDC 和 BDC 是 Windows 概念。
- **浏览列表 (Browse list)**：网络上共享资源的列表。
- **活动目录 (Active Directory)**：与 Windows 2000/2003 关联的目录服务。
- **浏览主 (Browse master)**：负责维护网络浏览列表的计算机。
- **域 (Domain)**：具有用户名和密码中心数据库的网络。这个概念与互联网域网络不同。
- **成员服务器 (Member server)**：Windows 网络上共享目录和打印机但不是 PDC 或 BDC 的任何计算机。
- **对等网络 (Peer-to-peer)**：局域网上一组计算机，每台计算机都可以作为服务器；通常与工作组相关。
- **服务器 (Server)**：共享目录或打印机的计算机。
- **共享 (Share)**：网络上共享的任何目录或打印机。
- **工作组 (Workgroup)**：没有专用服务器的局域网。每台计算机负责自己的用户名和密码；每台计算机通常与局域网的其他部分共享目录和打印机。

> 本章中，网络微软服务器是指任何共享目录或打印机的 Microsoft 操作系统。也可以是指 Linux 计算机上的 Samba 服务器。

## 软件包

Red Hat Enterprise Linux 上与 Samba 有五个基本包。将你的计算机配置为 Microsoft 客户端只需要 `samba-client-*` 和 `samba-common-*`。其他包帮助你将计算机配置为微软型网络上的服务器。这些软件包如表 24.1 所示。

# 第 24 章 让 Samba 为你服务

## 表格 24.1：Samba RPM 软件包

| 软件包 | 描述 |
| --- | --- |
| samba-* | 基础 Samba 服务器软件包，包含了用于匹配 Linux 和微软用户名及密码的命令。 |
| samba-client-* | 此软件包允许你设置 Linux 计算机以读取共享的微软目录并打印到共享的微软打印机上。 |
| samba-common-* | 此软件包包含支持 Linux 作为 Samba 客户端和 Samba 服务器的文件。 |
| samba-swat-* | 此 GUI 工具允许你修改 Samba 配置文件，特别是 sm.conf；如果你不需要精粒度的控制，可以考虑使用 redhat-samba 作为替代方案。这在 Red Hat 企业级 Linux 的 CD 中是不可用的，但可以通过 Red Hat Network 和 “rebuild” 站点下载。 |
| redhat-config-samba-* | 这是 samba-swat 的替代方案；它更简单但不够成熟，允许的配置控制较少。 |

> Red Hat 在其企业 CD 中不包含 samba-swat，在本书时，它可以作为个人身份通过 Red Hat Network 企业通道获取。这需要 Red Hat Network 的官方订阅。如果你正在使用其中一个 “rebuilds”，你可能需要在相应的下载服务器上搜索不同的目录，以通过 Extras 或 Addons 的形式找到 samba-swat RPM。

## 将 Samba 配置为客户端

通过 `samba-client-*` 和 `samba-common-*` RPM 软件包，你可以看到从微软计算机共享的目录和打印机。你有两种基本方式连接到共享目录：将共享的 Windows 目录挂载到本地 Linux 目录，以及在终端模式下连接共享目录，就像连接 FTP 服务器一样。此外，你还需要知道如何连接微软计算机的共享打印机。

## 共享 Samba 目录

从微软服务器连接到共享目录很容易。如图 24.1 所示，你只需要 `smclient` 命令以及服务器的名称或 IP 地址。该命令略显特殊；请注意与 `smclient` 命令相关的反斜杠。

这里有很多有趣的共享。如果微软服务器上设置了适当的权限，你几乎像挂载 NFS 目录一样挂载这些共享目录。区别是细微的。例如，如果你是 root 用户，可以使用以下将将 allaccess 的计算机共享的 Downloads 目录挂载到本地目录 `/root/downloads`。Linux 会请求密码。
