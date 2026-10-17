
你可能会被列入黑名单。被垃圾邮件滥用邮件账户的人可以将你的邮件服务器信息修复到黑名单中。这可以阻止你向自动检查黑名单（如 MAPS 邮件滥用预防系统实时黑名单）的域名发送合法邮件。

MAPS RBL 权威非常合理，一旦服务器权威证明该服务器不再是开放中继，他们会将黑名单的服务器从其 RBL 列表中移除。

## 第 17 章：邮件服务器安全

垃圾邮件发送者使用工具在互联网上自动搜索开放的中继服务器（`open relays`）。

如果你希望拥有一个安全且相对省心的网络，我建议你采取行动，阻止邮件服务器通过你的邮件服务器进行中继。

### 我的邮件服务器有漏洞吗？

要找到你的邮件服务器（或任何邮件服务器）是否容易受到开放邮件中继攻击（`open mail-relay attack`），请执行以下测试。

1. 登录你的 Linux 系统（或任何带有 `nslookup` 和 `Telnet` 客户端的系统）。
2. 运行 `nslookup -q=mx domain.com`，其中 `domain.com` 是你想查找 MX 记录的域名。

DNS 数据库中的 MX 记录指向一个域名的邮件服务器。在示例中，我使用一个虚的域名 `openrelay-ok.com` 作为示例域名。请注意该域名 MX 记录实际指向的邮件服务器。该域名至少应该配置一个邮件服务器。在此处，我假设 `openrelay-ok.com` 域名的 MX 记录指向的邮件服务器是 `mail.openrelay-ok`。
3. 运行 `telnet mailserver-host 25`，其中 `mailserver-host` 是邮件服务器的主机。我运行 `telnet mail.openrelay-ok 25` 以连接到测试邮件服务器的 25 端口（标准 SMTP 端口）。
4. 一旦连接，输入 `ehlo localhost` 命令向邮件服务器发送（某种形式的）你好。邮件服务器回复问候消息并等待输入。
5. 输入 `mail from:you@hotmail.com` 命令，告诉邮件服务器你想向一个名为 `you@hotmail.com` 的 Hotmail 地址发送邮件。我建议在替换 `you@hotmail.com` 时，使用任何外部域名。服务器将使用类似 `250 you@hotmail.com... Sender ok.` 的响应确认发件者地址。

如果服务器回复了不同的消息，说明发件者电子邮件地址不可接受，请确保你输入的命令正确。如果你仍然收到负面响应，说明服务器不接受该邮件目标地址，这表明服务器可能有特殊的 `MAIL FROM` 检查。这意味着服务器可能根本不会开放中继。大多数情况下你会收到 ok 消息；如果是这样，请继续。

此时，你已经指示邮件服务器你想从 `you@hotmail.com` 发送电子邮件。
6. 使用 `rcpt to:you@yahoo.com` 命令告诉服务器你想将其发送到 `you@yahoo.com`。如果服务器通过发送类似 `250 you@yahoo.com... Recipient ok` 的响应接受了，那么你就发现了一个开放邮件中继。这是因为邮件服务器接受了来自 `you@hotmail.com` 的邮件，并同意将其发送到 `you@yahoo.com`。

如果你不是在 `yahoo.com` 服务器上执行此测试，那么邮件服务器就不会接受来自域外任何人的发送给域外他人的邮件。这是一个开放邮件中继；垃圾邮件发送者可以使用此邮件服务器向你域之外的人发送邮件，如列表 17 所示。

列表 17：使用开放邮件中继

