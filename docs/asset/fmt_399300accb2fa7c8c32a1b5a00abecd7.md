
![](img/ad6042d5030475f5501749d5eb30744c_460_0.png)

# 第 13 章：Web 应用程序攻击

假设网络上使用的 Web 缓存代理实现的 HTTP 协议是接受最后一个 `Content-Length` 头作为有效头部；因此，接受第 7–9 行的 69 个字符作为 `welcome.html` 的请求体。这允许代理继续解析第 10-12 行包含的针对 `login.html` 页面的请求。

现在代理已将此内容传递给 Web 服务器，让我们分析 Web 服务器将如何解析这些请求，假设它接受看到的第一个 `Content-Length` 头作为有效头部。由于第一个 `Content-Length` 值为 0，Web 服务器接受第 1–6 行的第一个请求，并返回 `welcome.html`，代理也确定了这一点。这允许 Web 服务器继续解析从第 7 行开始的请求；然而，由于第 9 行末尾没有 CRLF，第 10 行被解析为 `Myheader` 头部的值。因此，请求由第 7–12 行组成，返回 `fakelogin.html`。

这导致了代理预期与服务器实际返回内容之间产生冲突。假设这些是可缓存的页面，代理会将 `http://www.malicious_site.com/fakelogin.html` 缓存到 URL `http://www.example.com/login.html` 下。此时，如果任何用户请求 `login.html`，代理将返回 `fakelogin.html` 的内容。

这可能导致此类攻击，例如捕获身份凭据、会话劫持、跨站脚本，甚至通过向 Web 服务器走私恶意的 HTTP 请求来绕过入侵防御系统或 Web 应用防火墙。

## 防止 HTTP 走私：Web 基础设施选择

被认为是 Web 应用程序基础设施部分的设备都需要安全配置，以保证 Web 应用程序的安全。如果 Web 应用程序架构的任何部分配置错误，Web 应用程序可能面临各种攻击。

研究并测试 Web 基础设施组件，以确保因相关协议的不同实现而产生漏洞。应用防火墙、入侵检测和防御系统、负载均衡器、Web 缓存、缓存代理和 Web 服务器等设备都可能导致漏洞。这些漏洞可能难以修复，因为相关供应商必须更改对 HTTP 协议的实现，否则需要更换设备。

在进行威胁建模并确定您的 Web 应用程序应该托管在服务器上，甚至作为第三方 Web 应用程序托管在相同环境中时，请考虑这些第三方应用程序带来的风险。如果这些风险过高且无法缓解，则您需要将 Web 应用程序移动到另一个环境或创建一个专用环境。

# 总结

在学习了 Web 应用程序可能面临的许多漏洞后，大多数 Web 应用程序安全的新手（包括很大比例的开发者）对 Web 应用程序可以以无数方式被攻击以操纵或破坏其核心目的感到非常惊讶。这是由于组织在开发系统时没有遵循 Web 应用程序安全框架，该框架包括：

- 对用户进行安全意识培训，以尽可能减少信息泄露并减少人为安全漏洞。
- 将安全性构建到您的 SDLC（软件开发生命周期）中，确保安全不是事后考虑。
- 加固 Web 服务器配置并执行补丁和升级。
- 验证所有数据以确保实施了适当的措施。
- 保持更新以防止攻击。
- 确保环境安全。

# 第 14 章

![](img/ad6042d5030475f5501749d5eb30744c_463_0.png)

## 案例研究

MED 是 UTC（某所大学）的一个实验室。该实验室完全由学生运行。实验室的创建有两个目的：1) 管理计算机科学（CS）部门教师和学生使用的网络，包括教授的桌面、服务器、交换机、防火墙等；2) 让学生在真实环境中学习系统管理员的技能。

周六早上，管理员 IO 收到一个来自 CS 部门 X 教授的电话。X 教授感到愤怒且焦虑，因为他的电子邮件无法工作，而论文周一就要交。他已经进行了基础测试——IO 和 PEEL（另一位管理员）来到 MED 开始调试电子邮件服务器。经过一些分析，他们发现 `Exim`（接收和递送电子邮件的开源邮件传输代理 MTA）在每次处理输出队列时都会崩溃。

在重启服务并从命令行以调试模式手动运行命令后，他们进入分析，但没有明确的答案。他们最终检查了队列中有多少邮件，发现有 10 万封！得知此，他们确定服务器正遭受 DDoS 攻击。通过对队列中的邮件进行快速分析，他们确定它们全部来自 MED 内部的一台机器。他们找到了那台机器并迅速拔掉了网线。

这样 DDoS 攻击得到了控制，他们开始恢复服务。这是不而易举的。通过 Perl 脚本，他们将攻击者 IP 地址的所有邮件从队列移动到另一个文件夹以便稍后分析。清理干净后，他们重启服务，一切正常。他们找到了负责攻击的学生及其团队，并告诉他们发生了什么。事实证明根本没有任何恶意活动。一个监视程序每秒发送一封邮件报告连接丢失。更糟糕的是，团队的邮箱已满，导致开始退信邮件。

在这次事故之后，学生修复了代码，X 教授按时交了论文，而管理员没有获得任何荣誉——一如既常。顺便说一下，在这次事件之后，邮件服务迁移到了 `Postfix` `19990906`。

## 第 14 章：邮件服务

![](img/ad6042d5030475f5501749d5eb30744c_465_0.png)

简单邮件传输协议 `SMTP` 能够用于电子邮件交换。尽管即时通讯 `IM` 日益流行，但自 1992 年（RFC 2822）以来，电子邮件仍然是互联网上最广泛使用的协作工具，该协议最近已由 RFC 2822 更新。电子邮件广泛参与各种网络活动，从最常用的社交媒体之一到各种自动化流程、监控系统、交易系统等。在本章中，我们将涵盖 `SMTP` 基础，以及涉及邮件服务安全的组件。

