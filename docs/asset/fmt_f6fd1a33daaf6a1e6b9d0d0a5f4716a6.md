
- `RELAY_DOMAIN(otherhost.domain)` 此宏识别一个应该进行邮件中继的主机。以这种方式识别的主机被添加到类 `R` 中。

- `RELAY_DOMAIN_FILE(filename)` 此宏识别一个包含应进行邮件中继的主机列表的文件。此宏从指定文件加载 `R`。

- `MASQUERADE_AS(host.domain)` 此宏将导出邮件中发送者地址的主机部分转换为指定的名称。没有主机名或在 `w` 类中找到主机名的发送者地址，其效果与 `sendmail.cf` 文件中的 `M` 宏相同。见第 9 章中 `MASQUERADE_AS` 和变量 `M` 的示例。

- `MASQUERADE_DOMAIN(otherhost.domain)` 如果发送者地址的主机部分匹配 `MASQUERADE_AS` 命令定义的值，此宏将导出邮件中发送者地址的主机部分转换为定义的域名。此命令必须配合 `MASQUERADE_AS` 使用。其效果与向 `sendmail.cf` 文件中的类 `M` 添加主机名相同。第9章。

- `MASQUERADE_DOMAIN_FILE(filename)` 此宏从指定文件加载 `M` 主名。其效果与使用 `sendmail.cf` 文件中的 `Fm1filename` 命令相同。

- `MASQUERADE_EXCEPTION(host.domain)` 此宏定义了一个不被伪装的主机，即使它属于正在伪装的域名。这允许你使用 `MASQUERADE_DOMAIN` 宏链接整个域名，然后豁免少数应该暴露在外部世界的主机。

`EXPOSED_USER(username)` 当发送者地址的用户部分与 `username` 匹配时，此宏禁用伪装。某些用户名（如 `root`）出现在许多系统中，因此在整个域名中并不唯一。对于用户名，转换地址的主机部分将无法区分消息的真实来源，并导致无法回复。此命令防止 `MASQUERADE_AS` 命令对特定用户的发送者地址产生影响。这与设置 `sendmail.cf` 文件中类 `E` 的值相同。

还有几个影响中继和伪装的特性。我们已经提到了 `FEATURE(stickyhost)`。其他与伪装相关的有：

- `FEATURE(masquerade_envelope)` 此功能对信封地址的伪装方式与发送者地址相同。见第 9 章。

- `FEATURE(allmasquerade)` 此功能使用收件者地址来控制消息。

- `FEATURE(limited_relay)` 此功能将伪装限制在类 `M` 中的主机上。

- `FEATURE(masquerade_entire_domain)` 此功能伪装整个域名。如果不使用此功能，则只对特定主机进行伪装。此功能用于域名。例如，`MASQUERADE_AS` 和 `MASQUERADE_DOMAIN` 被用于域名。如果不使用此功能，则只对特定主机进行伪装。

## 附录 A m4 宏命令参考

![](img/b8082498451dba2bf0cf290785cc4c83_407_0.png)

# 附录 A m4 宏引用

`FEATURE(always_add_domain)` 此功能将系统主机名添加到所有本地邮件中。当在台名为 `ibis.foobirds.org` 的服务器上启用此功能时，从本地用户 `craig` 发给本地用户 `kathy` 的邮件将作为 `craig@ibis.foobirds.org` 投递到 `kathy@ibis.foobirds.org`。

`FEATURE(bestmx_is_local)` 启用此功能后，发送至将 `Sendmail` 服务器列其 `MX` 服务器的任何主机的邮件都将被 `Sendmail` 服务器作为本地邮件接收。

`Dns` 宏如下：

- `CANONIFY_DOMAIN(domain)` 此宏定义了一个域名，如果使用了规范化（`canonify`）功能，则该域名将传递给 `DNS` 以获取其规范形式（`canonical form`）。计算机可以通过别名来识别。存储在 `DNS` 中的主机的官方域名称为其规范名（`canonical name`）。此宏通常用于在启用规范化功能时启用本地域的规范化。

- `CANONIFY_DOMAIN_FILE(filename)` 此宏标识一个包含域名列表的文件，如果规范化功能已选择该文件，则这些域名将被转换为规范形式。

- `LOCAL_DOMAIN(alias-hostname)` 此宏定义了本地主机的别名。发送至别名的邮件将被接收，就如同直接发送给本地主机一样。

本节描述的宏和功能不仅限于 `DOMAIN` 源文件。它们可以出现在任何 `m4` 源文件中，事实上，它们通常存在于宏控制文件中。我列出它们是因为它们与 `DOMAIN` 文件的关联最为自然。我之所以这样做是参考了 `cf/cf/README` 文件中的文档。

