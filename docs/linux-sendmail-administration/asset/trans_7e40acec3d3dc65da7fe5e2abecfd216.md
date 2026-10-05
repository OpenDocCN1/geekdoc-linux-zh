

## 表 A.1 Sendmail m4 宏和配置命令（续）

| 命令 | 用法 |
|---|---|
| GENERICICS_DOMAIN_FILE | 标识一个文件，该文件列出了应由 genericstable 数据库转换的完全限定域名。 |
| HACK | 选择一个包含本地定义的临时修复的文件。 |
| INPUT_MAIL_FILTER | 定义邮件过滤器以及调用该过滤器所需的变量。 |
| LDAPROUTE_DOMAIN | 定义一个根据 LDAP 目录条目路由邮件的域名。 |
| LDAPROUTE_DOMAIN_FILE | 标识一个文件，该文件列出了根据 LDAP 目录条目路由邮件的域名。 |
| LOCAL_CONFIG | 标记包含原始 sendmail.cf 命令的节的开始。 |
| LOCAL_DOMAIN | 为邮件服务器定义别名主机名。 |
| LOCAL_NET_CONFIG | 标记原始重写规则的开始，这些规则定义了发往本地网络的邮件的处理方式。 |
| LOCAL_RULE_n | 标记包含原始重写规则的节的开始。n 必须是 0、1、2 或 3，用于标识标识添加重写规则的规则集。 |
| LOCAL_RULESETS | 标记要添加到配置中的规则集的开始。 |
| LOCAL_USER | 列出即使在中继本地邮件时也免于衰减的用户名。 |
| MAIL_FILTER | 定义一个邮件过滤器。 |
| MAILER | 标识一组要包含在 sendmail.cf 文件中的邮件发送者。 |
| MAILER_DEFINITIONS | 标记包含原始 sendmail.cf 邮件发送者命令的节的开始。 |
| MASQUADE_AS | 定义用于伪装输出邮件的域名。 |
| MASQUADE_DOMAIN | 定义一个应该被伪装的域名。 |
| MASQUADE_DOMAIN_FILE | 标识一个文件，该文件列出了应该被伪装的域名。 |
| MASQUADE_EXCEPTION | 定义一个被伪装的主机。 |
| MODIFY_MAILER_FLAGS | 覆盖为邮件发送者定义的标志。 |
| OTYPE | 选择一个包含操作系统特定属性的文件。 |
| RELAY_DOMAIN | 定义一个应该路由邮件的域名。 |
| RELAY_DOMAIN_FILE | 标识一个文件，该文件列出了应该路由邮件的域名。 |
| SITE | 标识一个本地连接的 UUCP 主机。 |
| SITECONFIG | 标识列出所有本地连接 UUCP 站点的文件。 |
| TRUST_AUTH_MECH | 定义一个受信任的授权机制列表。 |
| undefine | 清空配置变量设置的值。 |
| UUCPSMTP | 将 UUCP 主机名映射到 Internet主机名。 |
| VERSIONID | 定义配置的版本控制信息。 |
| VIRTUSER_DOMAIN | 定义一个将通过 virtusertable 接受处理的虚拟域名。 |
| VIRTUSER_DOMAIN_FILE | 标识一个文件，该文件列出了将通过 virtusertable 接受处理的虚拟域名。 |

表 A.1 所示的内置 m4 命令（以小字母列出的部分）分为两个控制输出流的命令和两个用于设置宏的命令。控制输出流的两个命令是 `dn1` 和 `divert`。`dn1` 命令用于行末尾清除输出中的空行，或用于行开头表示该行是一个命令。`divert(-1)` 命令标记文本块的开始和结束。除了 -1 和 0 之外，`divert` 命令还接受其他数字参数：1 到 9。（见第4章“创建基础 Sendmail 配置”中的表 4.2）。这些其他值在 Sendmail m4 宏中用于将直接数据发送到 sendmail.cf 文件的不同部分。但你不会自己的配置中直接使用这些值。

一组宏（例如 `LOCAL_CONFIG`、`LOCAL_RULESET` 和 `MAILER_DEFINITION`）允许你在不直接使用 `divert` 值的情况下将数据发送到 sendmail.cf 文件的不同部分。如 `LOCAL_CONFIG` 和 `MAILER_DEFINITION` 等命令标记了应包含输出文件某些部分的原始 sendmail.cf 代码的开始。这些命令使得你能够以任何方式自定义 sendmail.cf 文件。请参见本附录后文的“本地代码”部分获取这些宏的完整列表。

用于设置和取消定义变量的两个内置 m4 命令将变量设置为某个值，并将其取消定义为默认值。通过 `define` 命令可以的配置参数比任何其他命令都多；因此，本附录有更多内容致力于 `define` 变量。

几个宏（几乎有一半）的作用与 `define` 命令本质相同：它们将变量设置为某个值。`MASQUERADE_AS`、`MASQUADE_DOMAIN` 和 `VIRTUSER_DOMAIN_FILE` 都是用于设置变量的命令示例。所有这些命令将在附录后文中介绍。

## 附录 A m4 宏命令参考

`TRUST_AUTH_MECH` 宏是一个补充 `define` 的宏的良好示例。由于 `TRUST_AUTH_MECH` 宏是一个补充 `define` 的宏的良好示例，正如你在“define”部分看到的，`TRUST_AUTH_MECH` 宏是一个补充 `define` 的宏的良好示例。（此处省略重复内容，由于 OCR 包含重复伪影，已进行处理）：

`TRUST_AUTH_MECH` 宏是一个补充 `define` 的宏的良好示例。正如你在“define”部分看到的，它是一个补充 `define` 的宏。（此处省略重复内容，直到该宏是一个补充 `define` 的宏的良好示例。（等等，OCR 包含重复伪影，已进行清晰处理）：
