

# 第 5 章了解厂商配置

在该系统上工作。（BITNET 是一种已经不再使用的过时邮件网络。）然而，在这一特定的配置中，没有需要从 UUCP_RELAY 或 BITNET_RELAY 清除的服务器名称。默认情况下，UUCP_RELAY 和 BITNET_RELAY 是空的，因此没有默认值需要清除。我们已经了在宏配置文件和 `linux.m4` 文件中到为止已执行的命令，其中没有一个命令设置过任何中继服务器名称。因此，这两个命令对于此配置是不必要的。

接下来是一系列九个 `define` 命令。我们知道 `PROCMAIL_MAILER_PATH` 指定了 procmail 程序的路径。然而，其他八个 `define` 变量都是新的。它们是：

- **CONTOBUILD**: 这告诉 Sendmail 是否自动重建别名（aliases）数据库。它的默认值为 `false`，这意味着必须按照第 6 章“使用 Sendmail 数据库”中的描述手动重建 aliases 数据库。如果设置为 `true`，Sendmail 会检查 aliases 源文件是否与 `aliases.pag`、`aliases.dir` 和 aliases db 数据库文件处于同一目录。如果是，Sendmail 将自动重建数据库。这种功能可能会被用于拒绝服务攻击。在 Sendmail 8.10 版本之前，该漏洞已添加了修复，Sendmail 开发人员已弃用此选项，并强烈建议不要使用它。

- **CONTO_CONNECT**: 此参数定义了 Sendmail 等待 TCP 连接完成的时间。默认情况下，Sendmail 不设置时间限制，并依靠内核中配置的 TCP/IP 参数来处理超时。列表 5.5 所示的 Red 配置 配置此超时设置为一分钟（`1m`），对于等待网络连接来说似乎已经足够了。

- **CONTRY_NULL_MX_LIST**: 这告诉 Sendmail 是否应该尝试向将自己列为最佳交换服务器的主机投递邮件。Red Hat 配置将其设置为 `true`，因此服务器将尝试向其 MX 客户端投递邮件。默认情况下将其设置为 `false`，这会导致向 MX 客户端发出的邮件被标记为配置错误。对于大多数配置，默认值是正确的。正如第 2 章解释过的，MX 服务器为客户端收集邮件，然后等待客户端使用 POP 等协议拉取邮件，或者使用 Sendmail 数据库之一将邮件路由到正确的目的地。然而，它不会使用最初投递邮件到服务器的相同地址在客户端上转发邮件。但是，正如我们在在本章早期对 class 的讨论中所看到的，只有在正确配置的情况下，MX 服务器才知道它的客户端是谁。如果它接收到 MX 记录显示应该接受但 `class w` 说不应该接受的邮件，则说明存在配置错误。Red Hat 配置宽恕了这个配置错误，并尝试直接将邮件投递给客户端。

- **DONT_PROBE_INTERFACES**: 这个布尔值告诉 Sendmail 是否应该将所有网络接口的名称和地址添加到 `class w`。默认值为 `false`，这意味着 Sendmail 会探测所有网络接口并自动将这些接口的名称和地址添加到 `class w`。在默认设置下，服务器上安装的第二个接口会被自动检测并视为一个电子邮件地址。Red Hat 配置将其设置为 `true`，这意味着与主网络接口关联的名称和地址会被添加到 `class w`。如果 Red Hat 系统中安装了另一个接口，必须手动将其添加到 `class w`，它才能被视为接受的电子邮件地址。

- **ALIAS_FILE**: 此参数定义了别名文件的路径。默认路径是 `/etc/mail/aliases`。Red Hat 配置将其设置为 `/etc/aliases`，这是 Sendmail 8.11 之前的默认路径，也是 Linux 系统上别名文件最常见的位置。

- **STATUS_FILE**: 此参数定义了统计文件的路径。默认是 `/etc/mail/statistics`。这是从 Sendmail 8.11 开始的新特性，它将文件名从之前的默认值 `sendmail.st` 改为 `statistics`。Red Hat 配置保留了传统的名称，并将文件放在 Linux 的 `/var/log` 目录下。

- **UOCP_MAILER_MAX**: 此参数定义了 UCCP 邮件消息的最大接受大小。默认值为 `100,000` 字节。Red Hat 配置将其设置为 `2,000,000` 字节。

- **USERDB_SPEC**: 此参数定义了用户数据库的路径，并决定是否使用该数据库。默认情况下，没有定义用户数据库的路径。当定义路径时，在处理地址时不会使用用户数据库。Red Hat 配置声明用户数据库的路径为 `/etc/mail/userdb.db`。这意味着 Sendmail 将检查该文件是否存在，并在别名数据库应用于地址之后、用户转发文件应用之前使用它来处理地址。用户数据库在第 6 章有详细介绍。

# 理解各项特性

列表 5.5 所示的 `redhat.mc` 配置文件还包含 10 个 `FEATURE` 命令。我们已经讨论过 `redirect`、`use_cw_file` 和 `local_procmail` 功能，但还有七个我们之前未见过的新功能。这些是：

- **smrs**: `smrs` 功能告诉 Sendmail 使用 `smrs` 而不是 `/bin/smh` 作为程序。这是一个非常推荐的功能。SendMail Restricted Shell (smrs) 限制了通过程序执行的操作，这是 Sendmail 安全性的重要改进。与 `smrs` 功能关联的参数是 smrs 程序的路径。默认是 `CONFEBINDIR` 变量定义的名为 `smrs` 的程序。在 `redhat.mc` 文件中，`smrs` 程序被显式设置为 `/usr/sbin/smrs`。正如我们之前提到的，smrs 目录通过 `.m4 OSTYPE` 文件中的 `CONFEBINDIR` 变量设置为 `/usr/sbin`。正因如此，`redhat.mc` 配置并不需要显式路径，可能只是为了让配置自明。

- **mailertable**: 此功能告诉 Sendmail 使用 `mailertable` 数据库将特定的域名路由到特定的程序。`mailertable` 功能的参数定义了数据库类型及其路径。默认数据库类型为 `hash`，默认路径为 `/etc/mail/mailertable`。Red Hat 配置显式指定了数据库类型为 `hash`，路径为 `/etc/mail/mailertable`。由于这些是默认值，`redhat.mc` 配置提供的 `mailertable` 功能参数并不真正需要，可能只是为了让配置自明。第 6 章详细涵盖了 `mailertable` 数据库。

- **virtertable**: 此功能告诉 Sendmail 使用 `virtertable` 数据库将域名和主机名映射到特定的电子邮件地址。该数据库是一个扩展的别名数据库，接受 `class w` 或 `class {$}` 中域名或主机名的传入邮件，并根据 `virtertable` 数据库的指示路由这些邮件。第 6 章描述了如何使用该数据库。

`virtertable` 功能的参数定义了数据库类型和数据库的路径。默认数据库类型为 `hash`，默认路径为 `/etc/mail/virtertable`。`redhat.mc` 配置提供的 `virtertable` 功能参数并不真正需要，因为它重复了默认值。可能只是为了让配置自明。

- **always_add_domain**: 此功能告诉 Sendmail 在本地投递的邮件中添加域名。默认情况下，用户名就足够进行本地投递。一个快速测试说明了 `always_add_domain` 对本地地址的影响：

