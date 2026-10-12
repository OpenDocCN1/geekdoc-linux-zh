
## 使用 /etc/mail/access 限制对 sendmail 服务器的访问

可以使用此配置文件创建针对您的 sendmail 服务器的访问限制数据库。您可以基于域名、子域名、IP 地址或网络来控制对 sendmail 服务器的访问。此文件中的配置行格式如下：

*host* 或 *user* *访问控制* *选项*

其中，*host* 或 *user* 可以是完全限定或部分限定的主机名、域名、IP 地址、网络地址或电子邮件地址，例如 *wormhole.nitec.com*、*nitec.com*、*192.168.1.10*、*192.168.1.0*、*spammer@somewhere.com* 等。可用的配置选项如表 9-2 所示。

表 9-2 /etc/mail/access 数据库的配置选项

| 选项 | 描述 |
| :--- | :--- |
| OK | 即使其他配置规则未拒绝来自指定主机或用户的邮件，也接受该邮件。 |
| RELAY | 作为指定主机的 SMTP 邮件中继。换句话说，接受发送给指定域名用户的邮件，并允许指定域名的用户通过服务器发送邮件。即使其他规则希望拒绝，也不拒绝来自指定域名的邮件。 |
| REJECT | 拒绝指定域名的所有（入站/出站）邮件。 |
| DISCARD | 使用 $d/discard 邮件器完全丢弃消息。被丢弃的消息会被接受，但会静默地保持未送达状态，从而让发送者以为已送达。 |
| 501 <message> | 如果发件人地址部分或完全匹配指定的 user@host，则不接受邮件。 |
| 553 <message> | 如果发件人地址不包含主机名，则不接受邮件。 |
| 550 <message> | 不接受发送给指定域名名称的邮件。 |

以下是一个配置示例：

```
any-spam-maker.com REJECT
client-domain.com RELAY
annoying-company.com DISCARD
dumbguy@dumb-net.com 501 You can't use this mail server.
```

来自 any-spam-maker.com 的所有邮件将被拒绝；发送到和来自 client-domain.com 的所有入站和出站邮件将被中继；来自 annoying-company.com 的所有邮件将被接受，但会被静默丢弃；来自 dumbguy@dumb-net.com 的所有邮件将拒绝，并提示“You can't use this mail server”信息。

请注意，sendmail 并不直接使用 /etc/mail/access 配置文件。它使用文件的 DBM 数据库版本。要为 /etc/mail/access 文件创建所需的 DBM 文件，请运行以下命令：

```
makemap hash /etc/mail/access < /etc/mail/access
```

这将在同一目录中创建所需的 DBM 数据库文件（例如 /etc/mail/access.db）。修改此文件后，无需重启 sendmail 守护进程。

## 使用 /etc/mail/aliases 为用户创建别名

此配置文件允许您为用户创建别名数据库。例如，假设您想为一个名为 carol 的用户创建一个名为 carol.godsave 的别名。您可以通过使用此配置文件来实现，其格式如下：

*别名名称：逗号分隔的用户列表*

要创建 carol.godsave 别名，在此配置文件中添加一行，如下所示：

```
carol.godsave: carol
```

当 sendmail 接收到发送给 carol.godsave@yourdomain.com 的邮件时，它将投递到您邮件服务器上的 carol 账户。

别名的一个有用用途是创建本地组。例如，`web-developers: keith, cynthia, jason` 定义了一个名为 web-developers 的别名，可用于向指定用户发送电子邮件消息。

默认的 /etc/mail/aliases 文件已经包含一组您可以根据需要更改的默认别名。另外，请注意，如果您有一个与别名同名的用户，邮件将发送到别名中指定的用户。以下是此类别名的示例：

```
root: kabir
```

当邮件发送给 root@ntec.com 时，即使邮件服务器上存在名为 root 的用户账户，邮件仍将发送给用户 kabir。

您还可以链式使用别名。在以下示例中，别名 root 解析为别名 kabir，进而解析为 mohammed：

```
root: kabir
kabir: mohammed
```

因此，在我的系统中，发送给 root@localhost 的邮件可以到达名为 mohammed 用户的邮箱。

Sendmail 并不直接使用 /etc/mail/aliases 配置文件。它使用文件的 DBM 数据库版本。要为 /etc/mail/aliases 文件创建所需的 DBM 文件，请运行以下命令：

```
newaliases
```

这将在同一目录中创建所需的 DBM 数据库文件（例如 /etc/mail/aliases.db）。修改此文件时，无需重启 sendmail 守护进程。

![](img/f9ec99365f159bfe663f8ac29732663c_222_0.png)

> **提示**
> 运行 newaliases 等同于运行 sendmail -bi 命令。

## 使用 /etc/mail/domaintable 映射域名

可以使用此配置文件创建域名映射数据库，例如将 yet-another-domain.com 映射到 yourdomain.com：

```
yet-another-domain.com yourdomain.com
```

因此，当接收到发送给 user@yet-another-domain.com 的邮件时，它将被转换为 user@yourdomain.com。目标域名（yourdomain.com）必须是完全限定域名。此外，域表中的域名映射反映在报头中；也就是说，这是在 ruleset 3 中完成的。

sendmail 并不直接使用 `/etc/mail/domaintable` 配置文件。它使用文件的 DBM 数据库版本。要为 `/etc/mail/domaintable` 文件创建所需的 DBM 文件，请运行以下命令：

```
makemap hash /etc/mail/domaintable < /etc/mail/domaintable
```

这将在同一目录中创建所需的 DBM 数据库文件（例如 `/etc/mail/domaintable.db`）。修改此文件时，无需重启 sendmail 守护进程。

## 使用 `/etc/mail/mailertable` 重新路由域名的邮件

可以使用此配置文件创建数据库，以覆盖特定域名的默认邮件路由。此文件的格式如下：

```
源域名 邮件器:替换域名或 user@host
```

例如：

```
visitor-01.mydomain.com    local:visitorl
```

当发给 **visitor-01.mydomain.com** 的邮件到达时，它将被重新路由到本地用户 **visitorl**。您只能使用在 `/etc/sendmail.cf` 文件中通过 M 行指定的邮件器。快速查看 `/etc/sendmail.cf` 文件可以看到 qsmtp, procmail, smtqp, smsmtp, smtph, relay, usenet, ucp, ucp-ol, smc-, ucp-new, ucp-om, ucp-uom, local, 和 prog 被定义为邮件器。

您还可以指定部分域名作为源域名。在以下示例中，发给 `*.mydomain.com` 主机的邮件将通过 SMTP 邮件器中继到 mail-hub.mydomain.com 服务器：

```
mydomain.com    smtp:mail-hub.mydomain.com
```

![](img/f9ec99365f159bfe663f8ac29732663c_223_0.png)

> **注意**
> 您必须拥有源域名的相应 MX 记录，否则邮件将永远无法送达。

考虑另一个示例，其中只要 ad-engine.com 列在 /etc/mail/sendmail.cw 文件中，发给 ad-engine.com 的所有邮件都将通过 SMTP 邮件器投递到 kabir@intevo.com：

```
ad-engine.com    smtp:kabir@intevo.com
```

sendmail 并不直接使用 /etc/mail/mailertable 配置文件。它使用文件的 DBM 数据库版本。要为 /etc/mail/mailertable 文件创建所需的 DBM 文件，请运行以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

这将在同一目录中创建所需的 DBM 数据库文件（例如 /etc/mail/mailertable.db）。修改此文件时，无需重启 sendmail 守护进程。

## 使用 /etc/mail/relay-domains 设置邮件中继

最新版本的 sendmail (v 8.11.x) 默认拒绝未经授权的邮件中继。换句话说，如果未明确告知 sendmail 接受发往其他域名的邮件，它将拒绝这样做。例如，假设您在名为 mail.mydomain.com 的主机上运行最新版本的 sendmail。如果未经授权的用户试图使用 mail.mydomain.com 将邮件投递到另一个 SMTP 服务器，您的 sendmail 服务器默认将拒绝此类请求。这样做是为了消除那些发送未经请求的电子邮件消息的人滥用邮件中继。

要允许合法域使用您的 sendmail 服务器作为中继，您必须在此文件中指定它们。添加您自己的域名以及您希望允许中继操作的其他友好域名。例如：

```
nitec.com
intevo.com
ad-engine.com
```

您还可以使用网络地址形式或完整 IP 形式的 IP 地址。

要测试中继配置，请运行以下命令：

```
echo '$=R' | sendmail -bt
```

这应该会显示所有允许的域名。
