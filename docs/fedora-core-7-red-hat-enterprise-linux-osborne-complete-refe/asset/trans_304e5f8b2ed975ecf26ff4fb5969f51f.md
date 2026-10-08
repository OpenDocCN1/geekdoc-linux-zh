

影响特定功能的本地宏和配置选项定义需要在 **FEATURE** 条目之前输入。例如，**redirect** 功能使用别名文件。别名文件的任何本地定义都需要在 **redirect** 功能之前输入。

```
define('ALIAS_FILE', '/etc/aliases')
FEATURE(redirect)
```

你在向 **sendmail.mc** 文件中输入注释时需要小心。此文件是作为宏流读取的，忽略所有空白字符，包括换行符。系统不会查找特殊的注释字符。相反，你必须使用 **dnl** 或 **divert** 命令来模拟注释指示符。 **dnl** 命令指示忽略紧随该 **dnl** 命令之后直到并包含下一个换行符的所有字符。如果你在 **sendmail.mc** 文件的文本行开头放置一个 **dnl** 命令，其效果是将该行变为注释，忽略该行上的所有内容——包括其换行符。即使是空行也需要一个 **dnl** 条目来忽略换行符：

```
dnl you will have to /etc/mail/sendmail.cf by running this the m4
dnl macro config through preprocessor:
dnl
```

或者，你可以使用 **divert** 命令。 **divert** 命令将忽略所有数据，直到遇到另一个 **divert** 命令为止：

```
divert(-1)
This is the macro config file used to generate
the /etc/mail/sendmail.cf file. If you modify the file regenerate
you will have to regenerate /etc/mail/sendmail.cf by running the m4
macro
divert(0)
```

为了让 Sendmail 正常工作，只需要定义 **OSTYPE** 和 **MAILERS** 宏，以及任何所需的功能和选项。这里展示了一个非常简单的 Sendmail 文件：

