
A 记录和 MX 记录并不一定一致，这正是最棒的地方。例如，假设你有两个主机，一个是 `client.company.com`，另一个是你的电子邮件网关，名为 `gateway.company.com`。你为 `client.company.com` 的 IP 地址拥有 A 记录。如果这台机器可以直接处理邮件，那么 MX 记录可以不存在，也可以指向 `client.company.com`；结果是相同的，发送到 `username@client.company.com` 的邮件将发送到这台机器。

另一方面，如果你想让 `gateway.company.com` 处理所有发送给 `client.company.com` 的邮件，你可以让 `client.company.com` 的 MX 记录指向 `gateway.company.com`，这样所有发送给 `client.company.com` 的邮件将会被递送到 `gateway.company.com`。此时，`gateway.company.com` 可以决定如何处理这封邮件——保留它（本地递送）或路由到其他地方。

# 安装和发送 sendmail

`sendmail` 软件以及关于它的所有信息可以在 `http://www.sendmail.org` 找到。最新版本在该网站上非常显眼。网页还包含指向其他与 `sendmail` 及非 `sendmail` 相关网站的链接。

`sendmail` 在许多 Unix 变体中都可以开箱即编译。你只需要编辑几个文件，以针对你想要编译 `sendmail` 的 Unix 变体调整各种参数。

要调整的第一个文件是 `Makefile` 文件，它包含了所有与你所使用的 Unix 版本编译标志相关的参数。第二个文件名为 `conf.h`，包含了额外的与 C 语言相关的配置细节。该文件为特定版本的 Unix 配置了 `sendmail` 配置，因为它还包含了你可能选择开启的选项。如果你调整了这两个文件，只需执行启动 `sendmail` 的命令即可。

当你拥有二进制程序后，下一步是构建一个名为 `sendmail.cf` 的配置文件，它基本上告诉 `sendmail` 它的行为模式，例如使用主机上的哪些资源、如何处理电子邮件地址、从谁接收邮件等。

一种粗糙、原始且低效的方法是实际上使用 `sendmail.cf` 文件并对其进行编辑。这种方法可能很粗糙，但老手们过去就是这样做的。这种方法也是 `sendmail` 赢得“可怕”名声的原因。事实上，这个文件的规则类似于二进制文件。

几年前，`sendmail` 的制作者 Eric Altman 决定是时候结束他自己手动维护 `sendmail` 的时代了。他决定包含一个工具包，用于从 M4（一个处理宏的工具包）源文件构建 `sendmail.cf` 文件。M4 文件要美观且易于维护得多。你无法逃避 `sendmail` 配置文件的丑陋，但正如你将在本章中看到的，`sendmail` 并没有那么可怕。

在能够实际构建 `sendmail` 配置文件之前，你必须获取 GNU（代表 GNU's Not Unix；这是一个递归缩写）M4 软件包。它提供了更高级的功能，而 `sendmail` M4 文件正使用了这些功能。使用 Unix 随带的普通 M4 软件包将无法工作。

![](img/c0f2cd6655e598a6e6ffb6a15368bc67_629_0.png)

GNU M4 软件包包含在随书附的光盘中（连同 `sendmail` 和相关工具）。

# SMTP 和邮件消息

`sendmail` 程序在 Unix 主机上作为守护进程运行，并监听 TCP 25 端口。当远程主机想要向监听的 `sendmail` 发送电子邮件时，它使用简单邮件传输协议（SMTP）。正如其名称所示，SMTP 是一个简单的协议。事实上，你可以尝试一下。通过 `telnet` 到任何 25 端口的主机复制列表 28-1 所示的 SMTP 事务示例。斜体部分是由我们输入的。在列表 28-1 中，我们输入的 SMTP 命令向 `smtp.domain.com` 发送邮件。

## 列表 28-1：一个 SMTP 事务示例

