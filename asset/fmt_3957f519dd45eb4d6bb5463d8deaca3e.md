
# FTP

如果你需要运行 FTP，请考虑以下步骤：

- 与任何安全敏感型软件一样，确保你安装了 UNIX 厂商最新版本的 `ftpd`。

- 较新版本的 `ftpd` 支持详细日志记录。`l-` 标志会将成功和失败的 ftp 会话记录到 syslog。其他标志支持对匿名 FTP 传输 (`-S`) 和当前 ftp 用户 (`-U`) 进行进一步日志记录。将你的 `ftpd` 设置为详细日志，并定期监控输出（对于繁忙站点建议每天一次）。

- 通过设置文件 `/etc/ftpchroot` 来提供受限的 FTP 环境。

- 如果你需要匿名 FTP，请审阅 CERT 在 http://www.cert.org/advisories/CA-93.10.anonymous.FTP.activity.html 发布的匿名 FTP 配置指南。

    本文档于 1993 年发布，以应对频频发生的 FTP 问题。

- 如果你需要匿名 FTP，请确保匿名 FTP 主目录 (`-ftp`) 不由用户 `ftp` 所有。这可能允许攻击者添加或修改文件。FTP 根目录及其所有子目录应由 `root` 所有。请注意，这与某些过时的帮助页（man pages）所提供的建议相矛盾。

- 如果你需要匿名 FTP，请将其托管在受信任内部网络或局域网之外的上。根据你的防火墙配置，你可能可以将主机置于非军事化区 (DMZ) 中（参见第 331 页的“筛选子网”）。

- 如果你需要提供“卸点”服务，请制定一项策略，要求系统管理员在文件公开之前对其进行检查。

- 通过将匿名 FTP 目录放置在隔离的分区或磁盘上，或者对 `ftp` 用户设置磁盘配额，来抑制拒绝服务攻击的风险。

- 如果你的 FTP 配置支持，通过限制服务器支持的最大并发会话数来抑制拒绝服务攻击的风险。考虑设置一个紧密的会话超时值（默认可能长达 15 分钟）。

- 通过文件 `/etc/ftpwelcome ~ftpd/ltcmod`（针对匿名用户）向潜在的 FTP 滥用者发送警告信息（“禁止未经授权的访问”）。

## wu-ftpd

Warchieve-ftpd (`wu-ftpd`) 是由 Bryan D. O’Connor 在华盛顿大学 (wust.edu) 开发的流行的替代守护进程。目前由 Acad Consulting Services 支持。`wu-ftpd` 部署在许多匿名站点。

更多信息请参见 FAQ：http://www.cetis.hvu.nl/~koos/wu-ftpd-faq.html
下载 `wu-ftpd` 请访问：http://www.academ.com/academic/wu-ftpd/

## ProFTpd

ProFTpd（专业 FTP 守护进程）是一种基于 Apache Web 服务器建模的新型 `ftpd`。作者承认它不是轻量级代码，但他认为它比 `wuftpd` 更安全。更多信息请参阅：http://www.proftpd.org/index.html

## FTP 的未来方向

即使是最好的 FTP 实现也受到底层协议缺陷的影响。在主动模式和被动模式下，在缺乏任何身份验证方法的情况下，协议假设打开数据通道的客户端或服务器与关联控制通道的客户端或服务器是同一个。以控制连接建立后在给定 TCP 端口监听的服务器为例：攻击者可以猜测服务器正在使用的端口并对其发起大量连接尝试。在这种拦截场景下，任何发送给客户端的数据都将流向攻击者的系统。或者，攻击者可以向服务器发送数据，替换客户端想要发送的数据。

# SMTP/sendmail

作为邮件传输代理（Mail Transport Agent），`sendmail` 的作用就像邮政，只不过缺少了真正的邮递员。就像邮局和邮件分拣中心，它作为一个中继，接收、解析、排序并将电子邮件引导至投递代理（“邮递员”），再由这些代理完成最终投递。投递代理通常是运行邮局协议（POP）或互联网邮件组用协议（IMAP）等协议的服务器，这些协议提供了本地存储并将邮件递送到 `/bin/mail` 或 Netscape Messenger 等终端用户程序。

