
| `=c` | 显示类`c`中的值。 |
| `.Dvvalue` | 将变量`v`设置为`value`。 |
| `.Ccvalue` | 为类`c`添加`value`。 |
| `-dvalue` | 将调试级别设置为`value`。 |
| `/tryflags flags` | 设置用于`/parse`和`/try`运行时地址处理的标志位。 |
| `/try mailer address` | 为该邮件传输器处理地址。 |
| `/parse address` | 返回该地址的邮件传输器/主机/用户交付三元组。 |
| `/canon hostname` | 规范化主机名。 |
| `/mx hostname` | 查询主机名的`MX`记录。 |
| `/map mapname key` | 在由`mapname`指定的数据库中查找`key`。 |
| `/quit` | 退出地址测试模式。 |

表 10.1 中的第一条代表了输入规则集列表和要由这些规则处理的地址的传统语法。因此，输入`canonify craig`将通过规则集`canonify`处理地址`craig`；输入`canonify, parse kathy@birds.org`将通过`canonify`和`parse`处理地址。列表 10.8 显示了使用`canonify`和`parse`处理地址的示例。

## 列表 10.8 通过规则集处理地址

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT invoked)
nEnter<ruleset> <address>
> 3,parse al@bird.org
canonify input: al@bird.org
Canonify2 input: al@bird.org
Canonify2 returns: al@bird.org
canonify returns: al@bird.org
parse input: al@bird.org
Parse0 input: al@bird.org
Parse0 returns: al@bird.org
ParseLocal input: al@bird.org
ParseLocal returns: al@bird.org
Parse1 input: al@bird.org
Mailtable input: <bird.org> al@bird.org
Mailtable input: <bird.org> al@bird.org
Mailtable returns: al@bird.org
Mailtable returns: al@bird.org
MailerToTriple input: <@bird.org>
MailerToTriple returns: al@bird.org
Parse1 returns: $ esmtp @bird.org
Parse1: <@bird.org>
parse returns: $ esmtp @bird.org
parse returns: al@bird.org
parse returns: $ al@bird.org
> /quit
```

列表 10.8 通过规则集 3、`canonify`规则集和`parse`规则集处理`@bird.org`。此示例表明，如果规则集有名称，可以通过其名称识别。示例中所有其他规则集`Canonify2`、`Parse1`等都是从规则集 3 或`parse`调用的（要了解各个规则集的作用，请参阅第 8 章的描述）。这种测试通常用于观察单个规则集 (3) 对地址的影响。模拟基本`Sendmail`处理的多步骤测试可以通过其他测试命令完成。

## 使用 `/parse` 命令进行测试

`/parse`命令可以规范化并解析地址，创建交付三元组。它根据为选的邮件传输器为地址准备好交付。列表 10.9 显示了`/parse`命令的作用。

### 10.9 使用 `/parse` 命令处理地址

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT invoked)
Enter<ruleset> <address>
> /parse al@bird.org
Cracked address = $ Parsing envelope address
canonify input: al@bird.org
Canonify2 input: al@bird.org
Canonify2 returns: al@bird.org
canonify returns: al@bird.org
parse input: al@bird.org
Parse0 input: al@bird.org
Parse0 returns: al@bird.org
ParseLocal input: al@bird.org
ParseLocal returns: al@bird.org
Parse1 input: al@bird.org
Mailtable input: <bird.org> al@bird.org
Mailtable input: <bird.org> al@bird.org
Mailtable returns: al@bird.org
Mailtable returns: al@bird.org
MailerToTriple input: <@bird.org>
MailerToTriple returns: al@bird.org
Parse1 returns: $ esmtp @bird.org
Parse1: <@bird.org>
parse returns: $ esmtp @bird.org
parse returns: al@bird.org
2 input: al@bird.org
2 returns: al@bird.org
EnvToSMTP input: al@bird.org
PseudoToReal input: al@bird.org
PseudoToReal returns: al@bird.org
MasqSMTP input: al@bird.org
MasqSMTP returns: al@bird.org
EnvToSMTP input: al@bird.org
EnvToSMTP returns: al@bird.org
```

![](img/9639113aa446fb8976cb3d377aafdd_306_0.png)

## 第 10 章 测试 `Sendmail`

```
final      input: al@bird.org
final      returns: al@bird.org
mailer smtp, host bird.org., user al@bird.org
> /quit
```

`/parse`命令通过打印两条信息开始。第一条信息表示输入地址在整个过程中存储在变量`g`中。注释将输入地址称为“解析后的地址（cracked address）”。这意味着在地址存储到变量`g`之前，任何随地址的标准`RFC 822`字段已被移除。第二条消息告诉你地址正在作为信封收件地址进行处理。

`/parse`命令将地址作为交付地址处理，通过规则 3 (canonical) 和规则 0 (parse)。一旦为地址选择了`smtp`邮件传输器，规范化地址将通过规则 2（由`smtp`邮件传输器的`R`参数定义的信封规则`EnvToSMTP`），最后通过规则 4 (final)。这种广泛的处理正是第 8 章图 8.1 所示的规则流。`/parse`命令让你能够在不记住规则执行顺序的情况下，让地址通过这一完整过程。

`/parse`命令显示的最后一行是将用于该地址的邮件交付三元组。如果`/parse`认为向所选地址交付邮件将出错，它还会显示错误消息，如下所示：

```
final      returns: al@bird.org
al@bird.org... Transient parse error -- message queued
for future delivery
```

这些值通常成对使用，以创建以下四个设置：

- `HS`这对标志请求发送者地址处理。
- `HR`这对标志请求收件者地址处理。
- `ES`这对标志请求信封地址处理。
- `ER`这对标志请求信封回执地址处理。

我建议你遵循标准做法，始终成对设置标志。我推荐这样做有两个原因。首先，`Sendmail`是成对使用标志的。如果你不显式地为其中一个标志赋值，`Sendmail`将使用该标志已有的值。其次，标志是具有“粘性”的——当一个标志被设置后，它会一直保持设置状态，直到被显式重置。这意味着如果你一直在调整这些标志，你就必须跟踪这些标志的值。因此，在运行测试之前显式地设置这些值要简单得多。
