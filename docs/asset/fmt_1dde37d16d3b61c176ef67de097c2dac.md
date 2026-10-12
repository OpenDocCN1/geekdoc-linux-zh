
dnl 你需要拥有 `sendmail`

如表 5.1 所示的变量定义在所有邮件器中都是可用的。请参阅附录 A 中的“OSTYPE”部分以获取这些变量的完整列表。

注意：附录 A 在 OSTYPE 文件的讨论中列出了这些变量，因为邮件器和路径信息应该存储在该处。然而，大多数 Sendmail 管理员并不想自己去创建 OSTYPE 文件。大多数管理员会直接将此类命令添加到宏配置文件中。

# 第 5 章了解厂商配置

在该系统上工作。（BITNET 是一种已经不再使用的过时邮件网络。）然而，在这一特定的配置中，没有需要从 `UUCP_RELAY` 或 `BITNET_RELAY` 清除的服务器名称。默认情况下，`UUCP_RELAY` 和 `BITNET_RELAY` 是空的，因此没有默认值需要清除。我们已经在了宏配置文件和 `linux.m4` 文件中到为止已执行的命令，其中没有一个命令设置过任何中继服务器名称。因此，这两个命令对于此配置是不必要的。

接下来是一系列九个 `define` 命令。我们知道 `PROCMAIL_MAILER_PATH` 指定了 procmail 程序的路径。然而，其他八个 `define` 变量都是新的。它们是：

- `CONTOBUILD`: 这告诉 Sendmail 是否自动重建别名（aliases）数据库。它的默认值为 `false`，这意味着必须按照第 6 章“使用 Sendmail 数据库”中的描述手动重建 aliases 数据库。如果设置为 `true`，Sendmail 会检查 aliases 源文件是否与 `aliases.pag`、`aliases.dir` 和 aliases db 数据库文件处于同一目录。如果是，Sendmail 将自动重建数据库。这种功能可能会被用于拒绝服务攻击。在 Sendmail 8.10 版本之前，该漏洞已添加了修复，Sendmail 开发人员已弃用此选项，并强烈建议不要使用它。

- `CONTO_CONNECT`: 此参数定义了 Sendmail 等待 TCP 连接完成的时间。默认情况下，Sendmail 不设置时间限制，并依靠内核中配置的 TCP/IP 参数来处理超时。列表 5.5 所示的 Red 配置 配置此超时设置为一分钟（`1m`），对于等待网络连接来说似乎已经足够了。

- `CONTRY_NULL_MX_LIST`: 这告诉 Sendmail 是否应该尝试向将自己列为最佳交换服务器的主机投递邮件。Red Hat 配置将其设置为 `true`，因此服务器将尝试向其 MX 客户端投递邮件。默认情况下将其设置为 `false`，这会导致向 MX 客户端发出的邮件被标记为配置错误。对于大多数配置，默认值是正确的。正如第 2 章解释过的，MX 服务器为客户端收集邮件，然后等待客户端使用 POP 等协议拉取邮件，或者使用 Sendmail 数据库之一将邮件路由到正确的目的地。然而，它不会使用最初投递邮件到服务器的相同地址在客户端上转发邮件。但是，正如我们在本章早期对 class 的讨论中所看到的，只有在正确配置的情况下，MX 服务器才知道它的客户端是谁。如果它接收到 MX 记录显示应该接受但 `class w` 说不应该接受的邮件，则说明存在配置错误。Red Hat 配置宽恕了这个配置错误，并尝试直接将邮件投递给客户端。

- `DONT_PROBE_INTERFACES`: 这个布尔值告诉 Sendmail 是否应该将所有网络接口的名称和地址添加到 `class w`。默认值为 `false`，这意味着 Sendmail 会探测所有网络接口并自动将这些接口的名称和地址添加到 `class w`。在默认设置下，服务器上安装的第二个接口会被自动检测并视为一个电子邮件地址。Red Hat 配置将其设置为 `true`，这意味着与主网络接口关联的名称和地址会被添加到 `class w`。如果 Red Hat 系统中安装了另一个接口，必须手动将其添加到 `class w`，它才能被视为接受的电子邮件地址。

- `ALIAS_FILE`: 此参数定义了别名文件的路径。默认路径是 `/etc/mail/aliases`。Red Hat 配置将其设置为 `/etc/aliases`，这是 Sendmail 8.11 之前的默认路径，也是 Linux 系统上别名文件最常见的位置。

- `STATUS_FILE`: 此参数定义了统计文件的路径。默认是 `/etc/mail/statistics`。这是从 Sendmail 8.11 开始的新特性，它将文件名从之前的默认值 `sendmail.st` 改为 `statistics`。Red Hat 配置保留了传统的名称，并将文件放在 Linux 的 `/var/log` 目录下。

