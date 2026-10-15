
# 第 20 章 电子邮件

要最好地阅读这些，请从 `Received` 行开始读，但要从发送方开始。这封来自 David Schweikert 在 schweikert.com 家庭机器的邮件发送到他的邮件服务器 (mail.schweigert.ch)，在那里经过了病毒扫描。它被转发给了收件者 evi@atrust.com。然而，接收主机 mail-relay.atrust.com 将其发送到了 sailing@gmail.com，在那里进入了 Gmail 邮件。

在报头中间，你会看到 SPF 验证失败。这是因为 Google 检查了 mail-relay.atrust.com 的 IP 地址，并将其与 schweweigert.ch 的 SPF 记录进行比较；当然，它们是不匹配的。SPF 记录识别伪造的固有弱点在于它们对于经过中继的邮件无效。

你还可以看到所使用的 MTA（schweigert.ch 上的`Postfix`，atrust.com 上的`sendmail` 8.12），在这种情况下你还可以看到病毒扫描是在运行 Debian Linux 的机器上通过端口 10.024 的`amavisid-new`执行的。你可以跟踪邮件从中欧夏令时区 (CEST +0200) 到科罗拉多 (-0600)，再到 Gmail 服务器 (PDT -0700) 的进度；这些数字是本地时间与 UTC（协调世界时）之间的差异。报头中有很多信息！

```
Received-SPF: neutral (google.com: 63.173.189.2 is neither permitted denied by best guess record for domain of smotherl39@sherman.dp.ua) client-ip=63.173.189.2.
Authentication-Results: mx.google.com; spf-neutral (google.com: 63.173.189.2 is neither permitted nor denied by best guess record for domain of smotherl39@sherman.dp.ua) smtp:mail=smotherl39@sherman.dp.ua
Received: from SpeedTouch.in (187-10.167-249.dsl.telesp.net.br [187.10.167.249 (by forged)]) from 187.10.167.249 by relay2trifle.net, Mon, 19 Oct 2009 13:59: ...
From: "alert@atrust.com" <alert@atrust.com>
To: <@atrust.com>
Subject: A new settings file for the ned@atrust.com mailbox
Date: 19 Oct 2009 13:59:12 -0300
```

根据`From`头部，此消息的发送者是 alert@atrust.com。根据`Return-Path`头部（该头部包含信封发送者的副本），源者是 smotherl39@sherman.dp.ua，这是一个位于乌克兰的地址。处理该消息的 MTA 位于 IP 地址 187.10.167.249，位于巴西。这些垃圾邮件发送者……

Google 的 SPF 检查失败了，这次得到的是“中性”（neutral）结果，因为域名 sherman.dp.ua 并没有 SPF 记录可以与 mail-relay.atrust.com 的 IP 地址进行比较。

收件人信息至少部分是混乱的。头部显示消息是给 ned@atrust.com 的。然而，信封收件人地址包含了 evi@atrust.com，以便将消息转发到 salingevi@gmail.com 进行投递。

## 20.3 SMTP 协议

简单邮件传输协议（SMTP）及其扩展版本 ESMTP 已经在 RFC 系列（`RFC5321`）中标准化，并用于邮件系统各个部分之间的大多数邮件交接：

- 当消息被注入邮件系统时，从 UA 到 MSA 或 MTA
- 当消息开始投递旅程时，从 MSA 到 MTA
- 从 MTA 或 MSA 到反病毒或反垃圾邮件扫描程序
- 当消息从从一个站点转发到另一个站点时，从 MTA 到 MSA
- 当消息被投递到本地消息服务器时，从 MTA 到 DA

由于消息格式和传输协议都是标准化的，因此我的 MTA 和你们的 MTA 不需要相同，甚至不需要知道对方的身份；它们只需要都支持 SMTP 或 ESMTP 即可。你们的各种邮件服务器运行不同的 MTA 且运行良好。

5. 留注意的是，头部中的许多行（包括 `Received` 行）可能被伪造。使用这些数据时请务必极其谨慎。

### SMTP 错误代码

顾副其实名，SMTP 非常简单。MTA 连接到你的邮件服务器并本质上说：“这里有一条消息；请将其投递给 user@your.domain。” 你的 MTA 说：“OK。”

