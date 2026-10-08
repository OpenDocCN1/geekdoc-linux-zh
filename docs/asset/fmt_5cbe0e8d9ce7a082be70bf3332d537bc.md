
你的 `smb.conf` 发行版可能配置了 `Sendmail` 使用 `access_db`（如 Red Hat 所示）。访问仅授予本地主机。如果你的系统被用作网络的邮件服务器，且你没有启用 `relay_entire_domain`，则你需要允许网络上的其他主机访问。在 `access` 文件中，你可以为你的设置一个 `RELAY` 规则。`RELAY` 规则将允许其他主机发送你发往其他主机的邮件。这通常用于从本地网络中继邮件到互联网的网关主机。以下示例允许来自 `mytrek.com` 网络的访问：`mytrek.com                 RELAY`

对于特定主机，在 `access` 文件中为其放置一个条目，如下所示：
`rabbit.mytrek.com             RELAY`

为了进一步保护 `Sendmail`，你应该禁用 `VRFY` 的使用。此选项允许远程用户尝试验证用户地址是否存在。通过 `noverifier` 功能禁用此选项：
`FEATURE('noverifier') dnl`

另一个潜在的安全漏洞是 `EXPN` 选项，它会将邮件列表和别名扩展到它们的实际地址。使用 `noexpn` 将其关闭：
`FEATURE('noexpn') dnl`

默认情况下，`Sendmail` 将拒绝来自任何无法解析的域的邮件。你可以通过 `accept_unresolvable_domains` 功能覆盖此限制。`Sendmail` 还会拒绝地址没有完全限定名称的邮件。

## POP 服务器

邮局局协议（POP）允许用户从邮件服务器检索邮件。当前版本 `POP3` 最常用。`POP3` 允许客户端连接到邮件服务器并将消息下载到本地设备。一旦下载了消息，它们通常会从服务器上删除。

通常使用的命令有：
- `USER`: 指定用户名。
- `PASS`: 指定密码。
- `LIST`: 列出服务器上可用的消息。
- `RETR`: 检索特定的消息。
- `DELE`: 标记消息待删除。
- `NOOP`: 不删除标记为待删除的消息。
- `DELE ALL`: 删除服务器上所有的消息。
- `QUIT`: 终止会话。

在 `sendmail.mc` 文件中通过 `access_db` 功能启用 `access` 文件的使用：
`FEATURE('access_db') dnl`

`access` 文件将拒绝来自列出地址的邮件。你还可以拒绝任何发送到以下位置的邮件：
你还可以拒绝网络上某些主机的邮件。你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 来。此选项控制收件者，而 `access` 控制服务器。这些地址将无法接收任何邮件。此功能也用于某些永远不应该接收邮件的管理员用户，例如 `nobody`（用户）或 `ftp`（FTP 用户）：
`FEATURE('blacklist_recipients') dnl`

接下来的示例将不允许发送邮件到 `cyberspammer`（收件者），但现在可能接收来自 `justin@lizard.mytrek.com`、`secretproject@rabbit.mytrek.com` 或 `mysurfboard.com` 的邮件：

```
mysurfboard.com             ERROR:Domain does not exist

justin@lizard.mytrek.com "Moved to Hawaii"

secretproject@rabbit.mytrek.com REJECT

cyberspammer.com             REJECT
```

## Qpopper

`Qpopper` 是 Berkeley POP 服务器的当前版本。`Qpopper` 由 Eudora 邮件软件的制造商 Qualcomm 支持。`Qpopper` 网页为 `//www.eudora.com/qpopper`。你可以从 `ftp.qualcomm.com/eudora/servers/unix/` 获取当前的源代码。RPM 包位于分发站点或包含在发行版中。

一旦下载了消息，它们通常会从服务器上删除。

通常使用的命令有：
- `USER`: 指定用户名。
- `PASS`: 指定密码。
- `LIST`: 列出服务器上可用的消息。
- `RETR`: 检索特定的消息。
- `DELE`: 标记消息待删除。
- `NOOP`: 不删除标记为待删除的消息。
- `DELE ALL`: 删除服务器上所有的消息。
- `QUIT`: 终止会话。

在 `sendmail.mc` 文件中通过 `access_db` 功能启用 `access` 文件的使用：
`FEATURE('access_db') dnl`