```
$ telnet mail.openrelay-ok.com 25
trying 192.168.1.250...
Connected to mail.openrelay-ok.com.
Escape character is '^'.
220. openrelay-ok.com SMTP Sendmail Pro-8.9.3/Pro-8.9.3/
Sun, 31 Dec 2000 11:04:33 -0800
250. openrelay-ok.com Hello [192.168.1.250], pleased to
meet you
250-EXPN
250-VERB
250-BBBITIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250-HELP
mail from: you@hotmail.com
250 you@hotmail.com... Sender ok
rcpt to: you@yahoo.com
250 you@yahoo.com... Recipient ok
data
354 Enter, end with "*" on a line by itself
THIS SERVER CAN BE AN OPEN MAIL RELAY
FUTURE SPAM WILL BE SERVED FROM HERE!
YOU NEED TO BLOCK THIS ASAP!

250 LAA15851 Message accepted for delivery
```

如果你在不允许开放邮件中继的邮件服务器上执行上述测试，输出将非常不同。这里是名为 `mail.safemta.com` 的邮件服务器 25 端口的 Telnet 会话示例，展示了在邮件服务器上的测试结果；你会得到以下输出：

```
kabir209~\~$ telnet localhost 25
Trying 172.20.15.250...
Connected to mail.safemta.com.
Escape character is '^'.
220 172.20.15.250 ESMTPS Mail 8.11.0/8.11.0; Sun, 31 Dec 2000 14:07:15 -0500
elo localhost
250-172.20.15.250 Hello mail.safemta.com [172.20.15.250], pleased to meet you
250-ENANCEDSTATUS
250-BBBITIME
250-SIZE
250-DSN
250-ONEX
250-XUSR
250-HELP
mail from: you@hotmail.com
250 you@hotmail.com... Sender ok
rcpt to: you@yahoo.com
250 you@yahoo.com... Relaying denied
```

上述输出显示邮件服务器拒绝了 `rcpt to:you@yahoo.com`。

## 加固 Sendmail

`Sendmail` 是最广泛使用的 MTA（邮件传输代理），也是 Linux 的默认选择。幸运的是，新版本的 `Sendmail` 默认不允许开放中继。为了加固它，你可能需要修改配置。

大多数情况下，你需要通过 `m4` 工具来生成配置。建议从 RPM 站点或 `mail.org` 下载最新版本的二进制文件和源码。使用源文件来生成 `/etc/mail/sendmail.conf`。此外，不要直接修改 `/etc/mail/sendmail.conf`，而是修改 `mail.cf` 模板然后重新生成。

请记住以下规则：

- 备份当前的 `/etc/mail/sendmail.conf`。
- `/etc/mail/sendmail.conf` 包含 `include` 指令指向 `/etc/mail/mail.cf` 所在的目录。
- 使用 `m4` 命令处理 `mail.cf` 以生成配置文件。

在接下来的章节中，当我使用 `FEATURE(fieldname)` 语法提到 Sendmail 功能时，请将其添加到 `whatever.mc` 文件中并重新创建 `/etc/mail/sendmail.conf`。为了对抗垃圾邮件，我将在 `whatever.mc` 中添加功能。

例如，如果我使用 `FEATURE(xyz)` 符号推荐一个名为 `xyz` 的功能，请将该功能添加到配置文件，然后使用上述命令创建 `/etc/mail/sendmail.conf` 文件。

### 控制邮件中继

最新版本的 `Sendmail 8.11.2` 允许你对 MTA（邮件传输代理）的邮件中继功能进行高度程度的控制。如前所述，邮件中继默认是禁用的。`Sendmail` 为合法用途提供了邮件中继控制功能。要启用此处讨论的配置控制，你需要在你的 m4 宏文件中包含以下功能，以生成相应的 `/etc/mail/sendmail.cf`。

#### 使用 FEATURE(ACCESS_DB)

此功能启用访问控制数据库，该数据库存储在 `/etc/mail/access` 文件中。该文件的条目具有以下语法：

`LHS(tab)RHS`

- `+` `*` 左侧 (`LHS`) 可以是表 17-1 中显示的任意项目
- `(tab)` 是一个制表符
- 右侧 (`RHS`) 可以是表 17-2 中显示的任意项目。

##### 表 17-1：/ETC/MAIL/ACCESS 中条目的左侧

| LHS | 含义 |
|---|---|
| user@host | 一个电子邮件 |