- `UOCP_MAILER_MAX`: 此参数定义了 UCCP 邮件消息的最大接受大小。默认值为 `100,000` 字节。Red Hat 配置将其设置为 `2,000,000` 字节。

- `USERDB_SPEC`: 此参数定义了用户数据库的路径，并决定是否使用该数据库。默认情况下，没有定义用户数据库的路径。当定义路径时，在处理地址时不会使用用户数据库。Red Hat 配置声明用户数据库的路径为 `/etc/mail/userdb.db`。这意味着 Sendmail 将检查该文件是否存在，并在别名数据库应用于地址之后、用户转发文件应用之前使用它来处理地址。用户数据库在第 6 章有详细介绍。

# 理解各项特性

列表 5.5 所示的 `redhat.mc` 配置文件还包含 10 个 `FEATURE` 命令。我们已经讨论过 `redirect`、`use_cw_file` 和 `local_procmail` 功能，但还有七个我们之前未见过的新功能。这些是：

- `smrs`: `smrs` 功能告诉 Sendmail 使用 `smrs` 而不是 `/bin/smh` 作为程序。这是一个非常推荐的功能。SendMail Restricted Shell (`smrs`) 限制了通过程序执行的操作，这是 Sendmail 安全性的重要改进。与 `smrs` 功能关联的参数是 smrs 程序的路径。默认是 `CONFEBINDIR` 变量定义的名为 `smrs` 的程序。在 `redhat.mc` 文件中，`smrs` 程序被显式设置为 `/usr/sbin/smrs`。正如我们之前提到的，smrs 目录通过 `.m4 OSTYPE` 文件中的 `CONFEBINDIR` 变量设置为 `/usr/sbin`。正因如此，`redhat.mc` 配置并不需要显式路径，可能只是为了让配置自明。

- `mailertable`: 此功能告诉 Sendmail 使用 `mailertable` 数据库将特定的域名路由到特定的程序。`mailertable` 功能的参数定义了数据库类型及其路径。默认数据库类型为 `hash`，默认路径为 `/etc/mail/mailertable`。Red Hat 配置显式指定了数据库类型为 `hash`，路径为 `/etc/mail/mailertable`。由于这些是默认值，`redhat.mc` 配置提供的 `mailertable` 功能参数并不真正需要，可能只是为了让配置自明。第 6 章详细涵盖了 `mailertable` 数据库。

- `virtertable`: 此功能告诉 Sendmail 使用 `virtertable` 数据库将域名和主机名映射到特定的电子邮件地址。该数据库是一个扩展的别名数据库，接受 `class w` 或 `class {$}` 中域名或主机名的传入邮件，并根据 `virtertable` 数据库的指示路由这些邮件。第 6 章描述了如何使用该数据库。

`virtertable` 功能的参数定义了数据库类型和数据库的路径。默认数据库类型为 `hash`，默认路径为 `/etc/mail/virtertable`。`redhat.mc` 配置提供的 `virtertable` 功能参数并不真正需要，因为它重复了默认值。可能只是为了让配置自明。

- `always_add_domain`: 此功能告诉 Sendmail 在本地投递的邮件中添加域名。默认情况下，用户名就足够进行本地投递。一个快速测试说明了 `always_add_domain` 对本地地址的影响：

# 第 5 章 理解供应商的配置

```
canonify input: craig
Canonify2 input: craig
Canonify2 returns: craig
canonify returns: craig
1 input: craig
1 returns: craig
HdrFromL input: craig
AddDomain input: craig
AddDomain returns: craig < @LOCAL*
MasqHdr input: craig < @ @LOCAL*
MasqHdr returns: craig < @wren.foobirds.org.
HdrFromL returns: craig < @wren.foobirds.org.
final input: craig < @wren.foobirds.org.
final returns: craig < @wren.foobirds.org
> ^D
```

我们使用 Sendmail `-bt` 模式运行了两个测试。在两种情况下，我们都使用了一个头/地址，并提供了地址 `craig` 以通过本地邮件传输器处理。第一次测试使用了 `generic-linux.cf` 配置，它没有使用 `always_add_domain` 特性。地址进入后输出的仍然 `craig`。在第二次测试中，我们使用了 `redhat.cf` 配置，它使用了 `always_add_domain` 特性。在此测试中，`craig` 被转换为 `craig@wren.foobirds.org`。`always_add_domain` 的效果显而易见。

这是一个非常好用的特性。本地邮件上显示的地址在任何地方都是有效的。这有助于避免用户之间的困惑，而你正想避免那些困惑的用户！

