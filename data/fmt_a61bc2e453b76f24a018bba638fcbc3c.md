
| `Restrictmailq` | 限制 `mail` 命令。启用此选项时，只有超级用户和队列的所有者可以运行 `mail`。 |

| `Restrictgrun` | 限制 `-q`。启用此选项时，只有队列的所有者可以运行 `mail`。 |

| `Norecepts` | 不返回状态。 |

| `Goaway` | 不允许 SMTP。 |

| `Autwarnings` | 在头部中插入 `X-Warning:` |

### 反垃圾措施

滥防御系统的实时黑名单（RBL）可用于通过 `sendmail` 服务器自动拦截已知的垃圾邮件发送者。RBL 的网站为 `http://maps.vix.com`

你可以将 RBL 视为一个已知垃圾邮件发送者的数据库。通过查询数据库，你可以发现谁是垃圾邮件发送者并拒绝相关域的服务。

为了理解 RBL 是如何工作的，请考虑一个示例。假设你想知道 IP 地址为 `127.0.0.2` 的特定域名是否在 RBL 中。运行以下命令：

```
nslookup -q=a 2.0.0.127.rbl.maps.vix.com
```

这将显示前面的主机（`2.0.0.127.rbl.maps.vix.com`）的 IP 地址为 `127.0.0.2`。在这里，你通过反转 IP 字节并在末尾添加 `rbl.maps.vix.com` 将 IP 地址作为一种特殊的主机名。然后你查找该主机的（地址）记录，它返回了你已知的 IP 地址（`127.0.0.2`）。

# 第 10 章：邮件服务

已经已知。换句话说，如果你知道可能的垃圾邮件发送者的 IP 地址，你只需执行上述测试，查看是否能返回一个 IP 地址。如果你从此类查询中获得了相同的 IP 地址，则说明该 IP 已列在 RBL 中。你可以执行另一个查询来获取文本记录 (`txt`)，如下所示：

```
nslookup -q=txt 2.0.0.127.rbl.maps.vix.com
```

这将显示以下内容：

```
2.0.0.127.rbl.maps.vix.com text = "Blackholed - see URL:http://maps.vix.com/cgi-bin/lookup?127.0.0.2" *
```

如果你用于创建特殊主机名的 IP 地址未列在 RBL 中，你将无法从 A（地址）记录或 TXT（文本）记录中获得任何响应，并可以假设该 IP 不在列表中。由于 RBL 为测试目的提供了 `127.0.0.2` IP 地址，因此它列在 RBL 中，你会在名称服务器查询中获得上述响应。

因此，MAP RBL 是一种基于 DNS 的垃圾邮件检查和拦截系统，可以通过查询它来确定特定 IP 地址是否被拦截作为垃圾邮件发送者。你可以通过两种方式使用 RBL：

- 与 Maps RBL 签署协议，将整个数据库传输到本地主机，并为供自己使用创建一个本地 RBL。
- 逐个查询主 RBL 数据库。

`sendmail` 8.10.x 带有 RBL。适用于最新版本的 SuSE Linux RPM 允许在 `/etc/sendmail.cf` 中启用 RBL，因此你不需要进行任何配置。要测试你的 `sendmail` 中的 RBL 配置，请运行：

```
sendmail -bt
```

在地址测试提示符处，输入：

```
.D(client_addr)127.0.0.1
Basic_check_relay <>
```

输出如下：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> .D(client_addr)127.0.0.1
> Basic_check_relay <>
rewrite: ruleset 190 input: <
rewrite: ruleset 190 returns: OKSOFAR
```

这告诉你地址 `127.0.0.1`（环回地址）在 RBL 中未被拦截，因为重写结果为 `OKSOFAR`。现在使用 `127.0.0.2` 重复上述测试（RBL 提供的测试 IP，它在 RBL 中被拦截）。你应该看到类似下面的内容的输出：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> .D(client_addr)127.0.0.2
> Basic_check_relay <
rewrite: ruleset 190 input: <
rewrite: ruleset 190 returns: ## $5 . 7 . $1: "Mail from
127 . 0 . 0 . 2 " refused by blackhole site.maps.vix.com. Email
from your server is blocked. Contact your local Systems
Administrator or ISP.
```

显然，该 IP 在 RBL 中被列入黑洞或黑名单，因此 `sendmail` 不允许其中继消息。

![](img/1d90939eac39ca76d12e353542e54751_313_0.png)

## 设置 POP 和 IMAP 服务

POP 和 IMAP 是客户端-服务器系统，极大地简化了在局域网、广域网和互联网上使用电子邮件的工作。传统方法要求在网络客户端上运行 `sendmail`。`sendmail` 系统会与中继系统通信，中继系统与外部世界通信。这意味着每个客户端都需要自己的 `sendmail` 配置，维护起来非常困难。

POP 和 IMAP 配置非常简单。你必须将邮件客户端指向 POP 或 IMAP 服务器以接收邮件，指向 SMTP 服务器以发送邮件，并配置你的用户名和可选的密码。从那时起，每当你发送或接收邮件，你的客户端都会为你工作。当出现新版本的 `sendmail` 时，你需要进行一些维护或配置。注意 POP 比 IMAP 简单，而 IMAP 更强大。

## 它们如何工作？

POP 和 IMAP 服务器以类似于 `sendmail` 的方式监听端口。默认情况下，POP 监听端口 `110`，IMAP 监听端口 `143`。`inetd` 系统通常用于按需启动服务器。POP 是一种相对简单的协议。POP 服务器包含在 `pop.rpm` 包中，未作为最小 SuSE 安装的一部分。你可以通过 `root` 登录、挂载光盘，然后按照以下方式安装：

```
rpm -ivh /cdrom/suse/n/pop.rpm
```

接下来，按照以下方式连接到 POP 服务器（使用 `localhost`）：

```
telnet localhost 110
```

收到 POP 服务器的以下消息：

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
+OK 2.5 at localhost starting.
```

输入以下 POP 命令告诉服务器打开哪个用户的邮箱：

```
USER paul
```

服务器响应：

```
+OK Password required for paul.
```

使用以下命令输入密码：

```
PASS whatever
```

POP 服务器响应：

```
+OK paul has 3 messages (304 octets).
```

你可以看到服务器上 `paul` 有三条邮件。使用以下 POP 命令：

```
LIST
```

POP 服务器回复：

```
+OK Mailbox list follows
1 213
2 434
3 447
```

要检索其中一条消息，输入以下命令：

```
RETR 3
```

服务器返回带有以下响应的消息：

```
+OK 447 octets
Return-Path: <paul>
Received: (from paul@localhost) by veracruz.paunchy.net (8.9.3/SuSE Linux 8.9.3-0.1) id LAA3684 for paul: Sun, 18 Jun 2000 11:31:25
Date: Sun, 18 Jun 2000 11:31:25
From: paul@veracruz.paunchy.net
Message-Id: <200006181731LAA3684@veracruz.paunchy.net>
To: paul@veracruz.paunchy.net
Subject: test again for pop
X-UIDL: a44fefb3db0f27c4abc3830cfe
```

`pop` 将完成。因此，每个 POP 事务都很简单。现在查看你如何设置支持 POP 的系统。

> 参考 RFC 1939 以了解更多关于 POP 的信息。你也可以咨询 `/usr/doc/packages/pop` 和 `/usr/doc/packages/imap` 目录下的文档。

## 配置 POP 服务
