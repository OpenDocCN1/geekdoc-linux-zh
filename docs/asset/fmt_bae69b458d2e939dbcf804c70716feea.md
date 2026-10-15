
```
mysendmail.mc
dnl My sendmail.mc file
OSTYPE(`linux')
define(`PROCMail_MAILER_PATH', `/usr/bin/procmail')
FEATURE(`redirect')
MAILER(procmail)
MAILER(smtp)
```

`sendmail.mc` 文件通常包含更多条目，特别是参数和功能。检查你的 Red Hat 系统上的 `/etc/mail/sendmail.mc` 文件，以查看 Sendmail 的标准默认条目。

## Sendmail 伪装

对于从本地主机中继邮件到 Internet 的邮件服务器，你可能希望伪装邮件的来源。在拥有自己的邮件服务器并连接到 Internet 的大型网络中，Sendmail 伪装可以使本地主机发送的消息看起来是由邮件服务器发送的。它们的主机地址将被邮件服务器的地址替换。退回的邮件随后可以发送到邮件服务器并保存在 POP 或 IMAP 服务器邮箱中，以便本地主机上的用户稍后访问。此外，服务器的虚拟用户表条目可以将邮件转发到本地主机中的对应用户。

伪装通常用于用域名掩盖本地主机。任何子域也可以被伪装。这种方法可应用于 ISP 或你的网络管理员已为你的网络分配了自己的域名的情况。然后你可以将所有邮件消息伪装成来自你的域名，而不是来自特定主机或你可能拥有的任何子域。例如，如果网络的官方域名是 `mytrek.com`，那么 `mytrek.com` 网络中的所有主机，如 `rabbit.mytrek.com` 和 `turtle.mytrek.com` 的消息都可以被伪装成仅来自 `mytrek.com`。如果 `mytrek.com` 网络有一个子网络，其域名为 `mybeach.com`，来自 `mybeach.com` 的任何消息也可以被伪装成来自 `mytrek.com`。

伪装通过 `MASQUERADE_AS` 命令开启。该命令以你希望伪装邮件的名称作为参数。通常使用的名称只是域名，不包括邮件主机。在以下示例中，邮件被伪装为 `simply mytrek.com`。来自 `turtle.mytrek.com` 等本地主机的邮件将看起来是由 `mytrek.com` 发送的：

```
MASQUERADE_AS(`mytrek.com')dnl
```

你还必须指定本地网络上 Sendmail 服务器应伪装的主机和域。如果你决定伪装本地网络中的所有主机，你只需设置 `masquerade_entire_domain` 功能，如下所示：

```
FEATURE(`masquerade_entire_domain')dnl
```

如果你相反想要伪装特定主机或你的域有多个子域需要伪装，你可以在 `MASQUERADE_DOMAIN` 条目中列出它们。

你既可以列出特定的主机，也可以列出整个域名。例如，给定一个本地网络，其本地主机为 `turtle.mytrek.com` 和 `rabbit.mytrek.com`，你可以用 `MASQUERADE_DOMAIN` 将它们列出以进行伪装。它们被伪装成的域名在 `MASQUERADE_AS` 条目中指定。

```
MASQUERADE_DOMAIN('turtle.mytrek.com rabbit.mytrek.com')dnl
```

如果你想伪装本地网络中的所有主机，你只需列出本地网络的域名。如果你的本地网络还支持多个子域名，你也可以将它们列出以进行伪装。例如，要伪装 `mybeach.com` 域中的所有主机，你将使用以下条目：

```
MASQUERADE_DOMAIN('mytrek.com mybeach.com')dnl
```

如果你的域名或主机列表很长，或者你希望能够轻松更改应被伪装的主机，你可以将它们放在一个供 Sendmail 读取的文件中。使用 `MASQUERADE_DOMAIN_FILE` 命令指定文件：

```
MASQUERADE_DOMAIN_FILE('mydomains')dnl
```

如果你只是想伪装本地域中的所有主机，你可以使用 `masquerade_entire_domain` 功能：

```
FEATURE(masquerade_entire_domain)dnl
```

本地网络的常见配置会在 `MASQUERADE_AS` 条目和 `MASQUERADE_DOMAIN` 条目中指定域名。使用示例 `myisp.com` 作为域名，条目将如下所示：

```
MASQUERADE_AS('mytrek.com')dnl
FEATURE(masquerade_entire_domain)dnl
```

如果你想伪装成 ISP 的邮件域名，你将在 `MASQUERADE_AS` 条目中使用 ISP 的域名，如下所示：

```
MASQUERADE_AS('myisp.com')dnl
MASQUERADE_DOMAIN('mytrek.com')dnl
```

当从外部接收仅带有地址 `mytrek.com` 的邮件时，你的网络需要知道将其发送到哪个主机。这是被指定为 `mytrek.com` 网络邮件服务器的主机。此信息由你在 DNS 配置中的邮件交换记录提供，该记录将指定发送到 `mytrek.com` 的邮件将由邮件服务器处理——在本例中为 `turtle.mytrek.com`：

```
mytrek.com. IN MX 0 turtle.mytrek.com.
```

你还必须确保通过 `relay_based_on_MX` 功能启用了 MX 中继：

```
FEATURE(relay_based_on_MX)dnl
```

所有邮件都将看起来源自邮件服务器的主机。例如，如果你的 Sendmail 邮件服务器运行在 `turtle.mytrek.com` 上，则从名为 `rabbit.mytrek.com` 的本地主机发送的邮件看起来将是从 `turtle.mytrek.com` 发送的。

你也可以伪装收件人地址，这样发送到本地主机的用户的邮件将被发送到伪装后的地址。使用 `allmasquerade` 功能启用收件人伪装：

```
FEATURE (allmasquerade)dnl
```

## 配置邮件服务器和邮件客户端

Sendmail 可用作邮件服务器，处理网络上各个主机的邮件，或用作邮件客户端，管理特定主机上本地用户的邮件。在简单的网络配置中，你会让每个主机以客户端配置运行 Sendmail，而一台主机作为邮件服务器，转发网络主机的邮件。对于连接到 Internet 的本地网络，你的本地主机将以客户端配置运行 Sendmail，而你的网关将以服务器配置运行 Sendmail（尽管邮件服务器不一定需要在网关上运行）。邮件服务器将把来自本地网络主机的消息中继到 Internet。邮件服务器还可用于阻止来自外部主机的不受欢迎的访问，例如发送垃圾邮件的主机。基本的客户端或服务器 Sendmail 配置仅涉及 `/etc/mail/sendmail.mc` 文件中的几个功能。安装在你的系统上的默认 Red Hat 配置允许在单个主机上使用，管理该主机上用户之间的消息。要启用客户端和服务器使用，你需要对 `/etc/mail/sendmail.mc` 文件进行更改。

## 为简单网络配置配置 Sendmail

Red Hat 最初将 Sendmail 配置为仅在它运行的系统上工作，`localhost`。要使用 Sendmail 向本地网络上的其他主机发送消息，你需要在 `sendmail.mc` 和 `/etc/mail/access` 文件中更改和添加设置。简单的网络配置将让 Sendmail 在每个主机上运行，处理该主机上用户之间发送的邮件以及与其它主机用户之间的邮件。对于每个 Sendmail 服务器配置，你将对以下简单本地网络配置部分中描述的更改进行修改。

对于在网络上主机之间发送的消息，你只需在每个主机上运行 Sendmail 服务器，对其 Sendmail 配置进行少量更改。你网络中的一台主机的 Sendmail 服务器可以配置为在主机之间中继消息的任务。使用前面描述的网络示例，主机 `turtle`、`rabbit` 和 `lizard` 将运行自己的 Sendmail 服务器。`turtle` 主机上的 Sendmail 服务器将配置为在所有主机之间中继消息，包括它自己。

在网络上的每个主机上，编辑 `/etc/mail/sendmail.mc` 文件并进行以下更改。在 Red Hat 系统上，通过在前面放置 `dnl` 词来注释掉默认 `sendmail.mc` 文件中的 `DAEMON_OPTIONS` 行，如下所示。删除此功能将允许你通过本地网络接收消息。此条目将 Sendmail 限制为 `localhost (127.0.0.1)`：

```
dnl DAEMON_OPTIONS ( `Port=smtp,Addr=127.0.0.1, Name=MTA' )dnl
```

在要处理中继消息的主机上的 `sendmail.mc` 文件中，你还需要添加以下行：

```
FEATURE(relay_entire_domain)dnl
```

运行 `m4` 操作以安装更改后的配置，然后使用 `service` 操作重启服务器，如前所述。
