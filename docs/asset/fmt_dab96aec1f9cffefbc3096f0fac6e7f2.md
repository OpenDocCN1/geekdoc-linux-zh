
真的比

```
0 AliasFile=etc/aliases
```

更简单吗？

答案是否定的。一旦你理解了 `sendmail.cf` 命令的含义和语法，单个 m4 Sendmail 宏在读写上并没有比单个 `sendmail.cf` 命令更简单。然而，m4 宏配置文件比 `sendmail.cf` 文件短得多且更容易阅读，而且单个 m4 命令的功能通常比单个 `sendmail.cf` 命令多得多。m4 使从头开始编写配置成为可能。但你可能不需要这样做。也许 Sendmail 开发人员或你的 Linux 供应商提供的示例 `sendmail.cf` 配置仅需少小改动就能适用于你。在这种情况下，我为什么反复坚持让你用 m4 构建配置呢？

原因是“因为大家一直是这么做的”。每个人都期望 Sendmail 配置定义在 m4 宏配置文件中。当你的同事调试你的系统时，他们会在那里寻找更改。直接将配置放在 `sendmail.cf` 文件中，只会让那些必须调试的人对一个复杂的系统感到更加混乱。更糟糕的是将某些更改放在宏配置中，而另一些放在 `sendmail.cf` 中。那种方法注定失败。坚持使用 m4 吧。它可能简单，但比替代方案更好，这也是 Sendmail 配置的标准做法。

## 总结

`sendmail.cf` 是 Sendmail 启动时读取的文件，它为 Sendmail 提供以下内容：

- 本地信息
- 定义 Sendmail 的选项
- 规则选项

规则集用于处理不同类型的地址。

### 图 8.1 被 Sendmail 规则处理的地址

![](img/9639113aa446fb8976cb3d377f7aafdd_244_0.png)

图 8.1 所示以及上述列表描述的规则由 Sendmail 自动调用，但并不意味着它们一定存在于配置中。这些规则的两个很好的例子是规则 1（发送者）和规则 2（接收者）。默认情况下，这些规则是空的，因此在 Sendmail 8.11 的 `sendmail.cf` 文件中并没有定义它们。（我们将在第 9 章“特殊配置”中看到，如果需要的话，你可以为规则 1 和 2 定义你自己的重写规则。）这些规则在 `sendmail.cf` 文件中未定义并不会给 Sendmail 带来任何问题。它只是调用它们，并在未找到时继续执行下一个规则。

## 更多规则集

到此为止描述的规则仅由 Sendmail 直接调用。`sendmail.cf` 文件中定义了更多规则集。例如，由 `redhat.mc` 宏配置创建的 `sendmail.cf` 文件包含 47 个规则集。其他规则集提供了额外的地址处理。它们包括图 8.1 中标识为 S 和 R 的规则集，以及从 `sendmail.cf` 文件内部通过单个重写规则或 `H` 命令调用的规则集。规则集使用 `$name` 语法调用，其中 `name` 是标识被调用规则集的名称或数字。我们稍将在讨论重写规则时看到更多关于 `$name` 语法的内容。

表 8.1 列出了你在 `sendmail.cf` 文件的重写规则（Rewriting Rules）部分中找到的规则集。它通过名称（在适用时通过数字）标识每个规则集，并对该规则集的目的提供简短描述。规则集按照它们在“重写规则”部分出现的顺序列出。

| 名称 | 编号 | 目的 |
| --- | --- | --- |
| `canify` | 3 | 将地址放入标准的内部格式。 |
| `final` | 4 | 将地址转换为外部格式。 |
| `parse` | 0 | 为投递地址选择邮件处理器。 |
| `localaddr` | 5 | 处理本地地址。 |
| `Mailertable` | 90 | 将域名与 `mailertable` 进行匹配。 |
| `MasqHdr` | 93 | 伪装头部名称。 |
| `MasqEnv` | 94 | 伪装信封名称。 |
| `LookupDomain` | | 在访问数据库中查找域名。 |
| `LookupAddress` | | 在访问数据库中查找主机名。 |
| `ParseRecipient` | | 将接收者地址转换为中继所需的适当地址格式。 |
| `check_relay` | | 用于反垃圾邮件功能的检查中继检查。 |
| `check_mail` | | 用于反垃圾邮件功能检查发送者地址。 |
| `check_rcpt` | | 用于反垃圾邮件功能检查接收者地址。 |
| `trust_auth` | | 测试是否应该信任 `AUTH` 参数。 |
| `tls_client` | | 验证到客户端的 `TLS` 连接。 |
| `tls_server` | | 验证到服务器的 `TLS` 连接。 |

