

# 386 附录 A m4 宏命令参考

MODIFY_MAILER_FLAGS(`local`, `+9`) 的作用相同——它们都会向本地邮件传输器（mailer）添加 9。但是

MODIFY_MAILER_FLAGS(`local`, `-w`) 执行的是 `define` 无法实现的操作。它从本地邮件传输器的定义中移除 `w` 标记。

## DOMAIN

DOMAIN 宏指向包含特定于域名配置信息的 m4 源文件。由于 DOMAIN 文件特定于你的域名，因此由你负责创建它。第 5 章提供了创建域名源文件并随后使用 DOMAIN 宏调用该文件的示例。

表 A.4 列出了在 DOMAIN 源文件中常见的 define 宏。每个参数提供的值要么是主机名（即邮件中继器的名称），要么是 mailer:hostname 对，其中 mailer 是内部邮件传输器，hostname 是邮件中继服务器。如果只使用主机名，则 mailer 默认为 relay，即 SMTP 中继匹配器的名称。

## 表 A.4 邮件中继定义

| 参数 | 定义了： |
|---|---|
| UUCP_RELAY | 用于 UUCP 地址电子邮件的服务器。 |
| BITNET_RELAY | 用于 BITNET 地址电子邮件的服务器。 |
| DECNET_RELAY | 用于 DECNET 地址电子邮件的服务器。 |
| FAX_RELAY | 用于发送到 .FAX 伪域名的邮件服务器。传真邮件传输器（mailer）会覆盖此值。 |
| LOCAL_RELAY | 用于不限定名称（unqualified names）的服务器。这已过时。 |
| USER_RELAY | 用于看似本地但实际上并非本地的名称的服务器。 |
| MAIL_HUB | 用于所有入站邮件的服务器。 |
| SMART_HOST | 用于所有导出邮件的服务器。 |

## 完整命令参考

这些参数定义的中继优先级从具体到不具体。如果同时定义了 UUCP_RELAY 和 SMART_HOST 中继，即使 SMART_HOST 中继被定义为处理“所有”导出邮件，UUCP_RELAY 也会用于导出的 UUCP 邮件。如果你同时定义了 LOCAL_RELAY 和 MAIL_HUB，则使用 FEATURE (sticky)host 来让 LOCAL_RELAY 处理所有不带主机部分的本地地址，并让 MAIL_HUB 处理所有带主机部分的本地地址。如果未指定 stickyhost 且两个中继均已定义，则忽略 LOCAL_RELAY，由 MAIL_HUB 处理所有本地地址。

除了表 A.4 中所示定义外，与伪装（masquerading）和中继（relaying）相关的宏也会出现在 DOMAIN 源文件中。这些宏包括：

- *LOCAL_USER (usernames)* 这定义了即使定义了 LOCAL_RELAY 或 MAIL_HUB 也不应中继的用户名。此命令与向 sendmail.cf 文件中的类 L 添加用户名的操作相同。
- *RELAY_DOMAIN(otherhost.domain)* 此宏识别一个应该进行邮件中继的主机。以这种方式识别的主机被添加到类 R 中。
- *RELAY_DOMAIN_FILE(filename)* 此宏识别一个包含应进行邮件中继的主机列表的文件。此宏从指定文件加载 R。
- *MASQUERADE_AS(host.domain)* 此宏将导出邮件中发送者地址的主机部分转换为指定的名称。没有主机名或在 w 类中找到主机名的发送者地址，其效果与 sendmail.cf 文件中的 M 宏相同。见第 9 章中 MASQUERADE_AS 和变量 M 的示例。
- *MASQUERADE_DOMAIN(otherhost.domain)* 如果发送者地址的主机部分匹配 MASQUERADE_AS 命令定义的值，此宏将导出邮件中发送者地址的主机部分转换为定义的域名。此命令必须配合 MASQUERADE_AS 使用。其效果与向 sendmail.cf 文件中的类 M 添加主机名相同。第9章。
- *MASQUERADE_DOMAIN_FILE(filename)* 此宏从指定文件加载 M 主名。其效果与使用 sendmail.cf 文件中的 Fm1filename 命令相同。
- *MASQUERADE_EXCEPTION(host.domain)* 此宏定义了一个不被伪装的主机，即使它属于正在伪装的域名。这允许你使用 MASQUERADE_DOMAIN 宏链接整个域名，然后豁免少数应该暴露在外部世界的主机。

EXPOSED_USER(username) 当发送者地址的用户部分与 username 匹配时，此宏禁用伪装。某些用户名（如 root）出现在许多系统中，因此在整个域名中并不唯一。对于用户名，转换地址的主机部分将无法区分消息的真实来源，并导致无法回复。此命令防止 MASQUERADE_AS 命令对特定用户的发送者地址产生影响。这与设置 sendmail.cf 文件中类 E 的值相同。

还有几个影响中继和伪装的特性。我们已经提到了 FEATURE(stickyhost)。其他与伪装相关的有：

- FEATURE(masquerade_envelope) 此功能对信封地址的伪装方式与发送者地址相同。见第 9 章。
- FEATURE(allmasquerade) 此功能使用收件者地址来控制消息。
- FEATURE(limited_relay) 此功能将伪装限制在类 M 中的主机上。
- FEATURE(masquerade_entire_domain) 此功能伪装整个域名。如果不使用此功能，则只对特定主机进行伪装。此功能用于域名。例如，MASQUERADE_AS 和 MASQUERADE_DOMAIN 被用于域名。如果不使用此功能，则只对特定主机进行伪装。此功能用于域名。例如，MASQUERADE_AS 和 MASQUERADE_DOMAIN 被用于域名。如果不使用此功能，则只对特定主机进行伪装。

## 附录 A m4 宏命令参考

![](img/b8082498451dba2bf0cf290785cc4c83_407_0.png)

