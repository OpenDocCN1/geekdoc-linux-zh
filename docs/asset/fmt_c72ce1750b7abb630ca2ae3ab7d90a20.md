
使用此命令可以发现哪些参数已从默认值发生更改，并显示当前设置：

```
matthew@seymour:-$ postconf -d
```

```
matthew@seymour:-$ postconf -n
```

设置参数需要 root 权限。例如，设置 `myhostname` 参数，请使用以下命令：

```
matthew@seymour:-$ sudo postconf -e "myhostname=mail.matthewhelmke.com"
```

`myhostname=mail.matthewhelmke.com`

此方法适用于 Postfix `main.cf` 文件列出的参数：

```
matthew@seymour:-$ sudo postconf -e "smtp_sasl_auth_enable = yes"
```

`myhostname=othername.matthewhelmke.com`

如你所见，`postconf` 非常方便。你可以从帮助页（man page）了解更多关于 `postconf` 的信息。

使用以下命令启动、停止和重启 Postfix，根据所示，使用三个动作词之一的 `start`、`stop` 或 `restart`：

```
matthew@seymour:-$ sudo /etc/init.d/postfix start
```

复杂的邮件服务器设置超本书的范围；更多信息请参阅 Kyle Dent 写的《Postfix: The Definitive Guide》。这是一本很好的参考书，仅用 250 页就作为一个完整且实用的参考书是不常的；如果你想了解关于 Postfix 的特定知识，这本书值得一读。

后续章节介绍了一些常用选项。有关 Postfix 以及其他 MTA 的更多信息，请参见本章末尾的“参考资料”部分。

## 配置伪装（Masquerading）

有时，你可能需要让 Postfix 伪装成系统实际主机名以外的主机。如果你通过拨号连接 Internet 且 ISP 为你处理所有邮件，就会出现这种情况。在这种情况下，你希望 Postfix 伪装成你 ISP 的域名。例如，以下配置将任何来自 `matthew.gracehopper.net` 的消息仅精简为 `gracehopper.net`：

```
masquerade_domains = gracehopper.net
```

## 使用智能主机（Smart Hosts）

如果你没有持续的 Internet 连接，你可能需要让 Postfix 将消息发送到你 ISP 的邮件服务器并由它为你交付。

## 基础 Postfix 配置与操作

在没有持续 Internet 连接的情况下，你可能会发现很难将消息交付到某些位置（例如世界上一些欠发达地区，那里的邮件服务不稳定且随机）。在这些情况下，你可以配置 Postfix 作为智能主机，将邮件传递给另一个发送者而不是尝试直接交付。你可以在 `main.cf` 中使用如下行来启用智能主机：

```
relayhost = mail.isp.net
```

此行会导致 Postfix 将任何邮件传递给服务器 `mail.isp.net` 而不是尝试直接交付。如果 ISP 阻止了任何邮件转发，智能主机将无法工作。某些 ISP 阻止中继是因为它经常用于传播垃圾邮件。

## 设置邮件交付间隔

如本初提到的，Postfix 通常在收到邮件后立即尝试交付，并在之后按固定间隔再次尝试交付。如果你只有周期性的 Internet 连接（如拨号连接），你可能更希望 Sendmail 将所有消息留在队列中，并在每次连接到 ISP 时尝试交付。

由于拨号连接已成为例外而非常态且现在非常稀少，Ubuntu 默认不配置它们，且默认安装中不包含 `ppd` 守护进程。如果你需要，请从 Ubuntu 软件仓库安装 `ppd`。你可以通过向 `/etc/ppp/peers/ppp0` 添加以下行来配置 Postfix 留存稍后交付：

```
/usr/sbin/sendmail -q
```

此行会导致 Postfix 在连接到 ISP 时自动发送所有邮件。

然而，无论连接在线还是线下，Postfix 都会尝试发送邮件，你的电脑可能会为了发送邮件而拨号。要禁用此功能，你需要在 `mail.cf` 中输入该行：

```
defer_transports = smtp
```

这会阻止任何意外的拨号！

