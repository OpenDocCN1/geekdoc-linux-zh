
允许攻击者利用类似的技术混淆请求/响应序列，从而接收本应属于另一个用户的服务器响应。这可能导致响应中的敏感信息泄露，包括会话标识符和 Cookie，这再次可能导致账户被破解。

## 防止 HTTP 响应分割：Web 缓存代理

Web 缓存代理可能是 Web 架构中危险的部分，因为它们可以被用于执行多种攻击，例如网站篡改、会话劫持或窃取敏感数据或凭据。

为了确保 Web 缓存仅用于善意而非恶意，Web 应用程序本身必须进行安全的设计和实现，特别是在输入和输出数据验证方面。

网页以及 Web 缓存中的缓存设置也需要进行配置，以减少滥用。

## HTTP 请求走私 (HTTP Request Smuggling)

| 流行度 | 2 |

| :--- | :--- |

| 简单性 | 2 |

| 影响力 | 7 |

| 风险等级 | 4 |

这种攻击并不依赖 Web 应用程序内部的漏洞，而是依赖于 Web 架构本身。它依赖于不同厂商和产品所使用的 HTTP 协议的不同实现方式，例如如何处理带有两个 `Content-Length` 头的请求。这种攻击由 Watchfire 开发，该其后已被 IBM 收购。原始白皮书可以在 `https://www.watchfire.com/securearea/whitepapers.aspx` 找到。

在以下示例中，虚拟主机 `www.example.com` 和 `www.malicious_site.com` 托管在具有相同 IP 地址的同一服务器上：

```
POST http://www.example.com/welcome.html HTTP/1.1
Host: www.example.com
Content-Type: text/html
Content-Length: 0
Content-Length: 69
[CR LF]
GET /login.html HTTP/1.1
Host: www.malicious_site.com
Myheader: [space no CR LF]
GET http://www.example.com/login.html HTTP/1.1
Host: www.example.com
[CRLF]
```

## 第 13 章：Web 应用程序攻击

假设网络上的 Web 缓存实现的 HTTP 协议将最后一个 `Content-Length` 头部接受为 Web 头部；因此，接受第 7–9 行的 69 个字符作为 `welcome.html` 的请求体。这允许代理随后继续解析第 10-12 行包含的 `login.html` 页面请求。

现在代理已将此内容传递给 Web 服务器，让我们分析 Web 服务器将如何解析这些请求，假设它接受看到的第一个 `Content-Length` 头部作为 Web 头部。第一个 `Content-Length` 值为 0，Web 服务器接受第 1–6 行的第一个请求，返回 `welcome.html`，代理也已经确定了这一点。这允许 Web 服务器继续解析从第 7 行开始的请求；然而，由于第 9 行末尾没有 CRLF，第 10 被解析为 `Myheader` 头部的值。因此，请求由第 7–12 行组成，返回 `fakelogin.html`。

这导致了预期的页面与服务器实际返回的页面之间存在冲突。假设这些是可缓存的页面，该页面会将 `http://www.malicious_site.com/fakelogin.html` 页面缓存在 URL `http://www.example.com/login.html` 下。在任何时候，如果有任何用户请求 `login.html` 页面，代理都将返回 `fakelogin.html` 的内容。

这可能导致诸如通过在 Web 服务器中走私恶意的 HTTP 请求来捕获身份验证凭据、会话劫持、跨站脚本，甚至绕过入侵防御系统或 Web 应用防火墙。

## 防止 HTTP 请求走私：Web 基础设施选择

每个被认为是 Web 应用程序基础设施一部分的设备都需要进行安全配置，以保证 Web 应用程序的安全。如果 Web 应用程序架构的任何部分配置不当，那么 Web 应用程序可能会面临各种攻击。

研究并测试 Web 基础设施组件，以确保由于相关协议的不同实现可能会产生漏洞。作为应用防火墙、入侵检测和防御系统、负载均衡器、Web 服务器、缓存代理的设备都可能在创建漏洞方面发挥作用。这些漏洞可能难以修复，因为相关厂商必须更改其对 HTTP 协议的实现，否则需要更换设备。

在进行威胁建模并确定您的 Web 应用程序应与第三方 Web 应用程序托管在同一台服务器上，甚至是同一个环境中时，请考虑这些第三方应用程序带来的风险。如果这些风险太高且无法缓解，那么你需要将 Web 应用程序移动到另一个环境，或者创建一个专用环境。

### 总结

在了解了 Web 应用程序可能面临的许多漏洞后，大多数 Web 应用程序安全的新手（包括大量的开发者）对 Web 应用程序可以被无数种方式攻击以操纵或破坏其核心目的感到非常震惊。这是由于组织在开发系统时没有遵循 Web 应用程序安全框架导致的，其中包括：

- 对用户进行安全意识培训，以最大限度地减少信息泄露并减少人为安全漏洞。
- 将安全性构建到 `SDLC`（软件开发生命周期）中，以确保安全不是事后考虑。
- 安全 Web 服务器配置并进行补丁和升级，以防止系统和应用程序被破解。
- 验证所有 Web 应用程序数据，以确保您的 Web 应用程序按预期运行。
- 跟上最新的 Web 2.0 攻击以确保您实施了适当措施。

