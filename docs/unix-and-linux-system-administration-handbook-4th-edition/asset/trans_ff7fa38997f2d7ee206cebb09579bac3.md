

乍一看，这个命令看起来像是会导致输入文件被空的输出文件覆盖的错误。然而，makemap 会加上适当的后缀，因此实际的输出文件是 /etc/mail/access.db，实际上并没有冲突。每次文本文件被更改时，数据库文件都必须使用 makemap 重新构建（但 sendmail 无需 HUP）。

可以从生成映射的文本文件中出现注释。它们以 # 开头并持续到行尾。

在大多数情况下，会使用最长的可能匹配作为数据库键。与任何哈希数据结构一样，输入文本文件中条目的顺序并不重要。期望数据库文件作为参数的 FEATURE 默认使用 hash 作为数据库类型，并将 /etc/mail/tablename.db 作为数据库文件名。

## 通用宏和特性

表 20.10 列出了常见的配置原语、它们是否通常被使用（是、否、也许），以及它们的作用简要说明。表后各节提供了更多细节和示例。

表 20.10 Sendmail 通用配置原语

| Primitive | Used? | Description |
|---|---|---|
| OSTYPE | Yes | Includes OS-specific paths and mailer flags |
| DOMAIN | No | Includes site-specific configuration details |
| MAILER | Yes | Enables mailers, typically smtp and local |
| FEATURE | Maybe | Enables a variety of sendmail features |
| use_cw_file | Yes (servers) | Lists hosts for which you accept mail |
| redirect | Maybe (servers) | Bounces mail nicely when users move |
| always_add_domain | Yes | Fully qualifies hostnames if UA didn't |
| access_db | Maybe (servers) | Sets database of hosts to relay mail for |
| virtusertable | Maybe (servers) | Turns on domain aliasing (virtual domains) |
| ldap_routing | Maybe (servers) | Routes incoming mail using LDAP |
| MASQUERADE_AS | Yes | Makes all mail seem to come from one place |
| EXPOSED_USER | Yes | Lists users who shouldn't be masqueraded |
| MAIL_HUB | Yes (servers) | Specifies mail server for incoming mail |
| SMART_HOST | Yes (clients) | Specifies mail server for outgoing mail |

### OSTYPE macro

OSTYPE 文件打包了各种供应商特定的信息，例如邮件相关文件的预期位置、sendmail 所需命令的路径、邮件程序的标志等。参见 cf/README 以获取可在 OSTYPE 文件中定义的所有变量的列表。

那么 OSTYPE 宏本身在哪里定义呢？在 cf/m4 目录中的一个文件中，当你运行 Build 脚本时，该目录会被神奇地添加到你的配置文件前面。

除了 SUSE 之外，我们的每个示例系统都包含了来自 sendmail 发行版的相应 OSTYPE 文件。SUSE 反而有自己的 suse_linux.m4 文件。该文件很长（超过 80 行，而可比的 linux.m4 文件只有 5 行），并包含许多 FEATURE 和其他宏，这些通常会出现在站点的主配置文件（.mc 文件）中，而不是 OSTYPE 文件中。这隐藏了 sysadmin 的真实配置——也许是利弊参半，但这不是我们推荐的做法。

### DOMAIN macro

DOMAIN 指令让你能够在一个地方指定站点范围的通用信息（cf/domain/filename.m4），然后通过以下方式将其包含在每个主机的配置文件中

```
DOMAIN('filename')
```

### MAILER macro

你必须为每个想要启用的投递代理包含一个 MAILER 宏。你可以在 cf/mailers 目录中找到受支持邮件程序的完整列表，但通常你只需要 local、smtp，也许还有 cyrus。MAILER 行通常是 .mc 文件中的最后一项。

### FEATURE macro

FEATURE 宏通过包含 feature 目录中的 m4 文件来启用大量常见场景（截至目前共 56 个！）。语法为

```
FEATURE(keyword, arg, arg, ...)
```

其中 keyword 对应 cf/feature 目录中的一个文件 keyword.m4，而 args 会传递给它。一个特性最多可以有九个参数。

### use_cw_file feature

sendmail 内部类 w（因此得名 cw）包含此主机接受并投递邮件的所有本地主机的名称。此特性指定应接受发往 /etc/mail/local-host-names 中列出的主机（每行一个）的邮件。配置行

```
FEATURE(use_cw_file)
```

调用此特性。客户端机器除非有昵称，否则并不真正需要此特性，但你的传入邮件中继主机需要。local-host-names 文件应包含你接受电子邮件的任何本地主机和虚拟域，包括其备份 MX 记录指向你的站点。

如果没有此特性，sendmail 仅在邮件地址为 sendmail 运行的机器时才本地投递邮件。

如果你在站点添加了新主机，你必须将其添加到 local-host-names 文件并向 sendmail 发送 HUP 信号以使更改生效。不幸的是，sendmail 仅在启动时读取此文件。

