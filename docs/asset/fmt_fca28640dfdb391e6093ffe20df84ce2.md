
MX 记录位于邮件事务的开始；查询后，`MTA`/`MUA` 会与指定的服务器建立 `SMTP` 连接（通常是优先级最高的服务器）以交付消息。在这个示例中，所有 MX 记录都返回相同的偏好值（10）。偏好值越低，优先级越高；偏好值为 10 的 MX 将偏好值为 20 的 MX 之前尝试（但并不总是如此，例如当另一个 `MTA` 通过 IP 地址静态链接时）。

每个 `MTA` 根据其路由配置决定对消息进行何处理（包括是否接受）。基本上，`MTA` 在通过 `SMTP` 接收消息后会执行以下两个评估：

- 如果电子邮件地址被认为是本地的，消息将投递送到本地信箱（通常是服务器上的一个文件或目录，但也可能是数据库或其他奇事物）。
- 如果电子邮件地址不是本地的但允许中继，或者入连接的源 IP 地址允许中继，则接受消息并传递给另一个 `MTA`（静态配置的 `MTA` 或 MX 记录）。

允许基于 IP 地址中继的服务器用于发送发送邮件。允许中继特定域名的服务器并不一定托管信箱（它们只是将消息传递到内部网络的其他服务器）。当然，像 TCP/IP 路由这样的规则是无限的，你可能会发现各种邮件路径是通过 `Received` 头部追踪的：

```
<Verbatim listing 4>

Delivered-To: <andrea@example.org>

Return-Path: test@example.org

Received: from smtp.example.org (smtp.example.org [140.211.166.183])

    by azurra.example.org (8.1/3) with ESMTP id k4L5U0q0147

    (version=TLSv1/SSLv3 cipher=DHE-RSA-AES256-SHA bits=256 verify=No)

    for <andrea@example.org>; Sat, 20 May 2006 21:05:30 GMT

Received: by smtp.example.org (Postfix)

    id D138a6413a; Sat, 20 May 2006 21:05:29 (UTC)

Delivered-To: <andrea@example.org>

Received: from localhost [127.0.0.1])

    by smtp.example.org (Postfix) with ESMTP id B87EF6409

    for <andrea@example.org>; Sat, 20 May 2006 21:05:29 (UTC)

Received: from smtp.example.org ([127.0.0.1])

    by localhost (smtp.example.org [127.0.0.1]) (id-new, port 10024)

    with ESMTP id 24780-3 for <andrea@example.org>

    Sat 20 May 2006 21:05:23 (UTC)

    using TLSv1 with cipher DHE-RSA-AES256-SHA (256/256 bits)

    (No client requested)

    Received: by smtp.example.org (Postfix) with ESMTP id 6B37E6405

    for <andrea@example.org>; Sat, 20 May 2006 21:05:25 (UTC)

Received: from localhost (localhost.example.org [127.0.0.1])

    by mail2.example.org (Postfix) with ESMTP id BDF11B0D2E

    for <andrea@example.org>; Sat, 20 May 2006 23:12:55 (CEST)

Received: from example.org ([127.0.0.1])

    by localhost ([127.0.0.1]) (id-new, port 10024)

    with ESMTP id 11508-04 for <andrea@example.org>; Sat, 20 May 2006 23:12:42 (CEST)

Received: from localhost (unknown [192.168.0.5])

    by mail2.example.org (Postfix) with ESMTP id 5466B0D2C

    for <andrea@example.org>; Sat, 20 May 2006 23:12:41 (CEST)

Date: Sat, 20 May 2006 23:05:04 +0200

From: John Doe <test@example.org>

To: andrea@example.org

</Verbatim listing>
```

每个 `MTA` 在路由消息时都会添加自己的追踪，但添加伪造的 `Received` 头部来混淆消息是非常简单的。由于每个 `MTA` 都会添加 `Received` 头部，在某个时刻你会拥有合法的头部（垃圾邮件者覆盖每一个服务器是不可能的）。

# Hacking Exposed Linux：Linux 安全秘密与解决方案

一种常见的伪造是在 `HELO` 命令中传递无效域名，这是初始问候命令（我们稍后将在“初始阶段”中讨论该命令的验证选项）。这是一个伪造域名的例子。你可以很快发现 82.157.137 并不解析到 foo.com。

```
<Verbatim listing 5>

Received: from foo.com ([82.157.137])

by mail.example.org (83.18/8/13.7) with SMTP id k96DsnOS0189

for andrea; Fri, 6 Oct 2006 13:55:06 GMT

</Verbatim listing>
```

`MTA` 可以配置为执行反向解析。在这种情况下，你需要一个更好的头部：

```
<Verbatim listing 6>

Received: from host137-175.pool8252.interbusiness.it ([82.157.137])

by mail.example.org (83.18/8/13.7) with SMTP id k96DsnOS0189

for andrea; Fri, 6 Oct 2006 13:55:06 GMT

</Verbatim listing>
```

某些 `MTA` 足够友好，报告可能的伪造（因为 213.155.199.178 的域名无法解析回 IP 地址，这在拨号池中很常见）：

```
<Verbatim listing 7>

Received: from [213.155.199.178] (hwads1-213-155-199-178.telvia.it [213.155.199.178])

(may be forged)by dns1.vanja.com with ESMTP<9C> id k77LAWAi00576

(Version=TLSv1/SSLv3 cipher=DHE-RSA-AES256-SHA bits=256 verify=NOT)

Mon, 7 Aug 2006 23:11:00 +0200

</Verbatim listing>
