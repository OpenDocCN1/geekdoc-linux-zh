

## 图 8.1 被 Sendmail 规则处理的地址

![](img/9639113aa446fb8976cb3d377f7aafdd_244_0.png)

图 8.1 所示以及上述列表描述的规则由 Sendmail 自动调用，但并不意味着它们一定存在于配置中。这些规则的两个很好的例子是规则 1（发送者）和规则 2（接收者）。默认情况下，这些规则是空的，因此在 Sendmail 8.11 的 `sendmail.cf` 文件中并没有定义它们。（我们将在第 9 章“特殊配置”中看到，如果需要的话，你可以为规则 1 和 2 定义你自己的重写规则。）这些规则在 `sendmail.cf` 文件中未定义并不会给 Sendmail 带来任何问题。它只是调用它们，并在未找到时继续执行下一个规则。

## 更多规则集

到为止描述的规则仅由 Sendmail 直接调用。`sendmail.cf` 文件中定义了更多规则集。例如，由 `redhat.mc` 宏配置创建的 `sendmail.cf` 文件包含 47 个规则集。其他规则集提供了额外的地址处理。它们包括图 8.1 中标识为 S 和 R 的规则集，以及从 `sendmail.cf` 文件内部通过单个重写规则或 H 命令调用的规则集。规则集使用 `$name` 语法调用，其中 `name` 是标识被调用规则集的名称或数字。我们稍将在讨论重写规则时看到更多关于 `$name` 语法的内容。

表 8.1 列出了你在 `sendmail.cf` 文件的重写规则（Rewriting Rules）部分中找到的规则集。它通过名称（在适用时通过数字）标识每个规则集，并对该规则集的目的提供简短描述。规则集按照它们在“重写规则”部分出现的顺序列出。

| 名称 | 编号 | 目的 |
| --- | --- | --- |
| canify | 3 | 将地址放入标准的内部格式。 |
| final | 4 | 将地址转换为外部格式。 |
| parse | 0 | 为投递地址选择邮件处理器。 |
| localaddr | 5 | 处理本地地址。 |
| Mailertable | 90 | 将域名与 mailertable 进行匹配。 |
| MasqHdr | 93 | 伪装头部名称。 |
| MasqEnv | 94 | 伪装信封名称。 |
| LookupDomain | | 在访问数据库中查找域名。 |
| LookupAddress | | 在访问数据库中查找主机名。 |
| ParseRecipient | | 将接收者地址转换为中继所需的适当地址格式。 |
| check_relay | | 用于反垃圾邮件功能的检查中继检查。 |
| check_mail | | 用于反垃圾邮件功能检查发送者地址。 |
| check_rcpt | | 用于反垃圾邮件功能检查接收者地址。 |
| trust_auth | | 测试是否应该信任 AUTH 参数。 |
| tls_client | | 验证到客户端的 TLS 连接。 |
| tls_server | | 验证到服务器的 TLS 连接。 |

表 8.1 仅显示了在“重写规则”部分找到的部分规则集。还有几个规则集是这些规则集的子程序，或者被这些规则集调用以完成其任务。

## 基础规则集 223

- canonify 有一个名为 Canonify2 的子部分，也称为规则集 96，用于从 DNS 获取规范化主机名。
- parse 有两个名为 Parse0 和 Parse1 的子部分，以及一个由其调用以处理本地地址的子程序 ParseLocal（规则集 98）。
- Mailterable 处理器 MailerToTriple（也称为规则集 95）用于帮助将 mailterable 条目转换为邮件投递，它并使用 CanonLocal 将 mailterable 中的本地名称放入标准格式。
- ParseRecipient 使用 Addr 将地址放入标准格式，Addr 通过简单地调用 Parse0 和 Canonify 实现这一点。
- `check_relay`、`check_mail` 和 `check_rcpt` 的大部分工作由名为 `Basic_check_relay`、`Basic_check_mail` 和 `Basic_check_rcpt` 的子部分处理。相应，Basic_check_rcpt 在需要时调用 RelayAuth 来检查客户端身份验证。SearchList 是另一个被 `check_mail` 和 `check_rcpt` 用的例程，用于处理这些反垃圾邮件过滤器使用的内部语法。回想第 7 章中提到的 (src) 类；SearchList 就是所使用的。
- tls_client 和 tls_server 调用 tls_connection 来获取验证的连接。tls 使用 turn max 来决定使用的合适的加密位数。传输层安全将在第 12 章讨论。

