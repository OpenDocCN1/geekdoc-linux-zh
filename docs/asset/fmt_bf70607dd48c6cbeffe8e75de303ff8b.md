
```
mydestination = $hostname.$mydomain $mydomain
```

此外，如果你的主机还有其他主机名，并且有 DNS 记录通过名称识别你的主机，你也需要指定这些名称。例如，你的主机可能还是 Web 服务器，邮件可以被定向到那里。主机 `turtle.mytrek.com` 可能被识别为网站 `mytrek.com`。这两个名称都必须列在 `mydestination` 参数中。

```
mydestination = $hostname.$mydomain $mydomain $mydomain
```

如果你的系统是一个一个或多个本地网络的网关，你可以使用 `networks` 参数指定它们。这允许你的邮件服务器向这些网络中继邮件。网络使用其 IP 地址指定。`relay_domains` 参数允许你指定你可以中继消息的网络域名地址。默认情况下，它设置为 `mydestination`：

```
networks=192.168.0.0
relay_domains=$mydomain
```

通过网关连接到互联网的本地网络内的主机需要知道中继主机（邮件服务器）的身份。你通过 `relayhost` 参数进行设置。此外，`myorigin` 应该设置为 `mydomain`。如果有一个 DNS 服务器将网关识别为邮件服务器，你可以将 `relayhost` 设置为 `mydomain` 的值。如果没有，`relayhost` 将设置为网关/邮件服务器的特定主机名。如果你的本地网络没有运行 DNS 服务器，请将 `disable_dns_lookups` 设置为 `yes`。

```
relay_host=$mydomain
```

## 直接连接

如果你的系统直接连接到互联网，并且你使用 ISP（互联网服务提供商）来接收邮件，你可以将 Postfix 配置为空客户端（null client），仅发送邮件。将 `relay_host` 参数设置为你自己的域名。此外，在 `master.cf` 文件中，注释掉 SMTP 服务器和本地投递代理条目。

```
relay_host = $mydomain
```

## 伪装 Masquerading

如果你的邮件服务器作为本地网络的网关运行，并且你想隐藏该网络中的主机，你可以对本地主机进行伪装，让所有邮件看起来都来自该域名，而不是特定的主机。要设置此选项，你使用 `masquerade_domains` 参数。在本例中，由本地主机（如 `rabbit.mytrek.com`）发送的所有邮件都将被标记为来自 `mytrek.com`。由用户 `chris@rabbit.mytrek.com` 发送的消息将从 `chris@mytrek.com` 发出：

```
masquerade_domains = $mydomain
```

默认情况下，收到的邮件不会被伪装。这允许 Postfix 仍然可以投递到特定主机。如果你希望收到的邮件也进行伪装，你必须将 `envelope_recipients` 参数添加到分配给 `masquerade_class` 参数的值列表中。在这种情况下，Postfix 将不再能够投递邮件。

## 虚拟域名和虚拟账户

如果你的网络实现了虚拟域名，你将需要设置一个虚拟域名表，并使用 `virtual_maps` 指定该表。建立表是一件简单，在 `/etc/postfix/virtual` 等文本文件中列出虚拟名称及其真实地址即可。然后使用 `postmap` 命令创建 Postfix 表：

```
/etc/postfix/virtual
(run postmap /etc/postfix/virtual)
```

在 `main.cf` 文件中，使用 `virtual_maps` 参数指定该表。Postfix 将使用此表来查找虚拟域名。

```
virtual_maps = hash:/etc/postfix/virtual
```

注意：请访问 www.postfix.org 查看 Postfix FAQ 获取有关如何为网关、本地工作站或直接连接互联网的主机（空服务器）设置 Postfix 的详细信息。

你可以设置虚拟账户，而不是使用系统上的实际用户。虚拟账户可以在标准的 Postfix 文本文件、SQL 数据库或作为 LDAP 别名进行管理。SQL 数据库优于管理大量的虚拟账户。为了支持 SQL，你需要在 MySQL 数据库中为（虚拟域名）、用户（用户账户）和转发（别名）创建表。相应的虚拟域名配置文件将列出使用的数据库、表和主机，例如用于访问 SQL 数据库的 `mysql_virt.cf` 和用于访问用户表的 `mysql_users.cf`。查看 www.postfix.org 文档获取详细信息。

