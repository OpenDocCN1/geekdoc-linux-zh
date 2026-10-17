
Sendmail 现在将所有配置和数据库文件保存在 `/etc/mail` 目录中。在这里你会找到 Sendmail 宏配置文件 `sendmail.mc`，以及多个数据库文件（见表 24-2）。许多文件在 Sendmail 8.10 发布时已更改名称。例如，帮助文件现在是 `/etc/mail/helpfile` 而不是 `/etc/sendmail.ht`。专用文件为某些功能提供支持，例如 `access`，它让你控制不同主机和网络对邮件服务器的访问。`virtusertable` 让你指定虚拟主机。这些文件都有文本和数据库版本。数据库版本以 `.db` 扩展名结尾，是 Sendmail 实际使用的文件。你将在文本版本中进行条目，然后通过生成相应的数据库版本来生效更改。数据库版本使用 `makemap` 命令配合 `hash` 选项以及文本和数据库文件的重定向操作来生成。例如，要拒绝特定主机的访问，你将在 `/etc/mail/access` 文件中为其放置适当的条目，使用任何文本文字处理器编辑文件。然后，要生成 `/etc/mail/access.db` 版本的 `access` 文件，你将切换到 `/etc/mail` 目录并使用以下命令：

```
cd /etc/mail
makemap hash access < access
```

要重新生成所有数据库文件，只需在 `/etc/mail` 目录中使用 `make` 命令：

```
make
```

某些文件和目录用于管理收发邮件。传入邮件通常保存在 `/var/spool/mail` 目录中，而传出消息则保存在 `/var/spool/mqueue` 目录中，并为不同用户设有子目录。监控和错误消息记录在 `/var/log/maillog` 文件中。

> NOTE Red Hat 现在将 Sendmail 配置文件 `sendmail.cf` 放在 `/etc/mail` 目录中，而不是像以前版本（7.3 及更早）那样放在 `/etc` 目录中。

| File | Description |
|---|---|
| `/etc/mail/sendmail.cf` | Sendmail 配置文件。 |
| `/etc/mail/sendmail.mc` | Sendmail M4 宏配置文件。 |
| `/etc/aliases` | Sendmail 别名文件，用于邮件列表。 |
| `/etc/aliases.db` | Sendmail 别名数据库文件，由 `newaliases` 命令使用别名文件生成。 |
| `/etc/mail/access` | Sendmail access 文本文件。用于筛选或中继来自不同主机、网络或用户的消息的访问控制。用于生成 `access.db` 文件。 |
| `/etc/mail/access.db` | Sendmail access 数据库文件。从 access 文本文件生成。 |
| `/etc/mail/local-host-names` | Sendmail 本地主机文件，用于使用同一邮件服务器的多个主机（以前为 `sendmail.cw`）。 |
| `/etc/mail/trusted-users` | Sendmail 受信任用户文件（以前为 `sendmail.ct`）。 |
| `/etc/mail/error-header` | Sendmail 错误头文件（以前为 `sendmail.oE`）。 |
| `/etc/mail/helpfile` | Sendmail 帮助文件（以前为 `sendmail.ht`）。 |
| `/etc/mail/statistics` | Sendmail 统计文件（以前为 `sendmail.st`）。 |
| `/etc/mail/virtusertable` | Sendmail 虚拟用户表文本文件。映射用户虚拟域地址，允许在同一系统上托管虚拟域。在此文件中添加条目，然后使用它生成 `virtusertable.db` 文件。 |
| `/etc/mail/virtusertable.db` | Sendmail 虚拟用户表数据库，由 `virtusertable` 文件生成。 |
| `/etc/mail/mailertable` | Sendmail 邮件路由表文本文件，用于覆盖你的域的路由。 |
| `/etc/mail/mailertable.db` | Sendmail 邮件路由表数据库文件，由 `mailertable` 文件生成。 |
| `/etc/mail/userdb` | Sendmail 用户数据库文件。 |
| `/etc/mail/domaintable` | Sendmail `domaintable` 文件，将域名映射到另一个域名。 |
| `/etc/mail/domaintable.db` | Sendmail `domaintable` 数据库文件，由 `domaintable` 文件生成。 |
| 文件 | 描述 |
|---|---|
| `/var/spool/mail` | 传入邮件。 |
| `/var/spool/mqueue` | 传出邮件。 |
| `/var/spool/maillog` | 邮件日志文件。 |