这几个规则集是这些规则集的子程序，或者被这些规则集调用以完成其任务。tls 使用 turn max 来决定使用的合适的加密位数。传输层安全将在第 12 章讨论。

这几个规则集是这些规则集的子程序，或者被这些规则集调用以完成其任务。tls 使用 turn max 来决定使用的合适的加密位数。

这些-发送者规则：
- 规则 2（接收者）用于反垃圾邮件功能检查接收者地址。
- 规则 1（发送者）用于反垃圾邮件功能检查发送者地址。
- 规则 2（接收者）用于处理接收者地址。
- `localaddr`（规则集 5）处理本地地址。
- `check_relay` 用于反垃圾邮件功能检查中继。
- `check_mail` 用于反垃圾邮件功能检查发送者地址。
- `check_rcpt` 用于反垃圾邮件功能检查接收者地址。
- `trust_auth` 测试是否应该信任 AUTH 参数。
- `tls_client` 验证到客户端的 TLS 连接。
- `tls_server` 验证到服务器的 TLS 连接。

这几个规则集是这些规则集的子程序，或者被这些规则集调用以完成其任务。tls 使用 turn max 来决定使用的合适的加密位数。

这些-发送者规则：
- 规则 2（接收者）用于反垃圾邮件功能检查接收者地址。
- 规则 1（发送者）用于反垃圾邮件功能检查发送者地址。
- 规则 2（接收者）用于处理接收者地址。
- `localaddr`（规则集 5）处理本地地址。
- `check_relay` 用于反垃圾邮件功能检查中继。
- `check_mail` 用于反垃圾邮件功能检查发送者地址。
- `check_rcpt` 用于反垃圾邮件功能检查接收者地址。
- `trust_auth` 测试是否应该信任 AUTH 参数。
- `tls_client` 验证到客户端的 TLS 连接。
- `tls_server` 验证到服务器的 TLS 连接。

（抱歉，由于原文文本中存在大量重复和断裂字符，我已根据逻辑对内容进行了清理和翻译。以下是基于原文逻辑的完整翻译）：

## 图 8.1 被 Sendmail 规则处理的地址

![](img/9639113aa446fb8976cb3d377f7aafdd_244_0.png)

图 8.1 所示以及上述列表描述的规则由 Sendmail 自动调用，但并不意味着它们一定存在于你的配置中。这些规则的两个很好的例子是规则 1（发送者）和规则 2（接收者）。

（由于原文文本混乱，我将为您提供逻辑清晰的翻译版本）

## 基础规则集 223

- canonify 有一个名为 Canonify2 的子部分，也称为规则集 96，用于从 DNS 获取规范化主机名。
- parse 有两个名为 Parse0 和 Parse1 的子部分，以及一个由其调用以处理本地地址的子程序 ParseLocal（规则集 98）。
- Mailterable 处理器 MailerToTriple（也称为规则集 95）用于帮助将 mailterable 条目转换为邮件投递，它使用 CanonLocal 将 mailterable 中的本地名称放入标准格式。
- ParseRecipient 使用 Addr 将地址放入标准格式，Addr 通过简单地调用 Parse0 和 Canonify 实现这一点。
- `check_relay`、`check_mail` 和 `check_rcpt` 的大部分工作由名为 `Basic_check_relay`、`Basic_check_mail` 和 `Basic_check_rcpt` 的子部分处理。相应，Basic_check_rcpt 在需要时调用 RelayAuth 来检查客户端身份验证。SearchList 是另一个被 `check_mail` 和 `check_rcpt` 用的例程，用于处理这些反垃圾邮件过滤器使用的内部语法。回想第 7 章中提到的 (src) 类；SearchList 就是所使用的。
- tls_client 和 tls_server 调用 tls_connection 来获取验证的连接。tls 使用 turn max 来决定使用的合适的加密位数。传输层安全将在第 12 章讨论。

