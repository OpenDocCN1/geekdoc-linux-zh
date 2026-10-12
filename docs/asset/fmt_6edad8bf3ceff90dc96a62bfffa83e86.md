
邮件服务器为互联网用户提供电子邮件服务。它们有自己的 TCP/IP 协议，例如简单邮件传输协议（`SMTP`）、互联网邮件访问协议（`IMAP`）。消息通过为本地域服务的邮件服务器在互联网上传输。一个域名可以看作是更大型互联网的子网，有自己的服务器来处理发送给用户或为用户接收的邮件。当用户发送消息时，消息首先从其主机系统发送到邮件服务器。邮件服务器将消息发送到互联网上的另一台邮件服务器，即为接收者所在子网提供服务的服务器。接收邮件服务器随后将消息发送到接收者的主机系统。

在每个阶段，都会使用不同的代理（程序）进行不同类型的操作。邮件用户代理（`MUA`）是一个邮件客户端程序，例如 `Elm`。通过 `MUA`，用户编写邮件消息并发送。然后由邮件传输代理（`MTA`）传输消息。`MTA` 是使用 `SMTP` 在互联网上从一个邮件服务器向另一台邮件服务器发送消息的邮件服务器，在子网之间进行传输。Linux 和 Unix 系统中常用的 `MTA` 是 `Sendmail`，它是一个邮件守护，不断检查来自其他邮件服务器的传入消息，并将传出消息发送给相应的接收者。其他日益流行的 `MTA` 有 `Postfix`、`Exim`、`Courier` 和 `Qmail`（见表 25-1）。邮件服务器接收的传入消息由邮件投递代理（`MDA`）分配给用户。大多数 Linux 系统使用 `procmail` 作为它们的 `MDA`，获取邮件服务器接收的消息并投递到用户账户（更多信息请参见 `procmail.com`）。

### 邮件传输代理

许多 Linux 发行版将自动为你安装和配置 `Sendmail` 或 `Postfix`。在启动系统时，你可以使用 `Sendmail` 或 `Postfix` 从本地用户发送和接收消息。你还可以设置你的 Linux 系统运行以替代 `POP` 服务器。`POP` 服务器在用户登录账户之前保留用户的邮件，而不是每天将邮件发送到他们的主机上。本章将讨论 `Postfix` 和 `Sendmail`。

`Courier` 是一个快速、小巧且安全的 `MTA`，它与 `Sendmail` 保持一定的兼容性。`Courier` 软件包还包括 `POP`、`IMAP` 和 Web 服务器以及邮件服务。它提供了广泛的身份验证方法，包括影子密码、`PAM` 和 `LDAP`。

| 代理 | 描述 |
|---|---|
| `Sendmail` | `Sendmail` 传输代理，由 Sendmail 联盟支持 | `sendmail.org` |
| `Postfix` | 快速、易于配置且安全的邮件传输代理，与 `Sendmail` 兼容并旨在取代它 | `postfix.org` |
| `Qmail` | 快速、灵活且安全的 `MTA`，有自己的实现并与 `Postfix` 竞争 | `qmail.org` |
| `Exim` | 基于 `mail3` 的 `MTA` | `exim.org` |
| `Courier` | `Courier` `MTA` | `courier-mta.org` |

**表 25-1 邮件传输代理**

`Exim` 是一种快速且灵活的 `MTA`，类似于 `Sendmail`。它在剑桥大学开发，其实现方式与 `Sendmail` 有很大不同之处。`Qmail` 也是一个快速且安全的 `MTA`，但它与 `Sendmail` 的兼容性很小。它有自己的配置和维护文件。像 `Postfix` 一样具有模块化设计，为每个任务使用不同的程序。它还关注安全、速度和易于配置。

> 在单个独立系统内发送的消息需要环回接口。环回接口允许你的系统访问本地。环回接口允许你发送并接收本地消息。

### 接收邮件：MX 记录

`MX` 记录不仅用于传入邮件，还用于传出邮件。`MX` 记录可以指定用于转发从访客主机传出的邮件的邮件服务器。邮件地址由用户名和域名组成。`MX` 记录显示为完全域名。为了使用域名，使用 `MX` 记录来决定实际投递的邮件服务器。例如，其 `MX` 记录显示，`mytrek.com` 实际上投递到 `turtle.mytrek.com`。这样的邮件服务器可以有多个，具有不同的优先级。

交换记录也用于没有主机的邮件。要使用域名，你通过 `MX` 记录将域名映射到邮件服务器。例如，通过 `MX` 记录，发送到 `mytrek.com` 的邮件将投递到 `turtle.mytrek.com`，由像 `Sendmail` 这样的邮件服务器路由。