## Postfix 灰名单策略服务器

Postfix 还支持通过灰名单策略服务器（`postgrey` 包）拦截垃圾邮件发送者。灰名单根据邮件方式而非内容拦截垃圾邮件发送者，基于垃圾邮件发送者在拒绝后不会尝试重试的事实（greylisting.org）。来自之前未知源的消息会被拒绝，而有效的 MTA 将重试，但垃圾邮件发送者则不会。为了支持灰名单策略服务器，Postfix 配置为将策略访问权限委托给服务器。在 `/etc/postfix/` 目录中，你可以使用 `postgrey_whitelist` 文件将电子邮件地址排除在灰名单之外。灰名单策略服务器作为独立服务器运行，使用它自己的启动脚本。Postgrey 手页提供了有关服务器选项的详细信息。

对于密集工作，你可以使用 SQL 灰名单策略服务器（`sqlgrey` 包）。该服务器使用 SQL 数据库后端处理灰名单任务。更多详情见 http://sqlgrey.sourceforge.net。

## 控制用户和主机访问

通过访问文件，你可以控制特定用户、主机和域的访问。访问文件的工作方式与 Sendmail 非常相似。条目由用户、主机或域名创建，后跟跟要执行的操作。你使用 `postmap` 命令：

```
postmap /etc/postfix/access
```

访问也可以通过邮件滥用预防系统（MAPS）控制，它提供了一个已知滥用者的列表。这些数据库（如实时黑洞列表 RBL）可以在本地服务器上访问，也可以直接访问。

## 头部和正文检查

通过 `header_checks` 参数，你可以指定一个 Postfix 表，在表中你可以列出拒绝消息的标准。检查 `/etc/postfix/header_checks` 文件获取详情。标准是能够匹配头部的模式。你可以让匹配的消息被拒绝、带回复的拒绝、简单删除或带有警告的记录。你可以选择采取几种操作，包括 `REJECT`、`DISCARD`、`WARN`、`HOLD` 和 `IGNORE`。

```
header_checks = regexp:/etc/postfix/header_checks
```

`body_checks` 参数允许你使用正则表达式逐行检查文本消息的正文，使用的操作类似于 `/etc/postfix/body_checks` 文件中用于 `header_checks` 的操作。

# 第 4 部分：网络服务

要实现来自访问文件的限制，你可以使用 `hash` 指令和文件名。

`smtpd_client_restrictions = hash://etc/postfix/access`

`smtpd_sender_restrictions` 参数的工作原理与其对应的参数许多相似，但它控制来自特定发送者的访问。它具有许多相同的限制，但增加了 `reject_non_fqdn_sender`（它会拒绝任何不包含完全限定域名的邮件头）以及 `reject_sender_login_mismatch`（它要求进行此类验证）。`reject_hsbsbl_sender_restriction` 限制会拒绝发送到指定 MAPS 服务的域名地址。

`smtpd_recipient_restrictions` 参数将限制服务器接受邮件的收件者。限制包括 `permit_auth_destination`（允许已授权的消息）和 `reject_unauth_destination`（拒绝未授权的消息）。`check_recipient_access` 限制将检查收件者地址所在的网络。`reject_unknown_recipient_domain` 限制会拒绝没有 DNS 记录的收件者地址。`reject_hsbsbl_recipient` 限制会拒绝发送到指定 MAPS 服务的域名地址。

你可以使用参数进一步细化限制，例如 `smptd_helo_hostname`（要求 HELO 主机名并检查错误的语法）、`reject_unknown_hostname`（针对没有 DNS 记录的主机）以及 `reject_non_fqdn_hostname`（针对名称不是完全限定的主机）。`strict_rfc821_envelopes` 参数将实现严格的协议合规性。

