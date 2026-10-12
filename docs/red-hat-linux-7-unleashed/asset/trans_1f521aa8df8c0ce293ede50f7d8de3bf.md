

要安装新版本的 `sendmail` 可执行文件，首先使用以下命令停止当前运行的守护进程：

```
[root@gonzo src]# /etc/rc.d/init.d/sendmail stop
```

然后输入以下命令：

```
[root@gonzo src]# ./Build install
```

当所有配置就绪后，你可以使用以下命令重启新的守护进程：

```
[root@gonzo src]# /etc/rc.d/init.d/sendmail restart
```

## sendmail.cf：配置文件

随着 V.8 版本的出现，`sendmail` 提供了一种快速简便的方法来自动为你创建 `sendmail.cf` 文件。事实上，强烈建议*不要*手动创建或修改任何 `sendmail.cf` 文件。如果你对 `sendmail.cf` 文件的细节不感兴趣，可以安全地跳过本节。（我将在下一节讨论配置 `sendmail` 的简便方法。）

`sendmail.cf` 文件提供了 `sendmail` 的“大脑”，由于其重要性，本节将相当详细地介绍它。不要担心你第一次阅读时不能完全理解本节内容。重新阅读并有机会操作自己的配置文件后，你会更清楚其中的含义。

`sendmail` 的强大之处在于其灵活性，这源于其配置文件 `sendmail.cf`。`sendmail.cf` 语句组成了一种晦涩的编程语言，乍一看可能让人缺乏信心（但你第一次看到 C 语言代码时可能也是如此）。然而，学习 `sendmail.cf` 语言并不难，除非你打算从头编写一个 `sendmail.cf`——这本来就是个坏主意——否则你不需要学习那些细枝末节的细节。

### 配置文件的一般形式

配置文件的每一行都以一个单字符命令开头，该命令指示该行的功能和语法。以 `#` 开头的行是注释，空行会被忽略。以空格或制表符开头的行是前续行的延续，但通常应避免使用延续行。

表 10.1 展示了命令字符及其功能，以及它们的使用示例。该表格分为三个部分，对应配置文件的三个主要功能，这些功能将在本章稍后的“配置文件的功能描述”部分中详细讲解。

#### 表 10.1 *sendmail.cf* 命令字符

| 命令字符 | 命令语法及示例 | 功能 |
|---|---|---|
| `#` | `#` 注释将被忽略 | 注释行。请始终使用大量注释。 |
| | `# Standard RFC822 parsing` | |
| `D` | `Dx string` | 定义宏 `x` 的字符串值为 `string`。 |
| | `DM mailhub.gonz o.gov` | |
| | `D({MacroName})value` | 定义长宏 `{MacroName}` 的值为 `value`，随后使用 `\$({MacroName})` 引用。 |
| `C` | `D(Relay)mailhub.gonz o.gov` | |
| | `CX word1, word2, and so on` | 将类 `X` 定义为 `word1`、`word2` 等。 |
| `F` | `CWlocalhost myusername` | |
| | `FX/path/to/a/file` | 通过读取文件来定义类 `X`。 |
| `H` | `Fw/etc/mail/host_aliases` | |
| | `H?mailerflag?name::template` | 定义邮件头部。 |
| | `H?F?From: $q` | |
| `O` | `OX option arguments` | 设置选项 `X`。大多数命令行选项都可以在 *sendmail.cf* 中设置。 |
| | `OL9 # sets the log level to 9.` | |
| `P` | `Pclass=nn` | 基于邮件类别设置邮件投递优先级。 |
| | `Pjunk=100` | |
| `V` | `Vn` | 告知 V.8 版 *sendmail* 配置文件的版本级别。 |
| | `V3` | |
| `K` | `Knane class arguments` | 定义键文件（数据库映射）。 |
| `M` | `Kuucphosts hash /etc/mail/uucphosts` | |
| | `Mname,field_1=value_1, ...,` | 定义邮件器。 |
| | `Mprog,P=/bin/sh,F=1sD, @A@sh -c $u` | |
| `S` | `Sm` | 开始一个新的规则集。 |
| | `S22` | |
| `R` | `Rlhs rhs comment` | 定义匹配/重写规则。 |
| | `R+ S:>S22 call ruleset 22` | |

### 配置文件的功能描述

配置文件执行三项任务。首先，它通过告知哪些选项需要设置以及所使用的文件和数据库的位置，为 `sendmail` 设置环境。

其次，配置文件定义了邮件器（投递代理或 MTA）的特征，`sendmail` 在决定信件的路由位置后使用这些邮件器。所有配置文件都必须定义本地和程序邮件器以处理向本地主机用户的投递，大多数文件还定义了一个或多个 SMTP 邮件器，而必须处理 UUCP 邮件的网站则定义 UUCP 邮件器。

