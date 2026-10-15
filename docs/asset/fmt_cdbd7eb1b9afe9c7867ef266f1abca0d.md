
# 投递代理

投递代理（有时称为本地投递代理 `LDA`）接受来自传输代理的邮件，并将其投递到本地机器上相应的收件人邮箱。按照最初的规定，电子邮件可以投递给个人、邮件列表、文件，甚至是程序。然而，最后几种类型的收件人可能会削弱你系统的安全性和安全性。

`MTA` 通常使用内置的本地投递代理进行早期投递。`procmail` (`procmail.org`) 和 `Maildrop` (`courier-mta.org/maildrop`) 是可以在投递邮件之前过滤或排序邮件的 `LDA`。某些访问代理（`AAs`）也具有兼顾投递和本地维护工作的内置 `LDA`。

## 邮件存储

邮件存储是电子邮件在完成跨越之旅并投递给收件人后的最终存放地。

邮件传统上存储在 `mbox` 格式或 `Maildir` 格式中。前者将所有邮件存储在一个文件中（通常位于 `/var/mail/username`），通过特殊分隔分隔。`Maildir` 将每条邮件存储在单独的文件中，创建了许多小文件；某些文件系统可能并不喜欢这样。每条邮件使用一个文件更方便。

## 访问代理

有两种协议用于访问消息并将电子邮件下载到本地设备（工作站、笔记本电脑、手机等）：`IMAP` 和 `POP`。这些协议的早期版本存在安全问题。确保使用 `IMAPS` 或 `POP3`，它们包含了 `SSL` 加密，因此不会在互联网上明文传输密码。

像 `IMAP`（互联网邮件访问协议）比 `POP` 更好。它一次投递一条邮件，而不是一次投递所有邮件，这对网络更友好（尤其是在慢链路上）。`IMAP` 特别擅长处理巨大的附件；人们可以在准备好处理它们之前浏览你的邮件标头。

`IMAP` 在多个站点之间管理文件夹；例如在你的邮件服务器和 `PC` 之间。留在服务器上的邮件是备份计划的一部分。`POP`（邮局协议）与 `IMAP` 类似，但它假设所有邮件从服务器下载到客户端。邮件要么从服务器删除（在这种情况下可能不会备份），要么保存在服务器上（在这种情况下你的邮件队列会变大）。“一次一个”的范式对网络压力很大，且对用户来说不够灵活。如果你是一个老鼠（rat），这可能会非常慢。

某些 `IMAP/POP` 服务器实现包括 `Courier`、`Cyrus`、`Dovecot` 和 `Zimbra`。`Dovecot` 和 `Zimbra` 是我们的首选。每个电子邮件代理都支持 `IMAP` 和 `POP`。由许多部分组成（甚至包括垃圾邮件和病毒扫描！）邮件架构很大程度上吸收了 `LDA` 的功能，使其保持简单。事实是，邮件处理系统可以像你要求的那样简单或复杂。见第 753 页。

### 20.2 邮件结构

一封邮件有三个不同的部分：

- 信封 (`envelope`)
- 标头 (`headers`)
- 正文 (`body`)

信封决定了邮件将投递到哪里，如果无法投递，它应该返回到哪里。信封对用户是不可见的，不是邮件本身；它由 `MTA` 内部使用。地址通常与 `From` 和 `To` 行一致，但如果邮件是发送给邮件列表或由试图隐藏身份的垃圾邮件发送者生成的，标头可能不一致。

标头是 `RFC5322` 中的属性/值对。它们记录了关于邮件的所有信息，例如发送日期和时间、经过的代理以及是谁。标头是邮件真实的组成，但用户在显示时经常隐藏那些不重要的部分。

正文是要发送的内容。它由纯文本组成，尽管通常代表各种二进制内容。

## 读取邮件标头

分析邮件标头并利用它们定位邮件中的问题。许多用户会隐藏标头，但如果你必须使用邮件编辑器，通常有一种方法可以看到它们。下面是大部分标头（带有截断如 ...）：`Gmail` 作为过滤的一部分。

```
Delivered-To: sailingevi@gmail.com
Received: 10.231.39.205 with SMTP id...; Fri, 16 Oct 2009 08:14:27 -0700
Received: 10.114.163 with SMTP id...; Fri, 16 Oct 2009 08:14:26 -0700
Return-Path: <david@schweigert.ch>
Received: from mail-reply.astrust.com (mail-reply.astrust.com [63.173.189.2])
by mx.google.com with ESMTP id 17si216978px34.299.2010.18.2; Fri, 16 Oct 2009 08:14:25 -0700 (PDT)
Received-SPF: spf [fail: google.com: domain of david@schweigert.ch does not designate 173.189.2 as permitted sender] client-ip=63.173.189.2;
```

```
Authentication-Results: mx.google.com; spf=hardfail(google.com: domain of david@schweigert.ch does not designate 63.173.189.2 as permitted sender) smtp.mail=david@schweigert.ch

Received: from mail.schweigert.ch (nigel.schweigert.ch [88.198.2.145])

from mail.relay.astrust.com (8.12.18/12.11) with SMTP ID 95NFEDKAO2950

for <env@atrust.com>; Fri, 16 Oct 2009 14:14 -0600

Received: from localhost (localhost [127.0.0.1])

by mail.schweigert.ch (Postfix) with SMTP ID 325111DA79; from Fri, 16 Oct 2009 14:12 +0200 (CEST)

X-Virus-Scanned: Debian amavis-new@schweigert.ch

Received: from mail.schweigert.ch [127.0.0.1]

by amavis-new, port 10024

with SMTP ID 8vdBBp7rhKC; Fri, 16 Oct 2009 17:14:07 +0200 (CEST)

by mail.schweigert.ch (Postfix), from user 1000

id 2A15612DB89; Fri, 16 Oct 2009 17:14:07 +0200 (CEST)

Date: Fri, 16 Oct 2009 17:14:06 +0200

From: David Schweikert <david@schweigert.ch>

To: evi@atrust.com

Cc: Garth Snyder <garth@garthsnyder.com>

Subject: Email header comments
```

# 第 20 章

## 电子邮件

```
Received-SPF: neutral (google.com: 63.173.189.2 is neither permitted nor denied by best guess record for domain smotherling39@sherman.dp.ua) client-ip=673.189.2.

Authentication-Results: mx.google.com; spf-neutral (google.com: 63.173.189.2 is either permitted nor denied by best guess record for domain of smotherling39@sherman.dp.ua) smtp.mail=smotherling39@sherman.dp.ua

Received: from SpeedTouch.in (187-10-167-249.dsl.telesp.net.br [187.10.167.249 (by forged)]) by mail-relay.atrust.com

Received: from 187.10.167.249 by relay2trfile.net, Mon, 19 Oct 2009 13:59: ...

From: "alert@atrust.com" <alert@atrust.com>

To: <@@atrust.com>

Subject: A new settings file for the nedatrust.com mailbox

Date: Mon, 19 Oct 2009 13:59:12 -0300
```

根据 `From` 头部，此条消息的发送者是 `alert@atrust.com`。但根据 `Return-Path` 头部（该头部包含信封发送者的副本），发源地是 `smotherling39@sherman.dp.ua`，这是一个乌克兰的地址。

处理该消息第一个 `MTA` 位于 `IP` 地址 `187.10.167.249`，位于巴西。笑脸的垃圾邮件发送者……
