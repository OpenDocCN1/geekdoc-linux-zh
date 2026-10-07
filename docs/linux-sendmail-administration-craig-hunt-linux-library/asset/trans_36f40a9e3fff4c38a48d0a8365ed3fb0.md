

# genericstable 169

它没有为 procmail 添加任何重写规则。要使用 procmail 邮件投递器处理非本地邮件，你需要将其添加到 mailertable 中，如下例所示：

此示例通过 procmail 为 fishforowl.org 域发送邮件。使用 procmail 的主要原因是它提供了强力的邮件过滤工具。（procmail 的功能将在第 11 节中介绍）。在上述示例条目的案例中，我们必须假设发往 fishforowl.org 的邮件需要经过特殊的过滤过滤。

在 Red Hat 默认配置中定义的数据库中，`mailertable` 是你最不可能使用的。除非你需要用 procmail 过滤发出的邮件，或者你必须将邮件发送到无法处理标准邮件的服务器，否则你不会在该数据库中创建任何条目。

尽管 `redhat.mc` 中配置了大量的数据库，但还有四个未包含在该配置中的基础数据库。在这四个数据库中，只有 `genericstable` 被频繁使用。

![](img/9639113aa446fb8976cb3d377f7aafdd_192_0.png)

# genericstable

`genericstable` 数据库重写发送者地址。一个 `genericstable` 条目由两个字段组成：原始发送者地址（作为键）和重写后的发送者地址（作为该键返回的值）。与其他数据库一样，`genericstable` 源文件必须通过 `makemap` 处理以构建哈希数据库，然后 Sendmail 才能使用它。列表 6.12 显示了一个合理的 `genericstable` 源文件。

+ 列表 6.12 使用 genericstable 映射发送者地址

```
andy andy.wright@foofield.org
sara sara.henson@foofield.org
kathy katleen.mccafferty@foofield.org
```

根据列表 6.12 所示的 `genericstable`，从用户账户 `andy` 发出的邮件其发送者地址为 `andy.wright@foofield.org`。如果你还记得本章之前对用户数据库的讨论，这可能听起来很熟悉。`genericstable` 中的条目执行的功能与用户数据库中的 `in` 条目完全相同——两种类型的条目都会重写发送者地址。

`genericstable` 数据库有一个用户数据库中没有的小功能。它可以接受原始地址中的*detail* 语法，并将地址的*detail* 部分作为变量 `%1` 传递给输出地址，其方式如下：

```
sales+@insects.org %1@sales.insects.org
```

当然，*detail* 语法只有在你实际使用它时才重要，而且它很少被使用。
如果域名名包含在 `genericstable` 条目的第一个字段中，则该域名必须在类 G 中定义。可以使用 `GENERIC_DOMAIN` 宏将值存储在类 G 中，也可以从由 `GENERIC_DOMAIN_FILE` 标识的文件加载到类 G。例如，以下命令将域名名 `insects.org` 存储在类 G 中：

```
GENERIC_DOMAIN('insects.org')
```

而接的命令从名为 `/etc/mail/generics-domains` 的文件加载类 G：
类 G 中的域名名通常需要精确匹配。使用上述方法，`user@insects.org` 将匹配类 G 设置的条件，而 `user@fly.insects.org` 则不会匹配，尽管 `fly.insects.org` 是 `insects.org` 域的一部分。要让 Sendmail 匹配类 G 中定义域的所有主机和子域名，请使用 `FEATURE(generic_entire_domain)`

```
GENERIC_DOMAIN_FILE('/etc/mail/generics-domains')
```

用户数据库与 `genericstable` 之间的相似性意味着你可以使用任一数据库来重写发送者地址。`genericstable` 条目的语法稍微简单，因为 `genericstable` 不使用像 `fieldname` 这样的关键字。但 `genericstable` 只处理发送者地址。接收者地址必须在单独的数据库中处理， `/etc/aliases` 或用户数据库。某些管理员喜欢 `genericstable` 数据库的简单性；另一些人则倾向于用户数据库，因为他们可以将所有内容放在一个文件中。这主要是一个喜好问题。两个文件的效果相同。

