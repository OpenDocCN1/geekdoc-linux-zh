

某些宏和宏类型需要在 sendmail.mc 文件中按照如下所示的特定顺序放置。请注意 MAILER 位于末尾，而 OSTYPE 位于开头。本地宏定义（define）和 FEATURE 条目跟在 OSTYPE 和 DOMAIN 条目之后。

```
VERSIONID
OSTYPE
DOMAIN
define
FEATURE
local macro definitions
MAILER
LOCAL_RULE_*
LOCAL_RULESETS
```

影响特定功能的本地宏和配置选项定义需要在 FEATURE 条目之前输入。例如，redirect 功能使用 aliases 文件。aliases 文件的任何本地定义需要在 redirect 功能之前输入。

```
define(`ALIAS_FILE', `/etc/aliases')
FEATURE(redirect)
```

你需要小心在 sendmail.mc 文件中输入注释的方式。该文件被读取为宏流，忽略所有空白字符，包括换行符。不会查找特殊的注释字符。相反，你必须使用 dnl 或 divert 命令来模拟注释指示。dnl 命令指示从该 dnl 命令之后的所有字符直到下一个换行符（包括换行符）都被忽略。如果你将 dnl 命令放在 sendmail.mc 文件中的文本行开头，它的效果就是将该行变成注释，忽略该行上的所有内容——包括其换行符。即使是空行也需要 dnl 条目来忽略换行符：

```
dnl you will have to /etc/mail/sendmail.cf by running this the m4
dnl macro config through preprocessor:
dnl
```

另外，你也可以使用 divert 命令。divert 命令将忽略所有数据，直到遇到另一个 divert 命令为止：

```
divert(-1)
This is the macro config file used to generate
the /etc/mail/sendmail.cf file. If you modify the file regenerate
you will have to regenerate /etc/mail/sendmail.cf by running the m4
macro
divert(0)
```

Sendmail 要工作，至少需要定义 OSTYPE 和 MAILERS 宏，以及任何需要的功能和选项。下面展示了一个非常简单的 Sendmail 文件。

```
mysendmail.mc
dnl My sendmail.mc file
OSTYPE(`linux')
define(`PROCMail_MAILER_PATH', `/usr/bin/procmail')
FEATURE(`redirect')
MAILER(procmail)
MAILER(smtp)
```

sendmail.mc 文件通常包含更多条目，特别是参数和功能。检查你的 Red Hat 系统上的 /etc/mail/sendmail.mc 文件，以查看 Sendmail 的标准默认条目。

## Sendmail 伪装

对于从本地主机中继邮件到 Internet 的邮件服务器，你可能希望伪装邮件的来源。在拥有自己的邮件服务器并连接到 Internet 的大型网络中，Sendmail 伪装可以使本地主机发送的消息看起来是由邮件服务器发送的。它们的主机地址将被邮件服务器的地址替换。退回的邮件随后可以发送到邮件服务器并保存在 POP 或 IMAP 服务器邮箱中，以便本地主机上的用户稍后访问。此外，服务器的虚拟用户表条目可以将邮件转发到本地主机中的对应用户。

伪装通常用于用域名掩盖本地主机。任何子域也可以被伪装。这种方法可应用于 ISP 或你的网络管理员已为你的网络分配了自己的域名的情况。然后你可以将所有邮件消息伪装成来自你的域名，而不是来自特定主机或你可能拥有的任何子域。例如，如果网络的官方域名是 mytrek.com，那么 mytrek.com 网络中的所有主机，如 rabbit.mytrek.com 和 turtle.mytrek.com 的消息都可以被伪装成仅来自 mytrek.com。如果 mytrek.com 网络有一个子网络，其域名为 mybeach.com，来自 mybeach.com 的任何消息也可以被伪装成来自 mytrek.com。

伪装通过 MASQUERADE_AS 命令开启。该命令以你希望伪装邮件的名称作为参数。通常使用的名称只是域名，不包括邮件主机。在以下示例中，邮件被伪装为 simply mytrek.com。来自 turtle.mytrek.com 等本地主机的邮件将看起来是由 mytrek.com 发送的：

```
MASQUERADE_AS(`mytrek.com')dnl
```

你还必须指定本地网络上 Sendmail 服务器应伪装的主机和域。如果你决定伪装本地网络中的所有主机，你只需设置 masquerade_entire_domain 功能，如下所示：

```
FEATURE(`masquerade_entire_domain')dnl
```

如果你相反想要伪装特定主机或你的域有多个子域需要伪装，你可以在 MASQUERADE_DOMAIN 条目中列出它们。

