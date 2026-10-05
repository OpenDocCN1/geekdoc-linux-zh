
列表 2.1 中的第二个命令略有不同。它评估投递地址 `craig`。由于该地址没有主机部分——即没有紧跟主机或域名的 @ 符号（@）——因此该地址被假设为本地系统上的一个用户名。Sendmail 会检查该用户名在本地主机上是可投递的。对于本地邮件投递，主机值作为投递三元组的一部分提供，因为不涉及远程主机。本地投递的内部传输器是本地的，在列表 2.1 中，传递给本地传输器的用户值是 `craig`。

## 格式化电子邮件地址

一旦 Sendmail 选择了传输器（mailer），它必须为该传输器正确地格式化邮件。Sendmail 使用称为“重写规则”（rewrite rules）的命令将从 MUA（邮件用户代理）接收到的电子邮件地址转换为 MTA（邮件传输代理）所需的格式。Sendmail 配置文件的大部分由重写规则组成。这些是定义了模式和转换的单独行。如果输入地址匹配规则中定义的模式，则使用该规则中定义的转换进行重写。

规则被分组为规则集（rulesets），内部通过名称或数字进行标识。规则集可以像函数一样从单个重写规则调用以处理复杂的地址。Sendmail 为某些规则集分配了特殊角色，用于处理不同类型的地址。例如，投递地址由 `canonify` 规则集（也称为规则集 3）处理，该规则集处理所有地址以符合 Sendmail 预期的格式；由 `parse` 规则集（也称为规则集 0）处理，它创建了投递管道。

你可以通过带有 `-bt` 选项的 `sendmail` 命令来观察规则集的运行——`-bt` 在测试模式下替换投递。一旦进入测试模式，它将接受一个规则集列表和一个要通过这些规则集处理的地址。在列表 2.2 中，带有 `-bt` 参数运行 `sendmail` 命令，并要求通过 `canonify` 和 `parse` 处理 `ed@xy.com`。

## 列表 2.2 查看重写规则的运行

```
[craig]$ sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter<ruleset>,parse ed@xy.com
canonify       input: ed < @xyz com
canonify2      input: ed < @xyz com >
Canonify2     returns: ed < @xyz com>
canonify      returns: ed < @xyz com>
parse         input: ed < @xyz com>
Parse0        input: ed < @xyz com >
```

## Sendmail 的角色

```
Parse0 returns: ed < xyz . com>
ParseLocal input: ed @ xyz . com
ParseLocal returns: ed @ xyz . com
Parse1 input: ed @ xyz . com
Mailertable input: < xyz . ed @ xyz . com >
Mailertable input: xyz . com < ed @ xyz . com >
Mailertable returns: ed @ xyz . com>
Mailertable returns: ed @ xyz . com >
MailerToTriple input: < > ed @ xyz . com >
MailerToTriple returns: ed @ xyz . com >
Parse1 returns: # $ esmtp $xyz , com$: ed < @ xyz . com >
parse returns: # $ esmtp $xyz , com$: < @ xyz . com >
> ^D
```

**sendmail -bt** 显示的比 `-dev` 更加详细。列表 2.2 显示，在 `canonify` 规则返回值之前返回了 `Canonify` 规则。这表明规则集可以被其他规则集中的规则调用。这就是列表 2.2 中发生的情况。总共有八个规则集处理了这个投递地址。结果就是投递路径。但注意，在三元组中，标签被符号 `$` 替换，主机标签被 `#` 替换，标签被 `:` 替换。你将在第 8 章看到这一点，符号在 Sendmail 重写规则中被大量使用。

投递地址只是 Sendmail 处理的地址类型之一。Sendmail 还处理发件地址和收件地址。发件地址是启动邮件的用户或进程名称。收件地址是邮件提供的收件人列表。收件人与投递地址的区别在于，收件人列表中每次只使用一个地址作为投递地址，但整个收件人列表都会被处理并包含在每条出站邮件中。

所有地址都通过重写规则进行处理，将输入地址转换为与传输邮件的传输器兼容的格式。重写取决于哪个传输器将处理邮件，首先处理投递地址以确定将使用哪个传输器。一旦选择了传输器，其他地址就可以通过标准规则集以及特定传输器的规则集进行处理。

处理和重写电子邮件地址是 Sendmail 功能的核心部分。这是一个大且复杂的话题。第 8 章详细介绍了该主题。

![](img/b8082498451dba2bf0cf2907c85c4c83_65_0.png)

## 格式化头部

除了修改邮件地址以符合邮件投递程序外，Sendmail 还确保邮件投递程序所需的所有头部都已提供并正确格式化。如上所述，传输器定义中的标志标识了该传输器所需的头部。

Sendmail 配置文件包含了定义各种消息头部正确格式的头部信息。每个模板都有一个关联的标志。如果在传输器定义中找到匹配的标志，Sendmail 就知道该传输器需要该特定头部并添加它。

（注：原文中存在大量重复段落，译文已按要求去重处理）
