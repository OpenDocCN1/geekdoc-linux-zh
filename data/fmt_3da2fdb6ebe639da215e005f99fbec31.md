
Sendmail 还支持许多你需要开启的功能。你可以通过 Sendmail `FEATURE` 宏来实现，请参表 25-3 的常用列表

## 第 25 章：邮件服务器：SMTP、POP 和 IMAP 535

| 特性 | 说明 |
| --- | --- |
| use_cw_file | 检查由邮件服务器 `/etc/mail/local-host` 名称提供的主机。 |
| use_ct_file | 从 `/etc/trusted-users` 文件中读取用户列表。这些是信任用户，可以更改其邮件的发件人名称。 |
| redirect | 拒绝所有发往 "address.REDIRECT" 的邮件，前提是在 `/etc/aliases` 句中放置了转发地址。 |
| mailertable | 使用邮件文件 `/etc/mail/mailertable` 来覆盖特定域的路由。 |
| domaintable | 使用域名文件 `/etc/mail/domaintable` 将一个域映射到另一个域。在更改域名时非常有用。 |
| allmasquerade | 使地址被伪装成来自伪装主机。 |
| masquerade_entire_domain | 伪装 `MASQUERADE_AS` 中指定域内的所有主机。 |
| masquerade_envelope | 伪装信封发件人、接收者以及报头。 |
| virtuous | 对于虚拟主机，将虚拟地址映射到真实地址。 |
| nullclient | 将 Sendmail 服务器转换为空客户端，它仅将邮件消息转发到中央邮件服务器进行处理。 |
| local_procmail | 使用 procmail 作为本地主进程。 |
| smrsh | 使用 Sendmail 限制 shell (smsh) 进行邮件传输。 |
| promiscuous_relay | 允许中继邮件，允许从域之外接收邮件并发送到域之外的主机。 |
| relay_entire_domain | 允许你域内的任何主机中继邮件（默认限制为缓存数据库中的主机）。 |
| relay_hosts_only | 检查特定主机而非域的中继权限。 |
| accept_unqualified_senders | 允许发件人电子邮件地址为单个用户名，而不仅仅包含域名的完全限定名。 |

表 25-3 Sendmail 特性（续）

## 536 第五部分：网络服务器

| 特性 | 说明 |
| --- | --- |
| accept_unresolvable_domains | 允许 Sendmail 接受无法解析的域名。对于那些被防火墙阻隔访问完整 DNS 命名空间的本地网络用户有用。默认情况下，Sendmail 要求地址中的域名必须通过 DNS 解析。 |
| access_db | 接受或拒绝来自访问数据库中域和主机的邮件。 |
| blacklist_recipients | 阻止发往某些用户的邮件，例如那些不应接收邮件的用户——如 `nobody` 和 `host`。 |
| dnsbl | 拒绝实时黑名单中的主机。由 MAPS（邮件滥用预防系统 LLC）管理，旨在限制不受欢迎邮件传输 (mail-abuse.org)。 |
| ldap_routing | 启用 LDAP 使用。 |

## 表 25-3 Sendmail 特性

使用了 Sendmail 特性。以下示例开启了 `redirect`（重定向）特性，该特性用于通知接收者现在位于不同的地址：

```
FEATURE(redirect)
```

此外，你可以设置某些配置选项。这些是以 `conf` 前缀开头的变量，你可以使用 `define` 命令对它们进行设置并赋值。配置选项非常多，其中大多数你都不需要更改。以下示例定义了 `confAUTO_REBUILD` 配置选项，如果满足以下条件，它将自动重建数据库：

```
define('confAUTO_REBUILD')
```

某些宏和类型的宏需要按照所示特定顺序放置在 `sendmail.mc` 文件中。注意 `MAILER` 位于结尾，`OSTYPE` 位于开头。本地宏定义 (`define`) 和 `FEATURE` 条目位于 `OSTYPE` 和 `DOMAIN` 条目之后：

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

## 第 25 章：邮件服务器：SMTP、POP 和 IMAP 57

影响特定特性的本地宏和配置选项定义需要在 `FEATURE` 条目之前输入。例如，`redirect` 特性需要别名文件（aliases file）。任何对别名文件的本地定义都需要输入在 `redirect` 特性之前。

```
define('ALIAS_FILE','/etc/aliases')
FEATURE (redirect)
```

你必须小心如何向 `sendmail.mc` 文件中输入注释。该文件作为宏流被读取，忽略所有空白字符（包括换行符在内）。它不会查找特殊字符。相反，你使用 `dnl` 或 `divert` 命令来模拟注释指示符。`dnl` 命令指示忽略该 `dnl` 命令到下一个换行符之前的所有字符。如果你在 `sendmail.mc` 文件的文本行开头放置 `dnl` 命令，它的效果是将该行变为注释，忽略该行上的所有内容——包括其本身。空行需要一个 `dnl` 条目来忽略换行符：

```
dnl you will have to /etc/sendmail.cf by running this the m4

dnl macro config through preprocessor:
```

或者，你可以使用 `divert` 命令。`divert` 命令将忽略直到另一个 `divert` 命令到达的所有数据：

```
divert (-1)

This is the macro config file used to generate

the /etc/sendmail.cf file. If you modify the file regenerate

ou will have to regenerate /etc/sendmail.cf by running the m4

macro

divert (0)
```

## 575 第五部分：网络服务器

通过 `MASQUERADE_AS` 命令开启伪装（Masquerading）。它接受的参数是你想要伪装的名称。通常，该名称是你的域名。在以下示例中，邮件被伪装为 `mytrek.com`。来自本地主机 `turtle.mytrek.com` 的邮件看起来是由 `mytrek.com` 发送的。

```
MASQUERADE_AS('mytrek.com')
```

你还需要指定本地网络中应当伪装的主机和域。如果你需要伪装整个本地网络，只需设置 `masquerade_entire_domain` 特性，如

## 伪装

如果你想伪装特定的主机或你的域有多个子域，请在 `MASQUERADE_DOMAIN` 条目中列出它们。你可以列出特定的主机或整个域。例如，对于拥有主机 `turtle.mytrek.com` 和 `rabbit.mytrek.com` 的本地网络，你可以列出 `MASQUERADE_DOMAIN` 以进行伪装。它们伪装的域在 `MASQUERADE_AS` 条目中指定：

```
MASQUERADE_DOMAIN('turtle.mytrek.com rabbit.mytrek.com')
```

如果你想伪装本地网络中的所有主机，只需列出你的本地网络域名即可。如果你的本地网络还支持多个子域，你也可以列出这些并进行伪装。例如，要伪装 `mybeach.com` 域的所有主机，你可以使用以下条目：

```
MASQUERADE_DOMAIN('mytrek.com mybeach.com')
```

如果你有一个长长的域名或主机列表，或者你想要轻松更改被伪装的对象，可以将它们放置在一个文件中供 Sendmail 读取。使用 `MASQUERADE_DOMAIN_FILE` 命令指定该文件：

```
MASQUERADE_DOMAIN_FILE('mydomains')
```

# 第 25 章：邮件服务器：SMTP、POP 和 IMAP

如果你只想对本地域网内的所有主机进行伪装，你可以使用 `masquerade_entire_domain` 功能：

```
FEATURE(masquerade_entire_domain) dnl
```

本地网络的常用配置是在 `MASQUERADE_AS` 条目和 `MASQUERADE_DOMAIN` 条目中指定域名名。使用 `mysp.com` 作为域名示例，看起来如下：

```
MASQUERADE_AS('mytrek.com') dnl

FEATURE(masquerade_entire_domain) dnl
```