```
mytrek.com. IN MX 0 turtle.mytrek.com.
```

发送到 `geo@mytrek.com` 的邮件将发送到该服务器。

> `MX` 记录不仅用于传入邮件，还用于传出邮件。`MX` 记录可以指定用于转发从访客主机传出的邮件的邮件服务器。`MX` 记录不是必须的。如果你有一个独立系统或只有几个主机的小型网络，你可能希望接收不同主机的邮件。

### Postfix

`Postfix` 是一种快速、安全且灵活的 `MTA`，旨在取代 `Sendmail` 同时保持所有兼容性。它由 Wiese Verena 开发，最初作为 IBM Mail Server 发布，现在根据 `GNU` 许可证可用（`postfix.org`）。`Postfix` 在设计时考虑了安全性，将所有传入邮件视为潜在的安全风险。`Postfix` 使用了许多 `Sendmail` 的目录和文件，并利用 `Sendmail` 包装器，让客户端与 `Postfix` 服务器无缝交互。

`Postfix` 不是一个大型程序，而是实现为一组小程序，每个程序都为执行特定的邮件任务而设计。`postfix` 主守护进程持续运行并管理其他 `Postfix` 守护进程的使用，仅在需要时运行。退回守护进程处理无法投递的邮件，简单重写守护进程重定向消息，`show` 守护进程提供队列的信息。

### Postfix 命令

几个 `Postfix` 命令允许你管理服务器任务。`sendmail` 命令发送消息。你使用 `mailq` 显示你的邮件队列状态。`newaliases` 命令读取 `aliases` 文件中的邮件别名，并将其存储在 `Postfix` 可以使用的数据库文件中。

`postfix` 命令用于维护 `Postfix` 使用的各种数据库文件，作为邮件别名的别名数据库，以及限制服务器接收消息的访问文件。你还可以将这些数据库文件实现为 SQL 数据库（如 `MySQL`），从而更容易管理。`mysql_table` 手册提供了有关如何配置 SQL 数据库支持的详细信息（`PostgreSQL` 数据库支持请查看 `pg_table`）。你也可以使用 `LDAP` 代替 SQL（`ldap_table`）。

此外，`Postfix` 还提供了更底层的工具，均以 `post` 词开头，例如维护别名数据库的 `postalias` 命令，以及显示队列文件的 `postcat`。

# 第六部分：互联网与网络服务

# Postfix 配置：main.cf

`Postfix` 的配置通过在其配置文件 `main.cf` 中设置参数来处理。安装 `Postfix` 时会带有一个默认的 `/etc/postfix/main.cf` 文件，其中大多数核心配置值已经设置好。参数通常对用户友好。例如，目录位置由以 `directory` 结尾的参数指定，例如用于 `Postfix` 队列位置的 `queue_directory` 和用于 `postfix` 守护进程位置的 `daemon_directory`。大多数参数已经实现了默认值。例如，针对特定的资源控制设置了默认值，如消息大小、时间限制和每个队列允许的消息数。你可以编辑 `main.cf` 来更改参数值以满足你的需求。进行任何更改后，你只需要使用 `postfix reload` 命令重新加载配置：

```
postfix reload
```

# 网络参数

你可能需要设置几个网络参数。为了方便这一过程，`Postfix` 定义了存储关键网络信息的参数，例如 `myhostname` 和 `mydomain`（持有你网络的域名）。例如，`myhostname` 将设置为 `turtle.mytrek.com`，而 `mydomain` 仅为 `mytrek.com`。`myhostname` 和 `mydomain` 参数本身作为分配给其他参数的值。在下一个示例中，`myhostname` 和 `mydomain` 被设置为运行邮件服务器的主机名及其网络域名：

```
myhostname=turtle.mytrek.com
mydomain=mytrek.com
```

`myorigin` 参数指定服务器发送邮件的源地址。默认情况下，它被设置为参数 `myhostname` 的值，如下所示。注意，`myhostname` 变量前有一个 `$` 以进行求值。

```
myorigin=$myhostname
```

如果你使用的是直接连接到互联网的单一系统，你可能希望保留此配置，将邮件标记为由你的主机发送。然而，如果你的系统作为网络的网关运行，你的邮件服务器从该网络上的不同主机发送邮件。你可能希望将源地址更改为域名，以便邮件被认为是从域名发送的。

```
myorigin=$mydomain
```

# 直接网络

`mydestination` 参数包含你的邮件服务器接收邮件的域名列表。默认情况下，这些使用 `localhost` 和你的系统主机名。
