

# 第 8 章 理解重写规则

规则集（ruleset）中的每一有效行都是一个 R 命令。R 命令的语法复杂且难以阅读。解释 R 命令的功能和语法将占据本章的剩余部分。

## 重写规则

规则集由单个重写规则组成，这些规则从用户邮件程序中解析电子邮件地址，并将其重写为邮件投递程序所需的格式。每个重写规则由一个 R 命令定义。在第 7 章中引入的 R 命令语法如下：

```
Rpattern template comment
```
R 命令中的字段由制表符分隔。系统会忽略注释字段，但良好的注释对于理解发生的情况至关重要。模式（pattern）和模板（template）字段是该命令的核心。

## 模式匹配

重写规则将输入与模式匹配，如果找到匹配项，则使用模板定义的规则将地址重写为新格式。重写规则可能会多次处理同一个地址，在重写之后，地址将再次与模式进行比较。如果仍然匹配，则将再次重写。模式匹配和重写的循环一直持续，直到地址不再匹配模式为止。

模式使用变量、类、字面量和特殊符号定义。变量、类和字面量提供了与输入比较的值，而符号定义了匹配模式时使用的规则。表 8.3 显示了用于模式匹配的符号。

表 8.3 模式匹配符号

| 符号 | 含义 |
| --- | --- |
| $@ | 精确匹配零个 token。 |
| $* | 匹配零或多个 token。 |
| $- | 精确匹配一个 token。 |
| $+$ | 匹配一个或多个 token。 |
| $x | 匹配宏变量 x 中的所有 token。 |
| $x | 匹配类变量 x 中的任何 token。 |
| $\~x$ | 匹配不在类变量 x 中的任何 token。 |

所有符号都匹配 token 的数量。token（标记符）是由运算符分隔的字符字符串。运算符包括右括号 `)` 和左括号 `(`、右角括号 `>` 和左角括号 `<`、逗号 `,`、分号 `;`、反斜杠 `\`、引号 `"`、回车符 (CR) 和换行符 (LF)，以及由 OperatorChars 选项定义的任何字符。对 `sendmail.cf` 进行 `grep OperatorChars` 操作显示，额外的运算符字符是 `; % @ ! ^ [ ] 和 ,`。

```bash
grep 'OperatorChars' /etc/sendmail.cf
0 OperatorChars=;%@!^]+
```

在解析地址时，运算符也算 token。假设以下地址：
sara@hawk.foobirds.org
此邮件地址包含七个 token：sara、@、hawk、foobirds 以及三个。其中，`.`（点）和 `@` 是运算符。另外四个 token 是字符串。该地址将匹配符号 `$`，因为它包含多个 token，但它不会匹配表 8.3 中的 `$`，因为它没有精确匹配一个 token。

表 8.3 中的符号在与字面量和变量结合使用时特别有用，可以创建更复杂的模式——例如：
$- @$-foobirds.org
示例地址 sara@hawk.foobirds.org 匹配该模式，是因为：
- 它在字面量 `@` 之前恰好有一个 token，符合 `$-` 的要求。
- 它有一个 `@` 匹配模式中的字面量 `@`。
- 它在字面量 `@` 之后、字面量 `.foobirds.org` 之前恰好有一个 token，符合第二个 `$` 符号的要求。
- 它拥有字符串 `.foobirds.org`，匹配模式中的字面量 `.foobirds.org`。
sara@hawk.foobirds.org 此模式，但许多其他地址并不匹配。例如，sara.hanson@hawk.foobirds.org 不匹配，因为它在字面量 `@` 之前有三个 token：sara、. 和 Hanson。因此，它未能满足第一个 `$-` 指定的精确一个 token 的要求。mandy@sooty.terms.foobirds.org 不匹配该模式，因为它在字面量 `@` 之后、字面量 `.foobirds.org` 之前有三个 token（sooty、.. 和 terms）。

字面量是模式匹配中非常重要的部分，以至于 Sendmail 在地址中插入字面量（如角括号 `< >`），使其更容易解析。列表 8.2 显示了这一点。