要求严格遵守 SMTP 协议已成为一种对抗垃圾邮件和恶意软件的技术，因此对于邮件管理员熟悉该协议至关重要。该语言只有几个命令；表 20.2 显示了最重要的几个。

#### 表 20.2 SMTP 命令

| 命令 | 功能 |
| --- | --- |
| `HELLO hostname` | 如果使用 SMTP，则识别连接的主机 |
| `EHLO hostname` | 如果使用 SMTP，则识别连接的主机 |
| `MAIL FROM: revpath` | 启动邮件事务（信封发送者） |
| `RCPT TO: fwdpath` | 识别信封收件人 |
| `VRFY address` | 验证地址是否有效 |
| `EXPN address` | 显示别名的展开 |
| `DATA` | 开始消息正文 |
| `QUIT` | 结束交换并关闭连接 |
| `RSET` | 重置连接状态 |
| `HELP` | 打印 SMTP 命令摘要 |

- a. 消息可以有多个 `RCPT` 命令。
- b. 通过在自己的行输入点（.）结束正文。

### You had me EHLO

ESMTP 发送者使用 `EHLO` 而不是 `HELO` 开始对话。如果对方理解并响应 OK，参与者将协商扩展并达成最小公约数。如果过程对 `EHLO` 返回错误，则 ESMTP 发送者将回退到 SMTP。但今天，一切都使用 ESMTP。

一个投递邮件的典型 SMTP 连接如下：`HELO` 或 SMTP，`MAIL FROM;` `RCPT TO;` `DATA`，以及 `QUIT`。发送者说话，收件人提供错误代码和确认。SMTP 和 ESMTP 都是基于文本的协议，因此在调试邮件系统时可以直接使用它们。只需 `telnet` 到端口 25 并开始输入 SMTP 命令。RFC 定义了一组错误代码。这些最初是三位数字（例如 `550`），每个数字单独解释。第一个数字 2 表示成功，4 表示临时错误，5 表示永久错误。三位错误代码系统无法扩展，因此 `RFC3463` 对其进行了重构以增加灵活性。它定义了名为 `DSN` 的扩展格式。`DSN` 的格式为 `X.X.X` 而不是旧的 `XXX`，每个 X 必须是 2、4 或 5。第二个数字指定主题，第三个提供详细信息。新系统使用第二个数字来区分主机错误和邮件错误。我们在表 20.3 中列出了一些 `DSN` 代码。`RFC3463` 的附 A 显示了所有的。

#### 表 20.3 RFC3463 投递通知

| 临时 | 永久 | 含义 |
| --- | --- | --- |
| `4.2.1` | `5.2.1` | 邮箱已禁用 |
| `4.2.2` | `5.2.2` | 邮箱已满 |
| `4.2.3` | `5.2.3` | 消息太长 |
| `4.4.1` | `5.4.1` | 主机无响应 |
| `4.4.4` | `5.4.4` | 无法路由 |
| `4.5.3` | `5.5.3` | 收件人过多 |
| `4.7.1` | `5.7.1` | 未授权投递，消息被拒绝 |
| `4.7.*` | `5.7.*` | 站点违规 |

### SMTP 身份验证

`RFC2954` 定义了原始 SMTP 协议的扩展，允许客户端向邮件服务器识别身份。服务器可能允许客户端通过转发邮件。协议支持多种不同的身份验证机制。交换如下：

- 客户端说 `EHLO`，宣布它支持 SMTP。
- 服务器响应并发布其身份验证机制。
- 客户端说 `AUTH` 以及想要使用的特定机制，可选包含其身份验证数据。
- 服务器接受随 `AUTH` 发送的数据，或与客户端启动挑战/响应序列。
- 服务器接受或拒绝身份验证尝试。要查看服务器支持哪些身份验证机制，你可以 `telnet` 到端口 25 并说 `EHLO`。例如，这里与邮件服务器 relay.atrust.com 的一个截断对话（我们输入的命令加粗）：

```
sol$ telnet mail-relay.atrust.com 25

Trying 192.168.2.10...

Connected to mail-relay.atrust.com.

220 mail-relay.atrust.com ESMTP Mail Service Tue, 20 Oct 2009 14:28:53 -0600
```
