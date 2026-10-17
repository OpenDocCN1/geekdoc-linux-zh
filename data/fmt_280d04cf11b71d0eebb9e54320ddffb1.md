
这样 Do 攻击被控制，他们返回恢复服务。这是显而易见的事。通过一个 Perl 脚本，他们移动了所有邮件-

# 攻客入侵：Linux 安全秘密与解决方案

```
Subject: 回: linux 安全内核补丁
From: rick@isecom.org
Date: 12/14/2007 7:37 PM
To: pete@isecom.org
X-Account-For:
X-Udbi: 221120dbee84c12
H-Mozilla-Status: 0000000
H-Mozilla-Path: rick@isecom.org
Delivered-To: <pete@isecom.org
Received: (0667 received from network): 14 Dec 2007 18:37:03 -0000
Received from mailwish4.com (66.239.48.96) with SMTP; 14 Dec 2007 18:37:03 -0000
Received from localhost [127.0.0.1] by mailwish4.com (Postix) with SMTP ID 68291C93B2 for <pete@isecom.org>; Fri, 14 Dec 2007 13:37:03 -0050 (UTC)
X-Virus-Check: by: mailwish4.com
X-Spam-Check: by: mailwish4.com
X-Spam-No: hits=0.1;rule=5.0;tests=ALL_TRUSTED_USER_IN_WHITELIST-enabled=3.200023
X-Spam-Filter: 574=77023996d32b6b41e647b2e (unknown) by <pete@isecom.org>
Received: (0668 received from rel00.isecom.org) (rel00.isecom.org) with SMTP ID 68291C93B2; 14 Dec 2007 18:37:03 -0000
Received: (0668 invoked by uid 0): 14 Dec 2007 18:37:03 -0000
Received: from (unknown) (HELO)
Authenticated: (unknown)
Message-Id: <77C3DE-903506@isecom.org>
User-Agent:
Mime-Version: 1.0
References: <476C2806.7026068@isecom.org>
In-Reply-To:
Content-Type: text/plain; charset=ISO-8859-1; format=flowed
Content-Transfer-Encoding: 7bit
```

## 图 14 MTA 与 MUA

在实际环境中发现非常自定义的标头信息并不罕见；大多数安全专家都希望看到这样的内容！

```
<逐字列表 1>
[示例消息]
From root@isecom.org Sep 30 13:50:39 2006
Return-Path: <root@isecom.org>
Received: from isecom.org (localhost.localdomain) [127.0.0.1]
by isecom.org (8.13.8/8.13.7) with SMTP ID k8UbodHH00194
for <test@isecom.org>; Sat, 30 Sep 2006 13:50:29 +0200
Received: (from root@isecom.org)
by isecom.org (8.13.8/8.13.5/Submit) id k8Uboncz2001193
for root; Sat, 30 Sep 2006 13:50:23 +0200
Date: Sat, 30 Sep 2006 13:50:23 +0200
Message-Id: <200609301150.k8Ubonc2001193@isecom.org>
From: root@isecom.org
```

## 第 14 章：邮件服务

致：test@isecom.org

主题：foobar

test

</逐字列表>

如果你查看原始邮件，有时会看到一个额外的 `From`，后面跟着空格和发送者地址，但在通常的 `From` 标头中没有冒号。这是一个由 `mbox` 格式定义的消息的内部服务器，它并不是一个真正的 `SMTP` 服务器。`mbox` 格式是存储电子邮件的一系列格式的一部分，邮件以纯文形式存储并链接到单个文件中。

邮件投递代理（`MDA`）是负责在最终交付期间存储消息的组件，它还负责保护任何正文中以 `From` 开头且被认为容易误解的电子邮件。

图 14-1 所示的示例消息是通过以下 `SMTP` 事务传输的：

```
<逐字列表 2>
CONNECT [127.0.0.1]
220 isecom.org SMTP Sendmail 8.13.8/8.13.7; Sat, 30 Sep 2006 14:08:38 +0200
EHLO isecom.org
250-isecom.org Hello localhost.localdomain [127.0.0.1], pleased to meet you
250-ENANCEDSTATUS
250-PIPELINING
250-BITIME
250-SIZE 500000
250-DSN
250-DELIVERY
250 HELMAIL From:<root@isecom.org> SIZE=57
250 2.1.0 <root@isecom.org>... Sender ok
RCPT To:<test@isecom.org>
DATA
250 2.1.5 <test@isecom.org>... Recipient ok
Received: (from root@localhost)
by isecom.org (8.13.8/8.13.5/Submit) id k8UCEMj00134
for root; Sat, 30 Sep 2006 14:08:14 +0200
Date: Sat, 30 Sep 2006 14:08:14 +0200
Message-Id: <200609301208.k8UCEMj00134@isecom.org>
From: root@isecom.org
To: test@isecom.org
Subject: foobar
250 2.1.5 k8UCEMj00134
221 2.0 isecom.org
closing
</逐字列表>
```

