
# 邮件服务器：SMTP、POP 和 IMAP

在每个阶段，都会使用不同的代理（程序）进行不同类型的操作。邮件用户代理 (MUA) 是客户端程序，例如 `mail` 或 `Elm`。通过 MUA，用户编写并发送邮件消息。然后，邮件传输代理 (MTA) 在互联网上传输邮件。MTA 是使用 SMTP 将邮件从一台服务器发送到另一台服务器的邮件服务器，在子网之间传输邮件。在 Linux 和 Unix 系统上，常用的 MTA 是 Sendmail，它是一个守护进程不断检查来自其他邮件服务器的传入邮件，并将传出的邮件发送到相应的服务器。其他流行的 MTA 还有 Postfix、exim 和 Qmail（见表 23-1）。邮件服务器接收的传入邮件通过邮件投递代理 (MDA) 分发给用户。大多数 Linux 系统使用 `procmail` 作为它们的 MDA，将邮件服务器接收的邮件投递到用户账户（更多信息请访问 www.procmail.org）。

| 代理 | 描述 |
| --- | --- |
| Sendmail | Sendmail 邮件传输代理 www.sendmail.com |
| Postfix | 快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 www.postfix.org |
| Qmail | 快速、灵活且安全的 MTA，拥有自己的实现并可与 Postfix 竞争 www.qmail.org |
| Exim | 基于 sm3 的 MTA www.exim.org |
| Courier | Courier MTA www.courier-mta.org |

**表 23-1.** 邮件传输代理

大多数 Linux 发行版都会自动为你安装并配置 Sendmail，尽管某些发行版也包含了 Postfix。在启动系统时，你可以使用 Sendmail 在本地用户之间发送和接收消息。你也可以配置 Linux 系统运行 POP 服务器。POP 服务器会保留用户的邮件，直到他们登录并访问消息，而不是直接发送到他们的主机上。由于 Sendmail 是几乎所有发行版安装的默认 MTA，本章将对其进行详细讨论。

## 环回接口

在单个独立服务器内部发送的邮件需要一个环回接口。大多数环回接口允许你的系统标识自身，允许它向自己发送和接收邮件。环回接口使用主机名 `localhost` 和解析供本地系统使用的主机 IP 地址 `127.0.0.1`。你可以检查 `/etc/hosts` 文件查看你的环回接口是否已配置为本地主机。你会看到 `127.0.0.1 localhost` 列在第一项。如果由于某种原因不存在 `localhost` 条目，你可能需要使用所示的 `ifconfig` 和 `route` 命令自行创建环回接口（`lo` 是环回的术语）：

```
ifconfig lo 127.0.0.1
route add -net 127.0.0.0
```

## 接收到的邮件：MX 记录

如第 13 章所述，邮件地址由用户名和域名组成。要向某个域投递邮件，发送服务器必须找到该域的邮件服务器。这是通过查找 DNS 中的 MX（邮件交换）记录来实现的。MX 记录指定了哪台邮件服务器负责接收该域的电子邮件。一个域名可以有多个 MX 记录，通过优先级值进行排序。发送服务器将尝试投递到优先级最低的服务器。如果该服务器不可用，发送服务器将尝试下一个优先级的服务器。

如果一个域名没有 MX 记录，发送服务器将尝试投递到 A 记录指定的主机。对于只有一台邮件服务器的小域，发送服务器将尝试投递。域的 MX 记录可能如下：

```
example.com MX 10 mail1.example.com
example.com MX 20 mail2.example.com
```

在此示例中，`mail1.example.com` 是首选邮件服务器，因为它具有较低的优先级。如果 `mail1.example.com` 宕机，发送服务器将尝试 `mail2.example.com`。MX 记录也可以用于将邮件路由到不同的部门。例如，公司可能为内部邮件使用一个邮件服务器，为外部邮件使用另一个。邮件传输协议还规定了发送服务器尝试投递到给定邮件服务器的次数限制。

> **注意** MX 记录不仅用于传入邮件，也用于传出邮件。如果你有一个独立系统或只有少数主机的网络，你可能希望直接由不同的主机接收邮件。

## Postfix 和 Qmail

Postfix 是一种快速、安全且灵活的 MTA，旨在取代 Sendmail 的同时尽可能保持兼容。它由 Witesene Secure Mailer 编写最初作为 IBM Secure Mailer 发布，现在根据 GNU 许可证提供。Postfix 使用许多与 Sendmail 相同的目录和文件并利用 Sendmail 包装器，让 Sendmail 客户端与 Postfix 服务器无缝交互。Postfix 同样更容易配置，使用它自己的配置文件。包括 Red Hat 在内的多个发行版在提供 Sendmail 的同时提供了 Postfix。Postfix 不是一个程序，而是实现为一组较小的程序，每个程序都作为守护进程运行，仅在需要时运行。此外，Postfix 在创建时考虑了安全性，将所有传入邮件视为潜在的安全风险。Qmail 也是一种快速且安全的 MTA，但与 Sendmail 的兼容性很差。它有自己的配置和维护文件。像 Postfix 一样，它采用模块化设计，为每个邮件任务使用不同的程序。它也关注安全、速度和易于配置。