`sendmail` 有两个主要部分：一个二进制程序（通常为 `/usr/lib/sendmail`）和一个配置文件（`sendmail.cf`）。该文件由一组复杂的规则集组成，用于重写邮件头信息、检查错误并选择邮件投递代理。由于 `sendmail` 在每次解析配置文件时都会查询每条规则，因此规则语法是为了程序运行速度优化的，而不是为了人类的可读性。这些规则曾被描述为“现代噪音、Dijkstra 先生在漫画《布丁记》中的咒言，以及标点符号工厂的爆炸”。

额外的组件包括系统级别名文件（它将用户名映射到别名）以及在个人用户家目录下维护的可选 `.forward` 文件。`.forward` 机制允许用户设置自己的转发别名。

Sendmail 在 UNIX 和互联网社区中有一段悠久而丰富的历史，可以追溯到 1979 年，当时该程序的作者 Eric Allan 在加州大学伯尔克利分校学习期间编写了一个名为 `delivermail` 的前身。多年来，该程序经过多次迭代：版本 5（也称为 IDA）在 1993 年被版本 8 代代（最新版本号为 8.9.3）。

在许多方面，`sendmail` 是一个经过验证的解决方案：它安装在超过 75% 的互联网邮件服务器和数千万邮件客户端上。1998 年，Allan 成立了 Sendmail 公司，采用双重业务模式：为企业和 ISP 提供商业级产品和服务，并通过继续开发“免费”开源版本的 Sendmail 分享成功。Sendmail Pro 商业版本具有用于配置的图形用户界面、安装“向导”、打印文档和技术支持。

> 您可以在 http://www.sendmail.com 了解更多关于 Sendmail 公司的信息，并在 http://www.sendmail.org 查找开源版本。在 http://www.sendmail.org/faq/ 可以找到详尽的 FAQ 文档。

## Sendmail 风险

自诞生以来，`sendmail` 设施一直面临着不利的安全风险——它非常复杂；它以 `root` 权限运行；它接受来自互联网上任何计算机的连接；而且它支持丰富的命令语言。它是无数黑客攻击和利用的目标，历史可以追溯到互联网蠕虫甚至更早。

- 1997 年 1 月——根据 CERT 的说法，`sendmail` 8.8.3 版本中引入了一个名为“MIME 转换缓冲区溢出”的严重安全漏洞，允许远程用户以 `root` 权限执行任意命令。攻击者可以通过向运行存在漏洞版本 `sendmail` 的系统发送精心构造的电子邮件邮件来利用此漏洞。

- 1996 年 11 月——CERT 描述了一个长期存在的编码错误，该错误允许任何本地用户获得 `root` 权限。通常，只有 `root` 才能以守护模式启动 `sendmail`，以便在 25 端口上“监听”入站邮件连接。截至 8.7 版本，可以通过使用 `SIGHUP` 信号重启 `sendmail` 来绕过此限制。

- 1995 年 8 月——CERT 报告了 `sendmail` 5 版本 (IDA) 中的一个漏洞，该漏洞允许入侵者获得未经授权的权限（包括 `root`）。解决方案是升级到 8.10 版本。

## 防止 Sendmail 风险

`sendmail` 的整体安全状况并不像这些报告可能指示的那样惨淡。对于每一个漏洞都有修复，而且较新版本经过了精细的加固。

然而，UNIX 供应商在当前的发行版本中发布旧版本的 `sendmail` 一直臭名昭著。如果可能，你希望运行最新版本——开发者定期发布安全修复和其他增强功能。你可以通过运行以下命令查看你的系统运行的是哪个版本的 `sendmail`：

```
$ /usr/lib/sendmail -d0 -bt < /dev/null | grep -1 Version 8.8.6 (PHNE_15509)
```

或者通过 `telnet` 连接到 25 端口：

```
$ telnet localhost 25

Trying...

Connected to localhost.example.com.

Escape character is '^'.

220 localhost.example.com SMTP Sendmail 8.8.6

PHNE_15509)/8.8.6: Thu, 14 Jan 1999 18:35:12 -0800 (PST)

Quit

221 localhost.example.com closing connection

Connection closed
```

## Sendmail 与垃圾邮件

