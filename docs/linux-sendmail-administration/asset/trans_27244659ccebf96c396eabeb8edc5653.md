
Sendmail 无需你的任何帮助就已经知道与本地用户名关联的家目录（这些是存储在 `$` 中的值）。仅仅因为 Sendmail 提供了一个配置选项，并不意味着你将来需要使用它。

大多数开关都属于你永远不会使用的配置选项类。`-m` 开关验证键是否存在，但不会返回该键的值。这通常很少被使用，因为在普通数据库中成功查找已经验证了该键的值。`-a` 开关在查找结果返回的值末尾添加一个固定字符串。例如，`-a foobirds.org` 会在数据库的每个响应中添加 `.foobirds.org` 字符串。这个开关很少使用，因为如果数据库中的每个值都需要附加特定的特定值，在最初构建数据库时就可以轻松完成，而无需对 `sendmail.cf` 进行任何手动修改。

最常用且最重要的开关是 `-o`，它告诉 Sendmail 一个基于数据的文件是一个选项。有了这个开关，在 `sendmail.cf` 中可以预留该开关并包含一个 `K` 命令，而不需要数据库已经存在。如果没有 `-o` 开关，如果找不到数据库文件，Sendmail 将在尝试访问数据库的第一个命令处失败。使用 `-o` 使 Sendmail 更加宽容且更健壮。

我们已经涵盖了大部分 `K` 命令名称、数据库类型和开关。`K` 命令的最后一个字段是路径。这仅仅是数据库的名称（`K` 命令会根据数据库类型向路径添加正确的扩展名——例如 `.db`）。只有当数据库位于 Sendmail 外部时，才需要路径值，因为由 `K` 命令声明的数据库类型是 Sendmail 内部的。当使用内部数据库时，不需要路径。`sendmail.cf` 文件中的一些示例 `K` 命令将使命令结构变得清晰。

## 实际命令

示例配置包含五个 `K` 命令，均显示在列表 7.6 中。

### 列表 7.6 sendmail.cf 中的的 K 命令

```
[kraig] $ grep '^K' /etc/sendmail.cf
Karith ar
Kquote devote
Kmailtable hash -o /etc/mail/mailertail
Kvirtuser hash -o /etc/mail/virtertuser
Kaccess hash /etc/mail/access
```

让我们从底往上分析列表 7.6。最后一个 `K` 命令声明了一个数据库名为 `access`。该数据库是标准的 `hash` 类型。包含数据库的文件是 `/etc/mail/access`。所有这些信息——内部名称、数据库类型以及持有数据库的文件——由 `K` 命令定义，它们都是我们示例配置文件中 `FEATURE(`access_db`)` 命令的直接结果。用于控制邮件中继和投递的 `access` 数据库将在第 6 章中介绍。

之前的 `K` 命令定义了 `virtuerstable` 和 `mailterable` 数据库，它们源于示例配置文件中找到以下命令：

```
FEATURE(`mailterable`, `hash -o /etc/mail/mailterable`)
FEATURE(`virtuerstable`, `hash -o /etc/mail/virtuerstable`)
```

两个 `hash` 类型数据库都使用了 `-o` 开关，这意味着即使找不到这些文件，Sendmail 也会运行。`access` 数据库的 `K` 命令没有使用 `-o` 开关。如果找不到 `/etc/mail/access` 文件，当命令尝试使用 `access` 数据库时，Sendmail 将失败。即使你没有 `access` 数据库的条目，也要创建一个空的 `/etc/mail/access.db` 文件以确保 Sendmail 的健壮，如下例所示：

```
+ [root] touch /etc/mail/access
[root] makedmap /etc/mail/access < /etc/mail/access
```

`mailterable`、`virtuerstable` 和 `access` 数据库在第 6 章中都有介绍。然而，其他数据库在该章并未介绍。`ar` 和 `deque` 数据库都是伪数据库。这意味着它们不是真实的数据库。相反，它们是 Sendmail 的内部例程，如果它们是数据库，则会被重写规则访问。已经讨论过的 `deque` map 用于移除地址中的引号。`ar` map 用于为 STARTTLS 设置执行算术函数。STARTTLS 将在第 12 章中介绍。

四个命令 `D`、`C`、`F` 和 `K` 说明了 `sendmail.cf` 文件中 `Local Info` 部分的所有内容。对于试图直接配置 `sendmail.cf` 的系统管理员来说，`Local Info` 部分是该文件最重要的部分，因为信息随系统而异。我们已经涵盖了示例系统中 `Local Info` 部分的每一个命令，但在移动到 `Options` 部分之前，我们应该介绍出现在 `Local Info` 之前的唯一配置命令——

## 版本级命令

版本级命令 (`V`) 定义了 `sendmail.cf` 文件的版本。这不应与用于标识 Sendmail 源码发布号的 `Z` 变量，或为宏源文件定义修订控制信息的 `m4 VERSIONID` 宏相混淆。

![](img/b8082498451dba2bf0cf2907c85c4c83_217_0.png)

## 第 7 章 sendmail.cf 文件

`V` 命令告诉 Sendmail 支持该配置所需的语法和命令级别。如果 Sendmail 程序无法支持请求的命令和语法，它会对它不理解的命令进行报错，并显示以下版本级错误消息：

```
[root]# sendmail -v -t
/etc/sendmail.cf: version 9 exceeds 8.11.0
/etc/sendmail.cf: version 8.11.0 exceeds 9
```
