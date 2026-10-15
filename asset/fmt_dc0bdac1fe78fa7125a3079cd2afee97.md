
最广泛支持的加密是 PGP。对于我们的 PGP 软件，我们倾向于 `GnPG`，即 GNU Privacy Guard，可以在 `http://www.gnupg.org` 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 PGP。

如果你的邮件包含敏感数据，你不应该在不加密的情况下发送它。任何现代客户端都有可用的钩子——如果没有，按照定义它就不是现代的。最广泛支持的加密是 PGP。对于我们的 PGP 软件，我们倾向于 `GnPG`，即 GNU Privacy Guard，可以在 `http://www.gnupg.org` 获取（以及那些烦人的密码学法）。许多邮件客户端会嗅探你机器与目标之间的连接。连接，许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 PGP。由于邮件经常通过不同的中继路由（例如对于企业内部网），因此在每一步，黑客或仅仅是不道德的管理员都可以获取。理论上，任何中继你邮件的系统如果需要，都会保留一份，即使是存储原始未加密位数据的磁盘，如果强大的组织决定恢复即使被删除的数据，也应该显示出来。

某些 `SMTP` 服务器和客户端开始支持 `SMTP-AUTH`，这是 `SMTP` 的一个扩展，允许用户向服务器进行身份验证。这通常用于允许在通常会被拒绝的情况下进行中继，例如合法用户从家庭拨号账户连接到公司的邮件服务器。此用户名和密码通常与 Linux 账户相同，这可能会产生灾性的安全影响。

# 第 11 章：邮件与 FTP 安全

```
220 example.org SMTP Postfix
EHLO localhost
250-example.org
250-PIPELINING
250-SIZE 5000000
250-ETRN
250-STARTTLS
250 8BITIME
```

列表底部 `250-STARTTLS` 条目显示该服务器支持通道加密。

# 深度解析 Linux Linux：Linux 安全机密与解决方案

## 使用 Stunnel 对 IMAP 进行加密

假设你想使用 `Mutt` 连接到 `mailserver.example.com`。你编译了带有 SSL 支持的 `Mutt`，但你的 IMAP 服务器不支持它。在服务器上运行 `Stunnel` 以在 `imaps` 端口上监听连接，具体如下所示：

```
mailserver# /usr/bin/stunnel -D mail.debug -p /path/to/stunnel.pem \
-N simapd -d simap -1l /usr/sbin/imapd
```

将你的 `$MAIL` 环境变量指向邮件服务器：

```
client$ export MAIL='mailserver.example.com/ssl'
client$ mutt
```

当连接到达 `imaps` 端口时，`Stunnel` 会启动 `imapd` 服务器，就像通常情况下直接启动它那样。然而，`Stunnel` 将处理 SSL 连接的解密，而 `imapd` 无需感知加密层的任何信息。

> 注意：`Stunnel` 可以使用 TCP wrappers，请确保在 `/etc/hosts.allow` 中添加了相应的行，以允许你想要接受的连接。

## 使用 SSH 对 POP 进行加密

假设我们希望让 `Fetchmail` 通过 POP 提取我们的电子邮件。如果我们能够通过 SSH 登录服务器，那么就可以使用 SSH 转发功能通过加密通道为我们的 POP 连接建立隧道。在尝试运行 `fetchmail` 之前，只需运行以下命令：

```
client$ ssh -n -x -f mailserver.example.com -L8765:mailserver.example.com:110 \
  'sleep 60'
```

运行 `fetchmail` 时，指向本地机器 `8765` 端口的任何连接都将通过加密通道发送到邮件服务器上的 POP 端口。在命令行参数中包含 `--port 8765` 并将其指向 `localhost` 而不是 `mailserver.example.com`。

你可以通过在 `.fetchmailrc` 中包含以下行来进一步简化操作，这样你就不再需要手动执行 SSH 了：

```
poll localhost port 1234 with proto pop3:
preconnect "ssh -n -x -f mailserver.example.com \
-L 8765:mailserver.example.com:110 'sleep 60'"
```