### SMTP 基础

其名称中的 S 代表“简单”（Simple），`SMTP` 被设计为一种在两个实体之间传递消息的简单协议，这两个实体通常称为*邮件传输代理 `MTA`* 和*邮件用户代理 `MUA`*。这些只是任何邮件系统中涉及的反复出现的断言中的两个。还有许多其他断言，了解和理解它们非常重要，特别是在比较不同的 `SMTP` 实现时。`MTA` 和 `MUA` 之间交互的一个简单示例见图 14-1，或者实际上，见每封电子邮件。

从 `SMTP` 的角度来看，消息由*报头 `headers`*和*正文 `body`*组成。报头是机器可解析的结构，包含各种信息，最基础的报头如用于收件者的 `To:` 或主题的 `Subject:`。发件者地址可能被快速地忽略为一个待描述的基础信息片段，但你会发现它是一个更复杂的概念。

消息的正文包含所有其他内容（所有其他报头），通常不被 `MTA` 解析（尽管正如你将看到的，`MTA` 可能会为了过滤目的进行解析）。通常邮件正文包含简单文本，但也可以是 HTML（这在技术上通常意味着人类），并在多部分消息（即带有附件的消息）中包含 MIME。`MIME` 代表*多用途互联网邮件扩展 `Multipurpose Internet Mail Extensions`*，它是一种用于发送除纯 ASCII 和二进制之外的不同字符编码的标准；客户端在需要时会自动使用 `MIME`。

某些报头可以被删除，某些可以被修改，某些会被邮件流过程中的不同组件添加。每个 `MTA` 都应该始终添加一个 `Received` 报头，以跟踪其在传输过程中邮件路径中的角色。理论上，通过查看报头，你应该能够追踪到原始发送者。然而，你会发现为什么情况并非如此。

每封电子邮件都有一组为了符合 `SMTP` 标准的报头，其中某些大多数 `SMTP` 实现认为是标准但实际上并非标准的报头，另一些报头是可自定义的并可以包含任何类型的消息。将其认为为一种将用户定义内容从正文转移到报头的方法。一些最广泛使用的示例是过滤应用程序 `X-Spam` 和 `MUA` `X-Mailer`。

### 432 Hacking Exposed Limit: Linux Security Secrets & Solutions

| Subject: Re: linux security kernel patch |
| :--- | :--- |
| From | rick@isecom.org |
| To | pete@isecom.org |
| Date | 12/14/2007 7:37 PM |
| X-Account-For | |
| X-Uid: 22120b8ee84c12 |
| X-Mozilla-Status: 0000000 |
| Return-Path | rick@isecom.org |
| Delivered-To | pete@isecom.org |
| Received | (10678 messages inserted from network): 14 Dec 2007 18:37:03 -0000 with SMTP; 14 Dec 2007 18:37:03 -0000 |
| from mail4-part.com (66.39.26.4) | |
| from localhost [127.0.0.1] by mail4-part.com (Postfix) with SMTP ID 62b91c93b82; for: <pete@isecom.org>; Fri, 14 Dec 2007 13:37:03 -0500 (EST) |
| X-Spam-Check-by | mail4-part.com |
| X-Spam-Status | No;hit=101.4 result=0.0; tests=ALL,TRUSTED_USER_IN_WHITELIST disabled version=3.002003 |
| X-Spam-Flag | NO |
| X-Spam-Filtered | sender whitelisted by 57e-47703906d3b10-4e61-a74b5d7b |
| Writing | sender@isecom.org |
| Received | from relay01.part.com (relay01.part.com) 14 Dec 2007 18:37:03 -0000 by mail4-part.com (Postfix) with SMTP ID 62b91c93b82; |
| Received | (6680 messages inserted by ULO): 14 Dec 2007 18:37:03 -0000 |
| Received from unknown (by HELO) (unknown) with SMTP; 14 Dec 2007 18:37:03 -0000 || Path: Authenticated |
| Message-ID | <C7C2CE9E.90D5506@isecom.org> |
| User-Agent | |
| Mime-Version | 1.0 |
| References | <476C2806.702608@isecom.org> |
| In-To | 1 |
| Content-Type | text/plain; charset=ISO-8859-1; format=flowed |
| Content-Transfer-Encoding | 7bit |

Figure 14-1 MTAs and weird deous (ss)

> [Sample message]
From@isecom.org Sep 30 13:50:39 2006
Return-Path: <root@isecom.org>
Received: from isecom.org (localhost.localdomain [127.0.0.1])
by isecom.org (8.1/13.7) with SMTP ID k8UBonod019
for <test@isecom.org>; Sat, 30 Sep 2006 13:50:39 +0200
Received: (root@localhost)
by isecom.org (8.1/13.5/Submit) it k8UBonoc0193
for root; Sat, 30 Sep 2006 13:50:23 +0200

It's uncommon to spot very customized headers in the world; most emails have weird ones!
Date: Sat 30 Sep 2006 13:50:23 +0200
Message-Id: <200609301150.k8UBonoc0193@isecom.org>
From: root@isecom.org
To: test@isecom.org
Subject: foobar

If you look at your raw mail you can sometimes see an additional From followed by a space and then sender address, without the colon in the From: header. This is an internal server defined by the mbox format and is not really an SMTP server. The Mail Delivery Agent `MDA`， which is responsible for storing the message during final delivery, also has the task of protecting any line that begins with From in the body of the message and is prone to misinterpretation. The sample message shown in Figure 14-1 was transmitted with the following SMTP:
