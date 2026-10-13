
```
dnl DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

在你希望处理消息中继的主机上的 `sendmail.mc` 文件中，你还需要添加以下行：

```
FEATURE(relay_entire_domain)dnl
```

运行 `m4` 操作以安装更改后的配置，然后使用 `service` 操作重启服务器，如前所述。

你现在可以跨网络从一个用户向另一个用户发送电子邮件。例如，`george@turtle.mytrek.com` 现在可以向 `larisa@rabbit.mytrek.com` 发送邮件。本地 Sendmail 服务器将负责向其主机内的用户以及位于其它网络主机上的用户发送和投递邮件。

### 为集中式邮件服务器配置 Sendmail

另外，你也可以设置一台中央邮件服务器来处理网络上的所有邮件。各个主机上的邮件客户端可以将消息发送到中央邮件服务器，后者再将其中继到更大的网络或互联网。邮件可先在中央邮件服务器接收，客户端随后可再取回。有多种方式设置中央邮件服务器。其中最简单的一种是在网关主机上运行中央邮件服务器，然后在本地主机上运行 Sendmail 服务器的 null 客户端版本。本地主机发送的任何邮件都会自动转发到中央邮件服务器。收到的邮件只能投递到中央服务器，通常投递到也在中央服务器主机上运行的 POP 或 IMAP 服务器。用户随后可以访问 POP 服务器来检索邮件。

对于集中式配置，将用户视为使用网络域名作为地址而不是网络中的单独主机地址是有意义的。因此，`rabbit.mytrek.com` 上的用户 `cece` 将使用邮件地址 `cece@mytrek.com`，而不是 `cece@rabbit.mytrek.com`。用户可以与各自主机上的用户同名，但相应的用户会在网关主机上设置，以处理由 POP 或 IMAP 服务器管理的收件邮件。

一个有效的简单邮件服务器将涉及以下几个组件：

- 在网关主机上运行的中央邮件服务器
- 每个客户端以 null 客户端方式运行 Sendmail
- 伪装所有邮件仅使用域名地址，而非主机地址
- 在网关主机上运行的 POP 或 IMAP 服务器来处理收到的邮件

### 配置具有直接 ISP 连接的工作站

如果你运行的 Linux 系统不属于网络，但通过 ISP（互联网服务提供商）直接连接到互联网，你可以简单地使用 ISP 的邮件服务器来发送和接收邮件。通常，你会有用于外发邮件的 SMTP 邮件服务器和用于收件的 POP 服务器。然而，你也可以配置 Sendmail 来与你的 ISP 接口。

请确保首先按前面各节所示注释掉 `DAEMON_OPTIONS` 选项。

通常，你的 ISP 会提供一个邮件服务器来处理其主机的邮件。要使用 ISP 邮件服务器，你可以用 `SMART_HOST` 选项定义它。邮件将通过 ISP 邮件服务器发送。`SMART_HOST` 的格式为 `type:hostname`，其中 `type` 是使用的邮件服务器类型，通常为 SMTP。默认值为 `relay`。定义 `SMART_HOST` 选项以使用你的 ISP 发送和接收邮件：

```
define ('SMART_HOST', 'smtp:mail.my-isp.com')dnl
```

`SMART_HOST` 选项用于指定你希望处理网络消息中继的特定远程邮件服务器。它可以是 ISP 邮件服务器，也可以是更大网络中的任何邮件服务器。

对于通过调制解调器的拨号连接，你可以使用各种配置选项来控制连接。`confMESSAGE_TIMEOUT` 选项让你控制邮件在输出队列中保留的时间，让你可以在准备拨号发送之前保留邮件。将 `confDELIVERY_MODE` 选项设置为 `queueonly` 可让你在准备好时发送邮件。

### 邮件传输表

邮件传输表让你可以将发往指定主机或域的消息路由到特定的邮件服务器。你可以使用邮件传输表将发往虚拟域的邮件路由到网络的邮件服务器。要引用整个域名，请在域名前加上句点。邮件被路由到的主机以使用的邮件传输程序为前缀，通常 Sendmail 使用 `smtp`。以下条目将把发往 `.mybeach.com` 的邮件路由到邮件服务器 `turtle.mytrek.com`：

```
.mybeach.com    smtp:turtle.mytrek.com
```

条目放置在 `/etc/mail/mailertable` 文件中。条目创建完成后，使用 `make` 命令生成 `mailertable.db` 数据库文件：

```
make mailertable
```

注：正如你在第 34 章中将会看到的，你可以为你的网络定义虚拟域。虚拟域由你的 DNS 服务器映射到一个或多个真实域。然而，你可以

### 安全

为安全起见，Sendmail 允许你筛选特定消息，同时为 Sendmail 传输提供身份验证和加密。从 8.11 版本开始，Sendmail 加入了对安全套接层（SSL）和简单身份验证和安全层（SASL）的支持。SSL 的支持通过 Sendmail 命令 `STARTTLS` 实现，其含义为“start transport layer security”（启动传输层安全）。SSL 为 Sendmail 操作提供身份验证、加密和完整性检查（参见第 18 章）。必须先安装 `OpenSSL` 才能使用 SSL 加密和身份验证方法。

`SASL` 由 `AUTH` 命令实现，被称为 SMTP AUTH。`SASL` 为邮件用户和服务器提供身份验证。它可以利用已安装的 `Kerberos` 服务来提供身份验证。

Sendmail 还提供了屏蔽来自特定域、主机、IP 和用户地址的消息的能力。执行此类筛选的规则保存在 `/etc/mail/access` 文件中。你可以编辑此文件并添加自己的规则。规则由一个地址后跟要执行的操作组成。（支持的操作列在表 24-4 中。）例如，要删除来自 `myannoyingad.com` 域的所有消息，你需要输入：

```
myannoyingad.com DISCARD
```

下一个示例拒绝来自 `larisa@turtle.mycar.com` 的任何消息并发送拒绝通知：

```
larisa@turtle.mycar.com REJECT
```

你还可以指定返回的错误消息，如下所示：

```
cecelia@rabbit.mytrek.com ERROR:"Retired yesterday"
```

要向垃圾邮件发送者发送错误消息，你可以包含如下所示的消息。第一个数字是错误代码。

```
cyberspammer.com ERROR:"550 We don't accept mail from spammers"
```

包含前面条目的 `/etc/mail/access` 文件如下所示：

```
myannoyingad.com DISCARD
larisa@turtle.mycar.com REJECT
cecelia@rabbit.mytrek.com ERROR:"Retired yesterday"
cyberspammer.com ERROR:"550 We don't accept mail from spammers"
```

Sendmail 实际上从位于 `/etc/mail` 目录中的名为 `access.db` 的数据库文件读取访问规则。要实现你的规则，你必须使用 `access` 文件重新生成 `access.db` 文件。你可以使用 `make` 命令并以 `access` 作为参数来完成此操作，如下所示：

表 24-4：访问操作

| 操作 | 描述 |
|---|---|
| OK | 接受消息，即使其他规则会拒绝（规则的例外）。 |
| DISCARD | 完全丢弃消息。 |
| REJECT | 拒绝消息，并向发送者发送拒绝通知。 |
| RELAY | 为指定域中继消息。 |
| SMTP-code message | 发送给发送者的代码和消息。 |

```
make access
```

然后必须重新启动 Sendmail 以读取新的 `access.db` 文件。

在 `sendmail.mc` 文件中，使用 `access_db` 功能启用 `access` 文件的使用：

```
FEATURE('access_db')dnl
```

`access` 文件将拒绝来自所列地址的收件邮件。然而，你也可以拒绝发送给它们的任何邮件。你还可以拒绝网络上某些主机的邮件。你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 选项来实现。此选项管理收件人，而 `access` 通常管理发件人。所列地址将无法接收任何邮件。此功能也用于某些不应接收邮件的管理用户，例如 `nobody`（访客用户）或 `ftp`（FTP 用户）：

```
FEATURE('blacklist_recipients')dnl
```

以下示例不允许向 `cyberspammer.com`（收件人）发送邮件，也无法接收发往 `justin@lizard.mytrek.com`、`secretproject@rabbit.mytrek.com` 或 `mysurfboard.com` 的邮件：
