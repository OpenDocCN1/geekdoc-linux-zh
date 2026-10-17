
```
uid=eric, o=sendmail.com, c=US
objectClass: inetLocalMailRecipient
mailLocalAddress: eric@sendmail.org
mailRoutingAddress: eric@eng.sendmail.com
```

会导致发至 `eric@sendmail.org`（由 DNS MX 记录导致投递到 `sendmail.com`）的邮件发送到 `eric@eng.sendmail.com`。如果该条目列出了该行：

`mailHost: mailserver.sendmail.com`

那么发往 `eric@sendmail.org` 的邮件将地址定为 `eric@eng.sendmail.com`，并发送到具有 `mailserver` 最佳 MX 记录的主机。

LDAP 数据库条目支持通配符条目 `@domain`，它可以重路由发至指定域的邮件（如在 `virtuosertable` 中所示）。

# 伪装与 MASQUERADE_AS 宏

`MASQUERADE_AS` 宏允许你指定一个其他身份可以隐藏的单一身份。所有邮件似乎都源自指定的机器或域。发送者地址被重写为 `user@masquerading-name` 而不是 `user@original-host.com`。当然，这些伪装的地址必须是有效的，以便人们可以回复邮件。

此配置允许所有用户使用通用的电子邮件地址。例如，如果 `xor.com` 的所有主机都伪装在 `xor.com` 域之后，那么来自 `user@host.xor.com` 的邮件将被加盖为来自发送邮件的用户的实际主机。代表 `xor.com` 的机器必须知道如何投递所有用户的邮件，即使对于那些在入站邮件服务器上没有登录的用户也是如此。自然地，登录名在整个域内必须唯一的。

某些用户和地址（如 `root`, `postmaster`, `hostmaster`, `operations`, `Mailer-Daemon` 等）应该从这种行为中排除。可以使用 `EXPOSED_USER` 宏显式排除。例如，以下序列：

```
MASQUERADE_AS(xor.com)
EXPOSED_USER('root')
EXPOSED_USER('Mailer-Daemon')
```

将对来自 `user@xor.com` 的邮件加盖章，除非它是由 `root` 或邮件系统发送的；在这些情况下，邮件将带有源主机的名称。

基础 `MASQUERADE_AS` 宏有几种扩展，均通过其他宏和 `FEATURES` 实现：

- `MASQUERADE_DOMAIN` 宏
- `MASQUERADE_DOMAIN_FILE` 宏
- `MASQUERADE_EXCEPTION` 宏
- `limited_masquerade` FEATURE
- `allmasquerade` FEATURE
- `masquerade_envelope_domain` FEATURE
- `masquerade_entire_domain` FEATURE

我们建议使用上述 `MASQUERADE_AS` 宏，并结合 `allmasquerade` 和 `masquerade_envelope` 特一起使用。`limited_masquerade` 功能修改了 `MASQUERADE_DOMAIN` 的行为，对于虚拟主机环境非常有用。`MASQUERADE_DOMAIN` 列出了你用于伪装的域；该列表从通常使用 `use_cw_file` 功能定义的 `w` 类中预加载，并列出你域中的主机。`limited_masquerade` 不会用 `w` 预初始化列表。所有域将将被你正在伪装的域所隐藏。

`allmasquerade` 功能将伪装扩展到消息的接收者（与发送者相反），而 `masquerade_envelope` 功能将其扩展到信封以及标头地址。² 通过这两个扩展，地址将以一致的方式被隐藏。`limited_masquerade` 功能将伪装扩展到指定的其他域列表。

如果你想使用其他的伪装技术，可以在 `cf/README` 文件或 `sendmail` 书中阅读关于它们行为的内容。请仔细阅读；某些伪装原语可能会让你隐藏得太深。

# MAIL_HUB 和 SMART_HOST 宏

伪装通过重写标头（可选的重写信封）使所有邮件看起来都来自同一个主机或域。某些站点可能希望所有邮件都来自（或发往）单台机器。你可以通过用于入站邮件的 `MAIL_HUB` 宏和用于出站邮件的 `SMART_HOST` 宏来实现配置。

如果你想将所有入站邮件路由到中央服务器，将 `MAIL_HUB` 设置为值 `mail:host`，其中 `mail` 是你用于访问指定主机的代理。如果没有指定代理，则使用 `relay`。例如：

```
define('MAIL_HUB', 'smtp:mailhub.cs.colorado.edu')
```

`SMART_HOST` 指定允许主机通过将邮件转交给 `SMART_HOST` 来投递本地邮件。此功能对于无法直接使用 DNS 的防火墙后的机器有用。它的语法与 `MAIL_HUB` Parallel；默认投递代理是 `agent relay`。例如：

```
define('SMART_HOST', 'smtp:mailhub.cs.colorado.edu')
```

+ 22. 标头地址是出现在消息标头中的 To、From 和 Bcc 地址。信封地址是邮件实际投递的地址。这些地址最初由用户代理从标头地址构建，但由 `sendmail` 独立处理。如果不维持标头地址和信封地址之间的区别，`sendmail` 的许多伪装和重定向功能将无法实现。

# 第19章 电子邮件 585

在这些示例中，同一台机器同时充当入站和出站邮件的服务器。较大的站点可能会将这些拆分到不同的机器上。

# 伪装与路由

使用所有这些功能，在这些示例中，同一台机器同时充当入站和出站邮件的服务器。较大的站点可能会将这些拆分到不同的机器上。

# 第19章 电子邮件 583

例如，LDAP 条目（针对配置根区分名称为 `cn=root, o=sendmail.com, c=US` 的服务器）

```
uid=eric, o=sendmail.com, c=US
objectClass: inetLocalMailRecipient
mailLocalAddress: eric@sendmail.org
mailRoutingAddress: eric@eng.sendmail.com
```

会导致发至 `eric@sendmail.org`（由 DNS MX 记录导致投递到 `sendmail.com`）的邮件发送到 `eric@eng.sendmail.com`。如果该条目列出了该行：

`mailHost: mailserver.sendmail.com`

那么发往 `eric@sendmail.org` 的邮件将地址定为 `eric@eng.sendmail.com`，并发送到具有 `mailserver` 最佳 MX 记录的主机。

LDAP 数据库条目支持通配符条目 `@domain`，它可以重路由发至指定域的邮件（如在 `virtuosertable` 中所示）。

# 伪装与 MASQUERADE_AS 宏

`MASQUERADE_AS` 宏允许你指定一个其他身份可以隐藏的单一身份。所有邮件似乎都源自指定的机器或域。发送者地址被重写为 `user@masquerading-name` 而不是 `user@original-host.com`。当然，这些伪装的地址必须是有效的，以便人们可以回复邮件。
