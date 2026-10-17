
## 第 20 章：邮件服务器

存储在 `/etc/aliases` 文件中。该文件由单行别名记录组成，将别名与用户地址关联。你可以编辑此文件以添加新条目或更改旧条目。它们通过 `newaliases` 命令存储在 `aliases.db` 文件中以便查找，该命令运行 Sendmail 指令来更新 `aliases.db` 文件。

别名允许你为电子邮件地址或一组电子邮件地址提供不同的名称。其最实用的功能之一是创建用户邮件列表。发送到别名的邮件将发送给与别名关联的用户或用户列表。别名条目由由冒号命名的别名和随后的用户名、用逗号分隔的用户列表组成。例如，要将 `filmcritic` 别名为用户 `george@rabbit.mytrek.com`，你可以使用以下命令：

```
filmcritic: george@rabbit.mytrek.com
```

将 `singers` 别名为本地用户 `aleina` 和 `larisa`，你应该使用：

```
singers: aleina, larisa
```

你也可以将别名作为目标地址，在这种情况下，它们将展开为各自的用户地址。例如，表演者 `filmcritic` 和 `singers` 别名指向用户 `george@rabbit.mytrek.com`、`aleina` 和 `larisa`：

```
performers: filmcritic, singers
```

一旦你在 `/etc/mail/aliases` 文件中创建了条目，你需要使用 `newaliases` 命令生成数据库版本：

```
newaliases
```

注意：Sendmail 现在支持邮件提交模式。在这种模式下，Sendmail 不再作为具有相应 root 权限的服务器运行，而仅仅是提交邮件。在此模式下，Sendmail 可以被邮件客户端调用来发送邮件。邮件提交模式使用 `/etc/mail/submit.cf` 配置文件，该文件可以使用 `/etc/mail/submit.mc` 文件中的宏进行配置。

## Sendmail 配置

Sendmail 配置文件为 `sendmail.cf`，位于 `/etc` 目录。该文件由长长的邮件定义列表组成，用于设置通用选项、指定 MTA 并定义重写规则。一系列选项设置了某些功能，例如邮件消息的最大大小以及 The MTAs。MTA 是 Sendmail 路由消息的邮件传输者。重写规则“重写”邮件地址以便将适当的 Internet 连接路由到目的地。

`sendmail.cf` 可能会非常复杂且难以理解。为了简化配置过程，你可以使用宏通过 M4 预处理器生成 `sendmail.cf` 文件。这需要安装 `sendmail-cf` 软件包。宏放置在 `/etc/mail/sendmail.mc` 文件中。在这里，你可以使用宏指定你想要的 Sendmail 的定义和功能，然后使用这些宏在 `sendmail.cf` 文件中生成相应的定义和重写规则。作为 Sendmail 软件包的一部分，`/usr/share/sendmail-cf` 目录下提供了多个特殊版本的 `sendmail.mc` 文件。这些文件以系统名称开头并以 `.mc` 为结尾。在许多发行版中，一个为你的发行版定制的特殊版本已经安装并作为你的 `/etc/mail/sendmail.mc` 文件。

一旦你配置了 `sendmail.mc` 文件，就可以可以使用以下命令生成 `sendmail.cf` 文件。请务必备份原始的 `sendmail.cf` 文件。你可以重命名 `sendmail.mc` 文件以反映特定的配置。你可以拥有任意数量不同的 `.mc` 文件并使用它们来实现不同的配置。在 Red Hat 和 Fedora 上，你可以在 `/etc/mail` 目录下使用以下命令：

```
make -C /etc/mail
```

或者，你可以使用原始的 m4 宏命令：

```
m4 sendmail.mc > /etc/mail/sendmail.cf
```

然后你需要重启 Sendmail 服务器以使配置生效：

```
service sendmail restart
```

在 `sendmail.mc` 文件中，你可以使用 `define` 命令设置 Sendmail 变量的值，或使用已定义的 Sendmail 宏设置特定的 Sendmail 功能，从而配置 Sendmail 的不同方面。例如，将 `PROC_PATH` 变量分配给目录 `/usr/bin/procmail`，你应该使用以下命令：

```
define ('PROMAIL_MAIL_PATH', '/usr/bin/procmail')
```

同样，如果有你不想定义的变量，可以使用 `undefine` 命令删除它们：

```
undefined ('UUCP_RELAY')
```

要指定运行 Sendmail 服务器的操作系统类型，你将使用 `OSTYPE` Sendmail 宏。以下示例指定了 Linux 操作系统：

```
OSTYPE ('linux')
```

| 特性 | 描述 |
| --- | --- |
| `use_cw_file` | 检查由邮件服务器 `/etc/mail/local-hosts` 文件提供的主机。 |
| `use_ct_file` | 从 `/etc/trusted-users` 文件中读取用户列表。这些是可以更改邮件发送人名称的信任用户。 |
| `redirect` | 拒绝所有发往 "address REDIRECT" 的邮件，前提是在 `/etc/aliases` 文件中放置了转发地址。 |
| `mailertable` | 使用邮件表文件 `/etc/mail/mailertable` 来覆盖特定域的路由。 |
| `domaintable` | 使用域名表文件 `/etc/mail/domaintable` 将一个域名映射到另一个域名。当你更改域名时非常有用。 |
| `allmasquerade` | 导致接收者地址也伪装成来自伪装主机。 |
| `masquerade_entire` | 使整个接收者地址伪装成来自伪装主机。 |