+ 列表 8.2 字面量的内部使用

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3 craig.hunt@ibis.foobirds.org
canonify input: craig.hunt@ibis foobirds.org >
canonify2 input: craig.hunt < ibis foobirds.org >
canonify2 returns: craig.hunt < ibis foobirds.org >
canonify returns: craig.hunt < ibis foobirds.org >
> ^
```

> 注意：在 DNS 中，结尾的点是域根。Sendmail 在内部使用它来表示名称已通过 DNS 成功处理。

sendmail.cf 文件中约 75% 的重写规则是使用角括号作为模式字段一部分的插入 token。列表 8.1 中来自 EnvTol 的单个规则演示了这一点。该规则包含此模式：

```
$ + $ $ >
```

该模式表示匹配任何在字面值 `<` 之前有一个或多个 token (`$+$`)，且在字面值之后、字面值 `>` 之前有零或多个 token 的地址。`Craig.hunt@ibis.foobirds.org>` 地址匹配此模式。它在 `<@` 之前有三个 token（craig、.. 和 hunt），在字面量 `<@` 和 `>` 之间有六个字面量 token（ibis、..、foobirds、.、org 和 .）。字面量是模式的重要部分，但它们缺乏创建适用于任何系统的通用配置所需的灵活性。这就是变量派上用场的地方。在第一个示例中，我们使用了模式：

```
$- @ $- .foobirds
```

该模式的问题是它只适用于域名名为 `foobirds.org` 的地址。字面量 `.foobirds` 在我们的站点运行良好，但如果我们需要为朋友们设置此配置，它就没什么帮助。类变量也可以用于模式匹配。事实上，模式匹配是类值唯一有用的地方。我们可以通过简单的命令演示这一点：

```bash
# SClassTest
R$ @ $w          Found it
R$+ @ ~w         Not in class w
R$               Wrong format
```
S 命令启动规则集并命名为 ClassTest。以下规则等于我们在第 4 章中创建的模式：

```bash
grep 'OperatorChars' /etc/sendmail.cf
0 OperatorChars=;%@!^]+
```

8.3 模式匹配符号（继续）

| 符号 | 含义 |
| --- | --- |
| $x | 匹配类变量 x 中的任何 token。 |
| $\~x$ | 匹配不在类变量 x 中的任何 token。 |

所有符号都匹配 token 的数量。token 是由运算符分隔的字符字符串。运算符包括右括号 `)` 和左括号 `(`、右角括号 `>` 和左角括号 `<`、逗号 `,`、分号 `;`、反斜杠 `\`、引号 `"`、回车符 (CR) 和换行符 (LF)，以及由 OperatorChars 选项定义的任何字符。对 `sendmail.cf` 进行 `grep OperatorChars` 操作显示，额外的运算符字符是 `; % @ ! ^ [ ] 和 ,`。

```bash
grep 'OperatorChars' /etc/sendmail.cf
0 OperatorChars=;%@!^
```

解析地址时，运算符也算 token。假设以下地址：
sara@hawk.foobirds.org
此邮件地址包含七个 token：sara、@、hawk、foobirds 以及三个。其中，`.`（点）和 `@` 是运算符。另外四个 token 是字符串。该地址将匹配符号 `$`，因为它包含多个 token，但它不会匹配表 8.3 中的 `$`，因为它没有精确匹配一个 token。

表 8.3 中的符号在与字面量和变量结合使用时特别有用，可以创建更复杂的模式——例如：
$- @$-foobirds.org
示例地址 sara@hawk.foobirds.org 匹配该模式，是因为：
- 它在字面量 `@` 之前恰好有一个 token，符合 `$-` 的要求。
- 它有一个 `@` 匹配模式中的字面量 `@`。
- 它在字面量 `@` 之后、字面量 `.foobirds.org` 之前恰好有一个 token，符合第二个 `$` 符号的要求。
- 它拥有字符串 `.foobirds.org`，匹配模式中的字面量 `.foobirds.org`。
sara@hawk.foobirds.org 此模式，但许多其他地址并不匹配。例如，sara.hanson@hawk.foobirds.org 不匹配，因为它在字面量 `@` 之前有三个 token：sara、. 和 Hanson。因此，它未能满足第一个 `$-` 指定的精确一个 token 的要求。mandy@sooty.terms.foobirds.org 不匹配该模式，因为它在字面量 `@` 之后、字面量 `.foobirds.org` 之前有三个 token（sooty、.. 和 terms）。字面量是模式匹配中非常重要的部分，以至于 Sendmail 在地址中插入字面量（如角括号 `< >`），使其更容易解析。列表 8.2 显示了这一点。

+ 列表 8.2 字面量的内部使用

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3 craig.hunt@ibis.foobirds.org
canonify input: craig.hunt@ibis foobirds.org >
canonify2 input: craig.hunt < ibis foobirds.org >
canonify2 returns: craig.hunt < ibis foobirds.org >
canonify returns: craig.hunt < ibis foobirds.org >
> ^
```

> 注意：在 DNS 中，结尾的点是域根。Sendmail 在内部使用它来表示名称已通过 DNS 成功处理。

sendmail.cf 文件中约 75% 的重写规则是使用角括号作为模式字段一部分的插入 token。列表 8.1 中来自 EnvTol 的单个规则演示了这一点。该规则包含此模式：

```
$ + $ $ >
```

该模式表示匹配任何在字面值 `<` 之前有一个或多个 token (`$+$`)，且在字面值之后、字面值 `>` 之前有零或多个 token 的地址。`Craig.hunt@ibis.foobirds.org>` 地址匹配此模式。它在 `<@` 之前有三个 token（craig、.. 和 hunt），在字面量 `<@` 和 `>` 之间有六个字面量 token（ibis、..、foobirds、.、org 和 .）。字面量是模式的重要部分，但它们缺乏创建适用于任何系统的通用配置所需的灵活性。这就是变量派上用场的地方。在第一个示例中，我们使用了模式：

```
$- @ $- .foobirds
```

该模式的问题是它只适用于域名名为 `foobirds.org` 的地址。字面量 `.foobirds` 在我们的站点运行良好，但如果我们需要为朋友们设置此配置，它就没什么帮助。类变量也可以用于模式匹配。事实上，模式匹配是类值唯一有用的地方。我们可以通过简单的命令演示这一点：

```bash
# SClassTest
R$ @ $w          Found it
R$+ @ ~w         Not in class w
R$               Wrong format
```
S 命令启动规则集并命名为 ClassTest。以下规则等于我们在第 4 章中创建的模式：

```bash
grep 'OperatorChars' /etc/sendmail.cf
0 OperatorChars=;%@!^]+
```

