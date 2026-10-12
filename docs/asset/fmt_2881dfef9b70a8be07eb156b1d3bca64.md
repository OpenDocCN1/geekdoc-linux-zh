
图 12. 卸载 Apache 及其依赖项。

有一个简单的解决方案。如图 12 所示，你可以使用相同的命令同时卸载两个包。对于图 11 所示的配置，我重复了此命令来卸载 DNS (`bind`)、`sendmail`、`lrda-utils` 和 `isdn4k-utils` RPM 软件包。你可以对你选择的 RPM 软件包重复此命令。

### 停用服务

如果你计划将来使用某项服务，可以停用它而不是卸载它。黑客无法进入停用的服务。因为这本书是为转向 Linux 的微软 Windows 管理员编写的，所以从 GUI 开始，此处使用“服务配置”工具。点击“主菜单 | 系统设置 | 服务器服务”启动它，这将打开图 13 所示的服务配置窗口。

如图所示，Apache 正在运行，并设置为下次启动计算机时启动。如果你想停用 Apache，需要采取以下步骤：

1. 选中该服务并点击“停止”。
2. 取消勾选该服务。这将确保它在下次启动时不会运行。
3. 如果你做了更改，请务必保存。
4. 对关键运行级别重复此过程。

## 第3章：设置你的服务器文件系统 59

在第 2 章中，我向你展示了如何在 Linux 电脑上安装 Samba。使用 Samba，你可以让 Linux 看起来像基于 Microsoft Windows 的网络中的计算机。在本章中，你将学习如何在 Linux 电脑上设置 Samba。我将向你展示需要配置哪些内容，以便使带有 Samba 的 Linux 可以在基于 Microsoft Windows 的网络中作为成员服务器或主域控制器（PDC）运行。

Linux 和 Unix 计算机可以相互共享文件和打印机。Microsoft Windows 计算机也可以相互共享文件和打印机。遗憾的是，每个操作系统原生的网络文件系统是不兼容的。这就是 Samba 存在的本质原因，它允许 Linux 计算机理解 Microsoft Windows 网络文件系统的语言。

本章重点关注于将 Linux 系统配置为 Microsoft 网络上的文件和打印机服务器的细节。由于文件系统不同，我在本章开头首先回顾了 Microsoft Windows 计算机之间网络的基础，以定义工作组（Workgroups）和域（Domains）的不同概念。

或者，你也可以使用 Microsoft Unix 服务（Microsoft Services for Unix）在 Linux 和 Unix 计算机网络上设置 32 位的 Microsoft Windows 操作系统。遗憾的是，这项 Microsoft 服务不支持 Windows 9XE 计算机。本章还涵盖了一些基础知识。我将解释与 Samba 相关的基本服务，以及 Linux 中如何组织用户和用户组。

Samba 包含了许多配置文件。你也将学习如何配置它们。配置 Samba 最简单的方法是使用 Red Hat 的 Samba 服务器配置工具，我口语中称之为 Samba 服务器配置，遗憾的是，它无法让你充分利用 Samba 在 Microsoft 网络上的所有功能。Samba 网页管理工具（SWAT）可以为你提供帮助，但它既冗长又复杂。最后，你可以编辑 Samba 主配置文件 `smb.conf`。

最后，我将详细介绍 Samba 如何通过其主配置文件 `smb.conf` 运行的细节，以及关于如何让你的 Linux 电脑在工作组或域中看起来像 Microsoft Windows 服务器的建议。通过 Samba，你还可以将 Linux 电脑转换为 Windows 内部命名服务（WINS）服务器和域主浏览器。我将向你展示如何直接编辑 `smb.conf` 来配置共享目录和打印机。

本节中的大多数命令都需要使用 Linux 管理账户 `root`。如果你是以普通用户身份登录的（你应该这样做），你可以通过以下命令获取 `root` 用户访问权限：

### Microsoft CIFS

简而言之，Microsoft Windows 通用互联网文件系统（CIFS）描述了 Windows 网络如何通过 TCP/IP 网络进行通信。虽然它完全基于服务器消息块（SMB）协议，但 Microsoft 使用 CIFS 来强调其网络与互联网的互连性。

Windows 计算机网络化背后有一段很长的历史。虽然以下描述是“过度简化的”，但它们能让你对 Windows 网络的复杂性有所了解。然而，Windows 网络的图形用户界面（GUI）具有共同的视觉和感受。网络可以组织成被称为工作组（Workgroups）的小型计算机组，以及具有集中式系统的较大组，即域（Domains）。

在继续之前，请确保你理解了应用于 Microsoft Windows 网络的工作组和域概念。