表 24-2 Sendmail 文件和目录（续）

> 注意：如果您的邮件服务器为多个主机提供服务，您需要在 `/etc/mail/local-host-names` 文件中输入这些主机。

## 别名与 LDAP

从 Sendmail 8.10 开始，Sendmail 现在可以支持轻量目录访问协议（LDAP）。LDAP 允许使用单独的服务器来管理 Sendmail 对用户邮件地址的查询。无需在不同服务器上维护别名和 `virtusertable` 文件，Sendmail 利用 LDAP 支持，只需使用一个集中式 LDAP 服务器即可定位收件人。邮件地址在 LDAP 服务器中查找，而无需在不同服务器上搜索多个别名和 `virtusertable` 文件。LDAP 还提供用户安全认证，允许对邮件帐户进行受控访问。以下示例在 `sendmail.mc` 文件中启用 Sendmail 的 LDAP 支持：

```
FEATURE(`ldap_routing')dnl
LDAPROUTE_DOMAIN(`mytrek.com')dnl
```

另外，Sendmail 仍然支持对发送或接收邮件使用别名。它会检查一个名为 `aliases.db` 的别名数据库文件，其中保存着别名及其关联的电子邮件地址。这通常用于管理员邮件，邮件可能会发送到系统的 `root` 用户，然后重定向到实际系统管理员的邮件地址。您还可以为主机地址设置别名，从而仅使用主机别名即可访问网络上的主机。别名条目保存在 `/etc/aliases` 文件中。该文件由一行行的别名记录组成，将别名与用户地址关联起来。您可以编辑此文件来添加新条目或修改旧条目。然后使用 `newaliases` 命令将它们存储在 `aliases.db` 文件中以供查找，该命令以更新 `aliases.db` 文件的指令运行 Sendmail。

别名允许您为一个电子邮件地址或一组电子邮件地址指定不同名称。它最有用的功能之一是创建用户邮件列表。发送到别名的邮件将被发送到与该别名关联的用户或用户列表。别名条目由以冒号结尾的别名组成，后跟一个用户名或以逗号分隔的用户列表。例如，要将别名 `filmcritic` 关联到用户 `george@rabbit.mytrek.com`，您可以使用以下条目：

```
filmcritic:    george@rabbit.mytrek.com
```

要将别名 `singers` 关联到本地用户 `aleina` 和 `larisa`，您可以使用

```
singers:    aleina, larisa
```

您也可以将别名用作目标地址，在这种情况下，它们将展开为各自的用户地址。例如，`performers` 别名将通过 `filmcritic` 和 `singers` 别名展开为 `george@rabbit.mytrek.com`、`aleina` 和 `larisa` 用户。

```
performers:  filmcritic; singers
```

在 `/etc/mail/aliases` 文件中完成条目添加后，您需要使用 `newaliases` 命令生成数据库版本：

```
newaliases
```

## Sendmail 配置

Sendmail 的主配置文件是位于 `/etc` 目录下的 `sendmail.cf`。该文件包含一长串邮件定义，这些定义设置常规选项、指定 MTA，并定义地址重写规则。一系列选项用于设置功能，例如邮件消息的最大大小或主机文件的名称。MTA 是 Sendmail 用来路由消息的邮件程序。重写规则会“重写”邮件地址，以便通过适当的 Internet 连接路由到其目的地（这些规则可能很复杂）。有关详细说明，请查看 Sendmail HOW-TO 和在线文档。
