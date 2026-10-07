

# Mailer 三元变体

Mailer 三元语法有几种变体，这些变体也用于某些规则的模板中。其中两种变体仅使用“mailer”组件。

$OK 表示输入地址通过了安全测试。例如，该地址允许中继邮件。

$discard 表示输入地址未通过某些安全测试，邮件信息应该被丢弃。

注意：OK、discard 以及 error（在第二部分中讨论）这者都不是像 real mailers 那样在命令（Commands）中声明的。但 Sendmail 文档将它们统称为“mailers”，我们也是如此。

$$OK 和 $$discard 用于垃圾邮件控制和安全。你将在后面的章节中看到更多它们。$$discard 会静默丢弃邮件，且不会向发送者返回错误信息。$$error mailer 是另一种处理无法投递邮件的 mailer，与 $$discard 不同，它会向发送者返回错误信息。与 $$error 使用的模板语法比 $$OK 或 $$discard 的语法更复杂。该语法如下所示：

```
$error $$dsn-code $:message
```

为了正确处理错误信息，mailer 必须是 $$error。$:message 字段包含你想要发送的错误信息文本。$$dsn-code 字段可选可选。如果提供，它将出现在消息之前，并且必须包含 RFC 1893（“邮件系统状态码”）定义的有效 DSN 错误代码或有效的 Sendmail 关键字。表 8.5 列出了有效的 Sendmail 错误代码关键字及其含义。

# 表 8.5 Sendmail 错误代码关键字

| 关键字 | 含义 |
| --- | --- |
| config | 检测到内部配置错误或路由循环。 |
| nohost | 者或接收者地址的主机部分无效。 |
| nouser | 者或接收者地址的用户无效。 |
| protocol | 网络传输失败。 |

# 表 8.5 Sendmail 错误代码关键字（续）

| 关键字 | 含义 |
|---|--|
| tempfail | 检测到临时失败。 |
| unavailable | 投递资源不可。 |
| usage | 投递地址语法错误。 |

使用错误代码的错误信息看起来如下：

```
$R<$+> #error S $:user address required
```

这种格式可以工作，但不是推荐的格式。事实上，随 Sendmail 8.11.0 交付的 sendmail.cf 文件中的单个错误消息使用了关键字格式。首选格式是使用 DSN 代码代替键。这些代码在互联网标准中有明确定义，并被所有 mailer 理解。DSN 代码由三个用点分隔的分组件组成：

class 为状态提供宽泛的分类。RFC 中为 class 定义了三个值：2 表示成功，4 表示临时失败，5 表示永久失败。

subject 将错误消息归类为八大类别之一：

- 0 (Undefined) 无法确定特定类别。 |
- 1 (Addressing) 地址遇到问题。 |
- 2 (Mailbox) 投递信箱遇到问题。 |
- 3 (Mail system) 目标投递系统出现问题。 |
- 4 (Network) 网络基础设施出现问题。 |
- 5 (Protocol) 遇到协议问题。 |
- 6 (Content) 消息内容导致翻译错误。 |
- 7 (Security) 报告了安全问题。 |

detail 提供特定错误的详细信息。detail 值仅在 subject 代码的上下文中才有意义。例如 x.1.1 表示目标用户错误，x.1.2 表示目标主机错误，而 x.2.1 表示信箱已禁用，x.2.2 表示信箱已满。detail 代码非常多，无法在此列出。完整列表请参见 RFC 1893。

使用错误代码的错误消息如下。如果将上述错误消息重写为首选的 DSN 格式，则是：

```
RC@$+> $error@5.1.1:user address required
```

当匹配模式时返回 DSN 代码 5.1.1 和消息“user address required”。DSN 代码的 class 字段为 5 表示永久失败；subject 字段为 1 表示地址失败；detail 字段为 1 表示给定 subject 值，用户地址错误。错误代码和语法可能会令人困惑。

# 总结