第三，配置文件指定了重写发件人和收件人地址并选择邮件器的规则集。所有规则集都是用户定义的，但其中一些对 `sendmail` 有特殊含义。例如，规则集 0 用于选择邮件器。规则集 0、1、2、3 和 4 对 `sendmail` 都有特殊含义，并按特定顺序处理（参见本章稍后的“S 和 R 运算符：规则集和重写规则”部分）。

以下部分将按表 10.1 中出现的顺序，更详细地介绍各个运算符。

### D 运算符：宏

宏类似于 Shell 变量。定义宏的值后，你可以在配置文件后续部分引用它，其值将被替换该宏。例如，配置文件中可能有许多行提到假设的邮件中心 `mailer.gonzo.gov`。而不是反复键入该名称，你可以定义一个宏 `R`（代表中继邮件器）如下：

```
DRmailer.gonzo.gov
```

当 `sendmail` 在 `sendmail.cf` 中遇到 `$R` 时，它会替换为字符串 `mailer.gonzo.gov`。

宏名称可以包含多个字符。例如，你可以定义 `D(Relay)mailer.gonzo.gov`，然后稍后使用 `$(Relay)` 来引用它。

`sendmail` 定义了许多宏，除非为了解决软件缺陷，否则不应重新定义它们。`sendmail` 使用小写字母作为其预定义宏。大写字母可以自由使用。V.8 版 `sendmail` 的预定义宏在 SIQ 的第 5.1.2 节中有完整文档。

### C 和 F 运算符：类

类与宏类似，但在*重写规则*中用于不同的目的（参见本章稍后的“S 和 R 运算符：规则集和重写规则”）。与宏一样，类由单个字符命名。小写字母保留给 `sendmail`，大写字母用于用户定义的类。类包含一个或多个单词。例如，你可以定义一个类 `H`，包含本地域中的所有主机，如下所示：

```
CH larry moe curly
```

为了方便，大型类可以延续到后续行。类 `H` 的以下定义与前面的定义相同：

```
CH larry
CH moe
CH curly
```

你还可以通过从文件读取单词来定义类：

```
CF/usr/local/lib/localhosts
```

如果文件 `/usr/local/lib/localhosts` 包含单词 `larry`、`moe` 和 `curly`，每行一个，那么这个定义与前面的两个定义等效。

为什么要使用宏和类？最好的理由是它们在配置文件中集中了信息。在上面的示例中，如果你决定将邮件中心的名称从 `mailer.gonzo.gov` 更改为 `mailhub.gonz o.gov`，你只需要更改 `$R` 宏的定义，配置文件就能像以前一样工作。如果名称 `mailer.gonzo.gov` 散布在整个文件中，你可能会忘记在某些地方更改它。此外，如果重要信息被集中，你可以在一个地方进行大量注释。由于配置文件最好理解起来都是晦涩的，大量的注释是六个月后当你疑惑为什么做出某个更改时，那种沉没感的良药。

### H 运算符：头部定义

你可能不想更改 V.8 `sendmail` 配置文件中给出的头部定义，因为它们已经遵循了接受的标准。以下是一些示例头部：

- `H?D?Date: $a`
- `H?F?Recent-From: $q`
- `H?F?From: $q`
- `H?x?Full-Name: $x`

注意，头部定义可以使用宏，这些宏在插入信件时会被展开。例如，前面的 `Full-Name:` 头部定义中使用的 `$x` 宏会展开为发件人的全名。

可选的 `?mailerflag?` 构造告知 `sendmail` 仅当所选邮件器设置了该邮件器标志时才插入头部（参见本章稍后的“M 运算符：邮件器定义”）。

假设你的本地邮件器定义包含一个标志 `Q`，并且 `sendmail` 选择该邮件器来投递信件。如果你的配置文件包含如下头部定义，`sendmail` 会向通过本地邮件器投递的信件插入该头部，并替换宏 `$F` 的值：

```
H?Q?X-Fruit-of-the-day: $F
```

为什么要使用 `?mailerflag?` 功能？不同的协议可能需要不同的邮件头部。由于它们还需要不同的邮件器，你可以在邮件器定义中为每个邮件器定义适当的邮件器标志，并在头部定义中使用 `?mailerflag?` 构造来告知 `sendmail` 是否插入该头部。

### O 运算符：设置选项

`sendmail` 有许多改变其操作或告知其使用文件位置的选项。其中大多数可以在命令行或配置文件中给出。例如，你可以在任何地方指定别名文件的位置。要在命令行上指定别名文件，你使用 `-oA` 选项：

```
$ /usr/sbin/sendmail -oA/etc/aliases [other arguments...]
```

要在配置文件中做同样的事情，你包含一行如下所示：

```
OA/etc/aliases
```

两种用法是等效的，但诸如别名文件位置之类的选项很少更改，大多数人会在 `sendmail.cf` 中设置它们。V.8 `sendmail` 选项在 SIQ 中有完整描述。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_326_0.png)

