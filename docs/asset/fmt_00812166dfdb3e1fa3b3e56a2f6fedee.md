
```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> .[client_addr]relay 127.0.0.2
> Basic_check_relay <>
rewrite: ruleset 190 input: <>
rewrite: ruleset 190 returns: ## error @ $5.7.1: "Mail from "127.0.0.2" refused by blackhole site rbl.maps.vix.com. Email from your server is blocked. Contact your local Administrator or ISP.
```

如你所见，此 IP 在 RBL 中被黑洞或列入名单，因此 `sendmail` 不允许此 IP 中继消息。你还可以使用你组合好的自动回复器（`autresponder`）进行真实测试。根据自动回复器的说明，你必须从 RBL 拦截你的服务器向 `nelson-test@autresponder.com` 发送邮件以进行测试。如果你的设置不起作用，预计将收到 `ns.example.com` 的回复。如果你想知道哪些邮件事务因为 RBL 被拒绝，你只需运行 `grep "maps.vix.com" /var/log/mail` 来查看被拒绝的请求。

# 设置 POP 服务

邮局协议（POP）被广泛用于检索由 SMTP 服务器存储的邮件。像 SMTP 一样，这也是一个非常简单的协议。考虑客户端如何从 POP 服务器检索邮件。

## 它是如何工作的？

我将使用 `telnet` 客户端来演示这一点，就像我之前对 SMTP 做的那样。因为 POP 服务器监听 TCP 端口 `110`，我可以如下所示 `telnet` 到我的服务器 `blackhole.nitec.com`：

```
telnet blackhole.nitec.com 110
```

我收到了来自 POP 服务器的欢迎消息：

+OK POP3 blackhole.nitec.com ready

然后我输入以下 POP 命令告诉服务器我要要登录的用户：

USER kabir

它回复：

+OK Name accepted, password

然后我使用 POP 命令输入 kabir 的密码：

PASSpwd

POP 服务器回复：

+OK Mailbox open

正如你所见，这里有三条邮件。我使用 POP 命令列出这些邮件：

LIST

POP 服务器回复：

+OK Mailbox scan

1

2

3

为了检索这些邮件中的一个，我输入 POP 命令：

RETR 3

服务器返回：

+OK Message

正如你所见，整个 POP 事务非常简单。现在看看如何为你的系统设置 POP。

![](img/cbfef09f620ba4100baa62876f6f02b1_352_0.png)

阅读 RFC 1939 以了解更多关于 POP3 的信息。

## 安装 POP3 服务器

POP 协议的最新版本是 3，因此你想安装 POP3 服务器。你的 IMAP 软件包包含了 POP3 服务器。因此，要安装 POP3，只需使用通常的 `rpm -ivh` 命令即可。

## 配置 POP3 服务

安装服务器后，你需要修改 `/etc/inetd.conf` 文件，使其包含如下行：

```
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
```

如果你有 `pop-2` 行，可以将其注释掉，因为 POP2 不被广泛使用，且大多数现代 POP 客户端支持 POP3。在设置了上述 `/etc/inetd.conf` 行后，你需要检查 `/etc/services` 文件以确保包含以下行：

```
pop-3 110/tcp # PostOffice V.3
```

检查这两个文件后，你可以使用 `killall -HUP inetd` 重启 `inetd` 进程，使其监听 TCP 端口 `110` 的 POP3 请求。当系统产生 POP3 连接请求时，`inetd` 进程将启动 `inpop3d` 进程来处理请求。你的 POP 服务器现在准备好提供服务。然而，如果你想增强系统安全性，可以使用 TCP wrapper (`tcpd`) 使用的 `/hosts.allow` 和 `/hosts.deny` 文件来限制对你的 POP 服务器的访问。详情请参第 18 章“安全 101”。

# 第11 章：电子邮件服务

## 商业替代方案

