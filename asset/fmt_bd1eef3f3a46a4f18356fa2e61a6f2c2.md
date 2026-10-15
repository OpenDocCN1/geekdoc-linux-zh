
垃圾邮件发送者使用在互联网寻找开放中继的工具。如果你想要一个安全的、相对无忧的网络，我建议你采取行动阻止你的邮件服务器进行中继。

## 我的邮件服务器容易受到攻击吗？

要找到你的邮件服务器（或任何邮件服务器）是否受到开放中继攻击，请执行以下测试：

1. 登录你的 Linux 系统（或任何带有 `nslookup` 和 `telnet` 客户端的系统）。
2. 运行 `nslookup -q=mx domain.com` 命令，`domain.com` 是你想要查找 MX 记录的域名。MX 记录在 DNS 数据库中指向域名的邮件服务器。在示例中，我使用一个虚拟域名 `openrelay-ok.com` 作为示例域名。注意，该域名应该至少配置有一个邮件服务器。
3. 运行 `telnet mailserver-host 25` 命令，`mailserver-host` 是邮件服务器的主机名。我运行 `telnet openrelay-ok.com 25` 连接到邮件服务器的 25 端口（标准 SMTP 端口）。
4. 连接后，输入 `ehlo localhost` 命令向邮件服务器说 `hello`。邮件服务器回复欢迎消息并等待输入。
5. 输入 `MAIL FROM:you@hotmail.com` 告诉邮件服务器你想发送一封到 `openrelay-ok.com` 地址的邮件。邮件服务器使用 `250 you@hotmail.com...` 响应确认发送者地址。
   - 如果服务器返回不同的消息，说明发送者的邮件地址是不可接受的。如果你仍然收到负面响应，说明服务器没有接受该邮件，这意味着服务器可能不允许中继。如果收到 `250 okay` 消息，继续。
   - 在这一点，你指示邮件服务器你想发送一封来自 `you@hotmail.com` 的邮件。
6. 使用 `RCPT TO:you@yahoo.com` 命令告诉服务器你想将其发送到 `yahoo.com`。如果服务器通过发送类似 `250... ok...` 的响应来接受它，你就发现了一个开放中继。这是因为邮件服务器接受了来自 `you@hotmail.com` 的邮件，并同意将其发送 `yahoo.com`。如果你不是在 `yahoo.com` 服务器上执行此操作，那么邮件服务器就不应该接受来自域外的邮件并发送给其他人。这是一个开放中继；垃圾邮件发送者可以使用此服务器向域外的人发送邮件，如列表 17-1 所示。

### 列表 17-1：使用开放中继

```
$ telnet openrelay-ok.com 25
Trying 192.168.1.250...
Connected to openrelay-ok.com.
Escape character is '^'.
220 openrelay-ok.com SMTP Sendmail 8.9.3/8.9.3;
, 31 Dec 2000 11:04:33
EHLO localhost
250-openrelay-ok.com Hello [192.168.1.250], pleased to meet you
250-EXPN
250-VERB
250-BITIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250 HELP
MAIL FROM:you@hotmail.com
250 you@hotmail.com... Sender ok
RCPT TO:you@yahoo.com
250 you@yahoo.com... Recipient ok
DATA
354 Entry mail, end with "." on a line
THIS MAIL SERVER CAN AN OPEN RELAY!
FUTURE SPAM WILL BE SERVED HERE!
NEED TO BLOCK THIS ASAP!
250 Message accepted for delivery
```

如果你在不允许邮件邮件的服务器上执行前面的测试，输出看起来非常不同。这是一个名为 `mailserver.com` 的邮件服务器 25 端口的 Telnet 会话示例，显示了受保护邮件服务器的测试情况；得到如下输出：