# Sendmail

Sendmail 作为服务器运行，用于接收和发送邮件。Sendmail 监听从其他主机接收并发送给其服务网络内用户的邮件。同时，Sendmail 处理发送给远程用户的消息，并确定哪些主机向他们发送消息。你可以在 [www.sendmail.org](http://www.sendmail.org) 学习更多关于 Sendmail 的信息，包括在线文档和当前的软件包。Sendmail 新闻组是 comp.sendmail.com。你也可以从 [www.sendmail.com](http://www.sendmail.com) 获取商业版本。

你网络的域名服务器指定运行 Sendmail 服务器的主机。这就是你的邮件主机。邮件被发送到该主机，由该主机的 Sendmail 服务器将邮件发送给相应的用户。在你的域名服务器配置文件中，邮件主机条目带有 MX 记录存在。要打印用于未来交付的邮件队列，可以使用 `mailq`（或 `sendmail -v -q`）。这会运行 Sendmail 并带有打印邮件队列的指令。

Sendmail 软件包含几个用于管理 Sendmail 服务器的实用工具。这些包括 `mailq`（显示传出邮件队列）、`mailstats`（显示邮件服务器使用的统计数据）、`hoststat`（提供连接邮件服务器的远程主机状态）以及 `paliases`（打印 `/etc/aliases` 文件中列出的邮件别名）。像 `mailq` 和 `hoststat` 这样的工具仅仅是带有特定选项调用 Sendmail。其他像 `mailstats` 和 `paliases` 则是独立的程序。

# 第 20 章：邮件服务器

| 文件 | 描述 |
| :--- | :--- |
| `/etc/mail/sendmail.cf` | Sendmail 配置文件 |
| `/etc/mail/sendmail.mc` | Sendmail M4 宏配置文件 |
| `/etc/mail/submit.cf` | Sendmail 邮件提交模式配置文件，在此模式下 Sendmail 不作为服务器运行，仅提交邮件。 |
| `/etc/mail/submit.mc` | Sendmail 提交模式的 Sendmail M4 宏配置文件 |
| `/etc/aliases` | 用于邮件列表的 Sendmail 别名文件 |
| `/etc/mail/aliases.db` | 使用 `newaliases` 命令根据别名文件生成的 Send 别名数据库文件 |
| `/etc/mail/access` | Sendmail 访问文本文件。控制来自不同主机、网络或用户的邮件筛选或中继。用于生成访问数据库 |
| `/etc/mail/access.db` | Sendmail 访问数据库文件。从访问文本文件生成 |
| `/etc/mail/local-host-names` | 使用同一邮件服务器的主机的 Sendmail 本地主机（原名为 sendmail.cw） |
| `/etc/mail/trusted-users` | Sendmail 受信任用户文件（原名为 sendmail.ct） |
| `/etc/mail/statistics` | Sendmail 统计文件（原名为 sendmail.st） |
| `/etc/mail/virtertable` | Sendmail 虚拟用户表文本文件。映射用户虚拟域名地址，允许虚拟域名托管在一个系统上。在此文件中创建条目并使用其生成 virtertable.db |
| `/etc/mail/virtertable.db` | 从 virtertable 文件生成的 Sendmail 虚拟用户表数据库 |
| `/etc/mail/mailertable` | Sendmail 邮件表文本文件，用于覆盖你域域的路由 |
| `/etc/mail/mailertable.db` | 从 mailertable 文件生成的 Sendmail 邮件表数据库文件 |
| `/etc/mail/userdb` | Sendmail 用户数据库 |
| `/etc/mail/domaintable` | Sendmail 域名表文件，将域名映射到另一个域名 |
| `/etc/mail/domaintable.db` | 从 domaintable 文件生成的 Sendmail 域名表数据库文件 |
| `/var/spool/mail` | 入站邮件 |
| `/var/spool/mqueue` | 出站邮件 |
| `/var/spool/maillog` | 邮件日志文件 |

表 20-2：Sendmail 文件和目录

# 第 4 部分：网络服务

Sendmail 现在将所有配置和数据库文件维护在 `/etc/mail` 目录中。在这里你会找到 Sendmail 宏配置文件 `sendmail.mc`，以及几个数据库文件（见表 20-2）。在 Sendmail 8.10 发布时，许多文件已更改了名称。专门的文件提供了某些功能的支持，例如 `access`（允许访问不同的主机和网络）和 `virtertable`（允许指定虚拟主机）。这些文件都有文本和数据库版本。数据库版本使用 `.db` 并由 Sendmail 实际使用。文本版本使用带选项 `make` 命令。例如，要拒绝对特定主机的访问，你可以使用任何文本编辑器在 `/etc/mail/access` 中放置相应的条目。要生成文件的 access.db 版本，你需要更改 /etc/mail 目录并使用以下命令：

```bash
cd /etc/mail
makemap hash < access
```

要重新生成所有数据库文件，请在 `/etc/mail` 目录下使用 `make` 命令：

```bash
make
```

入站邮件通常保存在 `/var/spool/mail` 目录下，按用户设有子目录。监控和错误消息记录在 `/var/log/maillog` 文件中。

> 注意：Red Hat 和 Fedora 使用 `/etc/mail` 目录下的 Sendmail 配置文件 `sendmail.cf`，而不是以前版本（7.3 及以前）中的 /etc 目录。

> 注意：如果你的邮件服务器服务于多个主机，你需要在 /etc/mail/local-host-names 文件中输入它们。

# 别名与 LDAP

Sendmail 现在支持轻量目录访问协议（LDAP）。LDAP 允许使用独立的服务器来管理跨邮件地址的查询。无需在不同服务器上维护别名和虚拟用户表，Sendmail 使用 LDAP 支持直接使用一个集中 LDAP 来接收位置。地址在 LDAP 服务器中查找，而不是在多个服务器的多个别名和虚拟用户表中搜索。LDAP 还为用户提供了安全的身份验证，允许访问邮件帐户。以下示例在 `sendmail.mc` 文件中为 Sendmail 启用 LDAP：

```mail
FEATURE('ldap_routing') dnl
LDAPROUTE_DOMAIN('mytrek.com') dnl
```

或者，Sendmail 仍然支持别名的数据库文件，用于接收邮件。它会检查名为 `aliases.db` 的数据库文件，该文件包含别名名称及其电子邮件地址。这通常用于管理员邮件，邮件可能发送到系统用户，然后重定向到实际系统管理员的邮件地址。你还可以为主机地址设置别名，以便仅使用其别名即可访问网络上的主机。别名条目

## 第 20 章：邮件服务器

别名存储在 `/etc/aliases` 文件中。该文件由单行别名记录组成，将别名与用户地址关联。你可以编辑此文件以添加新条目或更改旧条目。它们通过 `newaliases` 命令存储在 `aliases.db` 文件中以便，该命令运行 Sendmail 指令来更新 `aliases.db` 文件。

别名允许你为电子邮件地址或一组电子邮件地址提供不同的名称。其最实用的功能之一是创建用户邮件列表。发送到别名的邮件将发送给与别名关联的用户或用户列表。别名条目由由冒号命名的别名和随后的用户名、用逗号分隔的用户列表组成。例如，要将 `filmcritic` 别名为用户 `george@rabbit.mytrek.com`，你可以使用以下命令：

```
filmcritic: george@rabbit.mytrek.com
```

将 `singers` 别名为本地用户 `aleina` 和 `larisa`，你应该使用：

```
singers: aleina, larisa
```

你也可以将别名作为目标地址，在这种情况下，它们将展开为各自的用户地址。例如，表演者 `filmcritic` 和 `singers` 别名指向用户 `george@rabbit.mytrek.com`、`aleina` 和 `larisa`：

```
performers: filmcritic, singers
```

一旦你在 `/etc/mail/aliases` 文件中创建了条目，你需要使用 `newaliases` 命令生成数据库版本：

```
newaliases
```
