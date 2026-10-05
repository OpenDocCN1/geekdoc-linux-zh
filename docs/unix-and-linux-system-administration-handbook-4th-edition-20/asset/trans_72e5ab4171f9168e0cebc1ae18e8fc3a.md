

## 第 20 章 电子邮件

正如 SPF（第 767 页）和 DKIM（第 845 页）要求的那样，显示自组织的邮件必须源自该组织。

如果你使用 MSA（邮件提交代理），请确保配置你的传输代理，使其不会重复 MSA 已经完成的任何重写或报头修复工作。重复处理不会影响邮件处理的正确性，但会意味着额外的额外工作。

由于你的 MSA 使用 MTA（邮件传输代理）中继消息，MSA 和 MTA 必须使用 SMTP-AUTH 进行相互身份验证。否则，你将拥有一个所谓的开放中继，垃圾邮件发送者可以利用它，其他站点也会为你加入黑名单。

## 传输代理 (Transport agents)

传输代理必须接受来自用户代理或提交代理的邮件，理解收件者地址，并以某种方式将邮件发送到正确的主机。传输代理使用简单邮件传输协议（SMTP），该协议最初定义在 RFC2621 中，但现在已被 RFC5321 取代并扩展。扩展版本称为 ESMTP。

MTA 作为邮件发送者和接收者，其选择列表包括：

- 从远程邮件服务器接收邮件消息
- 理解收件者地址
- 将地址重写为投递代理理解的格式
- 将消息转发到下一个负责的邮件服务器，或将其传递给本地投递代理保存到用户的邮箱中

设置邮件系统涉及的大部分工作与 MTA 的配置有关。在书中我们涵盖了三个开源 MTA：sendmail、Exim 和 Postfix。

## 本地交付代理 (Local delivery agents)

投递代理（有时称为本地交付代理 LDA）接受传输代理的邮件，并将其投递到本地机器上相应收件者的邮箱。按照最初的定义，邮件可以投递给个人、邮件列表、文件，甚至是程序。然而，最后几种类型的收件者可能会削弱你系统的安全性。

MTA 通常包含一个内置的本地交付代理以便于投递。procmail (procmail.org) 和 Maildrop (courier-mta.org/maildrop) 是投递前对邮件进行过滤或排序的 LDA。某些访问代理（AA）也具有内置 LDA，同时负责投递和本地清理工作。

## 邮件存储器 (Message stores)

邮件存储器是邮件消息在完成跨越互联网的旅程并投递给收件者后的最终归宿。

## 碎片众多，时间有限

邮件传统上存储在 mbox 格式或 Maildir 格式中。前者将所有邮件存储在一个单一文件中，通常为 `/var/mail/username`，单独的消息通过一个特殊的“From”字段分隔。Maildir 格式将每条消息存储在单独的文件中。每个消息创建一个文件更方便，但会创建包含许多小文件的目录；文件系统可能并不喜欢。

这些扁平文件仍然是常见的存储器，拥有成千上万邮件客户端的 ISP 正在寻找其他技术作为其邮件存储，通常是数据库。邮件存储器正变得越来越透明。

## 访问代理 (Access agents)

使用两种协议访问存储器并将邮件消息下载到本地设备（工作站、笔记本电脑、电话等）：IMAP 和 POP。这些协议的早期版本存在安全问题。请确保使用包含 SSL 加密的版本（IMAPS 或 POP3s），因此不会在互联网上以明文传输密码。

我们使用 IMAP（互联网消息访问协议），但 POP 逐个交付你的邮件消息而不是一次性交付，这对网络更友好（尤其是于慢链上），并且对于在各地旅行的人更好。IMAP 特别擅长处理某些人发送的大型附件；你可以浏览消息的报头，并在准备好处理它们之前再下载附件。

IMAP 管理多个站点之间的文件夹；例如，你的邮件服务器和你的 PC。留在服务器上的邮件可以作为正常备份计划的一部分。IMAP 的 Wikipedia 页面包含信息和可用实现的列表。

POP（邮局协议）与 IMAP 类似，但它假设了一个所有邮件从服务器下载到客户端的模型。邮件可以从服务器删除（在这种情况下它可能不会被备份），也可以保存在服务器上（在这种情况下你的邮件池会越来越大）。“一次一个邮箱”的范式对用户来说很困难且不灵活。如果你是一个囤积者并有一个巨大的邮件池文件，速度会非常慢。

一些 IMAP/POP 服务器实现有 Courier、Cyrus IMAP、Dovecot、UW³ imap 和 Zimbra。Dovecot 和 Zimbra 是我们的最爱。每个邮件用户代理都支持 IMAP 和 POP。

## 碎片众多，时间有限

对于一个由这么多部分组成的邮件系统（我们还没有讨论垃圾邮件和病毒扫描！），邮件的架构显得过于复杂。在较小的站点，MTA 可以在很大程度上吸收 MSA 和 LDA 的功能，这使事情保持简单。较大的站点可能希望保持所有部分分离，并运行每个部分的多个实例以帮助分担。

