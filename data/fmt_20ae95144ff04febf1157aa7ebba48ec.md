
```
<Verbatim listing 13>
[bounce message example]

Date: Mon, 5 Mar 2007 11:18:28 -0300
From: Mail Delivery Subsystem <MAILER-DAEMON@huayraint.unju.edu.ar>
To: security@isecom.org
Subject: Returned mail: see transcript for details
-- Attachment #1 --
[-- Type: text/plain, Encoding: 7bit, Size: 0.5K --]
The original message was received at Mon, 5 Mar 2007 04:57:32 -0300
from 190-48-227-213.speed.com.ar [190.48.227.213] (may be forged)
-- The following addresses had permanent fatal errors :=:
<info@fhycs.unju.edu.ar>
(reason: 550 <info@fhycs.unju.edu.ar>... User unknown)
-- Transcript of session follows ---
while talking to mail.fhycs.unju.edu.ar:
\> RCP TO:info@fhycs.unju.edu.ar
<<< 550 <info@fhycs.unju.edu.ar>... User unknown
550 5.1.1 <info@fhycs.unju.edu.ar>... User unknown
-- Attachment #2 --
[-- Type: message/status, Encoding: 7bit, Size: 0.3K --]
Reporting-MTA: dns; huayraint.unju.edu.ar
Arrival-Date: Mon, 5 Mar 2007 04:57:32 -0300
Final-Recipient: RFC822; info@fhycs.unju.edu.ar
Action: failed
Status: 5.1.1
Remote-MTA: dns; mail.fhycs.unju.edu.ar
diagnostic-Code: SMTP; 550 <info@fhycs.unju.edu.ar>... User unknown
Last-Attempt-Date: Mon, 5 Mar 2007 11:18:27 -0300
-- Attachment #3 --
```

-- Type: message/rfc822, Encoding: 7bit, Size: 4.5K --

Date:Mon, 05 Mar 2007 09:50:37 +0200 (CST)

To: info@fhycs.unju.edu.ar

Subject: Semana Santa, ¿Pensamos en Gesell?

From: Semana Santa en y Vacaciones en familia <security@isecom.org>

</Verbatim listing>
# 第 14 章：邮件服务

## 管理出站流量与退信

为了管理你的出站流量，你的策略应该明确定义你的网络和邮件中继接受哪些类型的流量。重要的是尽力不要成为链条中最薄弱的环节，或者在特定情况下成为垃圾邮件、蠕虫或其他类型恶意软件的 {源头。退信消息使用常用的 SMTP DSN（递送状态通知）制作。DSN 不仅限于退信，你还可以将其用于对任何邮件交付的确认。尽管它是一个广泛接受的标准，但它并不是 SMTP 规范的一部分（作为一种扩展），并且某些实现使用了不同的退信格式。Qmail 是 MTA 世界中的一个例外，因为它从发送有关无效接收者的错误；它总是带有退信发送（SMF）。除了给你的 MTA 造成困扰外，感染病毒或恶意软件的邮件可能对你的信誉造成严重威胁。当然，在退信中只保留标头具有节省带宽和大量未请求流量的明显效果。在 Sendmail 中，你可以通过添加隐私标志在退信消息中仅保留标头而不保留正文：

```
define('PRIVACY_FLAGS', 'nobodyreturn')
```

在 Postfix 中，你必须限制从原始邮件中保留的字节数。如果支持 DSN（例如，你可能还想禁用成功 DSN 的报告（即成功交付的回执））以防止信息从你的本地进程泄露：

```
define('PRIVACY_FLAGS','noexpn,needmailhello,receipts')
```

## 用户枚举

| 流行度 | 8 |

| :--- | :--- |

| 简单性 | 3 |

| 影响 | 3 |

| 风险评分 | 5 |

侦察和用户枚举始终是任何渗透测试或垃圾邮件活动的首步之一。获取所有情报对于提高攻击效率至关重要。许多垃圾者收集邮件地址以发布这些转发，特别是当它们来自默认发布整个邮件（包括正文）的站点时。其他人则通过活动的 `EXPN` 和 `VRFY` 命令直接寻找可靠源。

## 处理用户枚举：EXPN、VRFY 和多个接收者

每个邮件服务器检查列表的第一项是禁用 `EXPN` 和 `VRFY` 命令。`EXPN` 命令允许你展开与列表相关的地址（例如别名）。允许 `EXPN` 通常是一个坏主意，因为可以用于用户枚举和邮件地址收割（有助于垃圾者）。此外由于由于邮件别名可以管道到程序，你可能会泄露操作系统和软件的信息。

`VRFY` 命令在 SMTP 会话中验证邮件地址是否有效（而不展开）。这允许轻松枚举地址，因为你可以在同一个 SMTP 会话中使用多个 `VRFY` 命令而不实际交付消息。以下是这两个命令用于友好型邮件服务器的示例：

```
<Verbatim listing 14>
# telnet mail.example.org 25
Trying 192.168.1.1...
Connected to mail.example.org.
Escape character is '^'.
220 box.example.org SMTP mail.example.org ; Mon, 9 Oct 2006 15:39:45 GMT
HELO testclient.example.org
250 mail.example.org Hello testclient.example.org [10.1.7.2], pleased to meet
expn root
250-2.1.5 <joe@mail.example.org>
250 2.1.5 <mike@somewhereelse.com>
expn sales
250 2.1.5 "|/usr/bin/lmmmj-receive -L /var/lists/example.org/sales/"
vrfy joe
250 5.1.5 <joe@mail.example.org>
vrfy notauser...
550 5.1.1 not User unknown
</Verbatim listing>
```

从列表中，你可以快速收集该箱至少有两个管理员（拥有本地邮箱的 `joe` 和指向 `lmmmj` 软件邮件列表的 `sales`）。在同一个 SMTP 会话中，你还可以验证 `<joe@mail.example.org>` 确实存在，而 `<fred@mail.example.org>` 不存在。你可以轻松在 MTA 上禁用这两个命令。在 Sendmail 中，向你的隐私标志中添加 `noexpn` 和 `vrf`：

```
define(`PRIVACY_FLAGS`, `noexpn`, `vrfy`)
```

Postfix 有 `EXPN` 服务，可以在 `main.cf` 中禁用 `VRFY`。

```
disable_vrfy_command = yes
```

在 Sendmail 中禁用 `VRFY` 还会启用 `VERB` 命令，该命令将连接设置为详细模式并可能导致敏感信息泄露。由于这两个命令已知与恶意活动有关，它们往往会在你的服务器日志中产生噪声；这里是 Sendmail 反应的示例：
