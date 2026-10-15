
如你所示，有用信息分布在许多行中。注意，标识符 `0E4A93688` 是每行通用的；当邮件进入邮件服务器并等待变化时，`Postfix` 会分配一个队列 ID。当发生变化时，邮件历史的日志首先集中在确定邮件的队列 ID 上。知道了这一点，就可以很容易地 grep 日志查找所有相关条目了。

`Postfix` 擅长记录关于它注意到的问题的有用信息。然而，在成千上条正常状态消息中识别重要行有时很困难。这时可以考虑使用第 220 页开始的“记录日志到有用信息”章节中讨论的工具。

## 第 18 章 – 电子邮件

### 查看队列

另一个查找问题的地方是邮件队列。与 sendmail 系统一样，`mailq` 命令会打印队列内容。你可以用它来查看邮件是否以及为什么被卡住。

另一个有用工具是随 `Postfix` 版本自带的 `qshape` 脚本。它显示关于队列内容的摘要统计数据。输出如下：

```
# qshape deferred
```

| T | 5 | 10 | 20 | 40 | 80 | 160 | 320 | 640 | 1280 | 1280 |
|---|---|---|---|---|---|---|---|---|---|---|
| TOTAL | 78 | 0 | 0 | 0 | 7 | 3 | 0 | 2 | 12 | 2 | 49 |
| expn.com | 34 | 0 | 0 | 0 | 0 | 0 | 0 | 9 | 0 | 25 |
| chinabank.ph | 5 | 0 | 0 | 0 | 1 | 1 | 2 | 0 | 0 | 0 |
| prob-helper.biz | 3 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 3 |

`qshape` 按接收者域名对给定队列（这里是延迟队列）进行汇总。列报告队列中相关消息的数量。例如，你可以看到 49 封 expn.com 的邮件在队列中的时间超过了 1280 分钟。这些目的地都暗示邮件是假期脚本响应垃圾邮件而发送的。

`qshape` 还可以通过 `-s` 标志按发送者域名进行汇总。

### 软退 (Soft-bouncing)

如果 `soft_bounce` 设置为 `yes`，当 `Postfix` 通常会以用户 "unknown" 或 "relaying" 发送永久错误消息时，它发送临时错误消息。这是一个非常好的测试功能；它监控配置更改后邮件的处理情况，而没有永久丢失合法邮件的风险。你拒绝的任何内容最终都会回来再次尝试。测试完成后，忘记关闭此功能，否则你将反复处理被拒绝的消息。

### 测试访问

测试访问的最简单方法是从外部主机发送一条邮件并观察发生了什么。这是一个很好的基础测试，但没有涵盖来自特定域名的邮件等特殊情况。`Postfix` 2.1 引入了名为 AUTH 的 SMTP 扩展。该功能默认是禁用的，但在 `main.cf` 中使用以下行可以启用它：

```
smtpd_authorized_networks = localhost
```

测试会话可能如下：

```
telnet localhost 127.0.0.1

Trying 127.0.0.1...

220 mail.colorado.ch ESMTP

HELO localhost

250-mail.colorado.ch SIZE 10240000

MAIL FROM: <evi@colorado.ch>

250-2.1

RCPT TO: <david@colorado.ch>

250
```

### 推荐阅读