`access_db` 此功能允许 Sendmail 使用访问数据库来决定哪些主机、域名和网络是可接受的邮件来源。可以使用可选参数定义数据库类型和路径来配合 `access_db` 功能。默认数据库类型为 `hash`，默认路径为 `/etc/mail/access`。访问数据库在第 6 章中描述。对抗垃圾邮件将在第 11 章介绍。

`blacklist_recipients` 此功能允许使用访问数据库来阻止来自特定收件人的邮件。通常，访问数据库用于控制来自不良源的邮件。通过此功能，访问数据库也可以用于控制发往某些目的地的邮件。`blacklist_recipients` 特性将在第 11 章中详细介绍。

`accept_unresolvable_domains` 告诉 Sendmail，如果源域名无法通过 DNS 解析，则接受来自该源的邮件。默认情况下，Sendmail 获取 `MAIL FROM:` 请求头中的主机名，并在请求 DNS 将该名称映射回地址之前才会接收入站邮件。此选项覆盖了该默认行为。

允许来自不可解析域的邮件是一个潜在的安全问题，但对于没有全天 DNS 服务的系统，此特性通常是必要的。此类系统包括可能断开连接的笔记本电脑，或者位于防火墙后未赋予完全 DNS 访问权的系统。Red Hat 配置包含了此特性，因为 Red Hat 必须创建一个适用于最广泛范围系统的配置。如果你为网络拥有全天 DNS 服务——你本应该拥有——请从你的配置中删除此特性。

在匹配 `FEATURE` 命令之后有两个 `MAILER` 命令。第一个是我们已经描述过的 `MAILER(smtp)` 命令。第二个是 `MAILER(procmail)` 命令。看到它，你可能会认为与之前描述的 `local_procmail` 参数有关。其实不是。`local_procmail` 意味着名为 `local` 的邮件传输器将使用 `procmail` 程序。而 `MAILER(procmail)` 意味着将添加一个名为 `procmail` 的邮件传输器，它将使用 `procmail` 程序。这两者是无关。通过 `MAILER(procmail)` 安装的邮件传输器仅在 `mailtable` 中配置了使用它时才会被使用。

这是一个大型配置，包含了重要的功能（如 `smsh`）和不重要的功能（如 `MAILER(procmail)`）。正如我们在第 4 章看到的，该配置运行良好并为我们的 Red Hat 系统投递邮件。但这只是一个开始。对 `accept_unresolvable_domains` 特性的讨论以及 `redhat.mc` 文件内部的注释明确表明，我们应该创建一个适合我们自己的配置。在下一节中，我们将这样做。从 `redhat.mc` 文件开始，我们创建自己的 Red Hat 配置。

# 修改 Red Hat 配置

`redhat.mc` 配置中有很多好的地方，也有一些不尽人意的地方以及冗余。由于我们要重写配置，我认为我们还应该重新组织它，将某些内容从宏配置文件移动到更适合这些项目的宏源文件中。因此，我们将编辑 `redhat.mc` 文件，创建一个新的 `OTYPE` 类型，并创建一个新的 `DOMAIN` 文件。为了做到这一点，我们首先

![](img/9639113aa446fb8976cb3d377f7aafdd_154_0.png)

将 `redhat.mc` 拷贝到 `redhat81.mc`，将 `octype/linux.m4` 拷贝到 `octype/redhat7.0.m4`，并将 `domain/generic.m4` 拷贝到 `domain/foobirds.m4`。

接下来我们编辑这些文件。首先我编辑了宏配置文件 `redhat81.mc`，将 `DOMAIN` 命令改为 `foobirds.m4` 而不是 `generic.m4`。然后我将 `CONF_USER_ID` 参数移动到新的 `OTYPE` 文件，因为我认为用户 ID 和组 ID 设置是 Red Hat Linux 特有的。我删除了 `undef` 定义，它们没有意义。我还删除了 `CONFAUTO_REBUILD`，这是一个已弃用的选项。

我考虑过将 `CONF_CONNECT` 移动到 `OTYPE` 文件，因为它设计用于覆盖 Linux 操作系统的默认 TCP 超时设置。相反，我决定将其移动到 `DOMAIN` 文件，因为我希望以非标准的方式处理 MX 记录。我删除了 `CONF_PROBE_INTERFACES` 选项，因为我拥有全天 DNS 服务，因此不需要该特性。

## 表 5.2 重写 Red Hat 配置文件（续）

| 命令 | 处置方式 |
|---|---|
| `blacklist_recipients` | 移动到 DOMAIN 文件。 |
| `accept_unresolvable_domains` | 已删除。 |
| `MAILER(smtp)` | 保留在宏配置文件中。 |
| `MAILER(procmail)` | 保留在宏配置文件。 |

列表 5.6 显示了新配置的三个文件的内容。检查该列表将清晰说明各个部分的位置。

## 列表 5.6 自定义 DOMAIN、OSTYPE 和宏控制文件

```