## 第 14 章

### 案例研究

`MED` 是 `UTC` 的计算实验室。该实验室完全由学生运行。实验室的创建有两个目的：1) 管理计算机科学（`CS`）部门教师和学生使用的网络，包括教授的桌面电脑、服务器、交换机、防火墙等；2) 让学生暴露在真实环境中以学习管理员的技能。

周六早上，管理员之一 `IO` 收到了来自 `CS` 部门教授 `X` 的电话。教授 `X` 感到愤怒且紧张，因为他的邮件无法工作，而论文周一就要提交。他已经进行了基础测试——从自己和其他其他账户发送邮件。`IO` 和另一位管理员 `PEEL` 去 `MED` 开始调试邮件服务器。经过一些分析，他们发现 `Exim`（用于接收和递送邮件的开源邮件传输代理 `MTA`）在每次尝试处理输出队列时都会崩溃。

在重启服务并在调试模式下从命令行运行命令后，他们开始分析代码但对发生了什么没有答案。他们最终检查队列中有多少邮件，发现有 100,000 封！得知这一点，他们确定服务器正遭受 Do 攻击。通过对队列中的消息进行快速分析，他们确定所有邮件都来自 `MED` 内部的一台机器。他们找到了该机器并迅速拔掉了网线。

这样 Do 攻击得到了控制，他们恢复恢复服务。使用 `Perl` 脚本将队列中匹配攻击者 IP 地址的所有邮件移动到另一个文件夹中供日后分析。一旦文件夹清理，他们重启服务，一切正常。他们找到了负责这次攻击的学生及其团队，并质问发生了什么。事实证明没有任何恶意活动。一个监控程序每两秒发送一封报告连接丢失的邮件。

# 第 14 章：邮件服务

简单邮件传输协议（`SMTP`）更便于电子邮件的交换。尽管即时消息（`IM`）日益流行，但自 1992 年以来，由于我们一直使用电子邮件作为通信媒介（参考 `RFC 822`，后由 `RFC 2822` 更新），它仍然是互联网上使用最广泛的协作工具。邮件广泛参与了各种网络活动，从最常用的社交媒体之一到各种自动化流程、监控系统、交易系统等。在本章中，我们将介绍 `SMTP` 的基础知识，以及涉及邮件服务的组件。

## SMTP 基础知识

其名称中的 S 代表“Simple”（简单），`SMTP` 被设计为一种简单的协议，用于在两个实体之间传递消息，这两个实体通常被称为邮件传输代理（`MTA`）和邮件用户代理（`MUA`）。这仅仅是任何邮件系统中涉及的两个循环往复的操作。还有许多其他操作，了解和理解这些操作非常重要，特别是在处理和比较 `SMTP` 实现时。`MTA` 和 `MUA` 之间事务的简单示例可以在图 14-1 中看到，或者在每封邮件中。

从 `SMTP` 的角度来看，一条消息由头信息（`headers`）和正文（`body`）组成。头信息是机器可解析的，有时包含各种信息，最基本的头信息如用于邮件收件人的 `To:` 或主题的 `Subject:`。发件人地址可能被被迅速视为描述的一项基础信息而忽略，但你会发现它是一个更复杂的概念。

消息的正文包含了除头信息以外的所有内容，并且通常不会被 `MTA` 解析（尽管正如你将看到的，`MTA` 会为了过滤目的对其进行解析）。通常，邮件正文包含纯文本，也可以是 HTML（这在技术上意味着人类），并且在多部分消息（即带有附件的消息）中包含 `MIME`。`MIME` 代表多用途互联网邮件扩展协议（Multipurpose Internet Mail Extensions），它是一种用于发送除纯 ASCII 和二进制内容之外的不同字符编码的标准；邮件客户端会在需要时自动处理 `MIME`。

某些头信息可以被删除，某些可以被修改，某些将由邮件流过程中的不同组件添加。每个 `MTA` 都应该始终添加一个 `Received` 头信息，以跟踪其在传输过程中邮件路径中的角色。理论上，通过查看头信息，你应该能够追踪到原始发送者。然而，你会发现为什么情况并不总是如此。

每封邮件都有一组头信息以供 `SMTP` 标准解析，某些头信息是大多数 `SMTP` 实现认为是标准的但实际上并非如此，另一些带星号（*）的头信息是可以自定义的，可以包含任何类型的消息。将其视为一种将用户定义的内容从正文转移到头信息的方法。一些广泛使用的示例是过滤应用程序（`X-Spam`）和 `MUA`（`X-Mailinger`）。

## Hacking Exposed 局限：Linux 安全秘密与解决方案

