

Debian：

```sh
# cd /usr/share/sendmail/cf/cf/
# m4 ../m4/cf.m4 debproto.m4 > /etc/sendmail.cf
```

Red Hat：

```sh
# cd /usr/lib/sendmail-cf/cf
# m4 ../m4/cf.m4 redhat.mc > /etc/sendmail.cf
```

## 电子邮件伪装（EMAIL MASQUERADING）

可以将 MTA 配置为对其他域名进行伪装。这可以通过修改 m4 配置文件添加所需功能，并按如下方式重新生成 /etc/mail/sendmail.cf 文件来轻松实现：

```sh
# cd /usr/share/sendmail/cf/cf
# cp generic-col1.2.mc tempfile.mc
```

在文件末尾添加以下两行：

```text
MASQUERADE_AS(domain-name.com)dnl
FEATURE(masquerade_envelope)dnl
```

然后按如下方式重新生成文件：

```sh
# m4 ../m4/cf.m4 tempfile.mc > /etc/mail/sendmail.cf
```

当然，你需要将 domain-name.com 替换为你想要伪装的域名，并使用上面相应的文件和路径。

伪装选项会更改电子邮件头中的名称。sendmail 不仅仅用于传输邮件；它更多的作用是重写邮件头。通常，sendmail 会将当前的完全限定域名作为发件人地址的一部分写入，但由于大多数人是通过域名而非特定主机发送邮件，因此伪装功能允许更改该名称。

你还可以看到伪装信封（masquerade envelope）。信封是消息最顶端的一部分，通常不可见，它会从一个 MTA 传递到另一个 MTA。伪装信封可将伪装扩展到消息的外层包装部分。

你可能还想了解 sendmail 的其他一些功能，如表 25.3 所示。

| 功能 | 作用 |
|---|---|
| `accept_unresolvable_domains` | 防止因无法解析的域而退回邮件。 |
| `access_db` | 用于垃圾邮件控制的功能之一。 |
| `bestmx_is_local` | 如果 DNS 表明我们是邮件主机，则接受邮件。 |
| `blacklist_recipients` | 另一个垃圾邮件控制功能（需要 access_db）。 |
| `dnsbl` | 以前称为 rbl，查询 sendmail 维护的黑名单。 |
| `domaintable` | 用于提供域名映射。 |
| `genericstable` | 用于更改外发邮件上的发件人地址。此功能消耗资源较多，除非必要，否则不应启用。 |
| `ldap_routing` | 实现基于 LDAP 的邮件收件人路由。 |
| `local_procmail` | 使用 procmail 作为本地邮件程序。 |
| `mailertable` | 用于覆盖特定域的路由。 |
| `masquerade_entire_domain` | 与 masquerade_as 和 masquerade_domain 一起使用，将所有域隐藏在伪装地址之后。 |
| `masquerade_envelope` | 对 MTA 之间传递的“接收自”行进行伪装。 |
| `nouucp` | 不添加处理 UUCP 地址（bang 路径）的规则。 |
| `nullclient` | 一种特殊情况，参数为邮件集线器。指定 nullclient 的 .m4 文件除了 nocanonify 之外不应有其他功能。 |
| `redirect` | 拒绝发送到 address.REDIRECT 的邮件，并返回“请尝试 `<address>`”的消息。 |
| `relay_based_on_MX` | 允许中继，但仅限具有有效 MX 记录的主机。 |
| `relay_entire_domain` | 允许你所在域（由 Dn 定义）中的所有主机进行中继。 |
| `relay_hosts_only` | 将 access_db 的默认行为从中继列表中列出的整个域，改为仅中继 access_db 中列出中继的特定主机。 |
| `relay_mail_from` | 如果邮件发件人在 access_db 中被列为 RELAY，则允许中继。注意：发件人地址可能被伪造。 |
| `smrsh` | 使用 sendmail 受限 shell。 |
| `use_ct_file` | 查询 sendmail.ct 以获取受信任用户列表。 |
| `use_cw_file` | 查询 sendmail.cw 以获取本地主机名列表。 |
| `virtusertable` | 用于将传入邮件上的收件人地址映射到本地用户名。 |

对于表 25.3 中的许多功能，你可以指定文件名和映射类型。文件名和映射类型的指定是为了覆盖默认值。

其他规范（如 PrivacyOptions）也可以更改。你可以直接在 sendmail.cf 中更改 PrivacyOptions，或者如果你希望构建多个保持一致性的 sendmail.cf 文件（并且不想忘记更改它），默认值位于 /usr/share/sendmail/cf/m4/proto.m4 文件中。不过，修改此文件时要小心。表 25.4 列出了隐私选项。