尽管我认为开源的 `sendmail` 服务器适用于几乎所有情况，但你的组织可能由于某些要求，不允许将 `sendmail` 作为主要的邮件服务器软件。例如，如果你的组织的软件策略要求组织内使用的所有软件都必须由供应商提供商业支持，那么你可能需要使用 `sendmail` 的商业版本，因为它由 Sendmail, Inc. 直接支持。以下是开源 `sendmail` 服务器的一些替代方案。

### Sendmail Pro

Sendmail Pro 是开源 `sendmail` 服务器的商业版本。它附带增强功能，并提供了你从可靠供应商处所的商业级支持。你可以在以下 URL 找到有关该产品的更多信息：http://www.sendmail.com/。

> 不要将 http://www.sendmail.org/ 与 http://www.sendmail.com/ 混淆。第一个网站由 Sendmail 财团（Sendmail Consortium）维护，第二个网站是 Sendmail, Inc. 的网站。

### qmail

`qmail` 软件包自称为开源 `sendmail` 的现代替代品。根据我从其他系统管理员那里听到的，它的安装非常简单，而且与邮件列表软件提供了良好的集成。你可以从以下 URL 下载该软件的 RPM 包版本：http://www.qmail.org。

如果你对在 `sendmail` 中使用邮件列表软件包感兴趣，你应该考虑使用 Majordomo，你可以在 http://www.greatcircle.com/majordomo/ 找到它。

## 总结

在本章中，你学习了如何将你的 Red Hat Linux 服务器配置为 SMTP 和 POP3 邮件服务器。你学习了 SMTP 和 POP3 的工作原理；如何使用广泛使用的 `sendmail` 服务器软件创建一个健壮的 SMTP 邮件服务器；以及如何使用 IMAP 软件包中的 POP3 服务器来为用户检索邮件消息而创建一个 POP3 服务器。

# 第12 章

## Web 服务

本章内容

- 如何编译、配置和安装 Apache Web 服务器
- 如何配置 Apache 以支持 CGI
- 如何配置 Apache 以支持服务器包含（SSI）
- 如何使用 Apache 支持虚拟 Web 服务
- 如何将 Apache 作为代理服务器
- 如何在 Apache 中使用 HTTP 身份验证
- 如何监控 Apache 服务器
- 如何使用 Apache 记录访问和错误日志
- 如何增强你的网站安全性
- 如何在 Apache 中使用 SSL 进行安全交易

在过去的几年里，全球约 50% 的网站运行在 Apache Web 服务器上。自 1996 年以来，Apache 一直一直是 Web 服务器第一。根据知名公司 Netcraft（http://www.netcraft.com/）的调查，Apache 及其派生 Web 服务器相比于 Microsoft 和 Netscape 等商业 Web 服务器具有明显的领先优势。因此，Red Hat 在官方 CD-ROM 发行版中将 Apache 作为默认 Web 服务器，这并不意外。在本章中，你将学习如何配置和管理 Apache Web 服务器。

我必须承认，由于尺寸限制，在单章中涵盖 Apache 的所有方面几乎是不可能的。因此，我将只讨论与 Apache 相关的主要的配置和管理问题。如果你需要对 Apache Web 服务器进行更深入的介绍，请考虑 IDG Books 出版的《Apache Server Bible》或《Apache Server Administrator's Handbook》。这两本书的作者也是本人！

### Apache 的系统要求

Apache 可以运行在任何能够运行最新版本 Red Hat Linux 操作系统的计算机上。然而，仅仅能够运行 Apache 可能并不是一个实用的目标，特别是当你计划运行高性能 Web 服务器时。为了给 Apache 创建一个稳定的平台，你应该注意以下系统要求。

### ANSI C 编译器

如果你计划在你的 Red Hat Linux 系统上编译 Apache，你将需要 ANSI C 编译器。推荐使用自由软件基金会（FSF）的 GNU C (`gcc`)，它已经包含在你的 Red Hat 发行中了。但是，请确保你拥有 2.7.2r 或更高版本的 `gcc`。另一方面，如果你计划安装预编译的二进制文件，则不需要在目标系统中拥有 C 编译器。我强烈建议编译你自己的 Apache 版本，因为它允许你根据自己的需要进行自定义。

### 足够的磁盘空间
