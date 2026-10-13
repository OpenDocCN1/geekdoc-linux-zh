
`MASQUERADE_DOMAIN('mytrek.com mybeach.com')`

如果你有一个很长的域名或主机列表，或者你想能够方便地更改需要伪装的内容，可以将它们放在一个供 Sendmail 读取的文件中。使用 `MASQUERADE_DOMAIN_FILE` 命令指定文件：

```
MASQUERADE_DOMAIN_FILE('mydomains')
```

如果你想伪装本地域名中的所有主机，你使用 `masquerade_entire_domain` 特性：

```
FEATURE('masquerade_entire_domain')
```

本地网络的常用配置是在 `MASQUERADE_AS` 条目和 `MASQUERADE_DOMAIN` 条目中指定域名。以 `myisp.com` 作为域名示例，条目看起来如下：

```
MASQUERADE_AS ('mytrek.com')
FEATURE('masquerade_entire_domain')
```

## 第 25 章：邮件服务器：SMTP、POP 和 IMAP

当从外部接收带有 `mytrek.com` 地址的邮件时，你的网络需要知道将邮件发送到何处。这就是被指定为 `mytrek.com` 网络邮件服务器的主机。此信息由 DNS 配置中的邮件交换记录 `MX` 提供的，该记录指定了发送到 `mytrek.com` 的邮件将由邮件服务器处理——在此例中为 `turtle.mytrek.com`。

```
mytrek.com. IN MX 0 turtle.mytrek.com.
```

你还必须确保通过 `relay_based_on_MX` 特性启用了 MX 中继：

```
FEATURE (relay_based_on_MX)
```

所有邮件看起来都源自邮件服务器的主机。例如，如果你的 Sendmail 服务器运行在 `turtle.mytrek.com` 上，那么从名为 `rabbit.com` 的本地主机发送的邮件看起来将是从 `turtle.mytrek.com` 发送的。

你也可以伪装收件人地址，使得发送给本地主机上用户的邮件将通过而非伪装地址发送。使用 `allmasquerade` 来启用收件人伪装：

```
FEATURE (allmasquerade)
```

## 配置邮件服务器和邮件客户端

Sendmail 既可以用作邮件服务器（处理网络上的各种主机），也可以用作邮件客户端（管理特定主机上本地用户的邮件）。在简单的网络配置中，你可以让每个主机都以客户端配置运行 Sendmail，并让一个主机作为邮件服务器运行，为网络主机中继邮件。对于连接到互联网的本地网络，你的本地主机将以客户端配置运行 Sendmail，而你的网关将以服务器配置运行 Sendmail（尽管邮件服务器并不一定需要运行在网关上）。邮件服务器将来自本地网络的消息向中继到互联网。该服务器还可用于阻止来自外部主机的非愿访问，例如发送垃圾邮件的主机。基本的客户端或服务器 Sendmail 配置涉及 `/etc/mail/sendmail.mc` 文件中的几个特性。你系统上安装的默认 Fedora 配置允许使用单个主机通过该主机管理用户。要启用客户端和服务器使用，你将对 `/etc/mail/sendmail.mc` 文件进行更改。

## 为简单网络配置配置 Sendmail

Fedora 初始将 Sendmail 配置为仅在它运行的系统（本地主机）上工作。要使用 Sendmail 发送到本地网络上的其他主机，你需要更改 `sendmail.mc` 和 `/etc/mail/access` 文件中的设置。简单的配置将让 Sendmail 运行在每个主机上，处理该主机用户之间以及与其他主机之间进邮件的邮件。对于每个 Sendmail 配置，你将按照下节关于简单本地网络配置的描述进行更改。

对于你网络中主机之间的消息，你只需要在每个主机上运行 Sendmail 服务器，并对其 Sendmail 配置进行一些更改。Sendmail

![](img/70a)

在每个主机上，`turtle` 将被配置为处理消息。使用之前描述的示例，`turtle` 和 `rabbit` 将运行 Sendmail。在你希望处理消息中继的主机上，你需要添加以下内容：

```
FEATURE(relay_entire_domain)
```