```
mysendmail.mc
dnl My sendmail.mc file
OSTYPE(`linux')
define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')
FEATURE(redirect)
MAILER(procmail)
MAILER(smtp)
```

**sendmail.mc** 文件通常包含更多条目，特别是针对参数和功能。请检查你的 Red Hat 或 Fedora 系统上的 /etc/mail/sendmail.mc 文件，以查看 Sendmail 的标准默认条目。

## Sendmail 伪装（Masquerading）

对于将本地主机的消息中继到 Internet 的邮件服务器，你可能希望伪装消息的来源。在拥有连接到 Internet 的自有邮件服务器的大型网络中，Sendmail 伪装可以使本地主机发送的消息看起来像是由邮件服务器发送的。它们的主机地址将被邮件服务器的地址替换。退信可以发送到邮件服务器，并保存在稍后可由本地主机用户访问的 POP 或 IMAP 服务器邮箱中。此外，服务器虚拟用户表中的条目可以将邮件转发到本地主机上的对应用户。

伪装通常用于使用域名掩盖本地主机。也可以对任何子域名进行伪装。此方法可应用于 ISP 或你的网络管理员为你的网络分配了自有域名的情况。然后，你可以将所有邮件消息伪装为来自你的域名，而不是来自特定主机或你可能拥有的任何子域名。例如，如果一个网络的官方域名是 mytrek.com，那么来自 mytrek.com 网络中的主机（如 rabbit.mytrek.com 和 turtle.mytrek.com）的所有消息都可以伪装为仅来自 mytrek.com。如果 mytrek.com 网络拥有一个域名为 mybeach.com 的子网络，那么来自 mybeach.com 的任何消息也可以伪装为来自 mytrek.com。

使用 MASQUERADE_AS 命令开启伪装。它接受你想要伪装邮件显示的名称作为参数。通常，使用的名称仅为域名，不包括邮件主机。在以下示例中，邮件被简单伪装为 mytrek.com。从像 turtle.mytrek.com 这样的本地主机发送的邮件将看似仅由 mytrek.com 发送：

```
MASQUERADE_AS( 'mytrek.com' )dnl
```

你还必须指定你的本地网络中的主机和域名，你的 Sendmail 服务器应该对它们进行伪装。如果你决定伪装本地网络中的所有主机，你只需设置 masquerade_entire_domain 功能，如下所示：

```
FEATURE( 'masquerade_entire_domain' )dnl
```

相反，如果你想伪装特定主机，或者你的域名有多个需要伪装的子域名，你可以在 MASQUERADE_DOMAIN 条目中列出它们。你可以列出特定主机或整个域名。例如，给定一个包含本地主机 turtle.mytrek.com 和 rabbit.mytrek.com 的本地网络，你可以使用 MASQUERADE_DOMAIN 列出它们以对它们进行伪装。它们被伪装成的域名在 MASQUERADE_AS 条目中指定。

```
MASQUERADE_DOMAIN( 'turtle.mytrek.com rabbit.mytrek.com' )dnl
```

如果你想伪装本地网络中的所有主机，可以简单列出你本地网络的域名。如果你的本地网络还支持几个子域名，你也可以列出这些子域名以对它们进行伪装。例如，要伪装 mybeach.com 域中的所有主机，你可以使用以下条目：

```
MASQUERADE_DOMAIN( 'mytrek.com mybeach.com' )dnl
```

如果你有一个长的域名或主机列表，或者你想能够轻松更改应该被伪装的域名，你可以将它们放在一个文件中供 Sendmail 读取。使用 MASQUERADE_DOMAIN_FILE 命令指定该文件：

```
MASQUERADE_DOMAIN_FILE( 'mydomains' )dnl
```

如果你只想伪装本地域中的所有主机，使用 **masquerade_entire_domain** 功能：

```
FEATURE (masquerade_entire_domain)dnl
```

本地网络的常见配置会在 **MASQUERADE_AS** 条目和 **MASQUERADE_DOMAIN** 条目中指定域名。使用示例 **myisp.com** 作为域名，条目将如下所示：

```
MASQUERADE_AS ('mytrek.com')dnl
FEATURE (masquerade_entire_domain)dnl
```

如果你想伪装成 ISP 的邮件域，你会在 **MASQUERADE_AS** 条目中使用 ISP 的域名，如下所示：

```
MASQUERADE_AS ('myisp.com')dnl
MASQUERADE_DOMAIN ('mytrek.com')dnl
```

当从外部收到仅带有 **mytrek.com** 地址的邮件时，你的网络需要知道将其发送到哪个主机。这是被指定为 **mytrek.com** 网络邮件服务器的主机。此信息由你 DNS 配置中的邮件交换记录 (MX) 提供，该记录将指定发送到 **mytrek.com** 的邮件将由邮件服务器处理——在这种情况下是 **turtle.mytrek.com**：

```
mytrek.com.   IN     MX      0       turtle.mytrek.com.
```

你还必须确保使用 **relay_based_on_MX** 功能启用基于 MX 的中继：

```
FEATURE (relay_based_on_MX)dnl
```

所有消息都将看似源自邮件服务器的主机。例如，如果你的 Sendmail 邮件服务器运行在 **turtle.mytrek.com** 上，从名为 **rabbit.mytrek.com** 的本地主机发送的邮件将看似是从 **turtle.mytrek.com** 发送的。

你还可以伪装收件人地址，这样发送到本地主机用户的邮件将改发至伪装后的地址。使用 **allmasquerade** 功能启用收件人伪装：

```
FEATURE (allmasquerade)dnl
```

## 配置邮件服务器和邮件客户端

Sendmail 既可以用作邮件服务器，处理网络中各种主机的邮件；也可以用作邮件客户端，管理特定主机上本地用户的邮件。在简单的网络配置中，每个主机都以客户端配置运行 Sendmail，而一个主机作为邮件服务器运行，为网络主机中继邮件。对于连接到 Internet 的本地网络，你的本地主机将以客户端配置运行 Sendmail，而你的网关将以服务器配置运行 Sendmail（尽管邮件服务器不一定非要在网关上运行）。邮件服务器将把来自本地网络主机的消息中继到 Internet。邮件服务器也可以用于阻止

