
主要的 Sendmail 配置文件是 `sendmail.cf`，位于 `/etc` 目录。该文件由一组相当冗长的定义列表组成，用于设置通用选项、设计 `MTA`（邮件传输代理）并定义地址重写规则。一系列选项设置了某些功能，例如邮件消息的最大限制或主机的名称。`MTA` 是 `Sendmail` 路由消息的邮件投递程序。重写规则“重写”邮件地址，以便通过适当的 `Internet` 连接将消息路由到目的地，这些规则（注：这些规则可能非常复杂）。

![](img/6ac214f13c9ea7c0ad85ba43163f14a1_522_0.png)

可以检查 `Sendmail HOWTO` 和在线文档。

此，可以使用 `/etc/mail.submit.cf` 文件中的宏来配置 `submit.cf`。

为了简化 `sendmail.cf`，使用宏来配置 `/etc/mail.submit.cf`。

`MTA` 是 `Sendmail` 路由消息的邮件投递程序。你可以使用一个 `procmail` 软件包来配置功能。此，使用 `sendmail.cf` 宏来配置 `/etc/mail/mail`。

若要配置 `PROCMAIL_PATH` 变量，使用：

```
define('PROCMAIL_PATH','/usr/bin/procmail')
```

同样，如果你有某些路径，可以使用 `undefined` 命令删除它们：

```
undefined('UUUC_RELAY')
```

要指定 `Sendmail` 运行的操作系统类型，使用 `OSTYPE` 宏。以下示例指定了 `Linux`：

```
OSTYPE('linux')
```

`MAILER` 宏指定了使用的投递代理（`MDAs`）。你可能有多个。通常，你需要 `procmail` 来投递网络中的邮件。

```
MAILER (procmail)
MAILER (smtp)
```

## 第 25 章：邮件服务器

`Sendmail` 还支持许多需要明确开启的功能。你可以通过 `Sendmail` 宏来实现此。见表 25-3 的常用 `Sendmail` 功能列表。以下示例开启了 `redirect` 功能，用于通知发送者接收者现在位于另一个地址：

```
FEATURE (redirect)
```

**表 25-3 Sendmail 功能**

| 功能 | 描述 |
| --- | --- |
| `use_cw_file` | 检查由邮件服务器提供的主机 `/etc/mail/local-host-names`。 |
| `use_ct_file` | 从 `/etc/trusted-users` 读取用户列表。这些是可以更改邮件发送名的信任用户。 |
| `redirect` | 拒绝所有指向 `REDIRECT` 的邮件，前提是转发地址已放在 `/etc/aliases` 文件中。 |
| `mailertable` | 使用邮件表文件 `/etc/mail/mailer` 覆盖特定域的路由。 |
| `domaintable` | 使用域名表文件 `/etc/mail/domaintable` 将一个域名映射到另一个域名。当你更改域名时非常有用。 |
| `allmasquerade` | 使接收者地址也伪装成伪装主机。 |
| `masquerade_entire_domain` | 对 `MASQUERADE_AS` 指定域名内的所有主机进行伪装。 |
| `masquerade_envelope` | 同标头一起对信封发送者和接收者进行伪装。 |
| `virtertable` | 用于虚拟主机；将虚拟地址映射到真实地址。 |
| `nullclient` | 将 `Sendmail` 服务器变为空客户端，它仅将邮件消息转发到中央邮件服务器进行处理。 |
| `local_procmail` | 使用 `procmail` 作为本地邮件投递程序。 |
| `smrh` | 使用拒绝限制 shell (`smrh`) 用于邮件。 |
| `promiscuous_relay` | 允许中继，允许从域名外部接收邮件并发送到域名外部的主机。 |
| `relay_entire_domain` | 允许你域名内的任何主机中继（默认限制为访问数据库中的这些主机）。 |
| `relay_hosts_only` | 针对特定主机检查中继权限而不是域名 |

## 第六部分：互联网与网络服务

**表 25-3 Sendmail 特性（续）**

| 特性 | 描述 |
|---|---|
| `accept_unqualified_senders` | 允许发送者电子邮件地址为单个用户名，而不仅仅是包含域名的完全限定名。 |
| `accept_unresolvable_domains` | 允许 `Sendmail` 接收无法解析的域名。这对于那些被防火墙隔在 `DNS` 命名空间之外的本地网络用户有用。默认情况下，`Sendmail` 要求地址中的域名必须可以通过 `DNS` 解析。 |
| `access_db` | 接受或拒绝来自访问数据库中域名和主机的邮件。 |
| `blacklist_recipients` | 阻塞发送给某些用户的邮件，例如那些从不接收邮件的用户——如 `nobody` 和 `host` 用户。 |
| `dnsbl` | 拒绝实时黑洞列表（Realtime Blackhole List）中的主机。由 `MAPS`（邮件滥用防止系统 LLC）管理，旨在限制不需要的垃圾邮件（mail-abuse.org）的传输。 |
| `ldap_routing` | 启用 `LDAP` 使用。 |

此外，你还可以设置某些配置选项。这些是以 `conf` 为前头的变量，你可以使用 `define` 命令进行设置和赋值。配置选项非常多，其中大多数你不需要更改。以下示例定义了 `CONFAUTO_REBUILD` 配置选项，如果需要，它将重新构建别名数据库：

```
define('CONFAUTO_REBUILD')
```

某些宏和类型的宏需要按照特定的顺序放在 `sendmail.mc` 文件中，如下所示。注意 `MAILER` 位于结尾，而 `OSTYPE` 位于开头。本地宏定义（define）和 `FEATURE` 条目位于 `OSTYPE` 和 `DOMAIN` 条目之后：

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

影响特定特性的本地宏和配置选项定义需要在进入 `FEATURE` 条目之前输入。例如，重定向（`redirect`）功能使用别名文件。任何别名文件的本地定义都需要在重定向功能之前输入。

## 第 25 章：邮件服务器

```
define('ALIAS_FILE','/etc/aliases')
FEATURE(redirect)
```
