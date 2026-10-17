
如第 1 章所述，邮件地址由用户名和主机地址组成。主机地址的形式为完全限定域名（FQDN），列出主机名和域名，并用点分隔。大多数主机名的用法（如 `FTP` 连接）会将主机名转换为 `IP` 地址，并使用 `IP` 地址定位主机系统。邮件消息的操作方式几乎相同。然而，它们利用域名服务（`DNS`）来确定实际上将消息发送到哪个主机。邮件地址中指定的主机可能并不是实际投递的目标的主机。不同的网络通常会指定一个邮件服务器，网络内主机的邮件应该投递到该服务器。例如，发送给 `rabbit.mytrek.com` 主机的邮件可能会投递到 `turtle.mytrek.com` 主机。`turtle.mytrek.com` 可能运行着一个 `rabbit.mytrek.com` 可以访问并读取邮件的 `POP` 邮件服务器。

此类邮件服务器通过网络 `DNS` 配置中的邮件交换记录（称为 `MX` 记录）与不同的主机相关（参见第 22 章）。当网络中接收到邮件时，首先会检查网络 `DNS` 配置中的 `MX` 记录，以确定邮件是否应该投递到与邮件地址中不同的主机。例如，以下 `MX` 记录表明，任何发送给 `rabbit.mytrek.com` 主机的邮件都要投递到 `turtle.mytrek.com` 主机。`turtle.mytrek.com` 是 `rabbit.mytrek.com` 的邮件交换器。

```
rabbit.mytrek.com. IN MX turtle.mytrek.com.
```

一个主机可能有多个邮件交换器，每个都有不同的优先级。如果其中一个宕机，将访问下一个优先级最高的。这种设计提供了更健壮的邮件投递，让几台维护良好的服务器处理邮件，而不是让每个主机都自行处理。

交换记录也用于没有对应主机的邮件地址。例如，你可以指定虚拟主机或使用域名作为地址。要使用域名，你需要一个 `MX` 记录，将域名映射到网络上的一个邮件服务器。发送到该域名的邮件将发送到该邮件服务器。例如，通过以下 `MX` 记录，发送到 `mytrek.com` 的邮件将投递到 `turtle.mytrek.com`，该处运行着类似 `Sendmail` 的邮件服务器：

```
mytrek.com. IN MX 0 turtle.mytrek.com.
```

发送到 `george@mytrek.com` 的邮件将发送到 `george@turtle.mytrek.com`。

> `MX` 记录不仅用于传入的邮件，也用于传出的邮件。`MX` 记录可以指定邮件服务器来处理来自给定主机的邮件。在某些特定的 `Sendmail` 配置中，`MX` 记录是必需的。如果你有一个独立系统或只有几个主机的网络，你可能希望直接接收邮件。

## Postfix

> 注：原文此处存在大量重复的文本片段，根据指令“不要重复输出原文”，翻译部分已精简或仅保留逻辑结构，若原文为无意义重复，此处按文档规范处理。由于原文内容为大量重复的填充句，此处仅翻译核心含义部分。

## 第 23 章：邮件服务器：SMTP、POP 和 IMAP

| 文件 | 描述 |
|---|---|
| `/etc/mail/mailertable.db` | `Sendmail` 邮件传输器表数据库文件，由 `mailertable` 文件生成。 |
| `/etc/mail/user` | `Sendmail` 用户数据库文件。 |
| `/etc/mail/domaintable` | `Sendmail` 域名表，将一个域名映射到另一个域名。 |
| `/etc/mail/domaintable` | `Sendmail` 域名表数据库文件，由 `domainable` 文件生成。 |
| `/var/spool/mail` | 入站邮件。 |
| `/var/spool/mqueue` | 出站邮件。 |
| `/var/spool/maillog` | 邮件日志文件。 |

表 23-3. `Sendmail` 文件和目录（续）

在 `Sendmail` 8.10 版本中，例如，帮助文件是 `/etc/mail/helpfile` 而不是 `/etc/sendmail.ht`。特殊文件为某些功能提供了支持，例如访问控制（`access`），允许你控制不同的主机和网络对你邮件服务器的访问。`virtertable` 允许你指定虚拟主机。这些文件同时具有文本版本和数据库版本。数据库版本以 `.db` 结尾，是 `Sendmail` 实际使用的文件。你可以在文本版本中输入条目，然后通过生成相应的数据库文件使更改生效。数据库版本是使用 `makemap` 命令配合 `hash` 选项以及对文本和数据库文件进行重定向来生成的。例如，要拒绝某个特定主机的访问，你将使用任何文本编辑器编辑 `/etc/mail/access` 文件，并在其中放置相应的条目。然后，使用以下命令生成 `/etc/mail/access.db` 版本的访问文件：