`access` 文件将拒绝来自列出地址的邮件。你还可以拒绝任何发送到以下位置的邮件：
你还可以拒绝网络上某些主机的邮件。你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 来。此选项控制收件者，而 `access` 控制服务器。这些地址将无法接收任何邮件。此功能也用于某些永远不应该接收邮件的管理员用户，例如 `nobody`（用户）或 `ftp`（FTP 用户）：
`FEATURE('blacklist_recipients') dnl`

接下来的示例将不允许发送邮件到 `cyberspammer`（收件者），但现在可能接收来自 `justin@lizard.mytrek.com`、`secretproject@rabbit.mytrek.com` 或 `mysurfboard.com` 的邮件：

```
mysurfboard.com             ERROR:Domain does not exist

justin@lizard.mytrek.com "Moved to Hawaii"

secretproject@rabbit.mytrek.com REJECT

cyberspammer.com             REJECT
```

针对邮件用户和服务器的身份验证。它可以利用已安装的 Kerberos 服务提供身份验证。

`Sendmail` 为你提供了筛选来自特定域、主机、IP 和地址邮件的能力。执行此类筛选的规则保留在 `/etc/mailaccess` 文件中。你可以编辑此文件并添加自己的规则。一条规则由一个示例后跟着要执行的操作组成。这些操作列在[表 24-4](#)。要删除来自 `myannyingad.com` 域的所有邮件，你需要输入：`myannyingad.com DISCARD`

下一个示例拒绝任何来自 `larisa@turtle.mycar.com` 的邮件，并发送一条拒绝通知：`larisa@turtle.mycar.com REJECT`

要向垃圾邮件发送者发送错误消息，你可以包含一条如处所示的消息。第一个数字是错误代码：`cyberspammer.com ERROR:"550 We don't accept mail from spammers"`

包含上述示例的 `/etc/mailaccess` 文件内容如下所示：

```
myannyingad.com         DISCARD

larisa@turtle.mycar.com  REJECT

cecelia@rabbit.mytrek.com  ERROR:"Retired yesterday"

cyberspammer.com         ERROR:"550 We don't accept mail from spammers"
```

`Sendmail` 实际上从数据库文件 `access.db` 读取规则，该文件也位于 `/etc/mail` 目录。要实现你的规则，你必须使用 `access` 文件重新生成 `access.db` 文件。你可以使用 `make` 命令并以 `access` 作为参数来实现此操作，如下所示：

| Action | Description |
| --- | --- |
| OK | 即使其他规则拒绝，也接受该邮件（规则的例外）。 |
| DISCARD | 完全丢弃邮件。 |
| REJECT | 拒绝邮件，向发送者发送拒绝通知。 |
| RELAY | 为指定的域中继邮件。 |
| SMTP-code message | 要发送给发送者的代码和消息。 |

`make access`

然后必须重启 `Sendmail` 以读取新的 `access.db` 文件。

在 `sendmail.mc` 文件中通过 `access_db` 功能启用 `access` 文件的使用：
`FEATURE('access_db') dnl`

`access` 文件将拒绝来自列出地址的邮件。你还可以拒绝任何发送到以下位置的邮件：
你还可以拒绝网络上某些主机的邮件。你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 来。此选项控制收件者，而 `access` 控制服务器。这些地址将无法接收任何邮件。此功能也用于某些永远不应该接收邮件的管理员用户，例如 `nobody`（用户）或 `ftp`（FTP 用户）：
`FEATURE('blacklist_recipients') dnl`

接下来的示例将不允许发送邮件到 `cyberspammer`（收件者），但现在可能接收来自 `justin@lizard.mytrek.com`、`secretproject@rabbit.mytrek.com` 或 `mysurfboard.com` 的邮件：

```
mysurfboard.com             ERROR:Domain does not exist

justin@lizard.mytrek.com "Moved to Hawaii"

secretproject@rabbit.mytrek.com REJECT

cyberspammer.com             REJECT
```

你的 `smb.conf` 发行版可能配置了 `Sendmail` 使用 `access_db`（如 Red Hat 所示）。访问仅授予本地主机。如果你的系统被用作网络的邮件服务器，且你没有启用 `relay_entire_domain`，则你需要允许网络上的其他主机访问。在 `access` 文件中，你可以为你的设置一个 `RELAY` 规则。`RELAY` 规则将允许其他主机发送你发往其他主机的邮件。这通常用于从本地网络中继邮件到互联网的网关主机。以下示例允许来自 `mytrek.com` 网络的访问：`mytrek.com                 RELAY`

对于特定主机，在 `access` 文件中为其放置一个条目，如下所示：
`rabbit.mytrek.com             RELAY`

为了进一步保护 `Sendmail`，你应该禁用 `VRFY` 的使用。此选项允许远程用户尝试验证用户地址是否存在。通过 `noverifier` 功能禁用此选项：
`FEATURE('noverifier') dnl`

另一个潜在的安全漏洞是 `EXPN` 选项，它会将邮件列表和别名扩展到它们的实际地址。使用 `noexpn` 将其关闭：
`FEATURE('noexpn') dnl`

默认情况下，`Sendmail` 将拒绝来自任何无法解析的域的邮件。你可以通过 `accept_unresolvable_domains` 功能覆盖此限制。`Sendmail` 还会拒绝地址没有完全限定名称的邮件。

## POP 服务器

邮局局协议（POP）允许用户从邮件服务器检索邮件。当前版本 `POP3` 最常用。`POP3` 允许客户端连接到邮件服务器并将消息下载到本地设备。一旦下载了消息，它们通常会从服务器上删除。

通常使用的命令有：
- `USER`: 指定用户名。
- `PASS`: 指定密码。
- `LIST`: 列出服务器上可用的消息。
- `RETR`: 检索特定的消息。
- `DELE`: 标记消息待删除。
- `NOOP`: 不删除标记为待删除的消息。
- `DELE ALL`: 删除服务器上所有的消息。
- `QUIT`: 终止会话。

在 `sendmail.mc` 文件中通过 `access_db` 功能启用 `access` 文件的使用：
`FEATURE('access_db') dnl`

`access` 文件将拒绝来自列出地址的邮件。你还可以拒绝任何发送到以下位置的邮件：
你还可以拒绝网络上某些主机的邮件。你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 来。此选项控制收件者，而 `access` 控制服务器。这些地址将无法接收任何邮件。此功能也用于某些永远不应该接收邮件的管理员用户，例如 `nobody`（用户）或 `ftp`（FTP 用户）：
`FEATURE('blacklist_recipients') dnl`

接下来的示例将不允许发送邮件到 `cyberspammer`（收件者），但现在可能接收来自 `justin@lizard.mytrek.com`、`secretproject@rabbit.mytrek.com` 或 `mysurfboard.com` 的邮件：

```
mysurfboard.com             DISCARD

justin@lizard.mytrek.com "Moved to Hawaii"

secretproject@rabbit.mytrek.com REJECT

cyberspammer.com             REJECT
```

你的 `smb.conf` 发行版可能配置了 `Sendmail` 使用 `access_db`（如 Red Hat 所示）。访问仅授予本地主机。如果你的系统被用作网络的邮件服务器，且你没有启用 `relay_entire_domain`，则你需要允许网络上的其他主机访问。在 `access` 文件中，你可以为你的设置一个 `RELAY` 规则。`RELAY` 规则将允许其他主机发送你发往其他主机的邮件。这通常用于从本地网络中继邮件到互联网的网关主机。以下示例允许来自 `mytrek.com` 网络的访问：`mytrek.com                 RELAY`

对于特定主机，在 `access` 文件中为其放置一个条目，如下所示：
`rabbit.mytrek.com             RELAY`

为了进一步保护 `Sendmail`，你应该禁用 `VRFY` 的使用。此选项允许远程用户尝试验证用户地址是否存在。通过 `noverifier` 功能禁用此选项：
`FEATURE('noverifier') dnl`

## Qpopper

`Qpopper` 是 Berkeley POP 服务器的当前版本。`Qpopper` 由 Eudora 邮件软件的制造商 Qualcomm 支持。`Qpopper` 网页为 `//www.eudora.com/qpopper`。你可以从 `ftp.qualcomm.com/eudora/servers/unix/` 获取当前的源代码。RPM 包位于分发站点或包含在发行版中。

`Qpopper` 通常通过 `xinetd` 运行。你可以在 `/etc/xinetd.d` 目录下创建一个类似于此处所示的 `popper` 文件：

```
service pop-3

  socket_type   = stream

  wait          = no

  user          = root

  server        = /usr/bin/popper

  disable       = no
```