我通常倾向于使用 `aliases` 处理接收者地址，使用 `genericstable` 处理发送者地址，因为这是我的习惯。我已经设置了好几处这样的配置。然而，`redhat.mc` 文件在配置中没有对 `genericstable` 支持。要在该配置中使用 `genericstable`，我必须在宏配置 `m4` 中添加 `FEATURE('genericstable')` 命令以构建新的 `sendmail.cf` 文件。在 `redhat.mc` 配置的情况下，使用用户数据库可能是最简单的。

# 很少使用的数据库

`genericstable` 是我使用的唯一 Red Hat 未包含在配置中的数据库。Red Hat 未配置的另外三个数据库非常少被使用。

# 很少使用的数据库

剩余的三个数据库在当前配置中几乎没用，因为它们处理的是过时的网络、过时的语法或罕见的情况。这三个数据库是：

- `dominateable`：`domaintable` 旨在通过在所有邮件中将旧域名翻译为新域名，来简化从旧域名到新域名的过渡。你很少遇到必须更改域名的情况，但如果你确实遇到了这种情况，这个数据库可以提供帮助。旧域名是键，新域名是该键返回的值。例如，假设我们将销售部门的域名从 `sales.business.com` 更改为 `marketing.business.com`。我们可以在 `domaintable` 中放置以下行行：

```
sales.business.com marketing.business.com
```

在 Sendmail 使用它之前，`domaintable` 文件必须转换为哈希数据库。文件名显而易见。它必须与 Sendmail 中配置的数据库名称匹配。有一点是：在 Sendmail 配置或 `makemap` 命令行中没有包含文件扩展名。如果你不提供文件扩展名，`makemap` 将根据数据库类型为文件名应用正确的扩展名。由于 Sendmail 从配置中知道数据库类型，它将搜索具有正确扩展的文件。

- `uucp`：此数据库已过时。
- `bitdomain`：BITNET 在 IBM 尚未提供 TCP/IP 时创建。

![](img/9639113aa446fb8976cb3d377f7aafdd_194_0.png)

# makemap 命令

`makemap` 命令作为工具随 Sendmail 一起提供，帮助构建数据库。在本章讨论的所有真实数据库中，只有一个 `aliases` 数据库——由 `newaliases` 构建——不是通过 `makemap` 命令构建的。

`makemap` 命令读取标准输入并根据你在命令行上提供的指令输出数据库。命令行接受三个参数：命令行选项、数据库类型以及输出数据库的名称。

文件名显而易见。它必须与 Sendmail 中配置的数据库名称匹配。有一点是：在 Sendmail 配置或 `makemap` 命令行中没有包含文件扩展名。如果你不提供文件扩展名，`makemap` 将根据数据库类型为文件名应用正确的扩展名。例如，我们使用此命令构建 `virtusetable`：

```
[root]# makemap hash virtusetable < virtusetable
```

简单读取此命令可能意味着我们读取并写入名为 `virtusetable` 的文件。实际上，我们读取了名为 `virtusetable` 的文件并写入了名为 `virtusetable.db` 的文件，因为 `makemap` 为哈希类型数据库添加了正确的 .db 扩展名。

`makemap` 命令的类型字段接受许多不同的数据库类型，以支持不同计算机上的各种数据库。然而，在 Linux 系统上，数据库类型将是 `hash` 或 `btree`，这是由 NEWDB 编译器提供的两种数据库类型。所选类型必须与 Sendmail 配置中为特定数据库定义的数据库类型匹配。在由 `makemap` 构建的所有数据库中，除用户数据库外，在 Sendmail 配置中默认为哈希类型数据库。用户数据库默认为 `btree`。

