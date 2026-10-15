

SASL 由 AUTH 命令实现，被称为 SMTP AUTH。SASL 为邮件用户和服务器提供身份验证。它可以利用已安装的 Kerberos 服务来提供身份验证。

Sendmail 还提供了筛选来自特定域、主机、IP 和用户地址的消息的功能。执行此类筛选的规则保存在 /etc/mail/access 文件中。你可以编辑此文件并添加自己的规则。规则由一个地址后跟要采取的操作组成。（支持的操作列在表 24-4 中。）例如，要删除来自 myannoyingad.com 域的所有消息，你将输入：

```
myannoyingad.com DISCARD
```

下一个示例拒绝来自 larisa@turtle.mycar.com 的任何消息并发送拒绝通知：

```
larisa@turtle.mycar.com REJECT
```

你也可以指定要返回的错误消息，如下所示：

```
cecelia@rabbit.mytrek.com ERROR:"Retired yesterday"
```

要向垃圾邮件发送者发送错误消息，你可以包含如下所示的消息。

```
cyberspammer.com ERROR:"550 We don't accept mail from spammers"
```

包含前面条目的 /etc/mail/access 文件如下所示：

```
myannoyingad.com DISCARD
larisa@turtle.mycar.com REJECT
cecelia@rabbit.mytrek.com ERROR:"Retired yesterday"
cyberspammer.com ERROR:"550 We don't accept mail from spammers"
```

Sendmail 实际上从位于 /etc/mail 目录中的名为 access.db 的数据库文件读取访问规则。要实现你的规则，你必须使用 access 文件重新生成

## TABLE 24-4
### Access Actions

| Action | Description |
|---|---|
| OK | 接受消息，即使其他规则会拒绝（规则的例外）。 |
| DISCARD | 完全丢弃消息。 |
| REJECT | 拒绝消息，向发件人发送拒绝通知。 |
| RELAY | 为指定域中继消息。 |
| SMTP-code message | 发送给发件人的代码和消息。 |

access.db 文件。你可以使用 make 命令并以 access 作为参数来完成此操作，如下所示：

```
make access
```

然后必须重新启动 Sendmail 以读取新的 access.db 文件。

access 文件的使用在 sendmail.mc 文件中通过 access_db 功能启用：

```
FEATURE(`access_db')dnl
```

access 文件将拒绝从所列地址收到的邮件。但是，你也可以拒绝发送给它们的任何邮件。你还可以拒绝网络上某些主机的收件邮件。你可以通过在 sendmail.mc 文件中启用 blacklist_recipients 选项来实现。 此选项管理收件人，而 access 通常管理发件人。所列地址将无法接收任何邮件。此功能也用于某些永远不应接收邮件的管理用户，例如 nobody（访客用户）或 ftp（FTP 用户）：

```
FEATURE(`blacklist_recipients')dnl
```

以下示例将不允许向 cyberspammer.com（收件人）发送邮件，并且也不能接收发给 justin@lizard.mytrek.com、secretproject@rabbit.mytrek.com 或 mysurfboard.com 的邮件：

```
mysurfboard.com            ERROR:"Domain does not exist"
justin@lizard.mytrek.com   "Moved to Hawaii"
secretproject@rabbit.mytrek.com REJECT
cyberspammer.com           REJECT
```

你的发行版 smb.conf 可能配置 Sendmail 使用 access_db（Red Hat 即是如此）。仅允许本地主机上的用户访问。如果你的系统用作网络的邮件服务器，并且你未启用 relay_entire_domain 功能，则需要允许网络上的其他主机访问。在 access 文件中，你可以为你的网络放置一个 RELAY 规则。RELAY 规则将允许其他主机使用你的邮件服务器向其他主机发送消息。这通常是为网关主机完成的，该主机需要将来自本地网络的消息中继到 Internet。以下示例允许从 mytrek.com 网络访问：

```
mytrek.com    RELAY
```

对于特定主机，将其条目放在 access 文件中，如下所示：

```
rabbit.mytrek.com    RELAY
```