## Sendmail

Sendmail 作为服务器既可以接收也可以发送邮件消息。Sendmail 监听从其他主机接收的并发送给其所服务网络主机上用户的邮件消息。同时，Sendmail 还处理用户发送给远程用户的消息，并决定将这些消息发送到哪些主机。你可以在 www.sendmail.org 和 www.sendmail.net 了解更多关于 Sendmail 的信息，包括在线文档和当前的软件包包。Sendmail 新闻组为 comp.mail.sendmail。你也可以从 www.sendmail.com 获取商业版本。

你网络的域名服务器指定了运行 Sendmail 服务器的主机。这就是你的邮件主机。邮件被发送到该主机，然后由该主机的 Sendmail 服务器将消息发送给相应的用户及其主机。在你的域名服务器配置文件中，通过 MX 记录目指定邮件主机。要打印未来投递的邮件队列，你可以使用 `mailq`（或 `sendmail -q`）。这会运行带有打印邮件队列指令的 Sendmail。

Sendmail 软件包包含几个管理 Sendmail 服务器的实用程序（这些包括 `mailq`，它显示传出消息队列；`mailstats`，显示邮件服务器使用的统计数据；`hoststat`，提供连接到邮件服务器的远程主机的统计；以及 `praliases`，打印 `/etc/aliases` 文件中列出的邮件别名）。某些工具如 `mailq` 和 `hoststat` 只是带有特定选项调用 Sendmail。另一些工具如 `mailstats` 和 `praliases` 则是独立的程序。

| 工具 | 描述 |
|------|---|
| hoststat | 显示最近与邮件服务器 (Sendmail) 联系的主机状态。 |
| mailq | 显示传出消息列表 (Sendmail)。 |
| newaliases | 生成别名文件的数据库版本 (Sendmail)。 |
| purgeestat | 清除状态信息 (Sendmail)。 |
| mailstats | 显示邮件服务器统计数据。 |
| makemap | 生成表文件的数据库版本。如果不带参数，它将重新生成所有数据库文件。 |
| praliases | 打印别名文件。 |
| smrsh | 一种安全工具，限制 Sendmail 可以运行的程序到安全目录。 |

**表 23-2.** Sendmail 工具

Sendmail 现在将所有配置和数据库文件维护在 `/etc/mail` 目录下。在这里你会找到 Sendmail 宏配置文件 `sendmail.mc`，以及其他几个数据库文件（见表 23-3）。在 8.10 版本发布后，许多文件的名称已更改。例如，帮助文件现在是 `/etc/mail/helpfile` 而不是 `/etc/mail/send.ht`。专门的文件为某些功能提供支持，例如 `access`，它允许你控制不同主机和网络对你邮件服务器的访问。`virtertable` 允许你指定虚拟主机。这些文件同时具有文本版本和数据库版本。

| 文件 | 描述 |
|---|---|
| /etc/mail/sendmail.cf | Sendmail 配置文件（在 Red Hat 上，位于 `/etc/sendmail.cf`）。 |
| /etc/mail/sendmail.mc | Sendmail M4 宏配置文件。 |
| /etc/aliases | 用于邮件列表的 Sendmail 别名文件。 |
| /etc/mail/aliases.db | 使用 `newaliases` 命令通过别名文件生成的 Sendmail 别名数据库文件。 |
| /etc/mail/access | Sendmail 访问文本文件。用于筛选或转发来自不同主机、网络或用户的消息的访问控制。用于生成 `access.db` 文件。 |
| /etc/mail/access.db | Sendmail 访问数据库文件。由访问文本文件生成。 |
| /etc/mail/local-host-names | 多个主机使用同一邮件服务器的 Sendmail 本地主机文件（以前为 `sendmail.cw`）。 |
| /etc/mail/trusted-users | Sendmail Trusted用户文件（以前为 `sendmail.ct`）。 |
| /etc/mail/error-header | Sendmail 错误头文件（以前为 `sendmail.oE`）。 |
| /etc/mail/helpfile | Sendmail 帮助文件（以前为 `sendmail.ht`）。 |
| /etc/mail/statistics | Sendmail 统计文件（以前为 `sendmail.st`）。 |
| /etc/mail/virtable | Sendmail 虚拟表文本文件。映射虚拟域名地址，允许将虚拟域名托管在一个系统中。在此文件中创建条目，然后使用它生成 `virtable` 文件。 |
| /etc/mail/virtable.db | 从 `virtable` 文件生成的 Sendmail 虚拟表数据库。 |
| /etc/mail/mailertable | Sendmail 邮件器文本文件，用于覆盖你的域的路由。 |

**表 23-3.** Sendmail 文件和目录

| 文件 | 描述 |
|---|---|
| /etc/mail/mailertable.db | Sendmail 邮件器表数据库文件，由 `mailertable` 文件生成。 |
| /etc/mail/userdb | Sendmail 用户数据库文件。 |
| /etc/mail/domaintable | Sendmail 域名表文件，将域名映射到另一个域名。 |
| /etc/mail/domaintable.db | Sendmail 域名表数据库文件，由 `domaintable` 文件生成。 |
| /var/sp/mail | 入入邮件。 |
| /var/sp/mqueue | 传出邮件。 |
| /var/sp/mailog | 邮件日志文件。 |

