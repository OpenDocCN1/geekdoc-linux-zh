
`reject_rbl_client` 限制根据指定的 `MAPS` 服务拒绝域名地址。该站点可以是在线站点，也可以是提供服务的本地设置。`reject_rhbsbl_client` 限制拒绝主机。

```
smtpd_client_restrictions = reject_rbl_client relays.mail-abuse.org
```

要实现来自访问文件的限制，你可以使用`hash`指令和文件名称。

```
smtpd_client_restrictions = hash;/etc/postfix/access
```

相应的`smtpd_sender_restrictions`参数与其对应项的工作相同，但它控制来自特定服务器的访问。它具有许多限制条件，但也包含`reject_non_fqdn_sender`（它将拒绝任何没有完全限定域名的邮件头）和`reject_sender_login_match`（它将要求服务器验证）。`reject_rhbsbl_restriction` 根据指定的 `MAPS` 服务拒绝域名地址。

`smtpd_recipient_restrictions` 参数将限制服务器将接受的收件者。限制条件包括：`permit_auth_destination`（允许经过授权的消息）和 `reject_unauth_destination`（拒绝未授权的消息）。`check_recipient_unknown_recipient` 限制会检查本地网络是否存在没有 DNS 目的目的收件者地址。`reject_rhbsbl_recipient` 限制根据指定的 `MAPS` 服务拒绝域名地址。

你可以使用如`smtpd_hello_restrictions` 等参数进一步细化限制，该参数要求客户端发送`HELO`命令。限制参数包括：`reject_invalid_hostname`（检查语法错误）、`reject_unknown_hostname`（针对没有 DNS 目的目的机）以及 `reject_non_fqdn_hostname`（针对名称不完全限定的主机）。`strict_rfc821_envelopes` 参数将实现严格的协议合规。

## Sendmail

`Sendmail` 作为服务器运行，接收并发送邮件消息。`Sendmail` 对于任何从其他主机接收并发送到其所服务网络主机的邮件，处理发送给远程用户的情况，并确定将它们发送到哪些主机。你可以在`sendmail.org` 了解更多关于 `Sendmail` 的信息，包括在线文档和当前的软件包包。`Sendmail` 新闻组是`comp.sendmail.org`。你也可以从`sendmail.com` 获取商业版本。

你网络的域名服务器指定了运行 `Sendmail` 服务器的主机。这就是你的邮件主机。邮件被发送到该主机，然后 `Sendmail` 将邮件发送给适当的用户及其对应的主机。在你的域名服务器配置中，通过`MX` 条目指定邮件主机。要打印待投递的邮件队列，你可以使用`mailq`（或`sendmail -v -q`）。

# 486 第 VI 部分：互联网与网络服务

| 文件 | 描述 |
|---|---|
| `/etc/mail/sendmail.cf` | `Sendmail` 配置文件 |
| `/etc/mail/sendmail.mc` | `Sendmail` M4 宏配置文件 |
| `/etc/mail/submit.cf` | 邮件提交模式下的 `Sendmail` 配置文件，在模式模式下，`Sendmail` 不作为服务器运行，仅用于提交邮件 |
| `/etc/mail/submit.mc` | `Sendmail` 提交模式的 `Sendmail` M4 宏配置文件 |
| `/etc/aliases` | 用于邮件列表的 `Sendmail` 别名文件 |
| `/etc/mail/aliases.db` | 使用`newaliases` 命令通过`aliases` 文件生成的 `Sendmail` 别名数据库文件 |
| `/etc/mail/access` | `Sendmail` 访问文本文件；用于筛选或依赖来自不同主机、网络或用户的邮件访问控制；用于生成`access.db` |
| `/etc/mail/access.db` | `Sendmail` 访问数据库文件，由访问文本文件生成 |
| `/etc/mail/local-host-names` | 使用相同邮件服务器的多个主机的 `Sendmail` 本地（曾名为`sendmail.cw`） |
| `/etc/mail/trusted-users` | `Sendmail` 信任用户文件（曾名为`sendmail.ct`） |
| `/etc/mail/error-header` | `Sendmail` 错误头文件（曾名为`sendmail.oe`） |
| `/etc/helpfile` | `Sendmail` 帮助文件（曾名为`sendmail.ht`） |
| `/etc/mail/statistics` | `Sendmail` 统计文件（曾名为`sendmail.st`） |
| `/etc/mail/virtertable` | `Sendmail` 虚拟表文件；映射虚拟域名地址，允许在一个系统上托管虚拟域名；在此文件中创建条目并使用它生成`virtertable.db` |
| `/etc/mail/virtertable.db` | 由`virtertable` 文件生成的 `Sendmail` 虚拟表数据库 |
| `/etc/mail/mailertable` | `Sendmail` 邮件表文件，用于覆盖你所在域的路由 |
| `/etc/mail/mailertable.db` | `Sendmail` 邮件表数据库文件，由`mailertable` 文件生成 |
| `/etc/mail/userdb` | `Sendmail` 用户数据库文件 |
| `/etc/mail/domaintable` | `Sendmail` 域名表文件，将域名映射到另一个域名 |
| `/etc/mail/domaintable.db` | `Sendmail` 域名表数据库文件，由`domaintable` 文件生成 |
| `/var/spool/mail` | 入站邮件 |
| `/var/spool/mqueue` | 出站邮件 |
| `/var/spool/maillog` | 邮件日志文件 |

**表 25-2** `Sendmail` 文件与目录

# 第 25 章：邮件服务器 487

此外，`Sendmail` 仍然支持使用别名（`aliases`）来处理发送或接收的邮件。它会检查名为`aliases.db` 的数据库文件，该文件存储了别名及其关联的电子邮件地址。这通常用于管理员邮件，邮件可能会被发送到系统的`root` 并重定向到实际系统管理员的邮件地址。你也可以对主机设置别名，允许你使用别名来访问网络上的主机。别名条目保留在`/etc/aliases` 文件中。该文件由与用户相关的单行别名记录组成。你可以编辑此文件以添加新条目或更改旧条目。它们通过`newaliases` 命令存储在`aliases.db` 文件中供查找，该命令会运行`Sendmail` 并带有更新`aliases.db` 文件的指令。

允许你为一个电子邮件地址或一组电子邮件地址提供不同的名称。它最实用的功能之一是创建用户列表。发送到别名的邮件将发送给与该别名关联的用户或用户列表。别名条目由一个逗号结尾的名字组成，后跟一个用户名或用逗号分隔的用户列表。例如，要使用`filmetric` 使用用户`george@rabbit.mytrek`，你需要使用以下内容：

```
filcritic: george@rabbit.mytrek.com
```

要将本地用户`aleina` 和`larisa` 设置为别名`singers`，你使用：

```
singers: aleina, larisa
```

你也可以将别名作为目标地址，在这种情况下，它们将展开为各自的用户地址。例如，`performers` 别名将通过`filcritic` 和`singers` 展开为用户`george@rabbit.mytrek.com`、`aleina` 和`larisa`：

```
performers: filcritic, singers
```

一旦你在`/etc/mail/aliases` 文件中创建了条目，你就需要使用`newaliases` 命令创建一个数据库版本：

```
newaliases
```

> 注意：`Sendmail` 现在支持邮件提交模式，在该模式下，`Sendmail` 不作为服务器运行，并具有相应的`root` 权限。相反，它提交邮件。在这种模式下，可以直接由电子邮件客户端调用`Sendmail` 来发送邮件。邮件提交模式使用`/etc/mail/submit.cf` 配置，可以使用`/etc/mail.submit.cf` 文件中的宏进行配置。

# Sendmail 配置
