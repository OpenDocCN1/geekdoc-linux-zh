
- 4. （可选）要获取每个状态的描述和建议操作，访问页面上的在线帮助。
- 5. 完成后，选择“确定”。

选中了您想要查看详情的服务器，您也可以点击相应的链接。

# 如何比较健康详情

要比较多个服务器的视图或查看一个服务器的多个页面，请执行以下操作：

- 1. 显示您想要监控的视图链接。
- 2. 右键点击该链接。
- 3. 在新窗口或标签页中打开链接。
- 4. 调整视图的大小和位置。

对每个视图重复这些步骤。

# 练习 3-6 检查您的 OES 服务器

在此练习中，您将使用 HMS 检查 OES 服务器的健康状况。

练习 3-6 检查您的 OES 服务器位于《Linux 版 Open 服务器集成工作手册》第 32 页。

# 总结

| 目标 | 总结 |
| :--- | :--- |
| 1. 使用 OpenSSH 远程管理 OES 服务器 | Novell OES 在 OES Linux 和 OES NetWare 上都提供了 OpenSSH 包。<br><br>为了有效使用 OpenSSH 远程执行基本任务，您需要了解：<br>- OpenSSH 的优势<br>- OpenSSH 与 OES Linux<br>- OpenSSH 与 OES NetWare<br>- 如何使用 SSH 命令 |
| 2. 使用 Novell 远程管理器 (NRM) 管理 OES 服务器 | Novell 远程管理器 (NRM) 是一种基于浏览器的工具，您可以使用它从远程管理一个或多个 OES NetWare 或 OES Linux 服务器。<br><br>在此目标中，您学习了关于 NRM 的以下内容：<br>- 混合 OES 服务器环境中的环境<br>- 如何在 OES NetWare 上开始使用 NRM<br>- 如何在 OES Linux 上开始使用 NRM<br>- 如何配置组和组操作 |

## 目标

## 摘要

## 3. 使用 Novell iMonitor 在 OES 上监控 eDirectory 目录树

Novell iMonitor 为您 eDirectory 目录树中的所有服务器提供跨平台的监控和诊断功能。

在 iMonitor 中查看的信息会立即显示您的服务器上正在发生的情况。

在本目标中，我们假设您已经知道如何对 NetWare 服务器使用 iMonitor，但由于以下信息适用于 OES Linux，您可能需要复习这些内容：

- Novell OES iMonitor 特性
- 系统要求
- 如何访问 iMonitor
- Novell Remote Manager 集成

# 集成 Linux 版 Open Novell Enterprise Server

## 目标

## 摘要

## 4. 使用 Novell iManager 管理 Novell OES 服务器

Novell iManager 是一个基于 Web 的管理控制台，它允许你在任何可以访问互联网和 Web 浏览器的地方，对网络管理实用程序和内容进行安全、自定义的访问。

在本目标中，您学习了关于 Novell iManager 2.5 以及从 OES Linux 服务器桌面启动并运行 iManager 的以下知识：

- 2.5 版本的新功能
- 如何访问 iManager
- 如何初始配置 RBS
- 如何配置 RBS
- 如何自定义 iManager
- 如何监控服务器健康
- Novell OES 中的 iManager 问题

严禁复制本手册全部或部分或分发此类副本。如怀疑有复制行为，请拨打 1-800-PIRATES。

3-102

版本 1

# 第 4 在 Novell OES Linux 服务器上实现 DNS/DHCP

在本节中，您将学习如何在 Novell OES Linux 服务器上配置 DNS/DHCP。

## 目标

- 1. 在 Novell OES Linux 上配置 DNS
- 2. 在 Novell OES Linux 上配置 DHCP 服务器

# 介绍

OES Linux 提供了您已经熟悉的所有网络基础设施服务。在本节中，您将配置集成在 OES Linux 中的 DNS 和 DHCP 服务，并通过 YaST 对其进行配置和管理。

## 目标 1

# 在 Novell OES Linux 上配置 DNS

在您的 OES Linux 服务器上配置 DNS 之前，您需要了解以下内容：

- DNS 在 OES Linux 上如何实现
- 如何使用 YaST 在 OES Linux 上配置 DNS
- DNS 服务器配置文件是什么
- 如何在 OES Linux 上测试 DNS

# DNS 在 OES Linux 上如何实现

