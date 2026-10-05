
# 第 10 章 测试 Sendmail

`mailq` 命令。在列表 10.7 中，这正是我们使用的命令。使用详细模式（verbose mode）可以显示邮件是否成功交付。

除了列表 10.7 中使用的 `-SSender` 和 `-qRecipient` 格式外，还可以使用 `-lqId` 参数格式通过队列 ID 选择消息。例如，`sendmail -qIEA1Fdp00879` 将处理列表 10.6 所示队列中的消息。使用选择性队列处理，可以在修复导致邮件进入队列的问题后，快速地将项目从队列中移出。

# 在测试模式下运行 Sendmail

在书中广泛使用的 Sendmail 选项是 `-bt`，该选项将 Sendmail 置于地址测试模式（address test mode）。当 Sendmail 处于测试模式时，你可以检查 `sendmail.cf` 变量和类的内容、规则中的列表，并检查地址通过重写规则（rewrite rules）的流程。`-bt` 选项是你精炼和调试 Sendmail 配置最重要的工具。

在书中，你已经看到了许多使用 `-bt` 选项运行 `sendmail` 命令的示例。但这些示例的重点在于测试结果；你并没有得到关于创建这些测试的“魔法命令”的详细解释。在本节中，我们将仔细查看每个命令、其语法及其目的。

运行 `sendmail -bt` 时，你会看到以下内容：

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
>
```

Sendmail 显示的第一行表示我们已进入地址测试模式，且没有自动运行规则集 3（ruleset 3）。3 是规范化规则（canonify rules）。在正常运行期间，Sendmail 处理的所有地址都会首先通过规范化处理，然后根据地址类型通过其他规则集。（如果你不确定我在说什么，你可能想参考第 8 章“理解规则”中的规则集材料）。曾几何时，地址测试模式无论你是否想要，都会通过规则集 3 处理每一个地址。现在它不再是理所当然的，但它会打印此消息，让老手知道，只有当你专门请求发送通过规则集 3 的地址进行测试时，地址才会通过规则集 3 处理。显示的第二行告诉你在 `>` 提示符处输入一个规则集和一个地址。规则后跟地址是输入类型，但还有许多其他类型。表 10.1 列出了你可以在地址测试模式提示符下输入的命令。

**表 10.1** 地址测试模式命令

| 命令 | 用法 |
| --- | --- |
| rulesets address | 通过逗号分隔的规则集列表处理地址。 |
| =ruleset | 显示规则集的内容。 |
| =M | 显示所有邮件传输器（mailer）定义。 |
| $v | 显示变量 v 的值。 |
| $=c | 显示类 c 中的值。 |
| .Dvalue | 将变量 v 设置为 value。 |
| .Cvalue | 为类 c 添加 value。 |
| -dvalue | 将调试级别设置为 value。 |
| /try flags | 设置由 `/parse` 和 `/try` 用于地址处理的标志。 |
| /try mailer address | 为该邮件传输器处理地址。 |
| /parse address | 返回地址的邮件传输器/主机/用户交付三元组。 |
| /canon hostname | 规范化主机名。 |
| /mx hostname | 查询主机名的 MX 记录。 |
| /map mapname key | 在由 mapname 指定的数据库中查找 key。 |
| /quit | 退出地址测试模式。 |

表 10.1 中的第一条目代表了输入规则集列表和由这些规则集处理的地址的传统语法。因此，输入 `canonify craig` 将通过规则集 `canonify` 处理地址 `craig`，而输入 `canonify,parse kathy@grebe.foobirds` 将通过 `canonify` 和 `parse` 处理地址。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。

# 10.8 通过规则集处理地址

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,parse@bird.org
canonify        input: al @ bird . org
canonify2       input: al < @ bird . org >
canonify2       returns: al < @ bird . org >
canonify        returns: al < @ bird . org >
parse           input: al < @ bird . org >
Parse0          returns: al < @ bird . org >
ParseLocal     input: al < @ bird . org >
ParseLocal     returns: al < @ bird . org >
Parse1          input: al < @ bird . org >
Mailertable     input: < bird . org al < @ bird . org >
Mailertable     input: < > org al @ bird . org >
Mailertable     returns: al < @ bird . org >
Mailertable     returns: al < @ bird . org >
MailerTriple returns: < > al < @ bird . org >
MailerTriple returns: $ # esmtp @ bird . org >
               $: al < @ bird . org >
Parse1
parse           returns: $ # esmtp @ bird . org >
               $: al < @ bird . org >
> /quit
```