```
[root@server ~] telnet localhost 25
Trying 172.20.15.250...
Connected to mailserver.com.
Escape character is '^'.
220 mailserver.com ESMTP Sendmail 8.11.0/8.11.0; Sun, 31 Dec 2000 14:07:15
HELO localhost
250-mailserver.com Hello [172.20.15.250], pleased to meet you
250-ENANCEDSTATUS
250-BMTIME
250-SIZE
250-DSN
250-XUS
250-AUTH DIGEST-MD5
250 HELP
MAIL FROM:you@hotmail.com
250 you@hotmail.com... Sender ok
RCPT TO:you@yahoo.com
550 5.7 you@yahoo.com... Relaying denied
```

列表显示邮件服务器拒绝了 `RCPT TO:you@yahoo.com` 命令给出的收件地址。

![](img/6d17ba5e3d85ca2b04a3ba254c_0.png)

## 安全 Sendmail

Sendmail 是发行最广泛的 MTA，目前是 Red Hat Linux 的默认设置。幸运的是，新版本的 Sendmail 默认不允许开放中继。最新版本中可用，我建议你从 RPM 镜像站点或直接从官方网站 `www.sendmail.org` 下载并安装最新版本的 Sendmail。

我强烈建议你同时下载二进制版本（来自 `www.rpmfind.net` 等 RPM 镜像站点）和源码发行（来自 `www.sendmail.org`）。使用 `rpm -iv sendmail-version.rpm` 命令安装 RPM 版本，其中 `sendmail-version.rpm` 是 Sendmail 的最新二进制文件。安装二进制版本可以确保为你创建配置文件和目录。

你可以决定不安装二进制 RPM，而是直接从头编译并安装源码发行。源码发行没有花哨的安装程序，因此创建和配置文件和目录是大量工作。为了避免过多的手动配置，我只需安装二进制发行，并在其之上编译并安装源码。

此外，将源码发行 tar 包解压到合适的目录，例如 `/usr/src/redhat/SOURCES`。然后按照顶层 readme 文件中的指令编译并安装 Sendmail。在接下来的章节中，我将讨论与对抗垃圾邮件相关的各种 Sendmail 安全和控制功能。你必须将它们整合到位于 `/etc/mail/` 的 Sendmail 配置文件中。不要直接修改该文件。相反，要修改 `whatever.mc` 文件。记住这些规则：

- 备份你当前的 `/etc/mail/cf` 文件。
- 在源码分发的 `cf` 目录中运行 `m4 /etc/mail/cf.new > /etc/mail/cf` 命令。
- 使用 `linux-dnsbl.mc` 替换 `whatever.mc`。`linux-dnsbl.mc` 文件在源码分发中，但它是当你创建邮件服务器时生成的。

在后面的章节中，当我提到使用 `FEATURE(featurename)` 语法的 Sendmail 功能时，将其添加到 `whatever.mc` 文件并重新生成 `/etc/mail/cf`。

# 控制邮件中继

最新版本的 Sendmail 8.11.2 允许你对 MTA（邮件传输代理）的邮件中继功能进行高程度的控制。如前所述，邮件中继默认是禁用的。Sendmail 为合法用途提供了邮件中继控制。要启用此处讨论的配置控制，你需要在 m4 宏文件中包含以下功能，以生成相应的 `/etc/mail/sendmail.cf`。

## 使用 FEATURE(ACCESS_DB)

此功能启用访问控制数据库，该数据库存储在 `/etc/mail/access` 文件。该文件的条目具有以下语法：

```
LHS(tab)RHS
```

- 左侧 `LHS` 可以表 17-1 所示的任意项。
- `(tab)` 是制表符。
- 右侧 `RHS` 可以表 17-2 所示的任意项。

表 17-1：`/ETC/MAIL/ACCESS` 中条目的左侧

| LHS | 含义 |
| --- | --- |
| user@host | 一个电子邮件地址 |
| IP address | 邮件服务器的 IP 地址 |
| Hostname or domain | 邮件服务器的主机名 |
| From: user@host | 来自名为 user@host 的电子邮件地址的邮件 |
| From: hostname or From:domain | 来自主机名或域名的邮件 |
| To: user@host | 发往名为 user@host 的电子邮件地址的邮件 |
