
pop 此邮件送器支持 Post 协议。在 Linux 系统上，POP 邮件由专门的 POP 邮件守护进程提供，因此不需要或使用 MAILER(pop) 命令。

procmail 此邮件送器为 mailtable 提供了一个 procmail 接口。尽管 procmail 被用作 Linux 本地邮件，但并不需要 MAILER(procmail) 命令。请参阅第 11 章中对 procmail 的讨论。

mail111 这是一个过时的邮件送器，仅用于使用 mail111 邮件送器的 DECnet 邮件网络。

phquery 此邮件送器使用 phquery 程序提供 CSO 电话簿（ph）目录服务。用户目录服务通常配置在用户代理（UA）邮件中，而不是在 Sendai 中。

cyrus 此邮件送器提供了一个使用信箱架构的本地邮件投递程序。该架构允许使用 `user+detail` 地址语法，其中 `detail` 被解释为信箱名称。尽管具有一些高级功能，但 cyrus 和 cyussbb 并不被广泛使用。

qpage 此邮件送器通过 QuickPage 程序提供从电子邮件到寻寻机的接口。

邮件送器的所有内容并非都定义在 MAILER 宏加载的源文件中。我们已经看到，许多与邮件送器相关的命令是在 OSTYPE 源文件中指出的。此外，你还可以使用宏命令来定义自己的所有者或覆盖邮件送器参数，这些命令允许你将原始的 `sendmail.cf` 代码直接放入 m4 源文件中。

# 本地代码

有几个 m4 宏允许你使用原始的 `sendmail.cf` 配置命令直接修改 `sendmail.cf` 文件。这些宏放置在 `sendmail.cf` 代码块的开头，并告诉 m4 在输出文件中将代码放在哪里。这些宏是：

- LOCAL_RULE LOCAL_RULE_n 引导一个要添加到规则集 `n` 中的代码段，其中 `n` 是 0, 1, 2 或 3。`LOCAL_RULE` 命令后的代码是 `sendmail.cf` 的重写规则。

- LOCAL_CONFIG LOCAL_CONFIG 这一段代码将被添加到 `sendmail.cf` 文件中，位于本地信息部分之后、重写规则之前。该代码段包含标准的 `sendmail.cf` 配置命令。

- LOCAL_RULEETS 此宏引导一个包含完整规则集的代码段，该段将被添加到 `sendmail.cf` 文件中。通常，这些是命名的而不是编号的规则集。

- LOCAL_NET_CONFIG 此宏引导一段 `sendmail.cf` 重写规则，定义了如何处理发往本地网络的邮件。

- MAILER_DEFINITIONS 此宏放置在 `sendmail.cf` 邮件定义之前。

# DAEMON_OPTIONS

DAEMON_OPTIONS 宏定义了 Sendmail 守护进程在作为 MTA 和 MSA 运行时的参数。（有关 MTA 和 MSA 目的的信息，请参阅第 2 章“理解电子邮件架构”）。需要 DAEMON_OPTIONS 命令来设置 MTA 和 MSA 的参数。Sendmail 配置的默认值如下所示：

```
DAEMON_OPTIONS(`Port=25, Name=MTA`)
```

```
DAEMON_OPTIONS(`Port=587, Name=MSA, M=E`)
```

这两行将标准端口分配给 MTA 和 MSA，并为 MSA 分配了一个修饰符。在使用 `DAEMON_OPTIONS` 宏设置新的 MSA 值之前，请使用 `no_default_msa` 功能以确保 MSA 使用默认值。并使用两个 DAEMON_OPTIONS 命令：第一个用于 MTA，第二个用于 MSA。

DAEMON_OPTIONS 参数使用 `keyword=value` 对进行赋值。可能的关键字和值列在下方：

- Port `Port` 关键字为守护进程分配一个网络端口号。MTA 的标准端口是 25，MSA 的标准端口是 587。更改这些标准端口意味着客户端将难以找到该服务。因此，端口号很少更改。

- Name `Name` 标识正在设置参数的 Sendmail 守护进程的地址。有四个记录的值：

- MTA 这标识了 Sendmail 传统的邮件传输代理接口，用于投递邮件。

