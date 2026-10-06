
# PINE 4.5 欢迎文本

欢迎使用 Pine ... 一个用于互联网新闻和电子邮件的程序。我们希望您探索 Pine 的许多功能。从主菜单的 `Setup/Config` 可以看到为您提供的许多选项。此外，所有屏幕都有上下文相关的帮助文本。特殊请求：此软件作为西雅图华盛顿大学的服务在全球范围内提供。

| Command | Action |
| :--- | :--- |
| G Get Help X Send |
| C Cancel | Compose |
| I MESSAGE INDEX | View messages |
| L FOLDER LIST | Select folder |
| A ADDRESS BOOK | Update address book |
| S SETUP | Configure Pine |
| Q QUIT | Leave the alpine |

alpine

与 `mail(1)` 类似，mutt 可以用于仅回复消息的发送者，也可以回复所有接收者。若要仅回复邮件发送者，按 `r`。若要向原始发送者以及所有消息接收者发送分组回复，按 `g`。

## mutt

mutt 可以使用 `mail/mutt` 端口安装 mutt。在安装了该端口后，可以通过执行以下命令启动 mutt：

```
% mutt
```

mutt 将自动读取并显示 `/var/mail` 中用户邮箱的内容。如果没有找到邮件，mutt 将等待用户的命令。下面的示例显示了 mutt 显示的消息列表：

要读取邮件，请使用光标键选择它并按回车。下面是 mutt 显示邮件的示例：

与 `mail(1)` 类似，mutt 可以用于仅回复消息的发送者，也可以回复所有接收者。若要仅回复邮件发送者，按 `r`。若要向原始发送者以及所有消息接收者发送分组回复，按 `g`。

> 注意
> 默认情况下，mutt 使用 `vi(1)` 编辑器创建和回复邮件。每个用户可以通过在其主目录中创建或编辑 `.muttrrc` 并设置编辑器变量，或者通过设置 `EDITOR` 环境变量来对其自定义。有关配置 mutt 的更多信息，请参阅 http://www.mutt.org/~。

## 第 29 章 电子邮箱

### alpine

alpine 面针对初级用户，但也包含了一些高级功能。

alpine 使用 `mail/alpine` 端口安装。一旦端口安装，可以通过执行以下命令启动 alpine：

```
% alpine
```

当 alpine 首次运行时，它会显示一个带有简要介绍的欢迎页，以及来自 alpine 开发团队的一封请求发送匿名邮件消息的请求，以便他们判断有多少用户在使用他们的客户端。要发送此匿名消息，按回车。或者，按 `E` 退出欢迎页而不发送匿名消息。欢迎页的示例见下文：

### 29.11. 使用 fetchmail

贡献者 Marc Silver。

fetchmail 是一个功能全的 IMAP 和 POP 客户端。它允许用户从远程 IMAP 和 POP 服务器自动下载邮件并保存到本地邮箱，以便方便访问。fetchmail 可以使用 `mail/fetchmail` 端口安装，并提供各种功能，包括；

- 支持 POP3、APOP、KPOP、IMAP、ETRN 和 ODMR 协议。
- 支持使用 SMTP 转发邮件，同时也允许进行正常的过滤、转发和别名设置。
- 可在守护模式下运行，以定期检查新邮件。
- 可以检索多个邮箱，并根据配置将它们转发给不同的本地用户。

本节解释了 fetchmail 的一些基本功能。该实用程序需要在用户主目录下有一个 `.fetchmailrc` 配置文件才能正确运行。该文件包含了服务器信息以及登录凭据。

由于该文件内容具有敏感性，建议使用以下命令将其设置为仅用户可读：

```
% chmod 600.fetchmailrc
```

以下 `.fetchmailrc` 是一个使用 POP 下载单个用户邮箱的示例。它告诉 fetchmail 使用用户名 `joesap` 和密码 `XXX` 连接到 `example.com`。此示例假设本地系统中存在用户 `joesap`。

```
poll example.com protocol pop3 username "joesap" password "XXX"
```

下一个示例连接到多个 POP 和 IMAP 服务器，并在适用的情况下将其重定向到不同的本地用户名：

```
poll example.com proto pop3:
user "joesap", with password "XXX", is "jsoap" here;
user "andrea", with password "XXXX";

poll example2.net proto imap:
user "john", with password "XXXXX", is "myth" here;
```

fetchmail 可以通过带有 `-d` 参数运行进入守护模式，后面跟着间隔（秒），即 fetchmail 轮询 `.fetchmailrc` 中列出的服务器的间隔。以下示例配置了 fetchmail 每 600 秒轮询一次：

```
% fetchmail -d 600
```

关于 fetchmail 的更多信息可以从 http://www.fetchmail.info/ 找到。

### 29.12. 使用 procmail

由 Marc Silver 贡献。

procmail 是一个用于过滤入邮件的强大应用程序。它允许用户定义“规则”，这些规则可以与入邮件匹配以执行特定功能，或将邮件重路由到备用邮箱或电子邮件地址。可以使用 `mail/procmail` 端口安装 procmail。安装后，它可以直接集成到大多数 MTA 中。更多信息请查阅 MTA 文档。或者，可以通过在用户主目录下的 `.forward` 文件中添加以下行来集成 procmail：

