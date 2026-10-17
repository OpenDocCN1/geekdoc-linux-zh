
所有消息都将来自邮件服务器的主机。例如，如果 `Sendmail` 邮件程序运行在 `turtle.mytrek.com` 上，那么从本地主机 `rabbit.mytrek.com` 发送的邮件看起来将是从 `turtle.mytrek.com` 发送的。

你也可以伪装收件者地址，使得发送到本地主机上用户的邮件将发送到实际地址，而不是伪装的地址。使用 `allmasquerade` 功能来确保收件者伪装：

```
FEATURE(allmasquerade) dnl
```

带有点的域名。邮件路由到的主机在前面带有使用的邮件传输器的前缀，对于 `Sendmail` 通常使用 `smtp`。以下条目将发送至 `.mybeach.com` 的邮件路由到邮件服务器 `turtle.mytrek.com`。

```
.mybeach.com    smtp:turtle.mytrek.com
```

条目放置在 `/etc/mail/mailertable` 文件。一旦创建了条目，可以使用 `make` 命令生成 `mailertable.db` 数据库文件：

```
make mailertable
```

## 虚拟域名：virtuertable

正如你在第36章中看到的，你可以为你的网络定义虚拟域名。这些虚拟域名由你的 DNS 服务器映射到一个或多个真实域名。然而，你可以接收使用虚拟域名邮箱地址的邮件。在这种情况下，你需要将这些地址映射到你的真实域名，以便邮件被投递到现有位置。这种映射通过虚拟用户表 `/etc/mail/virtuertable` 来执行。虚拟表允许你将虚拟域名的邮件地址映射到真实域名。一旦创建了条目，使用 `make` 命令生成 `virtuertable.db` 数据库文件：

```
make virtuertable
```

## 安全

为了安全，`Sendmail` 允许你保护特定邮件，并为 `Sendmail` 传输提供认证和加密。在 8.11 版本中，`Sendmail` 包含了对安全套接层 `SSL` 和简单身份验证安全层 `SASL` 的支持。对 `SSL` 支持通过 `STARTTLS` 命令实现，其意思是“传输层安全”。`SSL` 为 `Sendmail` 操作提供认证、加密和完整性检查（见第19章）。必须安装 `OpenSSL` 允许使用 `SSL` 加密和认证方法。

`SASL` 由 `AUTH` 命令实现，被称为 `SMTP AUTH`。`SASL` 为邮件用户和服务器提供身份验证。它可以利用已安装的 `Kerberos` 服务来提供身份验证。

`Sendmail` 还提供了功能，筛选掉来自特定域名、主机、IP 和用户地址的邮件。执行此类筛选的规则保留在 `/etc/mail/access` 文件中。你可以编辑此文件并添加自己的规则。一条规则由一个地址后跟一个要执行的操作组成。（例如，要删除来自 `annoyingad.com` 域的所有邮件，你输入：

```
annoyingad.com DISCARD
```

下一个示例拒绝任何来自 `larisa@turtle.mycar.com` 的邮件并发送拒绝通知：

```
larisa@turtle.mycar.com REJECT
```

## 第25章：邮件服务器：SMTP, POP, 和 IMAP

| 操作 | 描述 |
| --- | --- |
| OK | 即使其他规则会拒绝也接受邮件（规则的例外）。 |
| DISCARD | 完全丢弃邮件。 |
| REJECT | 拒绝邮件并向发送者发送通知。 |
| RELAY | 为指定域名中继邮件。 |
| SMTP-code message | 应当按顺序发送的代码和消息。 |

**表 25-4** 指定的操作

你也可以指定要返回的错误，如下所示：

```
cecelia@rabbit.mytrek.com    ERROR:"Retired yesterday"
```

要向垃圾邮件发送者发送错误消息，你可以包含如下所示的消息：第一个数字是错误代码：

```
cyberspam.com    ERROR:"550 We don't accept mail from spammers"
```

带有上述条目的 `/etc/mail/access` 文件看起来如下：

```
myannoying.com           DISCARD

laris@turtle.mycar.com    REJECT

cecelia@rabbit.mytrek.com  ERROR:"Retired yesterday"

cyberspam.com             ERROR:"550 We don't accept mail from spammers"
```

`Sendmail` 实际上从一个名为 `access.db` 的数据库文件读取规则，该文件也位于 `/etc/mail` 目录。要实现你的规则，你必须使用 `access` 文件重新生成 `access.db` 文件。你可以使用 `make` 命令并将 `access` 作为参数来实现，如下所示：

```
make access
```

必须重启 `Sendmail` 才能读取 `access.db` 文件。在 `sendmail.mc` 文件中通过 `access_db` 功能启用 `access` 文件：

```
FEATURE('access_db') dnl
```

`access` 文件将拒绝来自接收地址。然而，你也可以拒绝任何发送给它们的邮件。此外，你还可以接收网络上某些主机的邮件。你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 选项来实现。此选项控制收件者，而通常控制发送者。此功能也用于某些永远不应接收邮件的管理员用户，例如 `nobody`（客人用户）或 `ftp`（FTP 用户）：

```
FEATURE('blacklist_recipients') dnl
```

## 第五部分：网络服务器

以下示例将不允许邮件发送到 `cyberspammer.com`（收件者），也无法接收 `justin@lizard.mytrek.com`、`secretproject@rabbit.mytrek.com` 或 `mysurfboard.com` 的邮件：

```
mysurfboard.com           ERROR:Domain does not exist

justin@lizard.mytrek.com     'Moved to Hawaii'

secretproject@rabbit.mytrek.com REJECT

cyberspammer.com             REJECT
```

你的发行版将使用 `smb.conf` 配置 `Sendmail` 使用 `access_db`（如 Fedora 所示）。访问仅授予本地主机上的用户。如果你的系统被用作邮件服务器，你可以通过在 `sendmail.mc` 文件中启用 `blacklist_recipients` 选项来实现。

# 546 第 V 部分：网络服务器

`Maildir` 格式为每条消息使用单独的文件，使得更新更高效。`Dovecot` 将自动检测存储使用的类型，引用 `MAIL` 环境变量。这将是用户位于 `/var/mail` 的 `mbox` 文件。你可以通过设置 `mail_location` 选项为使用 `maildir` 设置并指定目录，来配置 `Dovecot` 使用 `Maildir` 格式。`~` 符号将用于表示用户名，`~h` 表示家目录。消息将存储在用户的 `Maildir` 目录中而不是 `mbox`。请务必创建 `Maildir` 目录并确保你拥有读、写、执行权限。

```
mail_location=maildir:/var/mail/$lu/%u/maildir
```