`SMTP` 在 `25` 端口上“说话”是为了通过 `STARTTLS` 升级到加密连接（`465` 端口和 `587` 端口）。对于 `MUA` 而言，`MSA`（邮件提交代理）是一个相对新的概念，它在 `587` 端口上与 `MUA` 进行通信。这种在 `MTA` 之间的传输方式具有某些安全影响。

### 理解发送者与信封发送者

正如图 14-2 所示，邮件包含 `Return-Path` 和 `From` 标头。两者之间的差异在随后的讨论中非常重要。`Return-Path` 指的是信封发送者地址。它在初始 `SMTP` 连接时获取，如果存在，则会被 `MTA` 保留。相反，`From` 标头在 `SMTP` 事务中没有这种关系，它可能会被 `MUA` 更改。当 `MUA` 读取邮件时，`Return-Path` 通常是隐藏的。任何形式的伪造都可能触发 `MTA` 的伪造警告标头。任何伪造的发送者都不应被视为可靠来源。

| From: | Delivered-To: | Received: | Return-Path: |
|---|---|---|---|
| pete@isecom.org | (gmail 7724 received from network): 28 May 2008 12:11:00 | from mail4@mail-pair.com [66.259.2.4] by kunatri.pair with SMTP; 28 May 2008 12:11:00 | <pete@isecom.org> |
| | from localhost (127.0.0.1) to mail4@mail-pair.com (Postfix) with SMTP ID E40DC9375 for <pete@isecom.org>; Wed, 28 May 2008 12:11:00 | from mr-out-0910.google.com [643.233.170.185] by mail4@mail-pair.com (Postfix) with SMTP ID E8AAD938CA for <pete@isecom.org>; | |
| | from mr-out-0910.google.com with SMTP 28 May 2008 09:12:07 (CDT) for <pete@isecom.org>; by mr-out-0910.google.com with SMTP 28 May 2008 09:12:07 (CDT) for <pete@isecom.org>; | | |
| | by 10.115.59.4 with SMTP ID m4w2738734wak104.121198751174113; Wed, 28 May 2008 08:11:51 (-0700) | | |
| | by 10.114.192.8 with HTTP; Wed, 28 May 2008 08:11:51 (-0700) | | |

图 14-2 消息与信封

### 邮件路由

`SMTP` 流量通常由你的客户端应用程序（`MUA`）用于连接 `MTA`，或者在 `MTA` 之间传输。邮件传输的最后阶段通常是 `MDA` 在信箱中完成的最终投递。

## 436 Hacking Exposed Linux: 安全秘密与解决方案

```
google.com             67916 IN NS ns1.google.com.
google.com             67916 IN NS ns2.google.com.
;; ADDITIONAL SECTION:
smt1.google.com.       600 IN A 216.239.57.25
smt2.google.com.       600 IN A 64.233.167.25
smtp3.google.com.      600 IN A 64.233.183.25
smtp4.google.com.      600 IN A 66.102.9.25
sns1.google.com.       152442 IN A 216.239.32.10
sns2.google.com.       152442 IN A 216.239.34.10
sns3.google.com.       152442 IN A 216.239.36.10
sns4.google.com.       152442 IN A 216.239.38.10
;; Query time: 157 msec.
;; SERVER: 140.105.134#53(140.105.134)
;; WHEN: Wed Oct 11 19:28:03 2006
;; MSG SIZE 316
</Verbatim listing>
```

`MX` 记录在邮件事务开始时被访问；查询后，`MTA`（邮件传输代理）/`MUA`（邮件用户代理）会与指定的服务器建立 `SMTP` 连接（通常是优先级最高的服务器）以投递消息。在这个示例中，所有 `MX` 记录返回了相同的优先级值（`10`）。优先级数字越低，优先级越高；优先级值为 `10` 的 `MX` 记录将在优先级值为 `20` 的 `MX` 记录之前进行尝试（但并非总是如此，例如当另一个 `MTA` 通过 `IP` 地址静态链接时）。

