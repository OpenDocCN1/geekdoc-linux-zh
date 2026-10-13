
定义选项 `HelpFile` 为文件名 `/etc/mail/helpfile`。该文件包含 `sendmail` 在收到 `HELP` 命令时使用的帮助信息。

表 4-1 总结了 `sendmail.cf` 中使用的单字母控制操作符。每个条目还显示了该操作符的示例。此表应帮助您理解 `sendmail.cf` 中的一些行。

### 表 4-1 sendmail.cf 中使用的控制操作符

| Operator | Description |
|---|---|
| C | Defines a class; a variable (think of it as a set) that can contain several values. For example, `Cwlocalhost` adds the name `localhost` to the class `w`. |
| D | Defines a macro, a name associated with a single value. For example, `DnMAILER-DAEMON` defines the macro `n` as `MAILER-DAEMON`. |
| F | Defines a class that's been read from a file. For example, `Fw/etc/mail/local-host-names` reads the names of hosts from the file `/etc/mail/local-host-names` and adds them to the class `w`. |
| H | Defines the format of header lines that `sendmail` inserts into a message. For example, `H?P?Return-Path: <$g>` defines the `Return-Path:` field of the header. |
| K | Defines a map (a key-value pair database). For example, `Karith arith` defines the map named `arith` as the compiled-in map of the same name. |
| M | Specifies a mailer. The following lines define the `procmail` mailer: `Mprocmail, P=/usr/bin/procmail, F=DFMSPhnu9, S=EnvFromSMTP/HdrFromSMTP, R=EnvToSMTP/HdrFromSMTP, T=DNS/RFC822/X-Unix, A=procmail -Y -m $h $f $u` |

表 4-1（续）

| Operator | Description |
|---|---|
| O | Assigns a value to an option. For example, `O AliasFile=/etc/aliases` defines the `AliasFile` option to `/etc/aliases`, which is the name of the `sendmail` alias file. |
| P | Defines values for the precedence field. For example, `Pjunk=-100` sets to `-100` the precedence of messages marked with the header field `Precedence: junk`. |
| R | Defines a rule (a rule has a left-hand side and a right-hand side; if input matches the left-hand side, it's replaced with the right-hand side — this is called rewriting). For example, the rewriting rule `R$* ; $1` strips trailing semicolons. |
| S | Labels a ruleset you can start defining with subsequent `R` control lines. For example, `Scanonify=3` labels the next ruleset as `canonify` or ruleset `3`. |
| T | Adds a user name to the trusted class (class `t`). For example, `Troot` adds `root` to the class of trusted users. |
| V | Defines the major version number of the configuration file. For example, `V10/Berkeley` defines the version number as `10`. |

## 其他 sendmail 文件

`/etc/mail` 目录包含 `sendmail` 使用的其他文件。这些文件在 `sendmail` 配置文件 `/etc/mail/sendmail.cf` 中被引用。例如，以下是如何在 `/etc/mail/sendmail.cf` 文件中搜索 `/etc/mail` 字符串：

```
grep "\/etc\/mail" /etc/mail/sendmail.cf
```

在我的 Red Hat Linux 系统上，`grep` 命令搜索结果显示如下：

```
Fw/etc/mail/local-host-names

FR-o /etc/mail/relay-domains

Kmailertable hash -o /etc/mail/mailertable.db

Kvirtuser hash -o /etc/mail/virtusertable.db

Kaccess hash -T<TMPF> -o /etc/mail/access.db

#O ErrorHeader=/etc/mail/error-header

O HelpFile=/etc/mail/helpfile

O StatusFile=/etc/mail/statistics

O UserDatabaseSpec=/etc/mail/userdb.db

#O ServiceSwitchFile=/etc/mail/service.switch

#O DefaultAuthInfo=/etc/mail/default-auth-info

Ft/etc/mail/trusted-users
```

您可以忽略以井号或数字符号（`#`）开头的行，因为 `sendmail` 将这些行视为注释。其他行是 `sendmail` 控制行，引用 `/etc/mail` 目录中的其他文件。

以下是这些 `sendmail` 文件应包含的内容（请注意，并非所有这些文件都必须存在于你的 `/etc/mail` 目录中，即使存在，其中某些文件也可能为空）：

- `/etc/mail/access` — 允许发送邮件的主机名称和/或 IP 地址（用于阻止垃圾邮件——不需要的邮件）
- `/etc/mail/access.db` — 从 `/etc/mail/access` 文件生成的访问数据库
- `/etc/mail/helpfile` — SMTP 命令的帮助信息
- `/etc/mail/local-host-names` — 主机所知的名称
- `/etc/mail/mailertable` — 用于覆盖邮件路由方式的邮件传输代理表
- `/etc/mail/relay-domains` — 允许中继的主机
- `/etc/mail/trusted-users` — 允许在未警告的情况下使用其他用户名称发送邮件的用户列表
- `/etc/mail/userdb.db` — 包含每个用户登录名和真实姓名信息的用户数据库文件
- `/etc/mail/virtusertable` — 在本系统上托管的具有虚拟域地址的用户数据库

## .forward 文件

用户可以通过在其主目录中放置一个 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，其中包含以逗号分隔的邮件地址列表。发送给该用户的任何邮件随后会被转发到这些地址。如果 `.forward` 文件包含单个地址，则该用户的所有电子邮件将被重定向到该单个电子邮件地址。例如，假设包含以下行的 `.forward` 文件被放置在名为 `emily` 的用户的主目录中：

```
ashley
```