列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。列表 10.8 处理了地址 `@bird.org`。列表 10.8 显示了使用 `canonify` 和 `parse` 处理地址的示例。 (此处省略)

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,parse@bird.org
canonify        input: al @ bird . org
canonify2       input: al < @ bird . org >
canonify2       returns: al < @ bird . org >
canonify        returns: al < @ bird . org >
parse           input: al < @ bird . org >
Parse0          returns: al < @ bird . org >
ParseLocal     input: al < @ bird . org >
ParseLocal     returns: al < @ bird . org >
Parse1          input: al < @ bird . org >
Mailertable     input: < bird . org al < @ bird . org >
Mailertable     input: < > org al @ bird . org >
Mailertable     returns: al < @ bird . org >
Mailertable     returns: al < @ bird . org >
MailerTriple returns: < > al < @ bird . org >
MailerTriple returns: $ # esmtp @ bird . org >
               $: al < @ bird . org >
Parse1
parse           returns: $ # esmtp @ bird . org >
               $: al < @ bird . org >
> /quit
```

列表 10.8 处理了地址 `@bird.org`。该列表显示 `@bird.org` 通过规则集 3、`canonify` 和 `parse` 进行处理。该地址通过规则集 3、`canonify` 和 `parse` 进行处理。该地址通过规则集 3、`canonify` 和 `parse` 进行处理。该地址通过规则集 3、`canonify` 和 `parse` 进行处理。该地址通过规则集 3、`canonify` 和 `parse` 进行处理。该地址通过规则集 3、`canonify` 和 `parse` 进行处理。 (此处省略)

# 测试地址

使用 `/parse` 命令地址

`/parse` 命令规范化并解析地址，创建邮件交付三元组。它随后根据邮件传输器准备地址。列表 10.9 显示了 `/parse` 命令的作用。

# 10.9 使用 /parse 命令测试地址

![](img/b02498451dba2bf0cf2907c854c8303_0.png)

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
>
final       input: al < @ bird . org
final       returns: al @ bird . org
mailer smtp, host bird.org., user@bird.org
>/quit
```

`/parse` 命令开始打印两条信息消息。第一条显示输入地址在处理期间存储在变量 `g` 中。注释将输入地址称为“规范化地址”。这意味着在存储到 `g` 之前，任何标准的 RFC 822 格式都已移除。第二条消息告诉你地址正作为信封地址进行处理。

第一个 `/parse` 命令通过规则集 3（`canonify`）和规则集 0（`parse`）处理地址。一旦为地址选择了 `smtp` 邮件传输器，该地址将通过规则集 2（由 `EnvSMTP` 的 `R` 参数定义）以及规则集 4（`final`）。这种广泛的处理正是第 8 章图 8.1 所示的内容。这种类型的测试通常用于观察单个规则对规则集的影响。

`/parse` 命令显示的最后一行是用于用于该地址的邮件交付三元组。如果 `/parse` 认为向所选地址交付会出现错误，它还会显示一条错误消息，如下：

```
final       returns: al @ bird . org
al@bird.org... Transient parse error - message queued
for future delivery
```

# 处理特定地址类型

默认情况下，`/parse` 命令和 `/try` 命令将地址作为信封接收地址处理。你会从图 8.1 回想起，不同类型的地址由不同的规则处理。使用 `/tryflags` 命令选择不同的地址处理类型。`/tryflags` 命令接受四个可能的值：

- H 请求报头地址处理。
- E 请求信封地址处理。
- S 请求发送者地址处理。
- R 请求接收者地址处理。