- MSA 标识了 Sendmail 的邮件提交代理接口，外部 MUA 可以用它来提交邮件。在实践中，此功能与 MTA 功能相同，只是端口号不同，因为 Sendmail 的这两个方面都确保所有邮件（无论如何到达）都会通过所有必要的规则、过滤器和数据库进行处理。

- MTA-v4 这与 MTA 接口相同，旨在处理向具有 32 位 IPv4 地址的主机的邮件投递。

- MTA-v6 MTA-v6 是一个旨在处理向使用 128 位 IPv6 地址的主机投递的接口。

# 目录 m4 宏命令参考

- Family `Family` 关键字定义地址族。默认是 `inet`，这意味着应该使用标准的 IPv4 地址。替代值是 `inet6`，它请求 IPv6 寻。

- M `M` 关键字是一个请求可选处理的修饰符。`M=E` 关闭 `E` 命令。此设置是 MSA 的默认值，因为 MSA 要求它。`M=a` 设置在 MSA 接受邮件之前请求通过信任的验证方法进行认证。

# LDAP 邮件路由

除了 Sendmail 内的各种数据库外，还可以轻级目录访问协议（LDAP）服务器。如果你的站点将 LDAP 用于其他用途，你可能会发现在使用 Sendmail 时使用它是有益的。通过以下定义、功能和宏为 Sendmail 增加了 LDAP 支持：

```
define(`confLDAP_DEFAULT_SPEC`, `ldap-arguments`) 此 `define` 命令设置了 LDAP 映射定义所需的参数。
```
define(`confLDAP_DEFAULT_SPEC`, `ldap-arguments`) 此 `define` 命令设置了 LDAP 映射定义所需的参数。

```
define(`confLDAP_DEFAULT_SPEC`, `ldap-arguments`) 此 `define` 命令设置了 LDAP 映射定义所需的参数。

```
FEATURE(`ldap_routing`) 此功能增加了对 LDAP 路由的支持。

LDAPROUTE_DOMAIN(domainname) 指定要从 LDAP 服务器获取路由信息的域名。

LDAPROUTE_DOMAIN_FILE(filename) 此宏指定从文件中加载路由信息的文件。

# sendmail 命令

在本书中，我们运行 `sendmail` 命令来收集邮件、验证地址、测试配置、打印队列、报告状态等。邮件送器的所有内容并非都定义在由 MAILER 宏加载的源文件中。我们已经看到，许多与邮件送器相关的命令是在 OSTYPE 源文件中指出的。此外，你还可以使用宏命令来定义自己的所有者或覆盖邮件送器参数，这些命令允许你改变邮件送器。

当 `sendmail` 命令用于发送邮件时，它从标准输入读取邮件内容。`sendmail` 命令的语法具有欺骗性的简单：

sendmail [switch] [address]

可选的地址（如果指定）是邮件投递的地址。`sendmail` 命令的复杂性并非来自地址或邮件文件；而是来自于可以随 `sendmail` 命令指定的大量开关。开关字段是改变 Sendmail 个性的关键。

# 命令行开关

附录是 `sendmail` 命令的完整参考。`sendmail` 命令接受大量的开关，均列在表 B1 中。表列出了每个开关并提供了其目的的简短描述。

### 表 B1 命令行开关

| 开关 | 目的 |
| --- | --- |
| -Btype | 设置邮件体类型为 7bit 或 8BIT |
| -ba | 使用过时的 FTP 协议发送邮件 |
| -bD |在前台作为守护进程运行 |
| -bd | 作为守护进程运行 |
| -b | 清除主机状态目录。相同的 `purstat` 命令。 |
| -bh | 显示主机状态报告。相同的 `hoststat` 命令。 |
| -bi | 构建别名数据库。相同的 `newaliases` 命令。 |
| -bm | 发送邮件。这是默认模式。 |
| -bp | 显示邮件队列。相同的 `mailq` 命令。 |
| -bs | 使 Sendmail 兼容由 inetd 或 xientd 执行。 |
| -bt | 运行地址测试模式 |
| -bv | 显示给定地址的邮件投递三元组 |
| -bz | 创建配置文件的“解析”副本 |
| -C | 指定配置文件文件名 |
| -c | 将 `HoldExpensive` 选项设置为 true |
| -dlevel | 指定调试级别 |
| -e | 设置 `ErrorMode` 选项 |
| -F | 设置发送者全名 |