![](img/579efec8c67772f31ecf34844bbb71a2_795_0.png)

1. 华盛顿大学，华盛顿州西。
2. Zimbra 不是一个访问代理，而是一个完整的工业级邮件系统；参见第 83 页。

现实情况是，邮件处理系统可以随你的要求简单或复杂。我们从第 753 页开始介绍设计建议。

## 20.2 邮件消息的解剖

一个邮件消息有三个不同的部分：

- 信封 (envelope)
- 报头 (headers)
- 正文 (body)

信封决定了消息何时投递、投递给谁。信封对用户是不可见的，由 MTA 内部使用。信封地址通常与报头的 From 和 To 行一致，但如果邮件发送到邮件列表或由垃圾邮件发送者生成，则可能不一致。报头是一组在 RFC5322 中属性/值对，记录了关于消息的所有信息，如日期和时间以及发送者。报头是消息真实的一部分，但用户在显示消息时经常隐藏不感兴趣的内容。邮件的正文是待发送的内容，通常由纯文本组成。

## 读取邮件报头

解析邮件报头并利用它们定位邮件系统的问题是管理员的基本技能。许多用户会隐藏报头，但如果你使用编辑器，通常可以看到它们。以下是邮件存储器的部分报头（带有截断），Gmail 用其进行垃圾过滤：

```
Delivered-To: user@gmail.com
Received: by 10.231.39.205 with SMTP id...; Fri, 16 Oct 2009 08:14:27 -000 (PDT)
Received: by 10.114.163.26 with SMTP id...; Fri, 16 Oct 2009 08:14:26 -000 (PDT)
Return-Path: <david@schweigert.ch>
Received: from mail-reply.astrus.com [mail-reply.astrus.com [63.173.189.2]]
by mx.google.com with ESMT id 216978px34.209.18.2;
Fri, 16 Oct 2009 08:14:25 -0700 (PDT)
SPF: fail [spf:google.com domain@schweigert.ch does not designate 173.189.2 as permitted sender] client-ip=63.173.189.2;
Authentication-Results: mx.google.com; spf=hardfail(google.com domain@schweigert.ch does not designate 173.189.2 as permitted sender) smtp.mail=david@schweigert.ch
Received: from schweigert.ch (nigel@schweigert.ch [88.198.52.145])
by mail.relay.atrust.com (8.12/11) with SMTP ID 95GFDKO29250 from <auth@com>; Fri, 16 Oct 2009 14:14 -0600
Received: from localhost (localhost.localdomain) [127.0.0.1]
by mail.schweigert.ch (Postfix) with SMTP ID 325511DA79;
Fri, 16 Oct 2009 14:17:12 +0200 (CEST)
X-Virus-Scanned: Debian amavisid-new@schweigert.ch
Received: from schweigert.ch [127.0.0.1]
by localhost (mail.schweigert.ch [127.0.0.1]) [amavisid-new, port 10024]
with SMTP ID 2A1561DB89; Fri, 16 Oct 2009 14:17:04 +0200 (CEST)
by mail.schweigert.ch (Postfix, from user 1000)
id 2A1561DB89; Fri, 16 Oct 2009 14:17:07 +0200 (CEST)
Date: Fri, 16 Oct 2009 14:17:06 +0200
From: David Schweikert <david@schweigert.ch>
To: evi@atrust.com
Cc: Garth Snyder <garth@garthnyder.com>
Subject: Email chapter comments
```

要最好地阅读这些，请从 `Received` 行开始读，但要从发送方开始。这封来自 David Schweikert 在 schweikert.com 家庭机器的邮件发送到他的邮件服务器 (mail.schweigert.ch)，在那里经过了病毒扫描。它被转发给了收件者 evi@atrust.com。然而，接收主机 mail-relay.atrust.com 将其发送到了 sailing@gmail.com，在那里进入了 Gmail 邮件。

在报头中间，你会看到 SPF 验证失败。这是因为 Google 检查了 mail-relay.atrust.com 的 IP 地址，并将其与 schweweigert.ch 的 SPF 记录进行比较；当然，它们是不匹配的。SPF 记录识别伪造的固有弱点在于它们对于经过中继的邮件无效。

你还可以看到所使用的 MTA（schweigert.ch 上的 Postfix，atrust.com 上的 sendmail 8.12），在这种情况下你还可以看到病毒扫描是在运行 Debian Linux 的机器上通过端口 10.024 的 amavisid-new 执行的。你可以跟踪邮件从中欧夏令时区 (CEST +0200) 到科罗拉多 (-0600)，再到 Gmail 服务器 (PDT -0700) 的进度；这些数字是本地时间与 UTC（协调世界时）之间的差异。报头中有很多信息！