**表 25-4. sendmail 的隐私选项**

| 隐私选项 | 作用 |
|---|---|
| `public` | 允许开放访问。 |
| `needmailhelo` | 在处理 MAIL 命令之前强制要求 HELO 或 EHLO 命令。 |
| `needexpnhelo` | 在处理 EXPN 命令之前强制要求 HELO 或 EHLO。 |
| `noexpn` | 禁止 EXPN。 |
| `needvrfyhelo` | 在处理 VRFY 命令之前强制要求 HELO 或 EHLO。 |
| `novrfy` | 禁止 VRFY。 |
| `noetrn` | 禁止 ETRN。 |
| `noverb` | 禁止 VERB。 |
| `restrictmailq` | 限制 mailq 命令。 |
| `restrictqrun` | 限制 -q 命令行标志。 |
| `noreceipts` | 不返回成功 DSN（投递状态通知）。 |
| `nobodyreturn` | 不随 DSN 返回消息正文。 |
| `authwarnings` | 在消息中加入 X 认证警告头。 |
| `goaway` | 禁止大多数 SMTP 查询。goaway 会设置上述所有标志，但 noreceipts、restrictmailq、restrictqrun、noetrn 和 nobodyreturn 除外。 |

你可以用逗号分隔多个选项，将它们放在同一行：

```
O PrivacyOptions=goaway,noreceipts,restrictmailq,restrictqrun,noetrn
```

这些限制旨在防止远程用户与 sendmail 守护进程进行交互。VERBOSE、EXPN（展开）以及有时使用的 VRFY（验证）命令本来用于调试目的，但现在常被垃圾邮件发送者用来获取或验证受害者列表。ETRN 允许外部人员运行 mailq。

前面的讨论只是简要涉及了所有可能性。如果你需要进行大量的 sendmail 管理工作，你将需要一份好的 sendmail 参考资料，就像 sendmail 源代码附带的那样。

## sendmail.cf 文件

必须修改 sendmail.cf 文件，使其包含你的主机可被识别的所有名称。例如，如果你的完全限定域名主机名是 `main.calderasystems.com`，你需要在 `/etc/mail/sendmail.cf` 文件中添加以下内容：

```
# sendmail.cf - 在此包含你机器的所有别名。
calderasystems.com
```

这使得传入邮件能够被 sendmail 正确处理。否则，sendmail 不知道如何处理发送到 me@calderasystems.com 的电子邮件。发送到 me@main.calderasystems.com 的电子邮件默认情况下可以被 sendmail 正常处理。

### `/etc/rc.d/init.d/mta` 文件

此文件包含启动 sendmail 或任何其他 MTA 的启动脚本。要手动启动或停止 sendmail，请执行以下操作：

```
# /etc/rc.d/init.d/mta start
# /etc/rc.d/init.d/mta stop
```

要让 sendmail 在系统启动时自动启动，请修改 `/etc/sysconfig/daemons/mta` 文件中的 ONBOOT 行，如下所示：

```
# /etc/sysconfig/daemons/mta
IDENT=MTA
DESCRIPTIVE="Mail Transfer Agent"
ONBOOT="yes"
VARIANT="sendmail"
```

### `/etc/mta/options/sendmail` 文件

`/etc/mta/options/sendmail` 文件定义了用作邮件传输代理的实际二进制文件以及初始启动时使用的选项。默认设置如下：

```
# /etc/mta/sendmail/options
ONBOOT=yes
DAEMON=/usr/sbin/sendmail
OPTIONS="-bd -q5m"
```

`-bd` 选项告诉 sendmail 以后台守护进程方式运行，`-q5m` 告诉 sendmail 每 5 分钟刷新一次邮件队列（`/var/spool/mqueue`）。还有大量其他选项可用，但这是最常用的。

> **注意**
> 
> 必须启用邮件传输代理才能通过 OpenLinux 接收传入邮件。这可以通过修改 `/etc/sysconfig/daemons/mta` 文件来完成。

## 别名（ALIASES）

别名可以有多种用途。别名最常见的用途之一是处理某个人的不同拼写或全名。别名还可以用来设置不一定要指向特定个人的通用名称。例如，可以设置一个 Webmaster 的别名，将所有传入邮件指向 Glenn。别名文件类似如下：

```
# 此文件列出了 Caldera OpenLinux 的默认邮件别名。
#
# 此文件中的别名不会在“发件人”头中展开
# Mail，但在网络上或通过 /bin/mail 可见。
#
#
#                         重要提示：
#
# 对此文件进行任何更改后，你必须运行
#
```