在 Fedora 系统上，通过以下方式注释 `sendmail.mc` 中的 `DAEMON_OPTIONS` 行：

```
dnl DAEMON_OPTIONS('Port-smtp,Addr=127.0.0.1')
```

运行 `m4` 操作以安装更改后的配置并重启服务。现在你可以跨网络从用户向另一个用户发送邮件。例如，`george@mytrek.com` 现在可以向 `rabbit@mytrek.com` 发送邮件。本地 Sendmail 服务器将负责内部的收发。

## 为集中邮件服务器配置 Sendmail

或者，你可以设置一个集中邮件服务器来处理你网络上的所有邮件。各种主机上的邮件客户端可以将其消息发送到集中邮件服务器，由该服务器将其中继到更大的网络或互联网。邮件然后在集中服务器上接收，客户端随后可以从中获取。设置集中邮件服务器有多种方法。最简单是在你的网关上运行集中邮件服务器，然后在本地主机上运行 Sendmail 客户端版本。任何来自本地主机的邮件将自动转发到集中邮件服务器。收到的邮件只能递送到集中服务器，到达运行在集中服务器主机上的 POP 或 IMAP 服务器。

对于集中式配置，将用户视为拥有网络地址而不是独立主机是合理的。因此， `rabbit.mytrek.com` 将使用邮件地址 `rabbit@mytrek.com`，而不是 `rabbit@rabbit.mytrek.com`。用户将与各自主机上的用户相同，但在网关主机上将设置相应的用户以便 POP 或 IMAP 服务器处理收到的邮件。

有效的邮件服务器将涉及某些组件：

- 运行在网关主机上的集中邮件服务器
- 每个客户端作为空客户端运行 Sendmail
- 伪装所有邮件以仅使用域名地址，而不使用主机地址
- 运行在网关主机上的 POP 或 IMAP 服务器用于处理收到的邮件

## 第 25 章：邮件服务器：SMTP、POP 和 IMAP 53

## 配置直接连接 ISP 的工作站

如果您运行一个不属于某个网络但通过 ISP（互联网服务提供商）直接连接互联网的 Linux 系统，您可以简单地使用 ISP 邮件服务器来发送和接收邮件。通常情况下，您有一个用于发送邮件的 SMTP 邮件服务器和一个用于接收邮件的 POP 服务器。然而，您也可以配置 Sendmail 与您的 ISP 接口。

通常，您的 ISP 会提供一个处理其主机邮件的邮件服务器。要使用 ISP 邮件服务器，您可以通过 SMART HOST 来定义它。邮件将通过 ISP 邮件服务器发送。SMART HOST 的格式为 `type:hostname`，其中 `type` 是使用的邮件服务器类型，使用 SMTP。默认值是 `relay`。定义 `SMART_HOST` 选项以使用您的 ISP 发收邮件：

```
define ('SMART_HOST', 'smtp:mail.my-isp.com')
```

`SMART_HOST` 选项用于指定您希望处理网络消息中继的特定远程邮件服务器。它可以是 ISP 邮件服务器，也可以较大网络中的任何邮件服务器。

对于通过调制解调器的拨号连接，您可以使用各种配置选项（如 `conMESSAGE_TIMEOUT`）来控制连接。邮件可以在输出队列中保留多久，直到您准备好拨号并发送它。将 `conIVERY_MODE` 选项设置为 `queueonly` 可以让只在准备就绪时发送邮件。

## 邮件表 (Mail Table)

邮件表允许您将指向指定主机或域的消息路由到特定的邮件服务器。您可以使用邮件表将发往虚拟域的邮件路由到您网络的邮件服务器。要引用整个域名，请在域名名前加一个点。邮件路由到的主机前带有有所使用的邮件协议类型，Sendmail 使用 `smtp`。以下条目将发往 `.mybeach.com` 的邮件路由到 `turtle.mytrek.com` 邮件服务器。

```
.mybeach.com smtp:turtle.mytrek.com
```

条目存放在 `/etc/mail/mailtable` 文件中。一旦您创建了这些条目，就使用 `make` 命令生成 `mailtable.db` 数据库文件：

```
make mailtable
```