域名系统服务 (DNS) 是基于 TCP/IP 网络中的标准名称解析服务。

DNS 基于为 UNIX 系统开发的 BIND（伯尔克大学互联网网域）架构。它通常与动态主机配置协议 (DHCP)配合使用，为客户端提供主机服务器配置信息。

Novell 为 NetWare 开发了支持目录的 DNS/DHCP 服务，该服务符合 BIND 9.2 标准。Novell DNS/DHCP 服务利用 eDirectory 提供这些服务的集中配置和管理。

管理员可以使用基于 Web 的 iManager 实用程序或独立的 DNS/DHCP 管理控制来管理 Novell DNS/DHCP 服务。

OES Linux 同样使用符合 BIND 标准的 DNS 服务器。

由于 OES NetWare 和 OES Linux 的 DNS/DHCP 服务都遵循 BIND 标准，因此可以在同一网络上共存。客户端可以从任何可用的 DNS/DHCP 服务器接收名称解析和主机配置信息。

某些 DNS 安全机制（例如 DNS 安全事务签名和 DNS 安全扩展）在 OES NetWare DNS 服务器中不受支持。

OES Linux DNS 服务器不支持 OES NetWare DNS 服务器提供的动态重新配置和 SNMP 陷阱。它没有与 iDirectory 或 Novell DNS/DHCP 管理控制集成。

有关 OES Linux 上 DNS 的详情，请参阅《SUSE Linux Enterprise Server 9 管理指南》(`sles_admin.pdf`) 第 310 页的“DNS - Domain Name Service”。您可以通过 `http://www.novell.com/documentation/oes` 或课程 CD 中的 `OES_Docs` 目录访问该指南。

有关 OES NetWare 上 DNS 的详情，请参阅《NetWare Novell DNS/DHCP 服务管理指南》(`dhcp_enu.pdf`) 第 71 页的“Configure DNS”。您可以通过 `http://www.novell.com/documentation/oes` 或课程 CD 中的 `OES_Docs` 目录访问该指南。

# 如何使用 YaST 在 OES Linux 上配置 DNS

在 OES Linux 上配置 DNS 服务器的过程是通过 YaST 实用程序完成的。

要开始此过程，启动 YaST 并选择 **网络服务 > DNS 服务器**。如果尚未安装 `bind` 包，系统将提示您安装它们并插入包含安装文件的 CD。

首次通过 YaST 访问 DNS 服务器时，将执行 DNS 服务器安装过程。在此过程中，您配置了某些 DNS 服务器设置，这些设置会被写入 `/etc/named.conf`。

在安装所需的包后，会出现一个适用于 DNS 服务器的转发器设置页面：

转发器 (Forwarders)

要允许守护进程在连接建立时更新转发器，请设置守护进程转发器。要手动更新，请设置手动转发器。要添加新转发器，选择 IP 地址并点击添加；要删除已配置的转发器，选择它并点击删除

配置好转发器设置后，第二个页面允许您定义 DNS 区域：

DNS 区域

使用此项管理 DNS 区域。要添加新区域，选择其区域名称和区域类型并点击添加。要添加反向区域，为网络输入 IP 地址的一部分，后跟 `.192.168.in-addr.arpa`。要删除已配置的区域，选择它并点击删除。要编辑区域，选择它并点击编辑区域...

# 集成 Linux 版 Open Novell Enterprise Server

最后一个页面允许您配置启动行为以及 LDAP 支持以及专家配置：

当您从此页面选择完成时，服务将停止，配置信息将写入文件，并重启。您将返回 YaST 控制中心。

一旦 DNS 服务器配置完成，再次从 YaST 访问配置将显示一个界面，您可以从中配置 DNS 区域、启动行为、日志和其他选项。

例如，如果选择区域选项，将显示可以创建、编辑和删除区域。当您编辑区域时，YaST 会启动编辑器（如下所示）：

当您正在编辑区域设置并为每个区域输入记录时，点击确定退出编辑器页面。

您将返回所示的 DNS 服务器页面。从 DNS 服务器页面选择完成。YaST 将停止服务、写入配置信息并重启服务。

# DNS 服务器配置文件是什么

YaST 及其自动化配置使其成为方便的工具。但您仍然需要熟悉以下配置和设置 DNS 服务的文件：
