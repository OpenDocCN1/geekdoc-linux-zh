
| 550 | 操作未执行。 |

| 551 | 地址不是本地的。 |

| 552 | 事务失败。 |

| 553 | 邮箱无效。 |

| 554 | 事务失败。 |

每一个 `SMTP` 命令都会触发响应。从表 1.2 的响应代码可以很容易看出，`200` 和 `300` 系列的代码表示事务成功，而 `400` 系列的代码表示失败。大多数情况下，你并看不到这些。本地系统和远程系统协作的 `Sendmail` 程序静静地运行。要观察 `Sendmail` 与远程系统的交互，请以详细模式运行 `sendmail` 命令。

### 使用详细模式观察 `SMTP`

使用 `telnet` 连接到 `SMTP` 端口是熟悉 `SMTP` 协议的一种有用方法，当你想要完全绕过本地 `Sendmail` 副本来测试远程服务器的响应时，这是一个实用的测试技术。用户输入 `SMTP` 命令是基于对两个系统如何交互的最佳猜测来交换协议信息的。在大多数情况下，坐下来观察系统的实际交互要好。`sendmail` 命令的 `-v`（详细）选项可以让你正是这一点。列表 1.2 是使用详细模式发送的一封邮件。

列表 1.2 详细模式显示的协议

```
[craig$ sendmail -v -t
To: craig@wren
From: craig@ani
Subject: Test
Please ignore this test.
^
craig@wren... Connecting to wen.foobirds.org via esmtp...
220 wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 23 Oct 2000
11:32:-0400
>>> EHLO ani.foobirds.org
250-wren.foobirds.org Hello root@ani.foobirds.org [172.16.12.11],
pleased to meet you
250-ENHANCEDSTATUSCODES
250-EXPN
250-VERB
250-8BITIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250-AUTH DIGEST-MDS
250 HELP

>>> MAIL From:<craig@ani.foobirds.org> SIZE=73
250 <craig@ani.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 <craig@wren.foobirds.org>... Recipient ok
>>> DATA
```

```
354 输入邮件，以单独占一行的 "." 结束
>>>

250 NAA01047 消息接受投递
craig@wren... 已发送 (NAA01047 Message accepted for delivery)
正在关闭 wen.foobirds.org 的连接。

>>> QUIT
221 wen.foobirds.org 正在连接
```

除了详细（`verbose`）选项外，列表 1.2 中的 `sendmail` 命令还通过 `-t` 参数调用，该参数直接从键盘接受邮件消息。在列表 1.2 中，用户输入了 `To:` 地址、`From:` 地址、一个 `Subject:` 行以及一条单行消息。用户输入通过 `Ctrl+D` 结束。列表 1.2 中的其他所有内容都由 `Sendmail` 显示。

显示的行中有三行是 `Sendmail` 的信息消息。第一行显示了回复：投递地址 `craig@wren`、远程服务器名称 `wen.foobirds.org` 以及入站邮件传输器名称 `esmtp`。稍后你会听到很多关于投递三元组（`delivery triple`）的内容。另外两个由 `Sendmail` 创建的行出现在列表 1.2 的底部。这两行中的第一行显示了发送消息使用的 `ID`，在示例中为 `NAA01047`。第二行通知我们 `Sendmail` 已准备好关闭连接。

`>>>` 显示的大部分输出是 `SMTP` 协议交互。每一行以从本地系统发送到远程系统的命令开头的。每一行以响应代码开头的都是远程系统的响应。发送消息仅使用了六条命令：

- `EHLO`：这是问候命令。它与表 1.1 中显示的不同，因为这是通过扩展 `SMTP`（`Extended SMTP`）进行的扩展问候，该内容将在本章稍后部分进行介绍。

- `MAIL From:`：这是 `From:` 地址。`SMTP` 协议交换中的地址被更改为信封地址（`envelope addresses`），与作为消息数据一部分发送的报头地址（`header addresses`）是不同的，尽管报头地址和信封地址通常包含相同的值。在我们第 8 章“理解规则”中讨论地址重写和测试时，你会听到更多不同地址类型的更多。

- `RCPT To:`：这是 `To:` 地址。它也是一个信封地址。

- `DATA`：`DATA` 命令标记消息的开始。

- `-`：点（`.`）用于标记消息的结束。

- `QUIT`：`QUIT` 关闭会话。

`SMTP` 协议交换简单直接，可以使用 `sendmail -v` 选项轻松观察。观察 `SMTP` 会话可以让你看到邮件是否离开了你的系统，以及它是否被远程系统接受。当你怀疑出现问题时，这是非常有价值的信息。

列表 1.2 中没有显示的内容是 `Sendmail` 在 `DATA` 命令和结束点（`.`）之间发送的邮件消息。协议命令和响应的交换只是通过 `SMTP` 连接流过的信息的一小部分。`SMTP` 的真实目的是以邮件消息的形式承载数据。

## 基础邮件消息

基础电子邮件的格式在 `RFC 822`（“`ARPA Internet` 文本消息格式标准”）中定义。根据 `RFC 822`，一封电子邮件由两部分组成：报头（`headers`）和正文（`message body`）。正如名称所示，报头位于消息正文之前。正文与报头之间由空行分隔——该行只包含回车/换行符（`CRLF`）字符。正文由若干行组成，每行包含 `1000` 字节的七位 `ASCII` 文本。

## 消息报头

报头是单行文本，以报头名称（`RFC 822` 中的字段名）开头，并用冒号与与报头相关的变量数据隔开（这些数据在 `RFC` 中也称为字段体）。报头提供了用于投递邮件的信息的记录。报头告诉你消息是发给谁的、来自谁、何时发送的，以及消息在网络中移动时哪些计算机处理了它。

消息报头与我们在 `SMTP` 协议交换中看到的信封报头不同。信封报头限于 `From:` 和 `To:` 地址。消息中有 `From` 和 `To:` 报头，但还有许多可能的报头，它们在不观察 `SMTP` 交互的情况下，提供了更多关于消息如何被处理的信息。列表 1.3 显示了为列表 1.2 中发送的消息创建的报头。

### 列表 1.3 完整的邮件消息

```
From craig.ani.foobirds.org Mon Oct 23 11:42:34 2000

Return-Path: <craig@ani.foobirds.org>

Received: from ani.foobirds.org (root@ani.foobirds.org [172.16.12.1])

  by wren.foobirds.org (8.9.3/8.9.3) with ESMTP id NAA01047

  for <craig@wren.foobirds.org>; Mon, Oct 23 11:42:33 -0400

From: craig@ani.foobirds.org
```
