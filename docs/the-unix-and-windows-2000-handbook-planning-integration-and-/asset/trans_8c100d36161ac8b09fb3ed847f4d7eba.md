

分别由各自的操作系统使用以允许目录或文件系统共享。

## NFS

网络文件系统允许不同的操作系统能够透明地交换数据。NFS 的主要组件是远程过程调用（RPC）和外部数据表示（XDR）语言。RPC 允许本地机器请求远程机器执行一个函数并返回该请求的结果。XDR 以机器无关的方式定义数据结构。这使得 NFS 能够在不同操作系统之间通过网络共享目录和文件系统。NFS 已成为 UNIX 操作系统中的事实标准，但在许多其他操作系统上也有提供，包括 Windows 2000。

## SMB

SMB 是 Windows 2000 主要用于网络连接文件、打印机和资源使用的协议。SMB 协议运行在 TCP/IP、NetBEUI 和 IPX/SPX 之上。这种多功能性使 SMB 能够在几乎任何网络环境中运行。多年来，基础 SMB 协议出现了多个变体，其中最著名的是 Windows NT 4.0 和 Windows 2000 中使用的 NTLM 协议。SMB 协议的最新变体是 CIFS，即通用 Internet 文件系统。CIFS 是 NTLM 加上一些用于优化 Internet 上性能的额外功能。SMB 是一种客户端/服务器协议，可用于许多平台。

## SAMBA

SAMBA 为 UNIX 系统提供客户端和服务器 SMB 服务。SAMBA 允许大多数 UNIX 平台进行 SMB 连接。除了 Linux 之外，没有任何标准 UNIX 系统随附任何 SMB 服务。Red Hat Linux 包含 SAMBA 的较新构建。SAMBA 已迅速成为 UNIX 系统的首要 SMB 服务。最近的 SAMBA 镜像站点位于 http://www.samba.org。SAMBA 是免费的且安装并不困难。

本章解释了在计算系统之间共享文件和目录所需的概念、应用程序和程序。下一步逻辑步骤，也是系统管理的重要组成部分，是为个人提供通过计算机/网络基础设施相互共享信息的能力。因此，下章将介绍电子邮件服务的安装和配置。

## 电子邮件和消息传递

## UNIX

- 电子邮件协议
- Sendmail 安装
- Sendmail 配置
- 测试 Sendmail
- 运行 Sendmail

## WINDOWS 2000

- Microsoft Exchange Server
- 安装 Exchange Server 5.5
- 创建邮箱
- 创建分发列表
- Exchange 2000 Server

![](img/415c89a1ede71e11e5040a0038b6916c_373_0.png)

电子邮件很可能是您网络上提供的最关键的服务之一。在当今世界，企业依赖电子邮件的程度与依赖电力或电话一样大。本章提供了 UNIX 系统的 Sendmail 和 Windows 2000 系统的 Microsoft Exchange Server 的概述。我们旨在为您提供一个基本框架，帮助您开始使用电子邮件服务。Sendmail 和 Exchange 5.5 之间一个根本性的区别是创建电子邮件账户的方式。电子邮件是 UNIX 账户的直接副产品。一旦账户创建，电子邮件即可使用。然而，在 Exchange 中，电子邮件账户必须单独创建。这种差异反映在本章所呈现的材料中。

## 电子邮件概述

将电子邮件发送到其目的地需要三个基本代理：邮件传输代理（MTA）、邮件投递代理（MDA）和邮件用户代理（MUA）。这些代理协同工作以发送、路由和投递电子邮件到最终目的地。为了成功交互，代理必须符合标准协议。Internet 工程任务组（IETF）管理电子邮件的官方 Internet 协议标准。我们将在接下来的两个部分简要解释电子邮件的代理和标准。

### 邮件代理

MTA 处理在 Internet 或您本地组织内的电子邮件路由。MTA 执行三个主要功能：它将电子邮件路由到其他 MTA，它将电子邮件投递到本地的 MDA（仅 Sendmail），并接受来自 MUA 的电子邮件。电子邮件传输中使用的协议是通过协商确定的。主要协议是简单邮件传输协议（SMTP）和扩展简单邮件传输协议（ESMTP）。Sendmail 和 Exchange 都是 MTA，将在本章后面进行回顾。

MDA 处理电子邮件的本地投递。MDA 从 MTA 接收电子邮件并将电子邮件投递到可由 MUA 访问的目录。UNIX Sendmail 经常使用 `/bin/mail` 或 `procmail` 作为其 MDA。Exchange 不使用 MDA。

MUA 是电子邮件的用户界面。它允许用户编辑、查看、存储和操作电子邮件。MUA 负责根据 ARPA Internet 文本消息格式标准（RFC822）格式化电子邮件。它还“与”MTA 使用 SMTP/ESMTP“对话”以发送电子邮件。邮局协议（POP）和 Internet 消息访问协议，版本 4rev1（IMAP4rev1）是为了将电子邮件从邮件服务器传输到客户端进行操作而开发的。我们在以下各节中介绍 UNIX 和 Windows 2000 客户端的不同类型的 MUA。

### 标准

电子邮件的官方 Internet 协议标准包含在由 Internet 工程任务组（IETF, http://www.ietf.org）管理的评论请求（RFCs）中。表 9.1 中列出的 RFCs 是电子邮件的当前 Internet 标准。这些 RFC 中的每一个都包含在 Internet 上交换电子邮件的详细协议规范。上面讨论的邮件代理必须符合这些标准才能成功在 Internet 上发送和接收电子邮件。涉及多用途 Internet 邮件扩展（MIME，RFC1521 和