Sendmail 的大部分工作由重写规则（rewrite rules）完成。相应，重写规则构成了 sendmail.cf 文件的主体。重写规则出现在 sendmail.cf 的 Rewriting Rules 和 Mailer 部分。重写规则通过字面量、变量和特殊符号组成的模式匹配地址。如果地址匹配模式，则使用模板通过规则进行重写。重写规则的语法和用法复杂，当详细检查重写规则时可以消除这种复杂性。相关的重写规则在规则集（rulesets）中分组。每个规则集的目的在本章中进行了描述。不需要知道每个规则的功能就能知道它询问 DNS 规范主机名。当需要理解单个规则的功能时，规则提供的注释可能提供你需要的信息。最后，如果需要对特定规则进行详细理解，本章对重写语法的描述将提供你所需的信息。通常，不需要读取 sendmail.cf 中已存在的单个规则。理解规则集的目的是为了理解配置的机制。理解重写语法的真实目的是编写你自己的规则。你很少需要这样做，但它是高级配置的一部分，正如我们在第9 章和后续章节中看到的。

# 特殊 m4 配置

百分之十的选项处理大部分配置。普通的 Sendmail 服务器可以使用厂商提供的配置运行，但并非每个服务器都是普通的。某些需要特殊选项来处理特殊需求。m4 提供了大量的选项来满足任何需求。附录 A“m4 命令参考”列出了所有选项。本章通过将这些选项组织成主题来帮助你理解它们。本章像是一个清单，因为它包含了一些不相关的主题。我最初计划将本章命名为“高级 m4 配置”，但事实是这些配置选项并不比其他的更高级。书中后面用于垃圾邮件控制和安全的选项与本章讨论的任何选项一样复杂。本章主题之间的真实关系是，它们是在特殊情况下才需要的配置选项。你可能会发现你不需要使用大部分，但你想了解它们。在本章中，你将学习这些选项的优缺点，以便判断哪些适合你。连接本章许多主题的一个共同点是它们与你企业的特殊需求。特定于你的网络或域的 m4 配置命令逻辑上放置在 DOMAIN 文件中。本章大量使用了 DOMAIN 文件。

# 使用 DOMAIN 文件

在第 5 章结束时，redhat.mc 文件被重写以利用 Sendmail m4 配置目录固有的结构。5.6 中，大型 redhat.mc 文件被分为三个文件：名为 redhat11.mc 的宏控制文件、名为 redhat7.0.m4 的 OTYPE 文件以及名为 foobirds.m4 的 DOMAIN 文件。传统上，宏控制文件选择组件，OTYPE 文件处理特定系统的值，而 DOMAIN 文件持有特定于你的网络或域的所有配置选项。在本章的前几节中，我们通过修改示例 9.1 所示的 foobirds.m4 文件遵循这些文件的传统用法。

## 9.1 示例 DOMAIN 文件

```
 # ../../foobirds.m4
VERSIONID(`Settings for the foobirds.org domain`)
define(`CONFORWARD_PATH`,
  $/forward.w+h$/forward+$h:/z$/forward.w:/z;
  forward`)
define(`CONFUSER_DB_SPEC`, `/etc/mail/userdb.db`)
FEATURE(`always_add_db`)
FEATURE(`access_db`)
FEATURE(`blacklist_recipients`)
FEATURE(`redirect`)
FEATURE(`use_cw_file`)
EXPOSED_USER(`root`)
# [root] m4 ../m4.cf redhat11.mc > plain.cf
# [root] cp ../domain/foobirds.m4 ../domain/old-foobirds.m4
```

此文件中的所有命令在第 5 章中都有解释，大部分情况下这些现有命令与本章涵盖的主题没有关系。我们处理 redhat11.mc，它是创建基准 sendmail.cf 文件的宏控制文件，我们可以以此比较更改。示例 9.1 最后，原始的 DOMAIN 文件被复制到 foobirds.m4。这提供了一个备份文件，以防我们不喜欢在接下来的几节中做的更改，并提供了一个用于比较更改的原始文件。原始文件将是测试的重要部分，帮助我们确定每个配置命令的影响。