表 8.1 仅显示了在“重写规则”部分找到的部分规则集。还有几个规则集是这些规则集的子程序，或者被这些规则集调用以完成其任务。

## 基础规则集 223

- `canonify` 有一个名为 `Canonify2` 的子部分，也称为规则集 96，用于从 `DNS` 获取规范化主机名。
- `parse` 有两个名为 `Parse0` 和 `Parse1` 的子部分，以及一个由其调用以处理本地地址的子程序 `ParseLocal`（规则集 98）。
- `Mailertable` 处理器 `MailerToTriple`（也称为规则集 95）用于帮助将 `mailertable` 条目转换为邮件投递，它并使用 `CanonLocal` 将 `mailertable` 中的本地名称放入标准格式。
- `ParseRecipient` 使用 `Addr` 将地址放入标准格式，`Addr` 通过简单地调用 `Parse0` 和 `Canonify` 实现这一点。
- `check_relay`、`check_mail` 和 `check_rcpt` 的大部分工作由名为 `Basic_check_relay`、`Basic_check_mail` 和 `Basic_check_rcpt` 的子部分处理。相应，`Basic_check_rcpt` 在需要时调用 `RelayAuth` 来检查客户端身份验证。`SearchList` 是另一个被 `check_mail` 和 `check_rcpt` 用的例程，用于处理这些反垃圾邮件过滤器使用的内部语法。回想第 7 章中提到的 `(src)` 类；`SearchList` 就是所使用的。
- `tls_client` 和 `tls_server` 调用 `tls_connection` 来获取验证的连接。`tls` 使用 `turn max` 来决定使用的合适的加密位数。传输层安全将在第 12 章讨论。

这些-发送者规则：
- 规则 2（接收者）用于反垃圾邮件功能检查接收者地址。
- 规则 1（发送者）用于反垃圾邮件功能检查发送者地址。
- 规则 2（接收者）用于处理接收者地址。
- `localaddr`（规则集 5）处理本地地址。
- `check_relay` 用于反垃圾邮件功能检查中继。
- `check_mail` 用于反垃圾邮件功能检查发送者地址。
- `check_rcpt` 用于反垃圾邮件功能检查接收者地址。
- `trust_auth` 测试是否应该信任 `AUTH` 参数。
- `tls_client` 验证到客户端的 `TLS` 连接。
- `tls_server` 验证到服务器的 `TLS` 连接。

### 图 8.1 被 Sendmail 规则处理的地址

![](img/9639113aa446fb8976cb3d377f7aafdd_244_0.png)

图 8.1 所示以及上述列表描述的规则由 Sendmail 自动调用，但并不意味着它们一定存在于你的配置中。这些规则的两个很好的例子是规则 1（发送者）和规则 2（接收者）。

## 基础规则集 223

- `canonify` 有一个名为 `Canonify2` 的子部分，也称为规则集 96，用于从 `DNS` 获取规范化主机名。
- `parse` 有两个名为 `Parse0` 和 `Parse1` 的子部分，以及一个由其调用以处理本地地址的子程序 `ParseLocal`（规则集 98）。
- `Mailertable` 处理器 `MailerToTriple`（也称为规则集 95）用于帮助将 `mailertable` 条目转换为邮件投递，它使用 `CanonLocal` 将 `mailertable` 中的本地名称放入标准格式。
- `ParseRecipient` 使用 `Addr` 将地址放入标准格式，`Addr` 通过简单地调用 `Parse0` 和 `Canonify` 实现这一点。
- `check_relay`、`check_mail` 和 `check_rcpt` 的大部分工作由名为 `Basic_check_relay`、`Basic_check_mail` 和 `Basic_check_rcpt` 的子部分处理。相应，`Basic_check_rcpt` 在需要时调用 `RelayAuth` 来检查客户端身份验证。`SearchList` 是另一个被 `check_mail` 和 `check_rcpt` 用的例程，用于处理这些反垃圾邮件过滤器使用的内部语法。回想第 7 章中提到的 `(src)` 类；`SearchList` 就是所使用的。
- `tls_client` 和 `tls_server` 调用 `tls_connection` 来获取验证的连接。`tls` 使用 `turn max` 来决定使用的合适的加密位数。传输层安全将在第 12 章讨论。

规则集（`ruleset`）中的每一有效行都是一个 `R` 命令。`R` 命令的语法复杂且难以阅读。本章的剩余部分将解释 `R` 命令的功能和语法。

# 重写规则

规则集由单个重写规则组成，这些规则用于从用户邮件程序中解析电子邮件地址，并将其重写为邮件递送程序所需的格式。每个重写规则都由一个 `R` 命令定义。第 7 节中引入的 `R` 命令语法如下：

```