```
|exec /usr/local/bin/procmail || exit 75
```

第 29 章 电子邮箱

下节显示了一些基本的 procmail 规则以及及其功能的简要描述。规则必须插入到 `.procmailrc` 中，该文件必须存在于用户主目录下。

大部分规则可以在 `procmaillex(5)` 中找到。

将来自 `<user@example.com>` 的所有邮件转发到外部地址 `<goodmail@example2.com>`：

```
:0
+ * ^From.*user@example.com
! goodmail@example2.com
```

将小于 1000 字节的邮件转发到外部地址 `<goodmail@example2.com>`：

```
:0
+ * < 1000
! goodmail@example2.com
```

将发送到 `<alternate@example.com>` 的邮件发送到名为 `alternate` 的邮箱：

```
:0
+ * ^TOalternate@example.com
alternate
```

将所有主题为“Spam”的邮件发送到 `/dev/null`：

```
:0
^Subject.:*Spam
/dev/null
```

一个实用的配方，用于解析入的 FreeBSD.org 邮件列表并将每个列表放在自己的邮箱中：

```
:0
* ^Sender:owner-freebsd-V\[^@]+@FreeBSD.ORG
{ LISTNAME=${MATCH}}

:0
* LISTNAME??\[^@]+
FreeBSD-${MATCH}
}
```

# 第 30 章 网络服务器

### 30.1. 概述

本章涵盖了 UNIX® 系统上一些最常用的网络服务。这包括安装、配置、测试和维护许多类型的网络服务。本章贯穿了示例配置文件供参考。

在本章结束时，读者将知晓：

- 如何管理 `inetd` 守护进程。
- 如何设置网络文件系统 `NFS`。
- 如何设置网络信息服务器 `NIS` 以集中化和共享用户账户。
- 如何设置 FreeBSD 运行 LDAP 服务器或客户端。
- 如何使用 DHCP 设置自动网络设置。
- 如何设置域名服务器 `DNS`。
- 如何设置 Apache HTTP 服务器。
- 如何设置文件传输协议 `FTP` 服务器。
- 如何使用 Samba 为 Windows® 客户端设置文件和打印服务器。
- 如何使用网络时间协议 `NTP` 同步日期并设置时间服务器。
- 如何设置 iSCSI。

本章假设具备以下基础知识：

- `/etc/rc` 脚本。
- 网络术语。
- 额外的第三方软件的安装（第 4 章，安装应用程序：软件包和端口）。

## 30.2. inetd 超级服务器

`inetd(8)` 守护进程有时被称为“超级服务器”（Super-Server），因为它管理着许多服务的连接。不需要启动多个应用程序，只需要启动 `inetd` 服务。

一个示例可以是 fingererd(8) 的默认设置：

`finger stream tcp nowait/3/10 nobody /usr/libexec/fingererd -k -s`

`user`: 守护进程运行的用户名。守护进程通常以 root、daemon 或 nobody 身份运行。

`server-program`: 守护进程的完整路径。如果该守护进程是 inetd 内部提供的服务，请使用 internal。

`server-program-arguments`: 用于指定传递给守护进程调用的任何命令行参数。如果该守护进程是内部服务，请使用 internal。

### 30.2.2. 命令行选项

与大多数服务器守护进程一样，inetd 有许多选项可以用来修改其行为。默认情况下，inetd 使用 `-wW -C 60` 启动。这些选项为所有服务（包括内部服务）启用了 TCP Wrappers，并防止任何 IP 地址每分钟请求任何服务的次数超过 60 次。

要更改传递给 inetd 的默认选项，请在 `/etc/rc.conf` 中添加 `inetd_flags` 条目。如果 inetd 已经在运行，请使用 `inetd restart` 重新启动它。

可用的速率限制选项有：

- `-c maximum`: 指定每个服务并发调用的默认最大次数，默认为无限制。可以通过 `/etc/inetd.conf` 中的 `max-child` 对每个服务进行覆盖。
- `-C rate`: 指定一个服务从单个 IP 地址每每分钟可以被调用的默认最大次数。可以通过 `/etc/inetd.conf` 中的 `max-connections-per-ip-minute` 对每个服务进行覆盖。
- `-R rate`: 指定一个服务在一分钟内可以被调用的最大次数，默认为 256。速率为 0 时允许无限次。
- `-s maximum`: 指定在任何时间一个服务从单个 IP 地址可以被调用的最大次数，默认为无限制。可以通过 `/etc/inetd.conf` 中的 `max-child-per-ip` 对每个服务进行覆盖。

安全考虑量

还有其他可用选项。请参阅 `inetd(8)` 获取完整的选项列表。

### 30.2.3. 安全考虑量

由 inetd 管理的许多守护进程并不注重安全。某些守护进程（如 fingered）可能会提供对攻击者有用的信息。仅启用所需的服务，并监控过度的连接尝试。`max.connections-per-ip-minute`、`max-child` 和 `max-child-per-ip` 可用于此类限制。