# MAILER

`MAILER` 宏指向一个 `m4` 源文件，该文件包含定义 `Sendmail` 服务器的配置命令。在配置文件文件中必须至少出现一个 `MAILER` 命令。通常情况下，会使用多个 `MAILER` 命令。

你可能需要自定义 `OSTYPE` 文件中的某个文件，或者可能需要在 `DOMAIN` 文件中定义特定于域名的信息，但除非你开发了属于自己的邮件投递程序，否则你不需要创建 `MAILER` 源文件。相反，你需要在你的宏配置文件中调用一个或多个已存在的文件。

表 A.5 列出了每个 `MAILER` 值及其功能。这些值在宏配置（`.mc`）中通过 `MAILER(value)` 命令调用。

# 表 A.5 MAILER 值

| 名称 | 功能 |
|---|---|
| `local` | 本地和程序邮件投递器。 |
| `smtp` | 所有 `SMTP` 投递器：`smtp`, `smtp`, `smtp8` 和 `relay`。 |
| `uucp` | 所有 `UUCP` 投递器：`uucp-old` (`uucp`) 和 `uucp-new` (`uuccp`)。 |
| `usenet` | `Usenet` 支持。 |
| `fax` | 使用 `HylaFAX` 软件的传真支持。 |
| `pop` | 邮局协议 (`POP`) 支持。 |
| `procmail` | `procmail` 的接口。 |
| `mail11` | `DECnet` `mail11` 投递器。 |
| `phquery` | 用于 `CCSO` 黄的 `phquery` 程序。 |
| `qpage` | 使用 `QuickPage` 程序向传呼机发送电子邮件的投递器。 |
| `cyrus` | `Cyrus` 和 `cyrusbb` 投递器。 |

你的宏配置文件应该有一个 `MAILER(local)` 和 `MAILER(smtp)` 条目。选择 `local` 和 `smtp` 提供了标准 `TCP/IP` 安装所需的所有内容。其他的如下：

`uucp` 为直接连接到 `UUCP` 网络的系统提供 `UUCP` 邮件支持。`uucp-old` 投递器支持标准的 `UUCP` 邮件，`uucp-new` 投递器用于可以在传输过程中处理多个接收者的站点。如果系统同时拥有 `TCP/IP` 和连接，请在 `MAILER(smtp)` 条目之后指定 `MAILER(uucp)`。

`usenet` 此邮件将收件人名称包含 `group.usenet` 的本地邮件发送到 `news` 程序。大多数当前用户邮件代理直接支持 `Usenet`，且大多数用户已经有了自己喜欢的订阅帖子。通过 `Sendmail` 使用 `group, **usenet**` 语法发布新闻并不常见。

`fax` 这是一个支持 `HylaFAX` 软件的实验性投递器。该软件多年来一直描述为实验性，这让我认为它并没有被广泛使用。

`pop` 此投递器支持邮局协议。在 `Linux` 系统上，`POP` 支持由专门的 `POP` 邮件守护进程提供，不需要或使用 `MAILER(pop)` 命令。

`procmail` 此投递器为邮件投递表提供了一个 `procmail` 接口。尽管 `procmail` 被用于 `Linux` 本地邮件投递，但不需要 `MAILER(procmail)` 命令。参见第 11 章关于 `procmail` 的讨论。

`mail11` 这是一个过时的投递器，仅用于使用 `mail111` 投递器的 `DCNet` 邮件网络。

`phquery` 此投递器使用 `phquery` 程序提供 `CCSO` 黄页 (`ph`) 目录服务。用户目录服务通常在用户邮件代理中配置，而不是 `Sendmail` 中。

`cyrus` 此投递器提供了一个使用邮箱架构的本地邮件投递程序。它允许 `user+detail` 地址语法，其中 `detail` 被解释为邮箱名称。尽管具有一些高级功能，`cyrus` 和 `cyrusbb` 投递器并未被广泛使用。

`qpage` 此投递器通过 `QuickPage` 程序提供从电子邮件到传呼机的接口。

投递器的并非所有内容都由 `MAILER` 命令加载的源文件定义。我们已经看到，某些与投递器相关的命令是在 `OSTYPE` 源文件中指定的。此外，你也可以定义自己的投递器。

# 本地代码

有几个宏允许你将内容放入 `sendmail.cf`。这些宏是：

- `LOCAL_RULE` 定义一个规则集段，其中 `n` 为 `0`, `1`, `2` 或 `3`。