> 提示：如果你正在使用调制解调器网络，有一个名为 `ppp0` 的 ppd 配置文件，位于 `/etc/ppp/peers`。该文件中的任何命令会在 PPD 守护进程启动时自动运行。你可以向此文件添加 `sendmail -q` 行，以便在每次拨号连接 Internet 时都自动处理邮件队列。

## 邮件中继（Mail Relaying）

默认情况下，Postfix 不中继并非来自本地域的邮件。这意味着如果运行在 `gracehopper.net` 的 Postfix 接收到发往 `seymoucray.net` 的邮件，且该邮件并非来自 `gracehopper.net`，则邮件将被拒绝且不中继。如果你想允许选定的域名通过你进行中继，如下所示在 `main.cf` 文件中为域名添加条目：

```
mynetworks = 192.168.2.0/24, 10.0.0.2/24, 127.0.0.0/8
```

IP 地址需要以无类域间路由（CIDR）格式指定。需要方便的计算器，请访问 www.subnet-calculator/cidr.php。你必须重启 Postfix 使此更改生效。

> 注意：记得我们提到过某些邮件客户端可以包含 MTA 功能吗？你可以配置 Microsoft Outlook 和 Outlook Express 使用 SMTP，并且如果你使用拨号连接，它们提供连接并发送邮件。

## 使用别名转发邮件

别名允许一个用户拥有多个地址。如果你希望发送到不同地址的邮件都进入同一个收件箱，这非常有用。要设置别名，你必须编辑 `/etc/aliases` 文件。这是一个示例：

```
root:
```

此条目将所有邮件转发给 root。另一种方法是在你的目录下创建一个名为 `.forward` 的文件。例如：

```
@example.com
```

> 注意：`.forward` 文件位于用户目录下。

在安装 Fetchmail 后，你必须在目录中创建 `.fetchmailrc`，它提供了 Fetchmail 程序的配置。当你修改 `/etc/aliases` 时，必须重建别名数据库。使用以下命令执行此操作：

```
matthew@seymour:-$ newaliases
```

## 使用 Fetchmail 获取邮件

SMTP 设计用于具有全 Internet 连接的系统。如果你使用的是拨号连接呢？在这种情况下，你无法使用 SMTP 接收邮件，而需要使用 POP3 等协议。

遗憾的是，MUA 不知道 POP3 或 IMAP。为了解决这个问题，你可以使用 Fetchmail 程序从服务器获取邮件，然后从那里下载邮件并将这些消息注入本地 MTA，就像它们来自标准的 SMTP 服务器一样。后续章节将介绍如何安装、配置和使用 Fetchmail 程序。

## 安装 Fetchmail

与其他软件包一样，你可以使用 synaptic 或 apt 安装 fetchmail。你可以在 www.catkb.org/-esr/fetchmail 获取最新版本的 Fetchmail。

## 配置 Fetchmail

在安装 Fetchmail 后，你必须在目录中创建 `.fetchmailrc`，它提供了 Fetchmail 的配置。你可以使用任何文本编辑器创建并随后编辑 `.fetchmailrc` 文件。配置文件直观且易于创建；后续章节将介绍主要。后续章节介绍的信息没有讨论 `.fetchmailrc` 文件中的所有可用选项，涵盖了使基础 Fetchmail 安装运行所需的常用选项。你必须使用文本编辑器创建该文件以包含示例所示的条目——当然要根据你的个人信息进行修改。对于高级配置，请查看 Fetchmail 的帮助页。

> 注意文件分为三个部分：全局选项、邮件服务器选项和用户选项。这些部分按照列出的顺序出现非常重要。不要将选项添加到错误的部分。将选项放在错误的位置是新用户在使用 Fetchmail 配置文件时常见的问题之一。

## 配置全局选项