- COSTAZES, BRYAN, AND ERIC ALLMAN. *sendmail (3rd Edition)*. Sebastopol, CA: O'Reilly Media 2002. 这是一本权威巨著，包含了教程以及完整的参考章节。
- CLAYTON, RICHARD. *“Good Practice for Combating Bulk Mail.”* RIPE/Net. 2000, www.ripe.net/rips/rfc-206.html. 这篇文章位于 ISPs。它有很多策略信息和指向技术主题的好链接。
- SCHWARTZ, ALAN, AND PAULA FERGSON. *Managing Mail Lists*. Sebastopol, CA: O'Reilly Media 1998.
- HAZEL, PHILIP. *The SMTP Server: Official Guide for Release 4*. Cambridge, UK: User Interface Technologies 2003. Exim 文档和信息也可以在 www.exim.org 找到。
- *Sendmail: An Internet Mail Router*, Eric Allman，描述了其命令行参数。安装说明和配置文件的详细描述在 *Sendmail Installation and Operation Guide* 中，可以在 sendmail 发行版的 doc/op 子目录下找到。该文档是完整的，并结合 cf 文件提供了 sendmail 系统的直观视图。sendmail.org 包含 sendmail 相关文档、HOWTO 和教程。RFC2822 代替了 RFC822，描述了网络邮件系统中的消息和地址的语法，RFC1123 描述了主机要求。这些是构建 sendmail 的功能规范。

## 第 18 章 — 电子邮件

RFC2821 代替了 RFC821，定义了简单邮件传输协议 (SMTP)，RFC 1869、1870、1891 和 1985 扩展了它。

RFC974 描述了域名系统中的 MX 记录及其与邮件路由的关系。其他相关的 RFC 包括：

- RFC1731 — IMAP4 认证机制
- RFC1733 — IMAP4 中的分布式电子邮件模型
- RFC2033 — 本地邮件传输协议
- RFC2076 — 常见互联网邮件头
- RFC2142 — 用于常见服务、角色和功能的邮箱
- RFC2505 — SMTP MTA 反垃圾邮件建议
- RFC2635 — DON'T SPEW: 批量未经许可邮件发送指南
- RFC2821 — 简单邮件传输协议
- RFC2822 — 互联网消息格式
- RFC4405 — 指明发送者的 SMTP 服务扩展
- RFC4406 — Sender ID: 电子邮件身份验证
- RFC4408 — 用于在电子邮件中使用域名的 SPF，版本 1
- RFC4409 — 邮件提交

RFC 2821 (SMTP) 和 2822 (互联网消息格式) 整理了一些常引用的电子邮件 RFC；它们取代了 RFC 821、822、974 和 1869。RFC 2821 和 2822 于 2001 年 4 月首次发布，是建议标准。

### 18.18 练习

- **E18.1 [sendmail 特定]** 简列出 `generictable` 和 `virtustable` 之间的差异和相似之处。在什么情况下你会使用它们？
- **E18.2 [sendmail 特定]** 比较使用 `/etc/mail/aliases` 与使用 LDAP 服务器存储邮件别名。各者的优缺点是什么？
- **E18.3** 简述邮件用户代理 (MUA)、投递代理 (DA) 和代理访问 (AA) 之间的区别。解释邮件传输代理 (MTA) 和邮件提交代理 (MSA) 之间的区别。
- **E18.4 [sendmail 特定]** 什么是 `smrish`，你为什么要用它代替 `/bin/sh`？如果 `smrish` 存在于你的站点，哪些程序允许作为邮件发送程序运行？它们中是否存在极不安全的程序？
- **E18.5 [sendmail 特定]** 编写一个小的 `/etc/mail/aliases` 文件，以演示不同类型的别名。简要说明每行的作用以及为什么它可能有用。

### 18.18 练习

E18.6 简要描述以下邮件头信息。这封邮件采取了什么？它是发给谁的，又是递给了谁的？邮件从发送者到目的地花了多少时间？

```
From elements@builderlabs.com Fri 28 17:06:57 2001

Return-Path: <clemente@mail.builderlabs.com>

Received: from builder.colorado.EDU (builder.Colorado.EDU)

[128.138.240.1] by ucsub.colorado.edu (11.6/8.11.2/ITS-5.0)

with ESMTP idBT06Vf10618 from <hallcp@ucsub.Colorado.Edu>; For,

28 Dec 2001 17:06:57-0700 (MST)

Received: from mail.builderlabs.com (mail.builderlabs.com)

[206.168.112.48] by builder.Colorado.EDU
```