**表 23-3.** Sendmail 文件和目录（续）

某些文件和目录用于管理接收和发送的邮件。入邮件通常保存在 `/var/sp/mail` 目录，传出邮件存在 `/var/sp/mqueue` 目录，带有不同的用户子目录。监控和错误消息记录在 `mailog` 文件中。

> **注意** Red Hat 将 Sendmail 配置文件 `sendmail.cf` 放在 `etc` 目录而不是 `/etc/mail` 目录。

> **注意** 如果你的邮件服务多个主机，你需要在 `local-host-names` 文件中输入它们。

### 别名与 LDAP

从 Sendmail 8.10 开始，Sendmail 现在可以支持使用独立的服务器来管理关于用户地址的查询。这就是 LDAP 轻量级目录访问协议。与其在不同服务器上维护别名和 `virtable` 文件，LDAP 支持允许 Sendmail 直接使用一个集中的 LDAP 服务器来查找接收者。邮件地址在 LDAP 服务器中查找，而不是搜索多个服务器上的别名和 `virtable` 文件。LDAP 还提供了用户安全身份验证，允许访问邮件账户。以下示例在 `sendmail.mc` 文件中启用 LDAP 支持：

```
FEATURE ('ldap_routing') dnl
LDAPROUTE('mytrek.com') dnl
```

或者，Sendmail 仍然支持使用别名，无论是用于发送还是接收邮件。它检查别名数据库文件 `aliases.db`，该文件存储别名名称及其关联的电子邮件地址。这通常用于管理员邮件，这些邮件可能会发送到系统的 root 用户，然后重定向到实际管理员的邮件地址。你也可以为主机设置别名，允许你仅使用别名访问网络上的主机。别名条目保存在 `/etc/aliases` 文件中。你可以编辑此文件以添加新条目或更改旧条目。它们通过 `newaliases` 命令存储在 `aliases.db` 文件中供查找，该命令运行带有更新 `aliases.db` 指令的 Sendmail。

别名允许为一个电子邮件地址或一组电子邮件地址提供不同的名称。发送给别名的将将到关联的用户或用户列表。别名条目由由冒号结尾的别名名称组成，后面跟着用户名或逗号分隔的用户列表。例如，将 `filmcritic` 别名为用户 `george@rabbit.mytrek.com`，你将使用以下条目：

```
filmcritic: george@mytrek.com
```

要为本地用户 aleina 和 larisa 设置歌手的别名，你可以使用：

```
singers: aleina, larisa
```

你也可以对目标地址使用别名，在这种情况下，它们将展开为各自的用户地址。例如，表演者 performers 将通过 filmcritic 和 singers 别名展开为用户 rabbit@mytrek.com、aleina 和 larisa。

```
performers: filmcritic, singers
```

一旦你向 `/etc/mail/aliases` 文件中添加了条目，就不需要使用 `newaliases` 命令生成数据库版本：

```
newaliases
```

## Sendmail 配置

主要的 Sendmail 配置文件位于 `/etc` 目录下的 `sendmail.cf`。该文件由一组有时很很邮件邮件定义组成，用于设置通用选项、定义 MTA（邮件传输代理）以及定义地址重写规则。一系列选项设置了功能，例如邮件消息的最大尺寸或主机文件的名称。MTA 是 Sendmail 路由消息的邮件发送程序。重写规则“重写”邮件以通过适当的 Internet 连接路由到目的地（这些规则可能非常复杂）。请查看 Sendmail HOW-TO 和在线文档以获取详细说明。

`sendmail.cf` 的定义可能复杂且令人困惑。为了简化配置过程，Sendmail 支持使用宏，你可以使用 `m4` 预处理器来生成 `sendmail.cf` 文件（这需要安装 `sendmail-cf` 包）。宏被放置在 `/etc/mail/sendmail.mc` 文件。在这里，你可以使用宏来指定你想要的定义和功能，然后使用这些宏在 `sendmail.cf` 文件中生成相应的定义和重写规则。作为 Sendmail 包的一部分，`/usr/share/sendmail-cf` 目录下提供了几个特殊版本的 `sendmail.mc` 文件。这些文件以系统名称开头，并带有 `.mf` 后缀。在许多发行版中，你的发行版已经安装了作为 `/etc/mail/sendmail.mc` 文件。

一旦你配置了 `sendmail.mc` 文件，就可以使用以下命令生成 `sendmail.cf` 文件（务必先备份原始的 `sendmail.cf` 文件）。你可以重命名 `sendmail.mc` 文件以反映特定的配置。随着你的使用和想要实现的不同配置，你可以拥有许多不同的 `.mc` 文件。

```
m4 sendmail.mc > /etc/mail/sendmail.cf
```

然后你将需要重启 Sendmail 服务器以使配置生效：

```
service sendmail restart
```

你也可以使用 Linuxconf 和 Webmin 执行基础的 Sendmail 配置。