每个 `MTA` 都根据其路由配置决定如何处理消息（包括是否接受它）。基本上，`MTA` 在通过 `SMTP` 接收消息后会执行以下两项评估：

- 如果电子邮件地址被认为是本地的，消息将投递到本地邮箱箱（通常是服务器上的一个文件或目录，但也可能是数据库或其他花哨的东西）。
- 如果电子邮件地址不是本地的但允许中继，或者传入连接的 `IP` 地址允许中继，则消息会被接受并传递给另一个 `MTA`（静态配置的 `MTA` 或 `MX` 记录指定的 `MTA`）。

通常，允许基于 `IP` 地址中继的服务器是你的 `ISP` 提供的发送外邮件的服务器。允许中继特定域名的服务器是特定域的暴露服务器，它们并不一定托管邮箱本身（它们可能只是将消息传递给内部网络更深处的服务器）。当然，就像 `TCP/IP` 路由一样，中继和路由规则有无限可能，你可能会发现各种类型的中继和配置。

## 第 14 章：邮件服务

邮件消息的路径通过 `Received` 头部进行追踪：

```
<Verbatim listing 4>
Delivered-To: <andrea@isecom.org>
Return-Path: test@isecom.org
Received: from smtp.isecom.org (smtp.isecom.org [140.211.166.183])
    by azurra.isecom.org (8.13.6/8.13.6) by ESMTP id k4L5Uq014773
    (version=TLSv1/SSLv3 cipher=DHE-RSA-AES-256-SHA bits=256 verify=NO)
    for <andrea@isecom.org>; Sat, 20 May 2006 21:05:30 GMT
Received: from smtp.isecom.org (Postfix)
    id D138a64413; Sat, 20 May 2006 21:05:29 +0000 (UTC)
Delivered-To: andrea@isecom.org
Received: from localhost [127.0.0.1]
    by smtp.isecom.org (Postfix) with ESMTP id B87EF64409
    for <andrea@isecom.org>; Sat, 20 May 2006 21:05:29 +0000 (UTC)
Received: from smtp.isecom.org [127.0.0.1]
    by localhost (smtp.isecom.org [127.0.0.1]) (amavisd-new, port 10024)
    with ESMTP id 24780-13 for <andrea@isecom.org>
Sat, 20 May 2006 21:05:23 +0000 (UTC)
Received: from mail2.isecom.org;heic.pl [83.18.69.210]
    (using TLSv1 with cipher DHE-RSA-AES-256SHA (256/256 bits))
    (No client requested)
    by smtp.isecom.org (Postfix) with ESMTP id 6B37E6405
    for <andrea@isecom.org>; Sat, 20 May 2006 21:05:25 +0000 (UTC)
Received: from localhost [127.0.0.1]
    by mail2.isecom.org (Postfix) with ESMTP id BDF110D
    for <andrea@isecom.org>; Sat, 20 May 2006 23:12:55 +0000 (CEST)
Received: from mail1.isecom.org [127.0.0.1]
    by localhost ([127.0.0.1]) (amavisd-new, port 10024)
    with ESMTP id 11508-0 for <andrea@isecom.org>; Sat, 20 May 2006 23:12:42 +0000 (CEST)
Received: from localhost [192.168.0.5]
    by mail2.isecom.org (Postfix) with ESMTP id 5466BD2
    for <andrea@isecom.org>; Sat, 20 May 2006 23:12:41 +0000 (CEST)
Date: Sat, 20 May 2006 23:05:04 +0000
From: John Doe <test@isecom.org>
To: andrea@isecom.org
</Verbatim listing>
```

每个 `MTA` 在路由消息时都应该添加自己的追踪信息，但在消息路径中伪造头部是轻而易举的。每个 `MTA` 都有合法的头部（伪造消息路径中的每个服务器是不可能的）。一种常见的伪造是在 `HELO` 命令中传递无效域名（我们稍会在“初始阶段”讨论该命令的选项）。这是一个伪造域名的示例。你可以很快发现 `82.157.137` 并没有解析 `foo.com`。正确的 `IP` 信息由接收 `MTA` 保存且无法伪造；其目的是欺骗任何懒于检查其是否与 `IP` 地址匹配的人。

```
<Verbatim listing 5>
Received: from foo.com ([82.157.137])
by mail.isecom.org (81.3.8/81.7) with SMTP id k96DsnOS5189
for andrea; Fri, 6 Oct 2006 13:55:06 GMT
</Verbatim listing 5>
```

`MTA` 可以配置为反向解析。在这种情况下，你需要更好的头部：