```
Subject: Re: linux security kernel cap
From: <rick@isecom.org>
Date: 12/14/2007 7:37 PM
To: <pete@isecom.org>
X-Account-For: 
X-Udbi: 22120db8ee84c12
X-Mozilla-Status: 0000000
X-Mozilla-Path: <rick@isecom.org>
Delivered To: <pete@isecom.org>
Delivered: (unknown) by mail4.isecom.org
Received: (06678 from network) [66.36.29.4] with SMTP; 14 Dec 2007 18:37:03 -0000
Received: from mail4.isecom.org (127.0.0.1) by mail4.isecom.org (Postfix) with SMTP ID 6B291C93B2 for <pete@isecom.org>; Fri, 14 Dec 2007 13:37:03 -0050 (EST)
X-Virus-Check: by mail4.org
X-Spam-Check: by mail4.org
X-Spam-No: hits=0;score=0.114=0.5-tests--ALL_TRUSTED_USER_IN_WHITELIST-enabled=3.200023
X-Spam-Filter: 5e7c702936d2b0b6a1e745b2e
Translating sender: (unknown) (HELO)
Received: from rel00.isecom.org (rel00.isecom.org) by mail4.isecom.org (Postfix) with SMTP ID 6B291C93B2 for <pete@isecom.org>; 14 Dec 2007 13:37:03 -0050 (EST)
Received: (0663 invited by uuu [id]) on 14 Dec 2007 18:37:03 -0000
Received: from (unknown) (with SMTP); 14 Dec 2007 18:37:03 -0000
Authenticated
Message-Id: <C76C3DE-9030506@isecom.org>
User-Agent:
Mime-Version: 1.0
References: <476C2806.7026068@isecom.org>
In-To: 1
Content-Type: text/plain; charset=ISO-8859-1
```

图 14-1：`MTAs` 和 `MUAs` 之间的事务示例

```
Subject: Re: linux security kernel cap
From: <rick@isecom.org>
Date: 12/14/2007 7:37 PM
To: <pete@isecom.org>
X-Account-For: 
X-Udbi: 22120db8ee84c12
X-Mozilla-Status: 0000000
X-Mozilla-Path: <rick@isecom.org>
Delivered To: <pete@isecom.org>
Delivered: (unknown) by mail4.isecom.org
Received: (06678 from network) [66.36.29.4] with SMTP; 14 Dec 2007 18:37:03 -0000
Received: from mail4.isecom.org (127.0.0.1) by mail4.isecom.org (Postfix) with SMTP ID 6B291C93B2 for <pete@isecom.org>; Fri, 14 Dec 2007 13:37:03 -0050 (EST)
X-Virus-Check: by mail4.org
X-Spam-Check: by mail4.org
X-Spam-No: hits=0;score=0.114=0.5-tests--ALL_TRUSTED_USER_IN_WHITELIST-enabled=3.200023
X-Spam-Filter: 5e7c702936d2b0b6a1e745b2e
Translating sender: (unknown) (HELO)
Received: from rel00.isecom.org (rel00.isecom.org) by mail4.isecom.org (Postfix) with SMTP ID 6B291C93B2 for <pete@isecom.org>; 14 Dec 2007 13:37:03 -0050 (EST)
Received: (0663 invited by uuu [id]) on 14 Dec 2007 18:37:03 -0000
Received: from (unknown) (with SMTP); 14 Dec 2007 18:37:03 -0000
Authenticated
Message-Id: <C76C3DE-9030506@isecom.org>
User-Agent:
Mime-Version: 1.0
References: <476C2806.7026068@isecom.org>
In-To: 1
Content-Type: text/plain; charset=ISO-8859-1
```

图 14-2：带有自定义头信息的邮件示例

```
Subject: Re: linux security kernel cap
From: <rick@isecom.org>
Date: 12/14/2007 7:37 PM
To: <pete@isecom.org>
X-Account-For: 
X-Udbi: 22120db8ee84c12
X-Mozilla-Status: 0000000
X-Mozilla-Path: <rick@isecom.org>
Delivered To: <pete@isecom.org>
Delivered: (unknown) by mail4.isecom.org
Received: (06678 from network) [66.36.29.4] with SMTP; 14 Dec 2007 18:37:03 -0000
Received: from mail4.isecom.org (127.0.0.1) by mail4.isecom.org (Postfix) with SMTP ID 6B291C93B2 for <pete@isecom.org>; Fri, 14 Dec 2007 13:37:03 -0050 (EST)
X-Virus-Check: by mail4.org
X-Spam-Check: by mail4.org
X-Spam-No: hits=0;score=0.114=0.5-tests--ALL_TRUSTED_USER_IN_WHITELIST-enabled=3.200023
X-Spam-Filter: 5e7c702936d2b0b6a1e745b2e
Translating sender: (unknown) (HELO)
Received: from rel00.isecom.org (rel00.isecom.org) by mail4.isecom.org (Postfix) with SMTP ID 6B291C93B2 for <pete@isecom.org>; 14 Dec 2007 13:37:03 -0050 (EST)
Received: (0663 invited by uuu [id]) on 14 Dec 2007 18:37:03 -0000
Received: from (unknown) (with SMTP); 14 Dec 2007 18:37:03 -0000
Authenticated
Message-Id: <C76C3DE-9030506@isecom.org>
User-Agent:
Mime-Version: 1.0
References: <476C2806.7026068@isecom.org>
In-To: 1
Content-Type: text/plain; charset=ISO-8859-1
```