```
220 smtp.domain.com 8.8/8.8: Tue, 9 Dec 1999 20:34 -0500 (EST)
HELLO remote.company.com
250 smtp.domain.com [23.45.67], pleased to meet you
MAIL FROM: yves@mcgill.ca
250 yves@mcgill.ca... Sender ok
RCP TO: yves@mcgill.ca
250 yves@mcgill.ca... Recipient ok
DATA
354 Enter mail, end with "." on a line
This is a test.
250 Message accepted for delivery
QUIT
```

由于 SMTP 是基于文本的协议，它也被用于伪造邮件。例如，如果我们输入 `MAIL FROM: president@whitehouse.gov`，邮件看起来就像来自美国总统。当然，`sendmail` 有检测这种欺的功能，但许多邮件阅读器并不显示伪造信息。伪造邮件的尝试通常是成功的。邮件头中包含了价值的信息，包含各种信息，例如邮件在递送到你的邮箱箱之前的完整路径、它是直接发送给你的还是由他人转发的等。

我们自己的邮件阅读器会向我们显示列表 28-1 中的邮件（如列表 28-2 所示）。基于 Unix 的邮件阅读器如 `pine` 显示列表 28-3 中的邮件。你可以看到列表 28-3 包含比列表 28-2 多得的信息。邮件的路径越长，这些信息看起来越混乱，但有一些技巧可以使其易读。

## 列表 28-2：常见的邮件阅读器显示

```
From: yves@mcgill.ca
Date: Tue 12/9/99 08:34 PM
Subject: This is a test.
```

## 列表 28-3：邮件的完整显示

```
Received: from smtp.domain.com (root@smtp.domain.com [23.45.67.89]) by maildrop.domain.com (8.6.12/8.6) id UAA2954; Tue, 9 Dec 1999 20:34:50 -0500
From: yves@mcgill.ca
Received: from remote.company.com [162.12.13] by smtp.domain.com (8.8.8/8.8) with SMTP ID UAA2682 for yves@domain.com; Tue, 9 Dec 1997 20:34:28 -0500 (EST)
Date: Tue, 9 Dec 1997 20:34:28 -0500 (EST)
Message-Id: <19971210134.UAA2682@smtp.domain.com>
Apparent-To: yves@domain.com

This is a test.
```

例如，如果你想追踪邮件在到达你之前之前的路径，你可以从查看最后一个 `Received` 头行开始。列表 28-3 中的这一行显示名为 `smtp.domain.com` 的主机接收了来自名为 `remote.company.com` 的主机的邮件，以及传输发生的日期（行的最后一个字段）。在 `remote.company.com` 主机名之后是该主机名的括号重复，它只是主机名后跟其 IP 地址。如果主机名与第一个不同，你就有早期迹表明邮件是伪造的。此外，如果 IP 地址与主机名不符（可以使用 `nslookup` 进行验证），则是邮件伪造的另一个迹象。

在这个示例中，你还可以看到路径上每个节点运行的 `sendmail` 版本。SMTP ID（有时是 ESMTP ID）是一个标签，用于唯一标识源自机器的电子邮件。如果邮件是伪造的，SMTP ID 提供了一个键值，用于在 `sendmail` 日志中搜索有关此邮件的更多信息。

你可能会遇到大量的头字段。只有极少数是高度重要的，例如 `Received`、`From`、`To`、`Date`、`Message-ID` 等。

> 注意：以 X 开头的头字段不应被 `sendmail` 或邮件阅读器处理；这些字段仅供参考。

当 `sendmail` 接收到邮件消息时，它会处理 `sendmail.cf` 文件中的一组规则。该 `sendmail.cf` 文件位于你编译 `sendmail` 之前编辑两个文件时所指定的位置。

# sendmail 的基础配置

首先，本节将对比 M4 源文件和生成的 `sendmail.cf` 文件中的基础配置项进行比较。列表 28-4 列出了与基础配置项相关的 M4 宏，而列表 28-5 列出了这些相同配置项出现在 `sendmail.cf` 文件中的形式。

## 第 28 章 - 电子邮件服务器 597