`.fetchmailrc` 的第一部分包含全局选项。这些选项影响你在配置文件中列出的所有邮件服务器和账户。正如你在本节后面将学到的，你可以用本地配置选项覆盖一些全局选项。以下是 `.fetchmailrc` 文件中全局部分可能出现的选项示例：

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log
```

示例中的第一行告诉 Fetchmail 它应该以守护模式启动，并每隔 600 秒（即 10 分钟）检查一次邮件服务器是否有新邮件。守护模式意味着 Fetchmail 启动后会将它自己移动到后台并继续运行。如果没有此行，Fetchmail 只会在启动时检查一次，然后终止，不再检查。

第二个选项告诉 Fetchmail 使用本地账户 `foobar` 作为最后的备用地址。换句话说，任何收到的无法投递到指定账户的邮件都将发送到 `foobar`。

第三行告诉 Fetchmail 将活动记录到 `./fetchmail.log` 文件中。或者，你可以使用 `set syslog` 行——在这种情况下 Fetchmail 将通过 syslog 设施记录日志。

## 配置邮件服务器选项

`.fetchmailrc` 的第二部分包含了每个应该检查新邮件的邮件服务器的信息。以下是邮件部分可能内容的示例：

```
poll mail.samplanet.org
proto pop3
no dns
```

第一行告诉 Fetchmail 应该按照全局选项中设置的轮询间隔（在本示例中为 600 秒）检查邮件服务器 `mail.samplanet.org`。或者，第一行也可以 `skip` 开头。如果邮件服务器以 `skip` 开头，则不会按轮询间隔轮询，只有在 Fetchmail 命令行指定时才进行轮询。

第二行指定了连接邮件服务器时使用的协议。此示例使用了 POP3。其他合法选项是 IMAP、身份验证邮局协议 `APOP` 和 Kerberos 邮局协议 `KPOP`。你可以在这里使用 `AUTH`，在这种情况下 Fetchmail 将自动确定与邮件服务器使用的正确协议。

第三行告诉 Fetchmail 不要尝试进行域名系统 `DNS` 查找。如果你运行的是拨号连接，可能需要包含此选项。

## 配置用户账户

`.fetchmailrc` 的第三部分也是最后部分，包含了在前节指定的服务器上的用户账户信息。这是一个示例：

```
user foobar
pass secretword
fetchall
no flush
```

第一行当然只是指定了用于登录邮件服务器的用户名，第二行指定了该用户的密码。许多关注安全的人对在配置文件中放置明文密码的想法感到不知所措，如果该文件对组组或所有用户可读，他们确实应该如此担心。对这些信息的唯一保护方法是确保文件仅对所有者可读——即权限设置为 `600`。

第三行告诉 Fetchmail 它应该从服务器获取所有消息，即使它们已经被读取过。

第四行告诉 Fetchmail 在完成下载后从服务器上删除这些消息。这是默认设置，因此你实际上不需要指定此选项。如果你想在下载后从服务器上删除消息，请使用 `flush` 选项。

你刚刚插入的配置使得整个 `.fetchmail` 文件看起来如下：

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log
```

```
poll mail.samenet.org
proto pop3
no dns
```

```
user foobar
pass secretword
fetchall
flush
```

此文件告诉 Fetchmail 执行以下操作：

- 每 600 秒检查 POP3 服务器 `mail.samenet.org` 是否有新邮件。
- 使用用户名 `foobar` 和密码 `secretword` 登录。
- 从服务器下载所有消息。
- 下载后从服务器上删除消息。
- 将收到的任何无法投递到本地用户的邮件发送到账户 `foobar`。

正如之前提到的，`.fetchmail` 文件中包含的选项比这里列出的多。然而，本节提供的选项将让你通过基础配置运行起来。

为了增加灵活性，你可以定义多个 `.fetchmail` 文件，使用相同的 Linux 用户账户从远程服务器检索邮件。例如，你可以为你最常用的账户定义设置并将其保存在默认的 `.fetchmail` 文件中。然后可以这样快速检索邮件：

```
$ matthew@you:~ fetchmail -a
1 message for matthew at mail.matthewhelke.com (1108 octets)
reading message 1 of 1 (1108 octets) flushed
```

通过使用 `fetchmail -f`，你可以指定备备资源文件，并轻松地从另一个服务器检索邮件，如下：

```
$ matthew@you:~ fetchmail -f .mymailrc
2 messages for matthew at mail.matthewhelke.com (5407 octets).
reading message 1 of 2 (3440 octets) flushed
reading message 2 of 2 (1967 octets) flushed
```