```
cd /etc/mail
makemap hash access < access
```

要重新生成数据库文件，只需在 `/etc/mail` 目录下使用 `make` 命令：

- `make`

某些文件和目录用于管理收到的和发送的邮件。入站邮件保留在 `/var/spool/mail` 目录下，出站消息保存在 `/var/spool/mqueue` 目录下，并有针对不同用户的子目录。监控和错误信息记录在 `/var/log/mailog` 文件中。

> `Red Hat` 将 `Sendmail` 配置文件 `sendmail.cf` 放在 `/etc` 目录下，而不是 `/etc/mail` 目录。
>
> 如果你的邮件服务器为多个主机提供服务，你需要在 `/etc/mail/local-hosts` 文件中输入它们。

## 别名与 LDAP

在 `Sendmail` 8.10 中，`Sendmail` 现在支持使用轻量级目录访问协议（`LDAP`）。`LDAP` 允许使用独立的服务器来管理关于用户邮件地址的查询。与其在不同的服务器上维护别名文件和 `virtertable` 文件，`LDAP` 支持允许 `Sendmail` 使用一个集中的 `LDAP` 服务器来查找收件者。邮件地址在 `LDAP` 服务器中查找，而不是在不同的服务器上搜索 `virtertable` 文件。`LDAP` 还提供了对用户的安全身份验证，允许对邮件账户进行受控访问。以下示例在 `sendmail.mc` 文件中启用 `Sendmail` 的 `LDAP` 支持：

```
FEATURE ('ldap_routing') dnl
LDAPROUTE_DOMAIN('mytrek.com') dnl
```

或者，`Sendmail` 仍然支持在发送或接收邮件时使用别名。它会检查一个名为 `aliases.db` 的别名数据库，该数据库存储了别名及其关联电子邮件地址。这通常用于管理员邮件，邮件可能会发送给系统的 `root` 用户，并重定向到实际系统管理员的邮件地址。你也可以对主机设置别名，允许你仅通过别名对网络上的主机进行地址。别名条目保留在 `/etc/aliases` 文件中。该文件由行记录组成，说明别名与用户之间的关系。你可以编辑此文件以添加新条目或更改旧条目。它们使用 `newaliases` 命令存储在 `aliases.db` 文件中供查找，该命令运行 `Sendmail` 并带有更新 `aliases.db` 文件的指令。

别名允许你为电子邮件地址或一组电子邮件地址提供不同的名称。它最强大的功能之一是创建用户邮件列表。发送到别名的邮件将发送给与该别名关联的用户或用户列表。别名由一个以冒号结尾的别名以及随后的用户名或用逗号分隔的用户列表组成。例如，将别名 `filmcritic` 指用户 `george@rabbit.mytrek.com`，你需要使用以下格式：

```
filmcritic: george@rabbit.mytrek.com
```

要为本地用户 `aleina` 和 `larisa` 设置歌手别名，你可以使用

- `singers: aleina, larisa`

你还可以将别名作为目标地址，在这种情况下它们将扩展为各自的用户地址。例如，`performers` 别名将通过 `filmcritic` 和 `singers` 别名扩展到用户 `george@rabbit.mytrek.com`、`aleina` 和 `larisa`。

- `performers: filmcritic`

一旦你在 `/etc/mail/aliases` 文件中创建了条目，就需要使用 `newaliases` 命令生成数据库。

## Sendmail 配置

`Sendmail` 的主配置文件 `sendmail.cf` 位于 `/etc` 目录。该文件包含了大量的选项定义、`MTA`（邮件传输代理）设置以及规则，例如邮件的大小限制等。`MTA` 是负责路由邮件的程序。为了简化配置，`Sendmail` 使用了 `sendmail.mc` 文件。

# 第 23 章：邮件服务器：SMTP、POP 和 IMAP

| 特性 | 描述 |
| --- | --- |
| `use_cw_file` | 检查由 `/etc/mail/local-host-names` 文件提供的由邮件服务器服务的主机 |
