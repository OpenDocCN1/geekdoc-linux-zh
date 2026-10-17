
`undefine(`UUCP_RELAY')`

```
要指定 Sendmail 服务器运行的操作系统类型，你可以使用 `OSTYPE` Sendmail 宏。以下示例指定了 Linux 操作系统：
```

```
OSTYPE(`linux')
```

`MAILER` 宏指定要使用的邮件传递代理（MDA）。你可能拥有多个 MDA。通常，你需要 procmail 等邮件传递代理来将邮件传递到网络上的主机。此外，Sendmail 实际上作为 MDA 运行，接收来自本地网络主机的消息，然后将其发送到更大的网络。

```
MAILER(procmail)

MAILER(smtp)
```

Sendmail 还支持大量需要显式开启的功能。你可以使用 Sendmail `FEATURE` 宏来实现这一点。请参见表 25-3 了解常用 Sendmail 功能的列表。以下示例开启了 `redirect` 功能，该功能用于通知发件人收件人已位于不同的地址：

```
FEATURE(redirect)
```

此外，你可以设置某些配置选项。这些是以 `conf` 为前缀的变量，你可以使用 `define` 命令为它们赋值。有大量配置选项，其中大多数你不需要更改。以下示例定义了 `confAUTO_REBUILD` 配置选项，如果需要，它将自动重建别名数据库：

```
define(`confAUTO_REBUILD')
```

某些宏和宏类型需要按照此处所示的特定顺序放置在 `sendmail.mc` 文件中。请注意，`MAILER` 位于末尾附近，而 `OSTYPE` 位于开头。本地宏定义 `define` 和 `FEATURE` 条目跟随在 `OSTYPE` 和 `DOMAIN` 条目之后：

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

### 表 25-3 Sendmail 功能

| 功能 | 描述 |
| --- | --- |
| use_cw_file | 检查由邮件服务器 `/etc/mail/local-host-names` 文件提供服务的 hosts。 |
| use_ct_file | 从 `/etc/trusted-users` 文件读取用户列表。这些是可信用户，可以更改其消息的发件人名称。 |
| redirect | 拒绝所有发送至 "address.REDIRECT" 的邮件，前提是 `/etc/aliases` 文件中已放置转发地址。 |
| mailer table | 使用 mailer 表文件 `/etc/mail/mailertable` 覆盖特定域的路由。 |
| domain table | 使用 domain 表文件 `/etc/mail/domain table` 将一个域映射到另一个域。如果你更改域名，这将非常有用。 |
| allmasquerade | 导致收件人地址也伪装为来自伪装主机。 |
| masquerade_entire_domain | 伪装 `MASQUERADE_AS` 中指定的域内的所有主机。 |
| masquerade_envelope | 伪装信封发件人和收件人以及头信息。 |
| virtual table | 对于虚拟主机，将虚拟地址映射到真实地址。 |
| nullclient | 将 Sendmail 服务器转换为 null 客户端，它只是将邮件消息转发到中央邮件服务器进行处理。 |
| local_procmail | 使用 procmail 作为本地邮件器。 |
| smrsh | 使用 Sendmail 受限 Shell `smrsh` 进行邮件处理。 |
| promiscuous_relay | 允许你中继邮件，允许接收来自你的域外部的邮件并将其发送到你的域外部的 hosts。 |
| relay_entire_domain | 允许你域内的任何主机中继邮件（默认情况下，将此限制在 access 数据库中的 hosts）。 |
| relay_hosts_only | 检查特定 hosts 的中继权限，而不是 domains。 |
| accept_unqualified_senders | 允许发件人电子邮件地址是单个用户名，而不仅仅是包含域名完全限定名称。 |
| accept_unresolvable_domains | 允许 Sendmail 接受无法解析的域名名称。对于被防火墙阻止访问完整 DNS 命名空间的本地网络中的用户很有用。默认情况下，Sendmail 要求地址中的 domains 可通过 DNS 解析。 |
| access_db | 接受或拒绝来自 access 数据库中 domains 和 hosts 的邮件。 |
| blacklist_recipients | 阻止发往特定用户的邮件，例如那些永远不应接收邮件的用户——如用户 `nobody` 和 `host`。 |
| dnsbl | 拒绝实时黑洞列表中的 hosts。由 MAPS `Mail Abuse Prevention System LLC` 管理，旨在限制不需要的批量电子邮件 `mail-abuse.org` 的传输。 |
| ldap_routing | 启用 LDAP 使用。 |

影响特定功能的本地宏和配置选项定义需要在 `FEATURE` 条目之前输入。例如，`redirect` 功能使用别名文件。别名文件的任何本地定义都需要在 `redirect` 功能之前输入。

```
define(`ALIAS_FILE', '/etc/aliases')

FEATURE(redirect)
```

你在向 `sendmail.mc` 文件中输入注释时需要小心。此文件是作为宏流读取的，忽略所有空白字符，包括换行符。系统不会查找特殊的注释字符。相反，你必须使用 `dnl` 或 `divert` 命令来模拟注释指示符。 `dnl` 命令指示忽略紧随该 `dnl` 命令之后直到并包含下一个换行符的所有字符。如果你在 `sendmail.mc` 文件的文本行开头放置一个 `dnl` 命令，其效果是将该行变为注释，忽略该行上的所有内容——包括其换行符。即使是空行也需要一个 `dnl` 条目来忽略换行符：

```
dnl you will have to /etc/mail/sendmail.cf by running this the m4

dnl macro config through preprocessor:

dnl
```

或者，你可以使用 `divert` 命令。 `divert` 命令将忽略所有数据，直到遇到另一个 `divert` 命令为止：

```
divert(-1)

This is the macro config file used to generate

the /etc/mail/sendmail.cf file. If you modify the file regenerate

you will have to regenerate /etc/mail/sendmail.cf by running the m4

macro

divert(0)
```

为了让 Sendmail 正常工作，只需要定义 `OSTYPE` 和 `MAILERS` 宏，以及任何所需的功能和选项。这里展示了一个非常简单的 Sendmail 文件：

```
mysendmail.mc

dnl My sendmail.mc file

OSTYPE(`linux')

define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')

FEATURE(redirect)

MAILER(procmail)

MAILER(smtp)
```