**工作组（Workgroup）：** 存储在网络中连接在一起的一组计算机。工作组中的任何计算机都没有用户和密码的集中式数据库。工作组是组织 10 台或以下计算机网络的常用方法，也被称为“点对点”网络。

**域（Domain）：** 在 Microsoft 世界中，这是一组在网络中连接在一起的计算机，拥有用户和密码的集中式数据库。这类网络通常使用针对用户和计算机的通用策略进行管理。这与互联网上的域名不同；那些名称与该网络上的层次结构化计算机相关。

### 背景

网络由两台或多台相互通信的计算机组成。通常，网络用于共享文件和打印机。当 Microsoft 最初想要建立文件和打印机服务器时，它借用了 IBM 的操作系统工作，并适配了 NetBIOS（网络基本输入输出系统）。计算机名称限制为 15 个字符。Microsoft 还适配了 IBM 的增强型 NetBIOS 系统 NetBEUI（NetBIOS 扩展用户界面），它支持多达 255 台计算机的用户独立网络。

NetBEUI 的弱点是它是不可路由的；换句话说，你无法设置 NetBEUI 让两个不同的网络相互通信。互联网的发展促使 Microsoft 将其网络接口推向不同的方向发展，这导致了 CIFS 的产生。因为基于 SMB，CIFS 留存了它与 Samba 的兼容性。

在现代网络中，有客户端和服务器。服务器提供与网络上其他计算机共享目录和打印机的服务。客户端连接并使用这些“共享”。

### 我的网络

在本书中，我设置了多台带有各种 Microsoft Windows 操作系统的计算机，从 Windows 95 到 Windows XP 专业版。我还设置了三台运行不同角色的 Red Hat Linux 9 计算机。我将它们设置在一个名为 Darkstar 的点对点工作组和一个名为 Grateful 的域中。表 1 列出的每台计算机都以各种 Grateful Dead Bean Bears（豆熊）命名。

表 1. 我网络上的计算机。

| 计算机名称 | 操作系统 | 角色 |
|---|---|---|
| `sugaree` | Windows NT 4 Server | PDC |
| `cosmmic` | Red Hat Linux 9 | PDC |
| `tennjed` | Windows 2000 Server | 域成员服务器 |
| `allaccess` | Windows XP Professional | 客户端 |
| `reuben` | Windows 98 | 客户端 |
| `stephen` | Windows 2000 Professional | 客户端 |
| `nopaws` | Red Hat Linux 9 | 域成员服务器 |
| `samson` | Windows 98 | 客户端 |
| `daisy` | Windows NT Workstation | 客户端 |
| `ripple` | Windows 95 | 客户端 |
| `althea` | Windows ME | 客户端 |
| `delilah` | Red Hat Linux 9 | 客户端 |

该网络中的客户端可以是 Darkstar 点对点工作组或 Grateful 域的一部分。我可以与它们共享本地目录或打印机。这里的许多计算机是使用 VMware (`www.vmware.com`) 安装的“虚拟机”。虽然我将 Windows 和 Linux 配置为 PDC，但我并没有同时运行这两台电脑。

## 基本视觉和感受

在各种 Windows 操作系统中，有三种查看网络上的计算机和共享的基本方法。旧的 Microsoft 操作系统（即 Windows 95/98）支持一个名为“网络邻域”（Network Neighborhood）的查看器。图 1 显示的是连接到 Darkstar 工作组和 Grateful 域的示例。

你会注意到工作组和域在 GUI 中看起来相似。但正如你作为 Microsoft 管理员所知，计算机组由一组规则管理。域用户名、密码和配置文件存储在集中位置。

较新的 Windows 操作系统包括 Windows ME，使用略不同的网络视图，被称为“我的网络”（My Network Places）。如图 2 所示，这是一个更广泛的网络视图，有趣的是，它可以包括 Linux 和 Unix 计算机原生 NFS（网络文件系统）网络。我将在本章稍后详细讨论它。

## Windows 管理员的 Linux 迁移

![img/64859e736a0839007ea9afb576c195_82_0.png](img/64859e736a0839007ea9afb576c195_82_0.png)

图 1. Microsoft Windows 网络邻域，显示 Darkstar 工作组和 Grateful 域。

![img/64859e736a0839007ea9afb576c195_82_1.png](img/64859e736a0839007ea9afb576c195_82_1.png)

图 2. 我的网络。

虽然 Microsoft Windows 中查看网络的标准方法基于 GUI 界面，但你可以将 Microsoft 网络工具追溯到命令行提示符处运行的文本命令。

在任何版本的 Microsoft Windows 中，打开命令行界面。点击开始 | 运行并在文本框中输入 `cmd`。在命令窗口中，尝试以下命令：

```bash
# 此处原文本未提供具体命令，保留结构
```
