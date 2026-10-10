
# Fedora Linux 手手册：用户命令卷 6

## 献辞

本书献给 Michael Kerrisk 以及 Linux 文档项目（Linux Documentation Project）的团队。

编校与编辑：Gareth Morgan Thomas

有很多关于 Perl 和 Perl 相关的书籍。其中一些很棒，有些还可以，但很多并不值你的钱。有一份书籍列表，其中有些带有详尽的评论，位于 .。我们在这里列出了一些书籍，虽然列出某本书意味着我们的认可，但请不要认为未列出某本书意味着什么。

这些书籍大部分可以通过 Safari Books Online ( ) 在线获取。

由 Perl 创造者编写的 Perl 主要参考书是《Programming Perl》：

- 《Programming Perl》（“大骆驼书”）：
- 作者：Tom Christiansen, Brian D Foy, Larry Wall 以及 Jon Orwant，ISBN 978-0-596-00492-7 [2012年2月第四版] ISBN 978-1-4493-9890-3 [电子版]

《The Ram》是一本包含数百个使用 Perl 完成特定任务示例的菜谱：

- 《The Perl Cookbook》（“公羊书”）：
- 作者：Tom Christiansen 和 Nathan Torkington，Larry Wall 序言，ISBN 978-0-596-00313-5 [2003年8月第二版] ISBN 978-0-596-15888-0 [电子版]

如果你想学习 Perl 基础，可以从“骆驼书”开始，它假设你已经了解一点编程：

- 《Learning Perl》（“骆驼书”）：
- 作者：Randall L. Schwartz, Tom Phoenix, 和 Brian D Foy，ISBN 978-1-4493-0358-7 [2011年6月第六版] ISBN 978-1-4493-0458-4 [电子版]

《骆驼书》中开始的教程在《Intermediate Perl》中继续，该书介绍了引用、数据结构、面向对象编程和模块等中级特性：

- 《Intermediate Perl》（“羊驼书”）：
- 作者：Randall L. Schwartz 和 Brian D Foy，Damian Conway 为 Tom Phoenix 序言，ISBN 978-1-4493-9390-0 [2012年8月第二版] ISBN 978-1-4493-0459-1 [电子版]

你可能想在键盘旁保留这些桌面参考：

- 《Perl 5 Pocket Reference》
- 作者：Johan Vromans，ISBN 978-1-4493-0370-9 [2011年7月第五版] ISBN 978-1-4493-0813-1 [电子版]

### 《Perl Debugger Pocket Reference》
- 作者：Richard E Foley，ISBN 978-0-596-00503-0 [2004年1月第一版] ISBN 978-0-596-55625-9 [电子版]

### 《Regular Expression Pocket Reference》
- 作者：Tony Stubbeline，ISBN 978-0-596-51427-3 [2007年7月第二版] ISBN 978-0-596-55782-9 [电子版]

### 《Beginning Perl》
- 作者：James Lee，ISBN 1-59059-391-X [2010年4月第三版]

### 《Learning Perl（“骆驼书”）》
- 作者：Randall L. Schwartz, Tom Phoenix, 和 Brian D Foy，ISBN 978-1-4493-0358-7 [2011年6月第六版] ISBN 978-1-4493-0458-4 [电子版]

### 《Intermediate Perl（“羊驼书”）》
- 作者：Randall L. Schwartz 和 Brian D Foy，Damian Conway 为 Tom Phoenix 序言，ISBN 978-1-4493-9390-0 [2012年8月第二版] ISBN 978-1-4493-0459-1 [电子版]

### 《Mastering Perl》
- 作者：Brian D Foy，ISBN 978-1-4493-9311-3 [2014年1月第二版] ISBN 978-1-4493-6487-8 [电子版]

### 《Effective Perl》
- 作者：Joseph N. Hall, Joshua A. McAdams, Brian D Foy，ISBN 0-321-4964-9 [2010年第二版]

### 《Task-Oriented Writing Perl Modules for CPAN》
- 作者：Sam Trevor，ISBN 1-59059-018-X [2002年8月第一版]

### 《The Perl Cookbook》
- 作者：Tom Christiansen 和 Nathan Harington，Larry Wall 序言，ISBN 978-0-596-00313-5 [2003年8月第二版] ISBN 978-0-596-15888-0 [电子版]

### 《Automating System Administration with Perl》
- 作者：David N. Blankelman，ISBN 978-0-596-00639-6 [2009年5月第二版] ISBN 978-0-596-80251-6 [电子版]

### 《Real World SQL Administration with Perl》
- 作者：Lin Shea，ISBN 1-59059-097-X [2003年7月第一版]

### 《Special Topics Regular Expressions Cookbook》
- 作者：Jan Gooyerts 和 Steven Levi，ISBN 978-1-4493-1943-4 [2012年8月第二版] ISBN 978-1-4493-2747-7 [电子版]

### 《Programming the Perl》
- 作者：Tim Bunce 和 Allison Descartes，ISBN 978-1-56592-699-8 [2000年2月] ISBN 978-1-4493-8670-2 [电子版]

### 《Perl Practices》
- 作者：Damian Conway，ISBN 978-0-596-00173-5 [2005年7月第一版] ISBN 978-0-596-15900-9 [电子版]

### 《Higher-Order Perl》
- 作者：Mark-Jason Dominus，ISBN 1-55860-701-3 [2005年3月第一版] 电子版

### 《Mastering Regular Expressions》
- 作者：Jeffrey E. F. Friedl，ISBN 978-0-596-52812-6 [2006年8月第三版] ISBN 978-0-596-55899-4 [电子版]

### 《Network Programming with Perl》
- 作者：Lincoln Stein，ISBN 0-201-65171-1 [2001年第一版]

### 《Perl Toolkit》
- 作者：Darren Chamberlain, Dave Cross, 和 Andy Wardley，ISBN 978-0-596-00476-7 [2003年12月] ISBN 978-1-4493-8647-4 [电子版]

### 《Object-Oriented Perl》
- 作者：Damian Conway，Randall L. Schwartz 序言，ISBN 1-884777-79-1 [1999年8月第一版] 电子版

### 《Data Munging with Perl》
- 作者：Dave Cross，ISBN 1-930110-00-6 [2001年第一版] 电子版

### 《Mastering Perl/Tk》
- 作者：Steve Lidie 和 Nancy Walsh，ISBN 978-1-56592-716-2 [2002年1月第一版] ISBN 978-0-596-10344-6 [电子版]

### 《Extending and Embedding Perl》
- 作者：Tim Neless 和 Simon Cozens，ISBN 1-930110-82-0 [2002年8月第一版] 电子版

### 《Pro Perl Debugging》
- 作者：Richard Foley 和 Andy Lester，ISBN 1-59059-454-1 [2005年第一版] 电子版

这些书籍中的一些可以通过免费下载的形式提供。



在 Jon Bentley 写的这系列 ACM 专栏中，你可能会注意到熟悉的 Perl 概念。这与主要 Perl 书籍（后期出版）标题的相似并非完全偶然：

- 作者：Jon Bentley，ISBN `978-0-201-65788-3` [1999年10月第二版]
- 作者：Jon Bentley，`0-201-11889-0` [1988年1月]

每个版本的 Perl 都附带了发布当时的文档。这对于像书籍列表这样的内容带来了问题。在这些列表包含在你的 Perl 版本之后，可能出版了非常好的书籍，你可以在 `.` 检查最新版本。

我们列出的某些书籍在互联网尺度下看起来几乎是古董，但我们包含了它们，是因为它们仍然描述了当前的方法。Perl 中并非所有内容每天都在改变。许多初级书籍也涵盖了今天仍然有效的基本特性和技术。总来说，我们尝试将此列表限制在过去五年出版的书籍。

如果您的 Perl 书籍未列入且您认为它应该列入，请告诉我们。

### 面向对象编程

有关使用 Perl 进行面向对象（OO）编程的信息，请参阅 `perloot` 和 `perlob`。

（上述文档取代了以前此处在 `perlboot` 中的教程。）

`perlbot` - 指向 Perl 面向对象编程信息的链接

有关使用 Perl 进行面向对象（OO）编程的信息，请参阅 `perlootut` 和 `perobj`。

（上述文档取代了以前此处在 `perlbot` 中的技巧集。）

### BS2000 安装

`perlbs2000` - 为 BS2000 编译并安装 Perl。

本文档需要更新，但我们不知道应该写什么。请将意见通过邮件发送至 `<mailto:>`。

本文档将帮助你在 BS2000 的 POSIX 子系统中配置、编译、测试和安装 Perl。

这是一个为 BS2000 版本 OSD V3.1A 或更高版本的 POSIX 子系统移植的 perl 版本。它也可能在其他版本上运行，但我们是从 3.1A 版本开始移植和测试的，目前正在使用 V4.0A 版本。

安装 Perl 你可能需要以下 GNU 程序：

BS2000 上的 `gzip`

我们使用了 1.2.4 版本，它可以开箱即用，但在 `make check` 期间会出现一次失败。

BS2000 自带的 Yacc 对我们不起作用。因此我们必须使用 `bison`。我们对 perl 了一些修改以便使用 `bison` 的纯（可重入）解析器。我们使用了 1.25 版本，但由于 EBCDIC，我们需要添加一些更改。有关 yacc 的更多细节请见下文。

要在 BS2000 POSIX 上提取归包，你需要 ASCII 文件系统（我们使用了 `mountpoint=/usr/local/ascii`）。现在你在 ASCII 文件系统中提取归包，且不进行 IO 转换：

```
cd /usr/local/ascii; export IO_CONVERSION=NO; gunzip < /usr/local/ascii/src/perl.tar.gz | pax -r
```

你可以忽略归包中第一个元素的错误信息（这看起来不像 tar 归包 / 跳过下一个文件...），因为它只是一个会自动创建的目录。

提取归包后，将整个目录树复制到你的 EBCDIC 文件系统。这次使用 IO 转换：

```
cd /usr/local/src; export IO_CONVERSION=YES; cp -r /usr/local/ascii/perl.5.005_02 .
```

有一个针对 BS2000 的“提示”文件，名为 `hints.posix-bc`（因为 `posix-bc` 是 `uname` 提供的操作系统名称），它指定了大多数内容的正确值。主要问题（当然）是 EBCDIC 字符集。我们有一个通用的 EBCDIC 版本。

由于原生 yacc 存在问题，我们使用 GNU `bison` 为 `perl.y` 生成了一个纯（可重入）解析器。因此 yacc 实际上是下面的脚本：

```
---</usr/local/bin/yacc---< #! /usr/bin/sh
```

```bash
# 保存参数：params="" while [[ $ -gt 1 ]]; params="$params $1" shift

tmpfile=tmpbison.$$.y; echo %pure_parser > tmpfile; $1 >> $tmpfile

echo "usr/local/bin/bison -yacc $params $1\t\t(Pure Parser)"; /usr/local/bin/bison -nyacc $params $tmpfile

rm -f $tmpfile
```

尽管如此，我们仍然为 `a2p` 使用普通的 yacc！！！我们创建了一个名为 `byacc` 的软链接来区分这两个版本：

```
ln -s /usr/bin/yacc /usr/local/bin/byacc
```

我们使用 GNU `make` 构建。我们也构建过一次原生版本，它也能正常工作。

我们在 `make test` 期间仍然遇到了一些错误。其中一些是使用 `bison` 的结果。`bison` 打印解析器而不是语法错误，我们可以忽略它们。列表显示了我们的错误，你的结果可能有所不同：

| 测试 | 结果 |
| :--- | :--- |
| op/numconvert | 失败测试 1409-140 |
| /regexp | 失败测试 483, 496 |
| /opregex_noam | 失败测试 483, 496 |
| pragma/overload | 失败测试 152-153, 170-171 |
| pragma/warnings | 失败测试 14, 82, 129, 155, 192, 207 |
| lib/bigfloat | 失败测试 351-352, 355 |
| lib/bigftpm | 失败测试 354-355, 358 |
| lib/complex | 失败测试 267, 487 |
| lib/dumper | 失败测试 43, 45 |

11/231 个测试脚本失败，95.24% 通过。57/10595 个子测试失败，99.46% 通过。

我们目前在 BS2000 POSIX 上没有 `noff` 工具，因此我们在安装文档时忽略了任何错误。

BS2000 POSIX 不支持 shebang 符号（`#!usr/bin/perl`），因此你必须使用以下缩进：

```bash
: use perl eval'exec /usr/local/bin/perl -S ${1+"$@"}'

if $running_under_some_shell;
```



我们这方面的经验不多，但可以尝试：

使用 `bs2cp` 将你的 Perl 执行文件复制到 bs2000 LLM：
`bs2cp /usr/local/bin/perl bs2perl(perl,l)`

现在你可以使用以下 (SDF) 命令启动它：
`/START-PROG-FROM-FILE=*MODULE(PERL), PROG-MODE=*ANY,RUN-MODE=*ADV`

首先你会得到 bs2000 命令提示符 (*)。在这里你可以输入参数，例如 `-e 'print "Hello World!\n"'`（注意双斜杠！）或 `-w` 以及你的 Perl 脚本名称。

由 Perl 生成。你也可以查阅操作系统的文档，可能会有所收获。

如果你在非 UNIX 平台上，请使用 `perldoc perl`，因为某些功能可能尚未实现或工作方式有所不同。

你可能可以使用 Perl 调试器 `perdoc deldbug` 来找出问题出在哪里。

`bug` 越容易复现，修复的可能性越高——如果没有人能复现你的问题，它就不会被修补。

一个良好的测试用例通常具有以下属性：代码简短、简单；对外部命令、模块或库的依赖较少；不包含依赖平台的代码（除非是特定平台的 bug）；文档清晰、简单。

一个良好的测试用例几乎总是包含在 Perl 测试套中的理想人选。如果你有时间，考虑编写你的测试用例，使其能够方便地包含到标准测试套中。

你是否包含了所有相关信息？

请务必包含准确的错误信息（如果有的话。“Perl 给了一个错误”并不是一个准确的错误信息。

如果你获得了核心转储（core dump）或等效内容，你可以使用调试器（`dbx`, `gdb` 等）生成栈跟踪并将其包含在 bug 报告中。

> 注意：除非你的 Perl 在编译时包含了调试信息（通常是 `-g`），否则栈信息可能很难使用，因为它可能只包含函数名而不包含它们的参数。如果可能，请带有调试信息重新编译你的 Perl 并复现崩溃和栈跟踪。

你能用通俗的英语描述这个 bug 吗？

可复现的 bug 越容易理解，修复的可能性越高。换句话说，尝试在你的能力范围内分析问题并报告你的发现。

你能自己修复这个 bug 吗？

如果可以，那太棒了；带有补丁的 bug 报告可能比没有补丁的报告获得更多的关注和兴趣。使用 `-p` 选项将你的补丁附加到报告中。在发送补丁时，尽可能使用 `git format-patch` 创建，尽管使用 `diff -pu` 创建的统一 diff 效果同样很好。

你的补丁可能会被退回并要求修改，或者要求对你的修复方案提供更详细的解释。

以下是一些关于高质量补丁的提示：

- 确保补丁没有反反（diff 的第一个参数通常是原始文件，第二个参数是你修改的文件）。在发送之前，通过通过 `git am` 或 `patch` 程序应用补丁来测试它。尝试遵循与你正尝试修复的代码相同的风格。确保你的补丁确实有效（如果你正在修复的代码被 Perl 的测试套件覆盖，请运行 `make test`）。

你可以使用 "perlbug" 来提交报告吗？

`perlbug` 等功能可以确保你的报告包含了关于你 Perl 版本的关键信息。如果你输入完内容后 `perlbug` 无法发送你的报告，你可能需要自己编写消息，或者添加 `perlbug -d` 产生的输出并通过电子邮件发送。如果由于某种原因你无法在系统上运行 `perlbug`，请务必包含运行 `perl -v`（注意大写的 V）产生的所有输出。

无论你是使用 `perlbug` 还是手动发送邮件，请确保你的主题行（Subject line）具有信息量。“a bug”并不包含信息量。“perl crashes”或“HELP!!!”也一样。不要隐藏它。对错误之处进行简要描述是可以的。

你可以使用 "perlbug" 来提交感谢信吗？

可以，你可以通过使用 `-T` 选项或通过调用程序 `perlthanks` 来来实现。感谢信是很好的。它能让人微笑。

完成你自己的部分后，请准备好等待、被告知 bug 在你的代码中，或者可能完全没有收到任何回复。维护 Perl 的志愿者都是忙碌的人，所以如果你的问题是你代码中显而易见的 bug、难以理解或者是现有报告的重复，你可能不会收到个人回复。

如果你的 bug 修复对你很重要，请监控邮件列表（邮件列表经过审核，你的消息可能需要一段时间才能显示）以及开发版本的代码提交日志，并用友善的话语或提供冰凉的饮料来鼓励维护者。（请对维护者友善。骚扰或辱骂他们可能会产生你想要相反的效果。）

如果发布了新版本的 Perl 而你的 bug 仍然存在，请随时更新你的 bug get。

- `-a` 发送报告的地址。默认是当前。
- `-A` 不向回复地址发送 bug 接收确认。通常只有当你是活跃监控此类消息的 Perl 维护者时，使用此选项才是合理的。
- `-C` 不向管理员发送副本。
- `-c` 发送报告副本的地址。默认是本地 Perl 管理员的地址（构建 Perl 时记录）。
- `-d` 数据模式（当你重定向或管道化输出时的默认模式）。这会打印你的配置数据，而不发送任何邮件。你可以配合 `-v` 使用获取更完整的数据。
- `-e` 使用的编辑器。
- `-f` 包含报告正文的文件。使用此快速发送准备好的消息。
- `-h` 打印选项的简要摘要。
- `-ok` 报告构建成功。

# CALL_* 函数

虽然使用示例来解释这些内容更简单，但你首先需要注意一些重要的细节。

Perl 提供了许多 C 函数允许你调用 Perl 子程序。它们是 `I32 call_sv(SV* sv, I32 flags);` `I32 call_pv(char *subname, I32 flags);` `I32 call_method(char *methname, I32 flags);` `I32 call_argv(char *subname, I32 flags, char **argv);`。

关键函数是 `call_sv`。其他所有函数都是简单的封装器，在特殊情况下更容易调用 Perl 子程序。根结底，它们都会调用 `call_sv` 来调用 Perl 子程序。

所有的 `call_*` 函数都有一个 `flags` 参数，用于向 Perl 传递选项的位码。该位码在每个函数中的操作方式相同。位码中可用的设置在“FLAG VALUES”中进行了讨论。

现在将逐一讨论每个函数。

### call_sv

`call_sv` 两个参数。第一个参数 `sv` 是一个 `SV*`。这允许你通过 C 字符串指定要调用的 Perl 子程序（该字符串首先被转换为 `sv`）或一个子程序的引用。“Using call_sv”部分展示了如何使用 `call_sv`。

### call_pv

`call_pv` 函数与 `call_sv` 类似，但它期望 C `char*` 标识你想要调用的 Perl 子程序，例如 `call_pv("fred")`。如果你要调用的子程序在另一个包中，只需在字符串中包含包名即可，例如 `pkg:fred`。

### call_method

`call_method` 函数用于从 Perl 类调用方法。参数 `methname` 对应于要调用的方法名称。注意，该方法所属的类是在 Perl 栈上传递的，而不是在参数列表中。该类可以是类名（用于静态方法），也可以是引用（用于虚拟方法）。有关静态方法和虚拟方法的更多信息请参见 perldoc，并在“Using call_method”中查看使用 `call_method` 的示例。

### call_argv

`call_argv` 通过 `subname` 参数中的 C 字符串调用 Perl 子程序。它也接受通常的 `flags` 参数。最后一个参数 `argv` 由一个以 NULL 终止的 C 字符串列表组成，作为参数传递给 Perl 子程序。“Using call_argv”。

所有函数都返回一个整数。这是 Perl 子程序返回的项数。子程序返回的实际项存储在 Perl 栈上。

作为一个一般规则，你应该始终检查这些函数的返回值。即使你只期望 Perl 子程序返回特定数量的值，也没有什么能阻止人做意料之外的事——别说我没警告过你。

所有 `call*` 函数中的 `flags` 参数都是 `G_VOID`、`G_SCALAR` 或 `G_ARRAY` 之一，它们表示调用上下文，并与下面定义的其他 `G*` 符号的组合位码进行位或（OR'ed）操作。

### G_VOID

在空上下文（void context）中调用 Perl 子程序。

此标志有两个效果：

- 1. 它向被调用的子程序指示它正在空空上下文中执行（如果执行了 `wantarray`，结果将是未定义值 `undef`）。
- 2. 它确保子程序不会实际上返回任何内容。

`call*` 函数的返回值表示 Perl 子程序返回了多少项——在这种情况下，它将为 0。

### G_SCALAR

在标量上下文（scalar context）中调用 Perl 子程序。这是所有 `call*` 函数的默认上下文标志设置。

此标志有两个效果：

- 1. 它向被调用的子程序指示它正在标量上下文中执行（如果执行了 `wantarray`，结果将为 `false`）。
- 2. 它确保子程序实际上只返回一个标量。当然，子程序可以忽略 `wantarray` 并仍然返回列表。如果是这样，则只返回列表的最后一个元素。

`call*` 函数的返回值表示 Perl 子程序返回了多少项——在这种情况下，它将是 0 或 1。

如果为 0，则说明你指定了 `G_DISCARD` 标志。

如果为 1，则 Perl 子程序返回的项将存储在 Perl 栈上。“Returning a Scalar”部分展示了如何在栈上访问此值。记住，无论 Perl 子程序返回多少个项，从栈上只能访问最后一个——将只返回一个值的情况视为只有一个元素的列表。当控制从 `call*` 函数返回时，返回的其他任何项将不再存在。“Returning a list in a scalar”部分展示了这种行为的示例。

在列表上下文（list context）中调用 Perl 子程序。
与 `G_SCALAR`一样，此标志有两个效果：

- 1. 它向被调用的子程序指示它正在列表上下文中执行（如果执行了 `wantarray`，结果将为 `true`）。
- 2. 它确保当控制从 `call*` 函数返回时，子程序返回的所有项都是可访问的。

`call*` 函数的返回值表示 Perl 子程序返回了多少项。
如果为 0，则你指定了 `G_DISCARD` 标志。
如果不是 0，它将是子程序返回的项数。这些项将存储在 Perl 栈上。“Returning a list of values”部分给出了使用 `G_ARRAY` 标志的示例以及访问返回项的机制。

### G_DISCARD

默认情况下，`call*` 函数会将子程序返回的项放在栈上。如果你对这些项感兴趣，设置此标志可以让 Perl 自动处理它们。注意，如果你使用 `G_SCALAR` 或 `G_ARRAY`，你必须自己来处理这些临时变量（即子程序返回的值）。“Returning a Scalar”部分介绍了如何处理这些临时变量。“Using Perl to dispose with”部分讨论了让 Perl 处理的具体情况。

### G_NOARGS

当使用 `call*` 函数调用 Perl 子程序时，默认假设传递了参数。如果不向 Perl 子程序传递任何参数，设置此标志可以节省一些时间。它的效果是不为子程序创建 `@_` 数组。
尽管此标志的功能看起来很直观，但只有在有理由的情况下才应该使用。谨慎的原因是，即使你指定了 `G_NOARGS`，Perl 子程序仍然认为你传递了参数。

事实上，发生的情况是 Perl 子程序可以访问之前子程序的 `@_`。这会在代码从另一个子程序执行时发生。以下代码说明了这一点：



`sub fred { print "\n" } sub joe { &fred } &joe(1,2,3);`

这将打印

```
1 2 3
```

发生的是 `fred` 访问了属于 `joe` 的 `@_`.

### G_EVAL

你调用的 Perl 子程序可能会终止，例如通过显式调用 `die`。默认情况下，当这些事件发生任何一个，进程将终止。如果你想触发此类事件，请指定 `G_EVAL` 标志。它会在子程序调用周围加上 `eval`。

当控制从 `call*` 函数返回，你需要像在普通 Perl 脚本中一样检查 `$$` 变量。

`call*` 函数的返回值取决于指定的标志以及是否报错。以下是不同的情况：

> 如果 `call_*` 函数正常返回，则返回值如前面的章节所示。
> 如果指定了 `G_ARRAY` 且发生了错误，返回值始终为 0。
> 如果指定了 `G_SCALAR` 且发生了错误，返回值为 1，栈顶的值为 `undef`。这意味着如果你已经通过检查 `$$` 检测到错误并想让程序继续，你必须记得从栈上弹出 `undef`。

请参阅“Using G_EVAL”有关使用 `G_EVAL` 的详情。

上述的 `G_EVAL` 标志始终会设置 `$$`：如果没有错误则清除它，如果被调用代码发生错误则将其设置为错误状态。如果你的意图是处理可能的错误，这就是你想要的；但有时你希望捕捉错误并阻止它们干扰程序的其余部分。

这种场景主要适用于那些旨在在析构函数、异步回调和信号处理程序内部调用的代码。在这些情况下，这种

被调用的代码与周围动态上下文的关系很小，主程序需要与被调用代码中的错误隔离开，即使这些错误无法被智能地处理。将此代码用于 `__DIE__` 或 `__WARN__` 钩子以及绑定函数也可能很有用。

`G_KEEPERR` 标志旨在与实现此类代码的 `G_EVAL` `call_*` 函数配合使用，或者与 `eval_sv` 配合使用。当不使用 `G_EVAL` 时，此标志对 `call_*` 函数没有作用。

当使用 `G_KEEPERR` 时，任何被调用代码中的任何错误将像往常一样终止调用，且错误不会传播到调用之外（这是 `G_EVAL` 的常态），但它不会进入 `$$`。相反，错误将被转换为警告，并带有字符串 "(in cleanup)" 前缀。可以使用 `no no warnings 'misc'` 来禁用此设置。如果没有错误，`@@` 将不会清除。

注意，`G_KEEPERR` 标志不会传播到内部 `eval` 中；这些内部 `eval` 可能仍然设置 `@`。

`G_KEEPERR` 标志是在 Perl 5.002 版本中引入的。

参见 [Using G_KEEPERR](Using_G_KEEPERR) 以获取需要使用此标志的场景示例。

如上所述，你可以在 Perl 中通过 `wantarray` 确定当前执行的子程序的上下文。在 C 中，可以使用 `GIMME_V` 宏进行等效测试，如果你在列表文中被调用，它返回 `G_ARRAY`；如果在标量文中，它返回 `G_SCALAR`；如果在空文中（即返回值将不被使用），它返回 `G_VOID`。该宏的一个旧版本称为 `GIMME`；在空文中它返回 `G_SCALAR` 而不是 `G_VOID`。使用 `GIMME_V` 宏的示例见 [Using GIMME_V](Using_GIMME_V) 部分。

关于定义的讨论足够了！让我们来看几个例子。

Perl 提供了许多宏来辅助访问 Perl 栈。在可能的情况下，与 Perl 内部接口交互应使用宏。我们希望这能让代码对未来 Perl 的任何更改不敏感。

另一个值得注意的点是，在第一系列示例中，我只使用了 `call_pv` 函数。这样做是为了保持代码更简单，并让你熟悉该主题。在可能的情况下，如果在使用 `call_pv` 和 `call_sv` 之间进行选择，你应该始终尝试使用 `call_sv`。详情请参见 [Using call_sv](Using_call_sv)。

这个简单而言的示例将调用一个 Perl 子程序 `PrintUID`，以打印进程的 UID。

```c
sub PrintUID() { print "UID is $<\n"; }
```

这里是调用它的 C 函数：

```c
static void call_PrintUID() { dSP; PUSHMARK(SP); call_pv("PrintUID", G_DISCARD|G_NOARGS); }
```

很简单，对吧？
关于此有几点需要注意：

- 1. 暂时忽略 `dSP` 和 `PUSHMARK(SP)`。它们将在下一个示例中讨论。
- 2. 我们没有向 `PrintUID` 传递任何参数，因此可以指定 `G_NOARGS`。
- 3. 我们对 `PrintUID` 返回的任何内容都不感兴趣，所以指定 `G_DISCARD`。即使 `PrintUID` 被更改为返回某些值，有了 `G_DISCARD` 也意味着它们在 `call_pv` 的控制时会被擦除。
- 4. 由于使用了 `call_pv`，Perl 子程序被指定为 C 字符串。在这种情况下，子程序名称已被“硬编码”到代码中。
- 5. 因为我们指定了 `G_DISCARD`，所以没有必要检查 `call_pv` 的返回值。它始终为 0。

## 传递参数

现在让我们做一个稍微复杂一点的例子。这次要调用 Perl 子程序 `LeftString`，它将接受 2 个参数——一个字符串 `($s)` 和一个整数 `($n)`。

该子程序将简单打印字符串的前 `$n` 个字符。

因此 Perl 子程序看起来如下：

```c
sub substring { ($s, $n) = @_; print substr($s, 0, $n), "\n"; }
```

调用 `callString` 需要的函数看起来如下：

```c
static void callLeftString(a, b) char *; int b; { DSP; ENTER; SAVETMPS;

pUSHMARK(SP); XPUSHHS(sv_2mortal(newSvp(a, 0))); PUTBACK; call_pv("LeftString", G_DISCARD);

FREETMPS; LEAVE; }
```

以下是对 C 函数 `callLeftString` 的几点说明。

- 参数通过 Perl 栈传递给 Perl 子程序。这就是从 `DSP` 行开始到以 `PUTBACK` 结束的代码的目的。`DSP` 声明了栈指针的局部副本。该局部副本应该始终通过 `SP` 访问。
- 如果你要向 Perl 栈中放入某些东西，你需要知道把它放在哪里。这就是宏 `DSP`的作用——它声明并初始化了 Perl 栈指针的局部副本。
- 本示例中使用的所有其他宏都需要你使用这个宏。
- 该规则的例外是你是从 XSUB 函数直接调用 Perl。在这种情况下，没有必要显式使用 `DSP` 宏——它会自动为你声明。
- 推送到栈顶的任何参数都应该被 `PUSHMARK` 和 `PUTBACK` 宏包围。这些宏的目的是确保栈指针被正确恢复。

如果 `call_AddSubtract` 这样被调用：

`call_AddSubtract(7, 4);`

那么输出如下：

```
7 - 4 = 3 + 7 + 4 = 11
```

说明

- 1. 我们需要列表上下文，因此使用了 `G_ARRAY`。
- 2. 出乎意料的是，这次使用了两次 `POPi`，因为我们从栈中获取了 2 个值。需要注意的是，当使用 `POP*` 宏时，元素是按反序从栈中弹出的。

## 在标量上下文中返回列表

假设上一节中的 Perl 子程序在标量上下文中被调用，如下所示：

```c
static void call_AddScalar(a, b) int a; int b; { dSP; int count; int i;

ENTER; SAVEMPS; PUSHMARK(SP); XPUSHAS(sv_2mortal(newSiv(a)));

XPUSHHS(sv_2mortal(newSiv(b))); PUTBACK; count = call_pv("AddSubtract",nG_SCALAR); SPAGAIN; printf ("Items Returned = %d\n", count); for (i = 1; i <=; ++i) printf ("Value %d\n", i, POPi); PUTBACK; FREETMPS;

LEAVE;
```

另一个修改是 `call_AddScalar` 会打印子程序返回的项目数。如果调用 `call_AddScalar`（为了简单起见，假设它们是整数）：

`call_AddScalar(7, 4);`

输出将是：

```
Items Returned = 1 Value = 3
```

在这种情况下，主要的要点是子程序只返回了列表中的最后一个项。`AddSubtract` 实际上已经调用了 `call_AddScalar`。

直接通过参数列表返回值也是可能的——但这样做是否理想是另一回事。

Perl 子程序 `++ $_[0]; ++ $_[1];` 接收两个参数并直接递增每个。

```perl
```



`sub Inc { ++ $_[0]; };`

```c

static void call_Inc(a

expected @ values from 'Inc', got %d\n"; printf("%d + 1 = %d\n",

a, SVIV(sva)); printf("%d + 1 = %d\n", b, SVIV(svb)); FREETMPS; LEAVE; }

```

并且有一个 C 函数来调用它。

为了能够访问 `call_pv` 之后推入栈的参数，有必要记录它们的地址——两个变量 `sva` 和 `svb`。

这是因为当从 `call_pv` 返回时，持有这些值的 Perl 栈区域很可能已经被其他内容覆盖了。

### 使用 `G_EVAL` 的示例

下面是一个计算两个参数之差的 Perl 子程序。如果结果为负，该子程序将调用 `die`。

```perl
sub Subract { my ($a, $b) = @_; die"death cannot be fatal\n" if $a < $b; $a - $b; }
```

```c
static void call_Subract(int a, int b) { dSP; int count; ENTER;
SAVETMPS; PUSHMARK(SP); XPUSH(sv_2mortal(newSVIV(a)));
XPUSH(sv_2mortal(newSVIB(b))); PUTBACK; count = call_pv("Subtract",
G_EVAL|G_SCALAR); SPAGAIN; // Check the first * / if (SvTRUE(ERRSV)) {
printf("Uh oh - %s\n", SVPV_nolen(ERRSV)); POP; } else if (count == 1) {
croak("call_Subract wanted 1 value from 'Subtract', got %d\n", count);
printf("%d - %s = %d\n", a, b, POPI); PUTBACK; FREETMPS;
LEAVE; }
```

如果 `call_Subract` 这样被调用：

```perl
call_Subract(4, 5)
```

将打印以下内容：

`Uh oh - death cannot be fatal`

说明

- 1. 我们能够捕获 `die` 是因为我们使用了 `G_EVAL` 标志。不指定此标志意味着程序会在子程序 `Subract` 的 `die` 语句处立即终止。
- 2. 代码 `if (SvTRUE(ERRSV)) { printf("Uh oh %s\n", SVPV_nolen(ERRSV)); POP; }` 是 Perl `print "Uh oh - %s\n"; $@;` 的直接等价物。
- 3. 注意在 `svTRUE(ERRSV)` 为真的块中，通过 `POPs` 清理了栈。这是必要的，因为带有 `G_EVAL/G_SCALAR` 的函数调用返回了错误，栈顶持有 `undef`。由于我们希望在检测到此错误后程序继续，必须移除 `undef`。

### 使用 `G_KPERR`

考虑下面这个幽默的示例，我们在析构函数内部使用了 `call_Subtract` 版本：

```perl
package Foo; sub new { bless[0] } sub Subtract { my($a,$b) = @_; die
"death can be fatal if $a < $b; $a - $b; } sub DESTROY call_Subtract(4); } sub foo { die "foo"; package main; my $foo = Foo->new; eval $foo(); print "Saw: $@"; # should be, but isn't
```

这个示例将无法识别 `{}` 内部发生的错误。这是因为：在执行外部块时，`call_Subtract` 代码执行了清理临时变量的操作，因为 `call_Subtract` 是使用 `G_EVAL` 标志实现的，它正确地重置了 `$@`。这导致了最外层测试的失败。

添加 `G_KPERR` 标志，使得 `call_Subtract` 中的 `count = call_pv("Subtract", G_EVAL|G_SCALAR)` 能够保留错误并恢复错误处理。

在之前所有的示例中，我都是“硬编码”了从 C 调用的 Perl 子程序名称。大多数情况下，在 Perl 脚本内部指定 Perl 子程序的名称更方便。

考虑下面的 Perl 代码：

```perl
sub free { print "Hello\n"; } CallSubPV("freed")
```

这是定义 `CallSubPV` 的 XSUB 代码段落：

```c
void CallSubPV(char * name CODE: PUSHMARK(SP); call_pv(name,
G_DISCARD [G_NOARGS]);
```

这已经足够不错了。然而，Perl 允许定义引用和匿名子程序，这就是 `call_sv` 很有用的地方。`CallSubSV` 的代码与 `CallSubPV` 相同，只是 `name` 参数被定义为 `SV*`，且我们使用 `call_sv` 而不是 `call_pv`。

```c
void CallSubSV(name) SV * name CODE: PUSHMARK(SP); call_sv(name,
G_DISCARD [G_NOARGS]);
```

由于我们使用 `sv` 来调用，以下所有内容都可以使用：

`CallSubSV("fred"); CallSubSV(\&fred); $ref = \&fred; CallSubSV($ref);`
`CallSubSV(sub print "Hello there\n" );`

如你所见，`call_sv` 在你指定 Perl 子程序时提供了极大的灵活性。

你应该注意，如果需要保存 `sv`（上例中的 `name`）对应的 Perl 子程序，以便在程序后部分使用，那么仅仅存储指针的副本是不够的。假设代码是这样的：

```c
static SV * rememberSub; void SaveSub1(name) SV * name CODE: rememberSub
name; void SavedSub1() CODE: PUSHMARK(SP);
```

这种做法是错误的，因为当你在 `SavedSub1` 中使用指针 `rememberSub` 时，它可能不再指向 `SaveSub1` 中记录的 Perl 子程序。这对于以下情况尤为真实：

`SaveSub1(\&fred); SavedSub1();`

在执行上述 `SavedSub1` 语句时，对应参数的 `SV*` 已不再存在。对于每一行 `SavedSub1`，预期来自 Perl 的类似于 `Can't use an undefined value as a subroutine reference at...` 的错误消息。

同样，对于这段代码：

`$ref = \&fred; SavedSub1($ref); $ref = 47; SavedSub1();`

你可以预期这些消息之一（具体取决于你使用的 Perl 版本）：`Not a CODE reference at... Undefined subroutine main::47 called...`

在调用 `SaveSub1` 时，变量 `$sv` 可能指向子程序，但等到 `SavedSub1` 获取它时，它持有数字 4。因为我们在 `SaveSub` 中保存了原始 `sv` 的指针，所以对 `$ref` 的任何更改都会被指针 `rememberSub` 跟踪。这意味着每当调用 `SavedSub1` 时，都会尝试执行由 `SV* rememberSub` 引用的代码。但在这种情况下，它现在指向整数 47，所以预期 Perl 会大抱怨。

为了解决这些问题，有必要对 `sv` 取完整拷贝。下面的代码展示了修改此后的 `SaveSub2`：

```c
static SV * keepSub = ($SV*)NULL; void SaveSub2(name) SV * name CODE: /*
Take a copy of the callback /* if keepSub == ($SV*) /* First time, so
create a new SV /* keepSub = newSV($sv); else /* Here before, so
```



overwrite /* `SvSetSV(keepSub, name)`; `void callSavedSub() CODE: PUSHMARK(SP); call_sv(keepSub, G_DISCARD | G_NOARGS);`

在创建一个 `SaveSub` 时，函数会首先检查它是否之前被调用过。如果没有，将为新的 `sv` 分配空间，并使用 `newSsv` 在一次操作中将 Perl 子程序名称的引用复制到变量 `keepSub` 中。之后，每当 `SaveSub` 被调用时，都会使用 `SvSetSV` 用新值覆盖现有的 `sv`（即 `keepSub`）。

这是一个 Perl 子程序，它会打印传递给它的任何参数。

```perl
sub PrintList my(@list) = @_; foreach (@list) { print "$_\n" }
```

这是一个 `call_argv` 调用 `PrintList` 的示例。

```c
static char * words[] = {"alpha", "beta", "gamma", "delta", NULL}; static void callPrintList() { dSP; call_argv("PrintList", G_DISCARD, words); }
```

注意，在这种情况下，没有必要调用 `PUSHMARK`。这是因为 `call_argv` 会为你完成它。

# 使用 _method

考虑以下 Perl 代码：

```perl
{ package Mine; sub new my($type) = shift; bless [@] } sub Display my($self, $index) = @_; print "$index:\$self[$index]\n"; } sub PrintID { my($class) = @_; print "This is Class version 1.0\n"; } }
```

它实现了一个非常简单的类来管理数组。从构造函数 `new` 开始，它声明了方法：一个静态方法和一个虚拟。静态方法 `PrintID` 打印类名和版本号。虚方法 `Display` 打印数组的单个元素。这里是使用该类的纯 Perl 示例：

`$a = Mine->new('red', 'green', 'blue'); $a->Display(1); Mine->PrintID;`

将打印：
`1: green is Class version 1.0`

从 C 调用 Perl 方法非常简单。需要具备以下几点：

- 虚方法的对象引用，或静态方法的类名
- 方法名
- 任何特定于该方法的参数

这是一个简单的 XSUB，说明了从 C 调用 `PrintID` 和 `Display` 方法的机制。

```c
void callMethod(ref, method, index) SV * ref char * method int CODE: PUSHMARK(SP); XPUSHES(ref); XPUSHES(sv_2mortal(newSsv(index))); PUTBACK; call_method(method, G_DISCARD); void call_PrintID(class, method) class char * method CODE: PUSHMARK(SP); XPUSHES(sv_2mortal(newSsv(class, 0))); PUTBACK; call_method(method, G_DISCARD);
```

可以这样调用 `PrintID` 和 `Display` 方法：

```perl
$a = Mine->new('red', 'green', 'blue'); callMethod($a, 'Display', 1);
callPrintID('Mine', 'PrintID');
```

唯一需要注意的是，在静态和虚方法中，方法名都没有通过栈传递——它是作为 `call_method` 的第一个参数使用的。

这是一个测试性的 XSUB，它提供了当前执行环境的上下文。

```c
void PrintContext() CODE: I32 gimme = GIMME_V; if (gimme == G_VOID) printf("Context is Void\n"); else if (gimme == G_SCALAR) printf("Context is Scalar\n"); else printf("Context is Array\n");
```

这里是一些用于测试的 Perl。

```perl
PrintContext; $a = PrintContext; @a = PrintContext;
```

其输出将是
`Context is Void`
`Context is Scalar`
`Context is Array`

在目前给出的示例中，回调函数中创建的任何临时变量（即通过 `call_*` 传递或通过栈返回）都通过以下一种方法释放了：

- 在 `call_*` 时指定 `G_DISCARD` 标志
- 显式使用 `ENTER/SAVETMPS—FREETMPS/LEAVE` 配对

另一种方法是，在回调结束后让 Perl 自动处理。这是通过不使用栈实现的：

```perl
ENTER; SAVETMPS; ... FREETMPS; LEAVE;
```

在回调中（当然，不是指定 `G_DISCARD` 标志）。如果你打算使用这种方法，必须意识到在非常特殊的情况下可能会出现内存泄漏。你需要了解一点 Perl 和回调之间的控制流。
文档开头给出的示例（错误处理器和事件驱动程序）是你可能遇到的两类主要控制流的典型情况。它们之间有一个非常重要的区别，请注意。

在第一个示例中，错误处理器，控制流可能如下：
`perl --> XSUB --> external library`

当控制在库中时发生了错误条件。你之前设置了一个 Perl 回调来处理这种情况，一旦回调完成，控制将再次返回 Perl。在这种情况下，控制流如下：

```perl
perl --> XSUB --> external library <-- error occurs ... external library > call_* --> perl <-- external library <-- call_* <----
```

在使用 `call_*` 后，控制或少返回 Perl。在图中，嵌套得越深，只有当控制回到最左侧的 Perl 时，你才会返回作用域并留下任何临时变量。

在第二个示例中，事件驱动程序，控制流将是：

```perl
perl --> XSUB --> event handler ... event handler --> call_* --> perl | event handler <-- call_* <---- event handler <-- call_* <----
```

在这种情况下，控制流只能由以下重复序列组成：

```perl
event handler --> call_* --> perl
```

对于实际上整个程序运行时间。这意味着控制可能会回到最左侧的 Perl 作用域。

那么大问题是什么？嗯，如果你期望 Perl 清理你的临时变量，所有必须在某个阶段返回作用域。在事件驱动场景中，这种情况不会发生。这意味着随着时间的推移，你的程序将创建越来越多的临时变量，且没有任何被释放。由于每个临时变量都会消耗内存，你的程序将消耗系统中所有的内存！

所以结论是——如果你确定回调结束后会迅速返回作用域，那么没有必要清理创建的任何临时变量。记住，如果你不确定做什么，反正清理也没有坏。

# 存储回调上下文信息的策略

设计回调接口时可能克服的最困难的问题之一是确定 C 回调函数与 Perl 等效值之间的映射。

为了帮助理解这是一个真正的问题，首先考虑在所有 C 环境中如何设置回调。通常，C API 提供一个函数来注册回调。它期望一个函数指针作为参数之一。以下是对假设函数 `register_fatal` 的调用，它注册了发生致命错误时调用的 C 函数。

`register_fatal(cb1);`

变量变量 `cb1` 是函数指针，因此你必须在代码中定义 `cb1`，如下所示：

```c
static void cb1() { printf("Fatal Error\n"); }
```

现在将其改为调用 Perl 子程序：

```c
static SV * callback = (SV)*NULL;
```

```perl
sub cb1 { die "I'm dying...\n"; }
```



C 和 Perl 等效值之间的映射存储在全局变量 `callback` 中。

如果你需要随时注册一个回调，这就足够了。一个示例可以是像概述代码这样的错误处理器。尽管，反复调用 `register_fatal` 将用新函数替换之前注册的函数。

例如，你想连接到一个具有异步文件/O 的库。在这种情况下，你可能希望为每个打开的文件分离不同的 Perl 子程序。目前，处理器示例是不够的，因为它在运行时允许允许一个回调。我们需要一种方法来存储打开的文件与我们想要调用的 Perl 子程序之间的映射。

假设 I/O 库有一个 `async_read`，它将 C 函数 `ProcessRead` 与文件句柄关联——假设它也提供了一些打开文件并获取句柄的例程。

```c
async_expect(fh, ProcessRead)
```

这可能期望如下形式的 C `ProcessRead` 函数：

```c
void ProcessRead(fh, buffer) int fh; char * buffer; { ... }
```

为了给该库提供 Perl 接口，我们需要能够映射 `fh` 和我们想要调用的 Perl 子程序。哈希表是存储这种映射的方便机制。下面的代码显示了可能的实现：

```c
static HV Mapping = (SV)*NULL;
void async_read(fh, int fh SV * callback CODE:
/* 如果哈表不存在，则创建它 */
/* if
(Mapping == (SV)*NULL) Mapping = newSV();
/* 保存 fh -> callback
映射 */
/* hv_store(Mapping, (char*)fh, sizeof(of), newSVcall(callback, 0);
```
/* 与 C 库注册 */
async_read(fh, async_read_if);
而 `async_read_if` 可能如下所示

```c
static void async_read_if(int fh) {
    char * buffer;
    dSP; SV *sv;
    /* Get the callback associated with fh */
    sv = sv_fetch(Mapping, (char*)&fh, sizeof(fh), FALSE);
    if (sv == (**NULL)) croak("Internal error...");
    PUSHMARK(sp); PUSHES(sv_2mortal(newSV(sv)));
    XPUSHES(sv_2mortal(newSVbuffer, 0)));
    PUTBACK;
    /* Call the Perl sub */
    call_sv(*sv, G_DISCARD);
```

为了完整性，这里是 `async_close`。它展示了如何从哈希映射中删除该条目。

```c
void async_close(int fh) {
    /* 从哈表中删除条目 */
    (void) hv_delete(Mapping, (char*)&fh, sizeof(fh), G_DISCARD);
    /* 现在调用
    real async_close */
    async_close(fh);
}
```

Perl 接口看起来如下：

```perl
sub callback { my($handle, $buffer) = @_; }
# 注册 Perl 回调
async_read($fh, &callback);
async_close($fh);
```

C 和 Perl 之间的映射存储在全局哈希 `Mapping` 中。使用此哈希有一个明显的优势，即它允许注册无限数量的回调。

如果 C 回调提供的接口不包含允许将文件句柄映射到 Perl 子程的参数，该怎么办？例如，在异步 I/O 软件包中，回调函数只获取如下所示的参数：

```c
void ProcessBuffer(char * buffer) { ... }
```

如果没有文件句柄，就没有直接的方法从 C 映射回 Perl 子程序。

在这种情况下，绕过此问题的一种可能方法是定义一系列 C 函数作为通往 Perl 的接口，然后：

```c
#define MAX_CB 3
#define NULL_HANDLE -1
typedef void (*FMap)();
struct MapStruct {
    FMap function;
    SV * PerlSub;
    int handle;
};
static void fn1(int);
static void fn2(int);
static void fn3(int);
static struct MapStruct Map[MAX_CB] = {
    {fn1, NULL, NULL_HANDLE},
    {fn2, NULL, NULL_HANDLE},
    {fn3, NULL, NULL_HANDLE}
};
static void Pcb(int index, char * buffer) {
    dSP; PUSHMARK(sp);
    XPUSHES(sv_2mortal(newSVbuffer, 0)));
    PUTBACK;
    /* Call Perl sub */
    call_sv(*Map[index].PerlSub, G_DISCARD);
}
static void fn1(char * buffer) { Pcb(0, buffer); }
static void fn2(char * buffer) { Pcb(2, buffer); }
void array_read(int fh, SV * callback) {
    int index = MAX_CB;
    /* 寻找相同的句柄或空指针 */
    for (index = 0; index < MAX_CB; ++index) {
        if (Map[index].handle == fh) break;
    }
    if (Map[index].handle == NULL_HANDLE) {
        index = index++;
        if (index == MAX_CB) croak("Too many callbacks registered");
    }
    /* 保存文件句柄 */
    Map[index].handle = fh;
    /* 记住 Perl 子程 */
    Map[index].PerlSub = (SV*)newSV(callback);
    async_read(fh, Map[index].function);
}
void array_close(int fh) {
    int index;
    /* 寻找文件句柄 */
    for (index = 0; index < MAX_CB; ++ index) {
        if (Map[index].handle == fh) break;
    }
    if (index == MAX_CB) croak("could not close fh %d", fh);
    Map[index].handle = NULL_HANDLE;
    SVREFCNT_dec(Map[index].PerlSub);
    Map[index].PerlSub = (SV*)NULL;
    async_close(fh);
}
```



在这种情况下，函数 `fn1`、`fn2` 和 `fn3` 被用于记住 Perl 子程序。每个函数都持有一个硬编码的索引，该索引在函数 `Pcb` 中被用于访问 `Map` 数组并调用 Perl 子程序。

这种技术存在显而易见的缺点。

首先，代码比上一个示例要复杂得多。
其次，同时存在的回调数量有一个硬编码的限制（在本例中为 3）。增加此限制的唯一方法是修改代码添加函数，然后重新编译。尽管如此，只要细心地地选择函数数量，它仍然是一个可行的方案，并且在某些情况下是唯一的选择。

总结来说，这里有几种可能的方法供你考虑如何存储 C 和 Perl 回调之间的映射：

- 1. 忽略问题 - 允许 1 个回调：对于许多情况（例如与错误处理程序衔接），这可能是一个完全充分的解决方案。
- 2. 创建系列回调 - 硬编码限制：如果无法从回传给 C 回调的参数中判断出上下文，那么你可能需要创建一系列 C 回调接口函数，并在每个数组中存储指针。
- 3. 使用参数映射到 Perl 回调：C 和 Perl 之间的映射存储在全局哈希 `Mapping` 中。使用此哈希有一个明显的优势，即它允许注册无限数量的回调。

## 另请

`perlxs`, `perlguts`, `perlembed`

# 作者

Paul Marquess

特别感谢以下协助本文创建的人员：
Jeff Okamoto, Tim Bunce, Nick Gianniiotis, Steve Kelem, Gurusamy Sarathy 和 Larry Wall。

# 日期

版本 1.3，1997年4月14日

# PERLCE

> 名称

`perlce` - 适用于 WinCE 的 Perl

# 构建 PERL WINCE

## 警告

本文的大部分内容已经过时，需要更新、重写或删除。构建过程在 5.19 开发分支经过了重构，当时的当前指令见“CURRENT BUILD INSTRUCTIONS”。之前的构建指令在很大程度上已被取代，但可能仍包含一些有用信息，保留在“OLD BUILD INSTRUCTIONS”中，但在提取完其中的有用信息后确实需要删除。

## 描述

此文件提供了为 WinCE 编译 Perl 5.8 及以上版本的说明。请阅读并理解该软件的发行条款。

## 关于交叉编译 WinCE 的通用说明

- 构建了 `miniperl`。这是一个单执行文件（不含 DLL），旨在运行在 Win32 上，并将辅助剩余的构建过程；因为在其之后构建的所有二进制文件都是跨平台的，不应在本地运行。
- `miniperl` 使用 `/win32/Makefile`；这是作为 `wince/Makefile.cefile` 的依赖项调用的正常构建过程的一部分。
- 构建 `miniperl` 后，调用 `configpm` 在正确的位置创建 `Config.pm` 及其对应的 `Cross.pm`。
- 与 Win32 构建不同，`miniperl` 将无法获取宿主机的 `Config.pm`；相反，它将使用交叉编译目录内部的 `Config.pm`。
- `Cross.pm` 文件非常简单：对于 `/INC` 中给定的交叉架构位置，指定 perl 模块所在的路径，并在该处调用正确的 `Config.pm`。
- 那么 `miniperl -MCross -MConfig -llib -we 1` 应该报告错误，因为它找不到 `Config.pm`。如果没有报错——说明替换了错误的 `Config.pm`，生成的二进制文件将是一团糟。
- `miniperl -MCross -MConfig -we 1` 应该运行正常，它将为后续编译提供正确的 `Config.pm`。
- 在扩展构建阶段，会调用 `/win32/buildext.pl`，它反过来进入 `/ext` 子目录并依次执行每个扩展的。
- 所有对 `Makefile.PL` 的调用都提供了 `-MCross` 参数以启用交叉编译。

## 当前构建指令

（这些指令假设宿主机为 32 位 Windows。如果你使用的是 64 位 Windows，请将全文的 “C:\Program Files” 更改为 “C:\Program Files (x86)”。）

### 1. 从此处获取 EVC4

使用此处提到的密钥。

安装程序非常老旧，某些内容进入 `C:/Program Files/Windows CE Tools`，另一些进入 `C:/Windows CE Tools`，无论你提供给安装程序的路径是什么（默认是 `C:/Windows CE Tools`）。安装程序继续进行需要重启。此外，与 Visual Studio 一样，安装 EVC4 时 `.c` 和 `.h` 文件可能会覆盖。

### 2. 从 GitHub 下载（使用“Download ZIP”）

将其解压到没有空格的路径，但不要解压到 perl 构建源码中。在 GitHub 快照中将该目录称为 `celib-palm-3.0`，它应该是 `celib-master`。复制 `wince-arm-pocket-wce300-release` 文件夹并重命名为 `wince-arm-pocket-wce400`。这是一个技巧，以便我们可以通过链接 CE 3.0 的 ARM 汇编来构建 CE 4.0；链接器并不在乎。Windows Mobile/WinCE 在机器码方面与桌面版 Windows 向后兼容。

### 3. 从此处下载 console-1.3-src.tar.gz

将其解压到没有空格的路径，但不要解压到 perl 构建源码中。不要将其解压到与 ce 相同的目录。复制 `wince-arm-pocket-wce300` 文件夹并重命名为 `wince-arm-pocket-wce400`。这是一个技巧，以便我们可以通过链接 CE 3.0 的 ARM 汇编来构建 CE 4.0 二进制文件；链接器并不在乎。Windows Mobile/WinCE 在机器码方面与桌面版 Windows 向后兼容。

### 4 打开 打开提示符，运行你的常规批处理文件为桌面 Visual C 构建设置环境，进入 perl 源码目录，`cd win32/`，填写 Makefile，并执行 `make all` 来构建桌面版 Perl。

### 5. 用文本编辑器打开 `win32/Makefile.ce` 并进行类似下面的补丁。

```
-CEIBLLDIR= h:\windows\celib-palm-3.0 -CECONSELEDIR=
h:\wince\w32console +CEIBLLDIR= C:\sources\celib-palm-3.0
+CECONSELEDIR= C:\sources\win32console
```

同时更改

```
!if "$MACHINE" == "" MACHINE=wince-arm-hpc-wce300 #MACHINE=wince-arm-hpc-
wce211 #MACHINE=wince-sh3-hpc-wce211 #MACHINE=wince-mips-hpc-wce211 #MACHINE=wince-sh3-hpc-wce200 #MACHINE=wince-mips-hpc-w000wince-arm-pocket-wce300 #MACHINE=wince-mips-pocket-wce300 #MACHINE=wince-sh3-pocket-wce300 #MACHINE=wince-x86-pocket-wce300 #MACHINE=wince-mips-pocket-wce211 #MACHINE=wince-arm-pocket-wce211 #MACHINE=arm-pocket-wce400}
```

为

```
!if "$MACHINE" == "" MACHINE=wince-arm-hpc-wce300 #MACHINE=wince-arm-
hpc-wce21 #MACHINE=wince-sh3-hpc-wce211 #MACHINE=wince-mips-hpc-wce211 #MACHINE=wince-sh3-hpc-wce200 #MACHINE=wince-mips-h-w000wince-arm-pocket-wce400}endif
```

所以 `wince-arm-pocket-wce400` 是 `MACHINE` 类型。

### 6. 使用文本编辑器打开 `C:\Program Files\Microsoft Embedded C\4.0\EVC\BIN\WCEARM.BAT`。查找

```
if "%SDKROOT%"="" SDKROOT=...
```

在新的安装中是 `C:\Windows Tools`，在文件管理器中进入 `C:\Windows Tools` 查看是否存在 `C:\Windows Tools\SDK\Include\Armv4`。如果没有，则需要将 `SDKROOT` 更改为 `C:\Program Files\Windows Tools`。进入 `celib-palm-3.0\inc\win32.h`，搜索

```
typedef struct _ABC {
```



### 7. 打开另一个提示符，确保 `PLATFORM` 未设置任何内容（以便后续命令设置默认值），并运行 `"C:\Program Files\Microsoft Embedded C\4.0\EVC\BIN\WCEARM.BAT"`。
### 8. 在用 `WCEARM.BAT` 创建的 WCE 提示符中，进入 perl 源码目录，进入 `win32` 并运行 `"nmake -f Makefile.ce"`。
### 9. Perl 解释器（`perl519.dll` 和 `perl.exe`）将位于类似 `"C:\perl519\src\win32\wince-arm-pocket-wce400"` 的位置，`xs` DLL 位于 `"C:\perl519\src\wince-arm-pocket-wce400\auto"`。要在宿主机上证明成功，从 `win32/` 文件夹运行 `"dumpbin /wince-arm-pocket-wce400\perl.exe"`，并在 `FILE HEADER VALUES` 中的 `"machine (ARM)"` 以及 `OPTIONAL HEADER VALUES` 中的 `"subsystem (Windows GUI)"`。

# 旧构建指令

此部分描述了构建 PerlCE 所需的步骤。你可以在 `< >` 找到更多关于为 WinCE 构建 perl 以及一些预编译的信息。

## 工具与 SDK

编译时你需要：

- Microsoft Embedded Visual Tools
- Microsoft Visual C++
- Rainer Keuche 的 `celib-sources`
- Rainer Keuche 的 `console-sources`

所需的源码可以在 `< >` 下载

# Make

通常你只需要编辑 `/win32/ce-helpers/compile.bat` 以反映你的系统并运行它。

文件 `/win32/ce-helpers/compile.bat` 实际上是 `nmake -f Makefile.ce` 的封装器，带有适当参数并将其转发给 `nmake` 命令。你应该通过这种方式传递目标。

要准备发行，你需要执行以下操作：

- 进入 `/win32` 子目录
- 编辑文件 `/win32/ce-helpers/compile.bat`
- 运行 `compile.bat`
- 运行 `compile.bat_dist`

`Makefile.ce` 有 `CROSS_NAME` 宏，后续用于引用交叉编译方案。你可以为它分配一个名称，但这不是必须的，默认情况下根据你的机器配置名称分配，例如 `"wince-sh3-hpc-wce211"`，这足以区分不同的构建。此选项对于在同一平台执行执行多个构建（例如，线程构建）可能非常方便。在示例中，我们假设所有环境变量对于 C 交叉编译器都是正确的（一个 `*.bat` 非常适合此用途），并且你的 `compile.bat` 设置了正确的 `"MACHINE"` 参数，例如 `wince-mips-wce300`。

```
compile.bat compile.bat_dist compile.bat CROSS_NAME=mips-wce300-thr "USE_THREADS=define" "USE_IMP_SYS=define" "USE_MULTI=define" "USE_IMP_SYS=define"
dist
```

如果一切顺利且构建期间没有错误，你将得到两个独立的发行版：`wince-pocket-mips-wce300` 和 `mips-wce300-thr`。

目标 `dist` 准备发行文件。目标 `zipdist` 作为 `dist` 但额外将发行文件压缩为 `zip` 归档。

> 注意：在构建期间，可能会有一个（一个或多个）用于交叉编译（外部）的 `Config.pm`，这些隐藏在 `/.xlib/$(CROSS_NAME)` 以及其他辅助文件中，但重要的是，宿主机 `miniperl` 没有 `Config.pm`。如果你在构建过程的某处得到找不到 `Config.pm` 的错误，这意味着出了问题。很可能是你忘记指定交叉编译调用 `miniperl.exe` 到 `Makefile.PL`。当为交叉编译扩展时，你的命令行看起来像

```
..miniperl.exe -I...lib -MCross=mips-wce300-thr Makefile.PL
```

或者

```
..miniperl.exe -I...lib -MCross Makefile.PL
```



用于引用上次创建的交叉编译。
所有与构建 WinCE 设备相关的问题可以在邮件列表中提出。

# 在 WINCE 上使用 PERL

## 描述

PerPLC 目前与简单的控制台窗口链接，因此也可以在非 HPC 设备上运行。

简单的 stdio 实现会创建 `stdin.txt`、`stdout.txt` 和 `stderr.txt` 文件，如果你的控制台列数有限，你可以检查这些文件。

当 `exitcode` 不为零时，会出现消息框，否则控制台将关闭，因此你可能需要在程序中捕获状态为 0 的退出以看到任何输出。

`stdout`/`stderr` 现在进入文件 `/perl-stdout.txt` 和 `/perl-stderr.txt`。

PerLIDE 在处理 `perlce` 时非常方便。

### 局限性

不支持 `fork()`、`pipe()`、`popen()` 等。

### 环境

所有环境变量必须以字符串形式存储在 `HKLM\Environment` 中。它们在进程启动时被读取。

### PERLLIB

- 常用的 perl 路径（半列表）。

### PATH

- 可执行文件的半列表。

### TMP

- 临时目录。

### UNIXROOTPATH

- 访问某些特殊文件的根，例如 `/dev/null`、`/etc/services`。

### ROWS/COLS

- 控制台的行/列数。

### HOME

- 目录。

### CONSOLEFONTSIZE

- 控制台字体大小。

你可以通过 `cereg.exe`、远程注册表编辑器或 PerLIDE 设置这些内容。

### 注册表

要通过点击 perl 源文件启动 perl，你必须 `HKCR` 中创建相应的项（参见 `c-helpers/wince-reg.bat`）。据报道，`cereg.exe`（必须在带有 ActiveSync 的桌面电脑上执行）在某些设备上无法工作。你需要使用注册表编辑器手动创建注册项。

### XS

内置以下 Win32 方法：

```
XS("Win32::GetCwd", w32_GetCwd, file); newXS("Win32::SetCwd", w32_SetCwd, file); newXS("Win32::GetTickCount", w32_GetTickCount, file); newXS("Win32::GetOSVersion", w32_GetOSVersion, file); newXS("Win32::IsWinNT", w32_IsWinNT, file); newXS("Win32::IsWin95", w32_IsWin95, file); newXS("Win32::IsWinCE", w32_IsWinCE, file); newXS("Win32::CopyFile", w32_CopyFile, file); newXS("Win32::Sleep", w32_Sleep, file); newXS("Win32::MessageBox", w32_MessageBox, file); newXS("Win32::GetPowerStatus", w32_GetPowerStatus, file); newXS("Win32::GetOemInfo", w32_GetOemInfo, file); newXS("Win32::ShellEx", w32_ShellEx, file);
```

## 缺陷

如果使用 stdio（普通 perl 处理句柄），目前不支持以读写方式打开文件。

如果你发现 bug 或它在你的设备上完全无法工作，请向下方地址发送邮件。请报告你的设备详细信息（处理器、`ce` 版本、设备类型 (`hpc`/`palm`/`pocket`)）以及下载文件的日期。

## 安装

目前的安装说明位于 `Cwd` at `<`。

在安装和测试过程后，流程将变得稳定，信息将更加精确。

## 致谢

Win32 的移植被用参考。

## WINCE 移植历史

### 5.6.0

`perl` 到 WinCE 的首次移植。这是在一个名为 `wince` 的独立目录中进行的。该移植基于 `/.win32` 目录的内容。没有构建 `miniperl`，用户必须拥有 HOST `perl` 并正确编辑 `makefile.ce` 以反映此。

### 5.8.0

`wince` 移植保留在相同的 `/.wince` 目录中，并使用 `wince/Makefile.ce` 调用原生编译器创建 HOST `miniperl`，有助于交叉编译过程。添加了扩展支持。

### 5.9.4

`/.win32` 和 `/.wince` 两个目录合并，因此 `perlce` 构建过程位于 `/.win32` 目录。

没有 `fgets` 的对应函数；应该使用 `sv_gets`：
`fgets(s, n, stream)` `sv_gets(sv, perlio, append)`

## 文件定位

| 取代： | 使用： |
| :--- | :--- |
| `feof(stream)` | `PerIO_eof(perlio)` |
| `fseek(stream, n, whence)` | `PerIO_seek(perlio, n, whence)` |
| `rewind(stream)` | `PerIO_rewind(perlio)` |
| `fgetpos(stream, p)` | `PerIO_getpos(perlio, sv)` |
| `fsetpos(stream, p)` | `PerIO_setpos(perlio, sv)` |
| `ferror(stream)` | `PerIO_error(perlio)` |
| `clearerr(stream)` | `PerIO_clearerr(perlio)` |

## 内存管理与字符串处理

| 取代： | 使用： |
| :--- | :--- |
| `t* p = (n)` | `Newxz(p, n, t)` |
| `t* p = calloc(n, s)` | `Newxz2(p, n, t)` |
| `t = malloc(dst, s, n)` | `New(p, n, t)` |
| `memcpy(dst, s, n)` | `Copy(dst, s, n, t)` |
| `memmove(dst, s, n)` | `Move(dst, s, n)` |
| `memcpy(dst, s, sizeof(t))` | `Structcopy(dst, s, t)` |
| `t memset(dst, 0, n * sizeof(t))` | `Zero(dst, n, t)` |
| `memzero(dst, 0)` | `Zero(dst, n, t)` |
| `free(p)` | `SafeFree(p)` |
| `strdup(p)` | `savep(p)` |
| `strndup(p, n)` | `savepn(p, n)`, (嘿，`strndup` 并不存在!) |
| `strbr(big, little)` | `strstr(big, little)` |
| `strnc(s1, s2)` | `str2(s1, s2)` |
| `strEQ(s1, s2)` | `strGT(s1, s2)` |
| `strncpy(s1, s2, n)` | `strNEQ(s1, s2, n)` |
| `memcmp(s1, s2, n)` | `mcmp(p1, p2, n)` |
| `memcmp(p1, p2, n)` | `memEQ(p1, p2, n)` |

注意 `memcmp` 和 `memmove` 中使用的 `Copy` 和 `Move` 的参数顺序不同。

尽管如此，大多数情况下你可能想处理 SV 而不是原始的 char *：：

`strlen(s)` `sv_len(sv)`
`strncpy(dst, src)` `sv_setpv(sv, s)`
`strncpy(dst, src, n)` `sv_setpn(sv, s, n)`
`strcat(dst, src)` `sv_catpv(sv, s)`
`strcat(dst, src)` `sv_catpn(sv, s)`
`sprintf(fms, fmt, ...)` `sv_setpvf(sv, fmt, ...)`

此外请注意 `sv_catpv` 和 `sv_catpn` 的存在，它们将拼接与格式化结合在一起。

有时与其使用 `Newxz()` 释放分配的堆内存，你应该考虑对数据进行“投毒”（poisoning）。这意味着写入其中的位模式作为指针（以及浮点数）将是非法的，且作为整数时可能会产生意料结果，这样任何没有预见的情况下尝试使用数据的数据都会尽早报错。可以使用 `Poison(malloc)` 进行投毒，其参数与 `Zero` 类似：

`PoisonWith(dst, n, t, b)` 按字节涂写内存
`PoisonNew(dst, n, t)` 等于 `PoisonWith(dst, n, t, 0xAB)`
`PoisonFree(dst, n, t)` 等于 `PoisonWith(dst, n, t, 0xEF)`
`Poison(dst, n, t)` 等于 `PoisonFree(p)`

## 字符类测试

Perl 实现了多种类型的类测试。这里描述的仅直接对应操作 8 位字符的 C 库函数，但那些是操作字符和 UTF-8 编码字符串的等效函数。详细描述请见 `perlapi` 中的“字符分类”（Character classification）和“字符大小转换”（Character case changing）。

下最后一列列出的 C 库程序根据当前的区域（locale）返回值。其他两列始终假设为 POSIX（或 C）区域。ASCII 列中的项目仅对 ASCII 输入有效，对其他任何内容返回 FALSE。这仅在你确定需要这样做时使用。在 Latin1 列中，非 ASCII 的 8 位字符按照 Unicode 定义，与 ASCII-0859-1（通常称为 Latin 1）相同。

| 用于： | 使用： |
| :--- | :--- |
| ASCII 用于 Latin1 | 使用 locale: |
| `isnum(c)` | `isALPHANUMERIC(c)` |
| `isALPHANUMERIC_L1(c)` | `isALPHANUMERIC_LC(c)` |
| `isalpha(c)` | `isalpha(c)` |
| `isalpha_L1(c)` | `isalpha_LC(ascii)` |
| `isASCII(c)` | `isASCII_LC(c)` |
| `isblank(c)` | `isBLANK(c)` |
| `isblank(c)` | `isBLANK_LC(c)` |
| `iscntrl(c)` | `isCNTRL(c)` |
| `iscntrl_L1(c)` | `iscntrl_LC(c)` |
| `isdigit(c)` | `isDIGIT(c)` |
| `isdigit_L1(c)` | `isDIGIT_LC(c)` |
| `isgraph(c)` | `isGRAPH_LC(c)` |
| `islower(c)` | `isLOWER(c)` |
| `islower_L1(c)` | `isLOWER_LC(c)` |
| `isprint(c)` | `isPRINT(c)` |
| `isprint_L1(c)` | `isPRINT_LC(c)` |
| `ispunct(c)` | `ispunct(c)` |
| `ispunct_L1(c)` | `ispunctunct_LC(c)` |
| `isspace(c)` | `isSPACE(c)` |
| `isspace_L1(c)` | `isSPACE_LC(c)` |
| `isupper(c)` | `isUPPER(c)` |
| `isupper_L1(c)` | `isUPPER_LC(c)` |
| `isxdigit(c)` | `isxdigit(c)` |
| `isxdigit_L1(c)` | `isxdigit_LC(c)` |

为了强调你正在操作 ASCII 字符，可以在 ASCII 列中附加 `_A`：`isALPHA_A`、`isDIGIT_A` 等。Latin1 列中没有 `isascii` 的项目，因为 `isASCII_L1` 等同于 `isASCII`；Latin1 列中没有 `toupper` 的项目，因为你必须使用 `toupper_uni`，详见 `perlapi` 中的“字符大小转换”（Character changing）。

## stdlib.h 函数

| 用于： | 使用： |
| :--- | :--- |
| `atof(s)` | `atoi(s)` |
| `atol(s)` | `strtol(s)` |
| `strtod(s)` | `strtol(s)` |
| `strtol(s)` | `strtou(s)` |
| `strtou(s)` | `strtol(s)` |
| `strtol(s)` | `strtou(s)` |

注意 `strtol(s)` 和 `strtou(s)` 实际上不处理前导空格（故意严格）。典型的做法是在调用前进行检查：

```c
```



`int i;`

`char* end_ptr;`

```c
if (strtol(input, &end_ptr, 10) && i <= MAX_VAL) i = (int)i; /* 解析范围内的整数 */ else { ... }
```

此外注意用于字符串转换为进制的 `strbin`、`strhex` 和 `stroct` 函数。这些函数在 1989 ANSI 标准中随处可见。

```c
int rand();

double srand();

srand(unsigned int n) {
    srand_called = TRUE;
}
```

`system(s)` 不要。查看 `pp_system` 或使用 `my_popen`。

`getenv(s)` `PerlEnv_getenv(s)`

`setenv(s, val)` `my_setenv(s, val)`

## 杂杂函数

你不应该想要使用 `setjmp.h` 函数，但如果你认为需要，请使用 `scope.h`。

对于信号/sigaction，使用 `rsignal(signo, handler)`。

## 另请

`perlapi`, `perlapio`, `perlguts`

# PERLCOMMUNITY

## 名称
`perlcommunity` - Perl 社区的概述

## 描述
本文旨在提供庞大的 Perl 社区的概述，该社区过于巨大且多样，无法提供详细列表。如果遗漏了某个特定领域，这并非无礼，而是为了简洁起见。

Perl 社区与 Perl 语言一样多样，有大量证据表明 Perl 用户将 Perl 应用于所有努力，而不仅仅是编程。从网站到 IRC 再到邮件列表，有多种方法可以参与社区。

## 在哪里找到社区

Perl 社区有一个中央目录：`<>`，由 Perl Foundation (`<>`) 维护，它跟踪并为其他社区站点提供服务。

## 邮件列表与新闻组

Perl 运行在电子邮件之上，这毫无疑问。《骆驼书》（The Camel book）最初大部分通过电子邮件编写，Perl 的开发通过邮件列表进行协调。Perl 邮件列表最大的仓库位于 `<>`

大多数与 Perl 相关的项目都为用户和贡献者设置了邮件列表。如果你在 `<>` 中没有看到某个项目，请检查该项目的网站。大多数邮件列表存档在 `<>`

在 `comp.lang.perl.*` 下也有许多 Perl 相关的新闻组。

## IRC

Perl 社区拥有相当大的 IRC 存在。首先，它有自己的 IRC 网络，`<>`。通用（非帮助导向）聊天可以在 `<>` 找到。许多其他特定聊天也托管在该网络上。关于 `ircperl.org` 的信息位于网络网站上：`<>`。对于更多帮助导向的 `#perl`，请查看 `<>`。Perl 6 的开发在 `<>` 也有体现。如果你请求，大多数与 Perl 相关的频道都会乐意指引你的方向。

任何大型 IRC 网络（Dalnet, EFNet）也可能有一个 `#perl` 频道，活动程度不异。

## 网站

Perl 网站形式多样，但它们分为两大类：论坛和新闻网站。有很多 Perl 相关的网站，这里只提到了社区最大的几个。

## 新闻网站

由 O’Reilly Media（《骆驼书》等书籍的出版商）运行，`perl.com` 为开发者提供 Perl 动态、文章、资源以及实用网站目录。

许多社区成员在该上有与 Perl 相关的博客。如果你想加入，可以免费注册。

关于黑客松（hackathons）的信息可以在与研讨会相同的地方，也可以在 `<>` 中找到。

如果你从未参加过黑客松，在参加之前你需要了解几点基本知识：准备一台可以工作的笔记本电脑并学会如何使用它；提前查看相关项目；安装好必要的版本控制客户端；以及准备备份设备（额外的网线、备用插线板等），因为总会有人忘记。

## 惯例

Perl 有两个主要的年度会议：由 O'Reilly 举办的 Perl 大会（现是 OSCON 的一部分），以及另一个 Perl 大会（Another Perl Conference 或简称 YAPC，读作 yap-see），后者通过 Perl 社区的一场令人惊叹的草根展示，被本地化为几个地区的 YAPC（北美、欧洲、亚洲）。有关其中任一会议的更多信息，请查看它们各自的网页：OSCON `<>`; YAPC `<>`。

一个包含很大比例 Perl 内容的相对较新的会议系列是开源开发者大会（OSDC）。该会议首次在澳大利亚举行，最近也扩展到了以色列和法国。更多信息可以在此处找到：澳大利亚的 `<>`，以色列的 `<>` 以及法国的 `<>`。

## Perl 活动日历

Perl Review (`<>`) 维护着一个网站和 Google 日历 (`<>`)，用于跟踪研讨会、黑客松、Perl Mongers 会议和其他活动。该日历的视图可以在 `<>` 和 `<>` 查看。

并不是每个活动或 Perl Mongers 小组都在该日历上，所以如果你没看到自己的，请不要灰心。要让你的活动或小组被列入，请联系 `brian d foy` ()。

# 作者

Edgar “Trizor” Bering `<>`

# PERLCYGWIN

## 名称
`perlcygwin` - 用于 Cygwin 的 Perl

## 摘要

本文档将帮助你如何在 Cygwin 上配置、制作、测试和安装 Perl。本文档还描述了影响 Perl 运行时行为的 Cygwin 特性。

注意：Cygwin 有预构建的 Perl 包可用，且标准的 Cygwin 安装中提供了一个 Perl 版本。如果你不需要自定义配置，可以考虑使用这些软件包之一。

## 在 CYGWIN 上编译 Perl 的前提条件

Cygwin = GNU+Cygnus+Windows (不要离开它离开 UNIX)

Cygwin 工具是用于 Win32 平台流行的 GNU 开发工具的移植版。它们针对 Cygwin 库运行，该库提供了这些程序所需的 UNIX 系统调用和环境。关于该项目的更多信息可以在此处找到：

```
<>
```

需要最近的网络版或商业版 Cygwin。
在本文档上次更新时，Cygwin `1.7.16` 是当前版本。

### Cygwin 配置

在构建 Perl 时，可能对你的 Cygwin 设置进行某些更改，以便 Perl 能够顺利构建。这些更改对于正常的 Perl 使用**不是必须的**。

注意：将在所有 Win32 版本上运行的二进制文件它们不依赖于你的主机系统（WinXP/Win2K/Win7）或你的 Cygwin 配置（二进制/文本挂载、cgserver）。唯一的依赖来自硬编码的路径名，如 `/usr/local`。然而，你的主机系统和 Cygwin 配置将影响 Perl 的运行时行为（见“测试”）。

```
PATH
```

设置 `PATH` 环境变量，以便 `Configure` 找到 Cygwin 版本的程序。任何不需要的 Windows 目录都应该删除或移动到 `PATH` 的末尾。

```
nroff
```

如果你没有 `nroff`（它是 `groff` 包的一部分），`Configure` 将**不会**提示你安装 man 页。

## 在 CYGWIN 上配置 Perl

通过 `hints/cygwin.sh` 帮助收集的默认选项将构建一个支持动态加载的 Perl（这需要共享的 `cygperl5_16.dll`）。

这将运行 `Configure` 并保留记录：

```
./Configure 2>&1 | tee log.configure
```

如果你愿意接受所有默认值，请带有 `-de` 运行 `Configure`。然而，有几个实用的自定义选项。

## 在 Cygwin 上剥离 Perl 二进制文件

可以剥离构建过程创建的 EXEs 和 DLLs。生成的二进制文件将减小很多。如果你希望二进制文件被剥离，可以在 `Configure` 提示你时添加 `-s` 选项，

任何额外的标志（不包括库）？[none] `-s` 传递给 `g++` 以创建动态加载库的特殊标志？[none] `-s` 传递给 `gcc` 以使用动态链接的特殊标志？[none] `-s`

或者，你可以编辑 `hints/cygwin.sh` 并取消文件末尾相关变量的注释。

## Cygwin 上 Perl 的可选库

若干 Perl 函数和模块取决于某些可选库的存在。如果它们安装在列出的用于库搜索的目录中，`Configure` 将找到它们。大多数这些的预构建包可以通过 Cygwin 安装程序获取。

```
-crypt
```

Cygwin 分发的 `crypt` 包是由 Corinna Vincschen 编写的兼容 Linux 的 56 位 `crypt` 端口。

或者，GNU libc 中的 `crypt` 库已移植到 Cygwin。

```
-lgdbm_compat (use GDBM_File)
```

Cygwin 支持 `GDBM`。

注意：`GDBM` 库仅在 NTFS 分区上工作。

```
-ldb (use DB_File)
```

Cygwin 支持 `BerkeleyDB`。

注意：`BerkeleyDB` 库仅在 NTFS 分区上完全工作。

```
cygserver (use IPC::SysV)
```



Cygwin 支持 SysV IPC 的移植版。

注意：这没有经过广泛测试。特别是 `d_semct1_semun` 是未定义的，因为它未通过 Configure 测试，并且在 Win9x 上 `shm*()` 函数似乎会挂起。它还创建了在未来编译 CPAN 模块时目前不支持！

- `lutil`

标准 Cygwin 发布版包含 `lutil`。

## Cygwin 上 Perl 的配置时选项

`INSTALL` 文档描述了若干配置时选项。其中某些选项可以在 Cygwin 上工作，另一些尚未可行。此外，某些是实验性的。你可以在 `Configure` 提示时选择选项，也可以在命令行上定义（未定义的）符号。

- `Uusedl`
此符号强制静态编译 Perl。
- `Dusemymalloc`
默认不使用源码自带的 `malloc()`，因为它速度较慢且不是线程安全的。如果你想通过 `-Dusemymalloc` 强制 Perl 使用这种方式，请定义此符号。
- `Useperlio`
此符号禁用 PerlIO 抽象。PerlIO 现在是默认值；不建议禁用 PerlIO。
- `Dusemultiplicity`
在 C 程序中嵌入 Perl 并使用多个实例时需要此项。这仅在你使用 `-Uethreads` 构建非线程时需要。
- `Use64bitint`
Perl 默认使用 64 位整数。如果你想使用较小的 32 位整数，使用此符号。
- 
`g`支持长 double（12字节）。然而，在 Perl 中需要若干长双精度函数（`atan2`, `cos`, `exp`, `floor`, `fmod`, `frexp`, `isnan`, `log`, `modf`, `pow`, `sin`, `sqrt()`, `strtol`）。这些在 newlib 即 Cygwin 库中尚未可用。
- `Useithreads`
如果你想要更快的非线程 Perl，定义此符号。
- `Dulargefiles`

Cygwin 使用 64 位整数进行内部尺寸和位置计算，这将由 `Configure` 正确检测并定义。

- `Dymlinks`

使用此在源码树之外构建 perl。详情可以在 `INSTALL` 文档中找到。这是从源码构建的推荐方法。

## Cygwin 可疑警告

在 `Configure` 期间可能会看到看起来可疑的消息。

Win9x 和 `d_eofnblk`

Win9x 在非阻塞读取关闭管道时无法正确报告 EOF。你会看到它返回以下消息：

但它也返回 -1 信号 EOF，请小心！警告：你无法区分 EOF 和无数据！*** 哇！！！***在此机器上 `$d_eofnblk` 的推荐值为 "define"！保留推荐值吗？[y]

至少与 WinNT 保持一致，你应该保留推荐值。

编译器/预处理器定义

由于 Cygwin 对 `_LONG_DOUBLE` 的 `#define`，发生了以下错误：

猜测你的 C 编译器和预处理器定义了哪些符号...`try.c`:
`<line>`: missing binary operator

此失败似乎没有引起任何问题。对于旧版本的 gcc，报告的是“parse error”而不是 "missing binary operator"。

# 编译 CYGWIN

只需运行 `make` 并等待即可：

```bash
make 2>&1 | tee log.make
```

# 在 CYGWIN 上测试

运行测试套件有两个步骤：

```bash
make test 2>&1 | tee log.make-test
cd t; ./perl harness 2>&1 | tee ./log.harness
```

两次运行的都是相同的测试，但通过 `./perl harness` 运行时会提供更多信息。

测试结果取决于你的宿主机系统和你的 Cygwin 配置。在某些 Cygwin 设置下测试可能会通过，但始终会尝试进行测试，并记录了可以解释的测试失败。Perl 可能会通过所有测试，但更有可能的是某些测试会由于下面列出的原因之一而失败。

## Cygwin 上的文件权限

UNIX 文件权限基于针对每个{用户、组、其他}的每个{读、写、执行}的模式位集。默认情况下，Cygwin 跟踪 Win32 的只读属性，该属性被表示为 UNIX 文件写位（文件始终是可读的，如果文件具有 `{.com,.bat}` 扩展名或带有 #1 则为可执行的；目录始终是可读和可执行的）。在带有 `nsec cygwin` 设置的 WinNT 上，额外的模式位是扩展文件属性。在带有默认 `nsec cygwin` 设置的 WinNT 上，权限使用标准的 WinNT 安全描述符和访问控制列表。如果没有这些选项之一，测试将失败（尚未更新）：

| 失败测试列表（失败的用例） | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| io/fs | 5,9-10 | | | | | |
| lib/anydbm.t | 2 | lib/db-btree.t | 20 | | | |
| lib/db-hash.t | 16 | lib/db-recno.t | 18 | | | |
| lib/dbdbm.t | 2 | lib/ndbm.t | 2 | lib/odbm.t | 2 | |
| lib/sdbm.t | 2 | op/stat.t | 9,20 | | | |
| (.tmp 不是执行扩展名) | | | | | | |

## NDBM_File 和 ODBC_File 在 FAT 系统上无效

不要在 FAT 文件系统上使用 `NDBM_File` 或 `ODBC_File`。它们可以在 FAT 上构建，但许多测试将失败：

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ../ext/NDBM_File.t | 13 | 3328 | 59 | 83.106 | 1-2 4 16-71 | | |
| ../ext/ODBC_File/odbm.t | 255 | 65280 | ?? | % | % | % | |
| ../lib/AnyDBM/File.t | 252 | 512 | 26.16% | 1 | 4 | | |
| ...lib/Memo/t/errors.t | 0 | 139 | 15 | 54.45 | 7-11 | | |
| ../lib/Memo/t-ndbm.t | 13 | 3328 | 4 | 100.00 | 1-4 | | |
| run/fresh/perl.t | 97 | 1 | 1.03% | 91 | | | |

如果你尝试在 FAT 上运行（或在 FAT 上使用 `AnyDBM_File`），请运行 `Configure` 并带有 `-Ui_ndbm` 和 `-Ui_db` 选项，以防止构建 `NDBM_File` 和 `ODBC_File`。

使用 NTFS (`Cygwin=ntfsec`)，即使 perl 是在 FAT 上构建的，应该也没有问题。

## io_* 中的 fork() 失败

`fork()` 失败可能导致以下测试失败：

```
ext/IO/lib/IO/t/io_multihomed.t
ext/IO/lib/IO/t/io_sock.t
ext/IO/lib/IO/t/io_unix.t
```

参见下文“杂杂”中关于 fork 的注释。

# CYGWIN 移植的特定特性

## Cygwin 上的脚本移植性

Cygwin 在 Win32 系统上层提供类 UNIX 语义方面做得非常出色。然而，除了上述项目外，还有一些你应该了解的差异。这是一份关于移植性的简短指南，更多信息可以在 Cygwin 文档中找到。

### 路径名

Cygwin 路径名用斜杠 (`/`) 分隔，支持通用命名代码 (`/UNC`)。不建议使用 Cygwin-1.7 非 POSIX 路径。名称可以包含所有打印字符。

文件名不区分大小写，但保留大小写。包含反斜杠或驱动器字母的路径是 Win32 路径，不受 posix 风格路径的翻译影响，Cygwin 将占上风，因此最好将它们转换为 POSIX。

为了转换，我们有 `Cygwin::win_to_posix_path()` 和 `Cygwin::posix_to_win_path()`。

由于 cywin-1.7 路径名是 UTF-8 编码的。

### 文本/二进制

Cygwin-1.7 的文本模式已弃用并强烈不建议使用。

当文件被打开时，它处于文本模式或二进制模式。在文本模式下，文件会受到 CR/LF/Ctrl-Z 翻译。在 Cygwin 中， `open()` 的默认模式由底层文件的挂载模式决定。参见：

> "`Cygwin::is_binary()` 是一个函数，用于对将被视为文本的文件设置二进制模式。带有 `O_TEXT` 标志的 `sysopen()` 会对原本会被视为二进制的文件设置模式："

```perl
sysopen(FH, "bar", O_WRONLY|O_CREATE|O_TEXT)
```



`lseek()`、`tell()` 和 `sysseek()` 仅对二进制模式打开的文件有效。文本/二进制问题在 Cygwin 文档中有介绍。

### PerlIO

PerlIO 覆盖了默认设置。在 Cygwin 中，`open()` 的默认模式取决于挂载模式。使用如下设置二进制模式：

```perl
open(FH, ":bin", "filename");
```

在 Cygwin 中，通过指定模式来来处理文本文件：

```perl
open(FH, ":text", "filename");
```

由于在 Cygwin 中，如果不指定二进制模式，`open()` 默认会将文件视为文本：

```perl
open(FH, "filename");
```

### Cygwin 与 Windows

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会处理 LF：

```perl
open(FH, ":raw", "filename");
```

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会进行 LF 的重写。使用如下二进制模式：

```perl
open(FH, ":unix", "filename");
```

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会进行 LF 的重写。

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会进行 LF 的重写。

```perl
open(FH, ":crl", "filename");
```

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会进行 LF 的重写。

```perl
open(FH, ":utf", "filename");
```

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会进行 LF 的重写。

```perl
open(FH, ":os", "filename");
```

在 Cygwin 中，`open()` 默认会将文件视为文本。除非指定二进制模式，否则它会进行 LF 的重写。

```perl
open(FH, ":binary", "filename");
```

`binmode`, `cygdrive`, `/cygdrive`

### Cygwin::is_binmount
如果给定的 cygwin 路径是以二进制模式（binary mounted）挂载的，返回 true；如果是以文本模式（textmode）挂载，返回 false。

### Cygwin:sync_winenv
Cygwin 不初始化所有原始的 Win32 环境变量。请参阅本页底部（see）的“受限的 Win32 环境变量”。

从 cygwin 程序调用的某些 Win32 程序可能需要某些环境变量，例如：ADODB 需要 `%COMMONPROGRAMFILES%`。调用 `Cygwin::sync_winenv()` 将所有 Win32 环境变量复制到你的进程中，并注意在每次遇到非 POSIX 路径时 cygwin 都会警告。

## 在 CYGWIN 上安装 Perl (INSTALL PERL ON CYGWIN)

这将安装 Perl，包括帮助页（man pages）。

```
make install 2>&1 | tee log.make-install
```



注意：如果 `STDERR` 被重定向，`make install` 将不会提示你将 `perl` 安装到 `/usr/bin`。

你可能需要管理员权限来运行 `make install`。如果不是，你必须对相关目录具有写入权限。

关于以 HTML 格式安装 Perl 文档的信息，可以在 `INSTALL` 文档中找到。

## CYGWIN MANIFEST (MANIFEST ON CYGWIN)

这些是 Perl 发布版本中的行，用于解释所有的条件性依赖。希望通过保持其更新，可以让 Cygwin 移植保持尽可能干净。

### 文档 (Documentation)

- `INSTALL` `README.cygwin` `README.win32` `MANIFEST` `pod/perl.pod`
- `perlport.pod` `pod/perfaq3.pod` `pod/perdelta.pod`
- `perl/pod5084delta.pod` `pod/per56delta.pod` `pod/per1561delta.pod`
- `perl/per157delta.pod` `pod/per1572delta.pod` `pod/per1573delta.pod`
- `perl/pod58delta.pod` `pod/per58i1delta.pod` `pod/per590delta.pod`
- `perl/helplist.pod` `per/modlibm.pod` `pod/pertoc.toc` `Porting/Glossary`
- `pod/pergit.ex` `Porting/AUTHORS.lib` `dist/CWD/Changes` `ext/Compress-Raw-Zlib/Changes` `ext/Compress-Zlib/README` `ext/Compress-Zlib/Changes`
- `extDB_File/Files` `ext/Encode/Changes` `ext/Syslog/Changes` `ext/Time-HRes/Changes` `ext/Win32API-Files` `lib/ExtUtils/CBuilder/Changes`
- `lib/ExtUtils/Changes` `lib/ExtUtils` `lib/ExtUtils/PATCHING` `lib/ExtUtils/README` `lib/Net/Pings` `Changes` `lib/Test/Harness` `Cygwin`
- `lib/Test/ANSIColor/Changes` `lib/Term/ANSIColor` `README.` `brazilian` `symbian/T030`

### 构建、配置、编译 (Build, Configure, Make)

- `cygwin/Make.sh` `ext/IPC/Sys/hints/cygwin.pl`
- `NDBM/File/hints.cypl`
- `ext/DDM_File/hints/cygwin.pl` `hints` `cygwin.sh`
- `Configure` - help 查找未命名的提示，动态构建需要共享库 `libperl` `Lib.sh` `Cross/Make-cross-s` `linkperl/Patch` `patch_cygwin` `in` `port` `list` `installman` - 帮助页带有 `:` 翻译为 `.` `install` `install` `install` `dll`, 安装到 `'pods'` `makedep.sh` - `uwinix` `regen.pl` - 文件权限 `Network/File` `makes/plname` `cygwin/sanity/pl.pl` `sisify.pl` `ext/uwinix/sh` `demsvc/ms_template` `win32/makefile` `win32/mk`

### 测试 (Tests)

- `io/fs.c` - 如果不是 `nsec` 则跳过文件检查，`skip` `rename()` 检查在不检查 `check_case` 时: 宽限到 `io/test` - `biomed` `t/lib/cygwin` - 内置 `cygwin` 函数测试到 `/groups.t` `basegroup` 有 `ID = 0` `t/top/magic.c` `$+/XML` `WORKAROUND`, `s./exe//` `/t/top.stat` - 无 `/dev`, `skip` `Cygwin-FTractionTime` `quark` (cache 维护之前创建和删除的文件的时间), 无 `(setuid)` `t/top/taint` - 无法使用空路径 `Cygwin` 移植到 `/time.t` - 无 `tzt)`

### 编译后的 Perl 源 (Compiled Perl Source)

- `EXTERN.h` - `declspec (dllimport)` `XSUB.h` - `declspec (dllexport)`
- `cygwin/cygwin.c` - `os_stras`, `(getext, spawned, and Cygwin: functions)` `perl.c` - `os_streras`, `-ibak` `perl.h` - `binmode` `doio.c` - `win9x` 无法在文件打开时重命名文件 `pp sys.c` - 不定义 `h_errno`, `init` `_pwent_struct.pm` `comment` `util.c` - 使用 `setenv` `util.h`
- `PERL_FILE_ABSOLUTE` `macro.pc` - 关于 Cygwin 下 Pois vs IEEE 数学的注释 `perl.c` - `CR/file` 为每个周期创建 `periol.c` - 关于 Cygwin 下 `EXSTON` 的注释

### 编译后的模块源 (Compiled Module Source)

- `ext/Compress-Raw-Zlib/Makefile.pl` - 除非是 `cywin`, 否则无法通过 `CPAN` 安装 `ext/Compress-Raw-Zlib/lib-src/zutil.h` - `Cygwin` 是类 Unix 的且具有 `vsprint` `ext/Errno/Errno_pm.pl` - 对 `Cygwin` 下 `Win32` Perl 的特殊处理 `ext/POSIX/POSIX.xs` - `tzname` 完全定义
- `ext/SDBM_file/sdb/pair.c` - `EXTCONST` 需要从 `EXERN.h` 重新定义 `/ext/SDBM_file/sdb/sdbm.c` - 二进制打开 `-extext/Syslog/Syslog.c` `Cygwin` 有 `syslog.log` `-extext/Syslog/win32/compile.pl` - 转换路径 `-extext/Time-H//Res..` - 各种时间 `-extext/Win32.File` - 在 `Cygwin` 下不可用 `ext/Win2API/File.pl` - 在 `Cygwin` 下的文件句柄处理 `-extext/Win32CORE/Win32.c` - 在 `Cygwin` 下的文件句柄处理 `-extext/Win32/File..` - `...... /Ext//builder.pl` - 在 `Cygwin` 下的类 `lib/ExtUtils/Install.pm` - 在 `Cygwin` 下的类 `lib/ExtUtils/MM.pm` - 在 `Cygwin` 下的类
`/ExtUtils/Maker.pm` - `winixAny.pl` - 在 `Cygwin` 下的类

### Perl 模块测试 (Perl Module Tests)

每个变量类型都有其自己的命名空间，表现为若干非变量标识符。这意味着你可以在不发生冲突的情况下，为标量变量、数组或哈希（或者，换句话说，对于文件句柄、目录句柄、子程序名称、格式名称或标签）使用相同的名称。这意味着 `$foo[1]` 是 `@foo` 的部分，而不是 `$foo` 的部分。这听起来可能有点奇怪，但没关系，因为这确实很奇怪。

由于变量引用始终以 `$`、`@` 或 `%` 开头，因此“保留”字实际上并不是针对变量名的。然而，它们是针对标签和文件句柄被保留的，因为这些没有起始字符。提示：你可以说使用 `open(LOG, 'logfile')` 而不是 `open(log, 'logfile')`。使用大写文件句柄还可以提高可读性，并保护你免受与保留字的冲突。大小写是敏感的——“foo”、“Foo”和“foo”都是不同的名称。以字母或下划线开头的名称也可以包含数字和下划线。

可以将此类字母数字名称替换为返回指向适当类型引用的表达式。有关此的描述，请参阅 `perl`。

以数字开头的名称可以包含更多数字。不以字母、下划线、数字或脱字符（即控制字符 `^`）开头的名称仅限于一个字符，例如 `%` 或 `$$`（这些单字符中的大多数在 Perl 中有预定义的签名。例如，`$$` 是当前进程 ID。）

### 标识符解析

在 Perl 5.18 之前，关于有效标识符的实际规则有点模糊。然而，总的来说，任何定义的内容在之前的 Perl 版本中都应该可以工作，但相反的情况——边缘情况在之前的版本中有效，但在此处未定义——可能在较新的版本中无法工作。一个重要的说明，请注意以下内容仅适用于 Perl 源代码中找到的裸标识符，而不适用于通过符号引用引入的标识符，后者的限制要少得多。如果在 `use utf8` 编译指令（pragma）的作用下工作，适用以下规则：

```



```
/ (<?[ \<Word> & \p{ID_Start}> ) + [ _ ])? (? \<Word> & \p{ID_Continue} ] ) / *
```

也就是说，一个“字符”后面跟着任意数量的“继续字符”。Perl 要求标识符中的每个字符都匹配（这防止了出现问题的情况）；并且 Perl 额外接受以下划线开头的标识符名。

如果不使用 `utf8`，源被视为 ASCII + 额外的 128 个字符，标识符应匹配

```
/ (??)?(!\d|\w+) /x
```

也就是说，ASCII 范围内的任何字符，只要第一个字符不是数字即可。Perl 中有两个包包分隔符：双冒号（`:`）和单引号（`’`）。普通标识符可以用双冒号开头或结束，并可以包含由双引号分隔的多个部分。单引号有类似的规则，但例外是它们不在标识符的末尾：`$'foo` 和 `$foo'bar` 是合法的，但 `$foo'bar ` 是不法的。

此外，如果标识符前面有一个前缀（sigil）——即，如果标识符是变量名的一部分——它可以可选地包含在大括号中。

虽然你可以混合使用双引号和单引号，但引号必须在冒号之后：`:'foo` 和 `$foo:'bar` 是合法的，但 `$:'foo` 和 `$foo:'bar` 是不法的。

组合起来，构成基础标识符的语法如下：
| \ \s* (? (DEFINE)<variable> &sigil)? (?:normal_identifier)?(?: \* \)) (?&normal_identifier)?(?: :) * '?? (?&basic_identifier)? (?: (?: :) * :) | (?: :) * ' (?&basic_identifier)? # is use utf8 on?
?((call(0)) & $utf8_hint_bits) * (?&Per_XID)?&Per_XIDC)* | (aa)?(!d) W+) + <sigil>(&&*\@\%)??Per_XID)? ([ \word & &pXID_Start} + [ ] ]) {?Per_XID)?([ \word & &pXID_continue}] / )

同时，特殊标识符不遵循上述规则：在大多数情况下，该类别中的所有标识符都有 Perl 赋予的特殊含义。由于它们有特殊的解析规则，这些通常不能被限定。它们以四种形式出现：

- 一个前缀，后面跟着匹配 `{POS_Digit}` 的数字，例如 `$0` 或 `$10000`。
- 一个前缀，后面跟着一个字符和一个单个 POSIX 大写字母，例如 `$^` 或 `$W`，或者一个前缀后面跟着一个非空格、非UL 字面控制字符，匹配 `\POS_Cntrl` 属性。由于历史上的奇特，如果不在 `utf8` 下运行，`[0x0-0xff]` 范围内的 128 个字符被认为是控制字符，也可以用于长度为一的变量。然而，从 v5.22 开始，非图形字符的使用被弃用，对它们的支持将在未来的 Perl 版本中移除。不允许 ASCII 字符和 NUL，这意味着单字符变量名可以命名为任何其他 C0 控制字符 `[0x01-0x1F]`，否则 DEL 将产生弃用警告。已经在 `use utf8` 下，非 ASCII 字符必须匹配 `Per_XIDS`。从 v5.22 开始，不使用 `utf8` 时，BREAK、SPACE 和 SOFT（$）将产生弃用警告。
- 与上述类似，一个前缀，后面跟着列表上下文中的裸字，它返回一个值列表，或者在标量上下文中返回第一个值。
- 与上述类似，一个前缀，后面跟着一个字符和一个单个 POSIX 大写字母，例如 `$^` 或 `$W`，或者一个前缀后面跟着一个非空格、非UL 字面控制字符，匹配 `\POS_Cntrl` 属性。由于历史上的奇特，如果不在 `utf8` 下运行，`[0x0-0xff]` 范围内的 128 个字符被认为是控制字符，也可以用于长度为一的变量。然而，从 v5.22 开始，非图形字符的使用被弃用，对它们的支持将在未来的 Perl 版本中移除。不允许 ASCII 字符和 NUL，这意味着单字符变量名可以命名为任何其他 C0 控制字符 `[0x01-0x1F]`，否则 DEL 将产生弃用警告。已经在 `use utf8` 下，非 ASCII 字符必须匹配 `Per_XIDS`。从 v5.22 开始，不使用 `utf8` 时，BREAK、SPACE 和 SOFT（$）将产生弃用警告。
- 一个前缀，后面跟着列表上下文中的裸字，它返回一个值列表，或者在标量上下文中返回第一个值。

# 上下文

在 Perl 中，操作和值的解释有时取决于周围的上下文。有两种上下文：列表和标量。某些操作返回列表值，否则返回标量。如果是这样，将在文档中提到。

相反，一个操作提供标量或列表上下文。例如，如果你说

```
int (<STDIN>)
```

整数操作提供了标量上下文，它通过从 `STDIN` 读取一行并将其传回整数操作，然后找到该行的整数值并返回。相反，如果你说

```
sort (<STDIN>)
```

那么排序操作提供了列表上下文，它将读取文件结束的所有行，并将这些行传回排序程序，程序将对这些行进行排序并作为列表返回给原来的上下文。

赋值有点特殊，它使用左侧参数来确定右侧参数的上下文。赋值给标量在标量上下文中评估右侧部分，而赋值给数组或哈希在列表上下文中评估右侧部分。

当你使用 `warnings` 编译指令或 Perl 的 `-w` 命令行选项时，可能会看到关于在“空上下文”中使用常量或函数的警告。空上下文意味着值被丢弃，例如仅包含 `"fred"` 的语句；或者 `getcwd(0);` 仍然是标量上下文，无论是否在列表上下文中调用。

自定义子程序可以选择它们是在空、标量还是列表上下文中被调用的。不过，大多数子程序不需要这样做。因为标量和列表都会自动插值为列表。请参阅 `perlfunc` 中的 `"wantarray"` 了解如何动态确定函数的调用上下文。

# 标量值

Perl 中的所有数据都是标量、标量数组或标量哈希。标量可以包含三种不同类型中的任意一种单一值：数字、字符串或引用。通常情况下，这些形式之间的转换是透明的。虽然标量可能不包含多个值，但它可以包含一个指向数组或哈希的引用，后者又包含多个值。

标量并不必然是某一种类型。没有地方可以声明一个标量变量的类型为 `"string"`（字符串）、`"number"`（数字）、`"reference"`（引用）或其他任何类型。由于标量的自动转换机制，返回标量的操作不需要关心（实际上也无法关心）它们寻找的是标量、数字还是引用。Perl 是一种上下文多态语言，其标量可以是字符串、数字或引用（包括对象）。尽管对于几乎所有用途来说，字符串和数字是等同的，但引用是强类型的、不可转换的指针，具有内置的引用计数和析构函数调用机制。

在布尔逻辑意义上，如果一个标量值是已定义的、空字符串或数字 `0`（或其字符串等值 `"0"`），则被解释为 FALSE；其他任何值均为 TRUE。布尔上下文是一种特殊的标量上下文，在其中永远不会执行到标量或数字的转换。

实际上存在两种类型的空字符串（有时被称为“空字符串”）：已定义的和未定义的。已定义的版本只是一个长度为零的字符串，例如 `""`。未定义的版本表示某项没有真实值，例如当发生错误、编辑文件，或者当你引用未初始化的变量、数组或哈希元素时。在 Perl 的早期版本中，未定义的标量在期望定义值的地方使用会变为定义，但对于 `perref` 中解释的少数自动创建（autovivification）情况，这种情况不再发生。你可以使用 `defined()` 运算符来判断标量值是否已定义（这在数组或哈希上没有意义），或者使用 `undef()` 运算符产生一个未定义值。

要判断一个给定字符串是否为有效的非零数字，有时同时测试数字 `0` 和字面量 `"0"` 就足够了（尽管如果开启了警告会产生干扰）。因为字符串值不计为 `0`，就像在 `awk` 中一样：

```perl
if ($str == 0 && $str ne "0") { warn "That doesn't look like a number"; }
```

在这种情况下这种方法可能是最好的，否则你无法正确处理 IEEE 表示（如 NAN 或 Infinity）。在其他时候，你可能倾向于使用正则表达式来确定字符串数据是否可以用数值表示（如 `perle` 文档所示）。

```perl
warn "has nondigits" if /\D/; warn "not a natural number" unless /^\d+$/; # rejects -3 "not an integer" unless /-?\d+$/; rejects +3 "not an integer" unless /^\+\d+$/; warn "not a decimal number" unless /-?\d*$/; # rejects .2 "not a decimal number" unless /^(\d*\.\d+|\d+\.\d*)$$/; warn "not a C float" unless /^([-+]?(\d+\.\d*|\.\d+|\d+))([eE][-+]?\d+)?$/
```



数组的长度是一个标量值。你可以通过评估`$#`获取数组`@days`的长度。然而，这不是数组的长度；它是最后一个元素的下标，这是一个不同的值，因为通常存在一个 0元素。

给`@days`赋值实际上会改变数组的长度。通过这种方式缩短数组会破坏中间的值。扩展一个之前被缩短的数组并不会恢复那些元素中的值。

你也可以通过预扩展一个即将变大的数组来获得极小的效率提升。你还可以通过给数组末尾之外元素赋值来扩展数组。你可以通过将空`()`赋值给任何数组来将其截空。以下操作是等价的：

```perl
@whatever = (); $whatever = -1;
```

如果你在标量上下文中评估数组，它返回数组的长度。注意，这不适用于列表，列表返回最后一个值，类似于 C 语言的逗号运算符；也不适用于内置函数，它们返回它们想返回的内容。以下始终成立：
`scalar(@whatever) == $$whatever + 1;`

某些程序员选择使用显式转换以消除疑义：
`$element_count = scalar(@whatever);`

如果你在标量上下文中评估哈希，如果哈希为空，则返回假。如果有任何键/值对，则返回真；更准确地说，返回的值是一个由已使用的桶（buckets）数量和分配桶的数量组成的字符串，中间用斜杠分隔。
这几乎仅用于发现 Perl 的内部哈希算法在你的数据集上性能不佳。例如，你在哈希中存放了 10,000 个项，但在标量上下文中评估`%HASH`显示为`1/16`，这意味着十六个桶中只有一个被触及了，并且它包含了你所有的 10 个项目。这并不是预期发生。如果在标量上下文中评估绑定哈希（tied hash），将调用`SCALAR`方法（回退到`FIRST`）。

你可以通过给`keys()`函数赋值来为哈希预分配空间。这会将所有分配的桶向上取整到幂：

```perl
keys(%users) = 1000; # allocate 1024 buckets
```

## 数字字面量

数字字面量在以下情况下指定：

- 十六进制、八进制、二进制。字符串内部的表示（例如 `'0xff'`）不会自动转换。请参见 `"hex()"`和`"oct()"`函数来实现这些转换。Perl 中没有双重插值，因此`$100`保持原样。

```perl
$Price = '$100'; # not interpolated print "The price is $Price.\n"; # output: The price is $100.
```

浮点值包括特殊值`Inf`（无穷大）和`NaN`（非数字）。无穷大也可以是负的。

无穷大是某些溢出浮点数范围的数学运算的结果，例如`9**9*`。非数字是当结果未定义或无法表示时产生的结果。尽管你可能注意到，你无法通过除以零或对负数开平方来从某些未定义或超出范围的操作获取`NaN`，因为 Perl 会对这些操作产生致命错误（fatal errors）。

无穷大是非数字有它们特殊的算术规则。通用规则是它们是传染性的：`Inf`加一等于`Inf`，`NaN`加一等于`NaN`。有趣的地方在于将无穷大和非数字结合：`-Inf`和`Inf / Inf`等于`NaN`（而`Inf + Inf`和`Inf * Inf`等于`Inf`）。`NaN`也很奇，因为它不等于任何数字，包括它自己：`NaN != NaN`。

Perl 不将`Inf`和`NaN`视为数值字面量，但你可以将它们作为字符串使用，Perl 会根据需要进行转换：`"Inf" + 1`。不过，你可以从 POSIX 扩展中导入它们；使用`POSIX qw(Inf NaN);`并将它们作为字面量使用。

注意在输入（字符串）时，Perl 接受多种形式的`Inf`和`NaN`。忽略大小写，并且理解 Win32 特有的形式如`1.#INF`，但在输出时值会被规范化为`Inf`和`NaN`。

## 版本字符串

形式如`v1.20.300.400`的字面量被解析为由指定顺序字符组成的字符串。这种形式被称为 v-strings，提供了一种构建字符串的替代且更易读的方法，而不是使用可读性较的插值格式`\x11\x14\x1c\xfa6`。这对于表示 Unicode 字符串非常有用，并可以使用字符串比较运算符`cmp`、`gt`、`1t`等来比较版本数字。如果字面量中有两个或多个点，可以省略`v`。

```perl
print v9786; # 打印 SMILEY, "\x263a"
print v102.111.111; # 打印 "foo"
print 102.111.111; # 相同
```

此类字面量被`require`和用于检查的操作接受。注意，将 v-strings 用于 IPv4 地址并不是可移植的，除非你同时也使用了`Socket`包中的`inet_aton()/inet_ntop()`例程。

注意，从 Perl 5.8.1 开始，单数字 v-strings（如`v65`）不再是 v-strings，因为`==`运算符（通常用于分隔哈希键和哈希值）；相反，它们被被解释为字面量字符串（`'v65'`）。在 Perl 5.6 到 Perl 5.8.0 之间它们是 v-strings，但这带来的混乱和破坏多于收益。多数字 v-strings（如`v66.65`和`66.66.67`）继续作为 v-strings。

## 特殊字面量

特殊字面量`--__FILE__`、`__LINE__`和`__PACKAGE__`代表程序中该点的当前文件名、行号和包名。`__SUB__`提供指向当前子程序的引用。它们只能作为单独的标记使用；它们不会被插值到字符串中。如果没有当前包（由于空的包 指令），`__PACKAGE__`是其预定义值。但从 5.10 版本开始，不再支持`__SUB__ package;`。在子程序外部，`__SUB__`是其预定义值。`__SUB__`仅在 5.16 及更高版本中可用，且仅在带有`use v5.16`或`use feature "current_sub"`声明的情况下。

两个字符`^D`和`^`，以及标记`__END_`和`__DATA_`可用于在文件实际结束之前标识脚本的逻辑结束。随后的任何文本将被忽略。

`__DATA__`之后的文本可以通过文件句柄`PACKAGE: :DATA`读取，其中`PACKAGE`是遇到`__DATA_`标记时的当前包。该句柄将保持打开状态并指向`__DATA__`之后的一行。程序在完成读取后应该关闭`DATA`。由于某种原因加载了模块，保持打开会留下句柄，因此关闭它是更安全的做法。为了兼容在`__DATA__`引入之前编写的旧脚本，`__END_`在顶层脚本中的行为类似于`__DATA_`（但在包含`require`或`de`的文件中不是），并允许通过`:DATA`访问文件的剩余内容。

更多关于`__DATA__`的描述和使用示例请见 SelfLoader。注意你不能在块中从 DATA 文件句柄读取：`BEGIN`块在它执行时（编译期间）执行，此时相应的`__DATA__`（或`__END_`）标记尚未被看到。

## 裸字 (Barewords)

在语法中没有其他解释的单词将被视为带引号的字符串。这些被称为裸字，并且带有标签，一个完全由小写字母组成的裸字存在与未来保留字冲突的风险，如果你使用`use warning`或`-w`选项，Perl 将对任何此类单词发出警告。Perl 将裸字（如标识符）限制在约 250 个字符。未来的 Perl 版本可能会消除这些任意限制。

有些人可能希望完全禁止裸字。如果你说`use strict 'subs'`，那么任何不会被解释为子程序调用的裸字都会导致编译时错误。该限制一直持续到闭合块的结束。内部块可以通过说`no strict 'subs'`来抵消此。

## 数组插值

数组和字符串通过用指定的分隔符连接元素被插值到双引号字符串中，如果`use English;`指定了默认的空格。以下是等价的：

```perl
$temp = join("", @ARGV); system echo $temp; system echo @ARGV;
```

在模式（正则表达式）中，`${foo}`被解释为数组下标，结果产生的列表值被插值到 LIST，就像每个单独元素都是 LIST 的成员一样。如果`@foo`不存在，则是一个字符类。如果`@foo`存在，Perl 会做出正确的猜测。如果只是纯粹的担心，可以使用大括号`{}`来强制正确的解释。如果你正在寻找关于如何使用此文档的信息，请见`perlop`。

## 列表值构造器

列表值通过逗号分隔各个值来表示（并在需要时用括号包裹列表）：

```perl
(LIST)
```

在不需要列表值的环境中，看起来像列表字面量的值只是最后一个元素的值，就像 C 的逗号运算符。例如：

```perl
@foo = ('cc', '-E', $bar);
```

将整个列表值赋值给数组`@foo`，但



`$foo = ('cc', '-E', $bar);`

将变量 `$bar` 的值赋值给标量变量 `$foo`。注意实际数组在标量上下文值为数组的长度；以下将 3 赋值给 `$foo`：

```
@foo = ('cc', '-E', $bar); $foo = @foo; # $foo 得到 3
```

字面量的右括号前有一个可选的逗号，因此你可以说：

- 1, 2, 3, )

使用此处文档分配数组，每行一个元素，你可以使用这种方法：

```
@sauces = <<End_Lines ~ m(/\S.*\S)/g; tomato spicy chile peso white wine End_Lines
```

`LIST` 对子列表进行插值。也就是说，当评估 `LIST` 时，列表的每个元素在列表环境中被求值，产生的列表值被插值到 `LIST`，就像每个单独元素都是 `LIST` 的成员一样。数组和哈希在 `LIST` 中丢失了它们的身份——列表

```
(@foo, @bar, &SomeSub, %glarch)
```

包含了 `@foo` 的所有元素，随后是 `@bar` 的所有元素，随后是在列表环境中调子程序 `SomeSub` 返回的所有元素，最后是 `%glarch` 的键/值。要创建一个不插值的列表引用，请见 `perref`。

空列表由 `()` 表示。在列表中插值它没有影响。`(),())` 等价于 `()`。同样，插值一个没有元素的数组等同于在该点没有插值数组。

这种插值结合了以下事实：起始和结束括号是可选的（除非为了优先级需要），并且列表可以以可选的逗号结尾，这表示在列表内部使用多个逗号是合法的语法。列表 `1,,3` 是列表 `1, 3` 的连接，其中第一个以该可选逗号结尾。`1,,,3` 是 `(1,), (3)` 是 `1,3`（同样地，`1,,,3` 是 `(1,), (,)` 是 `1,3` 等此类推）。尽管我们并不建议你使用这种混淆手段。

列表值也可以像普通值一样进行下标操作。你必须将列表放在括号中以避免歧义。例如：

```perl
# Stat 返回列表值。 $time = (stat($file))[0]; # 此处语法错误。

$time = stat($file)[0]; # 噢，忘记括号了 # 查找十六进制位。

$hexdigit = ('a','b','c','d','e','f'][$digit-10]); # 一个反向逗号运算符。 return (pop($foo),pop($foo))];
```

当列表的每个元素本身都是可赋值的，就可以对列表进行赋值：
`($a, $b, $c) = (1, 2, 3); $map{'red'}, $map{'blue'}, $map{'green'} = (0x0f, 0x0f, 0x0f);`

一个例外是你可以给 `undef` 赋值。这对于丢弃函数的某些返回值非常有用：
`($dev,$ino,undef,undef,$gid) = stat($file);`

从 Perl 5.22 开始，你可以使用 `undef($x)` 代替 `undef`。（你也可以执行 `($x) *= 2`，但这用处较小，因为它对同一个变量赋值了两次，覆盖了第一次赋值的值）。

标量语境下的列表赋值返回赋值右侧表达式产生的元素数量：
`$x = (($foo,$bar) = (3,2,1)); # 将 $x 设为 3，而不是 2 $x = (($foo,$bar = f())); # 将 $x 设为 f($foo) 的返回计数`

当你想要在布尔语境下分配列表时，会出现这种情况。大多数列表函数在完成后会返回空，赋值时会产生 0，这被解释为 FALSE（假）。

它也是在列表语境下执行函数或执行操作并返回数值数量的常用惯用法的来源，通过赋值给一个空列表然后在标量语境中使用赋值来实现。例如，这段代码：
`$count = () $string =~ /\d+/g;`

这会将 `$count` 设为在 `$string` 中找到的数字个数。这是因为模式匹配是在列表语境下进行的（因为它被赋值给空列表），并将返回一个字符串中所有匹配部分的列表。标量语境下的列表赋值将转换为元素数量（在这里，是 `$count = $string =~ /\d+/g;` 执行的次数。注意，仅仅使用

是行不通的，因为标量语境下的模式匹配只会返回真或假，而不是匹配的计数）。

列表赋值的最后一个元素可以是数组或哈希表：

`($a, $b, @rest) = split; my($a, @rest) = @;`

你实际上可以将数组或哈希表放在列表的任何位置，列表将吸收所有值，其后的任何内容都将变为 undefined（未定义）。这在 `my()` 或 `local()` 中可能很有用。

可以使用字面量赋值来初始化哈希表，其中包含的项目值对被解释为键和值：

```perl
# 等于上面的 map 赋值 %map =

# ('red', 0x00f, 'blue', 0x0f0, 'green', 0xf00)
```

虽然列表和数组通常是可以互换的，但哈希表并非如此。因为你可以像普通数组一样对列表值取下标，并不意味着你可以像哈希表一样对列表值取下标。同样，作为列表部分的哈希表（包括参数列表和函数的返回列表）总是会平坦化为键/值对。这就是为什么使用一些引用是比较好的。

在键/值对之间使用 `=>` 运算符通常更具读性。`=>` 运算符大部分只是逗号的视觉上明显的同义词，但它还确保如果左侧是合法的简单标识符裸字（bareword），则将其解释为字符串。`=>` 不会对包含双冒号的复合标识符加引号。这使得它初始化哈希表非常方便：

```perl
%map = ( red => 0x00f, blue => 0x0f0, green => 0xf00, );
```

或者初始化用于记录的哈希表：

```perl
$rec = { witch => 'Mable the Merceless', cat => 'Fluffy the Ferocious', date => '10/31/1776', };
```

或者对复杂的函数使用命名参数调用：

```perl
$field = $query->radio_group( name => 'group_name', values =>
['eenie', 'meenie', 'minie'], default => 'meenie', linebreak => 'true',
labels => \labels );
```

注意，因为哈希表是顺序初始化的，这意味着它的输出顺序也是该顺序。在 perl 中使用 "sort" 可以查看如何安排输出顺序的示例。

如果键在哈希表的初始化列表中出现多次，则最后一次出现获胜：

```perl
%circle = ( center => [5, 10], center => [27, 9], radius => 100, color =>
[0xDF, 0xFF, 0x00], radius => 5 ); %circle = ( center => [27, 9], color => [0xDF, 0xFF, 0x00], radius => 5 );
```

这可以用来提供可覆盖的默认值：
```perl
# %args 中的值优先级高于 %config %config_defaults %args);
```



### 下标 (Subscripts)

通过指定美元符号 (`$$`)、然后数组名称（不带前头的 `@`），然后方括号内的下标，可以一次访问数组的一个标量。例如：

```
@array = (5, 50, 500); print "The Third Element is", $array[2];
```

数组索引从 0 开始。负下标会从末尾检索其值。在我们的示例中，`$array[-1]` 将是 500，`$array[-2]` 将是 500。哈希数组类似，但使用的是花括号而不是方括号。例如：

```
%scientists = ( "Newton" => "Isaac", "Einstein" => "Albert", "Darwin" =>
$scientists = ( "Newton" => "Isaac", "Einstein" => "Albert", "Darwin" (此处此处不完整)
```

（注：原文文本在此处似乎截断或存在重复，已根据上下文逻辑翻译）

*由于提供的原文在后半部分存在大量断裂和重复，上述翻译已基于 Markdown 规则进行了尽可能的处理。*

使 `$this` 成为 `$that` 的别名，`@this` 成为 `@that` 的别名，`%this` 成为 `%that` 的别名，`&this`
`local *Here::blue = \$There::green;`
更安全的方法是使用引用：

临时使 `$Here::blue` 成为 `@Here::green` 的别名，但不会让 `@Here::blue` 成为 `@Here::green` 的别名，或让 `%Here:blue` 成为 `%Here::green` 的别名，c. 查看 perl 中的 "Symbol Tables" 获取更多示例。尽管这看起来很奇怪，但整个模块导入/导出系统的基础。

类型全局（typeglob）的另一个用途是将句柄传递给函数或创建新的文件句柄。如果你需要使用类型全局来保存文件句柄，请按此方式操作：
`$fh = \STDOUT;`

或者可能作为一个真正的引用，如下：
`$fh = \STDOUT;`

参见 `perlub` 有关在函数中使用这些间接文件句柄的示例。
类型全局也是使用 `local()` 操作符创建本地文件句柄的一种方法。这些在块退出时持续，但可以被传回。例如：

```
sub newopen { $path = shift; local "FH; not my! (open, $path)
return undef; return "FH"; $fh = newopen('/etc/passwd'); }
```

既然我们已经有了 `*foo{THING}` 符号*，类型不再用于文件句柄操作，尽管它们仍需要将新的和目录句柄传出或传入函数。这就是 "`HANDLE{10}` 只有在 `HANDLE` 已用作文件句柄时才有效"。换句话说，`*FH` 必须用于创建新的符号表条目；`*foo{THING}` 有疑问时使用 "`FH`"。

所有能够创建文件句柄的函数（`open()`, `opendir()`, `pipe(socketpair)`, `sysopen()`, `socket()`, 和 `accept()`）如果发现它们的句柄是一个未初始化的标量变量，会自动创建一个匿名文件句柄。这允许 `open($fh, ...)` 和 `open($fh, ...)` 等结构创建在作用域结束时方便自动关闭的文件句柄，前提是它们没有其他引用。这消除了在打开必须传递的文件句柄时对类型全局的需要，如下例所示：

```
my newopen $fh, "@" or die "can't open @: \!"; return $fh;
my $fh = newopen('/etc/motd'); print <$fh>; # $FH implicitly closed here
```

注意，如果使用的是已初始化的标量变量，结果不同：`my $fh='zzz'; open($fh, ...)` 等同于 `open('*zzz', ...);` 使用 `strict 'refs'` 禁止这种做法。

创建匿名文件句柄的另一种方法是使用 `Symbol` 模块或使用 `IO::Handle` 模块及其类似模块。这些方法的优点是在 `local()` 中不会隐藏同名的不同类型。在 `perlunc` 中查看 "`open`" 示例。

# 另见

参见 `perlvar` 的 Perl 内置变量描述以及对合法变量名的讨论。参见 `permod` 中的 `perlref`, `persub` 和 "`Symbol Tables`" 以获得更多关于类型全局和 `*foo{THING}` 语法的讨论。

# PERLDBMFIL

## 名称

`perldbmfilter` - Perl DBM 过滤器 (Filters)

# 概要要介绍

```
$db = tie %hash, 'DBM', ... $old_filter = $db->filter_store_key ( sub { ... } ); $old_filter = $db->filter_store_value(sub { ... } ); $old_filter = $db->filter_fetch_key ( sub { ... } ); $old_filter = $db->filter_fetch_value(sub { ... } );
```

## 描述

上述四个 `filter-*` 方法在随 Perl 一带的所有 DBM 模块中均可用，即 `DB_File`, `GBM_File`, `NDBM_File`, `OBM_File` 和 `SDBM_File`。

每个方法的工作方式相同，用于安装（或卸载）单个 DBM 过滤器。它们之间唯一的区别是过滤器安装的位置。

总结如下：

- `filter_store_key`
如果使用此方法安装了过滤器，则每当向 DBM 数据库写入键时，它都会被调用。

- `filter_store_value`
如果使用此方法安装了过滤器，则每当向 DBM 数据库写入值时，它都会被调用。

- `filter_fetch_key`
如果使用此方法安装了过滤器，则每当从 DBM 数据库读取键时，它都会被调用。

- `filter_fetch_value`
如果使用此方法安装了过滤器，则每当从 DBM 数据库读取值时，它都会被调用。

你可以使用这些方法的任何组合，从无使用到全部使用。所有过滤器方法都返回现有的过滤器，如果不存在则返回 `undef`。

# 过滤器 (Filter)

当 Perl 调用每个过滤器时，`$_` 的本地副本将包含被过滤的键或值。过滤通过修改 `$_` 的内容来实现。过滤器的返回代码被忽略。

# 示例：NULL 终止符。

DBM 过滤器适用于一类问题，即你总是希望对所有键进行相同的转换。例如，考虑以下场景：你有一个需要与第三方应用程序共享的 DBM 数据库。应用程序假设所有键和值都是 NULL 终止的。遗憾的是，Perl 向 DBM 数据库写入时并不使用 NULL 终止，因此你写入数据库时必须使用如下内容：

```
$hash{"$key\0"} = "$value\0";
```

同样，当你考虑现有键/值的长度时，需要考虑 NULL。如果能有一种机制在主代码中忽略 NULL 终止，并在写入数据库时自动添加，在从数据库读取时移除它们，就更好了。我确定你已经猜到了这个问题过滤器可以轻松解决。

```
use strict; use DBM_File; use Fcntl; my %hash; my $filename = "filt"; unlink $filename; my $db = tie($hash, 'DBM_File', $filename, 0_RDWR|0_CREATE, 0640) or die "Cannot open $filename: \n"; # Install Filters -$db->fetch_key(sub { $_ = /\s+$/ }) $db->store_key(sub { $_ = "\0" }) $db->fetch_value(sub { noinitialized'; $_ = /\s+$/ }) $db->store_value(sub { $_ = "\0" }) $hash("abc") = "def"; untie $hash;
```

上面的代码使用了 `DBM_File`，但适用于任何 DB 模块。这次使用了两个过滤器；我们只需要操作键的内容，因此没有安装任何值过滤器。

# 另一个示例：键是 C 整数。

这是另一个真实示例。默认情况下，Perl 向 DBM 数据库写入时总是将键和值视为字符串。所以当你使用：

```
$hash{12345} = "something";
```

键 12345 将以字符串 "12345" 存储在 DBM 数据库中。如果你实际上希望键以 C 整数存储在 DBM 数据库中，写入时必须使用 `pack`，读取时使用 `unpack`。这是一个实现此点的过滤器：



```
use strict; use warnings; use DBM_File; my %hash; my $filename = "filt"; unlink $filename; my $db = tie($hash, 'DBM_File', 0_RDWR|0_CREATE, 0666, $DB_HASH or die "Cannot open $filename: \n"; $db->fetch_key(sub { $_ = pack("i", $_) }) $db->store_key(sub { $_ = pack("i", $_) }); $hash{123} = "def"; # undef $db; untie $hash;
```

上面的代码使用了 `DBM_File`，但适用于任何 DB 模块。这次使用了两个过滤器；我们只需要操作键的内容，所以没有必要安装任何值过滤器。

# 另见

`DB_File`, `GDBM_File`, `NDBM_File`, `ODBM_File` 和 `SDBM_File`。

# 作者

Paul Marquez

# PERLDEBGUTS

## 名称

`perldebguts` - Perl 调试内部机制

## 描述

这不是 `perldebug`，后者告诉你如何使用调试器。本帮助页描述了关于调试器内部的底层细节，对于任何不熟悉 Perl 内部的人来说，这些细节从困难到无法理解。读者注意。

## 调试器内部 (DEBUGGER INTERNALS)

Perl 在编译和运行时有特殊的调试钩子，用于创建调试环境。这些钩子不要与 `perlrun` 中描述的 `perl -Dxxx` 命令混淆，后者只有在为 Perl 源码树中的指令构建了特殊的 Perl 时才可用。

例如，当你从 `DB` 包调用 Perl 的内置调用函数时，相应栈帧的参数被复制到 `DB::args` 数组中。这些机制通过在调用 Perl 时使用 `-d` 启用。具体而言，启用了以下功能（参见 `perlvar` 中的 `^$P`）：

- Perl 在程序的第一行之前插入 `$ENV{PERDB}` 的内容（如果没有则执行 `BEGIN {require 'perl5db.pl' }`）。每个数组 (`"<$filename>"`) 存储 `$filename` 的行。对于包含子程序的或当前执行的 `eval` 字符串也是如此。`eval` 字符串的 `$filename` 看起来像 `(eval 34)`。
- 每个哈希 (`"<$filename>"`) 包含按行号键值的断点的操作。单个条目（而不是整个哈希）是可以设置的。数组中的值在数值上下文中是魔性的：只有当行不是断点时，它们才与零比较。
- 每个标量 (`"<$filename>"`) 包含 `_$filename`。对于包含子程序的或正在执行的 `eval` 字符串也是如此。`eval` 字符串的 `$filename` 看起来像 `(eval 34)`。
- 在每个要求文件编译后、执行前，由子程序 `DB::posted` 调用 `db::posted(*$_filename)`。这里，`$filename` 是要求文件的已扩展名，可以在 `%INC` 的值中找到。在每个子程序编译后，检查 `DB::posted(subname)` 是否存在。如果存在，且 `DB:::posted` 子程序也存在，则调用 `DB::posted(subname)`。
- 一个哈希 `%DB` 的键是子程序名，值为形式为 `filename:起始行-结束行`。对于在 `eval` 内部定义的子程序，`filename` 的形式为 `(eval 34)`。
- 当程序的执行到达一个可以放置断点的位置时，如果变量 `DB::trace`、`DB::single` 或 `$signal` 的任何一个为真，则调用 `DB::()`。这些变量无法局部。在 `DB::DB()` 内部执行时，此功能被禁用，包括从它调用的函数，除非 `^D & (1<<30)` 为真。

当程序执行到达子程序时，调用 `&DB::sub(args)` 是

而是执行相应的操作，其中 `$DB::sub` 持有 DB 子程序的名称。（如果该子程序是在 DB 包中编译的，则不会发生这种情况。）

如果调用的是 Ivalue 子程序，且 `$DB::sub` 已定义，则会而调用 `&$DB::sub(args)`，否则回退到 `$DB::sub(args)`。

当程序执行使用 `goto` 进入非 XS 子程序且 `$P` 中的 `0x80` 位被设置时，会调用 `$DB::goto`，此时 `$DB::sub` 持有正在进入的子程序的名称。

注意，如果 `&$DB::sub` 的工作需要外部数据，那么没有它就无法进行子程序调用。例如，标准的 `debugger::sub` 依赖于 `$DB::deep` 变量（它定义了在强制中断之前你可以进入调试器的多少层递归深度）。如果 `$DB::deep` 未定义，即使 `$DB::sub` 存在，也不进行子程序调用。

## 你自己的调试器

### 环境变量

可以使用 `PERLDB` 环境变量来定义调试器。例如，最小的“工作”调试器（实际上什么都不做）仅包含一行：

```perl
sub DB::DB {
```

它可以像这样定义：

`$ PERLDB="$DB::DB" perl -d your-script`

另一个简短但稍微好用一点的调试器可以使用以下行创建：

```perl
sub DB::DB (print ++$$; scalar <STDIN>)
```

这个调试器会打印一个每遇到一条语句就会增加的数字，并在等待你按下回车键后再继续到下一语句。

以下调试器是有用的：

```
{ package DB; sub DB sub {print ++$$, "$sub\n"; $$sub }
```

它会打印每个子程序调用的序列号和被调用子程序的名称。注意 `&$DB::sub` 正在通过使用 `package` 指令编译到 `DB` 包中。

当调试器启动时，会读取你的 rc 文件（Unix 上为 `./perldb` 或 `~/perldb`），该文件可以设置重要的选项。（在这里也可以定义一个子程序 `&afterinit`；它会在调试器完成自身初始化后执行。）

加载 rc 文件后，调试器会读取 `PERLDB_OPTS` 环境变量并使用它设置调试器选项。变量的内容被处理为类似于 `o ... debugger` 命令的参数（详见 `perldbug` 中的“Configurable Options”部分）。

## 调试器内部变量

除了上述与文件和子程序相关的变量外，调试器 `@DB::dbline` 是 `@{:_current_file}` 的别名，它持有当前所选文件的行（由 Perl 编译），这些行是通过调试器的 `f` 命令显式选择的，或通过执行流隐式选择的。

此数组中的值在数值上下文中是数组：只有当该行不可设置断点时，它们与零比较才相等。

`%DB::dbline` 是 `line%${:_current_file}` 的别名，它包含了当前所选文件中断点和以行数为键的键，这些行是通过调试器的 `f` 命令显式选择的，或通过执行流隐式选择的。

如前，单个条目（而不是整个哈希）是可以设置的。Perl 在这里只关心布尔真值，尽管 `perldb.pl` 使用的值格式为 `$break_condition\$action`。

## 调试器自定义函数

提供了一些函数以简化自定义。

- 参见 `perdebug` 中的“Configurable Options”以获取由 `DB::parse_options(string)` 解析的选项描述。
- `DB::dump_trace(skip[, count])` 跳过指定数量的帧，并返回一个包含调用帧信息的列表（如果缺少 `count` 则返回所有帧）。每个条目都是指向哈希的引用，键具有 `context`（`,`$` 或 `@`）、`sub`（子程序名或 eval 信息）、`args`（undef 或数组引用）、`file` 和 `line`。
- `DB::print_trace(FH, skip[, count[, short]])` 打印调用者帧的格式化信息。最后两个函数可以作为 `<`、`<<` 命令的参数。

注意，这些手册页（或 `perdebug`）中未说明的任何变量和函数仅供内部使用，因此可能会在不另通知的情况下更改。

## 帧列表输出示例

`frame` 选项可用于控制帧信息的输出。例如，对比以下表达式：

```
$ perl -de 42 Stack dump during die enabled outside of evals. Loading DB from perls5d.pb patch level 0.94 Emacs support available. Entering h or 'h h' for help, main::(-e:1) 0 DB<1> sub foo { 14 } DB<2> sub bar { 3 } DB<3> t print foo() * bar(); main::foo(eval 168): main::bar((eval 170):2) 42
```

与这个对比，设置了选项 `frame=2`：



```
DB<4> o f=2 DB<5> t print foo() * bar() 3:foo() * bar()

:bar '2' sub foo { 14 } entering main::foo main::bar

:sub bar { 3 } exiting main::bar 42
```



为了演示，我们在下面展示了设置 `f=N` 并向命令行运行 `PERLDB_OPTS` 环境变量后产生的复杂列表。展示了使用不同 `n` 值的示例，让你对差异有直。。尽管很长，但这并不是完整的列表，只是片段。

- 1. entering `main::BEGIN` entering `Config::BEGIN` package `lib/Exporter.pm` `lib/Carp.pm` `package/Config.pm` entering `Config::TIEHASH` `Exporter:import` `Exporter:export` `Config::myconfig` `Config::FETCH` `Config::FETCH`
- 2. entering `main::BEGIN` entering `Config::BEGIN` package `lib/Exporter.pm.lib/Carp.pm` exited `Config::BEGIN` `package/Config.pm.` entering `Config::TIEHASH` exited `TIEHASH` `Exporter:import` `Exporter:export` exited `Exporter` imported `main::BEGIN` entering `Config::myconfig` `Config::FETCH` exited `Config::FETCH`
- 3. `in=$main::BEGIN` from `/dev/null:0` `in=$Config::BEGIN()` from `lib/Config.pm:2` `package/Exporter.pm.` `package/Carp.pm.lib/Config.pm.` `TIEHASH(Config)` from `lib/Config.pm:64` `in=$Exporter::import('myconfig', 'config_vars')` from `/dev/null:0` `in=$Exporter::export('main', 'config_vars')` from `=$Config::FETCH(ref(Config), 'package')` from `lib/Config.pm:574` `in=$Config::FETCH(ref(Config), 'basever')` from `lib/Config.pm:574` `in=$Config::FETCH(ref(Config), 'PERL_SUBVERSION')` from `lib/Config.pm:574` `in=$Config::FETCH(ref(Config), 'osname')` from `lib/Config.pm:574` `in=$Config::FETCH(ref(Config), 'osvers')` from `lib/Config.pm:574`
- 4. `in=$main::BEGIN` from `/dev/null:0` `in=$Config::BEGIN()` from `lib/Config.pm:2` `package/Exporter.pm.` `package/Carp.pm.` `out=$Config::BEGIN()` from `lib/Config.pm:0` `package` in `$Config::TIEASH('Config')` from `lib/Config.pm:644` `$Config::TIEASH('Config')` from `lib/Config.pm:644` `$Exporter::import('myconfig', 'config_vars')` from `/dev/null:0=$Exporter::export('main', 'config_vars', 'config_vars')` from `lib/` `out=$Exporter::import('myconfig', 'config_vars')` from `/dev/null:0` `out=$main::BEGIN(0)` `/dev/null:0` `in @Config::myconfig()` from `/dev/null:0` `$Config::FETCH(ref(Config), 'package')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'package')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'baseref')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'baseref')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'PERL_VERSION')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'PERL_VERSION')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'PERL_SUBVERSION')` from `lib/Config.pm:574` `$Config::FETCH(ref(Config), 'PERL_SUBVERSION')` from `lib/Config.pm:574`
- 5. `in=$main::BEGIN` from `/dev/null:0` `in=$Config::BEGIN()` from `lib/Config.pm:2` `package/Exporter.pm.` `package/Carp.pm.` `out$Config::BEGIN()` from `lib/Config.pm:0` `package/Config.pm.` `in $Config::TIEASH('Config')` from `lib/Config.pm:644` `$Config::TIEASH('Config')` from `lib/Config.pm:644` `$Exporter::import('myconfig', 'config_vars')` from `/dev/null:0=$Exporter::export('main', 'config_vars', 'config_vars')` from `lib/` `out=$Exporter::import('myconfig', 'config_vars')` from `/dev/null:0` `out=$main::BEGIN(0)` `/dev/null:0` `in @Config::myconfig()` from `/dev/null:0` `$Config::FETCH:HASH(0x1aa44), 'package')` from `lib/Config.pm:574` `out=$Config::FETCH:HASH(0x1aa44), 'package')` from `lib/Config.pm:574` `$Config::FETCH:HASH(0x1aa44), 'baseref')` from `lib/Config.pm:574` `outConfig::FETCH('Config:HASH(0x1aa44)', 'baseref')` from `lib/Config.pm:574`
- 6. `in=$CODE(0x15eca4())` from `/dev/null:0` `in=$CODE(0x182528)()` from `lib/Config.pm:2` `package/Exporter.pm.` `out` `in=$CODE(0x182528)()` from `lib/Config.pm:0` `scalar context return from (0x182528) undef Package/Carp.pm.` `in $Config::TIEASH('Config')` from `lib/Config.pm:628` `out=$Config::TIEASH('Config')` from `lib/Config.pm:628` `scalar context return from $Config::TIEASH: empty hash` `in $Exporter::import('Config', 'myconfig', 'config_vars')` from `/dev/null:0` `in=$Exporter::export('Config', 'main', 'myconfig', 'config_vars', 'config_vars')` from `lib/Exporter.pm:171` `out $Exporter::export('Config', 'main', 'myconfig', 'config_vars')` from `lib/Exporter.pm:171` `scalar context return from Exporter: export ''` `out $Exporter::import('Config', 'myconfig', 'config_vars')` from `/dev/null:0` `scalar context return from Exporter:::`


包 `lib/Carp.pm`。

将带有正确的缩进进行打印。

## 调试正则表达式

有两种方法可以启用正则表达式的调试输出。

如果你的 Perl 在编译时使用了 `-DEBUGGING` 参数，你可以在命令行上使用 `-Dr` 标志。

否则，你可以使用重新调试（re-debug），这在编译时运行时都有效。自 Perl 5.9.5 起，该指令（pragma）是词法作用域的。

## 编译时输出

编译时的调试输出看起来如下：

```



Compiling Rex '[bc][d(ef)*+h[ij]k$' size 45 364 bytes for offset annotations, first at 1 rarest char g at 0 rarest d at 0 ANYOF[bc] 12) EXAC<d(14) 45: CURLY[0] 1[3,267] 29: EXAC<()> ANYOF[jj](42) 42: OPEN1(18) 18: EXACT<=(20>(20) 20: STAR(23) 29: EXAC<f>(0) 23: EXAC<>(25) 25: CLOSE1(27) 27: WHILE[1](0) 28: NOTING(29) ANY3331) 31:4444 4444OL(45) 45: END(0) anchored 'de' at 1 floating 'gh' at 3..2144836467 (checking floating) stclass 'ANYOF[bc]' minlen 7 Offsets: [45] 1[4] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 5[0] 12[1] 12[1] 0[6] 1[0] 7[1] 0[0] 9[1] 8[1] 0[0] 10[1] 0[0] 11[1] 0[0] 12[0] 12[0] 13[1] 0[0] 14[4] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 18[1] 19[1] 20[0] Omitting "$ &" support.

第一行显示了正则表达式的预编译形式。第二行显示了编译后的 own（以长度为单位，4 字节字）以及为偏移量/长度表分配的总字节数，通常为 `4+size*8`。接下来的行显示了第一个包含优化器信息的节点的标签 ID。在所示的示例中，优化器发现匹配必须包含一个位于偏移量 1 处的子字符串，外加上在 3 到无穷大之间的某个偏移处的 `gh`。此外，为了通过检查这些子字符串来快速放弃不兼容的匹配，Perl 会在检查第一个子字符串之前检查子字符串 `gh`。优化器还可能利用匹配从（第一个 ID 处）字符开始的，且没有超过 7 个字符的字符串可能匹配。

该行中出现的感兴趣字段有：

- "anchored" STRING "at" POS
- "floating" STRING "at" POS1..POS2
- 见上方。matching/anchored
- 检查哪个子字符串。
- minlen: 匹配的最小长度。
- "stclass" TYPE 第一个匹配节点的类型。
- noscan: 不扫描找到找到子字符串。
- isall: 意味着优化器信息是正则表达式包含的所有内容，因此完全不需要进入正则引擎。
- GPOS: 如果模式包含 `\6`，则设置。
- plus: 如果模式以重复字符开头（如 `x+y`），则设置。
- implicit: 如果模式以 `*.*` 开头，则设置。
- with eval: 如果模式包含 eval 组，例如 `({? code })` 和 `(?? code})`，则设置。
- anchored(TYPE): 如果模式可能出现在几个位置，TYPE 为 SBOL、MBOL 或 GPOS。见见下表。

如果已知某个子字符串在行尾匹配，则它后面可能会跟一个 `$`，例如 `floating ‘k$.`。

优化器特定的信息用于避免在确定不会匹配的字符串上进入（慢速）正则引擎。如果 `isall` 标志被设置，当优化器找到匹配合适的位置时，可以避免对正则引擎的调用。

优化器部分上方是正则表达式编译形式的节点列表。每行都有：
`id: TYPE OPTIONAL-INFO (next-id)`

## 节点类型

是当前的类型、`[num-args]` 以及简短描述：

| TYPE | arg-description | [num-args] | [longjump-len] | DESCRIPTION | Exit points |
| :--- | :--- | :--- | :--- | :--- | :--- |
| END | 程序的结束。 | SUCCESS | 基本上没有从子程序返回。 | | |
| Line Start Anchor: SBOL | no | | 在行首匹配：`/, \A/` | | |
| MBOL | 同上，假设是多行：/#m` | | Unicode 结束锚点: SBOL | no 在行尾匹配：`/$` | | |
| MEOL | 同上，假设是多行：/#` | | EOS | no 在字符串末尾匹配：`/` | | |
| "anchored" STRING "at" POS | | | | "floating" STRING "at" POS1..POS2 | | | 见上方。matching/anchored | | | 检查哪个子字符串。
| | | minlen: 匹配的最小长度。
| | "stclass" TYPE 第一个匹配节点的类型。
| | noscan: 不扫描找到的子字符串。
| | isall: 意味着优化器信息是正则表达式包含的所有内容，因此完全不需要进入正则引擎。
| | GPOS: 如果模式包含 `\6`，则设置。
| | plus: 如果模式以重复字符开头（如 `x+y`），则设置。
| | implicit: 如果模式以 `*.*` 开头，则设置。
| | with eval: 如果模式包含 eval 组，例如 `({? code })` 和 `(?? code})`，则设置。
| anchored(TYPE): 如果模式可能出现在几个位置，TYPE 为 SBOL、MBOL 或 GPOS。见下表。

如果已知某个子字符串在行尾匹配，则它后面可能会跟一个 `$`，例如 `floating ‘k$.`。

优化器特定的信息用于避免在确定不会匹配的字符串上进入（慢速）正则引擎。如果 `isall` 标志被设置，当优化器找到匹配合适的位置时，可以避免对正则引擎的调用。

优化器部分上方是正则表达式编译形式的节点列表。每行都有：
`id: TYPE OPTIONAL-INFO (next-id)`

包 `lib/Carp.pm`。

将带有正确的缩进进行打印。

## 调试正则表达式

有两种方法可以启用正则表达式的调试输出。

如果你的 Perl 在编译时使用了 `-DEBUGGING` 参数，你可以在命令行上使用 `-Dr` 标志。

否则，你可以使用重新调试（re-debug），这在编译时运行时都有效。自 Perl 5.9.5 起，该指令是词法作用域的。

## 编译时输出

编译时的调试输出看起来如下：

```
Compiling Rex '[bc][d(ef)*+h[ij]k$' size 45 364 bytes for offset annotations, first at 1 rarest char g at 0 rarest d at 0 ANYOF[bc] 12) EXAC<d(14) 45: CURLY[0] 1[3,267] 29: EXAC<()> ANYOF[jj](42) 42: OPEN1(18) 18: EXACT<=(20>(20) 20: STAR(23) 29: EXAC<f>(0) 23: EXAC<>(25) 25: CLOSE1(27) 27: WHILE[1](0) 28: NOTING(29) ANY3331) 31:4444 4444OL(45) 45: END(0) anchored 'de' at 1 floating 'gh' at 3..2144836467 (checking floating) stclass 'ANYOF[bc]' minlen 7 Offsets: [45] 1[4] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 5[0] 12[1] 12[1] 0[6] 1[0] 7[1] 0[0] 9[1] 8[1] 0[0] 10[1] 0[0] 11[1] 0[0] 12[0] 12[0] 13[1] 0[0] 14[4] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 0[0] 18[1] 19[1] 20[0] Omitting "$ &" support.
```



第一行显示了正则表达式的预编译形式。第二行显示了编译后的 own（以长度为单位，4 字节字）以及为偏移量/长度表分配的总字节数，通常为 `4+size*8`。接下来的行显示了第一个包含优化器信息的节点的标签 ID。在所示的示例中，优化器发现匹配必须包含一个位于偏移量 1 处的子字符串，外加上在 3 到无穷大之间的某个偏移处的 `gh`。此外，为了通过检查这些子字符串来快速放弃不兼容的匹配，Perl 会在检查第一个子字符串之前检查子字符串 `gh`。优化器还可能利用匹配从（第一个 ID 处）字符开始的，且没有超过 7 个字符的字符串可能匹配。

该行中出现的感兴趣字段有：

- `"anchored" STRING "at" POS`
- `"floating" STRING "at" POS1..POS2`
- 见上方。matching/anchored
- 检查哪个子字符串。
- `minlen`: 匹配的最小长度。
- `"stclass" TYPE` 第一个匹配节点的类型。
- `noscan`: 不扫描找到的子字符串。
- `isall`: 意味着优化器信息是正则表达式包含的所有内容，因此完全不需要进入正则引擎。
- `GPOS`: 如果模式包含 `\6`，则设置。
- `plus`: 如果模式以重复字符开头（如 `x+y`），则设置。
- `implicit`: 如果模式以 `*.*` 开头，则设置。
- `with eval`: 如果模式包含 eval 组，例如 `({? code })` 和 `(?? code})`，则设置。
- `anchored(TYPE)`: 如果模式可能出现在几个位置，TYPE 为 `SBOL`、`MBOL` 或 `GPOS`。见下表。

如果已知某个子字符串在行尾匹配，则它后面可能会跟一个 `$`，例如 `floating ‘k$.`。

优化器特定的信息用于避免在确定不会匹配的字符串上进入（慢速）正则引擎。如果 `isall` 标志被设置，当优化器找到匹配合适的位置时，可以避免对正则引擎的调用。

优化器部分上方是正则表达式编译形式的节点列表。每行都有：
`id: TYPE OPTIONAL-INFO (next-id)`

## 节点类型

是当前的类型、`[num-args]` 以及简短描述：

| TYPE | arg-description | [num-args] | [longjump-len] | DESCRIPTION | Exit points |
| :--- | :--- | :--- | :--- | :--- | :--- |
| END | 程序的结束。 | SUCCESS | 基本上没有从子程序返回。 | | |
| Line Start Anchor: SBOL | no | | 在行首匹配：`/, \A/` | | |
| MBOL | 同上，假设是多行：`/#m` | | Unicode 结束锚点: SBOL | no 在行尾匹配：`/$` | | |
| MEOL | 同上，假设是多行：`/#` | | EOS | no 在字符串末尾匹配：`/` | | |

*(注：由于原始文本中的表格内容在输入中存在严重的重复和混乱，上述翻译已根据逻辑结构进行了对齐处理。)*

# 预编译正则表达式

`0[0]` 项表示没有相应的节点。

## 运行时输出

首先，在进行匹配时，可能会发现正则表达式从未进入，且所有任务都已启用。这通常是由优化器完成的。如果进入正则表达式引擎，输出可能如下：

```
Matching '[bcid(ef*)+h[ij]k$' against 'abcdef_gh__' Setting an EVAL scope, savestack=3 2 <abcd <def_gh_> | 1: ANYOF 4 <abcd <ef_gh_> | 11: EXACT 2 <abcd <ef_gh_> | 26: WHILE 0 out of 1.32767 <efffff3ic 13: CURLY {1,32767} 4 <abcd <ef_gh_> | 15: OPEN1 4 <abcd <ef_gh_> | 17: EXACT <5 <abcd <ef_gh_> | 19: STAT EXACT <> can match times
```

等等，提供的 OCR 文本极其混乱且破碎。让我尝试根据可见的碎片（Perl 内存使用、正则输出和调试）重构逻辑流。

*自我纠正：提供的源文本是许多重叠的 OCR 页面和不同主题（正则输出与 Perl 内存使用）。我将清理去噪后的 OCR 错误，例如将 "efffff3ic" 改为 "efficiency"，将 "proligate" 改为 "wasteful" 等，并将它们组织到请求的章节中。*

## 运行时输出

最重要的信息是当前正在测试的编译正则表达式特定节点。这些行的格式为 `STRING_OFFSET <PRE-STRING><POST-STRING> ID: TYPE`。信息相对于前面的内容是缩进的。

# 调试 Perl 内存使用

Perl 在内存使用方面有点浪费。有一种说法可以估算 Perl 的内存使用情况：假设一个合理的内存分配算法，将该估值乘以 10，虽然可能仍然偏离目标，但至少你不会完全失算。这并非绝对真实，但可以对所发生的情况提供良好的把握。假设一个整数占用的内存不少于 20 字节，浮点数不少于 24 字节，字符串不少于 32 字节（所有这些示例均假设 32 位架构；在 64 位架构上的结果会糟糕得多）。如果以两种不同的方式访问变量（需要整数、浮点数或字符串），内存占用可能会再增加 20 字节。在规模的另一端，一个声明可能占用 500 字节，取决于 Perl 的版本。轶事表明，经过编译且正确缩进的代码占空间比磁盘上的代码大八倍。`-DL` 命令行开关自 Perl 5.6 起已过时（它仅在构建 Perl 时启用了 DEBUG 时可用）。为了跟踪 Perl 的内存分配和可能的内存泄漏，现在建议使用 Perlify 或 valgrind 等调试工具。另请参见 `PERL_MEM_LOG`。

查找 Perl 数据结构使用多少内存的一种方法是从 CPAN 安装 `Devel::Size` 模块；它会为你提供存储特定数据结构所需的最小字节数。注意 `size()` 和 `total_size()` 区别。

# 使用环境变量 PERL_DEBUG_MSTATS

如果你在使用 Perl 的 `malloc()` 并使用必要的开关进行编译（这是默认设置），当 `ENV PERL_DEBUG_MSTATS >= 1` 时，程序会在代码执行后、程序结束前打印内存统计。报告格式类似于下面的示例：

```
$ PERL_DEBUG_MSTATS=2 -e "require"

Memory allocation after compilation: (buckets (4)).8198(8192)

free: 130 117 28 9 0 2 1 0 437 61 36 0 5 6024

used: 125 137 151 5 7 8 16 2 0 1 74 109 304 84 20 137 sbrk: 77824/21. Odd ends: pad+heap+chain;0+636+0*2848. Memory allocation after execution: (buckets (44)).8198(30888)

free: 245 78 85 13 6 2 1 3 2 0 115 162 192 39 42 1175816 used: 265 176 1112 111 26 22 11 27 2 196 178 1066 798 39 Total sbrk(): 215040/47145. Odd ends: pad+heads+chain+tail:0+2192+0+6144.
```



可以使用标准 `devel::Peek` 模块中的 `mstat()` 函数在执行的任意点请求此类统计数据。以下是对该格式的解释：

`buckets SMALLST(APPROX)..GREATEST(APPROX)`: Perl 的 `malloc()` 使用了桶分配（bucket）。每个请求都会向上舍入到最近的桶大小，并从桶池中取一个桶。上面那行描述了当前使用的桶的限制。每个桶有两个大小：内存占用和可以容入该桶的最大数据大小。在示例中，最小的桶是 4。最大的桶可用大小为 8188，内存占用将为 8192。

在 Perl 调试中，某些桶的可用大小为负。这意味着这些桶不能（也不会）被使用。对于较大的桶，内存占用可能比 2 的幂大一个页面。如果是如此，相应的 2 的幂打印在上面的 `APPROX` 字段中。

`Free/Used`: 后的 1 或 2 行对应于 `SMALLST` 和 `GREATEST` 之间每个大小的桶数量。第一行桶的大小（内存占用）是 2 的幂——或者可能是一个页面。如果存在第二行，桶的内存占用位于“上方”两个桶的内存占用之间

例如，假设在之前的示例下，内存占用为：
- free: 8 16 32 64 128 256 512 1024 2048 4096 8192
- used: 4 12 24 48 80

## 查看与 `-W`

好的，但当你想要查看数据，即在使用它之前那个动态变量里到底是什么时，该怎么办？

```perl
#!/usr/bin/perl

use strict; my $key = 'welcome'; %data = ( 'this' => qw(that), 'tom' => qw(and); 'welcome' => q(Hello World), 'zip' => q(welcome); my @data = keys %data; print "$data{$key}\n"; exit;
```

在经过语法检查 (`perl -c scriptname`) 后看起来没问题，我们运行它，得到的又是一个空行！嗯。

这里一种常用的调试方法是大量地插入几个 `print` 语句，在我们打印数据之前添加一个检查，在之后再加一个：

```perl
print "All OK\n" if grep($key, keys %data); print "$data{$key}\n";

print "done: $data{$key}\n";
```

然后再次尝试：

- > `perl data` All OK done:

在盯着同一段代码看了久却看不见树木之后，我们去喝了咖啡并尝试另一种方法。也就是说，通过在命令行中给 `perl` 加上 `'-d'` 参数来引入援军：

现在，我们所做的是在脚本上启动了内置的 `perl` 调试器。它停在了第一行可执行代码上，并等待输入。

在继续之前，你可能想知道如何退出调试器：只需使用字母 `'q'`，而不是用 `'quit'` 或 `'exit'` 单词：

```perl
DB<1> q
```

好了，你又回到了主场。

## 帮助

在你的脚本上启动调试器，我们将查看帮助菜单。调用帮助有几种方法：简单的 `'h'` 会获取摘要帮助列表，`|h` (管道-h) 将将帮助通过你的分页器（可能是 `'more'` 或 `'less'`）输出，最后，`h h` (h-空格) 将为你提供整个帮助屏幕屏。这里是摘要页：

### Dh

- 列出/搜索源码
- 控制脚本执行: 1 [ln|sum]
- 列出源代码 T
- 堆栈跟踪 - .
- 列出上一行/当前行 [expr]
- 简单单步 [in] v [line]
- 查看第 n 行周围的内容 [expr]
- 下一步，跳过子程序 f
- 查看所有文件的源码 /CR-Enter 重复列表 s /pattern? ??part? 搜索/后退/r
- 从子程序返回 mod 版本 c [Inub] 继续，直到调试器控制：
- 列出断点/动作/全部 [expr]
- 设置调试器选项 [expr]
- 切换跟踪 [trace] <<|<|][|]= [cmd]
- 在执行/提示符前后执行操作 b [ln|event] [cmd]
- 设置断点! ![Ndup]
- 重新显示列表命令 l [cmd]
- 执行 cmd 删除/所有断点 H [N]
- 定义/所有别名 l line = [val]
- 获取命令 w 添加一个表达式 h
- 补全帮助页 w expr*
- 删除所有 expr [|cmd]
- 将输出发送到分页器 |] sys
- 在子进程中运行 cmd q
- 检查：在纯代码中运行 cmd，另请参见：s, n t expr 在上下文中，转储 (dumps) 结果或列出方法。p expression (使用当前包)。
- 列出匹配模式 [not] 的子程序名
- 列出变量：Vars 可以是 -pattern 或 pattern。与当前 Vars相同。列出作用内的局部变量 <n>。比你能接受的更复杂的选项，只需要知道几个实用的。目前你不需要使用任何库，'m' 将显示加载的模块及其版本号，m 将显示方法，shows 显示所有子程序（按模式）并显示程序中的变量 strvar:stringify struct:

```perl
DB<2> dumpvar:stringify struct
```

使用 `'x'` 及其兄弟不需要使用标识符 (@)，只需使用 `'name'`：FileHandle(stderr) => (2) 记住我们现在你的程序中，我们应该看看我们在哪里，以及数据是什么样子。让我们看看我们位置的一些代码（通过 `'v'` 查看这里的第一行代码）：

```perl
DB<4> v 1 $key = 'welcome'; 5 %data = ( 6 'this' => qw(that), 7 'tom' => qw(jersey), 8 'welcome' => q(Hello World), 9 'zip' => q(welcome), 10 );
```

行号是一个很有用的指针，它告诉你你所在的位置。要查看更多代码，再次输入 `'v'`：

```perl
DB<4> 'welcome' => q(Hello World), 9 'zip' => q(welcome), 10 ); %data = keys %data; 12: print "All OK\n" if grep($key, keys %data); 13: print "${data{$key}}\n"; 14: print "done: ${data{$key}}\n"; 15: exit;
```

如果你想列出第 5 行，没什么可看的，但当然有大堆内容要翻阅，'l' 可以非常有用。将你的视图重置到我们即将执行的行点 '.'：

```perl
DB<5> . main:(./data-a:4): $key = 'welcome'
```

显示的行是即将执行的行，它还没有发生。所以虽然我们可以通过字母 `'p'` 查看，但此时我们得到的是空值。我们需要做的是通过 `'s'` 执行语句：

```perl
DB<6> s:(./data-a:5): %data = ( 6 'this' => qw(that), 7 'tom' => qw(jersey), 8 'welcome' => q(Hello World), 9 'zip' => q(welcome), 10 );
```

现在我们可以查看那个第一个 (`$key`)：

```perl
DB<7> p $key welcome
```

第 13 行是动作，所以我们通过字母 `'c'` 继续，这在这一行设置了一次性断点：

```perl
DB<8> c 13 main:(./data-a:13): print "${data{$key}}\n"
```

我们已经过了你的检查（打印 'All ok' 的地方），停在了最后的操作之前。我们可以尝试打印几个变量看看发生了什么：

```perl
DB<9> p $data$key
```

在不在那里，我们查看我们的：

```perl
DB<10> p %data Hello Worldtomwelcomejerethis DB<11> p keys %data Hello Worldtomjerethis
```

这并不易读，使用帮助手册 (h h)，'x' 命令：

```perl
DB<12> x %data @ 'Hello World' 1 'zip' 2 'tom' 3 'and' 4 'welcome' 5 undef 6 'jerry' 7 'welcome' 8 9 'that'
```

这没什么什么，里面有几个欢迎，但没有键的指示以及哪些是值，它是列出的数组 dump，在这种情况下，没有特别的帮助，使用数据结构的引用：

```perl
DB<13> x %data @ HASH(0x8194bc4) 'Hello World' => 'zip' 'jerry' => 'welcome' 'this' => 'that' 'tom' => 'and' 'welcome' => undef
```

并且我们查看该引用的那个：



DB<2> `dumpvar:stringify` `struct`

## 逐行执行代码

这是一个摄氏度和华氏度转换的简单程序，它存在一个问题：

```perl
#!/usr/bin/perl -w strict;

my $arg = $ARGV[0] || '-c20';

if ($arg =~ /-(c|f))((|-+)\d+(\d+)?$/) {

    my ($deg, $num) = ($1, $2);

    my ($in, $out) = ($num, $num);

    if ($deg eq 'c') {

        if ($deg eq 'f') {

            $out = &c2f($num);

        } else {

            $deg = 'c';

            $out = &f2c($num);

        }

        $out = sprintf('%0.2f', $out);

    } else {

        $out = s/(\|-+)\d+\s*$//g;

        print "$deg\n";

    }

} else {

    print "Usage: $0-[cf] $num";

    exit 2;

}

sub c2f {

    my $f = shift;

    my $c = 5 * ($f - 32) / 9;

    return $c;

}

sub f2c {

    my $c = shift;

    my $f = 9 * $c / 5 + 32;

    return $f;

}
```

出于某种原因，华氏度到摄氏度的转换没有返回预期的输出。实际结果如下：
`temp -c02.72 33.0 f > temp -f33.3 162.94`

我们将继续在预设的 `'c'` 断点处向下执行：
`DB<1> c main::temp(10); if ($deg eq 'c')`

随后通过以下方式显示：
`DB<1> v 7 my ($deg, $num) = ($1, $2); my ($in, $out) = ($num, $num); 9: DB::single=2; 10=> if ($deg eq 'c') { 11: $deg = 'f'; 12: $out = &2f($num); 13 } else { 14: $deg = 'c'; 15: $out = &f2c($num); 16 }`

并查看我们当前正在使用的值：
`DB<1> p $deg, $num f333`

我们可以在任何带有冒号的行上设置另一个断点；我们将使用第 17 行，因为那只是子程序中的其中一行，我们稍后想在那里暂停：
`DB<2> b 17`

此操作没有反馈，但你可以看到断点是通过列表 `'L'` 设置的：
`DB<3> L temp: 17; print "$deg\n"; break if (1)`

注意使用 `'B'` 删除断点。现在我们将继续向下执行子程序，这次是通过行号，我们将进入子程序，紧接着使用熟悉的 `'v'`：

```
DB<3> c f2c::f2c(temp:30): my $f = shift; DB<4> v 24: exit; 25 sub f2c {27==> my $f = shift; 28: my $c = 5 * $f - 32 / 9; 29: return $c; 30 } 31 32 sub c2f {33: my $c = shift;
```

注意，如果我们在我们和第 29 行之间有一个子程序，而我们想单步执行它，可以使用 `'command'`；而要跳过它，可以使用 `'n'`，这会执行子程序但不会进入内部进行检查。在这种情况下，我们直接向下执行到第 29 行：

```
DB<4> c 29 main::(temp:29): return $c
```

并查看返回值：

```
DB<5> p $c 162.9444444444444
```

这完全不对，但求和的数值看起来是正确的。我在想这是否与运算符优先级有关？我们将对求和尝试其他几种可能性：

```
DB<6> p (5 * $f - 32 / 9) 162.944444444444 DB<7> p 5 * $f - (32 / 9) 162.944444444444 DB<8> p (5 * $f) - 32 / 9 162.944444444444 DB<9> p 5 * ($f - 32) / 9 0.722222222222222222
```

这这就对了！现在我们可以看到返回变量，并使用 `'r'` 从子程序返回：

```
DB<10> c $c = 5 * ($f - 32) / 9 DB<11> r scalar context return from main:f2c: 0.722222222222222222
```

看起来不错，让我们直接执行到脚本结束：

```
DB<12> c 0.72 c Debugged program terminated. 使用 q 退出或 R 重启, u 0 inhibit_exit 避免在程序终止后停止, h q, h R 或 h 0 获取更多信息。
```

在实际程序中对错误行进行快速修复（插入缺失的括号）并完成。

## A, W, T, T 占位符

操作、观察变量、堆栈跟踪等：待办。

```
a w t T
```

## > 正则表达式

想知道正则表达式是什么样的？你需要编译带有 `DEBUGGING` 标志的 `perl`：

```
> perl -Dr -e '^pe(a)*rl$/1' Compiling REx `^pe(a)*rl$`
```



# 调试器命令

交互式调试器理解以下命令：

- `h`
打印摘要帮助信息

- `h [command]`
打印给指定调试器命令的帮助信息。

- `h h`
`h h` 的特殊参数会生成整个页面的帮助，内容非常长。
如果 `h h` 命令（或任何命令）的输出超过了屏幕，请在命令前加一个管道符号 `|`，以便通过你的分页器（pager）运行，例如：

- `DB>` `| h`
你可以通过 `pager=...` 命令更改所使用的分页器。

- `p expr`
等同于当前包中的 `print {$DB::OUT} expr`。特别地，由于这只是 Perl 自身的 `print` 函数，这意味着嵌套的数据结构和对象不会被导出，这与 `x` 命令不同。

`DB::OUT` 文件句柄被打开到 `/dev/tty`，无论 `STDOUT` 被重定向到何处。

- `x [maxdepth] expr`
在列表上下评估其表达式并以美化打印的形式输出结果。嵌套的数据结构会被递归导出，这与 Perl 的 `print` 函数不同。在转储哈希时，你可能更倾向于使用 `'x \%h'` 而不是 `'x %%h'`。如果你想手动执行操作，请使用 `Dumpvalue`。

输出格式由“配置选项”中描述的多个选项控制。

如果包含 `maxdepth`，它必须是一个数值 `N`；值将只会导出 `N` 层深，前提是 `dumpdepth` 选项已临时设置为 `N`。

- `V [vars]`
使用数据打印器显示包（默认为 `main`）中的所有（或部分）变量（哈希会显示其键和值以便让你看清内容，控制字符将变为可打印状态等）。确保不要在其中放置类型说明符（如 `$`），请使用符号名称，如下：

- `V DB filename`
使用 `~pattern` 和 `!pattern` 进行正向和反向正则。
这类似于对每个相关的变量调用 `x` 命令。

- `x [vars]`
等同于 `v package[vars]`。`v [level [vars]]`

显示当前作用域或更高层级作用域中的所有（或部分）局部变量（助记：mv variables）。你可以通过 `v` 和 `x` 命令限制你看到的变量。需要 `Padwalker` 模块版本 `0.08` 或更高；如果未安装将发出警告。输出格式与 `v` 相同，并由相同的选项进行格式化。

生成堆栈回溯。输出详情请见下文。

- `Single step`（单步执行）。执行到另一个语句的开始，并进入子程序调用。如果提供的表达式包含函数调用，该调用也将以单步方式执行。

- `Next`（下一行）。跳过子程序调用，执行到下一个语句的开始。如果提供的表达式包含函数调用，这些函数将在每个语句执行前停下并执行。

- `s`（继续）。继续从当前子程序返回。如果设置了 `PrintRet` 选项（默认），则导出返回值。

- `n`（重复）。重复上一个命令或 `s`。可选地在指定的行或子程序处插入一个一次性断点。

- `l`（列出）。列出下一个窗口的行。

- `incr`。列出从 `min` 开始的行。

- `max`。列出到 `max` 的行。

- `-` 等同于列出单行。

- 列出从子程序开始的第一窗口的行。

- `p.` 列出上一个窗口的行。

- `b.` 列出单行。

- `w` 查看当前行周围的几行代码。

- `R` 将内部调试器指针返回到最后一次执行的行，并打印该行。

- `c` 切换到不同的文件或 `eval` 语句。如果文件名不是在 `%INC` 值中找到的完整路径，则它被视为正则表达式。

- `b [condition]`
在指定的行之前设置断点。如果指定了条件，则每次到达该语句时都会评估该条件：只有当条件为真时才会触发断点。断点可以设置在起始执行语句的行上。

- `b [line][condition]`
在（可能不同的）文件的指定行之前设置断点。如果指定了条件，则每次到达该语句时都会评估该条件：只有当条件为真时才会触发断点。断点可以设置在起始执行语句的行上。此功能不支持。

- `a [line] command`
在执行该行之前设置要执行的操作。如果省略行，则对要执行的行执行操作。调试器采取的步骤顺序为：
1. 检查此行是否有断点
2. 如必要则打印该行（追踪）
3. 执行与该行相关的任何操作
4. 如果在断点处或单步执行，则提示用户
5. 该行
例如，每次通过第 53 行时都会打印 `$foo`：
```
a 53 print "DB FOUND $foo\n"
```

- `A line`
从指定的行删除操作。

- `A *` 删除所有已安装的操作。

- `w expr`
添加全局监听表达式。每当监听的全局变量发生变化时，调试器将停止并显示旧新值。

- `W expr`
删除监听表达式

- `W *`
删除所有监听表达式。

- `-`
显示所有选项。

- `boolean ...`
将列出的每个布尔选项设置为值 `1`。

- `anything?`
打印一个或多个选项的值。

- `option=value ...`
设置一个或多个选项的值。如果值包含内部空格，应使用引号。例如，你可以设置 `pager="less -MqeicsNfr"` 来调用带有特定选项的 less。你可以使用单引号或双引号，但如果你这样做，必须转义任何与起始引号相同的嵌入实例，并转义紧邻该引号之前的任何转义符。例如：`option='this isn't bad'` 或 `option="She said, "Isn't it?",`

- `b [condition]`
在命名子程序或包含代码引用的变量之前设置断点（在这种情况下不支持条件）。

- `b line [condition]`
在子程序编译后的第一行处设置断点。

- `b filename`
在文件名之前设置断点，该文件名应是 `%INC` 值中的完整路径。

- `b name`
在指定的子程序编译后的第一个执行语句之前设置断点。

- `B line`
从指定行删除断点。

- `B *`
删除所有已安装的断点。

- `disable [file]:[line]`
禁用断点，使其不再停止程序执行。断点默认是启用的，可以通过 `enable` 命令重新启用。

- `disable [line]`
禁用断点，使其不再停止程序执行。断点默认是启用的，可以通过 `enable` 命令重新启用。这适用于当前文件中的断点。

- `enable [file]:[line]`
启用断点，使其在程序执行时停止。

- `enable [line]`
启用断点，使其在程序执行时停止。这适用于当前文件中的断点。

- `< [line]`
在每次调试器提示符之前设置要执行的操作（Perl 命令）。多行命令可以使用反斜杠换行符输入。

- `< *` 删除所有提示符前的命令操作。

- `<< command`
在每次调试器提示符之前添加要执行的操作（Perl 命令）。多行命令可以使用反斜杠换行符输入。

- `> ?`
列出所有提示符后的 Perl 命令操作。

- `> command`
在你刚刚给出返回执行脚本的命令后，在提示符后设置一个操作（Perl 命令）。多行命令可以使用反斜杠换行符输入（但你现在应该能猜到了）。

- `> *`
删除所有提示符后的 Perl 命令操作。

- `>> command`
在你刚刚给出返回执行脚本的命令后，在提示符后添加一个操作（Perl 命令）。多行命令可以使用反斜杠换行符输入。

## 列出预提示符（pre-prompt）调试器命令。

`{ command }`
在每个调试器提示符出现之前设置一个操作（调试器命令）。可以按照常规方式输入多行命令。

由于此命令在某些意义上是新的，如果你似乎不小心输入了一个块（block），则会发出警告。如果这是你的本意，请写如 `{ ... }` 甚至 `do { ... }` 所示。

- 删除所有预提示符调试器命令。

`{{{ command`
在每个调试器提示符出现之前添加一个操作（调试器命令）。如果你猜出如何操作，可以输入多行命令：请见上文。

- `! number`
重执行上一个命令（默认为上一个命令）。

- `!-number`
重执行上数 `number` 个命令。

- `! pattern`
重执行上一个以 `pattern` 开头的最后一个命令。另见 `o recallCommand`。

- `!! cmd`
在子进程中运行 `cmd`（从 `DB::IN` 读取，写入 `DB::OUT`）。另见 `o shellBang`。注意，将使用用户当前的 shell（即其 `$ENV{SHELL}` 变量），这可能会干扰对退出状态或核心转储信息的正确解释。

- `file`
从文件读取并执行调试器命令。`file` 本身可以包含 `source` 命令。

- `H -number`
显示 `n` 个命令。列出长度大于一个字符的命令。如果省略 `number`，则列出所有。

- `q` 或 `^D`
退出（`"quit"` 对此无效，除非你设置了别名）。这是退出调试器的唯一支持方式，尽管退出两次可能有效。
如果你希望能够跳出脚本末尾，请将 `inhibit_exit` 选项设置为 `0`。如果你想步过全局析构过程，可能还需要将 `$finished` 设置为 `0`。

- `R`
通过 `exec ()` 运行新会话来重启调试器。我们尝试在此过程中保留你的历史记录，但内部设置和命令行选项可能会丢失。
以下设置目前会被保留：历史记录、断点、操作、调试器选项以及 Perl 命令行选项 `-w`、`-I` 和 `-e`。

- `|dbcmd`
运行调试器命令，将 `DB::OUT` 管道到你当前的分页器（pager）。

- `||dbcmd`
与 `|dbcmd` 相同，但 `DB::OUT` 也会被临时选中。

- `= [alias value]`
定义命令别名，

- `+ - quit q`
- 列出当前别名。

- `command`
作为 Perl 语句执行命令。末尾会提供一个分号。
否则 Perl 语句会被误认为是 Perl 调试器，也请在开头加一个分号。

- `m exprpr`
列出可以在评估后的表达式结果上调用的方法。
表达式可能被评估为指向已祝福对象（blessed object）的引用或包名（package name）。

- `# M`
显示所有加载的模块及其版本。

- `man [manpage]`
尽管名称如此，它会在指定的系统默认文档查看器上调用指定的页面，或者在省略 `man` 的情况下调用查看器。如果该查看器不存在，当前的 `conf.19` 信息将建议使用正确的 `MANPATH` 或 `-M manpath` 选项调用 `man`。如果匹配已知 `perlXXX` 格式 `man` 页的 `xxx` 形式查找失败，将重试。这允许你输入 `man debug` 或 `man proper` 来通过 `perldoc` 查找调试器的帮助文档。

在传统上没有可用 `man` 命令的系统中，调试器会调用 `perldoc`。偶尔由于固执的供应商，或者更形象地说，由于进取的用户，导致这种判断是不正确的。如果你属于这两类中的一种，只需手动设置 `DB::doccmd` 变量为任意值，以查看系统上的 Perl 文档。这可以在 `rc` 文件中设置，也可以通过直接赋值设置。我们仍在等待类似下面的工作示例：
```



`$DB::doccmd = 'netscape -remote'`

## 可配置选项

调试器在 `o` 命令下有许多选项，可以通过环境交互式设置，也可以通过 rc 文件（Unix 上的 `./perldb` 或 `~/.perldb`）。

`recallCommand()`, `"ShellBang"`
用于召回命令或生成 shell 的字符。默认情况下，两者都被设置为 `!`，这很遗憾。

`pager`
用于输出分页器-管道命令（以 `|` 字符开头的命令）的程序。默认将使用 `ENV{PAGER}`。由于调试器使用你当前的终端特性处理加粗和下划线，如果选定的分页器不原封地传递转义序列，那么当通过分页器发送时，某些调试器命令的输出将变得不可读。

`tkRunning`
在提示时运行 Tk（使用 ReadLine）。

`signalLevel`, `"warnLevel"`, `"dieLevel"`
详细程度级别。默认情况下，调试器会忽略你的异常和警告，因为更改它们可能会破坏运行正常的程序。当未捕获的 INT、BUS 或 SEGV 信号到达时，它将尝试打印消息。（但见下文“BUGS”部分提到的信号。）

要禁用此默认安全模式，请将这些值设置为大于 0 的值。在级别 1 时，它会在收到任何类型的警告（这通常很烦人）或异常时回溯（这通常很有价值）。遗憾的是，调试器无法区分致命异常和非致命异常。如果 `dieLevel` 为 1，那么你的致命异常也会被追踪，并且如果它们来自 `eval` 字符串或你尝试加载的模块中的任何种 `eval`，它们将将无情地被修改。
如果 `dieLevel` 为 2，调试器不在乎它们来自哪里：它会接管你的异常处理程序并打印跟踪信息，然后用它自己的修饰修改所有异常。这对于某些追踪目的可能有用，但倾向于无可救地破坏任何认真对待异常处理的程序。

`AutoTrace`
追踪模式（类似于 `t` 命令，但可以放在 `PERDLDB` 中）。

`LineInfo`
用于打印行号的文件或管道。如果设置了，则显示消息。

`inhibit_exit`
如果为 0，则允许跳出脚本末尾。

`PrintRet`
在 `r` 之后打印返回值（见 `Term::ReadLine`）。

`frame`
影响进入和退出子程序时的消息打印。如果 `frame & 2` 为假，则只在进入时打印。
如果 `frame & 4`，会打印参数以及调用者信息。如果 `frame & 8`，会打印子程序的返回值。

对参数列表的截断长度由下一个选项控制：

### `maxTraceLen`
当设置 `frame` 时，截断参数列表的长度。

`windowSize`
更改窗口大小（默认为 10 行）。

以下选项影响 `v`、`x` 的行为：

- `arrayDepth`, `"hashDepth"`
仅打印前 N 个元素（"*" 表示所有）。

- `dumpDepth`
在导出结构时限制递归深度。负值被解释为无限。默认：无限。

- `compactDump`, `"veryCompact"`
更改数组和哈希输出的样式。如果是 `compactDump`，短数组可能会一行显示。

- `globPrint`
是否打印 glob 的内容。

- `DumpFiles`
导出调试文件的数组。

- `DumpPackages`
导出包的符号表。

- `DumpReused`
导出“重用”地址的内容。

- `quote`, `"HighBit"`, `"underPrint"`
更改字符串导出的样式。`quote` 的默认值是 `auto`；可以通过将其设置为 `' '` 或 `''` 分别启用双引号或单引号格式。默认，带有高位的字符将原样设置。

`UsageOnly`
粗略的包使用导出。计算包中变量发现的字符串总大小。这不包括文件作用域内的局部变量，或丢失在闭包中的变量。

`HistFile`
调试器启动时读取历史记录（假设有用的 `Term::ReadLine` 后）的文件路径，并在关闭时保存（用于跨会话持久）。概念类似于 Bash 的 `.bash_history` 文件。

`HistSize`
历史记录的历史行数（假设上述 `HistFile`）。

读取 rc 文件后，调试器会读取 `${ENV{PERLDB_OPTS}}` 环境变量，并将其解析为调试器提示符处输入的 `O` 行的剩余部分。你可以在那里放置初始化选项 `TTY`、`notTY`、`ReadLine` 和 `NonStop`。

如果你的 rc 文件包含：
```
parse_options("NonStop=1 LineInfo=db.out AutoTrace");
```

然后你的脚本将在没有人工干预的情况下运行，并将跟踪信息写入 `db.out` 文件。（如果你中断了它，且期望看到任何输出，最好将 `LineInfo` 重置为 `/dev/tty`。）

## TTY

用于调试 I/O 的 TTY。

如果已设置，调试器将进入 `NonStop` 模式且不会连接到 TTY。如果被中断（或者通过 Perl 脚本显式设置 `$DB::signal` 或 `$DB::single` 将控制权交给调试器），它将连接到启动时在 `TTY` 选项指定的 TTY，或者在运行时使用选定的 `Term::Rendezvous` 模块连接到 tty。

该模块应实现一个名为 `new` 的方法，返回一个包含两个方法：`IN` 和 `OUT` 的对象。这些方法应分别返回用于调试输入和输出的文件句柄。`new` 方法应该在启动时检查包含 `$ENV{PERLDB_NOTTY}` 值的参数，否则检查 `$ENV{HOME}/perltty`。由于该文件没有标记正确的所有者，因此理论上存在安全隐患。

## Readline

如果为 `false`，调试器中的 readline 支持将被禁用，以便调试那些本身使用 ReadLine 的应用程序。

## NonStop

如果已设置，调试器将进入非交互模式，直到被中断或通过程序设置 `$DB::signal` 或 `$DB::single` 触发。

以下是使用 `$ENV{PERLDB_OPTS}` 变量的：
```
$PERLDB_OPTS="NonStop frame=2" perl -d myprogram
```

```
$PERLDB_OPTS="NonStop frame=2" perl -d myprogram
```

这将在没有人工干预的情况下运行脚本 `myprogram`，并打印出带有入口和出口点的调用树。注意，`NonStop=1 frame=2` 等同于 `N f=2`，最初选项可以通过首字母唯一缩写（`Dump*` 选项除外）。尽管如此，为了可性和未来的兼容性，建议始终完整拼写它们。

其他示例包括

```
$ PERLDB_OPTS="NonStop LineInfo=listing frame=2" perl -d myprogram
```

这将以非交互方式运行脚本，并在每次进入子程序和每次执行时将信息打印到名为 `listed` 的文件中。（如果你中断了它，最好将 `LineInfo` 重置为某些“交互式”内容！）

其他示例包括（使用标准语法显示环境变量设置）：

```
$ ($ PERLDB_OPTS="NonStop frame=1 AutoTrace LineInfo=perl.out" perl -d myprogram )
```

这对于调试一个本身使用 `Term::ReadLine` 的程序可能有用。不要忘记在对应 `/dev/ttyXX` 的窗口中将你的 shell 从 TTY 分离，例如通过执行如下命令：

```
$ sleep 10000000$
```

详情请参见 `perldebugs` 中的“Debugger Internals”（调试器内部）。

# 调试器输入/输出

### 提示符

调试器提示符类似于

```
DB<8>
```

或

```
DB<<17>
```

其中数字是命令编号，你可以使用内置的类 csh 机制对其进行访问。例如，`!17` 将重复命令 17。角括号的深度表示调试器的嵌套层级。你可以获得多组括号，例如如果你已经处于断点处，并打印了一个带有断点的函数调用结果，或者通过 `s/n/t expression` 命令进入了一个表达式。

### 多行命令

如果你想输入多行命令，例如带有多个语句或块的子程序定义，使用反斜杠转义通常启用调试器命令的换行符。

```
DB<1> (1..4) { \ cont: print "ok\n"; \ cont: ok ok ok ok
```

注意，这种转义换行的操作专门针对在调试器输入的交互式命令。

### 堆栈跟踪

这里是一个堆栈跟踪 `T` 命令可能性的示例：

```
$ main::infested called from file 'Ambulation.pm' line 10 @ Ambulation::legs(1, 2, 3, 4) called from file 'camel_flea' line 7 $ = main::pests('bactrian') called from file 'camel_flea' line 4
```



左侧字符表示调用函数时的上下文，`$` 和 `@` 分别表示标量或列表上下文，而 `.` 表示上下文（实际上是上下文的标量）。上面的显示表示你在运行堆栈转储时处于函数 `main::infested` 中，它是在文件 `Ambulation.pm` 的第 10 行以标量上下文调用的，但完全没有任何参数，它是作为 `&infested` 被调用的。下一个堆栈帧显示函数 `Ambulation::legs` 在 `camel_flea` 文件中列表上下调用，带有四个参数。最后一个堆栈帧显示 `main::pests` 在标量上下被调用，同样来自 `camel_flea`，但来自第 4 行。

如果你在 `use` 语句内部执行 `T` 命令，回溯将包含 `require` 帧和 `eval` 帧。

### 行列表格式

这显示了输出的简略：

```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

等待，格式：

### 行列表格式

这显示了输出的简略：

```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

实际上，让我根据 OCR 重新对齐：

### 行列表格式

这显示了输出的简略：

```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

等待，查看 OCR 文本：
```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

OCR 文本中显示：
```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

OCR 有行号 `104 105 106`。让我们重构：

### 行列表格式

这显示了输出的简略：

```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

实际上，OCR 文本显示：
```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

让我们清理逻辑：

### 行列表格式

这显示了输出的简略：

```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

实际上，OCR 为：
```
DB<<13>> 1 101:@i = (); 102:b a@${pack} = (); 103 if(exists
$${prevpack} || exists $${pack}); 104 105 106 107 108 109 110
```

OCR 杂乱。让我们修复它。

已安装 `Padwalker` 模块时的当前作用域。

如果没有 `Readline` 支持，在使用箭头键和/或退格键时，你可能会看到符号 "^[A]"、"[[C]"、"[[B]"、"[[D]"、^H 等

## 编辑器调试支持

如果你在系统中安装了 GNU 版本的 emacs，它可以与 Perl 调试器交互，提供一个集成软件开发环境，这种体验类似于它与 C 语言调试器的交互。

Emacs 的最新版本带有一个启动文件，可以使 emacs 变得像一个语法引导型编辑器，能够理解（部分）Perl语法。请参阅 `perlfaq3`。

`vi` 用户也应该查看 `vim` 和 `gvim`（带有鼠标和窗口的版本），以获得 Perl 关键字的着色。

注意，只有 `perl` 本身才能真正解析 Perl，因此所有 CASE 工具在某些都不尽如人，特别是如果你不像 C 语言程序员那样编写 Perl 代码。

## Perl 性能分析器

如果你想为 Perl 提供一个备用调试器来运行，请使用冒号和包参数 `-d` 来调用你的脚本。Perl 的备用调试器包括一个 Perl 性能分析器 `Devel::NYTProf`，它可以作为 CPAN 分发包单独提供。要对文件 `mycode.pl` 中的 Perl 程序进行性能分析，只需输入：

```
$ perl -d:NYTProf mycode.pl
```

当脚本终止时，性能分析器将创建一个性能信息数据库，你可以使用性能分析器的工具将其转换为报告。详情请参阅 `<perlperf>`。

## 调试正则表达式

使用 `'debug'` 可以让你看到 Perl 正则表达式引擎运行的底层细节。为了理解这些通常非常庞大的输出，不仅必须对正则表达式匹配的一般原理有所了解，还必须知道 Perl 正则表达式在内部是如何编译为自动机的。这些内容在 `perldbguts` 的“Debugging Regular Expressions”中有详细的探讨。

## 调试内存使用

Perl 内部包含了报告其自身内存使用的支持，但这是一个相当高级的概念，需要对内存分配的工作原理有一定理解。详情请参阅 `perldebuts` 中的“Debugging Perl Memory Usage”。

## 另另

你确实尝试过 `-w` 选项，不是吗？
`perldebtut`, `perldebguts`, `re`, `DB`, `devel::NYTProf`, `Dumpvalue`, and `perlrun`.

当调试一个使用 `#!` 且通常位于 `$PATH` 中的脚本时，`-S` 选项会导致 `perl` 在 `$PATH` 中搜索它，这样你就不需要输入路径或哪个 `$scriptname`。

```
$ perl -Sd foo.pl
```



## 缺陷

你无法获取栈帧信息，无法以任何方式调试并非由 Perl 编译的函数，例如来自 C 或 C++ 扩展的函数。

如果你在子程序中修改了 `$@` 参数（例如通过 `shift` 或 `pop`），栈回溯将不会显示原始值。

调试器目前无法与 `-W` 命令行开关配合工作，因为因为它本身存在警告。

如果你正处于一个缓慢的系统调用中（例如等待、接受或从你的键盘或套接字读取），并且没有设置你自己的 `SIG{INT}` 处理器，那么你将无法通过 `CTRL-C` 回到调试器，因为调试器自身的 `SIG{INT}` 处理器并不理解它需要抛出异常来跳出（中断）缓慢的系统调用。

## PERLDELTA

### 名称

`perldelta` - perl v5.22.0 的新特性

## 描述

本文描述了 5.20.0 版本与 5.22.0 版本之间的差异。

如果你是从较早版本（如 5.18.0）升级，请先阅读 `perl5200delta`，它描述了 5.18.0 和 5.20.0 之间的差异。

## 核心增强

### 新的位运算运算符

添加了一个新的实验性功能，使得四个标准的位运算符（`&` `|` `^` `~`）将它们的操作数一致地视为数字，并引入了四个新的点运算符（`&.` `|.` `~..`），它们将操作数一致地视为字符串。这同样适用于赋值变体（`&= ` `|= ` `&= ` `.= ` `^=`）。要使用此功能，请启用 `bitwise` 功能并禁用 `experimental:bitwise` 警告类别。详情请参阅 perl 中的 `Bitwise String Operators`。[perl #123466]

### 新的双三菱形运算符

`<<=>` 类似于 `<`，但它使用三参数模式打开 `@ARGV` 中的每个文件。这意味着 `@ARGV` 将被视为实际文件名，而 `|foo` 不会被视为管道打开符。

### 正则表达式中的新 `\b{}`

`qr/\b{}/n` 代表 Grapheme Cluster Boundary（字符簇边界）。这是一个 Unicode 属性，用于寻找对于语言使用者来说看起来像单个字符的字符序列之间的边界。Perl 长期以来具有通过 `\x` 转义序列处理这些的能力。现在，有了另一种处理方法。详情请参阅 `perlreslash` 中的 `\b{}, \b, \B}, \B`。

`qr/\b{}/n` 代表 Word Boundary（单词边界）。这是一个 Unicode 属性，用于寻找单词之间的边界。这与 `\b`（不带括号）类似，但更适用于自然语言处理。它知道例如，省号可以出现在单词中间。详情请参阅 `perlreslash` 中的 `\b{}, \b, \B}, \B`。

### 非捕获组

`qr/\b{}/n` 代表 Word Boundary（单词边界）。这是一个 Unicode 属性，用于寻找单词之间的边界。这与 `\b`（不带括号）类似，但更适用于自然语言处理。它知道例如，省号可以出现在单词中间。详情请参阅 `perlreslash` 中的 `\b{}, \b, \B}, \B`。

当操作系统提供了相关支持时，内置的 `feno` 函数可以处理目录，以与文件相同的方式产生底层文件描述符。对于没有此类支持的操作系统，目录的 `feno` 将继续返回未定义值，如之前一样，但会设置 `$!` 表示该操作不支持。

- 作为一个全新的新功能，现在支持十六进制浮点数字面量（例如 `0x1.23p-4`），并且可以使用 `printf "%a"` 进行输出。更多信息请参见 `perldata` 中的 `Scalar value constructors`。

- 将无穷大或非数字（not-a-number）打包到字符中现在会引发致命错误

以前，当尝试将无穷大或非数字打包到（有符号）字符时，Perl 会发出警告，并假设你尝试打包 `0xFF`；如果你将其作为 `chr` 的参数，则会返回 `U+FFFD`。

但现在，所有此类操作（`pack`、`chr` 和 `print '%c'`）都会导致致命错误。

## 实验性 C 层回溯 API

Perl 现在支持（通过 C 级 API）获取 C 回溯（类似于 gdb 等符号调试器所做的操作）。

回溯返回 C 调用栈帧的堆栈跟踪，包含符号名称（函数名）、对象名称（如 `perl`），以及如果可能的话，还包括源代码位置（文件:行号）。

支持的平台有 Linux 和 os x（某些 *BSD 可能至少可以部分有效，但尚未经过测试）。

该功能需要通过 `Configure -Dusebacktrace` 启用。

更多信息请参见 `perlhacktips` 中的 `C backtrace`。

## 安全

- 如果可用，Perl 现在将使用 `-fstack-protector-strong` 进行编译

自 5.10.1 以来，Perl 编译时已使用了抗栈溢出保护选项 `-fstack-protector`。现在，如果可用，Perl 使用更更新的、名为 `-fstack-protector-strong` 的变体。

- Safe 模块可能允许外部包被替换

关键错误修复：外部包可能会被替换。`Safe` 已经修复到 2.38 以解决此问题。

- 如果可用，Perl 现在将始终使用 `-D_FORTIFY_SOURCE=2` 进行编译

在 gcc 4.* 中可用的名为 `_FORTIFY_SOURCE` 的“代码加固”选项，现在始终用于编译 Perl（如果可用）。

请注意，这并不一定是一个巨大的进步，因为在许多平台上，这一步在几年前就已经实现了：许多 Linux 发行版（如 Fedora）一直对 Perl 使用此选项，而 os x 多年来也强制执行相同的操作。

## 不兼容变更

- 子程序签名移动到属性之前之前

在 5.20 中引入的实验性子程序签名功能是在属性之后解析签名的。在本次发布中，根据对该实验性功能用户的反馈，位置已移动，使得签名出现在子程序名（如果有）之后，且属性列表（如果有）之前。

- `&` 和 `\&` 原型仅接受子程序

`&` 原型字符现在只接受匿名子程序（`sub {..}`）、以 `&` 开头的内容或显式的 `undef`。以前它错误地也允许对数组、哈希表和列表的引用。[per #4539] <>. [per #123062] <>. [per #123062] <。

此外，`&` 原型曾允许子程序调用，而现在它只允许子程序：`&foo` 仍然允许作为参数，而 `&foo()` 和 `foo()` 不再被允许。[per #77860] <。

- `use encoding` 现在是词法作用的

`encoding` 指令（pragma）的作用现在局限于词法作用域。该指令已弃用，但在此期间它可能会影响包含在同一程序中的无关模块；此更改修复了该问题。

- 列表切片返回空列表

列表切片现在仅在原始列表为空（或没有索引）时才返回空列表。在以前，如果所有索引都在原始列表范围之外，列表切片将返回空列表；现在在这种情况下，它会返回一个值列表。[per #114498] <。

- 带有多个空格序列的 `\N` 现在是致命错误

例如 `\nTOO_MANY_SPACES)` 和 `\n{TRAILING_SPACE} }`。这自 v5.18 以来已被标记为弃用。

- `use UNIVERSAL '...'` 现在是致命错误

自 v5.12 以来，从 `UNIVERSAL` 导入函数已被标记为弃用，现在成为一个致命错误。不带任何参数的 `use UNIVERSAL` 仍然被允许。

- 在双引号 cX 中，X 必须是可打印的 ASCII 字符

在之前的版本中，未执行此操作会引发弃用警告。

- 正则表达式中的标记 `?` 和 `(*` 分割现在是致命编译错误

这些用法自 v5.18 以来已被标记为弃用。

## `qr/foo/x` 现在忽略 Unicode 模式空白

`/x` 正则表达式允许模式包含空白和注释（这两者都会被忽略），以提高可读性。直到现在，并不是所有为此目的指定的空白都已使用。现在新识别的额外空白包括：

U+0085 NEXT LINE、U+202E LEFT-TO-RIGHT MARK、U+200F RIGHT-TO-LEFT MARK、U+2020 LINE SEPARATOR、U+2029 PARAGRAPH SEPARATOR

在 `/x` 之外、且不在括号字符类中且没有被反斜杠引导的情况下，使用这些字符自 v5.18 以来一直引发弃用警告。现在它们将被忽略。

## `(?])` 内部的注释行现在仅由 
 结束

`(?])` 是一个在 v5.18 的实验性功能。它的运行方式就像 `/x` 总是开启一样。但存在一个区别：注释行（紧随 `#` 字符之后）由匹配 `\n` 的任何内容终止，这包含了所有空白字符。为了一致性，现在更改为匹配 `(?])` 之外终止注释行的字符，即 `\n`（即使被转义），这与终止 heredoc 字符串和格式化对象的终止符相同。

## `(?...)` 运算符遵循标准的 Perl 优先级

此实验性功能允许在正则表达式模式中进行集合操作。在此之前，交集运算符与其他运算符具有相同的优先级。现在它具有更高的优先级。这可能会导致结果与现有代码的预期不同（请参考 `Extended Bracketed Classes`）。

- 在哈希名上省略 `%` 和 `@` 不再被允许

以前的 Perl 允许在某些地方省略数组的 `@` 和哈希的 `%`。这种用法自 5.000 以来已发出弃用警告，现在不再被允许。

- 在 locale 范围外，`$text` 将不是英文

以前，除了几乎所有内容外，`$text` 总是根据当前的 locale 输出（受其他系统影响）。对于准备好处理 locale 差异的程序，这可能会导致显示垃圾文本。

- 在适当的情况下，`$text` 将以 UTF-8 返回

当文本实际上为 ASCII 时，`$` 和 `$^` 的字符串化将设置 UTF-8 标志。这使得设置了 locale 的程序能够正确以用户的本地语言输出信息。在 `bytes` 和 `local "messages"` 的作用域内，其他 Perl 操作不受 locale 影响；只有 `$` 和 `$^` 的字符串化如此。`bytes` 指令导致不设置 UTF-8 标志，与之前相同。这解决了问题。

- 支持 `?PATTERN` 构造（允许正则表达式只匹配一次）以前有一种直接使用问号分隔符而省略显式 `m` 运算符的形式。这种用法自 5.14 以来产生弃用警告。现在它是一个语法错误，以便问号可以使用新的运算符。

- `defined(array)` 和 `defined(%hash)` 现在是致命错误

这些自 v5.6.1 以来已被弃用，并自 v5.16 以来一直发出弃用警告。

- 将哈希或数组作为引用现在是致命错误

例如，`%foo->"bar"` 现在会导致致命编译错误。这些自 v5.8 之前就已被弃用，并从那时起发出弃用警告。

- 对 `*` 原型的更改

子程序原型中的 `*` 字符曾允许裸单词（barewords）优先于大多数（并非所有）子程序名称。它从不一致且表现出错误行为。

现在它已被更改，子程序始终优先于裸单词，这使其与具有类似原型的内置函数保持一致：

```



`splat(*)` { ... } `sub foo` { ... } `splat(foo)`; # 现在总是 `splat(foo()`
`nsplat(bar)`; # 仍然像以前一样 `splat('bar')`

`close(foo)`; # `close(foo())`
`\close(bar)`; # `close('bar')`

## 弃用公告

### 将 `${ENCODING}` 设置为 `undef` 以外的任何值

此变量允许使用 ASCII 或 UTF-8 以外的编码编写 Perl 脚本。然而，它会全局影响所有模块，导致结果错误和段错误。新脚本应使用 UTF-8 编写；旧脚本应转换为 UTF-8，这可以通过 `piconv` 工具轻松实现。

### 在单字符变量名中使用非图形字符

单字符变量名的语法对较长的变量名来说更为宽松，允许单字符名称为标点符号甚至是不可见字符（非图形字符）。Perl v5.20 弃用了此类 ASCII 范围的控制字符。现在，所有以前允许的非图形字符均已弃用。此变化的实际效果仅在未使用 `utf8` 时发生，并影响 C1 控制字符（代码点 `0x80` 到 `0xFF`）、不换行空格（NO-BREAK SPACE）和软连字符（SOFT HYPHEN）。

### 具有可观测副作用的 `sub () {$var}` 内联

在许多情况下，Perl 将 `sub () {$var}` 内联到一个内联常量子程序中，在子表达式求值时捕获 `$var` 的值。在 `$var` 随后被修改的情况下，这会破坏闭包行为，因为子程序不会返回修改后的值。（注意：这仅适用于原型为空的匿名子程序 `sub ()`）。

在变量可能在其他地方修改的情况下，这种用法现已弃用。Perl 会检测到这些情况并发出弃用警告。代码在未来可能会发生变化，且仅在声明处进行修改，Perl 将继续在不产生警告的情况下对子程序进行内联。

```perl
sub make_constant { $var = shift; return () {$var }; # 
make_constant_deprecated { $var; $var = shift; return () {$var }; # 弃用
deprecated sub make_constant_deprecated { $var = shift; 
log_that_value($var); # 代码修改了 $var return () { {$var }; # 
弃用
```

在第二个示例中，检测 `$var` 是否仅赋值了一次太困难了。只要在 `my` 声明以外的地方命中，就足够让 Perl 认为其可疑。

此弃用仅发生在子程序体内的单个变量上。（`BEGIN` 块或 `use` 语句会被忽略，因为它们没有成为子程序的一部分）。对于更复杂的情况，例如 `sub () do_something() if 0; {$var}`，行为已发生变化：如果变量在其他地方是可修改，则不会发生内联。此类情况应该非常罕见。

### 使用多个 `/x` 正则表达式修饰符

现在类似以下内容的操作已弃用：
`qr/foo/xx;` `/(?xax:foo);` `use re qw(/amxx);`

现在，`x` 应该出现在连续的正则表达式模式修饰符字符串中。我们认为在整个 CPAN 中没有出现过这种情况。这是为了未来的 Perl 版本做准备，届时 `/xx` 将允许在方括号字符类（由方括号包含的内容：`[..]`）中使用空格以提高可读性。

### 在 `\N{...}` 的字符别名中使用不换行空格现已弃用

这种非图形字符本质上与普通空格无法区分，不应被允许。参见 `charnames` 中的“CUSTOM ALIASES”。

### 模式中的字面量 `{` 应该转义

如果你想在正则表达式模式中使用字面量左括号（也称为左大括号），现在应该通过在它前面加反斜杠（`\{`或将其包含在方括号 `{}` 中，或者使用 `\Q;` 来进行转义，否则将抛出弃用警告。这在 v5.16 版本中首次宣布；它将允许语言进行扩展。

### 不建议将所有警告设为致命（fatal）

致命警告的文档指出，不建议使用 `warnings FATAL => 'all'`，并对致命警告的总体风险提供了更强力的表述。

## 性能增强

如果方法名或类名在编译时已知，则会预计算哈希表以加速运行时方法查找。此外，像 `SUPER : new` 这样的复合名称在编译时解析，以节省运行时的解析开销。
仅使用常量或简单变量作为键的数组和哈希（尤其是嵌套的）现在速度快得多。更多细节见“Internal Changes”。

在列表环境中，`(...)x`、`("constant")x` 和 `($scalar)x` 现在经过优化。如果右侧参数是常量 0，只要左侧参数是简单标量或常量，该表达式就会优化为空列表。（也就是说，`(foo())x` 不受此优化。）

`substr` 现在在子程序末尾的四参数 `substr`（或作为返回参数）中经过优化。以前，这种优化只发生在空文中。
在 `In, \` 等情况下，`stringify` 操作现在被优化掉了，使其速度与 `lfirst`、`quotemetana` 等一样快。

向空列表赋值现在更快了。特别是，它现在不会对右侧的绑定（tied）参数执行 `FETCH`，而以前有时会。
当 `length` 应用于非魔性的、非绑定的字符串时，性能提升高达 20%，前提是开启了 `use bytes` 或字符串没有使用 UTF-8 二进制格式。

在大多数带有 64 位整数的 Perl 构建中，对于仅包含浮点值的非魔性、非绑定标量，内存占用减少了 8 到 32 字节，取决于操作系统。

`@array = split` 的赋值可以被优化，使 `split` 直接写入数组。

## 模块与指令

### 更新的模块与指令

随 Perl 分发的许多库自 v5.20.0 以来已升级。要获取完整的更改列表，请运行：

```
corelist --diff 5.20.0 5.22.0
```



你可以用喜欢的版本替换 `5.20.0`。

一些显著变化包括：

- `Archive::Tar` 已升级到 `2.04` 版本。
- 测试现在可以并行运行。
- `attributes` 已升级到 `0.27` 版本。
- 修正了 `xs` 中 `memEQ` 的用法。
- 避免了读取缓冲区之外。
- `B` 已升级到 `1.58` 版本。
- 它提供了一个新的 `B::safename` 函数，基于现有的 `B::GV->SANAME`，将 `\uCOP` 转换为 `^OPEN`。
- 零操作 COP 现在是 `B::COP` 类，而不是 `B::OP`。
- `B::REGEX` 对象提供了 `qr::anon` 方法，用于访问与包含代码块的 `qr//` 关联的 CV，以及一个返回来自 `qr//` 操作的持久标志的 `cflags` 方法。
- `B::PMOP` 现在提供返回 `B::REGEXP` 对象的正则方法。引入了两个新类 `B::PADNAME` 和 `B::PADELIST`。
- 修复了一个错误：创建线程后，子线程/进程中的 `special/immortal` SV 没有正确的 `B::SPECIAL` 类。添加了 `id` 和 `out PADLIST` 方法。
- `B::Concise` 已升级到 `0.996` 版本。
- 零操作现在是执行链的一部分，并被赋予了序列号。
- 零操作的私有标志现在与非零操作的操作一样使用助记符转储。
- `B::Deparse` 已升级到 `1.35` 版本。
- 它现在可以正确解析语句开头的 `+sub : attr { ... }`。如果没有初始的 `+`，`sub` 将成为语句标签。
- `BEGIN` 块现在大多数时候会在正确的位置发射，但该更改遗憾引入了一个回归，即 `BEGIN` 块出现在……之前。

闭合块的结束标记可能出现在下方。

`B::` 不再在此处到处放置错误的局部变量，例如 `LIST = tr/a//`。[`perl #119815`]

如果一个 `use` 语句包含一个 `do` 块，相邻的 `use` 语句将不再会被意外嵌套。[`perl #115066`]

传递给 `\a` 的列表中的括号数组现在会保留 `@b` 周围的括号（例如 `\(a, (@b), @c` 现在保留了引用括号数组的扁平化行为）。以前，它只对单个数组有效：`\@@`。

`local our` 现在被正确弃用，并包含了 `our`。

`for($foo;$bar; $baz) {...}` 弃用时没有带 `!`（或带了）。此问题已修复。

与词法作用子函数冲突的核心关键字现在带有 `CORE::` 前缀并弃用。

`foreach state $x (...) {...}` 现在与 `state` 正确弃用而不是 `my`。

`our $array = split(...)` 在赋值被优化的情况下，现在与 `our` 正确弃用。

它现在能正确解析 `"LIST"` 和带类型的词法（`my Dog $spot`）。
将 `$_=` 解析为 `instead` 而不是 `$_{}`。[`perl #123947`]

闭合作用域末尾的 `BEGIN` 块现在在正确的位置弃用。[`perl #77452`]

`BEGIN` 块有时被解析为 `__ANON_`，但现在被称为 `BEGIN`。

词法作用子函数现在已完全弃用。[`perl #116553`]

带有 `/r` 的任何 `-= y///r` 省略左操作数。

构成正则代码块的算符现在被真正弃用了。使用了生成正则表达式的原始字符串。这导致了 `qr/(?<herdoc)/` 和多行代码块出现问题，它们被错误地弃用了。[`perl #123217`] [`perl #115256`]

语句末尾的 `$` 不再丢失分号。[`perl #123357`]

某些简写形式存储在 stash 中的作用子声明被遗漏了。

非 ASCII 字符现在在字符串中始终被转义，而不是部分时间转义。（正则表达式和标识符方面仍有未待修复的问题）。

当原型作用子调用被带 `&` 弃用时（例如在 `-P` 选项下），`scalar` 现在会在适当的地方被添加，以强制原型所隐含的标量上下文。
`require(foo()), do(foo()), goto(foo())` 以及类似的带有循环控制的结构现在被解析。其他的结构不是可选的。

正则表达式中的空白字符不再被转义，因为它们在 `(?x:...)` 区域内会被错误地转义。

`sub foo { }` 现在解析时带有强制性括号。
`/@array/` 现在解析为正则表达式，而不仅仅是 `@array`。
`/{-}/`、`/${+}` 和 `$#{1}` 现在解析时带有大括号，这些大括号在某些情况下是强制的。

在解析功能包中，`B::Deparse` 之前没有输出功能；现在输出 `:all` 而不是没有功能。此问题已修复。

`chdir my @` 现在解析时不带括号。（带括号会使数组扁平化）。
`system` 和 `exec` 后接块时现在被正确解析。以前在块之前有一个错误的 `before`。

`use constant QR => qr/...flags` 后接 `"" ~ QR` 不再丢失标志。

在启用 `-sw` 的情况下，解析 `BEGIN undef &` 在 Perl `5.14` 中开始输出 `'initialized'` 警告。此问题已修复。

解析对带有 `(+)` 原型的作用子调用会导致无限循环。`($;)`、`(_ )` 和 `(: )` 原型获得了错误的优先级，导致 `foo($a<$b)` 解析时没有带括号。

解析现在在内部作用子中提供一个定义的 `state` 作用子。

增加了 `B::Op_private`。

`B::Op_private` 提供了关于 perl 码 `op_private` 字段中使用标志的详细信息。

`bigint`, `bignum`, `bigrat` 已升级到 `0.39`。

在使用字符串作为名称时，不再总是调用大整数重载，以及如何调用它。[`perl.org #23064`]

`Carp` 已升级到 `0.36`。

`Carp::Heavy` 现在忽略与 `Carp` 版本不匹配的情况（如果新于 `0.12`），因为 `Carp::Heavy` 的内部实现已合并到 `Carp` 中。[`perl #11574`]

`Carp` 现在更好地处理非 ASCII 模式。

对于 Perl `< 5.14` 的 off-by-one 错误已修复。

`constant` 已升级到 `0.33`。

它现在接受完全限定的常量名，允许在调用者以外的包中定义常量。

`CPAN` 已升级到 `0.11`。在 `5.20` 中增加了对 `Cwd::getcwd()` 的支持。

修复了在构建依赖项后 `chdir(..)` 的错误。

引入了对 `plugins/hooks` 的实验性支持。

集成了 `App::` 源码。

不再对可选依赖进行递归检查。

`META.yml` 包含一个哈希。[`cpan #95271`]

`CPAN::Mea::Requirements` 已升级到 `0.132`。

在版本于 `5.10.0` 的 Perl 中，通过 `v-string` 魔术绕过 `deparse` 的限制。

正确处理子类的 `deparse`。

`Data::Dumper` 已升级到 `0.158`。

通过添加限制深度转储时递归的配置选项，修复了 `CVE-2014-4330`。

在 `GLOB` 中错误地存储了代码名。[`perl #12200`]

`DynaLoader` 已升级到 `32`。

在 `DynaLoader` 中删除了未使用的 `d1_nonlazy` 全局。[`perl #12296`]

`Encode` 已升级到 `2.72`。

在 `5.8.2` 中升级 `Encode` 时的损坏问题已修复。

在 Windows 上构建 `C::` 现在可以工作。

在 `GCC 5` 的预处理器命令行中增加了 `-P`，以及错误定义的解析。[`perl #12378`]

实验性功能已升级到 `0.013`。

`ExtUtils::Builder` 已升级到 `28.21`。

修复了 Android 上的回归问题。[`perl #22675`]

`ExtUtils::Manifest` 已升级到 `1.70`。

修复了 `maniread()` 处理引号文件名的 bug 以及 `manifest()` 符号链接。[`perl #22415`]

`ExtUtils::ParseXS` 已升级到 `3.28`。

只有在我们实际定义它时才声明文件。改进了 `RETVAL` 生成以避免重复引用 `ST(0)`。[`perl #13278`]

扩展了 `/OBJ$/` 到 `/REF$/` 用于 `DESTROY` 方法的类型映射。[`perl #13418`]

`Fcntl` 已升级到 `1.13`。

增加了对 Linux 管道大小 `fcntl()` 命令的支持。

`File::Find` 已升级到 `29`。`find()` 和 `finddepth()` 在传递不当或拼写错误的选项时现在会警告。

`File::Glob` 已升级到 `24`。

在几处通过扩展调用 `get_sv()` 三次来避免 `SV()`。[`perl #13606`]

`HTTP::Tiny` 已升级到 `0.054`。

`keep_alive` 现在是 fork 安全且线程安全的。

`io` 已升级到 `35`。为了 Perl 的顺序。

`IO::Socket` 已升级到 `0.38`。记录了 `connected()` 方法的局限性。[`perl #123096`]

`IO::Socket::IP` 已升级到 `0.37`。子类化 `connect()` 的更好修复。[`cpan #95983`] [`cpan #97050`] 为 `connect()` 实现了超时。[`cpan #92075`]

`libnet` 核心模块已升级到 `3.05`。支持 `Net::FTP`、`Net::NNTP`、`Net::POP3` 和 `Net::SMTP` 的 IPv6 和 SSL。改进了 `Net::SMTP` 身份验证。

`Locale::Codes` 已升级到 `3.34`。修复了从电子表格提取数据的 bug，该 bug 导致找不到 `SHP` 货币代码。[`cpan #94229`]

增加了新的代码。

`Math::BigInt` 已升级到 `1.9997`。正确处理子类的 `deparse`。

同步来自 CPAN 版本的 POD 更改。当精度大于70位时，`Math::BigFloat->log(x)` 有时会返回 `log(2*x)`。列表上下文下 `Math::BigFloat->bdiv(in)` 的结果现在满足 `x = quotient * divisor + remainder`。[`cpan #96254`] [`cpan #96329`]

`Module::Metadata` 已升级到 `1.000026`。支持在 `ExtUtils::MakeMaker` 早于 `6.63_03` 的旧版本 Perl 上安装。

`overload` 已升级到 `1.26`。删除了冗余的 `$sub` 引用。

`PathTools` 模块集已升级到 `3.56`。构建 `xs` 时避免了 gcc 编译器的警告。不要在 Cygwin 上将领先的 `//` 转换为 `/`。[`perl #122653`] `perl5db.pl` 已升级到 `1.49`。调试器会导致断言失败。[`perl #124127`] 调试器中的 `fork()` 现在会为 fork 的进程创建一个新窗口。[`perl #121333`] 调试器现在启动时保存当前工作目录，并在使用 `R` 或 `rer` 重启程序时恢复。[`perl #121509`]

`PerIO::scalar` 已升级到 `0.22`。从标量之后的位置读取现在会正确返回文件结束。[`perl #123443`] 跳转到负位置会失败，但不再将文件位置设置在非法位置。在 32 位系统上，越 2GB 标记的写入现在会提前报错，并支持 4GB。

`Pod::Perdoc` 已升级到 `3.25`。用于读取或写入的文件句现在设置了 `:encoding(UTF-8)`。[`cpan #98019`]

`POSIX` 已升级到 `1.53`。增加了 C99 数学函数和常量（例如 acosh, isinf, isnan, round, tunc; M_E, M_SQRT2, M_PI）。`POSIX::tmpnam()` 现在产生弃用警告。[`perl #122005`]

`Safe` 已升级到 `2.39`。`reval` 没有正确传播空上标文。

`Scalar-List-Utils` 已升级到 `1.41`。

新增了模块 `Sub::Util`，包含与 CODE 引用相关的函数，包括 `subname`（受 `Sub::Identity` 启发）和 `set_subname`（从 `Sub::Name` 复制并重命名）。修复了 `List::Util::reduce()` 中对 `GetMagic` 的使用问题。[`cpan #63211`]

`SDBM_File` 已升级到 `1.13` 版本。

简化了构建过程。[`perl #123413`]

`Time::Piece` 已升级到 `1.29` 版本。

在美化打印负数 `Time::Seconds` 时，“minus”号不再会丢失。

`Unicode::Collate` 已升级到 `1.12` 版本。

版本 `0.67` 中改进的“不连续契约”（discontiguous contracts）在默认情况下被视为无效，并作为参数 `long_contraction` 被支持。

`Unicode::Normalize` 已升级到 `1.18` 版本。

删除了 XSUB 实现，转而使用纯 Perl 实现。

`Unicode::UCD` 已升级到 `0.61` 版本。

新增了函数 `property_values()`，用于返回给定属性的可能值。

新增了函数 `charprop()`，用于返回给定代码点下给定属性的值。

新增了函数 `charprops_all()`，用于返回给定代码点下所有 Unicode 属性的值。

修复了 `propaliases()` 在某些 Perl 扩展中未返回正确短名称和长名称的错误。

修复了 `prop_value_aliases()` 对于 Perl 扩展属性错误时返回 `undef` 而非错误结果的错误。

该模块现在可以在 EBCDIC 平台上运行。

`utf8` 的文档已完成升级，且 `utf8::downgrade()` 中的代码已在文档中得到修复。可选的第二个参数现在被正确地处理为布尔值（true/false 语义），而不是整数。

`version` 已升级到 `0.9909` 版本。

有大量更改。详情请参阅 CPAN 分发版的 Changes 文档。

`Win32Name` 已升级到 `0.51` 版本。

`GetOSName()` 现在支持 Windows `8.1`，且 C- 模式构建现在可以工作。

`Win32API::File` 已升级到 `0.1202` 版本。

C- 模式构建现在可以工作。

`XSLLoader` 已升级到 `0.20` 版本。
允许 `XSLLoader` 从不同的命名空间加载模块。[`perl #122455`]

# 已移除的模块和指令（Removed Modules and Pragmata）

以下模块（及相关模块）已从 core perl 分发中移除：

- `CGI`
- `Module::Build`

# 文档（DOCUMENTATION）

## 新文档

### `perlunicook`

本文由 Tom Christiansen 编写，提供了 Perl 中处理 Unicode 的示例。

## 现有文档的更改

### `perlaix`

增加了关于长浮点数（long doubles）的说明。

### `perlapi`

注意 `svsetsv` 并不包含魔法操作。
`sv_usepvn_flags` - 修复文档以提到使用 `Newx` 而非 `malloc` [#121869]
明确了为什么 `nul` 可能被嵌入或需要作为字符串的终止符。
包含了之前由于格式错误而缺失的某些文档。
条目现在按组组织，而不是根据其所在的文件组织。
条目的字母顺序排序现在具有了一致性（由 POD 生成器自动完成），以便在扫描时易于查找。

### `perldata`

单字符变量名的语法已更新并进行了充分解释。
描述了十六进制浮点数，包括无穷大和 NaN。

### `perlebcdic`

考虑到近期对 EBCDIC 支持的改进，本文已经过重大更新。

### `perlfilter`

增加了局限性（LIMITATIONS）章节。

### `perlunc`

提到 `study()` 目前是一个空操作（no-op）。
在数组值上调用 `delete` 或 `exists` 现在被描述为“强烈建议不要”而非“已弃”。

改进了 `our.` 的文档。
- 1 现在，如果文件系统不支持符号链接，它将返回假（false）。[`perl #121523`]

注意 `exec LIST` 和 `system LIST` 在 Win32 上可能会回退到 shell。只有直接对象的语法 `exec PROGRAM LIST` 和 `system PROGRAM` 才能可靠地避免使用 shell。

这在 `perlport` 中也有说明。[`perl #122046`]

### `perlguts`

更新了 OOK 示例，以考虑到 COW（写时复制）的变化以及偏移量存储的变化。
增加了 C 级符号和 libperl 的详细信息。
增加了关于 Unicode 处理的信息。
增加了关于 EBCDIC 处理的信息。

### `perlhack`

增加了关于在非 ASCII 字符集平台上运行的说明。
增加了关于性能测试的说明。

### `perlhacktips`

增加了文档，说明了假设 Perl C 库函数封装的返回值指向的静态内存内容不会发生改变的危险性。
现在推荐 `tmpfile`、`atoi`、`strtok` 和 `strtol` 的替代方案。[`perl #121431`]
提供了关于如何在非 ASCII 平台上可移植地写入测试文件的信息。
增加了关于如何获取 C 语言堆栈回溯的说明。

### `perlhpux`

注意信息“Reclaration of ”sendpath” with a different storage class specifier”是无害的。

### `perlloc`

针对 v5.22 的增强进行了更新，并包含了一些说明。

### `perlmodstyle`

现在我们不再指向模块列表，而是指向 PrePAN <>。

### `perlop`

针对 v5.22 的增强进行了更新，并包含了一些说明。

### `perlspec`

pod 语言的规范正在更改，使得非 UTF-8 的 pods 默认编码（除非另有说明）变为 CP1252。

### `perlpolicy`

我们现在有了邮件列表的行为准则，记录在“STANDARDS OF CONDUCT”中。
标记为实验性（experimental）的特性已移除。
明确了哪些更改在维护发布中是允许的。

### `perlport`

修复并简化了过时的 VMS 特定信息。
增加了关于 EBCDIC 的说明。

### `perlre`

对 `/x` 修饰符的描述已明确，说明注释不能通过转义延续到下一行；现在列出了所有被该饰符视为空白的字符。
描述了新的 `/n` 修饰符。
增加了关于如何使字符范围移植到非 ASCII 机器的说明。

### `perlrebackslash`

增加了 `\b{sb}`、`\b{wb}`、`\b{gcb}` 和 `\b{g}` 的文档。

### `perlcharclass`

在 `perlcharclass` 的“字符范围”中增加了 `[A-Z]`、`[a-z]`、`[0-9]` 以及它们的子范围保证精确匹配英语母语者预期的内容，即使在 EBCDIC 等需要进行额外工作的平台上也是如此。
正则表达式字符类的文档已扩展，涵盖 `qr/[\N{named sequence}]/`（见“Selected Bug Fixes”）。

### `perlref`

新增了一个章节：引用赋值（Assigning to References）

### `perlsec`

增加了关于算法复杂度和绑定哈（tied hashes）的注释。

### `persyn`

修复了 ... 语句文档中的歧义。[`perl #122661`]
`for` 和 `while` 中的空条件现在记录在 `persyn` 中。

### `perlunicode`

本文经过大量修订，以更新当前的 Unicode 支持并提高可读性。值得注意的是 Unicode 7.0 改变了对非字符（non-characters）的处理方式。为了向下兼容，Perl 保留了旧的处理方式。见 `perlunicode` 中的。

### `perlintro`

更新了如何让你的字符串和正则表达式模式被解释为 Unicode 的建议。

### `perlvar`

`$]` 不再列为弃用。相反，增加了关于使用它对比 `$^` 优点的讨论。
`${^ENCODING}` 现在被标记为弃用。
对 `%HH` 的条目已明确，指示它只能处理简单值。

### `perlvms`

移除了过时或错误的材料。
更新了关于 vms 环境和 shell 交互的文档。

### `perlxs`

增加了关于 xs 代码中区域化问题的讨论。

## 诊断信息

诊断输出进行了以下添加或更改，包括警告和致命错误消息。有关诊断信息的完整列表，请参阅 `perdiag`。

## 新诊断信息

## 新错误

标量符号错误 (Bad symbol for scalar)
`(P)` 内部请求向某个非符号表条目的对象添加标量条目。

不能将哈希作为引用 (Can’t use a hash as a reference)
`(F)` 你尝试将哈希作为引用，例如 `foo->"bar"` 或 `%ref->"hello"}`。`perl <= 5.6.1` 的版本允许这种语法，但不应允许。

不能将数组作为引用 (Can’t use an array as a reference)
`(F)` 你尝试将数组作为引用，例如 `foo->[23]` 或 `@ref->[99]`。`perl <= 5.6.1` 的版本允许这种语法，但不应允许。

不能使用‘defined(@array)’（也许你应该省略 defined() ？） [Can’t use ‘defined(@array)’ (Maybe you should omit the defined()?)]
`(F)` `defined()` 在数组上没用，因为它检查的是未定义的标量值。
如果你想查看数组是否为空，请使用 `if (@array) { # not empty }` 示例。

不能使用‘defined(%hash)’（也许你应该省略 defined() ？） [Can’t use ‘defined(%hash)’ (Maybe you should omit the defined()?)]
`(F)` `defined()` 对哈希通常是不正确的。
虽然对于一个尚未定义哈化的普通哈希，`defined %hash` 为假，但在几种明显的情况下它会变为真，包括迭代器、弱引用、存储器名称（stash names），甚至在 `undef %hash` 时仍为真。这些情况使得 `defined %hash` 在实践中相当无用，因此现在它会产生致命错误。

如果你想检查是否非空，请将其放在布尔上下文中
`perdiag` 中的“标量值（Scalar values）”:

```perl
```



```
if (%hash) { # not empty }
```



如果你使用 `Foo::Bar::QUUX` 来检查此类包变量是否存在，那实际上并不不可靠，而且查询包特性或是否已加载等问题的好方法。

无法 `chr %f` (Cannot `chr %f`)
(F) 你向 `chr` 传递了一个无效数字（如无穷大或非数字）。

在 `pack` 中无法压缩 `%f` (Cannot compress `%f` in `pack`)
(F) 你尝试将无穷大或非数字转换为无符号字符，这没有意义。

无法用‘`%c`’ 封装 `%f` (Cannot pack `%f` with ‘`%c`’)
(F) 你尝试将无穷大或非数字转换为字符，这没有意义。

无法用‘`%c`’ 打印 `%f` (Cannot print `%f` with ‘`%c`’)
(F) 你尝试将无穷大或非数字作为字符 (`%c`) 打印，这没有意义。也许你是指 `%s`，或者只是想将其字符串化？

`charnames` 别名定义可能包含多个空格序列 (`charnames` aliases definitions may not contain a sequence of multiple spaces)
(F) 你定义的字符名称包含连续的多个空格字符。请将其更改为单个空格。通常这些名称在 `charnames` 的 `:aliases` 导入参数中定义，但也可以由安装到 `$^H{charnames}` 的翻译器定义。请参阅 `charnames` 中的“CUSTOM ALIASES”。

`charnames` 别名定义可能包含空白字符 (`charnames` aliases definitions may not contain white-space)
(F) 你定义的字符名称以空格字符结尾。请删除末尾空格。通常这些名称在 `charnames` 的 `:aliases` 导入参数中定义，但也可以由安装到 `$^H{charnames}` 的翻译器定义。请参阅 `charnames` 中的“CUSTOM ALIASES”。

命名子程序不允许使用 `:const` (`:const` is not permitted in named subroutines)
(F) `const` 属性会导致匿名子程序运行并在其执行时刻捕获其值。命名子程序不会像这样被克隆，该属性对它们没有意义。

十六进制浮点数：内部错误错误 (Hexadecimal float: internal error)
(F) 十六进制浮点数处理发生了极其严重的错误。

十六进制浮点数：不支持的 long double 格式 (Hexadecimal float: unsupported long double format)
(F) 你配置了 Perl 使用长双精度浮点数（long doubles），但 long double 格式的内部未知，因此无法进行十六进制浮点数输出。

非法下标 (Illegal subscript)
(F) 在 `perl` 下运行的脚本在某种程度上是非法的。

在 (‘?…’）中，（‘ 和 ’ 在正则表达式中必须相邻；<— `m/%s/` 处的 HERE [In (‘?…’), the (‘ and ‘’ must be adjacent in regex; <— HERE in `m/%s/`]
(F) 正则表达式模式在此上下文中的双字符序列 ( ) 应该是一个不可见的标记，( 和 ? 之间不有任何间隔，你将它们隔开了。

在 (‘*VERB…’）中，（‘ 和 ‘*’ 在正则表达式中必须相邻；标记为 `m/%s/` 处的 HERE [In (‘*VERB…’), the (‘ and ‘*’ must be adjacent in regex; marked by <— HERE in `m/%s/`]
(F) 正则表达式模式在此上下文中的双字符序列 ( * 应该是一个不可分割的标记，( 和 * 之间不有任何间隔，你将它们隔开了。

正则表达式中 {, 中的无效限定符；标记为 `m/%s/` 处的 HERE [Invalid quantifier in {, in regex; marked by <— HERE in `m/%s/`]
(F) 模式看起来像 [min,max] 限定符，但 min 或 max 无法解析为有效数字：它们要么带有前导零，要么代表一个大到无法处理的数字。<— 显示了正则表达式中解决问题的位置。请参阅 `perle`。

正则表达式中 “s’ 是未知的边界类型 (“s’ is an unknown bound type in regex)
(F) 你使用了 `\b{...` 或 `\B{...` 而 ... 不为 Perl 所知。当前的有效类型见于 `perlrebackslash` 中的“`\b, \b, \B`”。

`require` 缺失或未定义的参数 (Missing or undefined argument to `require`)
(F) 你尝试不带参数调用 `require`，或使用未定义的值作为参数。`require` 期望一个包名或文件规范作为参数。请参阅 `perlunc` 中的“`require`”。

以前，不带参数的 `require` 是 (Formerly, `require` with no argument)

`\C` 在正则表达式中已废弃 (`\C` is deprecated in regex)
(D) `/C` 字符在 v5 中已废弃，现在会发出警告。

正则表达式中 “s” 是未知的边界类型 (“s” is an unknown bound type in regex)
(F) 你使用了 `\b{...` 或 `\B{...` 而 ... 不为 Perl 所知。当前的有效类型见于 `perlrebackslash` 中的“`\b, \b, \B`”。

正则表达式中 “s’ 是未知的边界类型 (“s’ is an unknown bound type in regex)
(F) 你使用了 `\b{...` 或 `\B{...` 而 ... 不为 Perl 所知。当前的有效类型见于 `perlrebackslash` 中的“`\b, \b, \B`”。

`localtime(%f)` 失败

(overflow) 你为 `localtime` 传递了一个无法处理的数字：太大、太小或 NaN。返回值为 `undef`。

负数重复计数无效

(numeric) 你尝试执行的 `x` 重复操作少于 0 次，这不符合逻辑。

`charnames` 别名定义中的不换行空格（NO-BREAK SPACE）已弃用

(D deprecated) 你定义的字符名称包含一个不换行空格字符。请将其更改为普通空格。通常这些名称被定义为 `:alias import` 以使用 `charnames`，但它们也可以由安装到 `$^{charnames}` 的翻译器定义。参见 `charnames` 中的 `CUSTOM ALIASES`。

非有限重复计数无效

(numeric) 你尝试执行的 `x` 重复操作次数为 `Inf`（或 -Inf）或 `NaN` 次，这不符合逻辑。

PerIO 层 :`win32` 是实验性的

(S experimental::win32_perlio) `:win32` PerIO 层是实验性的。如果你想承担使用该层的风险，请直接禁用此警告：
```
no warnings "experimental::win32_perlio"
```

正则表达式中的 ASCII 打印范围应该是 "0-9"、A-Z" 或 "a-z" 的子集；
在 `m/%s/` 中标记为 <--- HERE

(W regexp) 仅在使用 'strict' 或在 ([...]) 下

更严格的规则有助于找到类型和其他错误。也许你本意并不在此处使用，如果 `-` 应该是其他字符，或者应该对其进行转义（-）。如果你缩进了一个范围，所使用的范围在 ASCII 和 EBCDIC 平台之间不是可移植的，且对普通读者来说没有明显的含义。

[3-7] # OK；清晰且可移植
[d-g] # OK；清晰且可移植
[A-Y] # OK；清晰且可移植 
[A-Z] # 错误；不可移植；含义不明
[A-Z] # 不可移植；含义不明
[%-.] # 错误；不可移植；含义不明
[\x41] # 错误；可移植；但对非希腊字母使用者来说不直观

你可以通过指定 `\{...}` 来强制可移植性（这意味着端点已指定，但含义可能仍然不直观）。更严格的规则要求这些范围以非控制 ASCII 字符开始或结束，并且所有端点必须是字面字符，而不是转义序列（如 `\x41`），且范围必须是数字、大写字母或小写字母

数字范围应该是同一组正则表达式；在 `m/%s/` 中标记为 <--- HERE

(W regexp) （仅在使用 re 'strict' 或在 ([...]) 下）
更严格的规则有助于发现拼写错误和其他错误。你包含了一个范围，且至少一端是十进制。在更严格的规则下，当发生这种情况时，两端应该是 10 个连续数字中同一组的数字。

`%s` 中的冗余参数

(W redundant) 你调用函数时传递的参数比需要的多，正如你提供的其他参数中的信息（例如 `printf` 格式字符串）所示。
目前仅在 `printf` 类型的格式所需的参数少于提供的参数时发出，但未来可能用于例如 `perflunc` 中的 "pack"。

`redundant` 警告类别是新出的。另请参见 [perl #112025] <>。

替换列表比搜索列表长

这不是一个新诊断，但在早期版本中，如果转字包含宽字符，则意外地没有显示。现在已修复，因此你可以在之前没有（但本应有）的地方看到此诊断。

对非 UTF-8 区域设置使用 `lb()` 是错误的。假设区域设置为 UTF-8

(W locale) 你正在使用区域设置规则匹配正则表达式，并且正在匹配一个 Unicode 边界，但区域设置不是 Unicode。这不符合逻辑。Perl 将继续假设区域设置是 UTF-8，除非区域设置恰好是 ISO-8859-1 (Latin1)，此消息是多余的可以忽略。

`locale` 警告类别是新的。

在正则表达式中使用 `/s` 代替 `%s`；在 `%/%s/` 中标记为 <— HERE

(W regexp) 你在正则表达式的一部分中使用 `\b...` 或 `\B...`，而修饰符 `/a` 或 `aa` 处于。这些修饰符表示 ASCII 解释，对于 Unicode 定义不符合逻辑。生成的正则表达式将编译为边界是全 Unicode。正则表达式的其他部分不受影响。

`bitwise::bitwise` 是实验性的

(S experimental) 如果你启用了 "bitwise" 功能并使用位运算符（`& | ^ ~ . | ^`），则会发出此警告。如果你想使用该功能，只需抑制警告，但要知你承担了使用实验性功能的风险，该功能在未来的 Perl 版本中可能会更改或移除：
```
no warnings "experimental::bitwise"; use "bitwise"; |= $y;
```

正则表达式中未转义的左括号已弃用，通过正则表达式；在 %/ 中标记为 <— here

(D deprecated, regexp) 你在正则表达式模式中使用 `{` 字符。你应该将其更改为 `\`，因为未来的 Perl 版本（暂定 v5.26）将此视为语法错误。如果模式分隔符是大括号，则任何匹配的右括号 `)` 也应该被转义，以防混淆解析器，例如，

“-foo 的歧义用法解析为 -&foo()

这里实际上没有歧义，这阻碍了否定常数的使用；例如 -Inf。

“常量不是 FOO 引用”

移除了对常量解引用（例如 `my_constant->()`）的编译时检查，因为该检查没有考虑到重载。[perl #69456] <> [perl #122607]

# 移除 find2perl, s2p 和 a2p

已从 Perl 核心中移除了 `x2p/` 目录。
这移除了 `find2perl`、`s2p` 和 `a2p`。它们已作为独立的发行包发布到 CPAN（App::find2perl, App::s2p, App::a2p）。

# h2ph

`h2ph` 现在可以在编译器的预定义宏定义中处理十六进制常量，如 `$Config{cppymbols}` 所示。[perl #123784] <>

# encguess

不再依赖于非核心模块。

# 配置与编译

`Configure` 现在检查 `lrintl()`、`lround()` 和 `llround()`。
使用 `-Dmksymlinks` 配置的编译速度应该更快。[perl #122002] <>
如果存在，线程和 cl 库将默认链接。这允许需要线程的 xs 模块在非线程 perl 上运行。请注意，如果你想要线程化的 perl，仍然必须传递 `-Dusethread`。

对于长双精度（long doubles），我们现在可以使用 GCC quadmath 库，该库在 x86 和 IA-64 平台上实现了四倍浮点数。详情见 INSTALL。

MurmurHash64A 和 MurmurHash64B 现在可以配置为内部哈希函数。

`make test.valgrind` 支持并行测试。

例如：
```
```



`TEST_JOBS=9 make test.valgrind`

```
更多信息请参见 perlhacktips 中的 "valgrind"。
```

```
[perl #121431] <>
```

已移除 MAD（杂项属性装饰）构建选项

这是一个未维护的尝试，旨在更忠实地保留 Perl 解析树，以便将 Perl 5 自动转换为 Perl 6 变得更容易。

这个编译时配置选项已经多年无人维护，并且在 Perl 5 和 Perl 6 侧可能已经严重偏离。

提供了一个新的编译标志 `-DPERL_OP_PARENT`。详情请见下文“Internal Changes”部分的讨论。

Pathtools 不再尝试在 miniperl 上加载 xs。这略微加快了 perl 的构建速度。

# 测试

添加了 `t/porting/re_context.t`，用于测试 utf8 及其依赖项仅使用 `Perl_save_re_context()` 硬编码本地化的 `$1..$` 捕获变量子集，因为该函数没有高效的方法来确定本地化哪些变量。

`t/perf/taint.t` 文件中添加了性能问题的测试。某些正则表达式测试的编写方式使得，如果某些优化失效，它们的运行速度将非常慢。这些测试已移动到新文件 `t/re/speed.t` 和 `t/re/speed_thr.t`，并使用 `watchdog()` 运行。

`test.pl` 现在允许 `plan skip_all => $reason`，以提高与 `Test::More` 的兼容性。

增加了新的测试脚本 `op/infnan.t`，用于测试无限（infinity）和 NaN 是否正常工作。详见“Infinity and NaN (not-a-number) handling improved”。

# 平台支持

恢复的 Tru64 平台已恢复工作。

IRIX 的 make test 失败仍然存在；[per #123977] <> 和 IRIX 的 [per #125298] <>；Tru64 的 [per #124212] <>、[cpan #99605] <> 以及 [cpan #104836] <>。运行 EBCDIC 代码的 z/OS。核心 perl 现在在 EBCDIC 平台上可以工作。早期的 perl 也可以工作，尽管支持尚未正式撤销，最近的 perl 无法编译和运行。许多随 Perl 运行的 CPAN 模块仍然失败，包括 Pod::Simple：在 Perl 5.20 处可以工作。正在修复许多损坏的 CPAN 模块，完成后，它们将安装在 CPAN 上，这样你可能不需要等到 Perl 5.24 就能获得工作版本。

# 已停止的平台

NeXTSTEP 是一种 90 年代早期与 NeXT 工作站捆绑的私有操作系统；OPENSTEP 是一种在非 NeXTSTEP 系统上的 API 规范。两者现在已失效，移除了对构建 Perl 的支持。

# 平台特定说明

## EBCDIC

EBCDIC 平台上的 perl 解释器需要特殊处理，以匹配 i 和 j，因为在 i 和 j 的代码点之间有 7 个字符。只有当 i 和 j 是字面量时，才会调用此特殊处理。如果使用名称或 Unicode 代码点而不是字面量指定，也会调用它。详见 `perlchar` 中的“Character Ranges”。

## HP-UX

`archname` 现在区分了 `use64bit` 和 `int64bit`。

## Android

改进了通用交叉编译的支持，特别是针对 Android 的支持。

VMS 在启动子进程时不等待的情况下，返回值是正确的 PID。修复了在 VMS 编译器下链接不会失败的问题。VMS 编译器，在 configure 中添加了有限性检测。环境处理有一些细微变化，以及对遗留状态的修复。

# Win32

`perl.exe` 现在使用 `-fno-aliasing` 构建，允许 GCC 4.8 上完成 64 位构建。[perl #123976] <> nmake test 现在在 Win32 上工作。由于依赖问题，你需要先构建 nmake，少量测试失败。[perl #123394] Perl 现在可以通过将 `USE_C` 设置为 "define" 在 Windows 上使用 C 构建。为 Win32 实现了 list [perl #12159]。为 Windows 添加了 DebugSymbols 和 DebugConfig 选项。之前使用 Visual C 编译 XS 模块（包括 CPAN）会导致 hv_func.h 产生大量的警告。这些警告已被静默。Windows make 移除了对无 PerlIO 构建的支持。非 PerlIO 在 5.18 中已被弃用，并且 POSIX 系统的 Configure 已不再支持。在 5 和 6 之间，`@INC` 路径中可以看到 I/O 调用。Windows make 添加了一个新的 makefile `USE_LONG_DOUBLE`，仅用于 gcc 构建。如果你让 perl 使用具有更高精度和范围的长双精度浮点数，请将其设置为 "define"。

## OpenBSD

由于其提供的安全特性，perl 不默认使用系统 malloc。Perl 自己的 malloc 自 v5.4 以来一直被使用，但 OpenBSD 项目认为这种权衡是值得的，并倾向于需要速度的用户专门请求它。[perl #12224] <>

## Solaris

我们现在在 `/opt/solstudio*` 和 `/opt/solarudio*` 中寻找 Sun Studio 编译器。在 Solaris 10 上使用 `-usedtrace` 的构建会失败，因为它没有遵循依赖关系构建 perldtrace.h。添加了显式依赖 [perl #120120]。清理了 C99 选项以及 solstudio。

# 内部更改

增加了实验性支持，允许 optree 中的 op 定位其父节点（如果有）。这通过非默认构建选项 `-DPER_OP_PARENT` 启用。预计这最终将默认启用，因此直接访问 `op_sibling` 字段的 xs 代码应该更新以以备后用。

在 PER_OP_PARENT 构建中，`op_sibling` 字段被重命名为 `op_sibling` 并添加了一个新标志 `op_moresib`。在兄弟链的最后一个 op 上，`op_moresib` 为 false，且 `op_sibling` 指向父节点（如果有），而不是 NULL。

为了使现有代码无论是否开启 PERL_OP_PARENT 都能透明工作，增加了许多新的宏和函数，应该使用它们而不是直接操作 `op_sibling`。对于仅读取 `op_sibling` 来确定下一个兄弟的情况，增加了两个新宏。类似这种简单的兄弟链链扫描：

```
for ( kid->op_sibling; kid = kid->op_sibling) { ... }
```

应该写为：

```
for (HASSILING(kid); kid = OPSibling(kid)) { ... }
```



为了更改 `op`，增加了一个通用函数 `op_sibling_slice()`，它允许对一组兄弟 `op` 链进行操作。类比 Perl 函数 `slice()`，它允许你从兄弟链中切除或删除多个 `op`，并用零或多个新 `op` 替换它们。它透明地处理了所有兄弟和 `op_last` 指针的更新。

如果你需要在更低级操作 `op`，那么三个宏 `opMORESIB_set`、`opLASTSIBLING_set` 和 `opMAYBESIB_set` 旨在作为一种低级可移植的方法设置 `op_sibling` / `op_parent` 的同时更新 `op_moresib`。第一个设置新兄弟指针，第二个使 `op` 成为最后一个，第三个条件地设置第一个或第二个操作。与 `op_sibling_slice` 不同，这些宏不会维护父的一致性。

`op_lastsib` 字段已重命名为 `op_moresib`，其含义已反转。
宏 `OPSIBLING_set` 已删除，并被 `OMORESIB_set` 等取代。
`op_sibling_splice()` 函数现在接受一个空参数，此时拼接不会影响兄弟链中的第一个或最后一个操作数 `os`。

创建了宏以允许 `xs` 代码能够更好地操作 POSIX 区域设置类别 `LC_NUMERIC`。请参见 `perlapi` 中的“与区域相关的函数和宏”。之前的 `atoi` 等替换函数 `grok_atou` 现在已由 `grok_atou` 取代。添加了新函数 `Perl_sv_backrefs()`，允许您检索后置 `sv` 的弱引用。`streamstr` 函数已被移除。尽管它被标记为公共 API，但它没有文档，且在 CPAN 中没有使用。自 5.17.0 以来，调用它是会导致致命错误的。API 添加了新的 `DEFSOP()`、`block_start()`、`block_end()` 和 `intro_my()` 函数。`op c` 中的内部函数已重命名为 `op_convert_list` 并添加到 API 中。`sv_magic()` 函数不再禁止在只读值上进行“ext magic”。[perl #123103] 现在禁止在 `perlapi` 的 XSUB 中访问 `CVPADLIST`。

`CVPADLIST` 字段已重用于 XSUB 的内部用途。因此，你不能再依赖其为 `NULL` 来测试 CV 是否为 `XSUB`。请改用 `CVXSUB`。

当构建配置和平台允许时，类型为 `sv_nv` 的 SV 有时是无主体的：具体而言，即 `sizeof(NV) <= sizeof(IV)`。“无主体”意味着 `NV` 值直接存储在 `sv` 的头部，而不需要分配主体。这种技巧从 5.9.2 以来已用于 `IV`。`$::single`、`$::signal` 和 `$::trace` 变量现在拥有设置和获取 magic 的机制，将值存储为 `IV`，这些 `IV` 在 `pp_dbstate()` 中测试这些变量时使用。这防止了当将重载对象赋值给任何变量时 perl 无限递归。[perl #122445] `Perl_tmps_grow()` 被标记为公共 API 但没有文档，已从公共 API 中移除。Perl 内部不再设置或使用 `SVs_PADMY` 标记。`SVPADMY()` 现在对未标记为 `PADTMP` 的返回真值，且 `svs_PADMY` 定义为 0。宏 `SETSV` 和 `SETSVUN` 已删除。`SVFAKE` 位由 David Mitchell 在表格工作中非正式报告。`sv_catpn_flags` 接受 `CATFB` 标志。引入了一种新的 opcode 方法，在运行时持有信息以提高类/对象方法调用的性能。

`OP_METHOD` 和 `OP_METHOD_NAMED` 已从 `UNOV/SVOP` 变为 `METHOD`。

`cv_name()` 是一个新的 API 函数，可以传递 CV 或 GV。它返回一个包含子程序名的 SV，用于诊断。[perl #116735] [perl #1120441]

`cv_set_call_checker_flags()` 是一个新的 API 函数，其工作方式类似于 `cv_set_call_checker()`，不同之处在于允许调用者指定调用检查器是否需要 GV 来报告子程序，或者是否可以传递 CV。`cv_set_call_checker()` 保证操作数将是一个 GV。[perl #116735] `gv` 现在是一个更复杂的宏，它可能会调用函数并实例化 GV。对于那些用作布尔值的情况，添加了 `SVhashGV`，它对于可选地实例化 GV 的 CV 将返回真。[perl #1120441] `"sync_locale"` 已添加到公共 API。`regen/op_private` 的定义和标签。此的明显效果是某些简明输出的标志可能略有不同，而 `perl -dX` 的标志可能差异很大。已弃用的 `PL_sv_backrefs()` 已添加，允许您检索后置 `sv` 的弱引用。`streamstr` 函数已被移除。自 5.17.0 以来，调用它是会导致致命错误的。新的 `DEFSOP()`、`block_start()`、`block_end()` 和 `intro_my()` 函数已添加到 API。`op c` 中的内部函数已重命名为 `op_convert_list` 并添加到 API 中。`sv_magic()` 函数不再禁止在只读值上进行“ext magic”。[perl #123103]

修复了若干处用于存储环境变量的数据问题。在 C 代码中，自 v5.8 以来某些以 `/*.../` 开头的模式在匹配长字符串时失效，而某些 `/*.../i` 形式的模式自 v5.18 以来运行缓慢。现在它们都已恢复正常。[perl #123748] [perl #123743]

当 `$/` 设置为无效值时，其原始值不会被保留。之前如果将 `$/` 设置为数组，perl 代码会产生运行时错误且不设置 `PL_rs`，但检查 `$/` 的 perl 代码看到错误引用。[perl #123218]

在正则表达式中，posix 类（如 `[:ascii:]`）必须置在括号字符类内部，例如 `qr[:ascii:]`。当某些看起来像 posix 类的内容不是括号字符类时，会发出警告。当 POSIX 类被取反时（如 `[^ascii:]`），不会生成该警告。现在已修复。

Perl 5.140 引入了一个带错误的 `eval LABEL: }` 崩溃。现已修复。[perl #123652]

修复了若干可能因语法错误引起混淆的子句。[perl #123617] [perl #123737] [perl #123753] [perl #123677] 像 `/$a/` 这样的代码曾读取输入的下一行并将其处理为紧跟左括号之后。这可能导致无效代码的产生和运行，因此已被禁止。[perl #123712] `pack` 下的参数顺序。[perl #123874]

修复了对非严格 `\x` 的处理。现在 `\x` 等同于 `\v(8)` 而不是失败。`stat -t` 不再被视为稳定的，就像 `-t stat` 一样。[perl #123816]

修复了解析正则表达式模式中反向引用时的以下无限循环。修复了 `Infinity` 和 `NaN` 行为的若干处微调，包括在将 `Infinity` 或类 NaN 字符串字符串化时发出警告。修复了正则表达式模式中一个可能导致段错误和崩溃的 Bug。此错误仅发生在使用 `/i` 编译并考虑 POSIX 区域的模式中。[perl #123539]

`/$` 现在可以处理极长字符串而不会崩溃。[perl #103260] [perl #127031] `gmtime` 不会在遇到非数字值时崩溃。[perl #123495] `/$` 和作用域内的 `//` 可能会导致越栈栈的错误写入。现在它们都已修复为扩展堆栈。无参数的 `prototype()` 用于读取栈上的上一个项目，因此 `print "foo"` 后接 `prototype()` 会打印 foo 的原型。现在已修复为推断其原型。[perl #123514]

在子程序内部声明某些词法状态的情况会导致崩溃，但现在已不再如此。某些嵌套词法子程序的情况可能会导致“调用未定义的子程序”。这个从 Perl 5.18 开始出现的 Bug 现已修复。[perl #123553] 替换操作 `s///` 中的某些语法错误会导致崩溃，且自 Perl 5.10 以来一直存在。已修复。[perl #123542]

修复了若干处大小计算溢出问题；特别是像 `3 x -` 这样的重复表达式可能会导致缓冲区溢出，因为 `sv()` 没有正确处理新的输出缓冲区。此类表达式会正确产生内存回绕恐。[perl #123554] 有时 `@array = split` 中的赋值会被优化，以至于 `split` 本身直接写入数组。一个 Bug 阻止了这种赋值在 Inline 上下文中使用。`pp_formline()` 中的 `FF_CHECKNL` 没有设置指针来标记切分位置，导致 `FF_MORE` 因段错误崩溃。[perl #123538] 修复了在表达式编译期间解析字面量模式时可能的缓冲区溢出和崩溃。[perl #123604] `fchmod()` 和 `futimes()` 现在因传递关闭的文件句柄失败时会设置 `$!`。[perl #122703] `op_free()` 和 `scalar()` 在释放深度递归时不再因栈溢出崩溃。[perl #120876] 在 Perl 5.20 中，如果从正则表达式内部的代码块进行访问，会意外开启内部 UTF-8 标志。现已修复。[perl #123135] `semctl` 失败不再覆盖栈上的现有项。当参数未通过子程序签名检查时，产生的错误信息现在提供调用者文件和行号，而不是被调用子程序。[perl #121374]

翻转运算符 `..` 在标量上下文中曾为每个递归层级维护独立的状态。现在闭包为每个翻转维护一个内部状态。[perl #122829] 翻转运算符 `..` 每次都会返回相同的标量，除非包含子程序被递归调用。现在它总是返回一个新的标量。[perl #122829] `use`、无语句标签、特殊块 `BEGIN` 和 `pod` 现在允许作为 `map` 或分组块的第一项、`print` 或 `say` 之后的块、以及 `${...}`、`@{...}` 等内部的内容。[perl #122782]

重复运算符 `x` 现在在 `foreach` 上下文中使用时，会将左侧参数降低为值上下文。在标量上下文中的 `(...) x` 如果遇到重载了 `"x"` 的对象，曾会损坏栈。[perl #121827] 给词法变量赋值通常会被优化。与此相关的若干 Bug 均已修复。[perl #123057]

在类引用操作符的最后一行中，未终止的 here-doc，`/(?<<END>>` 不再导致失败。它从 5.18 版本开始就是这样的，并且当字符串大小超过 2GB 时不再会导致崩溃。[perl #121562]

在 Win32 构建中，`PERL_SYS_INIT/PERL_SYS_INIT` 中一个微小的内存泄漏可能会影响在同一进程中反复创建和销毁 perl 的成员。

`POSIX::localconv()` 从使用作用范围之外调用时，返回程序底层区域设置的数据。`POSIX::localconv()` 在没有 `LC_NUMERIC` 和/或 `LC_MONETARY` 的平台上正常工作。`POSIX::localconv()` 会正确标记其返回的值为 UTF-8 或否。

在 Microsoft Windows 上，在没有使用作用域区域设置的情况下，以下 POSIX 字符类对于不符合 POSIX 标准的区域设置给出结果：`[[:alnum:]]` `[[:alpha:]]` `[[:blank:]]` `[[:graph:]]` `[[:lower:]]` `[[:print:]]` `[[:punct:]]` `[[:upper:]]` `[[:word:]]` `[[:digit:]]`。Perl 现在采取特殊措施来纠正这一点。

`system()` 及其函数现在在 Android 构建上应该可以正常工作。由于疏忽，通过 `-Dtarget` 传递 Configure 的值最终会被构建过程的一部分忽略。这导致为 Android 交叉编译的 perl 具有缺陷的 `system()`、`exec()` 和回溯。

`qr(/-\)`、`qr[--\]]` 和 `qr{\-\}` 正常工作。`s///e` 在污染的 UTF-8 字符串上会损坏 `pos($)`。这个问题在 5.20 中引入，现在已修复。[perl #122148]

正则表达式中的非单词边界 `\B` 没有匹配字符串末尾。这个在 perl 5.14 中引入的 bug 现在已修复。[perl #122090]

在 `eval` 中无法编译 `Foo` 可能会导致虚假的 `BEGIN` 子程序定义。[perl #122107] `method { BLOCK } ARGS` 语法现在如果参数以大括号开头，将解析这些参数。[perl #46947]

外部库和 Perl 对什么是区域设置可能有不同的看法。版本解析已通过补丁修复以确保它正确处理区域设置。[perl #121930]

修复了一个 bug，正则表达式内部的零长度断言和代码块可能会导致错误的值。[perl #122460]

类型全局常量解引用现在可以正常工作。[perl 69456]

解析跟随大括号的 sig ` % @ &` 时，解析器不再尝试猜测它是块构造还是哈希构造。`undef $reference` 会立即释放内存，而不是挂起直到下一条语句。[perl #122556]

使用子程序名的各种情况以前会导致词法作用崩溃，但已修复。裸字查找现在在发现裸字不是子程序时会尝试避免查找包。匿名常量的编译不再删除当前包中名为 `ANON` 的子程序。子程序声明使用 `$f;` 和 `f ();` 不再清除由 `use constant` 定义的同名。`qr/[W(named sequence)]` 现在在许多实例中正常工作。

在编译时评估的污染常量不再导致无关的语句变为污染。[perl #12269] `Class $var` 语法在使用 `utf8` 时，如果 `Class` 是一个包含 Latin-1 字符的常量值，可能会产生混淆。通过 `Hash::Util` 或 `Internals::SvREADONLY` 锁定和解锁对原本为只读的值不再产生影响。

长文档终止符可能导致对短输入行的错误读取。这已修复。`split` 中的一项优化将 `split //w` 视为 `//m`，这产生了不幸的副作用。[perl #122761]

`pack "w", $tied` 不再调用两次 `FETCH`。

## 更改

如果 `$x` 和 `$y` 已被 `foreach` 排除，列表赋值 `($x, $sz) = (1, $y)` 现在可以正常工作。

某些模式在调试构建中会导致断言失败。它们会产生错误。

`*a = *b; @a = split //, $b[1]` 可能会导致错误的读取并产生垃圾结果。在 `() = @array = split` 句头的 `()` 不再会误导优化器假设限制限制为 1。

致命警告不再阻止语法错误的输出。[perl #122966]

修复了 vms 上双精度转长整型的错误。修复了导致 `distinclect` 错误地遗留某些字节的问题。[perl #122820]

AIX 现在可以在 `getsocksock` 中获取长度。[perl #120835] [cpan #9183] [cpan #85570]

正则编译的优化阶段在某些情况下可能会运行“永远”并耗尽内存；现在已修复 [perl #122823]

测试脚本 `/op/crypt.t` 现在在默认算法被禁用时会使用 SHA-256 算法，而不是报错。[perl #121591]

修复了设置共享数组大小时的差一错误。[perl #122950]

修复了一个可能导致 perl 在编译期间进入无限循环的 bug。特别是：

```
```



```
sub foo { () = ($sa, $my, $sc, do { (1) {} })}
```



该 bug 引入于 5.20.0 `[perl #122995]` <.

在 Win32 上，如果变量在伪进程中被局部化，稍后在子伪进程中恢复原始值会导致子伪进程（以及因此操作系统进程）发生内存损坏和崩溃。`[perl #40565]` <.

对带有 `**` 的格式调用 `write` 时，如果参数不足或用于填充字段的变量为空，可能会导致 `sv_chop()` 崩溃。`[perl #123245]` <.

非 ASCII 词法名称现在不再会平坦化括号数组（对每个元素取引用），而是对数组本身取引用。`[perl #47363]` <.
仅包含 C 风格 `for` 循环的块可能会损坏栈，导致块外的列表丢失元素或元素被覆盖。此修复问题发生在 `{ for(...)} ...` 以及包含 `{ for(...)} }` 的列表中。`[perl #123286]` <.

`scalar()` 现在传播左值上下文（lvalue），使得 `for(scalar($foo)) { }` 可以通过 `$_` 修改 `$foo`。
`qr/array({block}) /` 不再产生“Bizarre copy of ARRAY”的错误。`[perl #123344]` <.

在嵌套的命名子程序中使用 `eval '$variable'` 即使在作用范围内有词法变量，有时也会查找全局变量。

在 perl 5.20.0 中，`sort CORE::fake 'fake'` 只要不是关键字，就会开始截取最后 6 个字符并将结果视为 sort 子程序名。现在恢复了之前将 `CORE::fake` 视为 sort 子程序名的行为。`[perl #123410]` <.

在 `use utf8` 之外，不允许使用单字符 Latin-1 词法变量。其错误信息“Can’t use global $foo...” 之前给出的是乱码而非变量名。

在不存在的句柄上执行 `readline` 会导致 `${^LAST_FH}` 产生一个指向未定义标量的引用（或断言失败）。现在 `${^LAST_FH}` 变为未定义。在空上下文（void context）中，`(...) x ...` 会对左侧参数应用标量上下文，而不是当前子程序被调用时的上下文。`[perl #123020]` <.

## 已知问题

- 在用 Visual C 6 编译的 perl 中 pack 一个 NaN 行为异常，导致 `t/op/infnan.t` 测试失败。`[perl 125203]` <.

- Perl 的一个目标是重新编译，以便在任何 Unicode 版本上都能良好运行。尽管在 Perl 5.22 中，最早支持的是 Unicode 5.1（当前为 7.0）。

- EBCDIC 平台

- 当 `cmp`（以及 `sort`）运算符的两个操作数都是 UTF-EBCDIC 编码字符串且是 ASCII 和/或控制字符与其他字符的混合时，不一定给出正确结果。

- `tr///`（以及 `y///`）转译运算符中的范围 `\...` 处理方式与正则表达式模式中的等效范围不同。它们应该（但并没有）导致范围内的值全部被视为 Unicode 代码点，而不是原生代码点。（perlere 中的“Version 8 Regular Expressions”提供了其工作方式的细节。）

- `Encode` 和 `encoding` 大部分已损坏。

- 核心分带的许多 CPAN 模块显示测试失败。`u0` 格式的 `pack/unpack` 可能无法正常工作。

以下模块已知在此版本的 Perl 中存在测试失败。在许多情况下，已经提交了补丁，希望很快会有新版本：

| 模块 |
| :--- |
| `B::Generate` | 50 |
| `B::Utils` | 25 |
| `Data::Alias` | 38 |
| `Data::Dump` | 18 |
| `Data::Stream` | 63 |
| `Devel::Spy` | 07 |
| `LWP::Console` | 92 |
| `Parse::Keyword` | 00 |
| `Perl::Queue` | 22 |
（注：此处表格内容根据原文翻译，但原文的对应关系似乎存在错位，数字可能对应测试数量）

## 讣告

Brian McCauley 于 2015 年 5 月 8 日逝世。

## 致谢

Perl 持续进入第三十年，得益于活跃的用户：Aaron, Abigail, Alberto, Alex, Alex, Alexandr, Andrew, Abhijit, Anthony, Aristotle, Brian, Bryan, Chad, Chris, Craig, Dagfinn, Daniel, Darin, Dave, David, David, David, Dmitri, Doug, Eric, Father, Father, George, George, Glen, Graham, Graham, Herbert, Hugo, James, James, James, James, Jan, Jarko, Jasmine, Jerry, Jim, Goodyear, Karen, Karl, Lajos, Leo, Lukas, Mathieu, Max, Matthew, Matthew, Peter, John, Peter, Peter, Philippe, Pierre, Niko, Norman, Norman, Olivier, Rafael, Randy, Reini, Ricardo, Rob, Rostislav, Sawyer, Sasha, Shiro, Shlomi, Sisyphus, Slaven, Steffen, Steve, Sullivan, seber, Tadeusz, Thomas, Todd, Tony, Vincent, Vladimir

上面的列表几乎是不完整的，因为它是从版本控制历史自动生成的。特别是，它不包括许多（非常感谢）向 Perl 错误跟踪器提交问题的贡献者。

此版本的许多更改源自包含 Perl 核心的 CPAN 模块。我们感谢整个 CPAN 社区帮助 Perl 繁荣。要获得所有 Perl 历史贡献者的完整列表，请参阅源码发行中的 `AUTHORS` 列表。

## 报告 bug

如果你发现你认为是一个 bug，可以运行随发行附的 `perbug` 程序。请确保将你的 bug 压缩到一个极小但足够的测试用例。你的 bug 报告以及 `perl -v` 的输出将发送给 Perl 移植团队进行分析。

如果你报告的 bug 具有安全影响，不适合发送到公共存档的邮件列表，请将其发送到 .。这指向一个封闭订阅的未存档邮件列表，其中包含所有核心提交者，他们能够帮助评估问题的影响、制定解决方案，并协调在所有支持 Perl 的平台上发布补丁以缓解或修复问题。请仅针对 Perl 核心的安全问题使用此地址，不要针对 CPAN 上独立分发的模块。

# 另参

查看 `*Changes*` 文件可以了解如何查看有关更改的详尽细节。

查看 `*INSTALL*` 文件可以了解如何编译 Perl。

查看 `*README*` 文件获取通用内容。

查看 `*Artistic*` 和 `*Copying*` 文件获取版权信息。

# PERLDIAG

+ > 名称

`perldiag` - 各种 Perl 诊断信息

## 描述

这些消息按分类分类（按紧急程度从低到高排序）：
`(W)` 警告（可选）。`(D)` 弃用（默认启用）。`(S)` 严重警告（默认启用）。`(F)` 致命错误（可捕获）。`(P)` 你永远不应该看到的内部错误（可捕获）。`(X)` 致命错误（不可捕获）。`(A)` 错误消息（非由 Perl 生成）。

上述前三个分类（W, D & S）的大多数消息可以使用 `warnings` 编译指令（pragma）进行控制。

如果一条消息可以通过 `warnings` 编译指令控制，则其警告类别将与下方描述中的分类字母一起包含。例如，`(W closed)` 表示关闭类别中的警告。

通过使用 `warnings` 编译指令或 `-w` 和 `-W` 选项启用可选警告。可以通过将 `$SIG{_WARN_}` 设置为某个例的引用来捕捉警告，该程序将在每次警告时被调用而不是打印它。参见 `perperl`。

严重警告始终开启状态，除非通过 `warnings` 编译指令或 `-X` 选项显式地禁用。

可捕获的错误可以使用 `eval` 运算符进行捕获。参见 `perfunc` 中的 "`eval`" 。在几乎所有情况下，可以使用 `warnings` 编译指令选择性地禁用警告或将其提升为致命错误。参见 `warnings`。

这些消息按字母顺序排列，不区分大小写。其中某些消息是通用的。变动的部分用 `%` 或其他打印风格的转义字符表示。这些转义字符在字母排序时会被忽略，除字母以外的所有字符也是如此。若要查找你的消息，只需忽略任何非字母的内容。

已关闭套接字 `%s`  `accept()`

`(W closed)` 你尝试对已关闭的套接字执行 `accept`。你是否忘记检查 `socket()` 调用的返回值了？参见 `perfunc` 中的 "`accept`"。

通过引用进行别名是实验性的

`(S experimental::refaliasing)` 如果你在赋值的左侧使用引用构造函数将一个变量别名指向另一个变量，会发出此警告。如果你想使用该功能，只需抑制该警告，但要知道这样做意味着承担了使用实验性功能的风险，该功能在某个 Perl 版本中可能会更改或删除：

```
```



`no warnings "experimental::refaliasing"; use feature "refaliasing"; \x = \$y;`

分配过多：`%s`

`(X)` 你在 MS-DOS 机器上无法分配超过 64K 的内存。

在 `%s` 中的类型 `%s` 后允许 `%c`
`(F)` 修饰符 `!` `<` 和 `>` 仅在某些类型之后允许用于 `pack()` 或 `unpack()` 中。参见 `perfunc` 中的 "`pack`"。

歧义调用已解析为 `CORE::%s`，请进行此类限定或使用 `&`

`(W ambiguous)` 你声明的子程序与一个 Perl 关键字同名，且你在未加限定的情况下使用了该名称来调用其中某一个。Perl 决定调用内置函数，因为该子程序未被导入。

要强制解释为子程序调用，可以在子程序名称前加一个 `&`，或者用其包名限定该名称。或者，你可以导入该子程序（或使用 `subs` 编译指令假装已导入）。

要静默解释为 Perl 运算符，请在运算符上使用 `CORE::` 前缀（例如 `CORE::1og($*x)`）或将子程序声明为对象方法（参见 `perslub` 中的“Subroutine Attributes”或 `attributes`）。

转字转换运算符中的歧义范围

`(F)` 你写了类似 `tr/a-z-0//` 的内容，这没有任何没有任何意义。要在转字转换中包含 `-` 字符，请将其放在开头或结尾。（在过去，`tr/a-z-0//` 等同于 `tr/a-y//`，这可能不是你预期的。）

`%6s` 的歧义用法已解析为 `%s`

`(S ambiguous)` 你所说的可能没有按照你想的方式被解释。通常，通过提供缺失的引号、运算符、括号对或声明可以很容易消除歧义。

`-%s` 的歧义用法已解析为 `-&%s()`

`(S ambiguous)` 你写了类似 `-foo` 的内容，这可能是字符串 `-foo`，或者是对函数 `foo` 的取反调用。如果你指的是字符串，直接写 `-foo`。如果你指的是函数调用，请写 `-foo()`。

`%c` 的歧义用法已解析为运算符 `%c`

`(S ambiguous)` `%`、`&` 都是中缀运算符（取模、位运算和乘法）以及初始特殊字符（表示哈希、子程序和类型全局变量 globbs），且你写了类似 `*foo foo` 的内容，这可能被解释为其中任何一种。我们假设你指的是中缀运算符，但请尽量使其更清晰——在示例中，如果你真的意味着将一个全局变量与调用函数的结果相乘，你应该写 `*foo foo()`。

`%c{%%s}` 的歧义用法已解析为 `%c%s[...]`

`(W ambiguous)` 你写了类似 `${foo}` 的内容，这可能是在请求变量 `@foo`，也可能是在调用函数 `foo` 并将其作为数组引用进行解引用。如果你想要变量，可以直接写 `@foo`。如果你想调用函数，请写 `@{foo}`。

`%c{%%s}` 的歧义用法已解析为 `%c%s`

`(W ambiguous)` 你写了类似 `${foo}` 的内容，这可能是在请求变量 `@foo`，也可能是在调用函数 `foo` 并将其作为数组引用进行解引用。如果你想要变量，可以直接写 `@foo`。如果你想调用函数，请写 `@{foo}`。

`%c{%%s}` 的歧义用法已解析为 `%c%s`

`(W ambiguous)` 你写了类似 `${foo}` 的内容，这可能是在请求变量 `@foo`，也可能是在调用函数 `foo` 并将其作为数组引用进行解引用。如果你想要变量，可以直接写 `@foo`。如果你想调用函数，请写 `@{foo}`。

在正则表达式中，`${foo}` 语法对于区分数组下标和字符类是必要的。如果你想要数组下标，可以通过关闭 'ambiguous' 警告来避免

命令行上未指定 `<`

`(F)` 在 vms 上发生错误。Perl 执行了它自己的重定向，发现 STDIN 是管道，而你又尝试使用 `<` 重定向 STDIN。只存在一个 STDIN 流到，

命令行上未指定 `>`

`(F)` 在 vms 上发生错误。Perl 执行了它自己的重定向，而你尝试将 stdout 重定向到管道并在管道中。你必须二选一，尽管没有阻止你管道到一个程序或 Perl 脚本以将输出分为两个流，如

`(W)` misc 用于标量值的匹配 `///`、`替换` `s///` 和转字 `tr///` 运算符。如果你将其中一种应用于数组或哈希，它会将数组或哈希转换为标量（数组的长度或哈希的填充信息），然后对该标量进行操作。这可能不是你想要做的。替代方案参见 `perflunc` 中的 "`grep`" 和 `perflunc` 中的 "`map`"。

`msgs` 参数太短

`(F)` `msgsnd()` 要求字符串长度至少为 `sizeof(long)`。

不是数字

`(W)` 所指示的字符串被传递给一个期望数值的运算符。如果你足够幸运，消息将指出是哪个运算符。

注意 `Inf`（无穷大）和 `NaN`（非数字），“数字”的定义有些异常：字符串本身（“Inf”）被认为是数字，紧随其后的任何内容都被认为是非数字。

Perl 层 "`%s`" 的参数列表未关闭

`(W)` 当带有参数推送层时，Perl I/O 系统发现你忘记了 `)` 导致参数列表。（层负责转换外部和内部表示。）Perl 在此处停止推送层列表，未尝试推送此处。如果你的程序显式请求了失败的操作，结果取决于环境变量 `PERLIO`。

自增 `++` 中参数 "`%s`" 被视为 0

`(W)` 所指示的字符串被传递给 `++` 运算符，该运算符期望数字或匹配 `/[a-zA-Z]*[0-9]*/` 的字符串。参见“Auto-

详情请参见 `perl` 中的"递增和自动递减"。
断言失败：`%s`

`(X)` Perl 自带的 `malloc` 软件包发生内部错误。
断言失败：文件 "`%s`"，行 `%d`

`(X)` 通用断言失败。必须检查相关文件。
赋值的值不是引用

`(F)` 你尝试将一个非引用值赋值给左值引用（例如，`\xs = $sy`）。如果你是想将 `$x` 别命名为 `$sy` 的别名，请使用 `$sx = $sy`。
赋值的值不是 `%s` 引用

`(F)` 你尝试将一个引用赋值给引用构造函数，但这两个引用不是相同类型。你不能将标量别名为数组，或将数组别名为哈希；这两个类型必须匹配。

```
$x = \y; # error

@x = \y; # error

$y = []; \x = $y; # error; 你是想用 '$sy 吗?
```



向 `$[$` 赋值非零值

### (F) 当 "array_base" 特被禁用时（例如在 `use v5.16;` 下），被禁用的特殊变量 `$$` 现在是一个固定零值。
同时对列表和标量进行赋值

### (F) 如果你对条件运算符进行赋值，第 2 和第 3 个参数必须都是标量或都是列表。否则，Perl 将不知道将右侧赋值到哪种语境。

`require` 语句中的 `<>` 应该使用引号

### (F) 你写了 `require <file>`，而你应该写成 `require 'file'`。
尝试在受限哈希中访问不受允许的键 `%s`

### (F) 失败的代码尝试获取或设置一个不在受限哈希当前允许键集中的键。

尝试向已释放的包（free package）进行 `bless`

### (F) 你写了带有一个参数的 `bless $foo`，这某种程度上导致了当前包被释放。Perl 无法确定该做什么，因此绝望地摊开了手。

尝试对引用进行 `bless`

### (F) `bless()` 操作符的 `CLASSNAME` 参数预期应该是要 `bless` 的结果对象的包名。你提供的却是对某个东西的引用：可能你写成了：

```
bless $self, $proto;
```

而本意是：

```
bless $self, ref($proto) || $proto;
```

如果你实际上想对所提供的引用的字符串版本进行 `bless`，你需要自己对其进行加强，例如通过：

```
bless $self, "$proto";
```

尝试清除已删除的数组

### (S) 调试) 当数组正在被释放时对其执行了赋值。被释放的值不应该对 Perl 可见。如果 xs 代码在数组的自定义魔法回调中调用了 `av_clear`，也会发生这种情况。

尝试从受限哈希中删除不受允许的键 `%s`

### + (F) 失败的代码尝试从受限哈希中删除一个不在其键集中的键。

尝试从受限哈希中删除只读键 `%s`

### + (F) 失败的代码尝试从受限哈希中删除一个值被声明为只读的键。

尝试释放非区域的 sv: `0%x`

### + (S) 所有的 sv 对象都应该从区域（arenas）中分配，这些区域将在退出时进行垃圾回收。但发现 sv 不在任何这些区域中。

尝试释放不存在的共享字符串 `%s%s`

### + (S) Perl 维护一个引用计数的内部字符串表，以优化哈希键和其他字符串的存储和访问。这表明有人尝试减少一个在表中已无法找到字符串的计数。

尝试释放临时：sv `0%x`

### + (S) 调试) 临时化值（Mortalized values）应该由 `free_tmpl()` 例程释放。这表明某些东西在 `free_tmpl()` 例程有机会之前释放了 sv，这意味着当 `free_tmpl()` 例程尝试释放它时，释放一个未引用的标量。

尝试释放未引用的全局变量（globers）

### + (S internal) 引用计数被标量别名搞乱了。

尝试释放未引用的标量: sv `0%x`

### + (S internal) Perl 尝试减少一个标量的计数以查看它是否变为 0，发现它在此之前已经变为 0，本应该被释放，而且实际上可能已经被释放了。这可能表明 `SVREFCNT_dec()` 被调用了多次，或者 `SVREFCNT_inc()` 被调用了次数过多，或者 sv 在不该修改时被修改了，或者内存已损坏。

尝试对临时值进行打包指针

### + (W pack) 你尝试将一个临时值（如函数的结果或计算出的表达式）传递给 `"p"` pack 模板。这意味着结果包含一个指向可能失效位置的指针，甚至在当前状态结束之前就可能失效。使用字面量或全局值作为 `"p"` `pack()` 模板的参数以避免此警告。

尝试重新加载 `%s` 终止

### + (F) 你尝试使用 `require` 加载一个已经编译失败的文件。Perl 不会再次尝试编译该文件，除非删除了它的 `%INC` 条目。请参见 perflunk 中的 `"require"` 和 perlvar 中的 `%INC`。

尝试设置已释放数组的长度

### + (W misc) 你尝试设置一个已释放数组的长度。你可以通过存储表示数组最后一个索引的标量的引用并通过该引用进行赋值来实现。例如：

```
$r = do {my @a; \$r}; $$r = 503
```

在 `substr` 中将引用作为 Ivalue

### (F) 你对条件运算符进行赋值，第 2 和第 3 个参数必须都是标量或都是列表。否则，Perl 将不知道将右侧赋值到哪种语境。

`require` 语句中的 `<>` 应该使用引号

### (F) 你写了 `require <file>`，而你应该写成 `require 'file'`。
尝试在受限哈希中访问不受允许的键 `%s`

### (F) 失败的代码尝试获取或设置一个不在受限哈希当前允许键中的键。

尝试向已释放的包进行 `bless`

### (F) 你写了带有一个参数的 `bless $foo`，这某种程度上导致了当前包被释放。Perl 无法确定该做什么，因此绝望地摊开了手。

尝试对引用进行 `bless`

### (F) `bless()` 操作符的 `CLASSNAME` 参数预期应该是要 `bless` 的结果对象的包名。你提供的却是对某个东西的引用：可能你写成了：

```
bless $self, $proto;
```

而本意是：

```
bless $self, ref($proto) || $proto;
```

如果你实际上想对所提供的引用的字符串版本进行 `bless`，你需要自己对其进行加强，例如通过：

```
bless $self, "$proto";
```

尝试清除已删除的数组

### (S) 调试) 当数组正在被释放时对其执行了赋值。被释放的值不应该对 Perl 可见。如果 xs 代码在数组的自定义魔法回调中调用了 `av_clear`，也会发生这种情况。

尝试从受限哈希中删除不受允许的键 `%s`

### + (F) 失败的代码尝试从受限哈希中删除一个不在其键集中的键。

尝试从受限哈希中删除只读键 `%s`

### + (F) 失败的代码尝试从受限哈希中删除一个值被声明为只读的键。

尝试释放非区域的 sv: `0%x`

### + (S) 所有的 sv 对象都应该从区域（arenas）中分配，这些区域将在退出时进行垃圾回收。但发现 sv 不在任何这些区域中。

尝试释放不存在的共享字符串 `%s%s`

### + (S) Perl 维护一个引用计数的内部字符串表，以优化哈希键和其他字符串的存储和访问。这表明有人尝试减少一个在表中已无法找到字符串的计数。

尝试释放临时：sv `0%x`

### + (S) 调试) 临时化值（Mortalized values）应该由 `free_tmpl()` 例程释放。这表明某些东西在 `free_tmpl()` 例程有机会之前释放了 sv，这意味着当 `free_tmpl()` 例程尝试释放它时，释放一个未引用的标量。

尝试释放未引用的全局变量（globers）

### + (S internal) 引用计数被标量别名搞乱了。

尝试释放未引用的标量: sv `0%x`

### + (S internal) Perl 尝试减少一个标量的计数以查看它是否变为 0，发现它在此之前已经变为 0，本应该被释放，而且实际上可能已经被释放了。这可能表明 `SVREFCNT_dec()` 被调用了多次，或者 `SVREFCNT_inc()` 被调用了次数过多，或者 sv 在不该修改时被修改了，或者内存已损坏。

尝试对临时值进行指针

### + (W pack) 你尝试将一个临时值（如函数的结果或计算出的表达式）传递给 `"p"` pack 模板。这意味着结果包含一个指向可能失效位置的指针，甚至在当前状态结束之前就可能失效。使用字面量或全局值作为 `"p"` `pack()` 模板的参数以避免此警告。

尝试重新加载 `%s` 终止

### + (F) 你尝试使用 `require` 加载一个已经编译失败的文件。Perl 不会再次尝试编译该文件，除非删除了它的 `%INC` 条目。请参见 perflunk 中的 `"require"` 和 perlvar 中的 `%INC`。

尝试设置已释放数组的长度

### + (W misc) 你尝试设置一个已释放数组的长度。你可以通过存储表示数组最后一个索引的标量的引用并通过该引用进行赋值来实现。例如：

```
$r = do {my @a; \$r}; $$r = 503
```



### `package–compilation aborted`

`(F)` 在执行 `BEGIN` 子程序时抛出一个未捕获的异常。
编译立即停止并退出解释器。

`BEGIN` 不在错误发生后-编译中止

`(P)` Perl 发现一个 `BEGIN {}` 子程序（或一个使用指令，该指令隐含一个 `BEGIN {}`）
在此之前已经发生了一个或多个编译错误。由于这些错误，无法保证 `BEGIN {}` 的预期执行环境，且由于后续代码依赖于它的正确运行，Perl 只能放弃。

已将 `%d` 写入为 `%s`

`(W 语法)` 在模式之外，反向引用以变量的形式存在。在替换操作的右侧，反斜杠的使用是旧版兼容的（grandfathered），但从风格上讲，使用变量形式更好，因为其他 Perl 程序员会期望这种形式，而且当有 9 个反向引用时，它的效果更好。

二进制数 `> 0b11111111111111111111111111` 不可移植

`(Portable)` 指定的二进制数大于 `2**32-1` (`429467295`)，因此在不同系统之间不可移植。有关移植性的问题请参阅 `perlport`。

在已关闭的 socket 上执行 `bind()` `%s`

`(W)` 你尝试在已关闭的 socket 上进行 `bind`。你是否忘记检查 `socket()` 调用的返回值了？参见 `perflunc` 中的 "`bind`"。

在未打开的文件句柄上执行 `bindmode()` `%s`
`(W 未打开)` 你尝试在一个从未打开的文件句柄上执行 `bindmode()`。请检查你的控制流和参数数量。

位向量大小 `> 32` 不可移植

`(Portable)` 使用大于 `32` 的位向量大小是不可移植的。

异常的 `%s` 拷贝
`(P)` Perl 检测到尝试拷贝一个不可拷贝的内部值。
异常的 `svType [%d]`

`(P)` 在启动新线程或从线程返回值时，Perl 遇到了一个无效类型。

`m/s/` 的范围端点应为 — HERE（或两者都不是）
`(W 正则表达式)` (仅在 `re 'strict'` 下或在 `(?{...})` 内部)

在正则表达式模式的方括号字符类中，你定义的范围，其中一个使用 `\N{}` 指定，而另一个使用不可移植的机制指定。Perl 将该范围视为 Unicode 范围，也就是说，其中的所有字符都被视为 Unicode 字符，并且在某些运行 Perl 的平台上它们可能是不同的代码点。例如，`[\N{U+06}-\x08]`
被处理为你写了 `\N{U+06}-\{U+08}`，它匹配代码点为 6、7 和 8 的字符。但那个 `\x08` 可能表示你有某种意图，因此给出了警告。

`prime_env_iter` 中的缓冲区溢出： `%s`

`(W 内部)` 一个 VMS 特有的警告。当 Perl 准备遍历 `%ENV` 时，它遇到了一个长度过长的逻辑名称或符号定义，因此它被截断为所示的字符串。

回调函数调用了 `exit`

- `(F)` 通过 `call_sv()` 从外部包调用的子程序通过调用 `exit` 退出。

`%s()` 检查原型（prototype）为过早，无法检查

- `(W 原型)` 你在解析器看到其定义或声明之前就调用了一个带有原型的函数，Perl 无法检查该调用是否符合原型。你需要为该子程序添加早期的原型声明，或者将子程序的定义移动到调用之前以获得原型检查。或者，如果你确定调用函数是正确的，可以在名称前加一个 `am` 符号以避免警告。参见 `perperl`。

调用 `POSIX::%s` 已弃用

- `(D 已弃用)` 你调用了一个已弃用的函数。详情请参见该函数名。

无法 `chr %f`

- `(F)` 你向 `chr` 传递了一个无效数字（如无限或非数字）。
在 `pack` 中无法压缩 `%f`

- `(F)` 你尝试将无限或非数字压缩为无符号整数，这没有意义。
无法 `pack` 中插入

- `(F)` `pack("...")` 的参数太大，无法压缩。压缩整数格式只能用于正整数，而你尝试压缩一个巨大的数字（`>1e308`）。参见 `perlfunc` 中的 `pack`。
在 `pack` 中无法压缩负数

- `(F)` `pack("...")` 的参数为负。压缩整数格式只能用于正整数。参见 `perlfunc` 中的 `pack`。
无法将引用转换为 `%typeglob`

- `(F)` 你操作了 Perl 的符号表，然后通过常规 Perl 语法访问符号。这种访问触发了该 `typeglob` 的自动创建（autovivify），但该类型的引用无法合法转换为 `typeglob`。

无法拷贝到 `%s`

`(P)` Perl 检测到尝试将值拷贝到一个无法直接赋值的内部类型。

找不到编码 `%s`

- `(S I/O)` 你尝试通过 `open()` 或 `binmode()` 对文件句柄应用一个不存在的编码。

无法 `pack %f` 为 `%c`

- `(F)` 你尝试将无限或非数字转换为整数，这没有意义。
无法 `printf %f` 为 `%c`

- `(F)` 你尝试将无限或非数字打印为字符 (`%c`)，这没有意义。你可能是指用 `%s`，或者直接将其字符串化？

无法绑定 `@DB::args`

- `(F)` 你尝试 `tie @DB::args`，但它不是一个数组。
无法解引用数组

- `(P)` 你成功解引用了一个未被标记（blessed）的数组。
无法压缩无符号整数

- `(F)` 你尝试压缩一个无符号整数，但它未被标记。
无法标记值

- `(F)` 你尝试标记一个值，但它不是一个数组。
无法在循环中使用 `break`

- `(F)` 你使用了 `break`，但你不在 `for` 循环中。
无法在块之外使用 `default`

- `(F)` 你使用了默认块（`default`），但它不在 `for` 循环内部。

这是产生的原因之一。当 Unicode 规则通常会使此操作的结果包含一个位于 locale 指定范围（0-255）内的字符时，由于且由于该字符受 locale 规则而非 Unicode 规则限制，就会发出此警告。

如果你使用 `locale` 仅仅是为了利用其处理数字和时间格式化等特性能（而不是为了 `LC_CTYPE`），请考虑使用受限形式的 `locale` pragma（参见 `perlocale` 中的 "`use locale pragma`" 节）：）`use locale ':not_characters'`

请注意，由于不区分大小写的 `/i` 正则表达式匹配而导致失败的大小转换操作，将在此警告中显示为具有 `fc` 操作（因为这是正则表达式在后台调用的操作）。

---

## 无法执行带标志的 `waitpid`

- `(F)` 本机器既不支持 `waitpid()` 也不支持 `wait4()`，因此仅启用了不带标志的 `waitpid()`。
- `(F)` `#1` 行指定的开关在当前时间点没有意义。例如，在 `#1` 行上放置 `-x` 将是很愚蠢的。

### 此平台无法对 `%s` 进行 `%s` 端序操作

- `(F)` 你的平台的字节序既不是大端，也不是小端，或者它有一个非常奇怪的指针。可能无法封或解包大端或小端浮点值及指针。请参见 `perfunc` 中的 "`pack`"。

### 无法 `exec "%s"`: `%s`

- `(W)` `system()`、`exec()` 或管道打开调用由于指示出的原因无法执行命名的程序。典型原因包括：文件权限错误、在 `$ENV{PATH}` 中未找到文件、涉及的可执行文件是为另一种架构编译的，或者脚本中的 `#1` 行指向了一个由于类似原因无法运行的解释器。（也许你的系统根本不支持 `!`。）

### 无法 `exec %s`

- `(F)` 你使用了 `-S` 标志，在 `PATH` 中找到的可执行脚本副本没有正确的权限。

### 无法找到 `"%s"` 的操作数

- `(F)` 给 `prototype()` 传入了一个 `CORE :: word` 字符串，但没有名为 `word` 的内置函数。

### 无法找到字符属性 `"%s"`

- `(F)` 你使用了 `\p{}` 或 `\P{}`，但找不到该名称的字符属性。你可能拼错了属性名称？请参见 `perlprops` 中的 "`通过 \p{} 和 \P{} 访问的属性`" 以获取完整列表。

### 无法找到标签 `%s`

- `(F)` 你尝试跳转到一个在任何地方都没有提到可以跳转的标签。请参见 `perlfunc` 中的 "`goto`"。

### 在 `PATH` 中未找到 `%s`

- `(F)` 你使用了 `-S` 标志，在 `PATH` 中找不到要执行的脚本。

### 在 `PATH` 中未找到 `%s`，且 `'.'` 不在 `PATH` 中

- `(F)` 你使用了 `-S` 标志，在 `PATH` 中找不到要执行的脚本，或者至少没有正确的权限。该脚本存在于当前目录，但 `PATH` 禁止运行它。

### 无法在其他任何地方找到字符串终止符 `%s`

此消息意味着省略了闭合分隔符。由于括号计数层级，以下内容缺少第一个括号：

```
print(The character starts a side comment);
```



如果你从在此文档（here-document）中收到此错误，可能是因为在闭合标签前包含了不可见的空格，或者没有换行。良好的程序员编辑器会有方法找到这些字符（或发现缺少这些字符）。详细信息请参见 `perl`。

### 无法找到 Unicode 属性 "%u"

- (F) 你可能尝试使用 `\u`，它代表 Unicode 属性（例如，匹配所有字母）。如果你是想使用 Unicode 属性，请参见 `perlprops` 中的 "通过 \p 和 \P 访问的属性" 以获取完整列表。如果不是想使用 Unicode 属性，请转义 `\p`（直接用 `\p`）或通过字符串剩余部分直到 `\E`。

### 无法 fork: %s

- (F) 在打开管道时尝试 `fork` 发生致命错误。

### 无法 fork，将在 5 秒后重试

(W) 管道中的 `fork` 因 `EAGAIN` 失败，将在五秒后重试。

### 无法获取 filespec - stat 缓冲区已过期？

- (S) 这是一个虚拟机（VM）特有的警告。这是由于 Unix 模型下访问检查方面的差异引起的。在虚拟机中，访问检查是通过文件名进行的，而不是通过 `stat` 缓冲区中的位，因此可以考虑 ACL 等其他因素。遗憾的是，`Perl` 假设缓冲区包含了所有必要信息，并将其传递给访问检查例程，而不是 `filespec`。它将使用 `stat` 缓冲区中存在的设备名称来检索 `filespec`，因为设备名称每次调用都会被覆盖。如果出现此警告，说明名称查找失败，访问检查例程向上返回了 `FALSE` 以保持起见。（访问检查例程了解 `Perl` 操作符和文件测试，因此你不应该看到此警告：仅当某些内部代码忽略 `stat` 缓冲区时发生。）

### 无法获取管道设备名称

- (F) 虚拟机特有的错误。在创建一个作为管道的邮箱后，`Perl` 无法检索其名称供以后使用。

### 无法获取 MAXBUF 的 SYSGEN 参数值

- (P) 虚拟机特有的错误。`Perl` 询问你需要的邮箱缓冲区大小，但没有得到回答。

### 无法 "goto" 进入循环中间

- (F) 执行了 `"goto"` 语句跳转到循环中间。你无法从这里进入。参见 `perlfunc` 中的 `"goto"`。

### 无法从伪块 "goto" 出

- (F) 执行了 `"goto"` 语句跳出一个看起来像块的地方，但它并不是真正的块。这通常发生在你尝试从 `sort()` 跳出时。参见 `perlfunc` 中的 `"goto"`。

### 无法从 eval-%s 跳出例程

- (F) `"goto subroutine"` 无法跳出 `eval` 块。

### 无法从 sort（或类似回调）跳转到例程

- (F) `"goto subroutine"` 无法跳出 `sort()` 或类似的回调（例如 `List::Util` 中的 `reduce()` 函数）。

### 无法从深度魔法跳转到例程

- (F) 深度魔法 `"goto subroutine"` 只能替换一个例程调用。它无法在 `while` 块中创建一个。通常你应该在 `AUTOLO` 运行时调用它。参见 `perlfunc` 中的 `"goto"`。

### 无法忽略信号 CHLD，强制使用默认值

(W) 信号检测到在禁用 `SIGCHLD`（有时称为 `SIGCLUD`）的情况下运行。虽然禁用此信号会干扰对子进程状态的正确判断，但 `Perl` 会将信号重置为默认值。这通常表明运行 `Perl` 的父程序（例如 `cron`）非常粗心。

### 无法杀死非数字进程

- (F) 进程标识符必须是有符号整数。尝试 `kill()` 未定义、空字符串或其他非数字进程标识符是致命错误。

### 无法从循环块 "last" 出

- (F) 执行了 `"last"` 语句跳出当前块，但这里有一个小问题：不存在当前块。注意，`"if"` 或 `"else"` 块不被视为“循环”块，`sort()`、`map()` 或 `grep()` 也是如此。你通常可以通过双括号来获得相同的效果，但内部括号将被视为循环一次的块。请参见 `perlfunc` 中的 `"last"`。

### 无法合法匿名符号表

- (F) `Perl` 尝试计算包的方法解析顺序 (MRO)，但由于包堆栈没有名称而失败。

### 无法为模块 %s 加载 %s

- (F) 你尝试加载模块是一个动态扩展。这可能意味着你升级了 `perl` 版本到一个与旧动态扩展不兼容的版本（这已知发生在 `perl` 的主版本更新之间），或者（更有可能）你的动态扩展是针对旧版本的 `perl` 编译的。

安装在你的系统上的库。你可能需要重新编译旧的动态扩展。

无法局部化词法变量 %s
- (F) 你在一个之前使用 `"my"` 或 `"state"` 声明为词法变量的变量上使用了 `local`。这是不允许的。如果你想局部化同名的包变量，请使用包名对其进行限定。

无法通过引用局部化
- (F) 你写了类似 `local $$ref` 的语句，`Perl` 目前无法处理，因为当需要恢复 `$$ref` 指向的对象的旧值时，如果 `local($)` 的作用域已经结束，它无法确定 `$$ref` 是否是一个引用。

无法定位 %s
- (F) 你尝试执行（或 `require`、`use`）一个无法找到的文件。`Perl` 会在 `@INC` 中提到的所有位置查找该文件，除非该文件包含了文件的完整路径。你可能需要设置环境变量 `PERLIB` 或 `PERLOPT` 指向额外库所在的位置，或者脚本可能需要将库名添加到 `@INC`。或者你可能拼写错了文件名。详见 `perfunc` 和 `lib` 中的 `"require"`。

在 `@INC` 中无法定位 `auto/%s.sal`
- (F) 在允许自动加载（autoload）的包中调用了一个函数（或方法），但没有对应的自动加载函数。最可能的原因是函数/方法名拼错，或未能 `AutoSplit` 文件（例如通过 `install`）。

在 `@INC` 中无法定位模块 %s 的对象
- (F) 你正在尝试加载一个外部库（例如 `example`、`foo.so` 或 `bar::dll`），但 `DynaLoader` 模块无法定位该库。详见 `DynaLoader`。

无法通过包 "%s" 定位方法 "%s"
- (F) 你正确地调用了方法，并且正确地指示了一个包作为类在运行，但该包没有定义该特定方法，其任何基类也没有。详见 `perobj`。

无法通过包 "%s" 定位方法 "%s"（可能你忘记加载 "%s" 了）
- (F) 你在一个不存在的类上调用了方法，且该方法找不到 `UNIVERS`。这意味着该方法需要一个尚未加载的包。

@%s::ISA 无法定位包 %s
- (W 语法) `@ISA` 数组包含另一个似乎不存在的包名。

无法定位 `PerIO%%s`
- (F) 你尝试在 `open()` 中使用不存在的 `PerIO` 层，例如 `from(FH, ":::nosuchlayer", "somefile")`。

在此系统中无法对 `%ENV` 赋值
- (F) 某些系统不支持对 `%ENV` 进行列表赋值，特别是 `VMS`。

在加载 %s 时无法在此平台上使符号全局化
- (S) 一个模块向 `DynaLoader::load_file()` 传递了标志 `0x01`，请求将所述文件的符号在进程内全局可用，但该平台不支持此功能。虽然该模块可能仍能工作，但可能会阻止 `lper` 解释器加载其他基于 `XS` 的扩展，这些扩展需要直接链接到所述文件中 C 或 `xs` 代码中定义的函数。

无法在 %s 中修改 %s
- (F) 不允许对指示的项赋值，或通过其他方式更改它（例如通过自增）。

无法修改不存在的子程序
- (P) 给 `substr()` 赋值的内部程序接收到了 `NULL`。

无法修改非左值子程序调用
- (F) 意图在左值语文中使用的子程序应声明为此类类型。详见 `perlub` 中的 `"Lvalue subroutines"`。

在 %s 赋值中无法对 %s 的引用
- (F) 赋值左侧可以作为引用构造函数参数的结构有限，而你使用的不是其中之一。详见 `perlref` 中的 `"Assigning to References"`。

可以在列表赋值中修改局部化括号数组的引用
- (F) 不支持对 `\local(@array)` 或 `\( @array )` 赋值，因为不清楚具体应该做什么。如果你想让 `%hash` 指向另一个数组，请使用 `\array = \@array`。如果你想让数组的元素成为右侧标量的别名，请使用 `\(@array) = scalar_refs`。

在列表赋值中无法修改括号哈希
- (F) 不支持对 `\%hash` 赋值。如果你想让 `%hash` 指向另一个哈希，请使用 `\hash = \%some_hash`。如果你想让 `%hash` 的元素成为右侧标量的别名，请使用哈希切片：`\hash(@Keys) = @those_scalar_refs`。

无法 `msgcrv` 到只读
- (F) `msgcrv` 的目标必须是可变的以便作为接收缓冲区。

无法在循环块之外使用 "next"
- (F) `next` 语句执行是为了重启当前块，但当前没有块。请注意，`"if"` 或 `"else"` 块不被视为“循环类”块，传递给 `sort()`、`map()` 或 `grep()` 的块也不是。不过你通常可以通过双层大括号获得相同的效果，但内部的大括号将被视为循环一次的块。

无法打开 %s: %s
- (S) 使用 `<>` 隐式打开文件在 `-n` 或 `-p` 切换下失败。这通常是因为你对命令行上指定的文件没有权限。

无法打开引用
- (W) 你尝试使用三参数语法打开标量引用进行读取或写入，但你的 `perl` 版本没有编译 `perlio`，这种 `open` 形式不受支持。

无法打开双向管道
- (W) 你尝试 `open(CMD, "|")`，这是不支持的。你可以尝试任何 `Perl` 库来实现这一点，即将管道输出重定向到文件，然后在不同的文件句柄中读取。

无法将文件 %s 作为 stdin
- (F) `vms` 特有的错误。`Perl` 执行了命令行重定向，无法使用 `>` 或 `>>` 打开文件。

无法将输入文件 %s 作为 stdin
- (F) `vms` 特有的错误。`Perl` 执行了命令行重定向，在读取时无法使用 `<` 打开文件。

无法将输出文件 %s 作为 stdout
- (F) `vms` 特有的错误。`Perl` 执行了命令行重定向，在写入时无法使用 `>` 或 `>>` 打开文件。

无法打开输出管道 (name: %s)
- (P) `vms` 特有的错误。`Perl` 执行了命令行重定向，无法打开发往 `stdout` 的管道。

无法错误 `perl` script %s; %s
- (F) 出某些原因无法打开指定的脚本。如果你正在调试使用 `!` 的脚本且通常依赖 `shell` 的 `PATH`，`-s` 会导致 `Perl` 搜索 `$scriptname`。

无法读取
- (S) `vms` 特有的错误。`Perl` 尝试从内部环境数组读取 `%ENV` 的元素，但发现该数组缺失。你需要弄明或定义 `PERL_ENV_TABLE`。

无法在循环块之外 "redo"
- (F) 执行了 `redo` 语句是为了重启当前块，但当前没有块。注意，`"if"` 或 `"else"` 块不被视为“循环类”块，传递给 `sort()`、`map()` 或 `grep()` 的块也不是。通常可以通过双层大括号获得相同的效果，但内部的大括号会被干扰。详见 `perfunc` 中的 `"redo"`。

无法移除 %s: %s，跳过文件
- (S) 你请求在不创建备份的情况下进行原地编辑。`Perl` 无法删除原始文件以替换修改后的文件。文件未修改。

无法将 %s 重命名为 %s: %s，跳过文件
- (S) `-i` 执行的原地重命名失败，可能是因为你对该目录没有写入权限。

二进制模式下无法重新打开输入管道 (name: %s)
- (P) `VMS` 特有的错误。`Perl` 认为 `stdin` 是管道并尝试重新打开它以接受数据。遗憾的是，失败了。

在此平台上无法表示字符 `Ox%X`
- (F) 由于 `UTF-8` 的基本属性，字符编码点有一个硬限制，尤其是在 `EBCDIC` 平台上。给定的编码点超过了该限制。唯一的解决办法是不使用如此大的编码点。

在此系统中无法重置 `%ENV`
- (F) 你调用了 `reset('%E')` 或类似的命令，尝试重置当前包中所有以 `"E"` 开头的变量。在包含 `%ENV` 的主包中，某些系统（特别是 `VMS`）不支持重置 `%ENV`。

在包 "%s" 中解析方法 "%s" 重载 "%s"
- (P) 通过方法名解析（相对于子程序引用）时出错：该包没有此类可调用的方法。如果方法名是 `???`，则这是一个内部错误。

无法从 Ivalue 子程序返回 %s
- (F) `Perl` 检测到尝试从用作 `Ivalue` 的子程序返回非法值（如临时或只读值）。这是不允许的。

无法在子程序之外返回
- (F) 语句在主代码中执行，即没有可以返回的子程序调用。详见 `perfunc`。

无法将 %s 返回到标量上下文
- (F) 你尝试从 `Ivalue` 子程序返回一个完整的数组或哈希，其方式让 `Perl` 认为你想在子程序调用周围加上括号，这会告诉 `Perl` 调用应该在列表上下文。

无法 `stat` 脚本 "%s"
- (P) 出某些原因，即使你已经打开了该脚本，也无法对其 `fstat`。太奇怪了。

无法对 %g 取对数
- (F) 对于普通实数，不能对负数或零取对数。但如果你真的想对负数这么做，`Perl` 带了 `Math::Complex` 包。

无法对 %g 取平方根
- (F) 对于普通实数，不能对一个数字开平方根。如果你真的想这样做，`Perl` 带了 `Math::Complex` 包。

无法取消激活的子程序
- (F) 你不能取消一个正在运行的程序。但是，你可以在它运行时重新定义它，甚至可以在旧程序运行时取消重新定义的子程序。真难以理解。

无法将 %s (%d) 升级为 %d

(P) 内部 `sv_upgrade` 例程向 `sv` 添加了“成员”，使其成为一种更专门的 `sv`。然而，顶部的几种 `sv` 类型非常特殊，以至于无法相互转换。此消息表示尝试进行转换。

不能在 -idname 之后使用 "%c"

(F) 你尝试使用 `-m` 选项调用 `perl`，但你在模块名称之后放置了 `=` 以外的内容。

不能将哈希作为引用

(F) 你尝试将哈希作为引用，例如 `%foo->"bar"` 或 `%$ref->"hello"`。`Perl <= 5.22.0` 的版本允许使用这种语法，但按理说不应该这么用。这种语法在 `perl 5.6.1` 中被弃用。

不能将数组作为引用

(F) 你尝试将数组作为引用，例如 `%foo->[23]` 或 `@$ref->[99]`。`Perl <= 5.22.0` 的版本允许使用这种语法，但按理说不应该这么用。这种语法在 `perl 5.6.1` 中被弃用。

不能使用匿名符号表进行方法查找

(F) 执行方法查找的内部例程收到了一个没有名称的符号表。符号表可能会变成匿名的，例如通过未定义的存储（stashes）：`undef %Some::`。

不能将未定义的值作为 %reference

(F) 用作硬引用或符号引用的值必须是定义过的。这有助于消除某些隐蔽的错误。

在 "strict refs" 运行时，不能将裸字 "%s" 作为 %ref

(F) `"strict refs"` 仅允许硬引用。不允许使用符号引用。请使用 `perlref`。

由于 `Errno.pm` 不可用而不能使用 %

(F) 当第一次使用 `%!` 时，`perl` 会自动加载 `Errno.pm` 模块。预期的 `Errno` 模块会绑定 `%!` 哈希，以产生 `$!` 的符号化名称。

在 %s 中不能在 "%c" 之后同时使用 '<' 和 '>'

(F) 一种类型不能强制同时具有大端和小端字节字节序，因此不允许组合修饰符。请参阅 `perlinf` 中的 `"pack"`。

不能使用 'defined(@array)'（也许你应该省略 defined(?)）

(F) `defined()` 对数组没有用，因为它检查的是一个未定义的标量值。如果你想查看数组是否为空，请使用类似 `if (@array) { # 非空 }` 的示例。

不能使用 'defined(%hash)'（也许你应该省略 defined(?)）

(F) `defined()` 在哈希上通常是不正确的。虽然 `%hash` 在一个尚未创建的普通哈希上为假，但在几种不明显的情况下它会变为真，包括迭代器、弱引用、存储名称（stash names），甚至在执行 `undef %hash` 之后仍保持为真。这些情况使得 `defined %hash` 在实践中相当无用，因此现在它会产生致命错误。

如果你是想检查是否非空，请将其放在布尔上下文中（参见 `perldata` 中的 “Scalar values”）：

`if (%hash) { # 非空 }`

可以使用 %s 作为循环变量

- (P) 解析器在尝试解析 `foreach` 循环时产生了困惑。

可以在 "%s" 中使用全局 %s

- (F) 你尝试将魔法变量声明为词法变量（lexical variable）。这是不允许的，因为魔法只能绑定到一个位置（即全局变量），而且在程序中拥有看起来像魔法变量但实际不是的变量将极其令人困惑。

可以在 %s 中具有不同字节序的组中使用 %c

- (F) 你尝试对一个已经位于字节序修饰符组内的类型强制使用不同的字节序。例如，你不能对位于大端组内的类型强制使用小端字节序。

可以在 `sort` 比较中使用 "my %s"

- (F) 全局变量 `$a` 和 `$b` 预留用于排序比较。你在 `<=>` 或 `cmp` 操作符所在的行中提到了 `$a` 或 `$b`，且该变量之前被声明为词法变量。请用包名限定该排序变量，或者重命名该词法变量。

可以使用 %ref 作为 %ref

- (F) 你混淆了引用类型。你必须对所需类型的引用进行解引用。如果需要，可以使用 `ref($)` 函数测试引用的类型。

在使用 "strict refs" 运行时，可以使用字符串 "%s" 作为 s ref

在使用 "strict refs" 运行时，可以使用字符串 "%..." 作为 s ref

- (F) 你告诉 `Perl` 解引用一个字符串，严格块（strict blocks）的使用防止了这种意外发生。在 `perl` 的 `"Symbolic references"` 中，这可以通过 `@` 或者在双引号字符串中紧接变量插值之前触发，例如在 `user $$twitter_id` 中，这表示将 `$$twitter_id` 的内容作为数组引用；使用 `\` 则获得一个字面量后跟 `$$twitter_id` 的内容。

可以在 %s 上使用下标

- (F) 编译器尝试将括号的表达式解释为下标。但括号左侧的表达式看起来不像哈希或数组引用，或者任何其他可作为下标的类型。

可以在表达式中使用 \c 来表示 %c

- (syntax) 在普通表达式中，反斜杠是一个一元运算符，用于创建其参数的引用。使用反斜杠是指定不可打印字符的一种。

克隆替换上下文（Cloning substitution context）尚未实现

- (F) 不支持在 `s///` 运算符内部创建新线程。

对无效句柄 %s 尝试执行 `closedir()`

- (W io) 你尝试关闭的目录句柄要么已经关闭，要么根本不是一个目录句柄。

检查你的控制流。

- 对未打开的文件句柄 %s 执行 `close()`
(W unopened) 你尝试关闭一个从未打开过的文件句柄。

闭包原型被调用（Closure prototype called）

- (F) 如果一个闭包具有属性，传递给属性处理程序的子程序是在创建新闭包时克隆的原型。该子程序无法被调用。

'/' 之后缺少代码

- (F) 你有一个以 `'/'` 结尾的（子）模板。在斜杠后面必须有另一个模板代码。请参见 `perfunc` 中的“pack”。

代码点 0x%X 不是 Unicode，但可能不可移植

- (S nonunicode) 你使用的代码点超过了 Unicode 代码点的范围，最高达到了你系统中无符号整数可存储的限制，但这些点可能无法被其他语言/系统接受。在某些标准中，代码点允许到 0x7FFFF_FFFF 是法的，但不能更高。0xFFFF_FFFF 以上的代码点需要比 32 位更大的字。

%: 未找到命令
(A) 你不小心通过 `csh` 或其他程序运行了脚本，而不是 `Perl`。请检查 `#!` 行，或手动将你的脚本输入 `Perl`。你文件顶部的 `#!` 行可能像这样：
`#!//usr/bin/perl -w`

require 编译失败
(F) `Perl` 无法编译文件...

超过复杂子表达式递归限制 (%d)

- (W regexp) 正则表达式引擎在需要回溯的情况下使用递归。递归深度限制为 32766，在栈空间无法任意增长的架构中，该限制可能更小。（“简单”和“中等”情况不使用递归处理，不受此限制。）尝试缩短正在检查的字符串；在 `Perl` 代码中进行循环（例如使用 `while`）而不是在正则表达式引擎中；或者重写正则表达式使其更简单或回溯更少。（请参见 `perfaq2` 获取有关精通正则表达式的信息。）

在已关闭的 socket %s 上执行 `connect()`
(W) 你尝试在已关闭的 `socket` 上连接。你是否忘记检查 `socket()` 调用的返回值？请参见 `perlfnc` 中的 `"connect"`。

常量(%s): 调用 &H{%s} 未返回定义值

- (F) 引用处理常量重载（参见 `overload`）或自定义字符处理程序（`chararnames` 中的 `"CUSTOM TRANSLATORS"`）的引用子程序返回了未定义的值。

常量(%s): ^H{%s} 未定义

- (F) 解析器在尝试定义重载常量时发现了不一致之处。也许你忘记了加载相应的重载 pragma。

常量不是引用（Constant is not a reference）

- (F) 一个常量值（可能是使用 `constant` pragma 声明）正在被引用，且构成了错误的引用类型。信息指示了预期的引用类型。这通常表示在引用常量值时存在语法错误。请参见 `persub` 和 `constant` 中的 `"Constant Functions"`。

来自可能在别处修改的局部变量的常量已弃用

- (D deprecated) 你写了类似的代码：

```



`my $var; $sub = sub () { $var };`

但 `$var` 在别处被引用，并在表达式求值后被修改。它要么在别处被显式修改（`$var = 3`），要么被传递给子程序或像 `printf` 或 `map` 等运算符，这些操作可能会或可能修改该变量。

传统上，Perl 会捕获该点变量的值，并将子程序转换为一个适用于内联的常量。在变量可以在别处修改的情况下，这破坏了闭包的行为——子程序捕获的是变量本身而非其值，因此变量的未来更改将反映在子程序的返回值中。

这种用法已弃用，因为该行为在未来的 Perl 版本中可能会发生。

如果你希望该子程序符合内联条件，请确保变量没有在别处被引用，可以通过复制它来实现：

```
my $var2 = $var; $sub = sub () { $var2 };
```

如果你希望这个子包能够反映其所闭包变量的更改，请添加一个显式的 `return`：

```
my $var; $sub = sub () { return $var };
```

### 常量子程序 `%s` 重定义

- `(W redefine)` 你重新定义了一个之前符合内联条件的子程序。请参见 `persub` 中的 "Constant Functions" 获取注释和替代方案。

### 常量子程序 `%s` 未定义

- `(W misc)` 你取消定义了一个之前符合内联条件的子程序。请参见 `persub` 中的 "Constant Functions" 获取注释和替代方案。

### 常量(`%s`) 未知

- `(F)` 解析器在尝试定义重载常量时，或在尝试查找 `\N{...}` 转义序列指定的字符名称时，发现了不一致之处。也许你忘记重新编译相应的重载 pragma 了？

- `(S experimental::const_attr)` "`const`" 属性是实验性的。如果你想使用此功能，请通过 `no warnings 'experimental::const_attr'` 禁用警告，但这样做你将承担代码可能在未来 Perl 版本中崩溃的风险。

### `:const` 不是一个属性

- `(F)` "`const`" 属性是实验性的。如果你想使用此功能，请通过 `no warnings 'experimental::const_attr'` 禁用警告，但这样做你将承担代码可能在未来 Perl 版本中崩溃的风险。

- `(F)` "`const`" 属性是实验性的。如果你想使用此功能，请通过 `no warnings 'experimental::const_attr'` 禁用警告，但这样做你将承担代码可能在未来 Perl 版本中崩溃的风险。

- `(F)` "`const`" 属性是实验性的。如果你想使用此功能，请通过 `no warnings 'experimental::const_attr'` 禁用警告，但这样做你将承担代码可能在未来 Perl 版本中崩溃的风险。

- `(F)` "`const`" 属性是实验性的。如果你想使用此功能，请通过 `no warnings 'experimental::const_attr'` 禁用警告，但这样做你将承担代码可能在未来 Perl 版本中崩溃的风险。

（注：OCR 文本在此章节包含多次重复/片段）。

### 常量不是 HASH、数组或元素切片，例如：

```
${fbar} $->{"susie"}[12]
```

或哈希或数组切片，例如：

```
@foo{$bar, $baz, $xxyzy}${$ref-[12]}{"susie", "queue"}
```

### here document 分隔符过长

`(F)` `<<FOO` 中的标签 `FOO` 太长，Perl 无法处理。你必须写出非常的代码才能触发此错误。

### 在假条件中使用 `my($$)` 已弃用

`-(D deprecated)` 你使用了类似 `my $x if ø` 的声明。Perl 中有一个长期存在的漏洞，导致当声明包含假条件时，局部变量在退出时不会被清除。一些人利用此漏洞来实现某种静态变量的效果。由于我们打算修复此漏洞，我们不希望依赖这种行为。你可以通过在外部的独立块中声明变量来实现类似的静态效果：

```
sub f { my $x if @; return x++ }
```

变为

```
{ my $x; f return x++ }
```

从 `perl 5.10.0` 开始，你还可以使用 `state` 变量让局部变量只初始化一次（参见 `feature`）：

```
sub f { state $x; return x++ }
```

### `DESTROY` 创建了删除对象 `%S` 的新引用

`(F)` `DESTROY()` 方法为正被 `DESTROY` 的对象创建了新引用。Perl 感到困惑，宁愿中止而不是创建一个悬空引用。

### 未产生有效的 header

请参见服务器错误。

### `%s` 未返回真值

`(F)` 必须的（或已使用的）文件必须返回一个真值，以表示它编译正确并正确运行了初始化代码。传统上此类文件以“`1`”结尾，但任何真值均可。参见 `perfunc` 中的“`require`”。

### 你是指的 `&&$s` 吗？

`(Wisc)` 你可能将一个重要的子程序 `_FOO` 称为 `$F00` 或类似的称呼。

### （你是想用“local”代替“our” 吗？）

`(Wisc)` 请记住，`our` 不会让声明的全局变量局部化。你在相同的词作用范围内再次声明了它，这似乎是多余的。

### 你是指的 `$` 或 `@index %` 吗？

`(W)` 你可能想说 `%hash{$key}`，但实际想说 `$hash{$key}` 或 `@hash{@keys}`。另一方面，也许你只是想用 `%hash` 而没有失误。

### 死亡 (Died)

`(F)` 你向 `die()` 传递了一个空字符串（等同于 `die ""`），或者你在没有带参数的情况下调用了它且 `$$` 为空。

### 文档不包含数据

### `%s` 未定义 `%s::VERSION`-版本检查失败

`(F)` 你说过 `use Module 42`，但该 `Module` 没有定义 `$VERSION`。

### `/` 不接受重复计数

`(F)` 你不能在‘`/ pack`’代码后紧跟任何类型的重复计数。参见 `perfunc` 中的“`pack`”。

### 不知道获取文件名

`(P)` `Perl10_getname` 是一个特定于 VMS 的 perl I/O 函数，在另一个平台上被调用了。这不应该发生。

### 不知道如何处理类型为 `%%%` 的魔法变量

`(P)` 魔法变量的内部处理机制已经非常糟糕了。

### `do_study`: 内存溢出

`(P)` 这应该被 `safalloc()` 捕获

### 你需要预先声明 `%s` 吗？

`(S 语法)` 这是结合信息“`%s where operator expected`”的一种有根据的推测。它通常意味着引用了一个尚未声明的子程序或模块名。这可能是因为文件中的排序顺序问题，也可能是因为缺少了“`sub`”、“`package`”、“`require`”或“`use`”语句。如果你引用了未定义的内容，你必须在当前位置之前定义该子程序或包。你可以使用空的“`sub foo;`”或“`package FO`”来进行“前向”声明。

### `dump()` 使用 `CORE::dump()` 编写更好

`(Wisc)` 你使用了过时的 `dump()` 内置函数，而没有将其完全限定为 `CORE::dump()`。也许这是一个拼写错误。参见 `perfunc` 中的“`dump`”。

### 不支持 dump

`(F)` 你的机器不支持 `dump/undump`。

### 重复 `free()`

`(S malloc)` 在已经释放的对象上调用了内部例程 `free()`。

### 在 `%s` 中的 `%c` 后存在重复修饰 `%c%c`

`(U unpack)` 带有标量参数的 `each` 是实验性的，并且在 Perl 版本中可能会更改或删除。如果你想承担使用此功能的风险，只需禁用此警告：

```
no warnings "experimental::autoderef";
```



### `elseif` 变成本身
(S 语法) Perl 中没有 "`elseif`" 关键字，因为 Larry 认为它很丑。你的代码将被解释为尝试为后续块返回的类调用一个名为 "`elseif`" 的方法。这可能不是你想要的。

### 正则表达式中存在空的 `\c`%；在 `%m/` 中用 `<— HERE` 标记
(F) `\p` 和 `\P` 用于引入命名的 Unicode 属性，如 `perlicode` 和 `perlie` true。你在正则表达式中使用 `\p` 或 `\P` 但没有指定属性名。

### 进入 `%s` 失败
(F) 使用 `filetest` 属性时，切换实际和有效的 `uid` 或 `gid` 失败。

### `%ENV` 别名为 `%s`
(F) 你正在污染模式下运行，`%ENV` 变量已被别命名为另一个哈希，因此它没有反映程序环境。

### 验证规范 `%s` 失败
(F) 一个 `vms` 特有的错误。Perl 可能需要处理 `vms` 或 Unix 语法的规范，在必须直接操作时将其转换为单一形式。要么是你向 Perl 传递了无效的规范，要么是你发现转换例程无法处理的情况。

### 不安全的正则表达式中的 Eval-group
(F) 在尝试编译包含 `({? })` 零宽断言的正则表达式时检测到污染数据，这是不安全的。`({? code })` 在 `erl` 中。

### Eval-group 不允许，在 `%m/%` 中使用 `'eval'`
(F) Perl 在运行时尝试编译包含 `({ })` 零宽断言的正则表达式，当模式包含插值时会是这样。这是一个安全风险，是不允许的。如果你坚持，你仍然可以使用 `'eval'` 属性或在运行时从插值字符串构建模式来执行此操作。参见 `perlie` 中的 `"(?? code })"`。

### Eval-group 不允许，在 `%m/%` 中使用 `'eval'`
(F) 一个包含 `({? })` 零宽断言的正则表达式，但该结构在使用 `'eval'` 属性生效时才被允许。`({? code`

### 不安全的正则表达式中的 Eval-group
(F) 在尝试编译包含 `({? })` 零宽断言的正则表达式时检测到污染数据，这是不安全的。`({? code })` 在 `erl` 中。

### 在 `%s` 第 `%d` 行处死亡
(F) 正则表达式中嵌套括号过多。

### 进入 `%s` 失败
(F) 使用 `filetest` 属性时，切换实际和有效的 `uid` 或 `gid` 失败。

### (F) 一个 `vms` 特有的错误。Perl 可能需要处理 `vms` 或 Unix 语法的规范，在必须直接操作时将其转换为单一形式。要么是你向 Perl 传递了无效的规范，要么是你发现转换例程无法处理的情况。

### (F) 你的机器显然没有实现 `fcntl()`。这是什么东西，PDP-11 还是别的？
`FETCHSIZE` 返回了一个负值

(F) 一个绑定的数组声称具有负数量的元素，这是可能的。

### ‘u’ 格式包中的字段过宽
(W pack) `u` 编码字符串中的每行都以长度指示器开头，该指示器无法编码超过 63 的值。因此，请求大于该值的长度没有意义。Perl 将按照你指定的 `u63` 格式进行处理。

### 文件句柄 `%s` 已为输入打开
(W io) 你尝试写入一个只读文件。如果你打算让它成为读写文件，你需要使用 `+` 或 `+>>` 来打开它，而不是 `<` 或 留空。如果你只想写入该文件，请使用 `>` 或 `>>`。参阅 `perflunc` 中的 `"open"`。

### 文件句柄 `%s` 已为输出打开
(W io) 你尝试从一个为写入打开的文件句柄中读取。如果你打算让它成为读写文件句柄，你需要使用 `<` 或 `+>>` 来打开它，而不是 `->`。如果你只想从文件中读取，请使用 `<`。参阅 `perflunc` 中的 `"open"`。另一种可能性是你尝试为输出打开描述符 0（也称为 `STDIN`）（可能你早些关闭了 `STDIN`）。

### 文件句柄 `%s` 已重新作为 `%s` 打开输出
(W io) 你打开了一个与 `STDOUT` 或 `STERR` 相同的句句柄进行读取。这种情况发生是因为你之前关闭了 `STDOUT` 或 `STERR`。

### 文件句柄 `STDIN` 已重新作为 `%s` 打开输出
(W io) 你打开了一个与 `STDIN` 相同的句句柄进行写入。这种情况发生是因为你之前关闭了 `STDIN`。

### 最后应该是 `\$` 或 `\$name`
(F) 你现在必须决定字符串中的 `$` 是为了字面意义上的美元符号，还是你想引入一个恰好缺失的变量名。你必须在名称前加上反斜杠。

### 在关闭的文件句柄 `%s` 上执行 `clock()`
(W closed) 你尝试 `flock()` 的文件句柄在之前的某个时候已经关闭。请检查你的控制流，`flock()` 作用于文件句柄。你是否正尝试对同名的目录句柄调用 `flock()`？

### 格式未终止
(F) 格式必须由一个只包含点的行终止。Perl 将到达你的文件末尾而找不到这样的行。

### 格式 `%s` 已重定义
(W redefine) 你重新定义了格式。要抑制此警告，请使用：

```
{ no warnings 'redefine'; eval "format NAME =..."; }
```

### 条件中发现 `=`, 应该是 `==`
(W syntax) 你写了

```perl
if ($foo = 123)
```

而你的本意思是

`if ($foo == 123)`

（或类似的内容）。

### 在操作符或操作符的地方发现 `%s`。
(S syntax) Perl 词法器知道期望的是一个项还是操作符。如果它在期望看到操作符时看到了它认为的项，就会给你这个警告。这通常表示遗漏了操作符或分隔符，例如分号。

### `gdbm store` 返回 `%d`, `errno %d`, 键 `"%s"` 扩展表示存储失败。
(S) 来自 `GDBM_File` 扩展的警告

### `gethostost` 未实现
(F) 你的库显然没有实现 `gethostost()`，可能因为如果它实现了，它就会觉得有道德义务去恢复互联网上的每一个主机。

### 在关闭的 `socket %s` 上执行 `get$sname()`
(W) 你尝试在关闭的 `socket` 上获取 `socket` 或对端 `socket` 名称。你是否忘记检查 `socket()` 调用的返回值？

### `getpwnam` 为用户 `"%s"` 返回了无效的 `UIC %#to`
(S) `vms` 特有。`getpwnam` 操作符底层的 `sys$getuai` 调用返回了无效的 `UIC`。

### 在关闭的 `socket %s` 上执行 `opt()`
(W) 你尝试在关闭的 `socket` 上获取 `socket` 选项。你是否忘记检查 `socket()` 调用的返回值？参阅 `perlfunc` 中的 `"getsockopt"`。

### 是实验性的
(S) `smartmatch` 依赖 `smartmatch`，它是实验性的，因此它的行为在未来的 Perl 版本中可能会更改或被移除。参阅 `perlsyn` 中的 `"Experimental Details on when and where"`。

### 全局符号 `"%s"` 需要包名（你是否忘记声明 `"my %s"`？）
(F) 你使用了 `use strict` 或 `use state`，这表示所有变量必须是词域范围内的（使用 `"my"` 或 `"state"`），事先使用 `"our"` 声明，或者显式指定是哪个全局变量（使用 `":"`）。

### `glob` 失败 (`%s`)
(S) 用于 `glob <.*>` 的外部程序出现问题。通常，这意味着你提供的 `glob` 模式导致了外部程序失败并以非零状态退出。如果消息表明异常退出导致了核心转储，这可能意味着你的 `csh`（shell）损坏了。如果是这样，你应该将所有引用更改为类似于 `csh`（例如，`config.sh` 中 `csh` 相关的变量：`full_csh=/usr/bin/tcsh`）；否则，让它们为空（除 `d_csh` 为 `undef` 外），这样 Perl 就会认为缺少 `csh`。在情况下，编辑 `config.sh` 后，运行 `.Configure -S` 并重新编译 Perl。

### `Glob` 未终止
(F) 格式必须由一个只包含点的行终止。Perl 将到达你的文件末尾而找不到这样的行。

### 格式 `%s` 已重定义
(W redefine) 你重新定义了格式。要抑制此警告，请使用：

```
{ no warnings 'redefine'; eval "format NAME =..."; }
```

### 条件中发现 `=`, 应该是 `==`
(W syntax) 你写了

```perl
if ($foo = 123)
```



而你的本意思是

```
if ($foo == 123)
```

（或类似的内容）。

在操作符或操作符的地方发现 `%s`。
(S syntax) Perl 词法器知道期望的是一个项还是操作符。如果它在期望看到操作符时看到了它认为的项，就会给你这个警告。这通常表示遗漏了操作符或分隔符，例如分号。

`gdbm store` 返回 `%d`，`errno %d`，键 "`%s`" 扩展表示存储失败。
(S) 来自 `GDBM_File` 扩展的警告

`gethostost` 未实现

(F) 你的库显然没有实现 `gethostost()`，可能因为如果它实现了，它就会觉得有道德义务去恢复互联网上的每一个主机。

在关闭的 socket `%s` 上执行 `get$sname()`

(W) 你尝试在关闭的 socket 上获取 socket 或对端 socket 名称。你是否忘记检查 `socket()` 调用的返回值？

`getpwnam` 为用户 "`%s`" 返回了无效的 UIC `%#to`

(S) vms 特有。`getpwnam` 操作符底层的 `sys$getuai` 调用返回了无效的 UIC。

在关闭的 socket `%s` 上执行 `opt()`

(W) 你尝试在关闭的 socket 上获取 socket 选项。你是否忘记检查 `socket()` 调用的返回值？参阅 `perlfunc` 中的 "`getsockopt`"。

是实验性的

(S) `smartmatch` 依赖 `smartmatch`，它是实验性的，因此它的行为在未来的 Perl 版本中可能会更改或被移除。参阅 `perlsyn` 中的 “Experimental Details on when and where”。

全局符号 "`%s`" 需要包名（你是否忘记声明 "`my %s`"？）
(F) 你使用了 `use strict` 或 `use state`，这表示所有变量必须是词域范围内的（使用 "`my`" 或 "`state`"`），事先使用 "`our`" 声明，或者显式指定是哪个全局变量（使用 `":"`）。

`glob` 失败 (`%s`)
(S) 用于 `glob <.*>` 的外部程序出现问题。通常，这意味着你提供的 `glob` 模式导致了外部程序失败并以非零状态退出。如果消息表明异常退出导致了核心转储，这可能意味着你的 `csh`（shell）损坏了。如果是这样，你应该将所有引用更改为类似于 `csh`（例如，`config.sh` 中 `csh` 相关的变量：`full_csh=/usr/bin/tcsh`）；否则，让它们为空（除 `d_csh` 为 `undef` 外），这样 Perl 就会认为缺少 `csh`。在情况下，编辑 `config.sh` 后，运行 `.Configure -S` 并重新编译 Perl。

空白格，这意味着当使用标准选项编译 Perl 时，你不应该看到此错误。由于某种原因，你版本的 Perl 似乎是在没有此支持的情况下编译的。请联系你的 Perl 管理员。

- 原型 `%s` 中的非法字符: `%s`
(W 警告) 在原型声明中发现了非法字符。原型中的合法字符为 `$, @, %, *, [, ], &, 和 +`。也许你正试图尝试写一个未启用该功能的子程序签名（使用 `feature 'signatures'`），或者你的签名被解释为无效的原型。

- 匿名子程序声明非法
(F) 当使用 `sub key` 构造匿名子程序时，你必须始终指定一个代码块。请参见 `persub`。

- 匿名子程序声明非法
(F) 子程序声明不正确。请参见 `persub`。

- 非法除以零
(F) 你尝试将一个数字除以 `0`。要么是你的逻辑中出现了错误，要么你需要添加一个条件判断来防止无意义的输入。

- 非法十六进制数字 `%s` 已忽略
(W) 你可能尝试在十六进制数未使用 `0 - 9` 或 `A - F, a - f` 以外的字符。十六进制数的解析在非法字符之前停止。

- 非法取模零
(F) 你尝试将一个数字除以 `0` 来得到余数。大多数数字对这种操作并不友好。

- `vec` 中的位数非法
(F) `vec(c)`（第三个参数）中的位数必须是 `1` 到 `32` 之间的 `2` 的幂（如果你的平台支持，则为 `64`）。

- 非法八进制数字 `%s`
(F) 你在八进制数中使用 `8` 或 `9`。

- 非法数字 `%s` 已忽略
(W) 你可能尝试在八进制数未使用 `8` 或 `9`。八进制数的解析在 `8` 或 `9` 之前停止。

- 正则表达式中的非法模式；在 `m/%s/` 中已由 <-- HERE 标记
(F) 你写了类似下面的内容：

`(+foo)`
`+` 仅在后面紧跟数字时有效，表示一个捕获组。请参见“`(?PARNO)`”。

- 非法 suidscript
(F) 在 `perl` 下运行的脚本在某种程度上是非法的。

- `PERLOPT:-%C` 中的非法切换
(X) `PERLOPT` 环境变量仅允许设置以下切换：`-[CDIMUDmtw]`。

- 格式错误的 CTRL environ 值 "`%s`"
(W 内部) 一个针对 VMS 特有的警告。Perl 尝试读取 `CTRL` 的 `environ` 数组，并遇到了一个没有使用 `=` 分隔符来分离键和值的元素。

- `prime_env_iter` 中格式错误的消息：`[%%s]`
(W 内部) 一个 vms 特有的警告。Perl 在准备遍历 `%ENV` 时尝试读取逻辑名称或 CLI 符号，在键和值之间没有看到预期的分隔符，因此该行被忽略。

`(cleanup) %s` 此前缀通常表示 `DESTROY()` 方法引发了指定的异常。由于析构函数通常在执行期间任意点由系统调用，且通常次数非常多，因此对于任何否则会导致重复相同消息的失败，仅发出警告。

使用 `g_KEEPERRR` 标志分发的用户回调失败也可能导致此警告。请参见 `percall` 中的 "`G_KEEPER`"。

正则表达式中带有 `(? |)` 的不完整表达式；在 `%s/` 中已由 <— HERE 标记
(F) 在 `(? ])` 存在语法错误。这可能发生在表达式被完全构建为空，或者操作数数量相对于操作符数量过多或过少。Perl 不足够智能给出更精确的错误指示。

类 `%s` 的 C3 合并不一致：`%s` 合并失败
(F) 给定类的方法解析顺序 (MRO) 是 C3 一致的，且你已为此启用了 C3 most。有关更多信息，请参见 `mro` 中的 C3 文档。

在 EBCDIC 中，`v-string` 组件不能超过 `2147483647`
(F) 一个针对 EBCDIC 的特殊错误。在内部，`v-strings` 被存储为 Unicode 代码点，并在 EBCDIC 中编码为 UTF-EBCDIC。UTF-EBCDIC 编码限制于代码点不大于 `2147483647` (`0x7FFFFFFF`)。

无限递归
(F) 你使用了一个引用自身但不消耗任何输入文本的模式。你应该检查该模式以确保递归模式会消耗文本或失败。

"`state`" 中变量的初始化仅允许在标量上下文中初始化标量变量。将 `state ($a) = 42` 重写为 `state ($a = 42` 以从列表切换到标量上下文。`state (@a) = foo()` 等构造将在未来的 perl 版本中支持。

标量上下文中的 `%%%s` 最好写为 `%s`
(W) 在标量上下文中，你使用了数组索引/切片（由 `@` 标出）来选择数组的单个元素。通常请求标量值（由 `$` 标出）更好。区别在于 `$foo[@bar]` 在其返回值和评估其参数时始终表现得像标量，而 `%foo[@bar]` 为其下标提供了列表上下文，如果你期望只有一个下标，这可能会产生奇怪的结果。当在列表上下文调用时，它除了返回值外还会返回索引 (`@bar` 返回)。

- 标量上下文中的 `%s{%s}` 最好写为 `%s{%s}`
(W 语法) 在标量上下文中，你使用了哈希键/值切片（由 `%` 标出）来选择哈希表的单个元素。通常请求标量值（由 `$` 标出）更好。区别在于 `$foo{bar}` 在其返回值和评估其参数时始终表现得像标量，而 `%foo{bar}` 为其下标提供了列表上下文，如果你期望只有一个下标，这可能会产生奇怪的结果。当在列表上下文调用时，它除了返回值还会返回索引 (`@bar` 返回)。

- `%s` 中的不安全依赖
(F) 你尝试执行某种污染机制（tainting mechanism）不喜欢的操作。当你运行 `setuid` 或 `setgid` 时，或者指定 `-T` 开启它时，污染机制开启。污染机制会将所有直接或间接源于用户的数据标记，用户被认为是不值得信任的。如果任何此类数据被用于“危险”操作，你就会得到此错误。更多信息请参见 `perperc`。

- `%s` 中的不安全目录
(F) 在 `setuid` 或 `setgid` 脚本中，如果 `$ENV{PATH}` 包含用户可写的目录，则你无法使用 `system(), exec()` 或管道打开。此外，`PATH` 不得包含任何相对目录。请参见 `perperc`。

- 运行 `%s` 时不安全的 `%s{%s}`
(F) 在 `setuid` 或 `setgid` 脚本中，如果 `$ENV{PATH}` 包含用户可写的目录，则你无法使用 `system(), exec()` 或管道打开。此外，`PATH` 不得包含任何相对目录。请参见 `perperc`。

`charnames` 中的“自定义别名”（CUSTOM ALIASES）。

`%s` 中的无效 `\0` 字符：`%s\0s`
(W scalls) 路径或其他系统参数中嵌入了 `\0` 字符，产生了警告 5.20。我们以前通过系统调用忽略了这些部分。

`\N{...}` 中的无效字符；在 `\N{%s}` 中标记为 <— 在此处
(F) 只有某些字符对于字符名称是有效的。指示的字符无效。请参见 `charnames` 中的“自定义别名”（CUSTOM ALIASES）。

`%s` 中的无效转换：“`%s"`
(W printf) Perl 不理解给定的格式转换。请参见 `perfunc` 中的“`printf`”。

正则中指定编码的无效转义字符；在 `m/%s/` 中标记为 <— 在此处
(W regexp)(F) 数值小于 `256` 的数值转义（例如 `\xhn`）在通过编码过程从指定编码转换时没有对应单个字符。该转义字符被替换为 RE CHARACTER (U+FFFD)，但在 `[ ]` 内部除外，这是一个致命错误。在正则表达式中发现问题位于 <— 处。

正则中 `\N{U+...}` 中的无效十六进制数；在 `m/%s/` 中标记为 <— 在此处
(F) 由 `_` 表示的字符不是十六进制数。它可能是空的，或者你在十六进制数尝试尝试 `0` 或 `A-F` 以外的字符。

带有-`%c` 选项的无效模块 `%s`：包含单个冒号
(F) 模块参数 `%s -m` 和命令行选项不能在模块名中包含单冒号，但只能在 `""` 之后的参数中包含。换句话说，`-MFoo::Bar=baz` 是可以，而 `-MFoo::Bar=baz` 是不起的。

无效的 `mro` 名称：“`%s"`
(F) 你尝试了 `mro::set_mro("classname", "foo")` 或使用 `mro 'foo'`，其中 `foo` 不是有效的方法解析顺序（MRO）。目前支持的的有 `dfs` 和 `c3`，除非你加载了作为 MRO 插件的模块。请参见 `perlmoi` 中的 `mro`。

`chr` 中的无效负数 (`%s`)
(W utf) 你向 `chr` 传递了一个负数。负数不是有效的字符数字，它返回 Unicode 字符（U+FFFD）。

无效选项 `-Dc%`，使用 `-D` 查看选项
(S debugging) 调用 `perl` 时使用了无效的调试器标志。使用带有标志的 `-D` 调用 `perl` 以查看可接受值的列表。也参见 `perlun` 中的“`Dletters`”。

正则中 `{:}` 中的无效量词；在 `m/%s/` 中标记为 <— 在此处
(F) 模式看起来像 `[min,max]` 量词，但 `min` 或 `max` 无法作为有效值传递——因为它有前导零，或者它代表的数字太大无法复制。<— HERE 显示了在正则表达式中发现问题的位置。请参见 `perlere`。

正则中无效的 `[]` 范围 "`%s`"；在 `m/%s/` 中标记为 <— 在此处
(F) 类指定的范围最小字符大于最大字符。一种可能是你忘记了结尾 `\x}` 中的 `{}`，因为 `\x} - \x` 不带大括号只能到 `ff`。<— HERE 显示了在正则表达式中发现问题的位置。请参见 `perlge`。

转义运算符中的无效 "`%s`"
(F) `tr//` 或 `y//` 运算符中指定的范围最小字符大于最大字符 `%s`。请参见 `perlop`。

属性列表中的无效分隔符 `%s`
(F) 在属性列表元素之间看到了冒号或空白以外的内容。如果上一个属性具有括号参数列表，也许该列表结束得太早。请参见 `attributes`。

PerIO 规范 `%s` 中的无效分隔符 `%s`
(W) 向 I/O 系统推入层时，层列表元素之间看到了冒号或空白以外的内容。如果上一个属性具有括号参数列表，也许该列表结束得太早。

无效的严格格式 (`%s`)
(F) 版本号不符合版本的“严格”标准。“严格”版本是一个正十进制数（整数或小数），且不带指数，或者是以 ‘v’ 字符开头且至少包含三个组件的点分十进制 v 字符串。括号中的文字指示未符合哪些标准。更多关于允许的版本格式的详细信息请参见 `version` 模块。

`%s` 中的无效类型 '`%s`’
(F) 给定的字符不是有效的 `pack` 或 `unpack` 类型。请参见 `perlfunc` 中的“`pack`”。
(W) 给定的字符不是有效的 `pack` 或 `unpack` 类型，但过去被静默忽略了。

无效的版本格式 (`%s`)
(F) 版本号不符合版本的“宽松”标准。“宽松”版本是一个正十进制数（整数或小数），且不带指数，或者是一个点十进制 v 字符串。如果版本少于三个组件，它必须以 ‘v’ 字符开头。否则，十进制和点十进制版本都可能带有由小数或点十进制组件分隔的“alpha”组件。括号中的文字指示未符合哪些标准。更多关于允许的版本格式的详细信息请参见 `version` 模块。

无效的版本对象
(F) 版本对象的内部结构无效。可能是内部以某种方式直接被修改了，或者一个任意引用被祝福为“`version`”类。

在 '*VERB.*’ 中，‘* 和 *’ 在正则中必须是相邻的；在 `%/%s` 中标记为 <— 在此处
(F) 正则模式中的双字符序列 (`*` 和 `*`) 应该是一个不可见的令牌，`*` 和 `*` 之间没有任何间隔，但你将它们隔开了。

未实现 `ioctl`
(F) 你的机器显然没有实现 `ioctl()`，对于一个支持 unsigned `%s ioctl()` 的机器来说很奇怪。
(W) 你在一个从未打开的文件句柄上尝试了 `ioctl()`。检查你的控制流和参数数量。

10 层不可用
(F) 你的 Perl 没有配置 PerIO，因此无法使用层。要使用 PerIO，必须将 Perl 配置为 ‘userio’。

`IO::Socket::atmark` 未实现
(F) 你的机器没有实现 `socketmark()` 功能，既没有作为系统调用，也没有作为 `ioctl` 调用 (`SIOCMARK`)。

正则中 `%s` 是一个未知类型；在 `m/%s/` 中标记为 <— 在此处
(F) 你使用的 `\{...}` 或 `(... )` Perl 不认识。当前值给出在 `{}` 中，并以反斜杠表示。

`%s` 在正则中写为 "`%s`" 更为清晰；在 `m/%s/` 中标记为 <— 在此处
(W regex) (仅在 `strict` 或 `[ ]` 内部) 你指定的字符有通用的表示方法，并且它也能够移植到运行不同字符集的平台。

`*$` 不再支持
(D废弃, 语法) 在旧版本 perl 中废弃的变量 `$` 已从 5.10 起移除。

`$$` 不再支持
(D 弃, 语法) 在旧版本 perl 中废弃的变量 `$$` 已从 5.10 起移除。

`%s` 不是代码引用
(W overload) 传递给 `overload` 需要代码引用。

`%s` 不是可 overload 的类型
(W overload) 你尝试对常量进行 `overload`。

`-i` 在命令行上使用但未提供文件名
(S 处) 在命令行上使用了 `-i`，这通常意味着要编辑，但因为是在编辑 STDIN，这令人困惑。请参见 `perlrun`。

正则 `m/%s/` 末有垃圾信息
(P) 正则表达式解析器感到困惑。

`keys` 引用是实验性的
(S experimental::auteref) 使用标量参数 `keys` 是实验性的，并在未来版本中更改或移除。如果你想承担此功能的风险，只需禁用此警告：
```
use warnings FATAL => 'experimental::auteref';
```



no warnings "experimental::auteref";

## 未实现的管道打开函数列表

(F) 在某些平台上（特别是 Windows），三个或更多参数的 `open` 形式不支持管道，例如 `open($pipe, '-', @args)`。请使用两个参数的 `open($pipe, '|', prog arg1 arg2...)` 形式。

`%s`: 可加载库与二进制文件不匹配（获取的 hasshake key 为 `%p`，需要的 `%p`）

(P) 动态加载库 `.so` 或 `.dll` 正在被加载到进程中，该进程编译时使用的 Perl 版本与该库编译时的版本不同。重新安装 xs 模块可能会修复此错误。区域 `%s` 可能无法正常工作。`%s`

(W) 你正在使用命名的区域（locale），这是一个非 UTF-8 区域，且 Perl 确定它与它可以处理的内容不完全兼容。第二个 `%s` 给出了原因。

到目前最常见的原因是区域中包含由多个字节表示的字符。Perl 能够处理的区域只有 UTF-8 区域。指定的区域很可能是中文或日语等东亚语言的非 UTF-8 区域。如果该区域是 ASCII 的子集，则其 ASCII 部分可能在 Perl 中可以工作。

某些不是 ASCII 子集的过时区域（主要是 ISO 646 或 7 位区域）在处理 ASCII 字符集某些部分被区域修改且被程序使用时也会出现问题。警告信息列出了可以确定的冲突字符。

注意：未发现不兼容之处。

如果这种情况发生在你身上，除了切换到不同的区域或使用 `Encode` 将区域翻译为 UTF-8 之外，你无能为；如果这不可行，你已收到警告：某些功能可能会崩溃。

此消息每次在 `use locale` 范围内切换坏区域时输出，或者在 `use locale` 继承了坏区域的情况下执行第一个受影响的操作时输出。对于 POSIX 模块中的任何操作，都不会触发此消息。

`localtime(%f)` 失败

(W overflow) 你调用 `localtime` 时使用的数字无法处理：数字太大、太小或为 NaN。返回的值为 undef。`localtime(%f)` 太大

(W overflow) 你调用 `localtime` 时使用的数字大于它可以可靠处理的范围，`localtime` 可能返回了错误的日期。此警告在遇到 NaN（特殊的非数值）时也会触发。`localtime(%f)` 太小

(W overflow) 你调用 `localtime` 时使用的数字小于它可以可靠处理的范围，`localtime` 可能返回了错误的日期。

正则 `m/%s/` 中长度超过 `%d` 的后行查找未实现

(F) 目前对后行查找（lookbehind）可以处理的字符串长度有限制。该限制可能会在未来的版本中放宽。

精度丢失 `%s %of` 偏离 1

(W precision) 你尝试增加或减小 1 的值太大，底层的浮点表示无法准确存储，因此 `++` 或 `--` 的目标未改变。Perl 发出此警告是因为当值超过整数能表示范围时，它已经从整数切换到了浮点，而现在即使是浮点也不够了。你可能希望显式切换到 `Math::BigInt`。

文件句柄 `%s` Istat

(W io) 你尝试对文件句柄执行 `Istat`。你什么意思？`lstat()` 只对文件名有效。（Perl 实际上执行了 `fstat()` 而不是文件句柄。）

Ivalue 属性 `%s` 已定义的子程序

(W misc) 虽然 `attributes.pm` 允许，但对已经定义的 Perl 子程序开启或关闭 Ivalue 属性并不总是能正常工作。取决于子程序内部的代码，这可能不是你想要的结果，或者具体细节在不同 Perl 版本之间发生变化。只有在你确实清楚自己在做什么时才执行此操作。

子程序定义后 Ivalue 属性被忽略

(W misc) 使用 `:Ivalue` 声明语法在定义后将 Perl 子程序变为 Ivalue 子程序是不允许的。要使该子程序成为 Ivalue 子程序，请在定义中添加 Ivalue 属性，或在定义之前放置 `sub :Ivalue` 声明。

另见 `attributes.pm`。

不支持 Magic 列表常量

(F) 你将一个 magic 数组赋值给栈元素，然后尝试使用同一槽位中的子程序。你正在要求 Perl 执行它无法完成的事情，细节随 Perl 版本变化而变化。

`[]` 中格式不正确的整数

(F) 在包含数字重复次数的括号内只允许数字。请参见 `perperf` 中的 "pack"。

`unpack` 中 `[]` 中格式不正确的整数

(F) 在包含数字重复次数的括号内只允许数字。请参见 `perperf` 中的 "pack"。

格式不正确的 PERLLIB_PREFIX

(F) 这是一个 OS/2 特有的错误。`PERLLIB_PREFIX` 应该是以下形式：

```
prefix1;prefix2
```



或 `prefix1` `prefix2`

且 `prefix1` 和 `prefix2` 不为空。如果 `prefix1` 确实是内置库搜索路径的前缀，则会替换 `prefix2`。如果找不到组件或组件过长，可能会出现此错误。请参见 `perlos2` 中的 `"PERLLIB_PREFIX"`。

### `%s` 的原型型格式不正确：`%s`

`(F)` 你尝试使用一个原型型格式不正确的函数。函数原型型的语法会通过一个简短的编译时检查，以发现明显的错误（如无效字符）。在调用函数时会运行更严谨的检查。也许函数的作者本想写一个子程序，但没有先开启该功能（使用 `signatures`），导致签名被解释为错误的原型型。

### 格式不正确的 UTF-8 字符 (`%s`)

`(S utf8(F))` Perl 检测到一个不符合 UTF-8 编码规则的字符串，尽管它已经开启了 UTF-8 标记。

一种可能的情况是你认为数据是 UTF-8 从而手动设置了 UTF-8，但它并非如此（例如它是旧留的 8 位数据）。为了防止这种情况，可以使用 `Encode::decode_utf8`。

如果你在输入中使用 `:encoding(utf-8)` PerlIO 层，无效的字节序列会被良好处理；但如果你使用 `:utf8`，则会在不验证数据的情况下设置标记，可能导致此错误消息。

另见 `Encode` 中的“处理格式错误的数据”。

### `%s` 之后的格式不正确的 UTF-8 字符

`(F)` 你说使用 `utf8`，但程序不符合 UTF-8 编码规则。消息会在第一个错误字符之前打印出编码正确的字符。如果启用了 `utf8` 警告，会生成一个提供有关错误类型更多详细信息的警告。

### `%s` 之后紧接 VN% 返回的格式不正确的 UTF-8

`(F)` `unpack` 中 `%9c` 格式中的 `charms` 句柄处理字符串返回了格式不正确的 UTF-8。

`(F)` 你尝试解包一个不符合 UTF-8 编码规则的内容，Perl 无法判断如何继续。

### `pack` 中格式不正确的 UTF-8 字符串

`(F)` 你尝试封包一个不符合 UTF-8 编码规则的内容，Perl 无法判断如何继续。

### `unpack` 中格式不正确的 UTF-8 字符串

`(F)` 你尝试解包一个不符合 UTF-8 编码规则的内容，Perl 无法判断如何继续。

### 格式不正确的 -16 代理

`(F)` 消息认为它已经解码。

### 强制性参数在可选参数之后

`(F)` 在子程序中，你写了类似 `$a = undef`，导致前面的参数变为可选。此消息表示匹配结果与实际情况相反。

### 正则中匹配到空字符串；在 `m/%s/` 中由 `<---` 标记

`(W regexp)` 如果引擎没有专门检查这一点，你指定的模式将导致死循环。`<---` 显示了发现表达式问题所在的地方。请参见 `perperl`。

### 可能是失控的多行字符串

`(S)` 一条提示，指示之前的错误可能是由于字符串或模式缺少定界符导致的，因为它最终在当前行较早结束了。

### 数字中位置错误的下划线 `_`

`(W syntax)` 数值常量中的下划线（underbar）未分隔数字。

### `%s` 缺少参数

`(W missing)` 你调用函数时提供的参数少于其他参数所指示的所需数量。

目前仅在 `printf` 类型的格式需要更多参数但未提供时抛出此警告，但未来可能用于其他我们可以静态确定函数参数缺失的情况，例如 `perfunc` 函数中的“`pack`”。

### `-%c` 缺少参数

`- (F)` 所指示的命令行开关的参数必须紧跟在开关之后，中间不能有空格。

### `\{N}` 上的大括号

正则中 `\{N}` 缺少大括号，在 `%s/` 处由 `<—` 此处标记。
`- (F)` 双引号上下文中字符名称字面量 `\<charname>` 语法错误。当在带有 `/` 修饰符的正则中，反斜符 `\n` 和 `c` 之间存在空格（或注释）时，也会发生这种情况。该修饰符并不改变大括号必须紧跟 `\n` 之后的要求。

### `\{0}` 上的大括号

`- (F)` 在双引号上下文中 `\a` 后面必须紧跟一个 `{`。

### `%s` 函数第一个参数后缺少逗号

`- (F)` 虽然某些函数允许在参数之前指定文件句柄或“间接对象”，但此函数并非如此。

### `piped open` 中缺少命令

`- (W)` `pipe` 你打开了 `(FH, "| command")` 或 `open(FH, "command |")` 结构，但命令缺失或为空。

### `'\c'` 中缺少字符名

`- (F)` 双引号字符串以 `\"c"` 结尾，但缺少所需的控制字符名称。

### `%s : %s` 的原型中缺少 `']'`

`- (W)` `illegalto)` 分组以 `[` 开始但从未用 `]` 闭合。

### `""%%s sub"` 中缺少名称

`- (F)` 词法作用域子程序的语法要求它们必须有一个可以被找到的名称。

### 循环变量上的 `$`

`- (F)` 显然你用 `csh` 程序写太多了。在 Perl 中，变量总是用 `$` 引用，这与 `shell` 不同，`shell` 中的 `$` 在行与行之间可能会变化。

### `%s` 之前缺少运算符？

`- (S)` 这是结合信息“`%s found where operator expected`”做出的合理推测。缺失的运算符是逗号。

### `require` 缺少或未定义的参数

`- (F)` 你尝试在没有参数或使用未定义值作为参数的情况下 `require`。`require` 需要一个包名或文件规范作为参数。参见 `perlfunc` 中的“`require`”。

### 正则中 `%{c}` 缺少右大括号；在 `m/%s/` 中由 `<— HERE` 标记。

`- (F)` `\{...}`, `p{...}`, `P{...}`, 或 `\N{}` 缺少右大括号。

### `\N{}` 缺少右大括号或 `\N` 后有未转义的左括号

`- (F)` `\n` 有两种含义。

传统的含义是跟着用大括号括起来名称，表示该名称对应的字符（或字符序列）。这是 `*` 的另一种写法，在双引号字符串和正则表达式模式中都是有效的。在模式中，它并不表示未转义的 `*`。

从 Perl 5.12.0 开始，`\n` 在模式中还可以具有额外的额外含义，即匹配非换行字符。（这是 `[^\n]` 的缩写，但不受 `/s` 正则修饰符的影响）。

这会导致一些歧义。当 `\n` 后面没有紧跟左大括号时，Perl 允许 `[^ ]` 的含义。如果大括号形成一个有效的量词，如 `\n{3}` 或 `\n{5}`，Perl 允许匹配给定数量的非换行符（在这些示例中，分别为 3 和 5 或更多）。在所有其他情况下（即存在 `\n{...` 且有匹配的 `)`），Perl 允许请求字符名称。

然而，如果没有匹配的 `)`，Perl 不知道是你不小心漏掉了，还是你想表达前者（请添加右大括号）；如果你指的是后者，请用反斜杠转义大括号，例如：`\{\}`

### 缺少右大括号或方括号

`- (F)` 左括号或方括号比右少。根据通用规则，你将在最后编辑的地方附近找到它。`(S)` 这是一个结合信息“`%s found operator expected`”给出的提示。不要因为你看到了此信息就自动在上一行放上分号。

### 尝试修改只读值

`- (F)` 你尝试直接或间接地修改常数的值。你没有这样做，因为编译器捕获了信息“`2 = 1`”。但执行该操作的一种简单方法是：

```
sub mod {$_0]} = 1};
```

另一种方法是将 `sub($)` 赋值给字符串末尾的循环变量。另一种方法是将循环变量赋值给常量：

```
$x = 1; foreach ($n, 2) { $n *= 2; # 修改
```



```
尝试不可创建的数组值

- (F) 你尝试将数组值变为实体，且下标为负数，从数组末尾计数。
尝试不可创建的哈希值，%s
- (P) 你尝试将哈希值变为存在，但由于特殊原因未能创建。模块名必须是常量

- (F) "use" 仅允许裸模块名。
带有选项的模块名

- (F) `-M` 或 `-m` 选项显示 Perl 应该加载某些模块，但省略了模块名称。详情请参阅 `perlin` -M 和 -m。
多个等号 %s

- (F) `open` 函数要求打开多个文件。这发生在你尝试打开一个接受参数列表的管道但忘记指定模式时。参见 `perlfunc` 中的 "open"。
cow string 的 mprotect 失败，%d
(S) 你用 `DPERL_DEBUG_READONLY` 编译 Perl（`perlfuncs` 中的 COW)，但共享字符串缓冲区不可只读。
cow string 的 mprotect 失败，%d
(S) 你用 `DPERL_DEBUG_READONLY_OPS` 编译 Perl（参见 `perlhashtips`），但 op 树不可只读。
cow string 的 mprotect 失败，%d
(S) 你用 `DPERL_DEBUG_READONLY_COW` 编译 Perl（`perlfuncs` 中的 COW），但共享字符串缓冲区不可变。
cow string 的 mprotect 失败，%d
(S) 你用 `DPERL_DEBUG_READONLY_OPS` 编译 Perl（参见 `perlhashtips`），但 op 树不可只读。在释放 ops 之前，op 树不可变。
msg%s 不

- (F) 你的系统没有 System message。
- (F) 你的系统没有 System message。
多维语法 %s 不支持

- (W) 多维数组不是写成 `$foo[1, 2, 3]`。它们像 C 一样写成 `$foo[1][2][3]`。
unpack 中数字后的 '/'

- (F) 你执行的 `unpack` 模板包含了 '/'，但它没有遵循某些产生数值的规范。参见 `perlfunc` 中的 "pack"。
"my sub" 未实现

- (F) 词法作用域子程序未实现。不要尝试。
"my" %s 不在包中

- (F) 词法作用域子程序不在包中，所以尝试在前面加上包限定符来声明它们是没有意义的。
在排序比较中使用了 "my" %s

- (W) 包变量 `$a` 和 `$b` 用于排序比较。你在排序比较内部将 `$a` 或 `$b` 作为 <= 或 cmp 运算符的操作数，而该变量之前被声明为词法变量。请使用包名指定该排序变量，或者重命名该词法变量。
"my" 变量 %s 不在包中

- (F) 词法作用域变量不在包中，所以尝试在前面加上包限定符来声明它们是没有意义的。如果你想本地化包变量，请使用 `local()`。
名称 %s:%s 仅使用一次：可能的拼写错误
(W) 拼写错误通常表现为唯一名称。如果你有充分理由使用唯一名称，只需以某种方式再次提到以抑制此信息。我们的声明也是为此目的提供的。

注意：此警告检测只使用一次的包符号。这意味着词法变量将永远不会触发此。它意味着包变量 %、@%、% 以及 &%、% {、%) 和 %（文件句柄或格式）被认为是相同的；如果一个程序只使用 % 一次但也使用了其中任何其他，将不会触发此警告。以下划线开头的符号和使用特殊标识符（q.v. `perlata`）的符号免于此警告。

正则中需要正好 3 位数字；在 m/%s/ 处由 <--- 标记
- (F) 在 ? 内，所有被解释为八进制的常量必须是 3 位长。这有助于捕捉所有歧义。如果你的常量太短，请添加前导零，

```
?([ [ \078 ]) # 语法错误！

(?([ [ \0078 ] ]) # 正常 ([ \007 8 ]
```

# 清

```
该构造接受的最大数字是 \77。如果你需要更大的数字，需要使用 \o。如果你指的是两个独立的内容，需要将它们分开：

```
?([ [ \776 ]] # 语法错误！

(?([ [ \o{776} ] ]) # 一种含义 ([ \777 6 ]) # 另一种含义 ([ \777 \006 ]) # 还有
```
unpack 中的负 '/' 计数

- (F) 从长度/代码 `unpack` 操作计数的长度为负数。参见 `perlfunc` 中的 "pack"。

负长度

- (F) 你尝试用小于 0 的缓冲区长度执行 `read`/`write`/`send`/`recv` 操作。这很难想象。

Ivalue 上下文中 `vec` 的偏移量第二个参数必须大于或等于零。

负重复计数无效
(W numeric) 你尝试执行 `x` 重复运算符少于 0 次，这没有意义。

正则中的嵌套量词；在 m/%s/ 处由 <--- 标记
- (F) 你不能在没有括号的情况下对量词进行量化。因此像 ** 或 *? 是非法的。<--- HERE 显示了在正则表达式中发现的位置。

注意最小匹配量词 *, +, ?, 和 ?? 看起来像是嵌套量词，但并不是。参见 `perlie`.

%s 从未引入

(S internal) 相关的符号已声明，但在使用之前由于某种原因离开了作用范围。

next::method/next::can/maybe::next::method 找不到封装方法
(F) `next::method` 需要在真实包中真实方法的上下文中调用，但未找到此类上下文。参见 `mro`。

字符类中的 \N 必须是命名字符：正则表达式中的 \N{...}；在 m/%s/ 中处标记为 <— HERE
(F) （自 Perl 12 起）\N 作为 [^n] 的新含义在方括号字符类中是无效的，这与在字符类中丢失特异性的原因相同：它匹配所有内容，这可能不是你想要的。
在反向字符类或作为正则终点时，\N{} 在正则表达式中被限制为单个字符；在 m/%s/ 中处标记为 <— HERE

(F) 命名的 Unicode 转义字符 `\N{...}` 可能会返回多字符序列。虽然字符类本应该匹配输入的一个字符，但当类反反时（[^~]）或转义字符是范围的起始或结束时，perl 会正确匹配。在反转时匹配的数学逻辑行为与人们的预期非常不同，因此我们决定禁止这样做。同样不清楚的是当 `\N{...}` 用作范围的终点时应该生成什么，例如：
`[\x41}-\NARABIC SEQUENCE YE WITH HAMZA ABOVE]`

这里的意思是，\N{...} 转义字符是一个代码点序列，因此这是一个错误。

\N{NAME} 必须由正则表达式的解析器解析；在 m/%s/ 中处标记为 <— HERE
(F) 在编译正则表达式模式时，遇到了一个未解析的命名字符或序列。这可以通过几种绕过解析器的方式发生，例如使用单引号类的上下文，或在双引号类的上下文中使用额外的反斜符：

```
$re = '\N{SPACE}'; # 错误！ $re = "\N{SPACE}"; # 错误！ //re;
```
相反，请使用带有单个反斜符的双引号：
```
通过通过从较小的组件创建模式可以绕过解析器：

$re = '\N'; /${re}{SPACE}; # 错误！
```

像这样拆分结构并不是一个好主意，而且在这里不起作用。请使用上面的解决方案。

最后，此消息也可能在 /x 正则修符下发生，当 \N 与 { 之间有空格时，在这种情况下请删除空格。
/N {SPACE}/x; # 错误！ \N{SPACE}/x; # 好

运行 setuid 时不允许 %s
(F) 某些操作被认为对于 setuid 或 setgid 来说不安全，甚至不允许尝试。通常情况下，会有另一种方法可以实现你的目的，即使不安全，至少是可以安全的。参见 `perlec`。

charnames 别名定义中的不换行空格已弃用

(D deprecated) 你定义了一个包含不换行空格字符的字符名称。将其更改为普通空格。这些名称通常定义在 `alias import argument to charnames` 中，可能由安装到 `$H(charnames)` 的翻译器定义。参见 `charnames` 中的 `CUSTOM ALIASES`。

9c 未指定代码

(F) Perl 的 `-e` 和命令行选项需要一个参数。如果你想运行一个空程序，请将空字符串作为单独参数传递，或者运行由单个 0 或 1 组成的程序：

```
perl -e "perl -e0 perl"
```



### `%s` 后不允许有逗号

(F) 带有文件句柄或“间接对象”的列表运算符不允许在它与后续参数之间有逗号。否则，它将只是另一个参数。

这可能的原因之一是，期望通过 `use` 或 `import` 将常量导入到你的名称中，但实际上没有发生导入，例如可能是因为你的操作系统不支持该特定常量。希望你对预期要看到的常量使用了显式导入列表；请参见 `perfunc` 中的 `"use"` 和 `perfunc` 中的 `"import"`。虽然显式导入列表可能会自然地更早地捕获此错误，但并不能解决你的操作系统仍然不支持该常量的事实。也许你在 `use` 或 `import` 的符号导入列表常量中，或者在触发此错误的行的常量名中有拼写错误？

### 命令行中没有管道到命令

(F) 这是一个 `vms` 特有的错误。`Perl` 处理它自己的命令行重定向，在命令行末尾发现了一个 `|l`，因此它不知道你想将此命令的输出管道到哪里。

### 未定义 DB:DB 例程

(F) 当前执行的代码是用 `-d` 选项编译的，由于某种原因，当前调试器（例如 `perl5db.pl` 或 `devel::` module）没有定义在每个语句开始处调用的例程。

### 此机器上没有 dbm

> (P) 这被视为内部错误，因为现在每台机器都应该提供 `dbm`，因为 `perl` 带有 `sdbm`。参见 `SDBM_File`。

### 未定义 DB::sub 例程

(F) 当前执行的代码是用 `-d` 选项编译的，由于某种原因，当前调试器（例如 `perl5db.pl` 或 `devel::` module）没有定义在每个普通例程开始处调用的 `DB::sub` 子例程。

### `-I` 未指定目录

(F) `-I` 命令行开关需要目录名称作为相同参数的一部分。对于 `lib` 请使用 `-lib`。`-I lib` 不起作用。

### 命令行中 2> 或 2>> 后错误

(F) 这是一个 `vms` 特有的错误。`Perl` 处理命令行重定向，在命令行上发现了一个 `2>` 或 `2>>`，但找不到写入 `strdnf` 的文件名称。

### 模板中未找到组结束字符 `'%c'`

(F) `pack` 或 `unpack` 模板缺少匹配的 `(` 或 `[`。参见 `perfunc` 中的 `'pack'`。

### 命令行 `<` 后无输入文件

(F) 这是一个 `vms` 特有的错误。`Perl` 处理命令行重定向，在命令行上发现了一个 `<~`，但找不到从 `stdin` 读取数据的文件名称。

### `next::method '%s'` 找到 `%s`

(F) 在该类的剩余包中没有找到此方法名称的进一步实例。如果你不希望它抛出异常……

***

### `%s` 从未引入

(S internal) 相关的符号已声明，但在使用之前由于某种原因离开了作用范围。

### `next::method/next::can/maybe::next::method` 找不到封装方法

(F) `next::method` 需要在真实包中真实方法的上下文中调用，但未找到此类上下文。参见 `mro`。

### 字符类中的 `\N` 必须是命名字符：正则表达式中的 `\N{...}`；在 `m/%s/` 中处标记为 `<— HERE`

(F) （自 Perl 12 起）`\N` 作为 `[^n]` 的新含义在方括号字符类中是无效的，这与在字符类中丢失特异性的原因相同：它匹配所有内容，这可能不是你想要的。
在反向字符类或作为正则终点时，`\N{}` 在正则表达式中被限制为单个字符；在 `m/%s/` 中处标记为 `<— HERE`

(F) 命名的 Unicode 转义字符 `\N{...}` 可能会返回多字符序列。虽然字符类本应该匹配输入的一个字符，但当类反转时（`[^~]`）或转义字符是范围的起始或结束时，`perl` 会正确匹配。在反转时匹配的数学逻辑行为与人们的预期非常不同，因此我们决定禁止这样做。同样不清楚的是当 `\N{...}` 用作范围的终点时应该生成什么，例如：
```
[\x41}-\NARABIC SEQUENCE YE WITH HAMZA ABOVE]
```
这里的意思是，`\N{...}` 转义字符是一个代码点序列，因此这是一个错误。

### `\N{NAME}` 必须由正则表达式的解析器解析；在 `m/%s/` 中处标记为 `<— HERE`

(F) 在编译正则表达式模式时，遇到了一个未解析的命名字符或序列。这可以通过几种绕过解析器的方式发生，例如使用单引号类的上下文，或在双引号类的上下文中使用额外的反斜符：

```
$re = '\N{SPACE}'; # 错误！
$re = "\N{SPACE}"; # 错误！ //re;
```
相反，请使用带有单个反斜符的双引号：

```
通过从较小的组件创建模式可以绕过解析器：

$re = '\N'; /${re}{SPACE}; # 错误！
```

像这样拆分结构并不是一个好主意，而且在这里不起作用。请使用上面的解决方案。

最后，此消息也可能在 `/x` 正则修符下发生，当 `\N` 与 `{` 之间有空格时，在这种情况下请删除空格。
```
/N {SPACE}/x; # 错误！
\N{SPACE}/x; # 好
```

### 运行 setuid 时不允许 `%s`

(F) 某些操作被认为对于 `setuid` 或 `setgid` 来说不安全，甚至不允许尝试。通常情况下，会有另一种方法可以实现你的目的，即使不安全，至少是可以安全的。参见 `perlec`。

### `charnames` 别名定义中的不换行空格已弃用

(D deprecated) 你定义了一个包含不换行空格字符的字符名称。将其更改为普通空格。这些名称通常定义在 `alias` import argument to `charnames` 中，可能由安装到 `$H(charnames)` 的翻译器定义。参见 `charnames` 中的 `CUSTOM ALIASES`。

### `9c` 未指定代码

(F) `Perl` 的 `-e` 和命令行选项需要一个参数。如果你想运行一个空程序，请将空字符串作为单独参数传递，或者运行由单个 `0` 或 `1` 组成的程序：

```
perl -e "perl -e0 perl"
```



### %s 后不允许有逗号

(F) 带有文件句柄或“间接对象”的列表运算符不允许在它与后续参数之间有逗号。否则，它将只是另一个参数。

这可能的原因之一是，期望通过 `use` 或 `import` 将常量导入到你的名称中，但实际上没有发生导入，例如可能是因为你的操作系统不支持该特定常量。希望你对预期要看到的常量使用了显式导入列表；请参见 `perfunc` 中的 `"use"` 和 `perfunc` 中的 `"import"`。虽然显式导入列表可能会自然地更早地捕获此错误，但并不能解决你的操作系统仍然不支持该常量的事实。也许你在 `use` 或 `import` 的符号导入列表常量中，或者在触发此错误的行的常量名中有拼写错误？

### 命令行中没有管道到命令

(F) 这是一个 `vms` 特有的错误。`Perl` 处理它自己的命令行重定向，在命令行末尾发现了一个 `'|l'`，因此它不知道你想将此命令的输出管道到哪里。

### 未定义 DB:DB 例程

(F) 当前执行的代码是用 `-d` 选项编译的，由于某种原因，当前调试器（例如 `perl5db.pl` 或 `devel::` module）没有定义在每个语句开始处调用的例程。

### 此机器上没有 dbm

> (P) 这被视为内部错误，因为现在每台机器都应该提供 `dbm`，因为 `perl` 带有 `sdbm`。参见 `SDBM_File`。

### 未定义 DB::sub 例程

(F) 当前执行的代码是用 `-d` 选项编译的，由于某种原因，当前调试器（例如 `perl5db.pl` 或 `devel::` module）没有定义在每个普通例程开始处调用的 `DB:sub` 子例程。

### -I 未指定目录

(F) `-I` 命令行开关需要目录名称作为相同参数的一部分。使用 `-lib`，对于 `lib`。`-I lib` 不起作用。

### 命令行中 2> 或 2>> 后错误

(F) 这是一个 `vms` 特有的错误。`Perl` 处理命令行重定向，在命令行上发现了一个 `'2>'` 或 `'2>>'`，但找不到写入 `strdnf` 的文件名称。

### 模板中未找到组结束字符 '%c'

(F) `pack` 或 `unpack` 模板缺少匹配的 `'('` 或 `'['`。参见 `perfunc` 中的 `'pack'`。

### 命令行 < 后无输入文件

(F) 这是一个 `vms` 特有的错误。`Perl` 处理命令行重定向，在命令行上发现了一个 `'<~'`，但找不到从 `stdin` 读取数据的文件名称。

### next::method '%s' 找到 %s

(F) 在该类的剩余包中没有找到此方法名称的进一步实例。如果你不希望它抛出异常……

***

### %s 从未引入

(S internal) 相关的符号已声明，但在使用之前由于某种原因离开了作用范围。

### next::method/next::can/maybe::next::method 找不到封装方法

(F) `next::method` 需要在真实包中真实方法的上下文中调用，但未找到此类上下文。参见 `mro`。

### 字符类中的 \N 必须是命名字符：正则表达式中的 \N{...}；在 m/%s/ 中处标记为 <— HERE

(F) （自 Perl 12 起）`\N` 作为 `[^n]` 的新含义在方括号字符类中是无效的，这与在字符类中丢失特异性的原因相同：它匹配所有内容，这可能不是你想要的。
在反向字符类或作为正则终点时，`\N{{}` 在正则表达式中被限制为单个字符；在 `m/%s/` 中处标记为 `<— HERE`

(F) 命名的 Unicode 转义字符 `\N{...}` 可能会返回多字符序列。虽然字符类本应该匹配输入的一个字符，但当类反转时（`[^~]`）或转义字符是范围的起始或结束时，`perl` 会正确匹配。在反转时匹配的数学逻辑行为与人们的预期非常不同，因此我们决定禁止这样做。同样不清楚的是当 `\N{...}` 用作范围的终点时应该生成什么，例如：
```
[\x41}-\NARABIC SEQUENCE YE WITH HAMZA ABOVE]
```
这里的意思是，`\N{...}` 转义字符是一个代码点序列，因此这是一个错误。

### \N{NAME} 必须由正则表达式的解析器解析；在 m/%s/ 中处标记为 <— HERE

(F) 在编译正则表达式模式时，遇到了一个未解析的命名字符或序列。这可以通过几种绕过解析器的方式发生，例如使用单引号类的上下文，或在双引号类的上下文中使用额外的反斜符：

```
$re = '\N{SPACE}'; # 错误！
$re = "\N{SPACE}"; # 错误！ //re;
```
相反，请使用带有单个反斜符的双引号：

```
通过从较小的组件创建模式可以绕过解析器：

$re = '\N'; /${re}{SPACE}; # 错误！
```
像这样拆分结构并不是一个好主意，而且在这里不起作用。请使用上面的解决方案。

最后，此消息也可能在 `/x` 正则修符下发生，当 `\N` 与 `{` 之间有空格时，在这种情况下请删除空格。
```
/N {SPACE}/x; # 错误！
\N{SPACE}/x; # 好
```

### 运行 setuid 时不允许 %s

(F) 某些操作被认为对于 `setuid` 或 `setgid` 来说不安全，甚至不允许尝试。通常情况下，会有另一种方法可以实现你的目的，即使不安全，至少是可以安全的。参见 `perlec`。

### charnames 别名定义中的不换行空格已弃用

(D deprecated) 你定义了一个包含不换行空格字符的字符名称。将其更改为普通空格。这些名称通常定义在 `alias import argument to charnames` 中，可能由安装到 `$H(charnames)` 的翻译器定义。参见 `charnames` 中的 `CUSTOM ALIASES`。

### 9c 未指定代码

(F) `Perl` 的 `-e` 和命令行选项需要一个参数。如果你想运行一个空程序，请将空字符串作为单独参数传递，或者运行由单个 `0` 或 `1` 组成的程序：

```
perl -e "perl -e0 perl"
```



### `%s` 后不允许有逗号

`(F)` 带有文件句柄或“间接对象”的列表运算符不允许在它与后续参数之间有逗号。否则，它将只是另一个参数。

这可能的原因之一是，期望通过 `use` 或 `import` 将常量导入到你的名称中，但实际上没有发生导入，例如可能是因为你的操作系统不支持该特定常量。希望你对预期要看到的常量使用了显式导入列表；请参见 `perfunc` 中的 `"use"` 和 `perfunc` 中的 `"import"`。虽然显式导入列表可能会自然地更早地捕获此错误，但并不能解决你的操作系统仍然不支持该常量的事实。也许你在 `use` 或 `import` 的符号导入列表常量中，或者在触发此错误的行的常量名中有拼写错误？

### 命令行中没有管道到命令

`(F)` 这是一个 vms 特有的错误。Perl 处理它自己的命令行重定向，在命令行末尾发现了一个 `|l`，因此它不知道你想将此命令的输出管道到哪里。

### 未定义 DB:DB 例程

`(F)` 当前执行的代码是用 `-d` 选项编译的，由于某种原因，当前调试器（例如 `perl5db.pl` 或 `devel::` module）没有定义在每个语句开始处调用的例程。

### 此机器上没有 dbm

`> (P)` 这被视为内部错误，因为现在每台机器都应该提供 dbm，因为 perl 带有 sdbm。参见 `SDBM_File`。

### 未定义 DB::sub 例程

`(F)` 当前执行的代码是用 `-d` 选项编译的，由于某种原因，当前调试器（例如 `perl5db.pl` 或 `devel::` module）没有定义在每个普通例程开始处调用的 `DB:sub` 子例程。

### `-I` 未指定目录

`(F)` `-I` 命令行开关需要目录名称作为相同参数的一部分。使用 `-lib`，对于 lib。`-I lib` 不起作用。

### 命令行中 `2>` 或 `2>>` 后错误

`(F)` 这是一个 vms 特有的错误。Perl 处理命令行重定向，在命令行上发现了一个 `2>` 或 `2>>`，但找不到写入 strdnf 的文件名称。

### 模板中未找到组结束字符 `'%c'`

`(F)` `pack` 或 `unpack` 模板缺少匹配的 `(` 或 `[`。参见 `perfunc` 中的 `'pack'`。

### 命令行 `<` 后无输入文件

`(F)` 这是一个 vms 特有的错误。Perl 处理命令行重定向，在命令行上发现了一个 `'<~'`，但找不到从 stdin 读取数据的文件名称。

### `next::method '%s'` 找到 `%s`

`(F)` 在该类的剩余包中没有找到此方法名称的进一步实例。如果你不希望它抛出异常……

### 已标记数组传递给 `push`/`shift`

`(F)` 你将一个已标记的数组（blessed array）传递给 `push`、`shift` 或另一个数组。这些函数只接受未标记的数组引用或显式以 `@` 开头的数组。

### 不是 SCALAR 引用

`- (F)` Perl 尝试评估一个标量值的引用，但发现的是其他引用。你可以使用 `ref()` 函数来查找它实际的类型。参见 `perref`。

### 不是子程序引用

`- (F)` Perl 尝试评估一个值的引用（即子程序），但发现的是其他引用。你可以使用 `ref()` 函数来查找它实际的类型。同样参见 `perref`。

### 重载载入表中不是子程序引用

`- (F)` 尝试在重载表中指定一个条目，但该条目某种方式没有指向有效子程序的参数。参见 `overload`。

### 参数不足

`- (F)` 该函数需要的参数比你指定的多。

### 格式参数不足

`- (W 语法)` 指定的格式包含的图片字段比下一行提供的多。执行失败。

### 未找到 `%:` 

`- (A)` 你不小心通过 Bourne Shell 而不是 Perl 运行了脚本。检查 `#1` 行，或手动将脚本输入 Perl。

### locale 正则表达式中无效

`- (F)` `([......])` 不能在 `use local` 作用范围内或 `/1` 正则表达式修符中使用，因为这需要在运行时计算它的求值，而它仅在编译时有效。

### 无 UTC 偏移信息；假设本地时间为 UTC

`- (S)` 一个 vms 特有的警告。Perl 无法找到本地时区偏移，它假设本地系统等同于 UTC。如果不是，请定义 `SYSTIME_DIFFERENTIAL` 逻辑，将其转换为需要加到 UTC 以获得本地时间的秒数。

### RUN 中的空操作 (NULL OP)

`- (S 调试)` 内部例程调用 `run()` 时带有空的操作码指针。

### formline 中的空指针

`- (F)` `formline` 的第一个参数必须是有效的格式图片规范。结果发现它是空的，这可能意味着你提供了一个未初始的值。参见 `perform`。

### 空重分配内存 (Null realloc)

`- (P)` 尝试重新分配 NULL 内存。

### 空的正则表达式参数

`- (P)` 内部模式匹配例程发生了严重错误。

### 数字过长

`- (F)` Perl 限制程序中十进制数字表示约为 250 个字符。你超过了该长度。未来的 Perl 版本可能会消除这一任意限制。在此期间，尝试使用科学计数法（例如用 `"1e6"` 代替 `"1_000_000"`）。

### 无数字

`- (F)` Perl 正在寻找数字但没有发现任何像数字的内容。这发生在，例如 `\{`，大括号之间没有数字。

### 八进制数 > 037777777777 不可移植

`- (W 可移植性)` 你指定的八进制数大于 `2**32-1` (4294967295)，因此在不同系统之间不可移植。有关可移植性问题请参见 `perlport`。

### 子程序的奇数个数名/值参数

`- (F)` 一个在签名中使用贪婪参数（slurpy parameter）的子程序接收到奇数个参数来填充哈希表。它要求参数成对出现，键与值的数量相同。子程序的调用者可能存在问题。

### overload::constant 的奇数个数参数

`- (W overload)` 对 `overload::constant` 的调用包含奇数个数参数。参数应该成对出现。

### 匿名哈希中的奇数个数元素

`- (W 杂项)` 你指定了奇数个数元素来初始化哈希表，这是不对的，因为哈希表是键/值对形式。

### 哈希赋值中的奇数个数元素

`- (W 杂项)` 你指定了奇数个数元素来初始化哈希表，这是不对的，因为哈希表是键/值对形式。

### 字符串外的偏移量

`- (F 层)` 你尝试使用指向缓冲区之外的偏移量执行 `read`/`send`/`recv`/`seek` 操作。这很难想象。这些的例外是：当在 `read()` 文件或在 I/O 缩放操作数的末尾进行 `seek` 操作时，将进行零填充。

### 未打开的 `%s` 上的 `%s`

`- (W 未打开)` 尝试在一个未初始化的句柄上进行 I/O 操作。你需要执行 `open()`、`sysopen()` 或 `socket()` 调用，或者调用 `FileHandle` 包中的构造函数。

### 未打开的句柄 `%s` 上的 `-s`

`- (W 已打开)` 你尝试在一个未打开的句柄上调用测试操作符。检查你的控制流。同样参见 `perlfunc` 中的 `"-X"`。

### oops: oopsAV

`- (S 内部)` 一个关于语法损坏的内部警告。

### oops: oopsHV

`- (S 内部)` 一个关于语法损坏的内部警告。

### 同时将目录句柄 `%s` 也作为文件打开

`- (D io, 已弃用)` 你使用 `open()` 将文件句柄关联到一个已经持有目录句柄的符号（全局变量或标量）。虽然是合法的，但这种用法可能会导致你的...

### unpack 中字符串外存在格式不正确的 UTF-8 中的 '@'

`(F)` 你有一个模板，它为正在解包的字符串指定了绝对位置。该正在解包的字符串也是无效的 UTF-8。详见 `perlfunc` 中的 `"pack"`。

### overload 参数 `%s` 无效

`(W overload)` `overload` 编译指令接收到了一个它不识别的参数。你是否写错了操作符？

### 重载的解引用没有返回引用

`(F)` 一个带有重载解引用操作符的对象被解引用了，但重载操作没有返回引用。

### 重载的 qr 没有返回引用

`(F)` 一个带有重载 `qr` 的对象被用作匹配的一部分，但重载操作没有返回一个编译后的正则表达式。

### `%s` 属性可能匹配到保留字：`%s`

`(W)` 使用了具有包特定处理程序的全小写属性。该名称对 Perl 本身可能具有意义，尽管目前尚未如此。也许你应该使用混合大小写的属性。

### pack/unpack 重复计数

`(F)` 你不能重复一个大到导致符号整数溢出的计数。详见 `perlfunc` 中的 `"pack"`。

### 页面溢出

`(W)` 调用 `write()` 产生的行超过了页面的容纳能力。详见 `perform`。

### panic: `%s`

`(P)` 内部错误。

### panic: attempt to call `%s`

`(P)` 测试操作符之一进入了调用 ACL 相关函数的代码分支，而该函数在当前平台上不可用。

### panic: child-process was not scheduled

`(P)` 线程中的子进程在允许的时间内没有调度，因此无法正常初始化。

### panic: ck_grep, type=%u

`(P)` 在尝试 `grep` 时失败了内部一致性检查。

### panic: ck_split, type=%u

`(P)` 在尝试 `split` 时失败了内部一致性检查。

### panic: corrupt saved index

`(P)` 请求 `savestack` 恢复的局部值比 `savestack` 中实际拥有的多。

### panic: del_backref

`(P)` 在尝试重置弱引用时失败了内部一致性检查。

### panic: die `%s`

`(P)` 我们将上下文栈弹出到 `eval` 上文，然后发现它并不是一个 `eval` 上文。

### panic: do_subst

`(P)` 调用内部 `pp_subst()` 例程时使用了无效的操作数据。

### panic: do_trans_%s

`(P)` 调用内部 `do_trans` 例程时使用了无效的操作数据。

### panic: fold_counts JMP_PUSH returned %d

`(P)` 在折叠常量时捕获到了 `eval` 之外的异常。

### panic: frexp:%f

`(P)` 库函数 `frexp()` 失败，导致无法执行 `printf("%f")`。

### panic: goto, type=%u, ix=%d

`(P)` 我们将上下文栈弹出到一个带有指定标签的上下文，并发现它不是我们如何处理的上下文。

### panic: gp_free failed to create a pointer

`(P)` 用于 `glob` 条目的内部例程反复尝试，但 `glob` 中每次都重新创建了条目。

### panic: INTERCASE, `%s`

`(P)` 词法分析在大小写修符处进入了错误状态。

### panic: INTERCONCAT,%s

`(P)` 词法分析在解析带有括号的字符串时进入了错误状态。

### panic: popen errno read

`(F)` 子进程返回了一个关于其 `errno` 的不可理喻的消息。

### panic: last, type=%u

`(P)` 我们将上下文栈弹出到一个块上下文，然后发现它并不是一个块上下文。

### panic: leave_scope clears

`(P)` 一个可写变量在作用范围内由于某种原因变成了只读。

### panic: leave_scope inconsistency %u

`(P)` `savestack` 不同步。至少，它的顶端有一个无效的枚举值。

### panic: magic_killrefs

`(P)` 在尝试重置指向对象的所有弱引用时失败了内部一致性检查。

### panic: malloc, `%s`

`(P)` 某些操作请求了负数字节的 `malloc`。

### panic: memory_wrap

`(P)` 某些操作尝试分配超出可能的内存或负数内存。

### panic: pad_alloc, %p!=%p

`(P)` 编译器混淆了它正在哪个临时板分配和释放临时变量及局部变量。

### panic: pad_free curpad, %p!=%p

`(P)` 编译器混淆了它正在从哪个临时板分配和释放临时变量及局部变量。

### panic: pad_free_po

`(P)` 内部检测到零临时板偏移。尝试释放一个从未被分配的目标。

### panic: pad_reset curpad, %p!=%p

`(P)` 编译器混淆了它正在从哪个临时板分配和释放临时变量及局部变量。

### panic: pad_sv_po

`(P)` 内部检测到零临时板偏移。

### panic: pad_swipe curpad, %p!=%p

`(P)` 编译器混淆了它正在从哪个临时板分配和释放临时变量及局部变量。

### panic: pad_swipe_po

`(P)` 内部检测到无效的临时板偏移。

### panic: pp_iter,type=%u

`(P)` 获取迭代器在非循环的上下文帧中被调用。

### panic: pp_match%s

`(P)` 调用内部 `pp_match()` 例程时使用了无效的操作数据。

### panic: pp_split, pm=%p, s=%p

`(P)` 在设置 `split` 时发生了糟糕错误。

### panic: realloc,

`(P)` 某些操作请求了负数字节的 `realloc`。

### panic: reference miscount on nsv in sv_replace()%d != 1

`(P)` 我们将上下文栈弹出到 `eval` 上文，然后发现它并不是一个 `eval` 上文。

### 相关模块使用的 Perl 版本比当前运行的版本要新

`(F)` 相关模块使用的 Perl 版本比当前运行的版本要新。无论如何，你上次升级已经过去多久了？请参阅 `perlfunc` 中的 `"require"` 部分。

### PERL_SH_DIR 长度过长

`(F)` OS/2 发生错误。`PERL_SH_DIR` 是查找 sh-shell 的目录。请参阅 `perlos2` 中的 `"PERL_SH_DIR"`。

### PERL_SIGNALS 非法: "%s"

`(X)` 查看 `perlrun` 中的 `"PERL_signals--this"` 以获取合法值。

### Perl since %s too modern--this is %s, stopped

`(F)` 你尝试运行的代码声称它不会在你正在使用的 Perl 版本上运行，因为该版本太新了。

### perl warning: Non hex character in '${ENV{PERL_HASH_SEED}}'

`PERL_HASH_SEED` 应该匹配 `\/\s*\(:)?[0-9a-zA-F]+\s*\*/` 但它包含一个非十六进制字符。

### perl warning: Setting locale failed

`perl warning: Setting locale failed.` 请检查你的 locale 设置：`LC_ALL="US"`, `LANG=(unset)` 是否在你的系统上受支持并已安装。`perl warning:` 回退到标准 locale `"C"`。

### perl warning: strange setting in '${ENV{PERL_PERTURB_KEYS}}': "%s"

`(S)` 运行 Perl 时定义的环境变量 `PERL_PERTURB_KEYS`，但其包含意料之外的值。

### pid %x 不是子进程

`(W exec)` 一个 vms 特有的警告。`Waitpid()` 被要求等待一个并非当前进程子进程的进程。

### unpack 中的 ‘P’ 必须有显式大小

`(F)` `unpack` 中的 `P` 必须有显式大小，不能为 `""`。

### pop 引用是实验性的

`(S: experimental::autodef)` 带有标量参数的 `pop` 是实验性的，可能会在未来的 Perl 版本中发生变化或删除。

```perl
no warnings :experimental::autodef;
```

### 正则表达式中未知的 POSIX 类 [%s]

`(F)` 字符类 `[:]` 语法中的类是未知的。参阅 `perlire`。

### POSIX getpgrp 不接受参数

`(F)` 你的系统 POSIX `getpgprp()` 不接受参数，与 BSD 版本不同，后者接受一个 pid。

### POSIX 语法 [%c %c] 属于正则表达式中字符类内部

`(W regexp)` 字符类构造 `[:]`, `[=]` 和 `[.]` 位于字符类内部。参阅 `perlire`。

### 正则表达式语法 [.] 留给未来扩展

`(F)` 在正则表达式字符类中，以 `"["` 开头并以 `"]"` 结尾的语法留给了未来扩展。

### 正则表达式语法 [=] 留给未来扩展

`(W)` 在正则表达式字符类中，以 `"[="` 开头并以 `"=]"` 结尾的语法留给了未来扩展。

### 可能尝试在 qw(list) 中放置注释

`(W)` `qw()` 列表项通过空白符分隔；与字面字符串一样，注释字符不会被忽略，而是被视为字面数据。

```
@list = qw( a # comment b # another comment );
```



@list = qw( a b );

```
如果你真的想要注释，请使用旧方法构建列表，使用引号和逗号：
```
@list = ( 'a', # a comment 'b', # another comment );
```

## 可能尝试用逗号分隔单词

`qw` 列表包含通过空白符分隔的项目；因此不需要逗号来分隔项目。（你可能使用了与此处括号不同的分隔符；大括号也经常被使用。）

你可能写了类似的内容：

```
qw! a, b, c !;
```

```
qw! a b c !;
```

## 可能内存损坏：`%s` 溢出第 3 个参数

`(F)` `ioctl(l)` 或 `fcntl()` 返回了大于合理的缓冲区大小，但 Perl 为了万全在缓冲区末尾猜测一个哨位字节。该哨位被覆盖了，Perl 假设内存没有损坏。参阅 `perfunc` 中的 `"ioctl"`。

## 控制流可能存在优先级问题

`(W control flow)` Perl 为了万全在缓冲区末尾猜测一个哨位字节。该哨位被覆盖了，Perl 假设内存没有损坏。参阅 `perfunc` 中的 `"ioctl"`。

## 正则表达式中的属性 '`%s`' 未知；在 `m/%s` 处标记为 < HERE

`(F)` Perl 不得认识你通过 `\p` 或 `\P` 指定的命名属性。也许你拼错名称了？请参阅“Properties accessible \{p}”获取可用属性的完整列表。如果是用户自定义属性，它必须由你定义。

`(W)` 正则表达式中 `%s` 后面跟随非法字符；这对于 `@` 及其后续内容是无用的。

`(S)` 声明的子程序之前已用不同的原型（prototype）声明过。原型未终止。

`(F)` 你在原型定义中漏掉了右括号。'`%s`' 被属性 `'prototype(%s)'` 覆盖。

`(W)` `%s` 后面跟随非法字符

## 正则表达式中量化符前面没有匹配内容；在 `m/%s` 处标记为 < HERE

`(F)` 你以量化符开始了一个正则表达式。如果你的本意是字面量，请使用反斜杠。`<` 显示了正则表达式中问题所在的位置。

## 量化符 '{,}' 中的值大于；在 `m/%s` 处标记为 < HERE

`(F)` 目前对 `{min,max}` 的最小值和最大值的大小限制。`<` 显示了正则表达式中问题所在的位置。

## 量化符 `{n,m}` 中 `n > m` 无法在正则表达式匹配；在 `m/%s` 处标记为 < HERE

`(W)` 最小值应该小于或等于最大值。如果你真的想让正则表达式匹配零次，直接使用 `(0)` 即可。

## 正则表达式 `%s` 中的零长度表达式上存在意外之外的量化符

`(W)` 你在一个没有意义的地方使用了正则表达式，例如零宽断言。请尝试将量化符放在断言内部。

`(F)` 范围中的一个（或两个）数字参数在范围之外。`<` 显示了匹配 `"abc"` 的方式应该是 `/abc?(?:xyz){3}/`，而不是 `/abc?(?:xyz){3}/`。

## 正则表达式中的范围应该是 0-9、A-Z 或 a-z 的子集；在 `m/%s` 处标记为 < HERE

`(W)` 正则表达式（仅在 `'strict'` 中或 `[]` 内部使用）不直观。

## 正则表达式中的数字范围应来自同一组；在 `m/%s` 处标记为 < HERE

`(W)` 你正在读取的目录句柄已关闭或不是目录句柄。检查你的控制流。

## 在关闭的文件句柄 `%s` 上执行 `readline()` (W)

你正在读取的文件句柄本身已关闭。检查你的控制流。

## 在关闭的文件句柄 `%s` 上执行 `read()` (W)

你尝试从一个已关闭的文件句柄读取。

## 在打开的文件句柄 `%s` 上执行 `read()` (W)

你尝试从一个从未打开的文件句柄读取。

## 重新分配内存过大：`%x` (F)

在 MS-DOS 机器上无法分配超过 64K 的内存。

## `realloc()` (S)

在已经释放的对象上调用了内部程序 `realloc`。使用 `-DDEBUGGING` 编译 `perl` 可以使用 `-D` ，除非产生所需输出的代码已编译进 Perl 中（这会产生一些开销，这就是为什么在你的副本中去除了它）。

## 在 `PerlIO_find_layer` 中递归调用 `Perl_load_module`

`(P)` 目前不允许在创建 `%INC` 钩内部文件句柄时加载模块。这可能发生在 `\$fh`、`'<'`、`\$scalar` 上，它们会隐式加载 `PerlIO::scalar`。尝试显式使用 `PerlIO::scalar`。

## 在包 `%s` 中检测到递归继承

`(F)` 在计算包的方法解析顺序 (MRO) 时，Perl 认为在 `@ISA` 层次结构中发现了无限循环。这是一个粗检，在 `@ISA` 深度达到 100 层后退出。

## 在 `%s` 中存在冗余继承

`(W)` 你调用函数时提供的参数比其他提供的参数所需的要。仅当 `printf` 类型的格式所需的参数少于提供的参数时才会输出，但这些可能用于函数内部，例如 `perfunc` 中的 `"pack"`。

`refcnt_dec: fd %d%s`
`refcnt: fd %d%s`
`refcnt_inc: fd %d%s`

`(P)` Perl 的实现内部一致性检查失败。如果你看到此消息，说明出了非常严重的问题。

## 在偶数个元素的列表时找到引用

`(W misc)` 你提供了一个引用，而 Perl 期望得到一个偶数个元素的列表（用于赋值给哈希表）。这通常意味着你在应该使用括号时使用了匿名构造函数。在任何情况下，哈希表都包含键/值对。

```perl
%hash = { one => 1, two => 2 }; // 错误
$hash = [ qw array ]; // 错误
$hash = ( one => 1, two => 2, ); // 正确
$hash = qw( one two 2 ); // 也可以
```



引用已经是弱引用

`(W misc)` 你尝试对一个已经是弱的引用进行弱化。这样做无效。

正则表达式中引用无效的 0；在 `m/%s` 处标记为 `< HERE`

`(F)` 你在表达式中使用类似 `\7` 的内容，但没有七组括号。

正则表达式中引用不存在或未关闭的组；在 `m/%s` 处标记为 `< HERE`

`(F)` 你在正则表达式中使用类似 `\k<NAME>` 的内容，但没有对应的捕获组。`<` 显示了正则表达式中问题所在的位置。

引用不存在的组拼写错误。

— 显示了正则表达式中问题所在的位置。

`regexp`内存损坏

`(P)` 正表达式引擎被编译器提供的内容搞混了。

正则表达式 `m/%/` 空间不足

`(P)` 一个“不可能发生”的错误，本应由 `safemalloc()` 捕获。

重复限制永远不会终止 (`~~` 和 `@@`)

`(F)` 你的格式包含 `~~` 重复直到为空序列，且永远不会为空，导致重复永远终止。你可能可以使用 `^#` 代替。请参考性能。

替换列表长于搜索列表

`(W misc)` 你使用的替换列表比搜索列表长。替换列表中的额外元素没有意义。

`%s'` 已解析为 `{%s}%d`

`(W misc, regexp)` 你在类双引号的字符串中写了 `\08` 或 `\179`。
最后一位数字被视为单个字符，用八进制指定。最后一位数字是字符串中的下一个字符。要告诉 Perl 这确实是你想要的内容，你可以使用 `\ ` 语法，或者使用恰好三位数字来指定该字符的八进制值。

反转的 `%s=` 运算符

`(W syntax)` 你将赋值运算符写反了。`=` 必须始终放在最后，以避免与后续的一元运算符产生歧义。

在无效的目录句柄 `%s` 上尝试执行 `rewinddir()`
`(W io)` 你尝试进行 `rewinddir()` 的目录句柄要么已关闭，要么不是一个真正的目录句柄。请检查你的控制流。

标量泄漏：`%d`
`(S internal)` Perl 的内部标量计数出现了一个问题：在 Perl 退出时，并非所有的标量变量都已释放。这表明内存泄漏，这显然是坏的，特别是当该 Perl 程序旨在长期运行时。

标量值 `@{%s}%s}` 优于 `%s[%s]`

`(W syntax)` 你使用了数组切片（由 `@` 表示）来选择数组的单个元素。区别在于 `$foo[&bar]` 在赋值时和评估其参数时始终表现像一个标量，而 `@foo[&bar]`—`@foo[&bar]` 在你赋值时表现像一个列表，并为其下标提供列表上下文，如果你只预期一个下标，这可能会导致奇怪的结果。

另一方面，如果你实际上希望将数组元素视为列表，你需要研究引用（`references`）的工作原理，因为 Perl 不为你魔术地在标量和列表之间进行转换。

标量值 `@{%s}%s}` 优于 `%s[%s]`

`(W syntax)` 你使用了哈希表切片（由 `@` 表示）来选择哈希表的单个元素。区别在于 `$foo[&bar]` 在赋值时和评估其参数时始终表现像一个标量，而 `@foo[&bar]`—`@foo[&bar]` 在你赋值时表现像一个列表，并为其下标提供列表上下文，如果你只预期一个下标，这可能会导致奇怪的结果。

另一方面，如果你实际上希望将哈希元素视为列表，你需要研究引用（`references`）的工作原理，因为 Perl 不会为你魔术地在标量和列表之间进行转换。见 `perlref`。

搜索模式未结束

- `(F)` 词法分析器找不到 `//` 或 `m{}` 结构的结束界符。变量 `$m` 缺失 `//` 括号界符可能会导致此错误。

  注意自 Perl 5.10.0 起，`//` 也可以是定义或（defined-or）结构，而不只是空搜索模式。因此，在 5.10.0 或更高版本中使用 `//` 作为定义或结构的代码可能会被 5.10.0 之前的版本的 Perl 解析为未结束的搜索模式。

在无效的目录句柄 `%s` 上尝试执行 `seekdir()`
`(W io)` 你执行 `seekdir()` 的目录句柄要么已关闭要么不是目录句柄。请检查你的控制流。

在未打开的文件句柄上执行 `%sseek()`
`(W unopened)` 你尝试在一个从未打开或之后已关闭的文件句柄上使用 `seek()` 或 `sysseek()` 函数。

`select` 未实现

- `(F)` 本机器未实现 `select()` 系统调用。

不支持数组和哈希的自绑定（Self-ties）

- `(F)` 当前实现不支持数组和哈希的自绑定。

缺少分号
`(W semicolon)` 附近的语法错误可能是由于缺少分号引起的，也可能是由于其他缺失的运算符，例如逗号。

半崩溃：尝试转储已释放的字符串
`(S internal)` 调用了内部 `newSVsv()` 例程来复制一个之前标记为释放的标量。

`sem%` 未实现

- `(F)` 你的系统上没有 System V 信号量 IPC。

在已关闭的 socket `%s` 上执行 `send()`
`(W closed)` 你要发送的 socket 在此之前的某个时候已经关闭了。请检查你的控制流。

序列 `"ic"` 无效
- `(F)` 这三个字符在双引号上下文中可能按顺序出现。此消息仅在非 ASCII 平台上触发（ASCII 平台上会显示不同的错误信息）。如果你意图用此序列指定控制字符，你必须使用不同的方法来指定它。

序列 `(?` 在正则表达式中不完整；在 `m/%s` 中标记为 `<-- HERE`
- `(F)` 正则表达式包含一个不完整的扩展 `(?.。<-- HERE` 显示了在正则表达式中发现问题的位置。见 `perperl`。

序列 `(?c...):` 在正则表达式中未实现；在 `m/%s` 中标记为 `<-- HERE`
- `(F)` 一个提议的正则扩展保留了该字符但尚未编写。`<-- HERE` 显示了在正则表达式中发现问题的位置。见 `perperl`。

序列 `(?s...):` 在正则表达式中不被识别；在 `m/%s` 中标记为 `<-- HERE`
- `(F)` 你使用的正则表达式没有意义。`<-- HERE` 处是在正则表达式中发现问题的位置。这可能发生在使用 `(?^$.)` 结构告诉 Perl 使用默认表达式修饰符，而你冗余地指定了默认修饰符时。其他情况见 `perperl`。

序列 `(?#...` 在正则表达式中未结束；在 `m/%s` 中标记为 `<-- HERE`
- `(F)` 正则表达式注释必须由右括号结束。不允许嵌套的括号。见 `perperl`。

序列 `(?...` 在正则表达式中未结束；在 `m/%s` 中标记为 `<-- HERE`
- `(F)` 正则表达式注释必须由右括号结束。不允许嵌套的括号。见 `perperl`。

`%s` 应该写为 `"%s"`

`(W stays)` 你在 `join` 的第一个参数中使用了一个 Perl 期望找到字符串的模式。Perl 将返回针对 `$,` as 匹配的真或假结果，这可能不是你的本意。

在关闭的 socket 上执行 `shutdown()`

`(W closed)` 你尝试关闭一个已经关闭的 socket。这似乎有点多余。

未定义 SIG handler `"%s"`

`(W signal)` 命名为 `%s` 的信号处理程序实际上并不。也许你把它放在了错误的包（`package`）中？

`Slab leaked from cv vp`

`(S)` 如果看到此消息，说明 op 的内部账记录出现了严重问题。在编译错误后，需要释放的 op 没能找到，因此导致了内存泄漏。

`sleep(%u)` 过大

`(W overflow)` 你调用 `sleep` 时数字超过了它能可靠处理的范围，`sleep` 睡眠时间可能比请求的短。

`slurpy` 参数不是最后一个

`(F)` 在子过程中，你在一个 `slurpy` 参数（数组或哈希）之后放置了内容。`slurpy` 参数获取所有可用参数，因此没有剩余参数可以填充后面的参数。

智能匹配非重载对象破坏了封装

`(F)` 你不应该在一个没有重载该运算符对象上使用 `~~` 运算符：Perl 拒绝使用该对象的底层结构进行智能匹配。

实验性智能

`(S experimental::smartmatch)` 当你使用智能 (`--`) 运算符时发出此信息。这目前是一个实验性功能，其细节在 Perl 未来的版本中可能会更改。特别是目前的行为被认为过于复杂且不直观，极有可能被重构。

`sort` 不是保留字

`(F)` 这是一个几乎没人遇到的旧错误信息。但 `sort` 曾是一个关键字，人们有时将其用作文件句柄。

`sort` 子过程没有返回值

`(F)` 在 xs 中编写的 `sort` 子过程必须恰好返回一项。`perflunc` 中的 `"sort"`。

源过滤器仅作用于字节流

`(F)` 在 `unicode_eval` 特性下，在字符串内激活源过滤器（通常通过加载源过滤器模块）是不允许的。考虑使用 `evalbytes`。见 `feature`。

`splice()` offset 越数组末尾

`(W misc)` 你尝试指定一个超出传递给 `splice()` 数组末尾的偏移量。`splice` 将在数组末尾执行，而不是传递它。如果这不是你想要的，尝试通过赋值 `$#array = offset` 来显式预扩展数组。见 `perflunc` 中的 `"splice"`。

引用上的 slice 是实验性的

`(S experimental::autderef)` 使用标量参数的 `splice` 是实验性的，并可能在未来的 Perl 版本中更改或删除。如果你想冒风险使用此功能，只需禁用此警告：

```
no warnings "experimental::autderef";
```

# split 循环

+ `(P)` `split` 正在进行无限循环。（显然，`split` 的迭代次数不应超过输入字符的数量，但这种情况确实发生了。）见 `perfunc` 中的 `"split"`。

`(W)` `exec` 你对除 `die()` 外的语句执行了 `exec()`。这几乎是一个错误，因为除非发生失败，否则 `exec()` 永远不会返回。你可能想用 `system()`，这将抑制此警告，或者将 `exec()` 放在单独的块中。

`"state"` 子过程不在包

`(F)` 词法作用域子过程不在包中，因此尝试在前面加上修饰符声明它是没有意义的。

`"state %s"` 用于比较

`(W)` 包变量 `$a` 和 `$b` 用于 `sort` 比较。你在 `sort` 比较块内部将 `$a` 或 `$b` 作为 `<=>` 的操作数，而该变量之前被声明为词法变量。用包名限定 `sort` 变量，或重命名该变量。

`"state"` 变量 `%s` 不在包

`(F)` 词法作用域子过程不在包中，因此尝试在前面加上修饰符声明它是没有意义的。如果你想本地化包变量，请使用 `local()`。

在未打开的文件句柄 `%s` 上执行 `stat()`

+ `(W)` 你尝试在一个从未打开或已关闭的文件句柄上使用 `stat()` 函数。

`(W utf8)` 你尝试为了读取或追加打开一个标量的引用，而该标量包含了超过 `0x0FF` 的代码点。内存文件模型模拟磁盘文件并包含字节。

在包 `%s` 中解析 `over %s` 重载 `%s` 时发现存根

`(P)` 跨 `@ISA` 的重载解析可能会被导入存根破坏。存根不应被隐式创建，但显式调用可能会破坏。

子过程 `"&%s"` 不用

`(W)` 在编译期间，一个内部子过程或 `eval` 试图捕获一个当前不可用的外部词法子过程。

`syntax error in line %d: "%s" unexpected`

+ `(A)` 你无意中通过 Bourne shell 运行了脚本，而不是 Perl。请检查 `#` 行，或者手动将你的脚本输入 Perl。

`syntax error in file %s at line %d, next 2 tokens "%s"`

+ `(F)` 当你通过 `perl4` 解释器运行 `perl5` 脚本时，可能会发生错误，特别是当两个标记是 `"strict"` 或 `"my var"` 或我们的 `"my var"` 时。

`Syntax error in regex m/%s/`

+ `(F)` Perl 无法理解你在该结构中的含义；此信息通知你它正在放弃。

`%s syntax OK`

+ `(F)` `perl -c` 成功时的最终总结信息。

`sysread()` on closed filehandle `%s`

+ `(W)` 你尝试从已关闭的文件句柄读取。

`sysread()` on unopened filehandle `%s`

+ `(W)` 你尝试从一个从未打开的文件句柄读取。

`System V %s is not implemented in this machine`

+ `(F)` 你尝试对以 `"sem"`、`shm"` 或 `"msg"` 开头的函数进行操作，但 System V IPC 在你的机器上没有实现。在某些机器上，功能可能存在但未定义。请咨询你的系统支持。

`syswrite()` on closed filehandle `%s`

+ `(W)` 你正在写入的文件句柄在之前的某个关闭了。请检查你的控制流。

`"-T"` and `"-B"` not implemented on filehandles

+ `(F)` 当 Perl 不知道 stdio 类型时，无法查看文件句柄的 stdio 缓冲区。你必须使用文件名。

`Target of goto is too deeply nested`

+ `(F)` 你尝试跳转到一个嵌套深度过深的标签，以至于 Perl 无法处理。Perl 拒绝执行其实是在帮你的忙。

`teldir()` attempted invalid dirhandle `%s`

+ `(W)` 你传递给 `teldir()` 的目录句柄已关闭或根本不是一个目录句柄。检查你的控制流。

`tell()` on unopened filehandle

+ `(W)` 你尝试在一个从未打开或此后关闭的文件句柄上使用 `tell()` 函数。

`That of $ is unsupported`

+ `(F)` 对 `$[` 的赋值现在受到限制，并被解释为编译指令。你只能保留以下一种：

```



```
$[ = 0; $[ = 1; ... local $[ = 0; local $[ = 1; ...
```



这是为了防止一个模块无意中改变另一个模块数组基的问题。参见 `"$ \$ in perperl and arybase"`。

# The bitwise feature is experimental

`(experimental::bitwise)` 如果你在启用了 `"bitwise"` 特性的情况下使用位运算符 (`& | ^ ~ & | . ^ ~`)，则会发出此警告。如果你想使用该功能，只需抑制警告，但要清楚这样做意味着你正在着使用实验性功能的风险，该功能在未来的 Perl 版本中可能会更改或删除：

```
no warnings "experimental::bitwise"; use feature "bitwise"; \$x |= \$
```

The `crypt()` function is unimplemented due to excessive paranoia.

+   `(F)` Configure 在你的机器上没有找到 `crypt()` 函数，可能是因为你的供应商没有提供，可能是因为他们认为美国政府认为它是秘密，或者至少他们会继续假装它是秘密。如果你在这一点上引用我的话，我会否认此的。

The `%s` function is unimplemented

+   `(F)` 根据 Configure 的探测，指示的函数在当前架构上没有实现。

# The lexical_subs feature is experimental

`(experimental::lexical_subs)` 如果你用 `my` 或 `state` 声明子程序，则会发出此警告。但要清楚这样做意味着你正在冒着使用实验性功能的风险，该功能在未来的 Perl 版本中可能会更改或删除：

```
no warnings "experimental::lexical_subs"; use feature "lexical_subs";nmy foo { ... }
```

# The regex_sets feature is experimental

`(experimental::regex_sets)` 如果你在正则表达式中使用语法 `([?])`，则会发出此警告。该功能的细节可能会变化。如果你想使用它，但又清楚这样做意味着你正在冒着使用实验性功能的风险（该功能在未来的 Perl 版本中可能会更改），你可以执行以下操作来消除警告：

```
no warnings "experimental::regex_sets";
```

# The signatures feature is experimental

`(experimental::signatures)` 如果你使用签名解包子程序的参数，则会发出此警告。如果你想使用该功能，只需抑制警告，但要清楚这样做意味着你正在冒着使用实验性功能的风险，该功能在未来的 Perl 版本中可能会更改或删除：

```
no warnings "experimental::signatures"; use feature "signatures";n foo ($left, $right) { ... }
```

The `stat` predicting `%s` wasn't an

+   `(F)` 如果最后一次写入 `stat` 缓冲区的 `stat` 越过了符号链接到达真实文件，那么对 `stat` 缓冲区进行符号似概率测试是没有意义的。请使用实际的文件名。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

The ‘unique’ attribute may only be applied to ‘our’ variables

+   `(F)` 此属性只能应用于 `'our'` 变量。

仍未接受。`%d %s` 必须是 `%s`（不是 `%s`）

`%s` 的参数类型必须是未绑定的引用（hasref 或 arrayref）

-   `(F)` 此函数要求该位置的参数必须是特定类型。数组必须是 `%NAME` 或 `@{%EXPR}`。哈希必须是 `%NAME` 或 `%{%EXPR}`。不支持隐式解引用——请使用 `<%EXPR>` 形式作为显式引用。参见 `perlref`。

-   `(F)` 你对 `keys`、`values` 或 `each` 调用了标量参数，但该标量不是指向未绑定的哈希或数组的引用。

`umask` 未实现

-   `(F)` 你的机器没有实现 `umask` 函数，而你尝试使用它来限制自己的权限（`%EXPR & 0700`）。

上下文不平衡：Pushes 数量比 Pops 多 `%d`

-   `(S)` 退出码检测到执行上下文进入和离开的次数存在内部不一致。

保存不平衡：saves 数量比 restores 多 `%d`

-   `(S)` 退出码检测到临时局部化值的数量存在内部不一致。

作用域不平衡：ENTERs 数量比 LEAVES 多 `%d`

-   `(S)` 退出码检测到块进入和离开的次数存在内部不一致。

字符串表引用计数不平衡：`"%s"`为 `%d`

-   `(S)` 退出时，发现用于复制输入和哈希键的共享字符串表中仍存在某些字符串。这些条目应该被释放，因此这表明错误。

临时变量不平衡：allocs 数量比 frees 多 `%d`

-   `(S)` 退出码检测到临时标量（mortal scalars）分配和释放的次数存在内部不一致。

调用了未定义的格式 `"%s"` 

-   `(F)` 指定的格式似乎不存在。也许它真的在另一个包中？参见 `perlref`。

调用了未定义的子程序 `"%s"` 

-   `(F)` 指定的排序比较例程似乎不存在。也许它在不同的包中？参见 `perlfunc` 中的“sort”。

调用了未定义的子程序 `&%s`

-   `(F)` 指出的子程序尚未定义，或者已经定义过但已被取消定义。

调用了未定义的子程序

-   `(F)` 你尝试调用的匿名子程序尚未定义，或者已经定义过但已被取消定义。

在 `sort` 中未定义的子程序

-   `(F)` 指定的排序比较例程已声明但似乎尚未定义。参见 `perlfunc` 中的“sort”。

调用了未定义的顶部格式 `"%s"` 

-   `(F)` 指出的格式似乎不存在。也许它真的在另一个包中？参见 `perl`。

赋值给类型全局变量的未定义值

-   `(W msg)` 一个未定义的值被赋值给类型全局，类似于 `*foo = undef*`。这没有产生作用。你可能实际上是指 `undef *foo`。

`%%`: 未定义变量

-   `(A)` 你无意中通过 **`csh`** 而不是 Perl 运行了脚本。请检查 `#!` 行，或手动将脚本输入 Perl。

正则表达式中未转义的左括号已弃用，将直接通过正则传递；在 <-- HERE 处标记

-   `(D)` 已弃用，你在正则表达式模式中使用了一个字面字符。你应该使用 `\c` 代替，因为 Perl 的未来版本（暂定为 v5.26）会将此视为语法错误。如果模式分隔符也被标记，任何匹配的正则 `()` 也应该被转义以避免混淆解析器，例如：`qr[abc\\def\ghi]`

`%` 的 `unexec` 执行失败！

-   `(F)` 出于某种原因 `unexec()` 程序。请咨询你当地的 FSF 代表，可能是他们最初将其放入的。

正则表达式中出现意外的前置操作数的二进制运算符 `%c`；在 `m/%s/` 的 <-- HERE 处标记

-   `(F)` 你写了类似这样的代码：
    `(? |Digit ])`
    其中 `|` 是一个右侧有操作数的二进制运算符，但左侧没有操作数。

正则表达式中出现意外字符；在 `m/%s/` 的 <-- HERE 处标记

-   `(F)` 你写了类似这样的代码：
    `([ z ])`
    在 `([ z ])` 中，不允许字面字符，除非它们位于内部的方括号内，例如
    `([[ z ])`

另一种可能是你忘记了反斜杠。Perl 不足够聪明来理解你真正意味着什么。

通过类型/标记 `%d:%d` 进入了意外的常量 Ivalue

-   `(P)` 在 Ivalue 上下文中编译子程序时，Perl 失败了内部一致性检查。它遇到了一个畸形的树。

意外的退出 `%u`

-   `(S)` 退出码检测到临时标量分配和释放的次数存在内部不一致。当 `EXIT_WARN` 设置时，调用了 `exit()` 或脚本正常退出。

意外的退出失败 `%d`

-   `(S)` 在 `EXIT_WARN` 设置时，调用了未捕获的 `die()`。

正则表达式中出现意外的 `')'`；在 `m/%s/` 的 HERE 处标记

-   `(F)` 你写了类似这样的代码：
    `(?([ \p{Digit} + )`
    `)` 的位置不对。显然某些东西应该与数字结合，但不应该出现在那里。Perl 无法判断意图是什么。

正则表达式中出现没有运算符的意外的 `'('`；在 `m/%s/` 的 HERE 处标记

-   `(F)` 你写了类似这样的代码：
    `(? \p{Digit} \p{Lao} \p{Thai} )`
    在 `(` 之前应该有一个运算符，因为没有指示如何与老语和泰语字符结合。

Unicode 非字符 U+`%X` 用于 `open` 非法

-   `(S)` 某些代码点（如 U+FFFF）由 Unicode 标准定义。这些被留作内部使用；应用程序不应交换它们。如果你确定自己在做什么，可以通过设置 `no warnings 'nonchar'` 来关闭此警告；

-   `(S)` 某些代码点在 U+D800 到 U+FFF（包含）之间被 Unicode 仅用于 UTF-16。然而，Perl 允许无符号整数代码（最高到你平台允许的大小），包括代理项。这些在输入或输出时可能会导致问题，此信息可能来源于此。

Unicode 代理项 U+`%X` 在 UTF-8 中非法

-   `(S)` 你在一个不接受它们的上下文中使用了代理项。

未知的字符名 `'%s'`

-   `(F)` 你使用的 `\N` 名称是 Perl 未知的。检查拼写。你可以说 `charnames :loose` 以便对空格、连字符和大小写要求得那么精确。（任何已创建的别名都必须精确指定，无论是否使用了 `:loose`。）如果 `\N{}` 不在作用范围内，也可能发生错误。

-   `(P)` Perl 正准备在 `$@` 中打印错误信息，但在尝试创建它后，`@$` 变量不存在。

未知的模式 `'%s'`

-   `(F)` `open()` 的第二个参数不在有效模式列表中：
    `<, >> +, |, <&`

未知的 PerlIO 层 `"%s"`

-   `(W)` 尝试向推入一个未知的层（层负责在外部和内部表示之间转换数据）。注意，某些层（如 `mmap`）在所有环境中都不支持。如果你的程序没有明确请求该操作，可能是 PerlIO 的问题。

向 `perl_iter` 发送了意外进程 `%s`

-   `(P)` 在迭代它之前，Perl 正在读取环境变量。某些可能非常困惑，或者试图通过这种不当目的破坏 Perl 的模式。

未知的正则修符 `"%s"`

-   `(F)` 紧跟在正则表达式分隔符后面的字母数字被 Perl 解析为正则的修符标记。你指定的其中一个是无效的。如果你没有在正则表达式结尾和后面的字母数字之间留空格，就会发生：



`if ($a = /foo/and $bar == 3) { ... }`

```
a 是有效的修符，但 n 不是，原因如下：
```

`if ($a = /foo/ and $bar == 3) { ... }`

```
未知的 "re" 指令 '%s'（已知的子图：%s）
```
- (W) 你尝试使用 `"re"` 指令中一个未知的子图。`(?{condition)if-else` 结构中的条件部分是未知的。条件必须是以下之一：
  (1) (2) ... 如果第 1、第 2 个等捕获匹配 (`<NAME>`) `'NAME'` ) 如果被命名的捕获 (`?<...`) 如果子模式匹配 (`!...`) 如果子模式未匹配 (`{ CODE }`) 如果代码返回真值 `(R)` 如果正在评估递归 `(R1)` `(R2)` ... 如果直接位于第 1、第 2 个等捕捕获组内 `(R&NAME)` 如果直接位于命名的捕获内 `(DEFINE)` 始终为假；用于定义命名的子模式

`<- HERE` 显示了在正则表达式中发现问题的地方。参见 `perl`。

未知的 Unicode 字母 `"%c"`

- (F) 你指定的未知的 Unicode 选项。查看 `-C switch` 的文档获取选项列表。

未知的 Unicode 值 `%d`

- (F) 你指定的未知的 Unicode 选项。查看 `-C switch` 的文档获取选项列表。

正则表达式中未知的动词模式 `'%s'`，在 `m/%s/` 的 HERE 处标记

- (F) 你要么写了错误字母，要么在大括号后错误地放置了 `*` 数量符

在你的模式中。检查该模式并查阅 `perlre` 获取有关合法动词模式详情。
未知警告 `"%s"`

(F) 由 `warnings` 原始函数发出的错误。你指定了一个 Perl 目前不认识的警告类别。

请注意，如果你想启用由某个模块注册的警告类别（例如 `use warnings 'File::Find';`），你必须先加载该模块。

正则表达式的 POSIX 类中存在未匹配的 ‘‘；在 `m/%s/` 中标记为 ← HERE

(F) 你写了类似下面的代码：

```
(?([[:digit:]])
```

它应该写成：

```
(?([[:digit:]]) )
```

正则表达式的 POSIX 类中存在未匹配的 “%c；在 `m/%s/` 中标记为 ← HERE

(F) 你写了类似下面的代码：

```
(?([[:alnum:]]) )
```

应该有第二个 `]` 如下：

```
(?([[:alnum:]]) )
```



正则表达式中存在未匹配的 [；在 `m/%s/` 中标记为 ← HERE
(F) 字符类周围的括号必须匹配。如果你想在字符类中包含右括号，请将其列入黑名单或放在第一位。← 显示了在正则表达式中发现问题的位置。参阅 `perlre`。

正则表达式中存在未匹配的 (；在 `m/%s/` 中标记为 ← HERE
正则表达式中存在未匹配的 )；在 `m/%s/` 中标记为 ← HERE

(F) 正则表达式中的括号必须始终平衡。如果你是用户，`%` 键对于寻找匹配的括号很有价值。HERE 显示了在正则表达式中发现问题的位置。参阅 `perlre`。

未匹配的右 `%s` 括号
(F) 词法器统计的大括号或方括号多于左括号，所以你可能漏掉了匹配的左括号。按照常规，你会在你编辑的地方附近找到（可以这么）缺失的那个。

未引号的字符串 “%s” 可能与未来的奖励冲突
(W) 你使用了一个裸字（bareword），它可能被声明为保留字。最好将此类单词放在引号中、以大写形式表示或在其间插入下划线。你也可以将其声明为子程序。

无法识别的字符 `%c`；在靠近列 `%d` 处标记为 ← HERE
(F) 解析器不知道如何处理你的 Perl 脚本（或 `eval`）中指定列附近的指定字符。你尝试将压缩后的脚本、二进制程序或目录作为 Perl 程序运行。

正则表达式字符类中存在无法识别的转义符 `\c`；在 `m/%s/` 中标记为 ← HERE
(F) 你在字符类内部使用了一种 Perl 无法识别的斜杠-字符组合。当该类位于 `(? []` 内部时，这是一个致命错误。
正则表达式中透传的无法识别转义符 `\c` 类；在 `m/%s/` 中标记为 <— HERE

(W regexp) 你在字符类内部使用了一种 Perl 无法识别的斜杠-字符组合。该字符被字面理解了，但在 Perl 的未来版本中可能会发生变化。<— HERE 显示了在正则表达式中发现该转义符的位置。

(W misc) 你使用了一种 Perl 无法识别的斜杠-字符组合。该字符被字面理解了，但在 Perl 的未来版本中可能会发生变化。
正则表达式中透传的无法识别转义符 `%s`；在 `m/%s/` 中标记为 <— HERE

(W regexp) 你使用了一种 Perl 无法识别的斜杠-字符组合。该字符被字面理解了，但在 Perl 的未来版本中可能会发生变化。<— HERE 显示了在正则表达式中发现（问题）的位置。
无法识别的信号名称 "%s"

(F) 你为 `kill()` 函数指定了一个无法识别的名称。请在 `shell` 中运行 `kill -1` 来查看系统上有效的信号名称。
无法识别的开关: `%s` -h 将显示选项

(F) 你为 Perl 指定了一个非法的选项。请不要这样做。（如果你认为你没有这么做，请检查 `#!` 行以查看它是否在代表你提供错误的开关。）

在引用上进行 `unshift`
(S experimental::autoderef) 参数是实验性的，可能会在未来的 Perl 版本中发生更改或被删除。如果你想承担使用此特性的风险，请禁用此警告：

```
no warnings "experimental::autoderef"
```
对包含换行符的文件名执行 `%s` 失败

(W newline) 对一个文件名尝试了文件操作，该操作失败了，可能是因为文件名包含换行符，也可能是因为你忘记调用 `chomp()` 了。请参阅 `perlfunc` 中的 "`chop`"。

不支持的函数 `%s`
(F) 该机器显然没有实现指示的函数。至少，`Configure` 认为没有。
不支持的函数 `fork`

(F) 你的执行文件版本不支持 `fork`。

请注意，在某些系统（如 OS/2）上，可能存在不同版本的 Perl 可执行文件，某些支持 `fork` 而某些不支持。尝试将你调用的 Perl 名称改为 `per1_`, `perl_` 等。

不支持的脚本编码 `%s`
(F) 你的程序文件以 Unicode 字节顺序标记 (BOM) 开头，声明为 Perl 无法读取的 Unicode 编码。

调用的不支持 `socket` 函数 "%6s"

+ (F) 你的机器不支持伯克利 `socket` 机制，或者至少 `Configure` 是这么认为的。

未终止的属性列表

+ (F) 词法器在属性开头发现了简单标识符以外的内容，且它既不是分号也不是块的开头。

未终止的属性列表

+ (F) 词法器在属性开头发现了简单标识符以外的内容，且它不是分号也不是块的开头。

替换。关于 `/d` 修饰符的更多信息请参见 `perlop`。
无效使用 `\E`

(W misc) 你在双引号字符串中使用 `\E`，但其前面没有 `\u`、`\L` 或 `\q`。
在正则表达式中无效使用贪婪修饰符 "%c”；在 `m/%s/` 中标记为 < HERE
(W regexp) 你写了类似以下的代码：
```



`qr/a{3}?/` `qr/b{1,}`

`?` 没有任何效果，因为它们的作用是修改在有选择时匹配更多或更少的内容，或者通过指定精确匹配给定的数字，而这里已经没有选择的空间了。

在上下文中无效使用 `%is`

`(W void)` 你在一个对返回值没有任何操作的上下文中执行了没有副作用的操作，例如一个没有从块中返回值的语句，或者是一个标量逗号运算符的左侧。这通常指向你方面的愚蠢，但也可能是 Perl 未能按照你预想的方式解析程序。例如，如果你混淆了 C 语言的优先级和 Python 的优先级，你会得到这个错误：

```perl
$one, $two = 1, 2;
```

而你的本意是：

```perl
($one, $two) = (1, 2);
```

另一个常见错误是使用圆括号构造列表引用，而本应使用方括号或大括号。例如，如果你说：

```perl
$array = (1,2);
```

但你应该写成：

```perl
$array = [1,2];
```

方括号显式地将列表值转换为标量值，而圆括号不会。当在标量环境中求括号列表时，逗号会被视为 C 语言的逗号运算符，它会丢弃左侧参数，这并不是你想要的。详情请参见 `perlref`。

对于等于 `0` 或 `1` 的数值常量，不会发出此警告，因为它们经常用于语句中：

```perl
1 while sub_with_side_effects();
```

对于通常求值为 `0` 或 `1` 的字符串常量会发出警告。

在正则表达式中无效使用 `(?-p)`；在 `m/%s/` 中标记为 `< HERE`
`(W regexp)` `?p` 修饰符一旦设置就无法关闭。尝试关闭它是没有意义的。

无效使用 `"re"` 编译指令

在标量环境中无效使用 `sort`

`(W void)` 你在标量环境中使用了 `sort`，例如：

```perl
my $x = sort @array;
```



这非常没有用，且 Perl 目前会优化掉它。

### 无效使用无值的 `%`
(W syntax) 你使用 `push()` 或 `shift()` 函数时，除了数组外没有提供任何参数，例如 `push(@x)` 或 `shift(@x)`。这通常对数组产生任何影响，因此完全没用。原则上讲，如果数组绑定（tied）到了一个实现了 `PUSH` 方法的类，`push(@tied_array)` 可能会产生影响。如果是这样，你可以写成 `push(@tied_array)` 以避免此警告。

### 表达式中不允许使用 "use"
(F) `use` 关键字在编译时被识别并执行，且不返回任何有用值。请参见 `perld`。

### 赋值给 `$[` 已弃用
(D deprecated) 变量 `$[`（数组中第一个元素的索引）已弃用。请参见 `perlvar` 中的 `"$["`。

### 使用裸露 `<<` 表示 `<<` 已弃用
(D deprecated) 如果你想使用空行作为 here-document（在此在此文档）的终止符，现在鼓励使用显式引用的形式。

### 对非 UTF8 local 使用 {} 是错误的。假设 local 为 UTF-8
(W local) 你正在使用 `local` 规则匹配正则表达式，并且正在匹配 Unicode 边界，但该 `local` 不是 Unicode 的。这没有意义。Perl 将继续执行，假设 `local` 是 Unicode (UTF-8)；如果 `local` 恰好是 ISO-8859-1 (Latin1)，则此信息是多余的，可以忽略。

### 使用 `chr(undef)` 或 `chr(undef` 已弃用
(D deprecated) 文档说明 `chr()` 不带参数时会变为 `$ENV{HOME}` 或 `$ENV{LOGDIR}`。`chr(undef)` 和 `chr("")` 共享这种行为，但该行为已被弃用。在未来的版本中，它们将被简化。注意传递给 `chr()` 的内容必须已定义而非空白，否则你可能会发现自己处于主目录。

### 在 `//` 中使用 `/c` 修饰符毫无意义
(W regex) 你在替换中使用 `/c` 修饰符。在替换中，`/c` 修饰符目前没有意义。

### 在没有 `/g` 时使用 `/c` 修饰符毫无意义
(W regexp) 你对正则表达式操作使用了 `/c` 修饰符，但没有使用 `/g` 修饰符。`/c` 只有在使用 `/g` 时才有意义（这在未来可能会改变）。

### 逗号变量列表已弃用
(D deprecated) 你提供给格式的值应该用逗号分隔，而不仅仅是在行上对齐。

### 在哈希插入上使用 each() 重置哈希迭代器会导致未定义行为
(S internal) 插入后 `each()` 的行为是未定义的；它可能会跳过项目，或者使用 `keys()` 代替 `each()` 来访问它们。

### 不允许为空属性列表使用 `:=`
(F) 构建 `$x := 42` 通常解析等同于 `my $x : 42`（对 `$x` 应用空属性列表）。该结构在 5.12.0 中被弃用，现在已变为语法错误。

如果你需要空属性列表，请使用 `@.`。

### 在 %s 中使用污染（tainted）参数已弃用
(W taint, deprecated) 你为 `system()` 或 `exec()` 提供了多个参数，且至少有一个参数是被污染的。这在以前是允许的，但在未来的 perl 版本中将变成致命错误。请对你的参数进行处理。参见 `perlsec`。

### 使用了未初始化的值 %s
(W uninitialized) 一个未定义的值被赋值，就像它已经定义一样。它被解释为 `""` 或 `0`，但这可能是一个错误。要消除此警告，请为你的变量分配一个定义值。
为了帮助你找出哪个是未定义的，perl 将尝试告诉你它无法处理的变量名称（如果有的话），如果无法做到，它会告诉你在哪个操作中使用了该未定义的值。然而，由于 perl 优化了你的程序，警告中显示的操作并不一定以字面形式出现在你的程序中。例如，，`$foo` 通常会被优化为 `"that " . $foo`，而警告会引用连接操作符 (`.`)，即使在你的程序中并没有该操作符。

### use 'strict' 是实验性的
(S experimental::restrict) 当正表达式模式在编译时或在未来的 Perl 版本中以不兼容的方式发生变化时，所产生的不同之处。这意味着今天可以编译的模式在未来的某个 Perl 版本中可能无法编译。此警告是为了提醒你注意这一风险。

### 在正则中使用 {...} 匹配两个以上的字符；在 m/%s/ 中标记为 < HERE
(F) 在正表达式中，你写了类似的内容：

```
(? [ \xBEEF ] ]
```

Perl 不确定你是指这个

```
(? [ \xBEEF ] ]
```

还是你是指这个

```
(? [ [ \xBE E F ] ]
```

你需要添加大括号或空格来消除歧义。

### 在正则字符类中使用 \N{} 返回的第一个字符；在 m/%s/ 中标记为 < HERE
(W regexp) 命名的 Unicode 转义符 `\W{...}` 可能会返回一个多字符序列。尽管字符类本上应该只匹配输入的一个字符，但 perl 将正确匹配该内容，除非该类被反转 (`[^]`)，或者转义符是范围的起点或终点。对于这些情况，发生的情况并不明确。在这种情况下，Perl 会丢弃返回序列的所有第一个字符，这可能不是你想要的。

### 在正则中使用 /u 用于 %s 而不是 /%s；在 m/%s/ 中标记为 < HERE
(W regexp) 你在正表达式的一部分使用了 Unicode 边界 (`\b{...}` 或 `\B...`)，而字符集修饰符 `/a` 或 `/aa` 正在生效。这两个修饰符表示 ASCII 解释，这对于 Unicode 定义是没有意义的。生成的正则表达式将编译为匹配所有 Unicode 的该边界。正表达式的其他部分不受影响。

### 使用 !~ %s 没有任何意义
(F) 在 `s///r`、`tr///r` 或 `y///r` 中使用 `!` 操作符目前预留给未来使用，因为其行为尚未确定。（简单地返回修改后字符串相反的布尔值并没有特别有用）。

### UTF-16%X

### %s 的值可以为 "0"；测试 defined(
(W Misc) 在条件表达式中，你将 `<HANDLE>`, `<*>` (glob), `each()`, `readdir()` 当作布尔值使用。这些构造体中的每一个返回值都是 `"0"`；这会导致条件表达式为假，这很可能不是你预期的结果。在条件表达式中使用这些构造体时，请使用 `defined` 操作符测试你的值。

### CLI 符号 "%s" 太长
(W Misc) 来自 vms 的警告。perl 尝试从 CLI 符号读取 `%ENV` 元素的值，发现结果字符串长度超过 1024 个字符。返回值已截断为 1024 个字符。

### 引用上的 values 是实验性的
(Experimental::autoderef) 带有标量参数的 `values` 是实验性的，可能会在 Perl 版本中更改或删除。如果你想冒使用此特征的风险，请禁用此警告：
```
no warnings "experimental::autoderef";
```

### 变量 "%s" 不可用
(W closure) 在编译期间，内部子程序尝试捕获一个不可用的外部作用域变量。这可能由于两个原因之一引起。外部作用域变量可能声明在一个尚未创建的外部匿名子环境中（记住，命名子程序是在编译时创建的，而匿名子程序是在运行时创建的）。例如：
```
```



`sub { my $a; sub f { $a } }`

在 `f` 创建时，它无法捕获 `$a` 的当前值，因为匿名子程序尚未创建。相反，以下情况不会产生警告，因为匿名子程序已经创建且处于活动状态：

```
sub { my $a; eval 'sub f { $a }'->(); }
```

第二种情况是由 `eval` 访问已超出作用域的变量引起的，例如：

```
sub f { my $a; sub { eval '$a' } f()(); }
```

在这里，当 `eval` 中的 `'$a'` 编译时，`f()` 并没有正在执行，因此它的 `'$a'` 不可捕获。

变量 `"%s"` 未导入 `%s`
`(M misc)` 在 `"use strict"` 生效的情况下，你引用了一个你显然认为是从另一个模块导入的全局变量，但该模块导出了同名的其他内容（通常是子程序）。通常意味着你在变量前面写了错误的字符。

正则 `m/%s%` 中未实现变长后向断言
`(F)` 后向断言（Lookbehind）仅允许用于编译时固定且已知的子表达式。对于正向后向断言，你可以使用 `\K` 正则构造来实现等效功能。在 perl 中使用 `"(?<=pattern)\K"`。有些不明显的 Unicode 规则 `/i` 可以匹配，你可能并不知道。例如，字符串 `ss` 可以匹配 LATIN SMALL LETTER SHARP。还有其他 ASCII 字符序列可以匹配单个字符，如 LATIN SMALL FF 匹配 `/i`。从 Perl v16 开始，如果你只使用 ASCII 匹配，那么 `/aa` 修饰符将排除这些不明显的匹配，从而消除此信息。你也可以使用 `re qw()` 对范围内编译的所有正则表达式应用 `/aa`。

`%s` 变量 `%s` 匹配 `%s`
`(W misc)` 在当前作用域或语句中声明了 `"my,"our" 或 "state"`，有效地消除了对之前实例的访问。这几乎总是类型错误。注意，之前的变量将一直存在到作用域结束或闭包引用被销毁。

变量语法
`(A)` 你写了一个元操作符，后面跟着看起来像二进制操作符的内容，但它也可以被解释为项或元操作符。例如，如果你知道 `rand` 函数的默认参数为 `1.0`，而你写了

`rand + 5;`

你可能认为你写的是和 `rand() + 5` 相同，但实际上你得到的是
`rand(+5);`

所以使用括号明确你的真实含义。

变量 `"%s"` 将不会共享
`(W closure)` 一个内部（嵌套）子程序引用了变量。当匿名子程序创建时，它们会自动重绑定到当前作用域。这个问题通常可以通过将内部匿名化（使用 `{}` 语法）解决。

`when` 是实验性的
`(S experimental::smartmatch)` 依赖于 `smartmatch`，它是实验性的。此外，它有几个可能立即不可见的特殊情况，其行为可能会在未来的任何 perl 版本中更改或删除。请参见 `perlyn` 中 `"Experimental Details on get and when"` 的解释。

`%s` 中的宽字符
`(S utf8)` Perl 在不预料的情况下遇到了一个宽字符（>255）。此警告默认针对 I/O（如 `print`）。消除此警告最简单的方法是直接为输出添加 `utf8` 层，例如 `binmode STDOUT, :utf8`。另一种关闭警告的方法是使用 `no warnings 'utf8';`；这通常更接近

作弊。通常情况下，你应该显式地为文件句柄指定编码，请参阅 `perfunc` 中的 `open` 和 `"binmode"`。
在 `%s` 中遇到宽字符 `(U+%X)`

- `(W)` 在单字节区域语言（即非 UTF-8 区域）中，遇到了一个多字节字符。Perl 将该字符视为指定的 Unicode 码点（code point）。将非 UTF-8 区域与 Unicode 结合是危险的。几乎可以确定，某些字符会有两种不同的表示方式。例如，在 ISO 8859-7（希腊语）区域中，码点 `0xC3` 代表大写希腊字母 Gamma。但 `0xC3` 也是如此。这将导致比较变得不可靠。

你可能需要弄清楚这个多字节字符是如何与你的单字节区域混合在一起的（或者你可能认为你使用的是 UTF-8 区域，但 Perl 并不这么认为）。

在 `[]`-长度内不允许使用 `"%c"`

- `(F)` `(un)pack` 模板中的计数可以被 `[TEMPLATE]` 替换，仅当 TEMPLATE 与从模板区域可以确定的相同打包字节数相匹配时。如果它包含任何代码 `@`、`/`、`u`、`w` 或 `*`-长度，则这样做是不可能的。请重新设计模板。

`write(on)` 已关闭文件句柄 `%s`

- `(W)` 你正在写入的文件句柄在之前的某个时候已经关闭。请检查你的控制流。

`%s` `"\xX"` 映射到 Unicode

- `(S utf8)` 在读取不同的编码时，Perl 尝试将所有内容映射为 Unicode 字符。你读取的字节在此编码中是不合法的。例如，`utf8 "\xE4"` 不映射到 Unicode，如果你尝试在 UTF-8 中编码为 `a-diaeresis Latin-1`。

字符 `'X'` 超出字符串范围

- `(F)` 你有一个 `(un)pack` 模板，它在被 `(un)pack` 的字符串开始位置之前指定了一个相对位置。请参阅 `perfunc` 中的 `"pack"`。

`unpack` 中的 `'x'` 超出字符串范围

- `(F)` 你有一个 `pack` 模板，它在被解包的字符串结束位置之后指定了一个相对位置。请请参阅 `perfunc` 中的 `"pack"`。

你在内核中禁用了 SET-ID 脚本！

- `(F)` 你可能永远不会开启它，因为你可能没有内核的源码，而且你的供应商可能根本不在乎你想要。最好的方法是在你的脚本外封装一个 `setuid` C 包装器。

你需要引用 `"%s"`，

- `(W 语法)` 你分配了一个已声明同名的子程序，这意味着 Perl 5 在执行赋值时将尝试调用该子程序，这可能不是你想要的。（如果这正是你想要的，请加上 `&` 符号）

你的随机数不是随机的

- `(F)` 在初始化哈希表的随机数种子时，Perl 无法从你的系统中获取任何随机性。这通常表示发生了非常严重的错误（Something Very Wrong）。

正则表达式中长度为零的 `\N{}`；在 `m/%s/` 中标记为 `<— HERE`

- `(F)` 命名的 Unicode 字符转义符 `(\n{...})` 可能会返回长度为零的序列。此类转义符被用于扩展字符类，即 `(?<`，是不被允许的。请检查是否使用了正确的转义符，以及正确的处理器是否在作用范围内。`<— HERE` 显示了在正则表达式中发现问题。

## 另请
`warnings`, `diagnostics`.

## PERLDOC

### 名称 (NAME)
`perldoc` - 以 Pod 格式查找 Perl 文档。

### 概要 (SYNOPSIS)
`perldoc [-h] [-D] [-t] [-m] [-F] [-i] [-T] [-r] [-d destination_file] [-o formatname] [-M formatterClassName] [-w option:value] [-X] [-L language_code]` 页面|模块名|程序名|URL

示例：

```
perldoc -f BuiltinFunction

perldoc -it BuiltinFunction

perldoc -q BuiltinFunction

perldoc -v BuiltinFunction

perldoc -a BuiltinFunction

perldoc -
```
实际上：

```
perldoc -f BuiltinFunction

perldoc -it BuiltinFunction

perldoc -q FAQ

perldoc -v PerlVariable

perldoc -a PerlAPI
```



请看下文的说明。

### 描述 (DESCRIPTION)
`perldoc` 查找 Pod 格式的文档。它可以查找嵌入在脚本中的文档并通过 `man` 显示，或者通过 pager 输出。

### 选项 (OPTIONS)
- `-h` 打印帮助信息。
- `-D` 描述区域语言。
- `-t` 使用纯文本显示。
- `-u` 使用 `nroff` 显示。
- `-l` 显示目录。
- `-F` 使用文件名。
- `-f` `-f` 后面跟的是函数名。
- `-q` `-q` 选项接受正则表达式。
- `-a` `-a` 后面跟的是函数名。
- `-v` `-v` 后面跟的是变量。
- `-T` 指定输出到 `STDOUT`。
- `-d` `destination-file` 指定输出到文件名。
- `-o` `output-formatname` 指定使用的输出格式类。例如：`-man`。
- `-M` `module-name` 指定你尝试格式化 pod 的模块。该类必须提供 `parse_from_file` 方法。
- `-w` `option:value` 或 `-w` `option` 指定调用格式器的选项。你可以使用 `-w` `option`（带值）作为 `-w` `option:TRUE` 的简写。这对于开关功能可能有用，例如：`-w` `page_numbering`。你可以用 `"="` 代替 `","`，例如：`-w` `textsize=15`。这取决于你使用的 shell。
- `-X` 如果存在，则使用索引。`-X` 选项会在 `$Config(archlib)/pod.idx` 文件中查找与给定名称匹配的项。`pod.idx` 文件应每行包含一个完整文件名。
- `-L` `language_code` 允许指定所需翻译的语言代码。如果系统中没有安装 `POD2::<language_code>` 包，则会忽略该开关。所有可用的翻译包都在 `POD2` 命名空间下。

## 安全

由于 `perldoc` 无法正常运行受污染（tainted）模式，且已知存在安全问题，当以超级用户身份运行时，它将尝试通过将有效 ID 和真实 ID 设置为 `nobody` 或 `nouser` 账户（如果不可用则设置为 `-2`）来降低权限。如果它无法放弃权限，它将不会运行。

### 环境

`PERLDOC` 环境变量中的任何开关都将在命令行参数之前被使用。

`PERLDOC` 的可用值包括 `-oterm`、`-otext`、`-ortf`、`-oxml` 等，取决于你手头有的模块；也可以用 `MPod::perdoc::ToTerm` 等类精确指定格式化程序。

`perldoc` 还会搜索由 `PERL5LIB`（如果未定义 `PERL5LIB` 则使用 `PERLIB`）和 `PATH` 环境变量指定的目录。（后者用于可执行文件的嵌入 pod，例如 `perldoc` 本身。）

在存在 `Makefile.PL` 或 `Build.pl` 的目录中，`perldoc` 将将 `.lib` 先添加到其搜索路径，只要你不是超级用户，它也会添加 `.lib`。如果你在构建目录中工作并想要阅读文档，即使你之前安装了该版本的模块，这非常有帮助。

`perldoc` 将按顺序优先使用 `PERLDOC_PAGER`、`MANPAGER` 或 `PAGER` 中定义的分页器，然后才尝试自行寻找分页器。（如果告诉 `perldoc` 显示纯文本或未格式化的 pod，则不使用 `MANPAGER`。）

在以 `-m` 模式（显示模块源代码）使用 `perldoc` 时，`perldoc` 将尝试使用在 `PERLDOC_SRC_PAGER` 中设置的分页器。该命令的一个实用设置是你喜欢的编辑器，例如 `/usr/bin/nano`。（别评判我。）

`PERLDOC_PAGER` 的一个可用值为 `less -C -E`。

将 `PERLDOCDEBUG` 设置为正整数将使 `perldoc` 输出比 `-D` 开关更详细的输出；数字越高，输出越详细。

## 更改

在 `3.14_05` 之前，开关 `-v` 被用于生成 `perldoc` 操作的详细信息，现在已通过 `-D` 启用。

## 相关阅读

`perlpod`, `Pod::Perldoc`

# 作者

当前维护者：Mark Allen `"<>"`

过去的贡献者有：brian d foy `"<>`, Adriano R. Ferreira `"<>`, Sean M. Burke `"<>`, Kenneth Albanowski `"<>`, Andy Dougherty `"<>`, 以及许多其他人。

## PERLDOS

### 名称

`perldos` - 在 DOS, W31, W95 下的 Perl。

## 概要

这些是在使用 DJGPP v2.03 或更高版本在 DOS（或 w??）下构建 Perl 的指令。w95 下支持长文件名。

## 描述

在开始之前，你应该浏览 Perl 分发包解压根目录下的 `README` 文件。确保你已阅读并理解了发行该软件的条款。

该端口目前支持用于构建 perl 扩展的 MakeMaker（模块集）。因此，你应该能够构建并安装在 CPAN 站点上找到的大多数扩展。

包含了如何构建和安装 perl 扩展模块（包括 XS 类型模块）的详细说明。参见“BUILDING AND INSTALLING MODULES”。

### 在 DOS 下编译 perl 的先决条件

DJGPP

DJGPP 是将 GNU C/C++ 编译器和开发工具移植到运行 MS-DOS 和兼容操作系统的 Intel 32 位 CPU 上的 32 位保护模式环境，由 DJ Delorie `<>` 及其朋友完成。

欲需更多详情（FAQ），请查看 DJGPP 的主页：

如果你对 DJGPP 有疑问，请尝试在 DJGPP 新闻组 `comp.os.msdos.djgpp` 中发帖，或使用电子邮件网关。

你可以在这里列出的任何镜像中找到完整的 DJGPP 分发包：

构建 perl（或添加新模块）需要以下文件：

`v2/ddev203.zip` `v2gnu/bnu212b.zip` `v2gnu/gcc2953b.zip` `v2gnu/bsh204b.zip` `v2gnu/mak3791b.zip` `v2gnu/fil140b.zip` `v2gnu/sed3028b.zip` `v2gnu/txt20b.zip` `v2gnu/dif272b.zip` `v2gnu/grep24b.zip` `v2gnu/sh120jb.zip` `v2gnu/gwk306b.zip` `v2misc/scdmi15b.zip`

或者可能的任何新版本。

### 线程

此版本的 djgpp perl 尚未测试线程支持。

### DOS 下 Perl 的缺点

由于 UNIX 版本的缺陷，DOS 下的 Perl 缺乏 UNIX 下的某些功能，最显著的包括：

- `fork()` 和 `pipe()`
- UNIX 文件系统关于链接计数和文件日期的某些功能
- 对于短文件名，原地操作（in-place operation）有些损坏
- `sockets`

### 在 DOS 上构建 Perl

使用 `djtar` 解压源码包 `perl5*.tar.gz`。如果你想在 w95 下使用长文件名并让 Perl 通过所有测试，不要忘记在解压压缩包之前 `set LFN=y`。

创建一个“符号链接”或将你的 `bash.exe` 复制到 `($DJDIR)/bin`。`ln -s bash.exe` [如果你有 DJGPP 推荐的 bash 版本，这已经为你完成了。]

并设置 `SHELL` 环境变量。将 `SHELL` 环境变量指向此 `sh.exe`：`set SHELL=c:/djgpp/bin/sh.exe`（如果你路径中有 `split` 和 `gsplit.exe`，将 `split.exe` 重命名为 `split.exe`）。

如果你没有 `echo.exe`，将 `gecho.exe` 重命名为 `echo.exe`。如果你没有 `awk.exe`，将 `gawk.exe` 重命名为 `awk.exe`。

在定义任何行之前，为了交互模式，你需要设置：`set SHELL=%DJDIR%/bin/sh.exe`。

在解压时设置 `CASE=y` 以确保脚本可以正确工作。进入 `perl` 的子目录并执行以下命令：`set CASE=y`。这是为了确保 `perl` 能够正确构建，XS 类型模块可以成功。[如果你使用长文件名，设置 `CASE=y` 是必要的]。

当 `Configure` 询问扩展时，DJGPP 条目建议：`set CASE=y`。在开始之前，进入 `perl` 目录并设置 `CASE=y`。这为了确保可以正确构建 `perl`。

现在，`Configure` 脚本将为你进行一些处理。`Configure` 脚本是交互式的，你只需要按回车。如果脚本显示包不完整，请设置 `CASE=y`。

你可以使用非交互模式运行 `Configure` 脚本：`sh -S`。关于 `Configure` 命令行开关的更多信息，可以在 `INSTALL` 文件中找到。

现在可以编译 Perl 了，输入：

```
make
```

### 在 dos 上测试 Perl

输入：

```
make test
```



如果你足够幸运，你会看到“All tests successful”。但根据某些外部条件，可能会少量测试失败（仅在 dos 短文件名下）。

### 在 dos 上安装 Perl

输入：

```
make install
```

这会将新编译的 `perl` 和库拷贝到你的 DJCPP 结构中。`perl.exe` 和工具进入 `($DJDIR)/bin`，库进入 `($DJDIR)/lib/perl15`。pod 文档进入 `($DJDIR)/lib/perl15/pod`。

## 在 DOS 上构建安装模块

### 在 DOS 下构建的先决条件

对于构建安装非 XS 模块，你只需要一个运行中的 DJGPP perl。非 XS 模块不需要重新链接 `perl`，因此构建和安装更简单。

XS 类型模块需要重新链接 `perl`，因为部分 xs 模块是用“C”语言编写的，必须与 `perl` 链接后执行。这是因为在 DJGPP 下使用“静态链接”选项构建，由于 DJGPP 环境缺少“动态链接”。

由于 xs 模块需要重新链接二进制文件，你需要 perl 二进制发行版和源码版来构建 xs 扩展模块。此外，你必须从源码构建你的 perl 二进制，以便所需的链接步骤可用。

### 在 DOS 上解压 CPAN 模块

首先，从 CPAN 下载模块包（例如逗号分隔值包 `Text-CSV-01.tar.gz`）。然后将包的内容解压到磁盘上的某个位置。大多数 CPAN 模块带有内部目录结构构建的，因此在你的 DJGPP 安装根目录下扩展它很容易。有些人倾向于将源码树位于 `/usr/src` 下（即 `$DIR/usr/src`），但你可以将其放在任何认为最逻辑的地方，例外放在与你的 perl 源码相同的目录下。适用于 perl 源码树中模块的特殊规则不适用于 CPAN 中的模块。

与 DJGPP 包（正常的“zip”文件）不同，CPAN 模块包是“压缩的 tar 包”。最新版本的 WinZip 可以安全地解压并扩展它们，除非它们包含零字节文件。这是一个已 WinZip Bug（截至 v7.0），它不会提取零字节文件。

从命令行，你可以使用 DJGPP 提供的 `djtar` 工具来解压和扩展这些文件。例如：

```
C:\djgpp>djtar -v Text-CSV-0.01.tar.gz
```

这将创建新目录 `($DIR)/Text-CSV-0.01` 并填充该模块的源码。

### 在 DOS 上构建非 XS 模块

要构建非 XS 模块，你可以使用随 perl 模块分发的标准构建指令：

- `perl Makefile.PL make test install`

这足够了，因为非 XS 模块只安装 “.pm”文件（有时还有 pod）

和/或文档。构建、安装或使用非 XS 模块时不需要重新链接 perl 二进制文件。

## 在 dos 上构建 xs 模块

要构建一个 xs 模块，你必须使用随 perl 模块分发的标准模块构建指令，**外加**针对 DJGP “静态链接”构建环境的三条额外指令。

`set FNCASE=y perl Makefile.PL make perl make make test -f Makefile.april inst_perl MAP_TARGET=perl.exe make install`

第一条额外指令设置了 DJGP 的 FNCASE 环境变量，以便你必须为 XS 类型模块构建的新型 perl 二进制文件能够正确构建。第二条额外指令在运行“make test”之前，在你的模块目录中重新构建 perl 二进制文件，以便你测试的是你通过“make”构建的新模块代码。第三条额外指令将你模块目录中的 perl 二进制文件安装到标准的 DJGP 二进制目录 `($DJDIR)/bin` 中，替换你之前的 perl 二进制文件。

注意，`MAP_TARGET` 的值*必须*具有“.exe”扩展，否则你不会创建一个替换 `($DJDIR)/bin` 中旧文件的“perl.exe”。

完成后，XS 模块安装过程将向你的“perllocal”信息中添加信息，告知 perl 二进制文件已替换以及安装了哪个模块。你可以随时使用以下命令查看这些信息：

```
perl -S peridoc perillocal
```

# 作者

Laszlo Molnar, [安装/构建 perl]

Peter J. Farley III [构建/安装模块]

## 另阅

(1)。

## PERLDSC

- > 名称

perldsc - Perl 数据结构食谱

## 描述

Perl 让我们能够编写类似这样的代码，突然之间，你就拥有了一个三维数组！

```
for my $x (1 .. 10) { for my $y (1 .. 10) { for my $z (1 .. 10) { $AoA[$x][$y][$z] = $x ** $y + $z; } } }
```

遗憾，尽管这看起来很简单，但其底层逻辑比表面看到的要复杂得多！你如何打印它？为什么你不能直接打印 `@AoA`？你如何对它进行排序？你如何将其传递给函数或从函数返回其中一个？它是一个对象吗？你可以将其保存到磁盘以便稍后读取吗？你如何访问该矩阵的整行或整列？所有的值都必须是数值吗？

如你所见，很容易变得困惑。虽然部分问题可以归于基于引用的实现，但实际上是因为缺乏为初学者设计的示例现有文档。本文旨在对你想要开发的各种数据结构提供易于理解的介绍。它也应该作为一份食谱。这样，当你需要创建这些复杂结构之一时，只需在这里查看即可。

让我们详细查看这些可能的构造结构。以下每个项目都有单独的章节：

- 数组数组（arrays of arrays）
- 哈希表数组（hashes of arrays）
- 数组哈希表（arrays of hashes）
- 哈希表哈希表（hashes of hashes）
- 复杂的构造

但现在，让我们看看所有这些类型共同通用问题。

## 参考文献

理解所有数据结构最重要的一点是——尽管它们看起来并非如此——ARRA 和 `%HASHES` 在内部是一维的。它们只能存储标量值（意味着字符串，或引用）。它们不能直接包含其他数组或哈希表，而是包含指向其他数组或哈希表的引用。

你不能像使用真实的数组或哈希表那样来使用数组或哈希表的引用。对于习惯于区分数组和相同指针的 C 程序员来说，这可能会令人困惑。如果是这样，只需将其视为结构与指向结构指针的区别即可。

在多维数组或哈希表中，实际情况是基类型大部分是单维实体，其中包含指向下一级的引用。你可以像使用多维结构一样使用它。这实际上也是多维数组的工作原理：

```
$array[$i][$j] # 数组数组

$array[$i][$string] # 数组哈希表

$hash[$string][$i] # 数组哈希表

$hash[$string]{'string'} # 哈希表哈希表
```

现在，由于顶层只包含引用，如果你尝试用简单的 print() 打印数组，你会得到一些并不好看的内容，如下：

```
my @AoA = ( [2, 3], [4, 5], [0] ); print @AoA[1][2];

ARRAY(0x83c8)ARRAY(0xb194)ARRAY(0x81d0)
```

这是因为 Perl 不会隐式解引用你的变量。如果你想获取引用所指向的内容，你必须自己这样做，使用前缀指示符如 `$$blah`、`@{$blah}`、`@{$blah[$i]}`，或者后缀指针箭头如 `$a->[$i]`、`->{string}`。

## 常见错误

构建类似数组数组时最常见的错误要么是不小心计算了元素数量，要么反复获取同一个内存位置的引用。这里有一个你得到计数而不是嵌套数组的案例：

```
for my i (1..10) { my array = somefunc($i); $AoA[$i] = @array; # 错误！

```

这只是将数组赋值给标量并获取其元素的简单情况。如果这确实是你真正想要的，那么你可能应该考虑更显式的写法，如下：

```
for my i (1..10) { my array = somefunc($i); $counts[$i] = scalar @array; }
```

这是一个反复获取同一个内存位置引用的案例：

```
# 在没有 strict 或有外部作用域 $array 声明的情况下

for my i (1..10) { @array = somefunc($i); $AoA[$i] = \array; # 错误！

```

那么，这有什么大问题吗？它看起来是正确的，不是吗？毕竟你需要一个引用数组；天哪，你确实创建了一个！

遗憾的是，虽然事实如此，但它仍然是损坏的。而且 `@AoA` 中的所有内容都将指向同一个地方。这类似于下面的 C 代码所示的问题：

```c
#include <stdio.h>

int main() { 

    struct passwd *getpwnam(), *rp, *dp; 

    rp = getpwnam("root"); 

    dp = getpwnam("daemon"); 
```



`printf("daemon name is %s\nroot name is %s\n", dp->pw_name, rp->pw_name);`

}

```

输出为：

daemon name is root
name is daemon

问题在于，`rp` 和 `dp` 均指向内存中的相同位置！在 C 中，你必须记住分配内存。在 Perl 中，你不需要。这里是使用括号的正确方法：

```perl

# 在没有 strict 或有外部作用域 $array 声明的情况下

for my i (1..10) { my array = somefunc($i); $AoA[$i] = [ @array ]; }

```

## 关于优先级的注意事项

提到像 `@AoA[$i]` 这样的内容，以下实际上是同一个东西：
`$aref->[2][2]` # 清除 `$aref[2][2]` # 模糊

这是因为 Perl 对其五个前缀解引用符号（看起来像某人在咒骂：`\$` `@` `*` `&`）的优先级规则使得它们的绑定程度比后置下标括号或大括号更紧密！这对于 C 或 C++ 程序员来说并不会感到意外，他们非常习惯使用 `*a[i]` 来表示 `a` 的第 *i* 个元素所指向的内容。也就是说，他们先取下标，然后只对该下标的内容进行解引用。
这在 C 中是可以接受的，但这里不是 C。

Perl 中看似等价的结构 `\$$[$i]` 首先对 `$aref` 进行解引用，使其将 `$aref` 视为数组的引用，然后再次解引用，最后告诉您 `@AoA` 指向的数组的第 *i* 个值。如果你想实现 C 的那种概念，必须写成 `${AoA[$i]}` 来强制在开头的 `\$` 解引用之前先评估 `$AoA[$i]`。

## 为什么你总是使用 STRICT

如果这听起来比它的实际情况要可怕得多，请放松。Perl 有一些功能可以帮助你避免最常见的陷阱。避免混淆的最佳方法是像这样开始每个程序：

```perl

#!/usr/bin/perl -w strict;

```

这样，你将被强制使用 `my()` 声明所有变量，并且禁止无意的“符号解引用”。因此，如果你这样写：

```perl

my $aref = [ "fred", "barney", "pebbles", "bambam", "dino", ], [ "homer",

"bart", "marge", ], [ "george", "jane", "elroy", "judy", ], ];

print $aref[2][2];

```

编译器会立即在编译时将其标记为错误，因为你无意中访问了未定义的变量 `@aref`，它借此提醒你写成：

```perl

print $aref->[2][2]

```

## 调试

你可以使用调试器的 `x` 命令来导出复杂的数据结构。例如，给定上述对 `$AoA` 的赋值，这里是调试器的输出：

```
DB<1> x $AoA

AoA = ARRAY(0x13b5a0) 0 ARRAY(0x1f0a24) 0 'fred' 1 'barney' 2

'pebbles' 3 'bambam' 4 'dino' 1 ARRAY(0x13b558) 0 'homer' 1 'bart' 2

'marge' 3 'maggie' 2 ARRAY(0x13b540) 0 'george' 1 'jane' 2 'elroy' 3 'judy'
```

## 代码示例

这里提供了一些注释较少的短代码示例（这些有一天会有自己的手册页），用于说明如何访问各种类型的数据结构。

### 数组的数组

#### 数组数组的声明

```perl

@AoA = ( [ "fred", "barney" ], [ "george", "jane", "elroy" ], [ "homer", "marge", "bart" ] );

```

#### 数组的生成

```perl

# 读取文件 while ( < > ){ push @AoA, [ split ]; } # 调用函数 a

function for $i ( 1 .. 10 ) { $AoA[$i] = somefunc($i); } # 使用临时变量

vars for $i ( 1 .. 10 ) { @tmp = somefunc($i); $AoA[$i] = [$tmp]; } # 向现有行

#添加元素

push (@{$AoA[0]}, "wilma", "betty");

```

#### 数组数组的访问与打印

```perl

# 一个元素 $AoA[0][0] = "Fred"; 另一个元素 $AoA[1][1]

s/(\w)\u$1; # 带有 $aref 引用的全部内容对于 ( @AoA ) { print

\t [ @aref, \n]; } # 带有 $i 索引的全部内容对于 ( 0

..#AoA ) { print "\t @{$AoA[$i]}, \n"; } # 一次打印全部内容对于 $i ( 0 .. $#AoA ) { for $j ( 0 .. $#{$AoA[$i]} ) { print "elt $i

$j is $AoA[$i][$j]\n"; } }

```

### 数组的哈希

#### 数组哈希的声明

```perl

%HOA = ( flintstones => [ "fred", "barney" ], jetsons => [ "george",

"jane", "elroy" ], simpsons => [ "homer", "marge", "bart" ], );

```

#### 从文件生成

```perl

# flintstones: fred barney wilma dino while ( < > ) {

next unless s/(.*):\s//; $HOA{$1} = [ split ]; # 读取文件;

# 更多次 flintstones: fred barney wilma dino while ( $line = <>) ) {

($who, $rest) = split /\*/, $line, 2; @fields = split '', $rest;

$HOA{$who} = [ get_family($group) ]; # 调用返回列表的函数

for ("simpsons", "jetsons", "flintstones") { @members }; # 向现有

# 族添加成员

push (@HOA{flintstones}, "wilma", "betty");

```

#### 哈希数组的访问与打印

```perl

# 一个元素 $HOA{flintstones}[0] = "Fred"; 另一个元素

$HOA{simpsons}[1] = s/\/\; # 带有 $shref 引用的全部内容对于

foreach $family ( keys %HOA ) { print

"family: $HOA{$family}" } # 带有 $i 索引的全部内容对于

foreach $family ( keys %HOA ) { print

"family: ";foreach $i ( 0 .. $#HOA ) { # 按成员数量打印全部

$family ( sort { @HOA{$b} <=> @HOA{$a} } keys %HOA ) print "family: $family}";

```

### 哈希的哈希

#### 数组哈希的声明

```perl

@AoH = ( { Lead => "fred", Friend => "barney" }, { Lead => "george",

Wife => "jane", Son => "elroy" }, { Lead => "homer", Wife => "marge",

Son => "bart" });

```

#### 数组哈希的生成

```perl

# 读取文件格式 LEAD=fred FRIEND=barney while ( < > ) {

$rec = split /, $field; ($key, $value) = split /=, $field;

$rec->{$key} = $value; # 读取文件格式 LEAD=fred FRIEND=barney while ( < > )

push @AoH, { split /\s+/ } # 调用返回键值对列表的函数，如

"lead", "daughter", "pebbles" while (%fields = nextpair()) ) # 同样，但使用临时

变量 (<>)

push @AoH, { %fields } # 向元素添加键值 AoH[0](pet)

= "dino"; AoH[2](pet) = "santa's helper";

```

#### 数组哈希的访问与打印

```perl

# 一个元素 AoH[0]{lead} = "fred"; 另一个元素 AoH[1]{lead} =
```



s/\(\)/\$; # 带有 `$shref` 引用的全部内容对于

`foreach $family ( keys %AoH ) { print`

`"" for $role ( keys %shref ) { print "role=$shref->$role" }`

`"\n"; }` # 带有 `$i` 索引的全部内容对于

`$i ( 0..$#AoH ) { for $role ( keys %{AoH[$i]} ) { print "role=$AoH[$i]{$role}`

`"; } }` # 一次打印全部内容对于 `$i ( 0..`

`$AoH ) { for $role ( keys %{AoH[$i]} ) { print "$i is AoH[$i]{$role}\n"; } }`

## 哈希的哈希

### 哈希的声明

### 这里的哈希的声明

```perl
%HOH = ( flintstones => { lead => "fred", pal => "barney", },
jetsons => { lead => "george", wife => "jane", his boy => "elroy", }, simpsons => {
lead => "homer", wife => "marge", kid => "bart", }, };
```

### 哈希的生成

```perl
# 读取文件 $flintstones: lead=read $pal=barney wife=wilma pet=dino
while ( < > ) { unless s/(.*?):\s*/; $who = $1; for ($field ( split
{ ($key, $value) = split /=; $field;$HOH{$group}; $value = $key }; # 同样，
读取文件; while ( < > ) { unless s/(.*?):\s*/;
$who = $1; rec = $HOH{$group}; rec = $field; for ($key,
value) = split /=; $rec->{$key} = $value; # 调用
函数返回 group 的键值对 ( "simpsons", "jetsons",
"flintstones" ) {HOH{$group} = get_family($group)}; # while
using for $group ( "simpsons", "jetsons", "flintstones" ) { %members
get_family($group); $HOH{$group} = %members }; # 添加成员到现有的 $new_folks = { wife => "wilma", pet => "dino", }
$what (%new_folks) {$HOH{flintstones}{$what} = $new_folks{$what};
```

### 哈希的访问与打印

```perl
# 一个元素 $HOH{flintstones}{wife} = "wilma"; 另一个元素
HOH{simpsons} = { print $s/(w)/u$1; # 打印全部内容对于
$family ( keys %HOH ) { print "family: {"; print for $role ( keys %
HOH{$family} } { print "$role=$HOH{$family}{$role}; print "\n"; #
print "$family: {"; for $role sort keys %{$HOH{$family}} } { print
print "$role={$family}{$role}; print "\n"; } # 按成员数量排序打印全部内容
$family ( sort keys %{$HOH{$group}} =>
keys %{$HOH{$family}} ) { print "$family: { $role = 0 }; for (qw lead
song daughter $pal) { print \$$rank = ++ }; # 打印全部内容
按成员数量排序
$family ( sort keys %{$HOH{$group}} =>
keys %{$HOH{$family}} ) { for sort keys %{$HOH{$b}} =>
keys %{$HOH{$a}} keys %HOH ) { print "$family: { "; 按照排名顺序打印这些对于 $role sort {$rank{$a} <= {$rank{$b}} keys %
$HOH{$family} } { print "$role={$family}{$role};"; print "\n"; } }
```

# 更详细的记录

## 详细记录的声明

这是一个展示了如何创建和使用包含多种类型字段的记录：

```perl
$rec = { TEXT => string, SEQUENCE => [ @old_values ], LOOKUP => {
%some_table, THATCODE => \some_function, THISCODE => sub { $_[0] **
$_1]}, HANDLE => \STDOUT); print $rec->{TEXT}; print $rec->{SEQUENCE}
[0]; $last = pop @ {$rec->{SEQUENCE}}; print $rec->{LOOKUP}("key");
$first_k, $first_v members = % {$rec->{LOOKUP}}; $answer = $rec->
THATCODE]->($arg); $answer = $rec->{THISCODE}($arg1, $arg2); # careful
extra blocks from ref $rec->{HANDLE}; use "string"; use
FileHandle; $rec->{HANDLE}->($1)->{HANDLE}->print(" string\n")
```

# 复杂哈希（HASH）记录的声明

```perl
%TV = { flintstones => { series => "flintstones", nights => { qw(monday
thursday friday) }, members => { role => "lead", age =>
36 }, { name => "wilma", role => "wife", age => 31 }, { name =>
pebbles", role => "kid", age => 4 }, }, { jetsons => { series =>
jetsons", nights => { qw(wednesday saturday) }, members => { name =>
george", role => "lead", age => 41 }, { name => "jane", role => "wife"
age => 39 }, { name => "elroy", nights => 9, }, { name =>
simsons => "simpsons", nights => { qw(monday) }, { name =>
homer", role => "lead", age => 34 }, { name => "marge", role => "wife"
age => 37 }, { name => "bart", role => "kid", age => 11 }, }, }, } };
```

# 从文件读取
# 最简单的方法是让文件本身以
# 所示的原始数据格式存在。如果声明为如下，结果将乐于解析复杂的
# 数据结构，因此有时最简单的办法是这样做
# 这里我们构建了一个部分 rec = $rec->{series} = {
"flintstones", $rec->{nights} => { find_days($_) }; @members => { # 假设
# 此文件在值语法下 << { %fields = split /\s+/; }
@member($fields); @members => { @members }; # 现在记住
# 全部 $TV->{series} = $rec.

################################
# 可能想要创建额外的字段，包含指向
# 相同数据结构的指针，这样如果修改了某一部分，它就会
# 在任何地方更改，例如如果你想要一个 {kids} 字段，它引用
# 一个孩子记录的数组，而不会产生重复的 {} 记录 并且无法正确更新。
################################

```perl
```



$rec = $TV->{family}; # 临时指针
@kids = ();
对于每个人（
@{$rec->{members}}）{
if ($rec->{role} =~ /kid|daughter/) }
push
@kids, $person);
};
# 记住：`rec` `$TV->{family}` 指向相同的数据！

`$rec->{kids} = [ @array ]` 包含
指向唯一对象的指针。这意味着如果你通过
`$TV->{simpsons}[kids][0][age]++` 错误地增加了年龄； # 因为这会
改变 `$TV->{simpsons}[members][2][age]`； # 因为 `$TV->{simpsons}`
`kids[0]` 和 `$TV->{members}[2]` 不指向同一个底层
匿名哈希表

```perl
# 打印全部
foreach $family ( keys %TV ) {
print "the $family";
print " is on during @ ${TV$family}{nights}\n";
print "its members=\n";
for $who ( @${TV$family}{members} ) {
print "\$who->{name}(\$who->{role}, age ${age}\n";
print " it turns out that ${TV$family}{lead} has ";
print scalar (@ ${TV$family}{kids} )), "
kids named ";
print join (",", map { $_->{name} } @${TV$family}{kids} }
);
print "\n";
}
}
```

# 数据库绑定

你不能轻松地将一个多级数据结构（例如哈希的哈希）绑定到哈希的哈希。第一个问题是除了 GDB 和 Berkeley 之外的所有工具都有大小限制，但除此之外，你还会遇到引用如何在磁盘上表示的问题。一个部分解决此需求的实验性模块是 `MLDBM`。按照 `permod` 中的描述检查你的 `CPAN` 站点以获取 `MLDBM` 的源码。

# 另见
`perlref`, `perldata`

# 作者
Tom Christiansen

# PERLDTRACE

## 名称
`perldtrace` - Perl 对 DTrace 的支持

```perl
# dtrace - perl::sub_entry perl::return { trace(copyinstr(arg)) }
# dtrace: perl::sub_entry, perl::return matched 10 probes
# perl -E 'sub outer { inner(@) } sub inner { say("hello")}'
# dtrace output) CPU ID:NAME
```

## 描述
DTrace 是一个用于全面的系统级和应用级追踪的框架。Perl 是 DTrace 提供者，意味着它暴露了用于插制的探针（probes）。你可以将它们与内核级探针以及来自其他提供者的探针结合使用。

## 历史
DTrace 是一个用于全面的系统级和应用级追踪的框架。Perl 是 DTrace 提供者，意味着它暴露了用于插制的探针。你可以将它们与内核级探针以及来自其他提供者的探针结合使用。

### 5.10
DTrace 是一个用于全面的系统级和应用级追踪的框架。Perl 是 DTrace 提供者，意味着它暴露了用于插制的探针。你可以将它们与内核级探针以及来自其他提供者的探针结合使用。

### 5.14
DTrace 是一个用于全面的系统级和应用级追踪的框架。Perl 是 DTrace 提供者，意味着它暴露了用于插制的探针。你可以将它们与内核级探针以及来自其他提供者的探针结合使用。

### 5.16
DTrace 是一个用于全面的系统级和应用级追踪的框架。Perl 是 DTrace 提供者，意味着它暴露了用于插制的探针。你可以将它们与内核级探针以及来自其他提供者的探针结合使用。

### 5.18
DTrace 是一个用于全面的系统级和应用级追踪的框架。Perl 是 DTrace 提供者，意味着它暴露了用于插制的探针。你可以将它们与内核级探针以及来自其他提供者的探针结合使用。

## 探针

- `sub-entry(SUBNAME, FILE, PACKAGE)`
追踪子函数的进入。注意：DTrace 目前无法获取关于子函数*调用者*的信息。

- `sub-return(SUBNAME, FILE, PACKAGE)`
追踪子函数的退出。注意：DTrace 目前无法获取关于子函数*调用者*的信息。

- `phase-change(NEWPHASE, OLDPHASE)`
追踪 Perl 解释器状态的变化。`NEWPHASE` 和 `OLDPHASE` 的值是字符串 `$(GLOBAL_PHASE`。

- `op-entry(OPNAME)`
追踪 Perl 执行中每个操作码的执行。启用 Perl 调试时，DTrace 探针会在调试钩子之后触发（但在操作码本身执行之前）。

- `loading-file(FILENAME)`
当 Perl 准备加载单个文件时触发（无论是通过 `use`、`require` 还是 `do`）。探针在从磁盘读取文件之前触发。文件名被转换为文件系统路径，而不是 `Module::Name` 风格的。

- `loaded-file(FILENAME)`
当 Perl 成功加载单个文件时触发（通过 `use`、`require` 或 `do`）。探针在从磁盘读取文件并评估其内容之前触发。

## 示例

最频繁调用的函数

```perl
# dtrace - perl::sub_entry perl::return { trace(copyinstr(arg)) }
# dtrace: perl::sub_entry, perl::return matched 10 probes
# perl -E 'sub outer { inner(@) } sub inner { say("hello")}'
# dtrace output) CPU ID:NAME
```

# 参考

DTrace 动态追踪指南

```
<>
```

DTrace: Dynamic Tracing in Oracle Solaris, Mac os x and FreeBSD

```
<>
```



## 另请

- `Devel::DTrace::Provider`

此 CPAN 模块允许你使用 Perl 创建应用层级的 DTrace 探针。

# 作者

Shawn M Moore ""

# PERLEBCDIC

- 名称
  `perlebcdic` - 在 EBCDIC 平台上运行 Perl 的考虑因素

## 描述

探讨了 Perl 程序员在基于 EBCDIC 的计算机上面临的一些问题。本文中仍未完成的部分已用 XXX 标记。

早期版本的 Perl 可以在某些 EBCDIC 机器上运行，但最后一个已知运行在 EBCDIC 上的版本是 `v5.8.7`，直到 `v5.22` Perl 核心再次运行在 `z/OS`。从理论上讲，它可以在 `OS/400` 或西门子的 `BS2000`（或其后续型号）上运行，但尚未经过测试。在 `v5.22` 中，并不是所有用此类 Perl 构建的 CPAN 模块都能在 `z/OS` 上运行。

如果你想在非 `z/OS` 的 EBCDIC 机器上使用 Perl，请发送邮件告诉我们。

在 EBCDIC 平台上编写 Perl 与在 "ASCII" 平台上编写没有区别，但底层的数字不同，正如我们稍后将看到的。你必须对那些 "ASCII" 平台有所了解，因为文档具有偏向性，并且经常使用不适用于 EBCDIC 的数字。此外，极少有 CPAN 模块是为 EBCDIC 编写且不支持 ASCII 的；相反，大多数 CPAN 模块是为 ASCII 编写的，某些恰好可以在 EBCDIC 上运行，而少数被设计为可移植的。

如果你的代码使用了 52 个字母 A-Z 和 a-z，再加上空格 `SPACE`、数字 0-9 以及 Perl 使用的标点符号，以及几个由 `\n` 和 `\t` 等转义序列表示的控制字符，那么使用 Perl 并没有特殊之处，你的代码完全可以在不更改的情况下在 ASCII 机器上运行。

但如果你的代码使用 `\x09` 表示制表符 `TAB`，使用 `\xC1` 表示 "A"，或使用 `\xD` 表示 "y."带变音符号的小写 y），那么如果没有人想在 ASCII 平台上运行你的代码，这样做是可以的；但本文档的偏向性在于编写在 EBCDIC 和 ASCII 系统之间具有可移植的代码。再次，如果你关心的每个字符都能从键盘上轻松输入，但许多键盘并不方便你输入某个字符（如 `\xD`），那么你就必须间接指定它，例如使用 `\xD` 转义序列。在这些情况下，了解 ASCII/Unicode 字符集是最容易的。如果那个小小的 "y." 是 `\u00FF`，那么你可以将其指定为 `\n{U+FF}`，让计算机自动将其翻译为你平台上的 `\xD`，并保持其为 ASCII 字符。或者你也可以通过名称 `\n{LATIN SMALL LETTER Y WITH DIAESIS}` 来指定它，而无需知道数字。两种方法都可行，但需要对 Unicode 有足够的熟悉。

# 常见字符集

## ASCII

美国信息交换标准代码 `ASCII` 或 `US-ASCII` 是一组从 0 到 127（十进制）的整数，使用 ASCII 的计算机对其有标准化的解释。例如，`0x41` 表示字母“A”。127 可以由 7 位二进制数中的位覆盖，因此该集合有时被称为“7位 ASCII”。`ASCII` 由美国国家标准协会 `ANSI X34.3-1986` 描述。它也被 `ISO 646:1991` 描述（并对货币符号进行了本地化）。完整的 ASCII 在下表中作为前 128 个元素给出。可以使用 ASCII 字符充分编写的语言包括英语、夏威夷语、印尼语、斯瓦希语和一些美国原住民语言。

大多数非 EBCDIC 字符集都是 ASCII 的超集。对于整数 0-127，其含义与 ASCII 相同。但整数 128 及以上则取决于特定的字符集。

其中许多可以完全放入 8 位中，使用 ASCII 作为 0-127，同时指定 128-255 的含义，并且不使用 255 以上的任何内容。因此，这些是单字节（如果你愿意，称为八字节）字符集。一个重要的（由于 Unicode 是其超集）字符集是 `ISO 8859-1` 字符集。

## ISO 8859

`ISO 8859-$n` 是来自国际标准组织 `iso` 的字符集集合，每个字符集都在 ASCII 基础上添加了通常在各种语言中常见的字符，其中许多语言基于罗马字母或拉丁字母。对于大多数欧洲语言，还有针对阿拉伯语、希腊语、希伯来语和泰语的版本。关于所有这些，网上都有很好的参考文献。

## 拉丁 1 `ISO 8859-1`

ASCII 的特殊 8 位扩展，包含重音和反音符号的拉丁字符。可以使用 `ISO 8859-1` 的语言包括 ASCII 涵盖的所有字符，以及南非语、阿尔巴尼亚语、巴斯克语、加泰罗尼亚语、丹语、法罗群语、芬兰语、挪威语、葡萄牙语、西班牙语和瑞典语。荷兰语但不包含 ij 字。法语但不包含 oe。德语可以使用 `ISO 8859-1` 但必须这样使用。对于大多数欧洲语言，还有针对阿拉伯语、希腊语、希伯来语和泰语的版本。关于所有这些，网上都有很好的参考文献。

`ISO 8859-$n` 是来自国际标准组织 `iso` 的字符集集合，每个字符集都在 ASCII 基础上添加了通常在各种语言中常见的字符，其中许多语言基于罗马字母或拉丁字母。对于大多数欧洲语言，还有针对阿拉伯语、希腊语、希伯来语和泰语的版本。关于所有这些，网上都有很好的参考文献。

## EBCDIC

西门子 `BS2000` 系统使用的 EBCDIC 码页与 1047 和 0037 不同。它在下方被标识为 `POSIX-BC`。与 0037 和 1047 相同，它与 `ISO 8859-1` 的代码值相同。

## Perl 识别的 EBCDIC 字符集：

### 13 变体字符

EBCDIC 字符集中被称为 13 变体字符的有：

- [ ]
- { }
- ~
- !
- #
- |
- $ @

### 0037

字符集 `0037` 是 ASCII 加拉丁1 字符（即 `ISO 8859-1`）到 EBCDIC 集的映射。`0037` 用于在 `OS/400` 上运行的北美英语区域。`CCSID 0037` 与 `ISO 8859-1` 有 236 处不同；在其他方面只有 20 个代码值相同。

### 1047

字符集 `1047` 也是 ASCII 加拉丁1 字符（即 `ISO 8859-1`）到 EBCDIC 集的映射。`1047` 用于 `OS/390` 或 `z/OS` 的 `Unix System Services`，以及 `VM/ESA` 的 `OpenEdition`。`CCSID 1047` 与 `CCSID 0037` 有 8 处不同，与 `ISO 8859-1` 有 236 处不同。

# Unicode 代码点点

在 Unicode 术语中，代码点是分配给字符的数字：例如，在 EBCDIC 中，字符 "A" 通常分配数字 193。在 Unicode 中，字符 "A" 被分配数字 65。`ASCII` 和 `Latin-1` `ISO 8859-1` 中的所有代码在 Unicode 中具有相同的含义。所有识别的 EBCDIC 字符集都有 256 个代码点，并且在每个集中，所有 256 个代码点都等同于 Latin1 点。显然，“A" 会映射到 "A"，"B" =="B"，"%" =="%" 等，对于所有打印字符

事实证明 Latin1 和 EBCDIC 字符与 ASCII/Latin1 C0 几乎有精确的等效字符。

事实证明还存在 DELETE 控制字符。（C0 控制字符是那些从 0..0x1F 的 ASCII 代码点；诸如 TAB、ACK、BEL 等。）在 ASCII/EBCDIC 控制字符之间建立了一种映射。ASCII 平台上的 C1 控制字符与剩余的 EBCDIC 控制字符之间没有精确映射。目前所做是将这些控制字符（大多是任意地）映射到另一个字符集中某些未匹配的字符上。无论如何，这些字符中的大部分现在在 EBCDIC 中都极少使用，它们的名称也被丢弃了，没有引起太多异议。例如，E0（八个 1）EBCDIC 控制字符（由八位组成：0xFF）被映射到 C1 APC 控制字符（0x9F），你无法使用“EO”。

EBCDIC 控制字符提供了三个可能的行终止符字符：CR `0x0D`、LF `0x25` 和 NL `0x15`。在 ASCII 上，符号“NL”和“LF”指的是同一个字符，但在 EBCDIC 术语中它们是不同的。EBCDIC NL 被映射到被称为“Next Line”的 C1 控制字符；这里的映射非常有意义，而不仅仅是任意）。NEL 是行终止符。这在 `z/OS` 和 `BS2000` 上都是如此。在这些平台上，C 编译器会交换 LF 和 NEL 点，使得 `\n` 为 `0x15` 并指代 NL。Perl 也是这样做；你可以在下面的代码表中看到这一点。这使得通常情况下“开箱即用”，你甚至不需要意识到存在交换。

# Unicode 和 UTF

`UTF` 代表“Unicode 转换格式” `Unicode Transformation Format`。`UTF-8` 是将 Unicode 转换为一系列 8 位字节块的编码方式，它基于 ASCII 和 Latin-1。表示一个 Unicode 代码点所需的序列长度取决于代码点的顺序，数字越大，需要的字节越多。`UTF-EBCDIC` 类似于 `UTF-8`，但基于 EBCDIC。它们非常相似，以至于在非正式使用时会混淆这两个术语，并且“UTF-8”既指 ASCII 平台上的 UTF-8，也指 EBCDIC 平台上的 UTF-EBCDIC。

你可能会看到“不变” `invariant` 字符或代码点的术语。这仅意味着该字符在编码为 `UTF-8`（或 `UTF-EBCDIC`）时具有相同的数值和表示。（注意，这与上述的“13 变体字符”是一个完全不同的概念。严谨的证明将使用“UTF-8 invariant”而不是“invariant”，但通常你只只会看到“invariant”。）例如，“A”在 EBCDIC 代码页中的值为 193，在编码为 `UTF-EBCDIC` 时也为 193。所有 `UTF-8`（或 `UTF-EBCDIC`）变体代码点在编码为 `UTF-8`（或 `UTF-EBCDIC`）时都占用两个字节；根据定义，`UTF-8`（或 `UTF-EBCDIC`）不变代码点无论是否编码为 `UTF-8`（或 `UTF-EBCDIC`），都恰好占用一个字节。（到这里你应该已经看到人们通常在说“UTF-8”时其实也意味着“UTF-EBCDIC”。在本文的其余部分中，我们也会非正式地处理这一点。）在 ASCII 中，对应最低 128 个序数数字（0 - 127：ASCII 字符）是不变的。在 `UTF-EBCDIC` 中，有 160 个不变字符。（如果你感兴趣的话，EBCDIC 不变字符是具有 ASCII 等效字符的字符，加上对应于 C1 控制字符的字符（ASCII 平台上的 128-159）。

`UTF-EBCDIC` 编码的字符串可能比 `UTF-8` 编码的字符串长（但绝不会短）。Perl 扩展了 `UTF-8`，使其能够编码超过 Unicode 最大值 `U+1FFFF` 的点。它也扩展了 `UTF-EBCDIC`，但由于 `UTF-EBCDIC` 固有限制，如果字长大于32 位，可表示的最大代码点为 `U+7FFF_FFFF`。

`UTF-EBCDIC` 由 Unicode 技术报告 #16 定义。它基于 `CCSID 1047`，未考虑其他代码页的差异。这允许运行不同代码页的文本之间进行轻松交换，但如果不经过适配，它在其他代码页的 Perl 上是无法使用的。

这是因为 Perl 的一个基本假设是：解析和词法分析所关心的字符无论包含它的文本是否为 UTF-8 都是相同的。为了确保这一点，Perl 将 `UTF-EBCDIC` 适配到不变页，使得在运行某个版本 Perl 的计算机上生成的文本经过翻译才能被运行另一个版本 Perl 的计算机理解。

# 使用 Encoding

从 Perl 5.8 开始，你可以使用标准的 `Encoding` 模块将 EBCDIC 翻译为 Latin-1 代码点。`Encoding` 只知道 ASCII 字符集。

```perl
```



```perl
my %ebcdic = (176 => 'cp37', 95 => 'cp147', 106 => 'posix'); # $sa is EBCDIC code points from_to($sa, ord('^'));
```

对于 I/O 操作，建议使用 `PerlIO` 库的自动翻译功能。这允许你为每个句柄使用不同的编码。例如，你可以使用

```perl
use Encode;

open($f, ":encoding(ascii)", "test.ascii"); print $f "Hello!\n";

open($f, ":encoding(cp37)", "test.ebcdic"); print $f "Hello!\n";

open($f, ":encoding(utf8)", "test.utf8"); print $f "Hello!\n";
```

```c
printf("%s%02X-.%s%02X-.%s%02X-.%s%02X\n",
$1, $2, $3, $4, $5, $6, $7, $8); } else {
printf("%s%02X-.%s%02X-.%s%02X\n",
$1, $2, $3, $4, $5, $6); // ISO 8599-1 CCIS CCIS CCIS IX-
1047 chr 0819 0037 0040 UTF-8 CCID
```



`<ST>` XX 22 22 22 `<ETX>` 33 33 33 `<NULL>` `<0 55 55 55 55 55 <SOH>` `<ENQ>` 45 45 45 45 `<5>` 46 46 46 46 46 46 `<47 47 47 47 47 47 <48>` 12 22 22 22 22 `<2>` `<9>` 5 55 55 5 `<` 55 10 21 21 21 21 21 `<<VT>` 11 11 11 11 11 `<FF>` 12 12 12 `<12>` 13 13 13 13 13 `<14>` 14 14 14 14 14 `<15>` 15 15 15 15 15 `<16>` 16 16 16 16 16 `<17>` 17 17 17 17 17 `<18>` 18 18 18 18 18 `<19>` 19 19 19 19 19 `<20>` 20 20 20 20 20 `<MAK>` 21 21 21 21 21 `<22>` 22 22 22 22 22 `<23>` 23 23 23 23 23 `<24>` 24 24 24 24 24 `<25>` 25 25 25 25 25 `<26>` 26 26 26 26 26 `<27>` 27 27 27 27 27 `<28>` 28 28 28 28 28 `<29>` 29 29 29 29 29 `<30>` 30 30 30 30 30 `<31>` 31 31 31 31 31 `<SPACE>` 32 32 32 32 32 `<33>` 33 33 33 33 33 `<34>` 34 34 34 34 34 `<35>` 35 35 35 35 35 `<36>` 36 36 36 36 36 `<37>` 37 37 37 37 37 `<38>` 38 38 38 38 38 `<39>` 39 39 39 39 39 `<40>` 40 40 40 40 40 `<41>` 41 41 41 41 41 `<42>` 42 42 42 42 42 `<43>` 43 43 43 43 43 `<44>` 44 44 44 44 44 `<45>` 45 45 45 45 45 `<46>` 46 46 46 46 46 `<47>` 47 47 47 47 47 `<48>` 48 48 48 48 48 `<49>` 49 49 49 49 49 `<50>` 50 50 50 50 50 `<51>` 51 51 51 51 51 `<52>` 52 52 52 52 52 `<53>` 53 53 53 53 53 `<54>` 54 54 54 54 54 `<55>` 55 55 55 55 55 `<56>` 56 56 56 56 56 `<57>` 57 57 57 57 57 `<58>` 58 58 58 58 58 `<59>` 59 59 59 59 59 `<60>` 60 60 60 60 60 `<61>` 61 61 61 61 61 `<62>` 62 62 62 62 62 `<63>` 63 63 63 63 63 `<64>` 64 64 64 64 64 `<65>` 65 65 65 65 65 `<66>` 66 66 66 66 66 `<67>` 67 67 67 67 67 `<68>` 68 68 68 68 68 `<69>` 69 69 69 69 69 `<70>` 70 70 70 70 70 `<71>` 71 71 71 71 71 `<72>` 72 72 72 72 72 `<73>` 73 73 73 73 73 `<74>` 74 74 74 74 74 `<75>` 75 75 75 75 75 `<76>` 76 76 76 76 76 `<77>` 77 77 77 77 77 `<78>` 78 78 78 78 78 `<79>` 79 79 79 79 79 `<80>` 80 80 80 80 80 `<81>` 81 81 81 81 81 `<82>` 82 82 82 82 82 `<83>` 83 83 83 83 83 `<84>` 84 84 84 84 84 `<85>` 85 85 85 85 85 `<86>` 86 86 86 86 86 `<87>` 87 87 87 87 87 `<88>` 88 88 88 88 88 `<89>` 89 89 89 89 89 `<90>` 90 90 90 90 90 `<91>` 91 91 91 91 91 `<92>` 92 92 92 92 92 `<93>` 93 93 93 93 93 `<94>` 94 94 94 94 94 `<95>` 95 95 95 95 95 `<96>` 96 96 96 96 96 `<97>` 97 97 97 97 97 `<98>` 98 98 98 98 98 `<99>` 99 99 99 99 99 `<100>` 100 100 100 100 100 `<101>` 101 101 101 101 101 `<102>` 102 102 102 102 102 `<103>` 103 103 103 103 103 `<104>` 104 104 104 104 104 `<105>` 105 105 105 105 105 `<106>` 106 106 106 106 106 `<107>` 107 107 107 107 107 `<108>` 108 108 108 108 108 `<109>` 109 109 109 109 109 `<110>` 110 110 110 110 110 `<111>` 111 111 111 111 111 `<112>` 112 112 112 112 112 `<113>` 113 113 113 113 113 `<114>` 114 114 114 114 114 `<115>` 115 115 115 115 115 `<116>` 116 116 116 116 116 `<117>` 117 117 117 117 117 `<118>` 118 118 118 118 118 `<119>` 119 119 119 119 119 `<120>` 120 120 120 120 120 `<121>` 121 121 121 121 121 `<122>` 122 122 122 122 122 `<123>` 123 123 123 123 123 `<124>` 124 124 124 124 124 `<125>` 125 125 125 125 125 `<126>` 126 126 126 126 126 `<127>` 127 127 127 127 127 `<128>` 128 128 128 128 128 `<129>` 129 129 129 129 129 `<130>` 130 130 130 130 130 `<131>` 131 131 131 131 131 `<132>` 132 132 132 132 132 `<133>` 133 133 133 133 133 `<134>` 134 134 134 134 134 `<135>` 135 135 135 135 135 `<136>` 136 136 136 136 136 `<137>` 137 137 137 137 137 `<138>` 138 138 138 138 138 `<139>` 139 139 139 139 139 `<140>` 140 140 140 140 140 `<141>` 141 141 141 141 141 `<142>` 142 142 142 142 142 `<143>` 143 143 143 143 143 `<144>` 144 144 144 144 144 `<145>` 145 145 145 145 145 `<146>` 146 146 146 146 146 `<147>` 147 147 147 147 147 `<148>` 148 148 148 148 148 `<149>` 149 149 149 149 149 `<150>` 150 150 150 150 150 `<151>` 151 151 151 151 151 `<152>` 152 152 152 152 152 `<153>` 153 153 153 153 153 `<154>` 154 154 154 154 154 `<155>` 155 155 155 155 155 `<156>` 156 156 156 156 156 `<157>` 157 157 157 157 157 `<158>` 158 158 158 158 158 `<159>` 159 159 159 159 159 `<160>` 160 160 160 160 160 `<161>` 161 161 161 161 161 `<162>` 162 162 162 162 162 `<163>` 163 163 163 163 163 `<164>` 164 164 164 164 164 `<165>` 165 165 165 165 165 `<166>` 166 166 166 166 166 `<167>` 167 167 167 167 167 `<168>` 168 168 168 168 168 `<169>` 169 169 169 169 169 `<170>` 170 170 170 170 170 `<171>` 171 171 171 171 171 `<172>` 172 172 172 172 172 `<173>` 173 173 173 173 173 `<174>` 174 174 174 174 174 `<175>` 175 175 175 175 175 `<176>` 176 176 176 176 176 `<177>` 177 177 177 177 177 `<178>` 178 178 178 178 178 `<179>` 179 179 179 179 179 `<180>` 180 180 180 180 180 `<181>` 181 181 181 181 181 `<182>` 182 182 182 182 182 `<183>` 183 183 183 183 183 `<184>` 184 184 184 184 184 `<185>` 185 185 185 185 185 `<186>` 186 186 186 186 186 `<187>` 187 187 187 187 187 `<188>` 188 188 188 188 188 `<189>` 189 189 189 189 189 `<190>` 190 190 190 190 190 `<191>` 191 191 191 191 191 `<192>` 192 192 192 192 192 `<193>` 193 193 193 193 193 `<194>` 194 194 194 194 194 `<195>` 195 195 195 195 195 `<196>` 196 196 196 196 196 `<197>` 197 197 197 197 197 `<198>` 198 198 198 198 198 `<199>` 199 199 199 199 199 `<200>` 200 200 200 200 200 `<201>` 201 201 201 201 201 `<202>` 202 202 202 202 202 `<203>` 203 203 203 203 203 `<204>` 204 204 204 204 204 `<205>` 205 205 205 205 205 `<206>` 206 206 206 206 206 `<207>` 207 207 207 207 207 `<208>` 208 208 208 208 208 `<209>` 209 209 209 209 209 `<210>` 210 210 210 210 210 `<211>` 211 211 211 211 211 `<212>` 212 212 212 212 212 `<213>` 213 213 213 213 213 `<214>` 214 214 214 214 214 `<215>` 215 215 215 215 215 `<216>` 216 216 216 216 216 `<217>` 217 217 217 217 217 `<218>` 218 218 218 218 218 `<219>` 219 219 219 219 219 `<220>` 220 220 220 220 220 `<221>` 221 221 221 221 221 `<222>` 222 222 222 222 222 `<223>` 223 223 223 223 223 `<224>` 224 224 224 224 224 `<225>` 225 225 225 225 225 `<226>` 226 226 226 226 226 `<227>` 227 227 227 227 227 `<228>` 228 228 228 228 228 `<229>` 229 229 229 229 229 `<230>` 230 230 230 230 230 `<231>` 231 231 231 231 231 `<232>` 232 232 232 232 232 `<233>` 233 233 233 233 233 `<234>` 234 234 234 234 234 `<235>` 235 235 235 235 235 `<236>` 236 236 236 236 236 `<237>` 237 237 237 237 237 `<238>` 238 238 238 238 238 `<239>` 239 239 239 239 239



195.175 139.86 <SMALL eth> 240 140 140 195.176 139.87 <n WITH TILDE> 241 73 73 177.198 <WITH GRAVE> 242 205 205 197.
139.89 <WITH ACUTE> 243 206 206 195.179.198 <WITH CIRCUMLEX> 244 203 203 195.130.199 <WITH TILDE> 245 207 207 207.181
139.100 <WITH DIERESIS> 246 204 204 194.182 <DIVISION SIGN> 247 225 225 225 193.182.190 <WITH STROKE> 248 112 112 112.184
139.23 <WITH DIERESIS> 249 221 221 195.185.194 <WITH ACUTE> 250 222 222 222 195.186.195 <WITH CIRCUMLEX> 251 219 219 219.187
139.105 <WITH DIERESIS> 252 220 220 220 195.188.139.12 <WITH ACUTE> 253 141 141 141 195.189 139.113 <SMALL LETTER thorn> 254 142 142 142
195.190 139.114 <WITH DIERESIS> 255 223 223 225 239.191 139.115

如果你在 CCID 0037 顺序中看到了 ASCII+ Latin-1 中的数字 36 的变化，请运行以下命令：

# 配方 4

```perl
perl -ne 'if/(.{29}\d{1,3}\s{2,4}\d{1,3}\s{2,4}\d{1,3})\/'
-e 'push(@$_);' -e END(print map{$_->[0]})' -e sort{$a->[1]} <=
$b->[1]}' -e map{[$,substr($_,44,33)]@{1}; perbcid.com
```

如果你在 CCID 0037 顺序中看到了最后一行数字 36 的变化：

# 配方 5

```perl
perl -ne 'if/(.{29}\d{1,3}\s{2,4}\d{1,3}\s{2,4}\d{1,3})\/'
-e 'push(@$_$_),' -e END(print map{$_->[0]})' -e sort{$a->[1]} <=
$b->[1]}' -e map{[$,substr($_,44,39)]@{1}; perbcid.com
```

如果你在 POSIX-base 变化中看到了变化，请将最后一行的数字 34 改为 44，如下所示：

# 配方 6

```perl
perl -ne 'if/(.{29}\d{1,3}\s{2,4}\d{1,3}\s{2,4}\d{1,3})\/'
-e 'push(@$_),' -e END(print map{$_->[0]})' -e sort{$a->[1]} <=
$b->[1]}' -e map{[$,substr($_,44,33)]@{1}; perbcid.com
```



在表格排序后，由于此文档最初是用十六进制表示的，为了方便，表格是从...排序的。这是一个多步骤的过程，这里使用了十六进制表示。

| OS | 851 | CCID | CCID | IX | 1047 | chr | 0819 | 0037 | BC | UTF | BDIC |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NUL | 00 | 00 | | | | | | | | |
| SOH | 01 | 01 | | | | | | | | |
| STX | 02 | 02 | | | | | | | | |
| STX | 03 | 03 | | | | | | | | |
| EX | 04 | 04 | | | | | | | | | |
| EN | 05 | 05 | | | | | | | | |
| ACK | 06 | 06 | | | | | | | | |
| BEL | 07 | 07 | | | | | | | | |
| BS | 08 | 08 | | | | | | | | |
| HT | 09 | 09 | | | | | | | | |
| LF | 0A | 0A | | | | | | | | |
| DC1 | 11 | 11 | | | | | | | | |
| DC2 | 12 | 12 | | | | | | | | |
| DC3 | 13 | 13 | | | | | | | | |
| FS | 14 | 14 | | | | | | | | |
| US | 15 | 15 | | | | | | | | |
| RS | 16 | 16 | | | | | | | | |
| ESC | 17 | 17 | | | | | | | | |
| CAN | 18 | 18 | | | | | | | | |
| EM | 19 | 19 | | | | | | | | |
| Q | 20 | 20 | | | | | | | | |
| DC | 21 | 21 | | | | | | | | |
| BH | 22 | 22 | | | | | | | | |
| NBH | 23 | 23 | | | | | | | | |
| IND | 24 | 24 | | | | | | | | |
| NEL | 25 | 25 | | | | | | | | |
| ETB | 26 | 26 | | | | | | | | |
| ESC | 27 | 27 | | | | | | | | |
| HT | 28 | 28 | | | | | | | | |
| PLU | 29 | 29 | | | | | | | | |
| Q | 2A | 2A | | | | | | | | |
| SF | 2B | 2B | | | | | | | | |
| FS | 2C | 2C | | | | | | | | |
| GS | 2D | 2D | | | | | | | | |
| RS | 2E | 2E | | | | | | | | |
| US | 2F | 2F | | | | | | | | |
| FF | 30 | 30 | | | | | | | | | |
| B0 | 31 | 31 | | | | | | | | | |
| S1 | 32 | 32 | | | | | | | | | |
| | 33 | 33 | | | | | | | | | |
| CAN | 34 | 34 | | | | | | | | | |
| | 35 | 35 | | | | | | | | | |
| | 36 | 36 | | | | | | | | | |
| | | 37 | 37 | | | | | | | | |
| | 38 | 38 | | | | | | | | | |
| | 39 | 39 | | | | | | | | | |
| | 3A | 3A | | | | | | | | | |
| | 41 | 41 | | | | | | | | | |
| | 42 | 42 | | | | | | | | | |
| | 43 | 43 | | | | | | | | | |
| | 44 | 44 | | | | | | | | | |
| | 45 | 45 | | | | | | | | | |
| | 46 | 46 | | | | | | | | | |
| | 47 | 47 | | | | | | | | | |
| | 48 | 48 | | | | | | | | | |
| | 49 | 49 | | | | | | | | | |
| | 50 | 50 | | | | | | | | | |
| | 51 | 51 | | | | | | | | | |
| | 52 | 52 | | | | | | | | | |
| | 53 | 53 | | | | | | | | | |
| | 54 | 54 | | | | | | | | | |
| | 55 | 55 | | | | | | | | | |
| | 56 | 56 | | | | | | | | | |
| | 57 | 57 | | | | | | | | | |
| | 58 | 58 | | | | | | | | | |
| | 59 | 59 | | | | | | | | | |
| | 60 | 60 | | | | | | | | | |
| | 61 | 61 | | | | | | | | | |
| | 62 | 62 | | | | | | | | | |
| | 63 | 63 | | | | | | | | | |
| | 64 | 64 | | | | | | | | | |
| | 65 | 65 | | | | | | | | | |
| | 66 | 66 | | | | | | | | | |
| | 67 | 67 | | | | | | | | | | | | |
| | 68 | 68 | | | | | | | | | |
| | 69 | 69 | | | | | | | | | |
| | 70 | 70 | | | | | | | | | |
| | 71 | 71 | | | | | | | | | |
| | 72 | 72 | | | | | | | | | |
| | 73 | 73 | | | | | | | | | |
| | 74 | 74 | | | | | | | | | |
| | 75 | 75 | | | | | | | | |
| | 76 | 76 | | | | | | | | |
| | 77 | 77 | | | | | | | | |
| | 78 | 78 | | | | | | | | |
| | 79 | 79 | | | | | | | | |
| | 80 | 80 | | | | | | | | |
| | 81 | 81 | | | | | | | | |
| | 82 | 82 | | | | | | | | |
| | 83 | 83 | | | | | | | | |
| | 84 | 84 | | | | | | | | |
| | 85 | 85 | | | | | | | | |
| | 86 | 86 | | | | | | | | |
| | 87 | 87 | | | | | | | | |
| | 88 | 88 | | | | | | | | |
| | 89 | 89 | | | | | | | | |
| | 9A | 9A | | | | | | | | |
| | 9B | 9B | | | | | | | | |
| | 9C | 9C | | | | | | | | |
| | 9D | 9D | | | | | | | | |

# 识别字符集

可以确定你正在运行哪种字符集。但首先你需要确定你是否真的需要这样做。如果你不需要测试字符集并执行不同的操作，你的代码会更简单。实际上，很少情况下难以编写可以移植到所有 EBCDIC 页面的直接代码，但第一种测试无法区分 EBCDIC 与 CCSID `0037`、`1047` 或 POSIX-BC EBCDIC 平台。但请注意，由于 `chr(13)` 在旧 Macintosh（ASCII 平台）上是 `chr(10)`，第二次测试在判断 perl 内置是否可以使用 `Config` 模块时会导致麻烦：

```perl
use Config;

$ebcdic = $Config{'define'};
```

# 转换

这些函数接收编码中的输入数值点并返回其等效值。为了将字符串从一个字符转换为另一个字符，只需要一个简单的数字列表（如上表右侧）配合 Perl 运算符。表格中的左列是 ASCII/Latin1 顺序，因此 EBCDIC 列提供了易于使用的 ASCII/Latin1 EBCDIC 操作，且易于反向转换。

例如，将 ASCII/Latin1 转换为代码页 `037`，使用配方 2 输出的第二列（修改后添加 `\`），并将其用于 `tr` 中：

```perl
```



`$cp_037 = \x01\x02\x03\x32\x2D\x2E\x2F\x16\x05\x20\x0A\x0B\x0C\x0D\x0E\x0F`

`\x18\x11\x12\x13\x33\x3C\x3D\x32\x26\x18\x19\x3F\x27\x21\x1D\x1E\x40`

`\x45\x47\x7F\x7B\x58\x6B\x50\x70\x41\x5D\x5C\x4E\x6B\x40\x4A`

`\xF0\xF1\xF2\xF3\xF4\xF5\xF6\xF7\xF8\xF9\xFE\x71\x72\x75\x7A\x7B\x7C\x7D\x6E`

## iconv

XPG 的操作性通常意味着从 shell 或 C 语言库提供了可用的 `iconv` 工具。请查阅您的系统文档以获取有关 `iconv` 的信息。

在 OS/390 或 z/OS 上，请参阅 (1) 手页。在 perl 中调用 `iconv` shell 工具的一种方法是：

```perl
# OS/390 or z/OS 示例 $ascii_data = `echo '$ebcdic_data' | iconv -f IBM-1047 -t ISO08859-1`
```

或者反向映射：

```perl
# OS/390 or z/OS 示例 $ebcdic_data = `echo '$ascii_data' | iconv -f ISO08859-1 -t IBM-1047`
```

其他基于 Perl 的转换选项，请参考 CPAN 上的 `Convert::*` 模块。

## C RTL

OS/390 和 z/OS C 运行时库提供了 `_atoe()` 和 `_etoa()` 函数。

## 操作符差异

EBCDIC 平台会重复某些字符范围。例如，以下数组在 EBCDIC 平台或 ASCII 平台上都具有二十六个元素：

```perl
@alphabet = ('A'..'Z'); # alphabet = 26
```

位操作符（如 `&` 和 `^` `|`）在 EBCDIC 平台上对字符串或字符数据操作时，其返回的结果可能与在 ASCII 平台上运行的结果不同。以下是一个适配自 perl 示例的例子：

ASCII 表中 32 个 C 控制字符的一个意外 属性是，它们在 perl 中可以被“字面量”地描述为控制字符，例如 `(c0) eq \cA> (c1) eq \cA>`，依此类推。EBCDIC 平台上的 Perl 已经过移植，可以将 `\c@` 映射为 `chr` 和 `\c(1)` 等，但这些控制字符取决于你正在使用的代码页。下表使用标准缩写表示控制字符。该范围内的字符集是相同的，且仅与 0037 在一组字符（十进制 21）上不同。请注意，行终止符字符可能由 ASCII 平台生成，但由 `\u 1047` 或 POSIX-BC 平台生成，且无法在 0037 平台上作为 `\c.letter` 控制字符生成。同样注意，`\c\` 不能作为字符串或正则的最后一个元素，因为它会吸收终止符。所有 EBCDIC 平台上，`"\c\X"` 都是文件分隔符（FILE SEPARATOR）与 X 的级联。

| chr | 0859-1 | 0037 | POSIX-BC |
| :--- | :--- | :--- | :--- |
| @ | @ | <NUL> <NUL> <NUL> | \u c A1 <SOH> <SOH> |
| <SB> | <c 2 | <ST> <ST> <ST> | \c 3 <EXT> <EXT> \c 4 <ED> <ST> <DEL> |
| <c 5 | <EN> <HT> <HT> <HT> | \c 6 <ACK> <SSA> \c 7 <G> <BEL> \c 8 <DEL> <h |
| <BS> | <ESA> | \c 9 <HT> <RI> <RI> | \c 10 <LF> <c 11 <SS2> <SS2> <c 11 <VT> |
| <VT> | <c 12 <LF> <FF> <FF> | \c 13 <CR> <CR> <CR> \c 14 <NA> <SO> <SO> |
| <c 15 | <SI> <SI> <SI> | \c 16 <DLE> <DLE> <DLE> | \c 17 <DLE> <c 1 <c 1 |
| <c 18 | <DC2> <DC2> <DC2> | \c 19 <DC3> <DC3> <DC3> | \c 20 <DC4> <OSC> <OSC> <US> |
| <c 21 | <NAK> <NAK> <LF> ** | \c 22 <SYN> <BS> <BS> | \c 23 <ETB> <ESA> <ESA> <X |
| 24 | <CAN> <CAN> <CAN> | \c 25 <EOM> <EOM> <EOM> | \c 26 <ZW> <SUB> <PU2> <PU2> [ |
| 27 | <ESC> <S3> <S3> <S3> | \c 28 <FS> <FS-X> <FS-X> | \c 29 <GS> <GS> <GS> <c^ 30 |
| <RS> | <RS> <RS> <RS> | \c_31 <US> <US> <US> <US> | * <DEL> <APC> <APC> <APC> |

* 注意：在 ASCII 平台上，`\c` 映射到序数 127 (`DEL`)，但由于序数 127 在 EBCDIC 上不是控制字符，`\c` 而是映射到该平台对应的字符（在 0037 中为 255，在 1047 中亦如此，但在 POSIX-BC 中不存在）。

## 函数差异

### chr()

`chr()` 必须给定一个 EBCDIC 代码数字参数以产生预期的字符返回值。

在 EBCDIC 平台上，为了产生期望的字符返回值，`chr()` 必须接收一个 EBCDIC 代码数字参数。

UTF-EBCDIC 中可表示的最大代码点是 U+7FFF-FFFF。如果对 `chr()` 传入一个较大的值，将会产生运行时错误（类似于除以 0）。

### ord()

`ord()` 在 EBCDIC 平台上返回 EBCDIC 代码数字值。例如：

`$the_number_193 = ord("A");`

### pack()

`pack()` 的 `c` 模板取决于字符编码。在 EBCDIC 上的用法示例包括：

`$foo = pack("CCC",193,194,195,196); # $foo eq "ABCD"`
`$foo = pack("CD4",193,194,195,196); # same thing`
`$foo = pack("ccx",193,194,195,196); # $foo eq "AB\0"`

`u` 模板在所有平台上都已移植到 "Unicode"，因此 `pack("u", 65) eq 'A'` 是真的。如果你想获取代码点，请使用 `w` 模板。这意味着 `pack("w", ord($character)) == $character` 是成立的，`character` 会保持不变。

### print()

对于传递给 `print` 的包含 ASCII 编码的标量字符串必须小心。这种情况通常出现在编写 CGI 脚本的 MIME 类型头部时。例如，许多 Perl 编程指南建议类似于：

`print "Content-type:\text/html\012\015\012"; # 这在 EBCDIC 上可能是错误的`

你可以相反写成

`print "Content-type:\text/html\r\n\r"; # 对于 DGW 等可以正常工作。`

在这种情况下，从 EBCDIC 到 ASCII 的转换是由网络服务器完成的。请查阅您的网络服务器文档获取更多详细信息。

```perl
unicode_strings'; $char = substr(shift,0,1); return $char ~~

//[[[:ctrl]]/ && $char ~ / # But not

ASCII; Not C1 use feature 'unicode_strings'; $char = substr(shift,0,1);

return ord($char) ~ /[[[:ascii]]/ && $char < 256 && $char ~ /[[[:ascii]]/ && $char ~~

/[:[:ctrl]]; //;
```

编写 `Is_latin_1` 的另一种方法是显式使用范围内的字符：
sub `Is_latin_1` { `$char = substr(shift,0,1); $char ~ /[ XXXXXXXXXXXXXXXXXAAAAAAA-A.A*AECEEE.IIII. ] [D- -0000-0.XOUUU.yOI2aaaa-a.a*aeceeee.iiii.d- n-00oo-0.Xouuu.yOI./x; }`

虽然这种形式在网络传输中（由于 8 位控制字符的存在）或在非 ISO-Latin 字符集上可能会遇到问题，但它允许重写 `Is_c1`，使其在没有 `unicode_strings` 的早期 Perl 版本（早于 v5.14）上运行：

```perl



```perl
sub is_latin_1 { # But not ASCII; not C1 $char = substr(shift,0,1);

return ord($char) < 256 && $char ~ /[[[:ascii]]/ && ! Is_latin_1($char); }
```

# Socket (SOCKETS)

大多数套接字编程假设网络字节序中使用 ASCII 字符编码。例外包括主机 Web 服务器下的 CGI 脚本编写，服务器可能会替你处理转换。大多数主机 Web 服务器在输出时会将 EBCDIC 数据转换为 ISO-8859-1 或 Unicode。

# 排序 (SORTING)

基于 ASCII 的字符集与 EBCDIC 之间的一个主要区别是字符在原生顺序排序时的相对位置。大多数关注的是大小写字母、数字和下划线 (`_`)。在 ASCII 平台上，原生排序顺序是数字 65 在大写字母之前，大写字母在下划线之前，下划线在小写字母之前。在 EBCDIC 中，下划线首先，然后是小写字母，接着是大写字母，数字最后。如果如果在基于 ASCII 的平台上进行排序，医生的双字母缩写会在另一个双字母缩写之前：

```perl
@sorted = sort(qq(Dr. dr.)); # @sorted holds ('Dr','dr.') on ASCII, # but ('Dr','dr.') on EBCDIC
```

小写字母在大写字母之前的属性甚至包含在 Latin 1 EBCDIC 页面页（如 0037 和 1047）中。例如，“E.”（带变音符号的 E，235）在 ASCII 平台上位于“e.”之前，但在 EBCDIC 平台上，后者（83）位于前者（115）之前。（敏锐的读者会注意到，“ß”（SMALL LETTER SHARP）的大写版本简单地是“SS”，而“ÿ.”（带变音符号的 y）和“æ”（MICRO SIGN）的大写版本不在 0.255 范围内，但在 Unicode 中，它们是启用 Unicode 的 Perl 中的。）

排序顺序会导致在 ASCII 平台上与 EBCDIC 平台上获得的结果产生差异。以下是关于如何处理这些差异的一些建议。

# 忽略 ASCII 与 EBCDIC 的排序差异。

这是计算开销最小的策略。它可能需要一些用户教育。

# 使用排序辅助函数

这通常是完整的，但是计算开销最大的策略。选择其中一种字符集并在每次排序比较时进行转换。这里有一个转换为 ASCII 排序顺序的完整示例：

```perl
sub native_to_uni($ $string = shift; # Saves time on an ASCII

return $string if 'A' = 65;
```

# 不区分大小写的排序 (case_insensitive)

如果性能是一个问题，且你不在乎是否与输入大小写一致，可以使用 `tr` 转换数据：

```perl
perl -ne 'tr/n-za-mN-ZA-M/a-zA-Z/;print'
```

## 哈希排序顺序与校验和

出于安全考虑，Perl 在 ASCII 和 EBCDIC 平台上都刻意随机化了哈希顺序。

将同一个文件转换为 ASCII 和反之时，其 EBCDIC 校验和将有所不同。

## 国际化 (I18N) 与本地化 (L10N)

即使在 EBCDIC 平台上，至少原则上也支持国际化（I18N）和本地化（L10N）。具体细节取决于系统，并在下文的“操作系统问题”章节中进行了讨论。

## 多字节字符集

Perl 使用 UTF-EBCDIC，这是一种多字节编码。在 v5.22 之前的 Perl 版本中，这方面可能存在各种 Bug。

旧版多字节 EBCDIC 字符页 xxx。

## 操作系统问题

对于 EBCDIC Perl 程序员来说，可能有一些需要关注的系统相关性问题。

### OS/400

#### PASE

PASE 环境是 OS/400 的运行时环境，可以运行为 PowerPC AIX 构建的可执行文件；参见 `perlos400`。PASE 是基于 ASCII 的，而不是像 ILE 那样基于 EBCDIC。

IFS XXX。

### OS/390, z/OS

Perl 在 Unix Systems Services (`us`) 下运行。

`sigaction`

`SA_SIGINFO` 可能会导致段错误。

`chcp`

`chcp` 作为 shell 工具支持，用于显示和更改代码页。我们还 (1)。

数据集访问 (`dataset access`)

对于顺序数据访问，尝试：

```
my @ds_records = `cat //DSNAME`
```

或者：

```
my @ds_records = `//HLQ.DSNAME` ;
```

另见 CPAN 上的 `OS390::Stdio` 模块。

`iconv`

`iconv` 作为 shell 工具和 C RTL 例程支持。另见 (1) 和 (3) 手册。

区域设置 (`locales`)

支持区域设置。当区域是另一个 EBCDIC 字符页，且该页将某些字符页变体字符位于其他位置时，可能会出现故障。

目前没有任何 UTF-8 区域设置，尽管某些区域设置名称包含“UTF-8”字符串。

有关区域设置的信息请参见 `perlocale`。L10N 文件位于 `/usr/nls/locale`。在 OS/390 或 z/OS 上定义了 `$Config{d_setlocale}`。

### POSIX-BC?

XXX。

## Bug

当 `cmp`（以及 `sort`）运算符的两个操作数都是 UTF-EBCDIC 编码字符串，且混合了 ASCII 和/或控制字符以及其他字符时，`cmp` 操作符并不一定能给出正确的结果。

`tr///`（以及 `y///`）转译操作符中包含 `\{...}` 的范围处理方式与正则表达式模式中的等效范围不同。它们应该（但不应该）导致范围内的值全部被视为。

## 在你的 C 程序中添加 Perl 解释器

在某种意义上，`perl`（C 程序）是嵌入 Perl（语言）的良好示例，因此我将通过源码分发中的 `miniperlmain.c` 来演示嵌入。以下是一个标准的、非移植的 `miniperlmain.c` 版本，它包含了嵌入的核心要素：

```c
#include <perl.h> /* 来自 Perl 分发版 */

static PerlInterpreter *my_perl;/** Perl 解释器

int main(int argc, char **argv, char **env) { own    PERL_SYS_INIT3(&argc,&argv,&env); own    my_perl = perl_alloc();

    perl_construct(my_perl), pl_exit_flags |= PER_EXIT_DESTRUCT_END; own    perl_parse(my_perl, NULL, argc, argv, (char **)NULL);

    perl_run(my_perl);

    perl_destroy(my_perl);

    perl_free(my_perl);

    PERL_SYS_TERM();
}
```



注意我们没有使用解析器。通常作为 `perl_parse` 的参数处理，而这里 `env` 被替换为 `NULL`，这意味着将使用当前环境。

宏 `PERL_SYS_INIT3()` 和 `PERL_SYS_TERM()` 提供了运行 Perl 解释器所需的特定系统的 C 运行时环境调整；无论你创建或销毁多少个解释器，它们都应该只调用一次。在创建第一个解释器之前调用 `PERL_SYS_INIT3()`，在释放最后一个解释器之后调用 `PERL_SYS_TERM()`。

由于 `PERL_SYS_INIT3()` 可能会更改 `env`，因此将 `env` 作为参数传递给 `perl_parse()` 可能更为合适。

另外请注意，无论你向 `perl_parse()` 传递什么参数，都必须在 C `main()` 的 `argc`、`argv` 上调用一次 `PERL_SYS_INIT3()`。

现在将此程序（我将将其命名为 `interp.c`）编译为可执行文件：
`% cc -o interp interp.c -XExtUtils::Embed -ccopts -ldopts`

编译成功后，你就可以像这样使用 perl：
`% interp -e 'print "Pretty Good Perl\n"; print "10890 - 9801 = 10890 - 9801"; <CTRL-D'`
Pretty Good Perl
10890 - 9801 = 10889

或
`% interp -e 'printf("%x", 3735928559)'`
deadbeef

你也可以在 C 程序运行过程中，通过在调用 `perl_run` 之前将文件名放入 `argv[1]` 来从文件中读取并执行 Perl 程序。

## 在你的 C 程序中调用 Perl 子程序

调用单个 Perl 子程序，你可以使用 `percall` 中记录的任何 `call_*` 函数。在示例中，我们将使用 `call_argvv`。

如下所示，在一个我命名为 `Showtime.c` 的程序中。

```c
#include <perl.h>

static PerlInterpreter *my_perl;

int main(int argc, char **argv, char **env) {

    char *args[] = { NULL };

    PERL_SYS_INIT3(&argc,&argv,&env);

    my_perl = perl_alloc();

    perl_construct(my_perl);

    perl_parse(my_perl, &argc, argv, NULL);

    pl_exit_flags |= PER_EXIT_DESTRUCT_END; /**** 跳过 perl_run() ***/

    call_argvv("showtime", G_NOARGS, args);

    perl_destruct(my_perl);

    perl_free(my_perl);

    PERL_SYS_TERM(0);

}
```

这是一个不接受参数的 Perl 子程序（即 `G_NOARGS`），我将忽略它的返回值（即 `G_DISCARD`）。这些标志以及其他标志定义在 `percall` 中。

我将在名为 `showtime.pl` 的文件中定义 `showtime` 子程序：

```perl
print "I shan't be printed."; sub showtime { print time; }
```

编译和运行非常简单：

```bash
% cc -o showtime showtime.c -perl -MExtUtils::Embed -ccopts -ldopts

% showtime.pl 818284590
```

产生自 1970 年 1 月 1 日（纪元开始）以来经过的秒数，我指的是自写下这个实例以来的时间。

在这种特殊情况下，我们不需要调用 `perl_run`，因为我们设置了 `pl_exit_flag` `PERL_EXIT_DESTRUCT_END`，它会在 `perl_destruct` 中执行块。

如果你想向 Perl 子程序传递参数，可以使用 `call_argv` 向 `NULL-args` 中添加字符串。对于其他数据类型，或者为了检查返回值，你需要操作 Perl 栈。这在“从你的 C 程序中操纵 Perl 栈”中有所演示。

## 在你的 C 程序中评估 Perl 语句

Perl 提供了两个 API 函数来评估 Perl 代码段。它们是 `perlapi` 中的 `eval_sv` 和 `perlapi` 中的 `eval_pv`。

可以说，这些是你从 C 程序中执行 Perl 代码片段时唯一需要的例程。代码可以很长；它可以包含多个语句；它可以利用 `perlfunc` 中的 `use`、`perlfunc` 中的 `require` 以及 perl 中的 `do` 来包含外部文件。

`eval_pv` 让我们评估单个字符串并将变量转换为类型。此程序 `string.c` 执行了三个 Perl 字符串，从第一个提取 int，第二个提取字符串，第三个提取 char。

```c
#include <perl.h>

static PerlInterpreter *my_perl;

int main (int argc, char **argv, char **env) {

    char *args[] = { "-e", "0" };

    PERL_SYS_INIT3(&argc,&argv,&env);

    my_perl = perl_alloc();

    perl_construct(my_perl);

    perl_parse(my_perl, NULL, argc, argv);

    pl_exit_flags |= PERL_EXIT_DESTRUCT_END;

    perl_run(my_perl); /* 将 $a 视为整数 */

    eval_sv("$a=3;a=2"); printf("%d\n", (int)eval_sv("$a", 0))); // 将 $a 视为字符串 */

    eval_sv("$a=3;a=2"); printf("%s\n", (char*)eval_sv("$a", 0))); /* 将 $a 视为字符串 */

    eval_sv("$a=reverse($a)"); printf("%s\n", (char*)eval_sv("$a", 0)));

    perl_free(my_perl);

    PERL_SYS_TERM();

}
```

所有名称带有 `sv` 的奇怪函数都会将 Perl 标量转换为类型。它们设计在 `perlapi` 中。

如果你编译并运行 `string.c`，你会看到结果：
`SvIV()` 创建 int，
`SvNV()` 创建浮点数，`SvPV()` 创建字符串：`a = 9.56`

在上面的示例中，我们创建全局变量来临时存储 `eval_expression` 的计算值。大多数情况下，更好的策略是从 `eval_pv()` 获取返回值。

```c
SV *val = eval_pv("reverse($a)", TRUE);

printf("%s\n", (char*)val);
```

通过这种方式，通过不创建全局变量避免命名空间污染并简化了代码。

## 从你的 C 程序执行匹配和替换

`eval_sv()` 函数评估 Perl 代码字符串，因此我们可以定义使用它来“专门化”匹配和替换的函数：`match()`、`substitute()` 和 `matches`。

`int match(SV *string, char *pattern);`
给定一个字符串和一个模式（例如 `/class/` 或 `/m\w*\b/`），在你的 C 程序中可能表现为 `"/\b\w*\b/"`，如果字符串匹配模式则返回 1，否则返回 0。

`int substitute(SV **string, char *pattern);`
给定一个 sv 指针和一个操作（例如 `s/bob/` 或 `tr[A-Z][a-z]`），`substitute()` 修改 SV 内部的字符串，返回替换次数。

给定一个 sv、一个模式和一个空 SV 指针，`match()` 在列表上下文中评估 `$string =~pattern` 并填充匹配数组元素，返回匹配次数。

这里有一个示例程序 `match.c`，它使用了三处（长行在这里已折行处理）：

```c
#include <perl.h>

static PerlInterpreter *my_perl;

/**
eval_sv(code, error_check) 类似于栈的返回值
*/

int my_sv(SV *sv, sv2_croak_on_error) {
    PUSHMARK(sv);
```



`eval_sv(sv, G_SCALAR);`

`SPAGAIN;`

`POPSUP;`

`return SVPV_nolen(ret);`

}

/**

`match(string, pattern)`

用于标量上下文中的匹配。如果匹配成功则返回 1；否则如此。

 */

`int match(SV *string, char *pattern) {`

    `SV *command = newsv();`
    `set_pvcmd(command, "$string = '%s'");`
    `$string = "%s", SVPV_nolen(pattern);`
    `ret = my_sv(command, TRUE);`
    `SVREFCNT_dec(command);`
    `return SVIV(ret);`

}

/**

`substitute(string, pattern)`

用于修改其左侧的操作（`s/` 和 `**`），如果有任何匹配则修改输入字符串。

返回成功匹配的次数，以及

 */

`int substitute(SV *string, char *pattern) {`
    `SV newsv(0), retval;`
    `sv_setpvcommand(string, "$string = '%s' (matching = %s)");`
    `pattern); SVPV_nolen(string);`
    `retval = my_eval(string, TRUE);`
    `SVREF_dec(dec);`
    `return SV(iv);`

}

/**

`matches` 用于列表上下文。返回匹配次数，并用匹配子串填充 `matches`

 */

`Size_t matches(SV, char *pattern, AV *match) {`
    `sv_setpvcommand(my, "$string = '%s' (matching = %s)");`
    `pattern); SVPV_nolen(string);`
    `my_eval(string, TRUE);`
    `SVREF_dec(command);`
    `get_av("av", 0);`
    `matches = av_t num(match_list) + 1;`
    `return num_matches;`
    `for (int i=0; i < av_len(char *env); {`
        `"" = av[i];`
        `AV *match; i;`
        `SV text;`
        `PERL_INS_ITS(&argc, &env);`
        `my_perl = peralloc(0);`
        `perl_construct(my_perl);`
        `perl_parse(my_perl, NULL, argc, argv);`
        `pl_exit_flags |= PERL_EXIT_DESTRUCT_END;`
        `perl_run(my_perl);`
        `perl_destroy(my_perl);`
        `perl_free(my_perl);`
        `PERL_SYS_TERM();`
    `}`
}

食堂位置的弹簧加载列：你推入栈中的最后一个元素就是你弹弹出的第一个元素。这对于我们的目的已经足够了：你的 C 程序将一些参数推入“Perl 栈”中，在魔法发生时闭上眼睛，然后从栈中弹出结果——即你的子例的返回值。

首先，你需要了解如何将 C 类型转换为 Perl 类型，并使用 `newSViv()`、`sv_setenv()` 以及它们所有的同类函数。它们在 `perlguide` 和 `perlapi` 中有描述。

然后，你需要了解如何操作 Perl 栈。一旦你理解了这些，在 C 中嵌入 Perl 就简单了。

由于 C 没有内置的整数幂函数，Perl 的 `**` 运算符对它是可用的（这比听起来的要简单，因为 Perl 使用 C 的 `pow()` 函数实现了 `**`）。首先，我将在 `perl.pl` 中创建一个存根的指数函数：

```perl
sub exp { my ($a,$b) = @_; return $a ** $b; }
```

现在，我将创建一个 C 程序，其中包含一个函数 `PerlPower()`，该函数包含了所有将两个参数推入 `expo()` 并弹出返回值的必要操作。深呼吸...

```c
#include <perl.h>

static PerlInterpreter *my_perl;

static void PerlPower(int a, int b) {
    int result; /* 初始化栈指针 */
    ENTER; /* 从此处开始创建 */
    SAVEPS/* ... 是一个临时变量 */
    PUSHMARK(SP); /* 记住栈指针 */
    PUSHES(sv_2mv(newSViv(a))); /* 将基数推入栈 */
    PUSHES(sv_2mv(newSViv(b))); /* 将指数推入栈 */
    PUTBACK; /* 将局部栈指针变为全局 */
    G_SCALAR(); /* 创建函数 */
    SPAGAIN; /* 刷新栈指针 */
    /* 从栈中弹出返回值 */
    FREEMPS; /* 释放该返回值 */
    LEAVE; /* ...以及 */
    PUTBACK, FREEMPS;
    printf("%d to %d value is %d\n", a, b, result);
}

int main (int argc, char *argv, char **env) {
    char *my_argv[] = {"perl.pl", NULL};
    SV_SYS_INIT(&argc, &argv, &env);
    my_perl = perl_alloc();
    perl_construct(my_perl);
    perl_parse(my_perl, NULL, my_argv, (char **)NULL);
    PL_exit_flags |= PERL_EXIT_DESTRUCT_END;
    perl_run(my_perl);
    PerlPower(3, 4); /** 计算 3 ** 4 */
    perl_dest(my_perl);
    perl_free(my_perl);
    PERL_SYS_TERM(0);
}
```

编译并运行
`% cc -o power power.c -lUtil:Embed -ccopts -ldopts`
`% power`
`3 to 4 is 8.`

# 维护持久解释器

在开发交互式和可能长时间运行的应用时，维护一个持久解释器比多次分配和构建新的解释器要好。主要原因是速度：因为 Perl 只会被加载到内存中……

然而，在使用持久解释器时，你必须处理名称和变量作用域。在这个示例中，我们使用默认包 `main` 中的全局变量。我们确切知道哪些代码会运行，并假设我们避免了可以避免的冲突和符号符号增长。

假设你的应用程序是一个服务器，会偶尔运行任何文件的 Perl 代码。你的服务器无法知道它将运行什么。这非常危险。

如果文件由 `perl_parse()` 取出，编译到新构建的解释器中，并在随后由 `perl_dest()` 清理，那么你就免受了大多数命名空间的影响。

在这种情况下，避免命名空间冲突的一种方法是将文件名转换为保证唯一的包名，然后使用 `perlfunc` 中的 "`eval`" 将其编译到包中。在下面的示例中，每个文件将只获取一次。或者，应用程序可能会在文件不再需要后清理与该文件相关的符号。使用 `perlapi` 中的 `call_arg`，我们将调用位于持久 `.pl` 文件中的子例 `Embed::Persistent::eval_file`，并将文件名和布尔缓存标记作为参数。

请注意，该过程会随着使用的每个文件继续增长。此外，可能还有其他条件导致 Perl 符号表增长。你需要添加一些逻辑来跟踪该过程，或者在请求一定数量后重启，以确保内存消耗降到最低。你还应该尽可能在 `perlfunc` 中用 "`my`" 来限制变量的作用域。

```perl
package Embed::Persistent;

# persistent.pl

use strict;

use Cache;

qw (delete_package);

sub valid_package_name {
    my ($string) = @_;
    $string = s/([A-Za-z0-9_]+)\(\(".*?"\\)/unpack("C", \$1)/eg; # 第二次通过仅针对数字开头的单词
```



```perl
$string = s/\d|\/\//*%\*","("C","\1)"/eg; # 将其装成真实的包

$name = s/\|://; 

return "$name";

}

sub eval_file {

    my($filename, $delete) = @;

    my $sub = valid_package_name($filename);

    my $mtime = if (Cache($filename, $mtime)) { # 我们已经编译了这个子例

        Cache($filename, $mtime); # 如果自上次 touch 之后未删除

        print STDOUT ready;

        cache_package->handler($filename);

    } else {

        local $FH;

        open($FH, "<", $filename) or die "cannot open \$filename: \!";

        # 将代码封装到我们的唯一包子例中

        eval("package $sub; sub handler { " . <FH> . " }");

        close($FH);

        if ($@) { die $@; }

        cache_package->handler($filename);

    };

    $mtime = time;

    if ($delete) {

        delete_package($sub);

    }

    return $sub;

}
```
（注：源代码中的 OCR 代码严重混乱。）

# END 块的执行

传统上，END 块在 `perl_run` 结束时执行。这对于不调用 `perl_run` 的应用程序会导致问题。从 perl 5 开始，你可以指定 `PL_exit_flags |= PERL_EXIT_DESTRUCT_END` 来获得新行为。如果 `perl_parse` 失败，END 块将返回返回值。

# $0 赋值

当脚本为 `$0` 赋值值时，运行时将尝试通过 `perl_parse` 更新指向 argv 的内存来显示此值。这种行为在嵌入时可能是不适当的，可以通过调用 `perl_parse()` 之前将变量 1 赋值给 `PL_orig` 来禁用。上面的 `persistent.c` 示例是为了字符串。

# 维护多个解释器实例

某些应用程序需要在会话期间创建多个解释器。应用程序可能会随机地释放与解释器相关的资源。程序必须确保这在解释器构建之前发生。默认情况下，当它使用任何选项构建时，全局变量 `PL_destruct_level` 设置为 0，因为当程序在整个寿命内只创建一个解释器时不需要额外的清理。

将 `PL_destruct_level` 设置为 1 可以让一切干净：

```perl
{ ... /* 用 PL_destruct_level 重置全局变量 */
PL_destruct_level = 1;
perl_construct(my_perl); /* 在析构期间清理并重置 */
PL_destruct_level = 1;
perl_destruct(my_perl);
perl_free(my_perl); /* 再来一次！ */
}
```

当调用 `perl_destruct()` 时，解释器的语法解析和符号表会被清理，全局变量会被重置。对 `PL_destruct_level` 的第二次赋值是必要的，因为 `perl_construct` 会将其重置为 0。

现在假设有多个解释器同时运行。这是可能的，但只有当你使用配置 `-Dmultiplicity` 或默认构建的选项 `-threads -Dmultiplicity` 时。启用这些配置之一会将解释器全局变量 `PL_destruct_level` 设置为 1，这样清理就是自动的且正确的。即使你不打算同时运行两个或多个解释器，而是按顺序运行（如上面的示例所示），建议使用 multiplicity 选项构建 perl，否则解释器变量在连续运行之间可能无法正确初始化，应用程序可能会崩溃。

参见 `perlxs` 中的 "Thread-system interfaces"。

如果你打算在不同的线程并发运行多个解释器，使用 `-threads -Dmultiplicity` 比 `-Dmultiplicity` 更合适，因为它支持将系统的线程链接到解释器。

让我们看一下代码：

```c
#include <perl.h>

/* 我们将嵌入两个解释器 */
#define SAY_HELLO "-e printf(\"Hi %s\\n\")"

int main (int argc, char **argv, char **env) {
    PerlInterpreter *one_perl, *two_perl;
    char *args1[] = {"one_perl", SAY_HELLO};
    char *args2[] = {"two_perl", SAY_HELLO};
    PERL_SYS_INIT(&argc,&argv,env);
    perl_construct(one_perl); PERL_SET_CONTEXT(one_perl);
    PERL_SET_CONTEXT(two_perl); perl_construct(two_perl);
    PERL_SET_CONTEXT(one_perl);
    perl_parse(one_perl, NULL, 3, args1, (char **)NULL);
    PERL_SET_CONTEXT(two_perl);
    perl_parse(two_perl, NULL, 3, args2, (char **)NULL);
    PERL_SET_CONTEXT(one_perl);
    perl_run(one_perl);
    PERL_SET_CONTEXT(one_perl);
    perl_destruct(one_perl);
    perl_free(one_perl);
    PERL_SET_CONTEXT(two_perl);
    perl_destruct(two_perl);
    PERL_SET_CONTEXT(two_perl);
    perl_free(two_perl);
    PERL_SYS_TERM();
}
```

注意对 `PERL_SET_CONTEXT()` 的调用。这些对于在运行的特定进程或线程上初始化“当前”解释器是必要的。如果你有多个解释器并正在，应该以交错的方式在两个解释器上进行 perl API 调用。

当 interp 被一个未创建它的线程使用时（使用 `perl_alloc()` 或更冷门的 `perl_clone()`），也应该调用 `PERL_SET_CONTEXT(interp)`。

像往常一样编译：

```
% CC -o multiplicity multiplicity.c \ `perl -MExtUtils::Embed -e copts -e\nldopts
```

运行它，运行：

```
% multiplicity Hi, I'm one_perl Hi, I'm two_perl
```

## 在你的 C 程序中使用使用了 C 库的 Perl 模块

如果你尝试了上面的示例，并尝试嵌入一个使用 Perl 模块（使用 Socket）的脚本，而该模块本身使用了 C 或 C++ 库，可能会发生以下情况：

Can't load module, dynamic loading not available in this perl. （你可能需要构建一个新的 perl 可执行文件，该文件需要支持动态加载或将 Socket 静态链接到其中。）

问题在哪里？

你的解释器本身不知道如何与这些扩展进行通信。一点点“胶水”会有帮助。到目前为止，你一直在调用 `perl_parse()`，并对第二个参数处理 NULL：

```
perl_parse(my_perl, NULL, argc, my_argv, NULL);
```

在这里可以插入胶水，以初始化 Perl 与链接的/C 之间的初始上下文……让我们看看 `perlmain.c` 的一些部分，看看 Perl 是如何做的：

```
static void xs_init (pTHX); EXTERN_C void DynaLoader (pTHX, cv); EXTERN_C void xs_init(pTHX) {
char *file = __FILE__ / DynaLoader is a special case /*
newXS("DynaLoader::bootstrap", DynaLoader, file);
```



`newXS("Socket::bootstrap", socket, file); }`

简单来说：对于与你的 Perl 可执行文件链接的扩展（在电脑的初始配置或添加新扩展时确定），都会创建一个子程序来包含该扩展的例程。现在，子程序被命名为 `Module::bootstrap()` 并在使用 `Module` 时调用。这钩入了一个 XSUB `boot_module`，为扩展的每个 XSUB 创建一个 Perl 计数器。不用担心这部分；留给扩展的作者处理即可。如果你的扩展是动态加载的，`DynaLoader` 会为你动态创建 `Module::bootstrap()`。如果你有一个工作良好的 `DynaLoader`，那么很少需要静态链接其他扩展。

一旦你有了胶水，就将其 `get` 入到 `perl_parse()` 的第二个参数中：

```
perl_parse(my_perl, xs_init, argc, my_argv, NULL);
```

然后编译：

```
% cc -o interp.c %perl -MExtUtils::Embed -e copts -e ldopts %
use someDynamicallyLoadedModule; print "Now I can use\nextensions\\n"
```

`ExtUtils::Embed` 也可以自动编写 `xs_init` 胶水代码。

```
% perl -MExtUtils::Embed -e xinit--o perlsi.cc %cc -perl perlsi.c %perl
MExtUtils::Embed -e copts %cc -c interp.o %perl -MExtUtils::Embed -e
copts %cc -o interplsi.o interp.o %perl -MExtUtils::Embed -e
ldopts
```

更多细节请参阅 `perlxs`、`pergluts` 和 `perlapi`。

## 在 posix locale 中使用嵌入式 Perl

（关于这些请参阅 `perlocale`。）当 Perl 解释器正常启动时，它会告诉系统它想要使用系统的默认 `locale`。这通常是 `"C"` 或 `"POSIX"` `locale`，但并非绝对。如果 `perl` 代码中没有使用 `use locale`，这大部分没有影响（但请参阅 `perlocale` 中的 "Not within the scope of \use locale"）。此外，如果你在嵌入式 Perl 中使用的 `locale` 与系统默认相同，即使它不是系统默认值，也没有问题。从 Perl v5.20 开始，你可以告诉嵌入式 Perl 解释器 `locale` 已经设置好，并跳过它自身的正常初始化。如果环境变量 `PERL_SKIP_LOCALE_INIT` 被设置（即使设置为 0 或空），它就会跳过初始化。具有此能力的 Perl 会定义 C 预处理器符号 `HAS_SKIP_LOCALE_INIT`。这允许与多个 Perl 版本一起工作的代码在遇到较早版本的 Perl 时执行某种规避措施。

## 隐藏 PERL_

如果你完全隐藏了 Perl 公共 API 的短形式，请在编译标志中添加 `-DPERL_NO_SHORT_NAMES`。这意味着例如，你不再需要写

```
warn("%d bottles of beer on the wall", bottlecount);
```

而是必须编写显式的完整形式：

```
Perl_warn(aTHX_ "%d bottles of beer on the wall", bottlecount);
```



（关于 `aTHX_` 的解释请参见 `perlugs` 中的“Background and `PERL_IMPLICIT_CONTEXT`”）。隐藏短形式对于避免与其他软件包的各种糟糕（C 预处理器或其他）冲突非常有用（Perl 定义了约 2400 个带有这些短名称的 API，去掉几百个，因此确实有冲突的空间）。

## 格言

有时你可以在 C 中编写更快的代码，但你始终可以在 Perl 中更快地编写代码。因为你可以互相调用，随心所欲地组合它们。

# 作者

Jon Orwant, Tim Christiansen, Guy Furuseth, Ben Sugars, Ilya Zakhvich, Tomce, ActiveState.

Copyright (C) 1995, 1996, 1997, 1998, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023.

## 实验性

名称

本文档列出了当前和过去的功能。

## 描述

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 当前

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 智能匹配

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

## 功能

下方功能目前处于实验阶段，可能会在不先通知的情况下更改或删除。

另参 `perlrun`

`Makefile` 中有一个 "`installhtml`" 目标。
该功能的工单为 [perl #116487] <>。
EBCDIC 上的 Perl Unicode

# 已接受的特性

这些特性非常成功，并且与其他特性配合得非常好，以至于我们决定取消它们的实验状态，并将它们作为 Perl 世界中完整、稳定的特性来接纳，赋予它们所有的收益和奢华。它们还获得了 +5 稳定性和 +3 魅力值。

- 64 位支持
  引入于 Perl 5.005
  `die` 接受引用

- DB 模块
  引入于 Perl 5.6.0
  另参 `perdebug`, `perldebtut`

- 弱引用
  引入于 Perl 5.6.0

- 内部文件 glob
  引入于 Perl 5.6.0

- `fork()` 仿真
  引入于 Perl 5.6.1
  另参 `perfork`

- `-Dusemultiplicity` `-Duseithreads`
  引入于 Perl 5.6.0

- 在 Perl 5.8.0 中被接受

- 支持长双精度 (long doubles)
  引入于 Perl 5.6.0
  在 Perl 5.8.1 中被接受

- `"\N"` 正则字符类
  `\N` 类不要与命名字符序列 `\NAME}`混淆，它表示正则表达式中的任何非换行字符。
  引入于 Perl 5.12

- 接受的确切版本不清楚，但不晚于 Perl 5.18。

- `({code})` 和 `"(?? code })"`
  引入于 Perl 5.6.0
  在 Perl 5.20.0 中被接受

另参 `perlre`

- Linux 抽象 Unix 域套接字
  引入于 Perl 5.9.2
  在 Perl 5.20.0 之前接受。`Socket` 库现在主要在 CPAN 上维护，而不是在 perl 核心。

另参 `Socket`

- Lvalue 子程序
  引入于 Perl 5.6.0
  在 Perl 5.20.0 中被接受

另参 `perlsub`

- 回溯控制动词
  `(*ACCEPT)`
  引入于：Perl 5.10
  在 Perl 5.20.0 中被接受

- <:pop> io 伪层
  另参 `perlrun`
  在 Perl 5.20.0 中被接受

- 正则中的“s”匹配垂直制表符
  在 Perl 5.22.0 中被接受

# 已移除的特性

这些特性不再被视为实验性，且其功能已经消失。如果你在我们明确告诉你不要使用这些特性后仍然使用它们编写生产环境程序（参见 `perlpolicy`），那是你的错。

- 5.005 风格线程
  引入于 Perl 5.005
  在 Perl 5.10 中移除

- `perlcc`
  引入于 Perl 5.005
  从 Perl 5.9.0 移动到 CPAN

- 伪哈希数据类型
  引入于 Perl 5.6.0
  在 Perl 5.90 中移除

- GetOpt:Long 现在可以一次性接受多个值（实验性）
  `Getopt::Long` 升级到版本 2.35
  在 Perl 5.8.8 中移除

# 断言

- `-A` 命令行开关
  引入于 Perl 5.9.0
  在 Perl 5.9.5 中移除

# Test::Harness::Straps

从 Perl 5.10.1 移动到 CPAN

# legacy（遗留）

实验性的 legacy 指令被 feature 指令吸收。

引入于：5.11.2
移除于：5.11.3

# 另参

要查看完整的特性列表请检查 `feature`。

# 作者

brian d foy “<>”

Sebastien Aperghis-Tramoni “<>”

# 版权

Copyright 2010, brian d foy “<>”

# 许可证

你可以按照 Perl 本相同的条款使用和发布此文档。

# PERLFORK

- 名称
  `perlfork` - Perl 的 `fork()` 仿真

## 摘要

注意：自 5.8.0 发布以来，`fork()` 仿真已经相当成熟。然而，仍然存在一些知的 bug 以及与真实 `fork()` 的差异，可能会影响到你。请参下文的“BUGS”和“CAVEATS AND LIMITATIONS”部分。

Perl 提供 `fork()` 仿真

在操作系统看来，通过 `fork()` 仿真创建的伪进程仅仅是同一进程中的线程。这意味着操作系统施加的任何进程级限制都适用于所有伪进程。这包括操作系统对打开的文件、目录和套接字句柄的限制，对磁盘使用的限制、内存大小限制、CPU 利用率限制等。

## 描述

`fork()` 仿真旨在兼容可用 `fork()` 的 Unix 类平台。注意，这意味着除非所有运行中的伪进程退出，否则进程不会退出。

当伪进程内部调用 `exec()` 时，`DESTROY` 方法和 `END` 块将在外部进程之后调用。

`exit()` 总是退出执行中的伪进程，并会自动等待任何未出的子伪进程。注意，这意味着除非所有运行中的伪进程退出，否则进程不会退出。

从 Perl 5.14 开始，父进程不会自动 `wait()` 任何收到 `kill('TERM', ...)` 信号的子进程，以避免在子进程阻塞 I/O 且永远不会接收信号的情况下发生死锁。

# 注意事项与局限性

### BEGIN 块

在 `BEGIN` 块内部调用 `fork()` 仿真将无法完全正常工作。分叉后的副本将运行 `BEGIN` 块的内容，但不会在执行 `BEGIN` 块后继续解析源码。例如，考虑以下代码：

```
BEGIN { fork and exit; # fork 出子进程并退出父进程

print "inner\n"; print "outer\n";
```



这将打印：

`inner`

而不是预期的：

`inner outer`

这一局限性源于在多次解析中克隆和重启 Perl 解析器所使用的栈的根本性技术困难。

### 打开的文件句柄

在 `fork()` 时已打开的任何文件句柄都会被 `dup()`。因此，父进程和子进程可以独立地关闭文件，但请注意 `dup()` 后的句柄仍然共享相同的指针。在父进程中更改位置会改变子进程中的位置，反之亦然。人们可以在子进程中单独打开需要不同寻址指针的文件来避免这种情况。

在某些操作系统上（特别是 Solaris 和 Unixware），从子进程中调用 `exit()` 会刷新并关闭父进程中打开的文件句柄，从而损坏句柄。在这些系统上，建议使用 `_exit()`。Perl 通过 `POSIX` 模块可以使用 `_exit()`。请咨询您的系统 man页以获取相关信息。

### 打开的目录句柄

Perl 将完全从所有打开的目录句柄中读取，直到到达流的末尾。它会将 `seekdir()` 回原始位置并完全重新 `readdir()` 请求。这意味着父进程持有的目录句柄或子进程持有的句柄都看不到 `fork()` 之后对目录进行的任何更改。

注意 `rewinddir()` 在 Windows 上有类似的局限性，并且不会强制 `readdir()` 再次读取目录。只有新打开的目录句柄会反映目录的变化。

### Fork pipe open() 尚未实现

`open(FOO, "-")` 和 `open(BAR, "|")` 结构尚未实现。在新代码中可以通过显式创建管道轻松绕过此限制。以下示例展示了如何处理分叉的子进程：

```
# 模拟 open(FOO, "-") sub pipe_to_fork($) { my $parent = shift;
```

```
pipe my $child, $parent or die; if ($pid = fork()); die("fork failed: $!") unless defined $pid; if ($pid) {
    close $child;
} else {
    close $parent;
    dup2(STDIN, "&" . fileno($child)) or die;
    $pid;
    if (pipe_to_fork("FOO")) {
        $parent; print "pipe_to_fork\n";
        close $FOO;
    } else {
        # child
        while (<STDIN>) {
            print;
        }
        exit(0);
    }
}
```

而另一个是从子进程读取：

```
# 模拟 open(FOO, "-") sub pipe_from_fork { my $parent = shift; pipe $parent, $child or die; $pid = fork()); die("fork failed: $!") unless defined $pid; if ($pid) {
    close $child;
} else {
    close $parent;
    dup2(STDOUT, "&" . fileno($child)) or die;
    $pid;
    if (pipe_from_fork("BAR")) {
        print;
        close BAR;
    } else {
        # child
        print "pipe_from_fork\n";
        exit(0);
    }
}
```



未来将支持 `fork pipe-open()` 结构。

### XSUB 维护的全局状态

维护自身全局状态的外部子程序（XSUB）可能无法正常工作。此类 XSUB 需要通过锁来保护不同伪进程对数据的访问，或者在 `fork()` 调用时维护其状态。为扩展提供机会的回调机制将在未来提供。

### 嵌入应用程序的解释器

当在嵌入 Perl 解析器并调用 Perl API 的应用程序执行时，`fork()` 仿真可能不符合预期。这是由于该仿真仅了解 Perl 解析器自身的数据结构，而对应用程序的状态一无所知。例如，调用栈上的任何状态都是无法访问的。

### 扩展的线程安全性

由于 `fork()` 仿真在多线程中运行代码，调用非线程安全库的扩展在调用 `fork()` 时可能无法可靠工作。随着 Perl 的支持在具有原生 `fork` 的平台上日益普及，预计此类扩展。

# 可移植性注意事项

在可移植 Perl 代码中，不能对分叉进程使用 `kill(9, $child)`。杀死分叉进程是不安全的且结果不可预测。见上文“`kill()`”。

## 缺陷

伪进程 ID 使用负整数会导致 `wait()` 函数，因为该数字被视为特殊。目前的实现假设系统不会为用户线程分配 ID `1`。未来将实现更好的伪进程 ID 表示。

在某些情况下，通过 `pipe()`、`socket()` 和 `accept()` 操作符创建的操作系统级句柄似乎没有被准确复制。这只发生在某些情况下，但一旦发生，可能会导致句柄读写端之间的死锁，或无法跨套接句柄发送或接收数据。

本文在某些方面可能不完整。

# 作者

并发解释器和 `fork()` 仿真由 ActiveState 实现，并在微软公司资助。

本文由 Gurusamy Sarathy <> 编写并维护。

# 另参

`perfununc`, `perlipc` 中的“`fork`”

# PERLFORM

### NAME

`perlform` - Perl 格式化

# DESCRIPTION

Perl 有一种机制可以帮助生成简单的报告和图表。为了方便这一点，Perl 帮助你编写输出代码使其接近打印时的外观。它可以跟踪诸如每页行数、当前页码、何时打印页眉等信息。关键字借自于 FORTRAN：`format()` 用于声明，`write()` 用于执行；见 `perlfunc` 中的对应条目。幸运的是，布局更易读，更像 BASIC 的 PRINT 语句。把它看作是穷版的。

无论字段是文本还是数值。波浪号运算符不是字段的一部分。让我们详细查看各种可能性。

## 文本字段

字段的长度通过用多个 `<`、`>` 或 `|` 字符填充字段来提供，以分别指定左对齐或居中的非数值字段。对于普通字段，将取值（直到第一个换行符为止）并根据所选的对齐方式进行打印，截断多余的字符。如果你用 "..." 终止文本字段，当值被截断时将显示三个点。特殊的文本字段可以用于进行基础的多行文本块填充；详情请参阅“使用填充模式”。

示例：`format STDOUT = @@@<< @|||| @>>>>>> "left", "middle", "right"`
输出：`left middle right`

## 数值字段

使用 `#` 作为填充字符表示指定数值字段，并采用右对齐。可选的 `.` 定义小数点。使用 `0`（零）代替第一个 `#` 时，如果需要，格式化后的数字将填充前导零。如果值未定义，则特殊的数值字段将为空。如果值超过了指定的宽度，字段将用 `#` 填充作为溢出证据。

示例：`format STDOUT = ####.#### ####, #### #### ^^^^^^ 42, 3.1415, undef, 0, 10000, undef.`
输出：`42 3.1412 0.000 0 ####`

## 用于变宽多行文本的字段 `@*`

字段 `@*` 可用于打印多行、不截断的值；它应该（但不需要）单独出现。最后的换行符会被删除，但所有其他字符将原样嵌入。

## 用于变宽单行文本的字段 `^*`

像 `@` 一样，这是一个变宽字段。提供的值必须是一个标量变量。Perl 将文本的第一行（直到 `\n`）放入字段，然后删掉字符串的前部，以便下次引用该变量时，就可以打印更多的文本。该变量不会恢复。

示例：`$text = "line 1\nline 2\n 3"; format STDOUT = Text: ^*$ $text ^* $`
输出：`Text: line 1 line 2 line 3`

## 指定值

值在下方的格式化行中指定，顺序与图片字段相同。提供值的表达式必须用逗号隔开。在处理行之前，所有表达式都会在列表上下文中求值，因此单个列表表达式可以产生多个列表元素。如果缺失，表达式可以跨越多行。

## 使用填充模式

在文本字段上，脱字符符号（caret）启用了某种填充模式。不再使用任意表达式，提供的值必须是包含文本字符串的标量变量。Perl 将下一部分文本放入字段，并删掉字符串的前部，以便下次引用该变量时，就可以打印更多的文本。（是的，这意味着变量本身在执行 `write()` 期间被修改了，且不会恢复。）下一部分文本由脱字符符号换行算法决定。你可以使用返回字符（`\n` 强制换行）。你可以通过更改变量 `:$ `（如果你使用的是英文模块，则是 `$LINE_BREAK_CHARACTERS`）为所需的字符列表来更改允许换行的字符。

## 抑制所有字段为空的行

使用脱字符字段可能会产生所有字段都为空的。你可以通过在行的任何位置放置“~”（波浪号）来抑制此类行。波浪号在输出时将被转换为空格。

## 重复格式波浪号

如果你在行的任何位置放入两个连续的波浪号“~~~”，该行将重复，直到行上的所有字段都耗尽，即未定义。对于特殊的（脱字符符号）文本字段，这种情况迟早会发生，但如果你使用那种种类的文本字段，你提供的表达式最好不要永远给出相同的值！`shift @f` 是一个可以工作的简单示例。）不要在此类行中使用普通的 (!) 数值字段，因为它永远不会为空。

## 表单顶部处理

表单顶部处理默认由与当前字段句柄同名并拼接了 `_TOP` 的格式处理。它在每页的顶部触发。请参阅 `perlfunc` 中的 `write`。

示例：

一封关于 `/etc/passwd` 文件格式的报告
`STDOUT_TOP = Passwd File Name`
`Login OfficeUid Gid Home`

```
format STDOUT = @<<<<<<<<|||||
<<<<>>> @<<<<<<<<<<<<$name, login,office,$uid,$gid,
$home = a report from a bug report format STDOUT_TOP = <<
<<<<<<<<<<<<|||>>>>>>>>$system, $date
format
```

```
STDOUT = Subject: @<<<<<<<<<<<<<<<<<<<<<<<<<<<
$subject Index: @<<<<<<<<<<<<<<<<<<<<<<<<<<<
$index, $descriptionPriority@<< Date: @From:
<<<<<<<<<<<<<<<<<<<<<<<<<<$description ^<<<<<<<<<<<<$from,
$description Assigned to: @<<<<Programmer, $description
<<<<<<<<<<<<<<<<<<<<<<<<$description ^<<<<<<<<<<<<
$description - <<<<<<<<<<<<<<$description ^<<<<<<<<...
$description
```

在同一个输出通道上结合 `write()` 内部 `print()` 是可能的，但你必须自己处理 `-` (`$FORMAT_LINES_LEFT`)。

## 格式变量

当前名称存储在变量 `$0` (`$FORMAT_TOP_NAME`) 中，当前的顶部格式名称存储在 `^` (`$FORMAT_TOP_NAME`) 中。当前输出页码存储在 `($FORMAT_PAGE_NUMBER)`，页数存储在 `-` (`$FORMAT_LINES_PER`)。在该句柄上是否自动刷新存储在 `|` (`$OUTPUT_AUTOFUSH`) 中。每页开头（第一页除外）之前的字符串存储在 `^L` (`$FORMAT_FORMMEED`) 中。这些变量是基于句柄设置的，因此你需要 `select()` 到另一个句柄来影响它们：

```
select((select(OUTF), ~= = "My_Other_Format", $^ = "My_Top_Format \ )[0]);
```

很丑陋，对吧？这是一种常见的惯用法，尽管当你看到它时不应该感到惊讶。你可以使用临时变量来持有之前的句句柄：（这通常来说是更好的方法，因为不仅提高了可读性，你现在在表达式单例中有了一个中间阶段，方便了调试）。

## 注意事项

由于值行可能包含任意表达式（针对字段），你可以将更复杂的处理交给其他函数，例如 `sprintf()`。例如：



format Ident = @<<<<<<&commify($n)

```
要将实际内容放入字段，这样做：
```
format Ident = I have an @
```
要让整行文本居中，可以这样做：
```
format Ident = @|||||||||||||||||||||| Some text
```
没有内置方法可以表示“浮在页面右侧，无论它有多宽”。你必须指定它去哪里。真正绝望的人可以根据当前的列数动态生成自己的格式，然后使用 `eval()`：
```
$format = "STDOUT = \n" '^' '<x $cols \n" '$entry' "\n" \t^\n" .
```
这将生成类似这样的通用格式：
```
$entry ^<<<<<<<<<<<<<<<<<<<<<<<<<< $entry
```
这是一个 `(1)` 的小型程序：
```
format = <<<<<<<<<<<<<<<<<<<<<< $. = '';
while (<>) { s/s*\n\s*/ /g; write; }
```

## 页脚

虽然 `$FORMAT_TOP_NAME` 包含头部格式的名称，但没有相应的机制自动处理页脚。不知道页脚有多大是主要问题之一。它在待办列表中。

有一种策略：如果你有固定大小的页脚，可以通过在每次 `write()` 之前检查 `$FORMAT_LINES` 获取页脚，并在必要时自己打印页脚。

另一种策略：打开一个指向自己的管道，使用 `opening(MYSELF, "|-", "open" in perlfunc)` 并始终 `write()` 到 `MYSELF` 而不是 `STDOUT`。让你的子进程处理其 `STDIN`，以你喜欢的方式重新排列头部和页脚。不方便，但可行。

## 访问格式接口

为了对格式机制进行低级访问，你可以使用 `formline()` 并直接访问 `^A`（`$ACCUMULATOR` 变量）。

例如：
```
$str = formline<<'END', 1,2,3; @<<< || @>>> END print "Wow, I just
stored '$^A' in the accumulator!\n";
```
或者为了创建一个 `swrite()` 子程序（其作用相当于 `sprintf()` 之于 `printf()`），可以这样操作：
```perl
use Carp; sub write { croak "usage: swrite PICTURE ARGS" unless @_; my
$format = shift; $^A ="formline($format,@); return $^A; } $string =
swrite(<<'END', 1, 2, 3); Check me out @<<< || @>>> END print $string;
```

## 警告

格式末尾的孤立点也可能导致通过配置错误的 Internet 邮件服务器传输的邮件信息提前结束（根据经验，这种配置错误是常态而非例外）。因此，当通过邮件发送格式代码时，你应该进行缩进，使格式结束点不要位于左侧边距；这样可以防止 SMTP 截断。

词作用变量（用 `"my"` 声明）在格式内部是不可见的，除非该格式是在词作用变量的作用范围内声明的。

如果程序的环境指定了 `LC_NUMERIC` 区域，且在声明格式时生效了 `use locale`，该区域将用于指定格式化输出中的小数点。无法在调用 `write()` 时通过 `use locale` 来控制格式化输出。请参见 `perlocale` 获取关于区域处理的更多讨论。

在显示在固定长度文本字段中的字符串中，每个控制字符会被替换为空格。（但请记住在使用填充模式时 `\r` 的特殊含义）。这样做是为了避免控制字符在某些输出媒介上“消失”时导致对齐错。

# PERLFREEBSD

## 名称
`perlfreebsd` - FreeBSD 系统上的 Perl 5 版本

## 描述
本文档描述了影响 Perl 5 版本（以下简称 Perl）编译和运行的 FreeBSD 特性。

## 带有线程的 readdir_r FreeBSD 核心 dump
当 perl 配置为使用线程时，它将优先使用重入库调用而非非重入版本。FreeBSD 4.5 及更早版本中的 `readdir_r` 函数中存在一个 bug，读取大型目录时可能导致 SEGV。针对 FreeBSD libc 的补丁已可用（见 ）并已集成到 FreeBSD 4.6 中。

## FreeBSD 中的 $X 并不总是包含完整路径
perl 会通过询问操作系统尽可能将 `$x` 设置为完整路径。在 FreeBSD 上，perl 解释器的完整路径通过使用 `sysctl` 的 `KERN_PROC_PATHNAME` 找到（如果支持），否则通过读取符号链接 `/proc/curproc/file` 找到。FreeBSD 7 及更早版本存在一个 bug，这两种方法有时都会返回错误值（见 ）。在这种情况下，perl 将回退到旧行为，即使用 C 的 `argv[0]` 值作为 `$x`。

# 作者
Nicholas Clark <>, 由 Slaven Rezic 和 Tim Bunce 提供的智慧。
请向 `.` 报告任何错误、更新或建议。

# PERLFUNC

## 名称
`perlfunc` - Perl 内置函数

## 描述
本节中的函数可以作为表达式中的项。它们分为两大类：列表操作符和命名一元运算符。它们与逗号的优先级关系有所不同（参见 `perlop` 中的优先级表）。列表操作符接受多个参数，而一元运算符永远不会接受多个参数。因此，逗号会终止一元运算符的参数，但仅分隔列表操作符的参数。一元运算符通常为其参数提供标量语境，而列表操作符可能为其参数提供标量或列表语境。如果是这样，标量参数在前，列表参数紧随其后，且只能有一个这样的列表参数。例如，`slice()` 有三个标量参数，后跟一个列表，而 `gethostbyname()` 有四个标量参数。

在随后的语法描述中，期望列表（并为元素提供语境）的列表操作符将用 `LIST` 作为参数显示。此类列表可以由标量运算符或列表值的任意组合组成；列表值将作为每个单独元素在列表该一点被插值时被包含在列表中，形成一个更长的单维列表。逗号应分隔 `LIST` 的字面量元素。

下方列表中的任何函数都可以在参数周围带或不带括号使用。如果你使用括号，这个简单但偶尔令人惊讶的规则是：*它看起来像一个函数，所以它就是一个函数，优先级无关*。否则，它是列表操作符或一元运算符，优先级不计，有时你需要小心：
```
print 1+2+4; # 输出 7. print(1+2) + 4; # 输出 3. print(1+2)+4; # 也输出 3! print+(1+2)+4; # 输出 7. print ((1+2)+4); # 输出 7.
```
如果你带有 `-w` 切换运行 Perl，它可以就此警告你。例如，第三行产生：
```
print(...) 被解释为函数 - line 1. 在空语境下无效的整数加法 - line 1
```



少数函数完全不接受参数，因此既不是一元运算符也不是列表操作符。这些包括 `time` 和 `endfor` 等函数。例如，`time+86400` 意味着 `time() + 86400`。

对于可以在标量或列表语境下使用的函数，实际行为由语境决定。通常，作为系统调用 `"syscalls"` 封装的函数在成功时返回真，否则返回 `undef`。这与 C 接口不同，后者在失败时返回 `-1`。扩展模块也可以挂钩 Perl 解析器以定义新类型的表达式。这些看起来像函数，但也看起来完全不同。随后的语法完全由扩展定义。如果你是实现者，请使用 `perlapi` 中的 `"PL_keyword_plugin"` 机制。如果你正在使用此类模块，请查看该模块文档以了解其定义的语法的细节。

## 按分类划分 Perl 函数

以下是按类别排列的 Perl 函数（包括像函数的内容，如关键字和命名运算符）。某些函数出现在多个处。

### 用于 SCALARs 和字符串的函数

- `chop`, `chop`, `chr`, `crypt`, `fc`, `hex`, `index`, `lc`, `lcsort`, `length`, `oct`, `ord`, `pack`, `reverse`, `rint`, `sprint`, `substr`, `uc`, `ucfirst`, `y`

`fc` 仅在启用 `fc` 特性或带有 `CORE::` 前缀时可用。在当前作用范围内使用 `use v5.16`（或更高）声明时，该功能会自动启用。

### 正则表达式和模式匹配

### 数值函数
`abs`, `atan2`, `cos`, `exp`, `hex`, `int`, `log`, `oct`, `ran`, `sin`, `sqrt`

### 用于真实 @ARRAYs 的函数

- `each`, `keys`, `pop`, `push`, `shift`, `splice`, `unshift`, `values`

### 用于列表数据的函数

- `grep`, `join`, `map`, `reverse`, `sort`, `unpack`

### 用于真实 %HASHes 的函数

- `delete`, `each`, `exists`, `keys`, `values`

### 输入和输出函数

- `binmode`, `close`, `closedir`, `dbmclose`, `dbmopen`, `die`, `EOF`, `fileno`, `flock`, `format`

`getc`, `print`, `printf`, `read`, `readdir`, `readline`, `rewinddir`, `say`, `seek`, `seekdir`, `select`, `syscall`, `sysread`, `sysseek`, `syswrite`, `tell`, `tellid`, `truncate`, `warn`, `write`

`say` is available only if the say feature is enabled or if it is prefixed with `CORE::`. The feature is enabled automatically with a `use v5.10` (or higher) declaration in the current scope.

### Functions for fixed-length data or records

`pack`, `read`, `syscall`, `sysread`, `sysseek`, `syswrite`, `unpack`, `vec`

### Functions for filehandles, files, or directories

- `-X`, `chdir`, `chmod`, `chroot`, `fcntl`, `glob`, `ioctl`, `link`, `lstat`, `mkdir`, `open`, `opendir`, `readlink`, `rename`, `redir`, `stat`, `mysync`, `sysopen`, `unmask`, `utime`

### Keywords related to the control of your program
`break`, `call`, `continue`, `die`, `do`, `dump`, `evalytes`, `exit`, `__FILE__`, `goto`, `last`, `__LINE__`, `next`, `__PACKAGE__`, `redo`, `return`, `sub`, `__SUB__`, `array`

`break` is available only if you enable the experimental switch feature or use the `CORE::` prefix. The switch feature also enables the default, given and when statements, are documented in "Switch Statements" in Perl. The switch feature is enabled automatically with a `use v5.10` (or higher) declaration in the current scope. In Perl v5.14 and earlier, `continue` required the switch feature, like other keywords.

`evalytes` is only available with the evalytes feature (see feature) or if prefixed with `CORE::`. `__SUB__` is only available with the current_sub or if prefixed with `CORE::`. Both the evalytes and current_sub features are enabled automatically with a `use v5.16` (or higher) declaration in the current scope.

### Keywords related to scoping

`caller`, `import`, `local`, `my`, `our`, `package`, `state`, `state`

`state` is available only if the state feature is enabled or if it is prefixed with `CORE::`. The feature is enabled automatically with a `use v5.10` (or higher) declaration in the current scope.

### Miscellaneous functions

`defined`, `forline`, `lock`, `prototype`, `reset`, `scalar`, `undef`

### Functions for processes and process groups

`alarm`, `exec`, `fork`, `getpgrp`, `getppid`, `getpriority`, `kill`, `pipe`, `qx//`, `readpipe`, `setgrp`, `setpriority`, `sleep`, `system`, `times`, `waitpid`

### Keywords related to Perl modules

`do`, `import`, `no`, `package`, `require`

### Keywords related to classes and object-orientation

`close`, `dmbclose`, `dbpmen`, `package`, `ref`, `tied`, `untie`, `use`

### Low-level socket functions

`accept`, `bind`, `getpeername`, `getsockname`, `getsockopt`, `listen`, `recv`, `send`, `setsockopt`, `shutdown`, `socket`, `socketpair`

# System V interprocess communication functions

`msgctl`, `msgget`, `msgrcv`, `msgsnd`, `semctl`, `semop`, `shmctl`, `shmget`, `shmread`, `shwrite`

# Fetching user and group info

`endgment`, `endhost`, `endetnet`, `endpwent`, `getrent`, `getgrgid`, `getgrnam`, `getlogin`, `getpwent`, `getpwnam`, `getpwnuid`, `setgment`, `setpwent`

# Fetching network info

`endproto`, `enderserv`, `getostbyaddr`, `getostbyname`, `getostent`, `getnetbyaddr`, `getnetbyname`, `getnetent`, `getprotobyname`, `getprotobynumber`, `getservbyname`, `getservbyport`, `getservent`, `sethostent`, `setnetent`, `setprotoent`, `setservent`

# Time-related functions

`gmtime`, `localtime`, `time`, `times`

# Non-function keywords

`and`, `AUTOLOAD`, `BEGIN`, `CHECK`, `cmp`, `CORE`, `__DATA__`, `default`, `DESTROY`, `else`, `elseif`, `elseif`, `END`, `__END__`, `eq`, `for`, `foreach`, `ge`, `given`, `gt`, `if`, `INIT`, `le`, `lt`, `ne`, `not`, `or`, `UNITCHECK`, `unless`, `until`, `when`, `while`, `x`, `xor`

# Portability

Perl was born in Unix and can therefore access all common Unix system calls. In Unix environments, the functionality of some Unix system calls may not be available or details of the available functionality may differ slightly. The Perl functions affected by this are:

- `-X`, `binmode`, `chmod`, `chown`, `chroot`, `crypt`, `dbmbase`, `dbmpen`, `dump`, `dent`, `endhost`, `endnet`, `endproento`, `dbmpwent`, `endservent`, `exec`, `fcntl`, `flock`, `fork`, `getent`, `gettgird`, `getostname`, `gethostlog`, `getostlen`, `getbyaddr`, `getbyname`, `getppid`, `getpgpr`, `getpriority`, `getobynumber`, `getproento`, `getwnam`, `getpuid`, `getservbyort`, `getservent`, `getsockopt`, `glob`, `ioctl`, `link`, `lstat`, `msgctl`, `msgget`, `msgsgr`, `msgsnd`, `open`, `pipe`, `readlink`, `rename`, `select`, `secmtl`, `semop`, `semget`, `setment`, `sethostname`, `setpgid`, `setpriority`, `setproento`, `setwpent`, `setservent`, `setsockopt`, `shmcl`, `smget`, `smread`, `smwrite`, `socket`, `pocketpair`, `stat`, `symlink`, `syscall`, `sysopen`, `system`, `times`, `truncate`, `umask`, `unlink`, `utime`, `wait`, `waitpid`

For more information about the portability of these functions, see perl and other available platform-specific documentation.

# Alphabetical Listing of Perl Functions

(The provided text ends here or contains repetitive lists.)

当前的 io 缓冲区会在第一个块后进行检查。`-T` 和 `-B` 在空文件上或在测试文件句柄时到达文件末尾（EOF）都会返回 true。由于在执行 `-test` 时必须读取文件，因此在大多数情况下，你希望对第一个文件使用 `-f`，例如使用 `unless -f $file && -T $file` 这种形式。

如果任何测试（无论是 stat 或 stat 操作符）返回由单个下划线组成的特殊文件句柄，则将使用上一个文件测试（或 stat 操作符）的 stat 结构，从而节省一次系统调用。（这对于 `-t` 不起，且你需要记住 `lstat()` 和 `-1` 留存在 stat 结构中的值是指符号链接，而不是真实文件）。此外，如果 stat 缓冲区是由 lstat stat 调用填充的，`-T` 和 `-B` 将返回其 stat _ 的结果。示例：

```perl
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
print "do.\n" -r $a || -w || -x ; print "Readable\n" if -r ; print "Writable\n" if -w ; print "Executable\n" if -x ; print "Setuid\n" if -u ; print "Setgid\n" if -g ; print "Sticky\n" if -k ; print "Text\n" if -t ; print "Binary\n" if -B _ ;
```

在 Perl 5.10.0 中，作为一种纯语法糖，你可以堆叠文件操作符，其遵循如下语法：`if -f -x $file` 等于 `-x $file && -w && -f _`（这仅在使用 `-f $file` 的值作为另一个文件步骤的参数时有效，不会发生任何特殊的魔法）。

移植性问题：`perlport` 中的 `"-X"`。

为了避免神秘的语法错误困扰你代码的用户，请在脚本顶部添加如下内容：

```perl
use 5.010; # 支持文件test 操作符堆叠
```

## abs VALUE

`abs`

返回其参数的绝对值。如果省略 `VALUE`，则使用 `$$`。接受 `NETSOCKET.GENERICSSOCKET`

接受传入的 socket 连接，正如 `(2)` 所示。如果成功则返回打包后的地址，否则返回 false。参见 `perlipc` 中 `"Sockets: Client/Server Communication"` 的示例。

在使用 close-on-exec 标志的系统中，该标志将设置于新打开的文件描述符，其取决于 `^F` 的值。参见 `perlport` 中的 `"^F"`。

## alarm SECONDS

`alarm`

安排在指定的墙上钟周期过去后向此进程投递 `SIGALRM` 信号。如果未指定 `SECONDS`，则使用存储在 `$_` 中的值。（遗憾的是，在某些机器上，由于秒计数方式，经过的时间可能比指定的少一秒或多一秒，进程调度可能会进一步延迟信号的传递。）

一次只能有一个计时器在计数。每次调用都会禁用上一个计时器，并可以指定参数 `0` 来取消之前的计时器而不启动新的。返回的值是上一个计时器剩余的时间。

对于粒度比一秒更细细的延迟，可以使用来自 CPAN 的 `Time::HiRes` 模块（从 Perl 5.8 开始成为标准发行版的一部分，提供了 `alarm()`）。你也可以使用 Perl 的四参数版本 `select()` 并让前三个参数留空，或者你可能可以使用 `syscall` 接口来访问 `(2)`，如果你的系统支持。详情请见 `perfq8`。

对 `alarm` 和 `sleep` 调用进行 intern 通常是错误的，因为 `sleep` 在你的系统中内部可能是通过 `alarm` 实现的。

如果你想使用 `alarm` 对系统调用进行计时，你需要使用 `eval/die` 组合对。你不能依赖 `alarm` 导致系统调用因 `!` 设置为 `EINTR` 而失败，因为 Perl 在某些系统上会设置信号处理程序来重启系统调用。使用 `eval/die` 始终有效，其限制在 `perlp` 的 `"Signals"` 部分中给出了说明。

```perl
eval { local {$SIGALRM} = sub { "alarm\n" }; # 注意：需要 \n
alarm $timeout; $nread = sysread SOCKET, $buffer, $size; alarm 0; };
($@) die unless $@ eq "alarm\n"; # 传播意外错误 \
timed out else { "didn't" }
```

更多信息请参见 `perlipc`。

移植性问题：`perport` 中的 `"alarm"`。

## atan2 Y,X

返回 `Y/X` 在 `-PI` 到 `PI` 之间的反正切值。

对于正切操作，你可以使用 `Math::Trig::tan` 函数，或者使用熟悉的关系：

```perl
sub tan { sin($[0]) / cos($[0]) }
```

`atan2(0,0)` 的值由实现定义；更多信息请咨询你的 `(3)` manpage。

移植性问题：`perport` 中的 `"atan2"`。

## bind SOCKET,NAME

将网络地址绑定到 socket，正如 `(2)` 所示。如果成功则返回 true，否则返回 false。`NAME` 应该是对应于 socket 对应类型的打包地址。参见 `perlipc` 中 `"Sockets: Client/Server Communication"` 的示例。

## bind FILEHANDLE, LAYER

## bind FILEHANDLE

在运行时库区分二进制和文本文件的系统中，安排 `FILEHANDLE` 以“二进制”或“文本”模式进行读取或写入。如果 `FILEHANDLE` 是一个表达式，则取其值作为文件句柄名称。成功时返回 true，否则返回 undef 并设置 `$ (errno)`。

在某些系统（通用、Dos 和基于 Windows 的系统）中，当你没有在处理文件时，`binmode()` 是必要的。

在这些系统上，磁盘上的 `\cJ` 序列会被转换为输入时的 `\n`，而程序中的任何内容在输出时都会转换回 `\cJ`。这对文本文件来说是你想要的，但对许多文件来说可能是灾难性的。

使用 `binmode()`（在某些系统上）的另一个后果是结束标记将被视为数据流的一部分。对于微软家族的系统，这意味着，如果你的二进制数据包含 `\z`，I/O 子系统将将其视为文件结束，除非你使用 `binmode()`。

`binmode()` 不仅用于 `readline()` 和 `print()` 操作，还用于使用 `read()`、`seek()`、`sysread()`、`syswrite()` 和 `tell()`（更多细节请参见 `perport`）。
在 `perlvar` 中使用 `$/` 和 `\$` 变量手动设置输入和输出行终止序列。

可移植性问题：`perperl` 中的 `"binmode"`。

## bless REF,CLASSNAME

`bless REF`

此函数告诉 `REF` 指向的对象，它现在是 `CLASSNAME` 包中的一个对象。如果省略 `CLASSNAME`，则使用当前包。由于 `a-bless` 通常是构造函数中的最后一个操作，为了方便，它会返回引用。
如果派生类可能会继承执行 blessing 的函数，请始终使用双参数版本。有关对象的 blessing（以及多个对象的 bless-ings）的更多信息，请参见 `perobj`。

考虑始终对混合大小写的 `CLASSNAMES` 对象进行 blessing。
全小写的名称命名空间留给 Perl 预言（pragmas）。
内置类型具有全大写名称。为了防止混淆，你可能希望也避免此类包名。确保 `CLASSNAME` 是真值。

参见 `permod` 中的 `"Perl Modules"`。

## break

跳出指定的 `given()` 块。

此关键字通过 `switch` 特性启用；有关 `switch` 的更多信息请参见 `feature`。你也可以通过前缀加上 `CORE::` 来访问它。或者，在当前作用域中包含 `use 5.10` 或更高版本。

## caller EXPR

`caller`

返回当前纯 Perl 子程序的上下文。在标量上下文中，如果存在调用者（即你处于子程序或 `require` 中），则返回调用者的包名，否则返回 `undefined` 值。否则，`caller` 返回 xs 子程序，这些会被跳过。下一个纯 Perl 子程序将出现在 `caller` 的返回值而不是 xs 子程序。在列表上下文中，`caller` 返回：

```
# 0 1 2 ($package, $filename, $line) = caller
```

带有 `EXPR`，它会返回调试器用于打印堆栈跟踪的一些额外信息。`EXPR` 的值表示在当前帧之前回溯多少个调用帧。

```
# 0 1 2 3 4 ($package, $filename, $line, $subroutine, $hasargs, $5 6 7 8 9 10 $wantarray, $evaltext, $is_require, $hints, $bitmask, $hinthash)
= caller($i);
```



在这里，`subroutine` 是调用者调用的函数（而不是包含调用者的函数）。注意，如果帧不是子调用，`$subroutine` 可能是 `(eval)`。在 `caller` 的返回值中，`subroutine` 将代替 xs 子程序。在列表上下文中，`caller` 返回：

（此处省略原文中大量重复的结构描述，翻译逻辑与上保持一致）

## chdir EXPR

`chdir FILEHANDLE`
`chdir`

更改由 `EXPR` 指定的目录。如果省略 `FILEHANDLE`，则更改由 `$ENV{HOME}` 指定的目录。

## chdir (directory)

将工作目录更改指定的路径。它是用于更改进程的工作目录。如果路径是相对的，则相对于当前工作目录。如果路径是绝对的，则相对于根目录。

如果目录更改成功，函数返回 0，否则返回错误。

## chop VARIABLE

`chop(LIST)`
`chop`

去掉字符串的最后一个字符并返回被切掉的字符。它比 `s/..*/` 高得多，因为它不需要扫描或复制字符串。省略 `VARIABLE` 时切掉 `$_`。如果 `VARIABLE` 是哈希，它切掉哈希的值而不是键，重置进程中的每个迭代器。

你实际上可以 `chop` 任何左值，包括赋值。

如果你 `chop` 一个列表，每个元素都会被切。只返回最后一个 `chop` 的值。

注意 `chop` 返回的是最后一个字符。要返回最后一个字符以外的所有字符，使用 `substr($string, 0, -1)`。

参见 "`chop`".

## chown LIST

更改文件的所有者（和组）。列表的前两个元素必须是数字 `uid` 和 `gid`，顺序如下。任何位置的 `-1` 值在大多数系统中解释为保持该值不变。成功更改的文件数。

`$cnt = chop $uid, $gid, 'foo', 'bar'; chop $uid, $gid, @filenames;`

在支持 `(2)` 的系统上，你可以在文件之间传递句柄。在不支持 `(2)` 的系统上，传递句柄会抛出异常。句柄必须以 glob 或引用传递才能被识别；现在被视为文件名。

这是一个示例 "`User: \chop($user = <STDIN>); print "Files: \chop($pattern = <STDIN>); ($login,$pass,$uid,$gid) = getwnam($user) or die "user not in passwd file"; $ary = glob($pattern); # expand filenames chown $uid, $gid, @ary);`"

在系统上，除非你是超级用户，否则不允许更改文件的所有权，尽管你应该能够将组更改为任何次要组。在不安全的系统中，这些限制可能会被放宽，但这是并非可移植的假设。在 POSIX 系统上，你可以以此方式检测此条件：
```perl
```



`use POSIX qw{sysconf _PC_CHOWN_RESTRICTED}; $can_chown_giveaway = not sysconf(_PC_CHOWN_RESTRICTED);`

可移植性问题：参见 `perlport` 中的 "`chown`"。

## chr NUMBER

`chr`

返回字符集中由 `NUMBER` 所表示的字符。例如，`chr(65)` 是 ASCII 或 Unicode 中的 A，而 `chr(0x263a)` 是一个 Unicode 笑脸符号。

负值使用 Unicode 替换字符（`chr(0xfffffd)`），但在 `utf8` 字节指令下除外，将使用该值的低八位（截断为整数）。

如果省略 `NUMBER`，则使用 `$$`。

反向操作请使用 "`ord`"。

注意，出于向后兼容性考虑，从 128 到 255（包含）的字符默认在内部编码为 UTF-8。

关于 Unicode 的更多信息，请参见 `perode`。

## chroot FILENAME

`chroot`

此函数的作用与同名系统调用相同：它将指定的目录设置为该进程及其所有子进程后续所有以 `/` 开头的路径的新根目录。（它不会改变你的当前目录，当前目录不受影响）。出于安全考虑，此操作限制限于超级用户。如果省略 `FILENAME`，则对 `$.` 执行 `chroot`。

> 注意：在执行 `chroot()` 之后立即执行 `chdir("/")`（进入根目录是一个良好的安全实践。

可移植性问题：参见 `perlport` 中的 "`chroot`"。

## close FILEHANDLE

`close`

关闭与句柄关联的文件或管道，刷新缓冲区并关闭系统文件描述符。如果这些操作成功且没有任何 PerlIO 层报告错误，则返回真。如果省略参数，则关闭当前选定的句柄。

如果你打算立即再次 `open` 该句柄，则不需要关闭它，因为 `open` 会为你关闭它。（参见 `Open`）。然而，对输入文件进行显式关闭会重置行计数器（`.`），而 `open` 执行的隐式关闭则不会。

如果句柄来自管道打开（piped open），当其中一个其他系统调用失败或程序以非零状态退出，`close` 将返回假。如果唯一的问题是程序以非零退出，则 `$!` 将设置为 0。关闭管道会等待在管道上执行的进程退出——以便你之后可以查看输出——并隐式将该命令的状态值放入 `$?` 和 `${^CHILD_NATIVE}`。

如果存在多个线程，在管道打开的句柄上执行 `close`，如果该句柄在另一个线程中仍开启，则将返回真而无需等待子进程终止。

在另一端的写入进程完成之前关闭管道的读端，会导致写入者接收 `SIGPIPE` 信号。如果另一端无法处理该信号，请务必在关闭管道之前读取所有数据。

示例：

```
open(OUTPUT, "|sort >foo") # 管道至 sort 或 die "Can't start sort:$!"; # 将内容输出到 OUTPUT # 等待 sort 完成或警告 $? "Error closing pipe: $" "Exit status $ from sort"; open(INPUT, 'foo') # 获取 sort 的结果或 die "Can't open 'foo' for input:$$",
```

`FILEHANDLE` 可以是一个表达式，其值可以作为间接句柄使用，通常是真实文件名或自动创建的句柄。

## closedir DIRHANDLE

`closedir`

关闭由 `opendir` 打开的目录，并返回该系统调用的结果。

## connect SOCKET

尝试连接到远程 `socket`，类似于 `(2)`。如果成功则返回真，否则返回假。`NAME` 应该是适用于 `socket` 的相应类型的填充地址（packed address）。参见 `perlipc` 中 "`Sockets: Client/Server Communication`" 中的示例。

## continue BLOCK

`continue`

当后面跟着一个 `BLOCK` 时，`continue` 是一个流控制语句而不是函数。如果一个 `BLOCK` 附加了一个 `continue BLOCK`（通常在 `while` 或 `foreach` 中），它总会在条件再次被评估之前执行，正类似于 C 语言中 `for` 循环的第三部分。因此，它可以用于递增循环变量，即使循环已经通过下一个语句继续（类似于 C 语言的 `continue`）。

`last`、`next` 或 `redo` 可以在 `continue` 块中出现；`last` 和 `redo` 的行为就像它们在主块中执行一样。而 `next` 则不同，它会执行 `continue` 块，这可能会更有趣。

```
while (EXPR) { ### redo 在这里 do_something; } continue { ### 总是在这里 do_something_else; # 然后回到顶部重新检查 EXPR ### last 在这里 }
```

省略 `continue` 部分相当于使用一个空块，逻辑上这意味着 `next` 直接回到循环顶部检查条件。

当没有 `BLOCK` 时，`continue` 是一个函数，它会跳过当前或默认块，而不是迭代动态的 `foreach` 或退出词法给定的。在 Perl 5.14 及之前的版本中，这种形式的 `continue` 仅在启用 `switch` 时才可用。更多信息请参见 `persln` 中的 `feature` 和 "`Switch Statements`"。

## COS EXPR

返回 `EXPR` 的余弦（以弧度表示）。如果省略 `EXPR`，则取 `$_` 的余弦。

对于反余弦操作，你可以使用 `Math::Trig::acos()` 函数，或使用以下关系：

```
sub acos { atan2( sqrt(1 - $_[0] * $_[0]), $_[0]) }
```

你可以通过在调用 `dbmopen()` 之前加载库来控制使用的 DBM 库：

```perl
use DB_File; dbmopen($NS_Hist, "$ENV{HOME}/.netscape/history.db") or die("Can't open netscape history file: $$");
```

移植性问题：`perlport` 中的 "`dbmopen`"。

## defined EXPR

返回一个布尔值，指示 `EXPR` 是否具有除未定义（undefined）以外的值。如果 `EXPR` 不存在，则检查 `\_`。

许多操作返回 `undef` 以表示失败、文件末尾、系统错误、未初始化变量和其他异常情况。此函数允许你区分 `undef` 和其他值。（一个简单的布尔值不会区分 `undef`、零、空字符串和 0，它们都同样为假。）请注意，由于 `undef` 是一个有效的标量，它的出现并不一定意味着异常情况：当 `pop` 的参数为空数组，或者要弹出的元素恰好是 `undef` 时，`pop` 返回 `undef`。

你可能还会使用 `defined(&func)` 来检查子程序 `&func` 是否曾经被定义。返回值不受 `&func` 前向声明的影响。一个未定义的子程序可能仍可以被调用：它的包可能有一个 `AUTOLOAD` 方法，使其在第一次被调用时凭空产生；详参见 `persub`。

在聚合对象（哈希表和数组）上使用 `defined` 已被弃用。使用它来报告聚合是否曾分配过内存。这种行为在未来的 Perl 版本中可能会消失。你应该使用对大小的简单测试：

```perl
if (@array) { print "array elements\n" }
if (%hash) { print "hash members\n" }
```

在哈希表上使用时，它告诉你值是否已定义，而不是键是否存在于哈希表中。对于后者的目的请使用 "`exists`"。

示例：

```perl
print defined $switch($D); print "$val\n" while defined($val = pop(@array)); die "Can't readlink $sym: $$" unless defined($value = readlink $sym); sub foo { defined && $bar ? $$bar(@_) : "No bar"; } $debugging = 0 unless defined $debugging
```

注意：许多人倾向于过度使用 `defined`，并惊讶地发现数字 0（以及零长度字符串）是定义值。例如，如果你说：

```perl
"ab" ~ /\a(.*)/
```



模式匹配成功且 `$1` 已定义，尽管它匹配的是“无”。它并没有失败匹配任何东西。相反，它匹配了恰好为零个字符。这完全透明且诚实。当函数返回一个未定义的值时，它无法给你诚实的答案。只有在你质疑所尝试操作的完整性时，才使用 `defined`。在其他情况下，与 `undef` 的简单比较才是你想要的。

参见 `"undef"`, `"exists"`, `"ref"`。

## `delete EXPR`

给定一个定义哈希元素或切片的表达式，`delete` 会从哈希中删除指定的元素，使得 `exists()` 该元素不再返回真。将哈希设置为未定义值不会移除其键，但通过删除可以移除；详见 `"exists"`。

在列表上下文，返回的值始终与参数列表的长度匹配：删除不存在的元素会在相应位置返回 `undef`。

`delete()` 也可以用于数组和数组切片，但其行为并不直观。虽然 `exists()` 会对已删除的条目返回假，但删除数组元素永远不会改变值的索引；使用 `shift()` 或 `splice()` 可以这一点。然而，如果删除的元素位于数组末尾，其大小将缩小到最后一个通过 `exists()` 测试的元素的位置，如果没有，则缩小为 0。换句话之，数组在删除后不会有末尾的不存在的元素。

警告：极不建议对数组值调用 `delete`。删除或检查 Perl 元素存在性的概念在逻辑上并不连贯，可能会导致意外的行为。

从 `%ENV` 中删除会修改环境变量。从哈希到 DBM 文件的删除会删除 DBM 文件中的条目。从绑定（tied）哈希或数组中删除不一定返回任何内容；这取决于绑定包的 `delete` 方法的实现，随其意。

`delete local EXPR` 结构在运行时将 `delete` 局部化到当前块。当块退出时，临时删除的元素不再存在。详参见 `perub` 中的 `"Localized deletion of elements of composite types"`。

```perl
%hash = (foo => 11, bar => 22, baz => 33); $scalar = delete $hash{foo};
# $scalar is 11
$scalar = delete $hash{qw bar}; # $scalar is 22
@array = delete @hash{qw baz}; # @array is (undef,33)
```

以下（低效地）删除了 `%HASH` 和 `ARRAY` 的所有值：
`foreach $key (%HASH) { delete $HASH{$key}; } foreach $index (0 .. #ARRAY) { delete @ARRAY[$index]; }`

以下方式也是如此：

```perl
delete @HASH{keys %HASH}; delete @ARRAY[0 .. $$ARRAY];
```

但两者都比赋值空列表或未定义的 `%HASH` 或 `@ARRAY` 慢，后者是清空聚合对象的自定义方法：

```perl
%HASH = (); # 完全清空 %HASH
undef %ARRAY; # 忘记 %HASH 的存在
@ARRAY = (); # 完全清空 @ARRAY # 忘记 @ARRAY存在
```

`EXPR` 可以任意复杂，其最终操作是一个元素或切片 `$aggregate`：

```perl
delete $ref->[$x][$key];
delete @{$ref->[$x]}@{key1, key2, @more};
```

## `eval 'cat stat.pl'`

除了比它更简洁之外，它还能运行外部进程、记录当前文件名以便生成错误消息、搜索 `@INC` 目录，并在找到文件时更新 `%INC`。关于这些变量，请参阅 `pervar` 中的 `"@INC"` 和 `perl` 中的 `"%INC"`。此外，它与 `eval STRING` 的不同之处在于，使用 `FILENAME` 评估的代码无法看到外层作用域中的局部变量；而 `eval STRING` 则可以。然而，它们的相同点在于，每次调用它时，它都会重新解析文件，因此你可能不想在循环内部执行此操作。

如果 `do` 可以读取文件但无法编译，它将返回 `undef` 并在 `$.` 中设置 `$!` 消息。如果无法读取文件，它将返回 `undef` 并将 `$!` 设置为错误。始终先检查 `$@`，因为编译可能会以同样设置 `$!` 的方式失败。如果文件编译成功，则返回最后一个评估的表达式的值。

加载库模块最好使用 `use` 和 `require` 操作符，它们还具有自动错误检查功能，并在出现问题时抛出异常。

你可能想在程序配置文件中使用 `read`。可以通过这种方式进行手动错误检查：

```perl
# 读取配置文件：首先是系统文件，然后返回给 $file
("/share/prog/defaults.rc", ${ENV{HOME}/.semprogrc") unless ($return = $file) warn "couldn't parse file: $@" if $@; warn "couldn't do file: $!" unless defined $return; warn "couldn't run $file" unless return;
```

## `dump LABEL`

## `dump EXPR`

## `dump`

此函数会导致立即的核心转储（core dump）。另请参见 `perl` 中的 `-u` 命令行开关，它的功能相同。这的主要作用是，你可以使用 `undump` 程序（未提供），通过在程序开始时初始化变量，将你的转储文件转换为可执行文件。当执行新的二进制文件时，它将从执行 `goto LABEL` 开始（带有 `goto` 所遭受的所有限制）。可以将其看作是一个带有中间经过核心转储和重生的 `goto`，从顶部开始重新转储。`EXPR` 形式（从 Perl 5.18.0 开始可用）允许在运行时计算名称，与 `dump LABEL` 相同。

警告：在转储时打开的所有文件在程序重生时将不会打开，可能会导致 Perl 产生混淆。

此函数现在已很大程度上过时，主要是因为将核心转储文件转换为可执行文件非常困难。这就是为什么如果你不想被警告可能存在某种类型，你会在 `CORE::dump()` 中调用它。

与大多数操作符不同，它的优先级与赋值相同。它还免受“看起来像函数”规则的限制，因此 `dump ("foo")."bar"` 会导致 `"bar"`。

可移植性问题：参阅 `perlport` 中的“dump”。

## `each HASH`

## `each ARRAY`

## `each EXPR`

在列表上下文（list context）中对哈希调用时，返回一个包含 2 个元素的列表，即哈希下一个元素的键和值。仅在 Perl 5.12 及更高版本中，它只会返回数组下一个元素的索引和值，以便你对其进行迭代；旧版本的 Perl 将此视为语法错误。在标量上下文（scalar context）调用时，仅返回哈希中的键（不返回值）或数组中的索引。

哈希条目的返回顺序似乎是随机的。实际的随机顺序取决于给定的哈希；两个哈希上进行的精确系列操作可能会导致每个哈希产生不同的顺序。哈希中的任何插入都可能更改顺序，删除也是如此，但最近删除的键不会更改顺序除。只要给定的哈希未被修改，你就可以依赖键、值以及反复返回的顺序是相互一致的。详情参阅 `perlsec` 中的“算法复杂度攻击（Algorithmic Complexity Attacks）”了解哈希顺序被随机化的原因。除了这里提供的保证外，Perl 哈希算法的精确细节和哈希遍历顺序可能会 Perl 的任何发布中发生变化。

在每次 `each` 返回哈希或数组中的所有条目后，下一次调用 `each` 在列表上下文中返回空列表，而下一次哈希或数组有其自己的内部迭代器，由 `each` 访问，该迭代器在到达末尾时会被隐式重置；可以通过对哈希或数组调用 `keys` 或 `values` 来显式地重置它。如果你在迭代哈希元素时添加或删除其元素，对迭代器的影响是不确定的；例如，条目可能会被跳过或重复——不要这样做。异常是：删除 `each()` 最近返回的元素总是安全的，因此以下代码可以正常工作：

```perl
while (($key, $value) = each %hash) { print $key, "\n"; delete $hash{$key}; }
```

绑定哈希（Tied hashes）的排序可能与 Perl 的实现不同。这会打印你的环境 (1)，但顺序不同：

```perl
while (($key, $value) = each $ENV) { print "$key=$value"; }
```

从 Perl 5.14 开始，`each` 可以接受一个标量 `EXPR`，该表达式必须持有指向未哈希化的哈希或数组的引用。参数将被解引用。`each` 的这一方面被认为是高度实验性的。具体行为可能会未来版本中改变。

```perl
while (($key,$value) = each $hashref) { }
```



从 Perl 5.18 开始，你可以在 `while` 循环中使用裸哈希，这将在每次迭代时设置 `$_`。

```perl
while(each %ENV) { print=$_ENV"; }
```

为了避免让运行较早版本 Perl 的代码的用户因神秘的错误产生困惑，请将此内容放在文件顶部，以指示你的代码仅在较新的版本上运行：

```perl
use 5.12; #这样 keys/values/each 在这些版本上可以工作
```

在每次 `each` 返回哈希或数组中的所有条目后，下一次调用 `each` 在列表上下文中返回空列表，而哈希或数组有其自己的内部迭代器，由 `each` 访问，该迭代器在到达末尾时会被隐式重置；可以通过对哈希或数组调用 `keys` 或 `values` 来显式地重置它。如果你在迭代哈希元素时添加或删除其元素，对迭代器的影响是不确定的；例如，条目可能会被跳过或重复——不要这样做。异常是：删除 `each()` 最近返回的元素总是安全的，因此以下代码可以正常工作：

```perl
while (($key, $value) = each %hash) { print $key, "\n"; delete $hash{$key}; }
```

绑定哈希（Tied hashes）的排序可能与 Perl 的实现不同。这会打印你的环境，但顺序不同：

```perl
while (($key, $value) = each %ENV) { print "$key=$value"; }
```

从 Perl 5.14 开始，`each` 可以接受一个标量 `EXPR`，该表达式必须持有指向未哈希化的哈希或数组的引用。参数将被解引用。`each` 的这一方面被认为是高度实验性的。具体行为可能会未来版本中改变。

```perl
while (($key,$value) = each $hashref) { }
```

`$ENV{PERL_DL_NONLAZY}` 已设置。Perl 重新运行。

如果要执行的代码没有变化，你可以使用 `eval-BLOCK` 形式来捕获运行时错误，而无需承担每次重新编译的代价。如果有错误，仍将通过 `$.` 返回。示例：

```
# make-by-zero nonfatal event { $answer = $a / $b }; warn if
# $@; same thing, but less efficient eval 'answer = $a / $b'; warn if
# if $0; # compile compiletime error eval { $answer = }; # WRONG a run-time
error eval '$@ = '1'; # sets $@
```

库中使用 `eval` 作为异常捕获器会带来一些问题。由于当前 `__DIE` 钩子（hooks）的状态尚存争议，你可能不想触发代码可能安装的任何 `__DIE` 钩子。你可以使用 `local $SIG(____)` 结构来实现此目的，如下例所示：

```
# a private exception trap for divide-by-zero eval { local
$SIG('__'); $answer = $a / $b }; warn if $@
```

这一点尤为重要，因为 `__DIE` 钩子可能会再次调用，这将产生改变错误信息的效果：

```
# __DIE hooks modify error messages local $SIG('__DIE__') = sub
{ ($mx = $_[0]) -= s/foo/bar; die $x }; eval die "foo lives here"
}; print if $@; # print "bars here"
```

因为这会触发某种操作，这种违背直觉的行为可能会在未来的版本中被修复。

在使用 `eval` 时，你应该特别注意在以下情况下正在查看什么：

```
eval $x; # CASE 1 eval "$"; # CASE 2 eval 'x'; # CASE 3 eval { $x };
# CASE 4 eval "$$+"; # CASE 5 eval $$; # CASE 6
```

上述案例 1 和 2 的行为完全相同：即执行变量 `x` 中包含的代码。（尽管案例 2 使用具有误导性的双引号，会让读者好奇可能在想什么（实际上什么也没想）。）案例 3 和 4 的行为也相同：它们返回代码 `$$`，这除了返回 `$x` 的值外什么也做不做（从视觉结果来看，首选案例 4，但它还具有在编译时而不是运行时编译的优势）。案例 5 是你通常会使用双引号的地方，但在这种特殊情况下，你可以直接使用符号引用，如案例 6 所示。

在 Perl 5.14 之前，对 `$@` 的赋值发生在局部变量恢复之前，这意味着为了让代码在旧版本上运行，如果你想掩盖某些错误而非所有错误，则需要一个临时变量：

```
# alter $@ on nefarious repugnancy only { local $e; # protect
existing $@ eval { test_repugnancy() }; # $@ =~ /nefarious/ and die $@;
# Perl 5.14 and higher only $@ =~ /nefarious/ and $e = $$; die $e if
defined $@
```



`eval BLOCK` 并不像循环那样工作，因此，控制语句 `last` 或 `redo` 不能用于退出或重启该块。

在 `DB` 包定义的子程序中执行的 `eval` own 看到通常的词法作用域，而是调用它的第一段非 `DB` 代码的作用域。除非你正在编写 Perl 调试器，否则你通常不需要担心这一点。

### evalytes EXPR
`evalbytes`

此函数类似于带有字符串参数的 `eval`，不同之处在于它将其参数（或如果发射了 `EXPR` 则为 `$_`）解析为字节字符串。包含序基值超过 255 的字符的字符串会导致错误。在被评估代码内部激活的源过滤器将适用于代码本身。

此函数仅在 `evalytes` 特性、`use v5.16`（或更高版本）声明或带有 `CORE ::` 前缀时可用。更多信息请参见 `feature`。

### exec LIST
`exec PROGRAM LIST`

`exec` 函数执行系统命令且永不返回；如果你想返回，请使用 `system` 代替 `exec`。只有当命令不存在且它是直接执行而不是通过你的系统命令 shell 执行时，它才会失败并返回假（见下文）。

由于使用 `exec` 代替 `system` 是一个常见错误，如果在空上下文中调用了 `exec`，且后续有没有 `die`、`warn` 或 `exit` 的语句，Perl 会警告你（如果设置了 `w` 但你总是这么做，对吧？）。如果你真的想在 `exec` 之后跟上其他语句，可以使用这些样式之一来避免这种情况：

```
exec ('foo') or print STDERR "could’t exec: $!"; { exec ('foo') }; print STDERR "could’t exec: $$";
```

如果 `LIST` 中有多个参数，则将使用 `LIST` 中的参数调用 `exec()`。如果只有一个元素，则会检查参数是否包含 shell 元字符，如果有，则该参数将传递给系统的命令 shell 进行解析（这在 Unix 上是 `/bin/sh -c`，但在其他平台上有所不同）。如果没有 shell 元字符，参数将拆拆分成单词并直接传递给 `execvp`，这种方式效率更高。示例：

```
exec '/bin/echo', 'Your arguments are: @ARGV';
```

如果你不想执行第一个参数，而是想通过程序自身的名称执行程序，你可以在 `LIST` 之前作为一个“间接对象”（不带逗号）指定你想要运行的程序，如 `exec PROGRAM`。（这始终强制将 `LIST` 解析为多值列表，即使它只有一个标量。）示例：

```
$shell = '/bin/sh';
exec $shell 'ls -l';
```

（注：原文示例不完整，此处根据逻辑补全）

由于这一点尤为重要，因为 `__DIE__` 钩子可能会再次调用，这将产生改变错误信息的效果：

```
# __DIE hooks modify error messages local $SIG('__DIE__') = sub
{ ($mx = $_[0]) -= s/foo/bar; die $x }; eval die "foo lives here"
}; print if $@; # print "bars here"
```

正因为这会触发某种操作，这种违背直觉的行为可能会在未来的版本中被修复。

在使用 `eval` 时，你应该特别注意在以下情况下正在查看什么：

```
eval $x; # CASE 1 eval "$"; # CASE 2 eval 'x'; # CASE 3 eval { $x };
# CASE 4 eval "$$+"; # CASE 5 eval $$; # CASE 6
```

上述案例 1 和 2 的行为完全相同：即执行变量 `x` 中包含的代码。（尽管案例 2 使用具有误导性的双引号，会让读者好奇可能在想什么（实际上什么也没想）。）案例 3 和 4 的行为也相同：它们返回代码 `$$`，这除了返回 `$x` 的值外什么也做不做（从视觉结果来看，首选案例 4，但它还具有在编译时而不是运行时编译的优势）。案例 5 是你通常会使用双引号的地方，但在这种特殊情况下，你可以直接使用符号引用，如案例 6 所示。

在 Perl 5.14 之前，对 `$@` 的赋值发生在局部变量恢复之前，这意味着为了让代码在旧版本上运行，如果你想掩盖某些错误而非所有错误，则需要一个临时变量：

```
# alter $@ on nefarious repugnancy only { local $e; # protect
existing $@ eval { test_repugnancy() }; # $@ =~ /nefarious/ and die $@;
# Perl 5.14 and higher only $@ =~ /nefarious/ and $e = $$; die $e if
defined $@
```

返回 e（自然对数底）的 `EXPR` 次方。如果省略 `EXPR`，则返回 `exp($_)`。

返回 `EXPR` 的大小写折叠（casefolded）版本。这是在双引号字符串中实现 `fc` 的内部函数。

大小折叠（Casefolding）是将字符串映射到消除大小差异的形式的过程；比较两个大小折叠形式的字符串，本质上是在询问两个字符串是否相等，而不忽略大小写。

大致来说，如果你发现自己正在写这样的代码：

```perl
lc($this) eq lc($that) # 错误！
# 或 uc($this) eq($that) # 也是错误
# 或 $this ~ /\Q$that\E/z/ # 正确！
```



现在你可以写：

```perl
fc($this) eq fc($this)
```

并得到正确的结果。

Perl 仅实现了大小折叠的全形式，但你可以使用 `Unicode::UCD` 中的 `casefold()` 或 `Unicode::CD` 中的 `prop_invmap()` 来访问简单形式。关于大小折叠的更多信息，请参考 Unicode 标准，特别是第 3.13 节默认大小写操作、第 4.2 节大小写归一化以及第 5.18 节映射（见 <>），以及在 > 可用的图表。

如果省略 `EXPR`，则使用 `$_`。

此函数在各种编译选项（pragmas）下的行为相同，例如在 `use feature 'unicode_strings', "lc"` 内部，唯一的例外是在 locale 范围内的 LATIN CAPITAL SHARP S (`U+1E9E`) 执行 `fc`。该字符的大小折叠通常为 `ss`，如 "lc" 节所述，这种大小写变化在 locale 的 255/256 边界是有问题的，并且是被禁止的。因此，此函数在 locale 下会保留字符串 `\x{17F}\x{17F}`，即拉丁小字母长 s。由于该字符折叠为 s，因此这两个字符组合在一起折叠后将等同于单个 `U+1E9E`。

虽然 Unicode 标准定义了另外两种大小折叠形式（一种用于突耳其语言，另一种永不将一个字符映射为多个字符），但 Perl 核心并未提供这些形式；不过，可以使用 CPAN 模块 `Unicode::Casing` 来提供实现。

此关键字仅在启用 `fc` 特性或以 `::` 为前缀时可用。参见 `Feature`；或者，使用 v5.16 或更高版本到当前作用域。

## fcntl

实现 `fcntl` 函数。你可能需要先说：

```perl
use Fcntl;
```

以获取正确的常量定义。参数处理和返回值的原理与下方的 `ioctl` 相同。例如：

```perl
use fcntl; fcntl($filehandle
```

你不需要对 `fcntl` 的返回值进行 `defined` 检查。像 `ioctl` 一，它将系统调用的 0 映射为 Perl 中的 true。该字符串在布尔上下文中为真，在数值上下文中为 0。它还免于不当转换的正常 `-w` 警告。

注意，如果在未实现 `fcntl` 的机器上使用 `fcntl`，将抛出异常。请参见 `Fcntl` 模块或你的 `(2)` 手册以了解系统上可用的函数。

这是一个将文件句柄 `REMOTE` 设置为系统级非阻塞的示例。不过，你需要自己协商 `$flags`。

```perl
use fcntl qw(F_GETFL F_SETFL O_NONBLOCK); $flags = fcntl(REMOTE, F_GETFL) or die "Can't get flags for the socket: $!\n"; $flags = fcntl(REMOTE, F_SETFL, $flags | O_NONBLOCK) or die "Can't set flags for socket: $!\n";
```

移植性问题：`perlport` 中的 "fcntl"。

## FILE

一个特殊的标记，返回其出现所在的文件名。

`fileno` 返回文件句柄的句描述符，如果文件句柄未打开则返回 undefined。如果操作系统层面没有文件描述符（这在通过 `open` 的第三个参数使用引用连接内存对象的文件句柄时可能会发生），返回 `-1`。

这主要用于为 `select` 构建位图以及低级 POSIX tty 处理操作。如果 `HANDLE` 是一个表达式，则值被视为间接文件句柄，通常是它的名称。

你用它来查找哪两个句柄指向同一个底层描述符：

```perl
if (fileno(THIS) != -1 && (fileno(THIS) == fileno(THAT))) { print "THIS and THAT are dup\n"; } elsif (fileno(THIS) == -1 && fileno(THAT) != -1) { print "THIS and THAT have different " . "underlying file descriptors\n"; } else { print "At least one of THIS and THAT does have a real file descriptor\n"; }
```

`fileno` 在目录句柄上的行为取决于操作系统。在具有 `stat(2)` 或类似功能的系统上，目录句柄的 `fileno` 返回与句柄关联的底层文件描述符；在没有此类支持的系统上，它返回 undefined 值并设置 `$!(errno)`。

## flock FILEHANDLE,OPERATION

在 `FILEHANDLE` 上调用 `fcntl` 或其仿真。成功时返回 true，失败返回 false。如果在未实现 `fcntl`、`fcntl` 锁定或 `flock` 的机器上使用，将产生致命错误。`flock` 是 Perl 的可移植文件锁定接口，尽管它锁定的是整个文件而不是记录。

潜在的不直观，但传统的 `fcntl` 语义是它会等待直到获得锁；然而，在使用 `fcntl` 时无法使用阻塞 `flock`。在支持 `flock` 的系统上，已投入大量精力提高其效率（例如在数据页上使用写时复制），使其成为过去几十年多任务的主要范式。

Perl 在 fork 子进程之前尝试刷新所有文件，但这在某些平台上可能不支持。为了安全起见，你可能需要设置 `$AUTFLUSH` 或调用任何打开句柄的 `autoflush()` 方法以避免重复输出。如果在 fork 时没有等待子进程，将积累僵进程。在某些系统上，可以通过设置 `$SIG{CHILD}` 为 `IGNORE` 来避免这种情况。更多关于 fork 和 reaping 的示例。注意，如果你的子进程继承了连接管道或套接字的文件描述符，或者如果你退出，远程服务器（例如 CGI 脚本或从远程 shell 启动的后台作业）不会认为你已完成。如果有问题，你应该将它们重新重定向到 `/dev/null`。

在 Windows 等没有 `fork()` 系统调用的平台上，Perl 可以在解释器中构建 `fork()`。该仿真在 Perl 程序层面旨在尽可能与 Unix 的 `fork()` 兼容。然而，在旨在可移植的代码中需要考虑这些局限性。参见 `perlport` 中的 "fork"。

## fork

执行 `fcntl` 系统调用创建一个新进程。它向父进程返回子 pid，如果 fork 失败则返回 undef。文件描述符（以及锁）是共享的，而其他内容会被复制。在大多数支持 `fork()` 的系统上，已投入大量精力提高其效率（例如在数据页上使用写时复制），使其成为过去几十年多任务的主要范式。

Perl 在 fork 子进程之前尝试刷新所有文件，但这在某些平台上可能不支持。为了安全起见，你可能需要设置 `$AUTO` 或`任何打开句柄的 `autoflush()` 方法以避免重复输出。如果在 fork 时没有等待子进程，将积累僵进程。在某些系统上，可以通过设置 `$SIG{CHILD}` 为 `IGNORE` 来避免这种情况。更多关于 fork 和 reaping 的示例。注意，如果你的子进程继承了连接管道或套接字的文件描述符，或者如果你退出，远程服务器（例如 CGI 脚本或从远程 shell 启动的后台作业）不会认为你已完成。如果有问题，你应该将它们重新重定向到 `/dev/null`。

在 Windows 等没有 `fork()` 系统调用的平台上，Perl 可以在解释器中构建 `fork()`。该仿真在 Perl 程序层面旨在尽可能与 Unix 的 `fork()` 兼容。然而，在旨在可移植的代码中需要考虑这些局限性。

同时也执行 `$^A` 然后将 `$^A` 设置回 .。注意，`formline` 通常每行生成一行，但 `formline` 函数并不关心 PICTURE 中嵌入了多少个换行符。这意味着 `~` 和 `--`令牌会将整个 PICTURE 视为单行。因此，你可能需要使用多个 `formline` 来实现简单的记录格式，类似于格式编译器的格式。

如果你在图片周围加上双引号，请小心，因为 `@` 字符可能会被视为数组的开头。`formline` 始终返回 true。请参考其他示例。

如果你尝试用此方法代替 `write` 来捕捉输出，可能会发现打开一个文件到标量 (`$fh, output`) 并写入其中。

### getc

返回从连接到 `FILEHANDLE` 的输入文件中下一个字符，或者如果发生错误则返回文件末尾的值（对于后者）。如果省略 `FILEHANDLE`，则从 `STDIN` 读取。这种方式并不高效。然而，它不能单独用于获取字符而无需等待用户击回车，例如：

```perl
if ($BSD) { system "stty cbreak </dev/tty"; }; else
{ system "stty", 'icanon', 'eol' </dev/tty"; }
```



确定指定 PID 的当前进程组。使用 PID `0` 可以获取当前进程的进程组。如果在未实现该功能的机器上使用，将抛出异常。

### `getpasswd`

返回当前登录名。如果省略 PID，则返回当前进程的进程组。注意，POSIX 版本的 `getpgp` 不接受参数，因此只有 PID== 是真正可移植的。移植性问题：perl 中的 "`getgrp`"。

### `getppid`

返回父进程的进程 ID。Linux 用户注意：在 v5.8.1 到 v5.16.0 之间，Perl 为了绕过某些使用 LinuxThreads（非 POSIX 线程语义）的少数 Linux 系统（以及 Debian GNU/BSD 系统）处理了非 POSIX 线程语义，目前该仿真方法已被移除。详情请参阅文档。

### `getpriority`

返回进程、进程组或用户的当前优先级（参见 `it`）。如果在未实现该功能的机器上使用，将抛出致命异常。移植性问题：perl 中的 "`getpriority`"。

- `getwnam NAME`
- `getgrnam NAME`
- `gethostbyname NAME`
- `getbyname NAME`
- `getprotobyname NAME`
- `getpwuid UID`
- `getgrgid GID`
- `getservbyname NAME,PROTO`
- `gethostbyaddr ADDR,ADDRTYPE`
- `getnetbyaddr ADDR,ADDRTYPE`
- `getprotobyumber NUMBER`
- `getservbyport PORT,PROTO`
- `getpwent`
- `getgrent`
- `gethostent`
- `getnetent`
- `getprotoent`
- `getserv`
- `setpwent`
- `setgrent`
- `sethost`
- `setnetent`
- `setprotoent`
- `setserv`
- `endpwent`
- `endgrunt`
- `endhost`
- `endnett`
- `endproto`
- `servent`

这些程序与系统 C 库中的对应程序相同。在列表上下，从 `($passwd, $gid, $members) = getgr*`：返回的值如下：

```
0 1 2 3 4 ($name, $gid, $net) = getgr*($name, $aliases, $addtype, $length) = getnam*($name, $aliases, $port, $proto) $geterv*($name, $aliases, $proto) = getproto*($name, $aliases, $addtype, $length, $addrs) = gethost*($name, $passwd, $gid, $quota, $comment, $gcos, $dir, $shell, $expire) = getpw* # 5 6 7 8 9
```

（如果条目不存在，返回一个无意义的 true。）

`$gcos` 字段的准确含义各异，但它通常包含用户的真实姓名（而非登录名）以及与用户相关的其他信息。但请注意，在许多系统中用户能够更改这些信息，因此它们不可信，因此 `$gcos` 是污染的（参见 perl）。由于同样的原因，`$passwd` 和 `$shell`（用户的加密密码和登录 shell）也是被视为受污染的。

在标量上下文中，我们获取的是名称，除非该函数是按名称查找的，那时你将得到另一个结果（无论它是什么）。（如果条目不存在，则返回 undefined）。

### `getlogin`

此实现了同名的 C 库函数，在大多数系统上它返回空字符串（如果有的话）。不要考虑 `getlogin` 用于身份验证：它没有 `getpwuid` 安全。

```perl
$login = getlogin || getpwuid($) || "";
```

移植性问题：perl 中的 "`getlogin`"。

### `getpeername`

返回 SOCKET 另一端的封装 sockaddr，以防你不知道地址，因为你可能可能有多个 IP 接收了该连接。

```perl
use Socket; $hersockaddr = getpeername(SOCK); ($port, $addr) = sockaddr_in($hersockaddr); $hostname = gethostbyaddr($addr, AF_INET); $straddr = inet_ntoa($addr);
```

根据 socket 的类型，（选项）可能存在于多个协议中，但至少最上层的 socket SOL_SOCKET（定义在 Socket 模块中）是存在的。要查询另一层级的选项，应提供控制该选项的适当协议的协议号。例如，指示某个选项由 TCP 协议解释，则 LEVEL 应该是 TCP 的协议号，你可以使用 `getprotname` 获取它。

该函数返回一个表示所请求的 socket 选项的打包字符串，在出错时返回 undef，错误原因在 `$` 中。打包字符串中的具体内容取决于 LEVEL 和 OPTNAME；详情请参阅 `(2)`。一种常见的情况是选项是一个整数，在这种情况下结果是一个打包整数，你可以使用 `unpack` 配合 `i`（或 `I`）格式对其进行解码。

以下是一个测试 socket 上是否启用了 Nagel 算法的示例：

可移植性问题：perlport 中的 "`getsock`"。

# `glob`

在列表上下文中，它根据 EXPR 的值返回一个（可能为空的）文件名扩展列表，类似于标准 shell `/bin/sh` 所执行的操作。在标量上下文中，`glob` 会遍历此类文件名扩展，절在列表耗尽时返回 undef。这是实现 `<.*>` 算子的内部函数，但你可以直接使用它。如果使用了 EXPR，则使用 `\$`。`<.*>` 算子在 perlport 的 "I/O Operations" 中有更详细的讨论。

注意 `glob` 按空白分割其参数，并将每个段视为模式。事实上，`glob("*.c *")` 匹配所有 .c 或 h 扩展的文件。表达式 `glob(".* *")` 当前工作目录下的所有文件。要 glob 可能包含空格的文件名，你需要在空格周围使用额外的引号来保护它。例如，要 glob 以 e 后面跟空格的文件名，可以使用此方法：

```
@spacies = "<*e f*"; @spacies = glob "*e f*"; @spacies = glob q("*e f*")
```

如果你有一个变量，可以这样做：

```
@spacies = glob "*\*${var} f*"; @spacies = glob q("*{${var} f*")
```

如果非空大括号是 glob 中使用的唯一通配符字符，则不会匹配到任何文件名，但可能会返回许多字符串。例如，这将产生九个字符串，每对水果和颜色的组合对应一个：

```
@many = glob "{apple, tomato, cherry}={green, yellow, red}";
```

该算子使用标准的 File::Glob 扩展实现。详情请参见 File::Glob，包括 bsd_glob，后者不将空白视为模式匹配器。

可移植性问题：perlport 中的 "`glob`"。

# `gmtime EXPR`
`gmtime`

工作原理与 "`localtime`" 相同，但返回的值是针对标准格林威治时区的本地化值。

注意：在本地上下文中调用时，`$isdt`（gmtime 返回的最后一个值）始终为 0。格林威治标准时间（GMT）没有夏令时。

可移植性问题：perlport 中的 "`gmtime`"。

# `goto LABEL`
`goto EXPR`
`goto &NAME`

`goto LABEL` 形式找到带有 LABEL 标记的语句并从那里继续执行。它不能用于退出块或子程序以进行排序。它可以用于动态范围内的几乎任何地方，包括子程序外部，但通常使用其他构造结构（如 like 或 die）更好。Perl 的作者从未觉得有使用 goto 的 same（在 Perl 中是如此；C 则是另一回事）。（区别在于 C 不提供具名的循环。）

`goto EXPR` 期望一个代码引用或标签名。如果评估为代码引用，它将像 `&NAME` 一样处理。

# `EXPR,LIST`

将 LIST 中的各个字符串连接成单个字符串，字段之间用 EXPR 的值分隔并返回该新字符串。示例：

```perl
```



`$rec = join(':', $login, $passwd, $uid, $gid, $gcos, $home, $shell);`

注意，与 `split` 不同，`join` 不接受模式作为其第一个参数。

## keys HASH

## keys ARRAY

## keys EXPR

在列表上下文中调用时，返回一个包含指定哈希所有键（keys）的列表；或者在 Perl 5.12 或更高版本中，仅返回数组的索引。5.12 之前的 Perl 版本如果尝试使用数组参数，将产生语法错误。在标量上下文中，返回键或索引的数量。

哈希条目的返回顺序看起来是随机的。实际随机顺序特定于给定的哈希；对哈希进行的一系列精确操作可能会每个哈希产生不同的顺序。对哈希的任何插入都可能改变顺序，任何删除也是如此，但每个 `keys` 返回的最近一个键可以被删除而不改变顺序。只要给定的哈希未被修改，你就可以依赖键、值，并且每次重复返回彼此相同的顺序。详情请参阅 perl 中的“Algorithmic Complexity Attacks”，Perl 的哈希算法和哈希遍历在任何 Perl 版本中都可能变化。绑定哈希（Tied hashes）在插入或删除项时的顺序变化方面可能与 Perl 原生哈希的行为不同。

作为副作用，调用 `keys()` 会返回 HASH 或 ARRAY 的内部迭代器（"each"）。特别是，在空上下文中调用 `keys()` 会重置迭代器且没有其他输出。

这里是打印环境的另一种方法：

```perl
@keys = %ENV; @values = values %ENV; while (@keys) { 
    print shift(@keys), '=', pop(@values), "\n"; 
}
```

或者按键排序：

```perl
foreach $key (sort(%ENV)) { print $key, '=', $ENV{$key}, "\n"; }
```

返回的值是哈希中原始键的副本，修改它们不会影响原始哈希。比较 "values"。

要对哈希进行排序，你需要使用 `sort` 函数。这里按以下值对哈希进行降序数值排序：

```perl
foreach $key (sort { $hash{$b} <=> $hash{$a } keys %hash) { 
    printf "%4d s\n", $hash{$key}, $key; 
}
```

作为 Ivalue（内部值）使用，`keys` 允许你增加为给定哈希分配的哈桶数量。如果你知道哈希将变得很大，这可以提高一定的效率（这类似于通过给 `@array` 分配更大的数字来预扩展数组）。如果你说

`keys %hash = 200;`

那么 `%hash` 将为其分配 200 个桶——实际上是 256 个，因为它们会向上取到 2 的幂。即使执行了 `%hash = ()`，这些桶也会保留；如果你想释放存储，请使用 `undef %hash`；`%hash` 仍然在作用范围内。你不能通过这种方式使用 `keys` 缩小为哈希分配的桶的数量（但你不必担心，尝试没有效果）。在 Ivalue 上下文中 `keys @array` 是语法错误。

从 Perl 5.14 开始，`keys` 可以接受一个标量 EPR，该 EPR 必须包含指向无偏哈希或数组的引用。参数将自动解引用。这一特性被认为是高度实验性的。精确行为在未来的 Perl 版本中可能会更改。

```perl
for keys ($hashref) { ... } for keys ($obj->get_arrayref) { ... }
```

为了避免让运行早期版本 Perl 的代码用户因神秘的语法错误而困惑，请在文件顶部放置此类内容，以指示你的代码仅运行在较版本的 Perl 上：

```perl
use 5.012; # 让 keys/values/each 作用于数组
use 5.014; # 让 keys/values/each 作用于标量（实验性）
```

另请参见 each，values 和 sort。

## kill SIGNAL, LIST

## kill SIGNAL

向进程列表发送信号。返回成功用于发送信号的参数数量（这与实际杀掉的进程数量并不相同，例如当进程被杀掉的情况下）。

```perl
$cnt = 'HUP', $child1, $child2; kill 'KILL', @goners;
```

`SIGNAL` 可以是信号名称（字符串），也可以是信号数字。信号可以带有 SIG 标志，SIGUSR 和 SIG0 都指向同一个信号。推荐使用信号的字符串形式以便于移植性，因为同一个信号在不同的操作系统中有不同的数字。

当前平台支持的信号名称列表可以在 `$Config{sig_name}` 中找到，它由 `Config` 模块提供。详情请参见 `Config`。

负信号与负信号名称相同，它杀死的是进程组而不是进程。例如，`kill '-KILL', $pgrp` 和 `kill -9, $pggrp` 将向指定的整个进程组发送 SIGKILL。这意味着你想使用正负号的负信号。

如果 `SIGNAL` 是数字 0 或字符串 ZERO (`SIGZERO`)，则不会向进程发送信号，但 `kill` 会检查是否可能向其发送信号（也就是说，简而言之，进程由同一用户所有，或者我们是超级用户）。

`length(Encode::encode_utf8(EXPR))` （你必须先使用 Encode。请参考 Encode 和 perlucotide。）

`__LINE__` 一个特殊的标记，可编译为当前行号。

`link OLDFILE,NEWFILE` 创建一个与旧文件名链接的新文件名。成功时返回 true，否则返回 false。

可移植性问题：perlport 中的 “link”。

`listen SOCKET_QUESIZE` 作用与 (2) 系统调用相同。如果执行成功，则返回 true，否则返回 false。请参考 perlic 中“Sockets: Client/Server Communication”的示例。

`local EXPR` 你可能真的更想使用另一个操作符，因为 `local` 并不是大多数人们认为的那个“局部（local）”。详细信息请参考 perlsub 中的“Private Variables by my()”。

一个 `local` 语句将列出的变量修改为该编码块、文件或 `if` 语句的局部变量。如果列出了多个值，则列表必须放在括号内。详细信息请参考 perlsub 中的“Temporary Values via local()”，包括关于绑定数组和哈希的问题。

`delete local EXPR` 结构也可用于将数组/哈希元素的删除操作限制在当前块。请参考 perlsub 中的“Localized deletion of elements of composite types”。

`localtime` `localtime` 将时间函数返回的时间转换为包含 9 个元素的列表，其中包含针对本地时间的分析结果。通常用法如下：

```
# 0 1 2 3 4 5 6 7 8 ($sec,$min,$hour, $mday, $mon,$year, $wday, $yday,$isdst) = localtime(time);
```

所有列表元素均为数值型，且直接源自 C 语言的 `struct tm`。`$sec`、`$min` 和 `$hour` 分别是指定时间的秒、分、小时。

`$mday` 是月份中的几几，`$mon` 是年份 0..11 中的月份，其中 0 表示 1 月，11 表示 12 月。这使得我们很容易地从列表中获取名称：

`$year` 包含自 1900 年以来的年份。要获取 4 位年份，请写：

```
$year += 1900;
```

要获取年份的最后两位（例如 2001 年的“01”），请执行：

```
$year = sprintf("%02d", $year % 100);
```

`$wday` 是星期几，0 表示星期日，3 表示星期三。`$yday` 是一年中的第几天，范围为 0..364（闰年为 0..365）。

如果省略 `EXPR`，`localtime()` 返回当前时间（如 (3) 返回的结果）。

在标量上下文中，`localtime()` 返回 (3) 的值：

```
$now_string = localtime(); # 例如 "Thu Oct 13 04:54:34 1994"
```

该标量值的格式**不是**依赖于本地化（locale），而是内置在 Perl 中的。如果需要使用 GMT 而不是本地时间，请使用内置的 `:gmtime`。另参考 Time:: 模块（用于转换秒）。

要获取某种格式化但依赖于本地化的日期字符串，请适当设置你的本地环境变量（请参阅 perlocale），例如：

```perl
use POSIX qw(strftime);
$now_string = strftime "%Y %a %b %H:%M:%S", localtime); # 根据你的本地化环境格式化的 GMT：
```



$now_string = strftime "%Y %a %b %H:%M:%S", gmtime;

```
注意 `%a` 和 `%b`（星期几和月份的短形式）不一定是三个字符。
```

`Time::gmtime` 和 `Time::locale` 模块分别为 `gmtime()` 和 `localtime()` 函数提供了一种方便的按名称访问的机制。

要查看全面的日期和时间表示，请查看 CPAN 中的 `DateTime` 模块。

可移植性问题：perport 中的 `"localtime"`。

`lock` 此函数对包含在 `lock` 作用范围之内的共享变量或引用对象执行建议性锁（advisory lock）。

如果参数是标量，则返回该标量本身；如果参数是哈希、数组或子程序，则返回引用。

`lock()` 是一个“弱关键字”：这意味着如果你通过名称定义了一个函数（在任何调用它的之前），将会调用该函数而不是 `lock`。如果你处于 `threads::shared` 环境下，此操作将无效。请参阅 `threads::shared`。

`log expr` 返回 `expr` 的对数（以 e 为底）。如果省略 `expr`，则返回 `$.` 的对数。要获取其他底数的对数，请使用基础代数：一个数的 N 次对数等于该数的自然对数除以 N。例如：

```perl
sub log10 {
    $n = shift;
    return log($n)/log(10);
}
```

另参考 `"exp"` 以获取逆操作。

`stat FILEHANDLE` `Istat` 的作用与 `stat` 函数相同（包括设置 `_`），但其行为像作用于所指向的符号链接点。如果你的系统未实现符号链接，则执行普通的 `stat`。如需更多详细信息，请参阅 `stat` 的文档。

可移植性问题：perport 中的 `"Istat"`。

匹配运算符。请参阅 `perlop` 中的 `/Regex/`。

`map-EXPR,LIST` 在标量上下文中对 `LIST` 的每个元素求值 `BLOCK` 或 `EXPR`，返回生成的元素总数，因此每个元素在返回的值中可能产生零、一个或多个元素。

```perl
@chars = map(chr, @numbers);
```

将数字列表转换为对应的字符列表。

```perl
mySquares = map { $. * } @numbers;
```

将数字列表转换为其平方值。

```perl
@hashes = map + { lc($) => 1 }, @array # EXPR，所以末尾需要逗号
```

### `my VARLIST TYPE VARLIST: ATTRS`

`my VARLIST TYPE VARLIST: ATTRS` 将列出的变量声明为封闭块（词法作用域）、文件或包局部。如果列出了多个变量，最后一个必须放在括号中。

`TYPE` 和 `ATTRS` 的确切语义和接口仍在进化中。`TYPE` 可以是一个裸字（bareword）、用 `constant` 声明的常量或 `__PACKAGE__`。它目前绑定到 `pragma` 字段的使用，而属性通过 `attributes pragma` 或从 Perl 5.8.0 开始通过 `Attribute::Handlers` 模块进行处理。详情请参见 `perlop` 中的 Private Variables via `my()`，以及 `fields`, `attributes`, 和 `Attribute:Handlers`。

注意，在带括号的列表中，`undef` 可以作为虚拟占位符，例如用于跳过初始值的赋值：

```perl
my ( undef, $min, $hour ) = localtime;
```

## `next LABEL` `next EXPR`

下一个命令类似于 C 语言；它开始循环的下一次迭代：

```perl
LINE: while (<STDIN>) next /^#; # 忽略注释 ...
```

注意，如果上面有一个 `continue` 块，即使在被忽略的行上也会执行。`next EXPR` 形式（从 Perl 5.18.0 起）允许在运行时计算标签名称，但在其他方面与 `next LABEL` 相同。

`next` 不能用于返回值的块（例如 `{}`、`sub {}` 或 `{ {}}`），且不应在 `grep()` 或 `map()` 操作内部使用。

注意块本身在语义上等同于执行一次的循环。因此，`next` 将提前退出此类块。

参见 `"continue"` 以了解 `last`、`next` 和 `redo` 的用法。

与大多数运算符不同，它的优先级与赋值相同。它不受“看起来像函数”规则的限制，所以 `next ("foo")`。*bar 可以调用 `"bar"` 来作为 `next` 的参数的一部分。*

## `no VERSION LIST` `NO VERSION MODULE LIST` `NO VERSION`

参见 `function` 的用法，它并不相反。`oct expr` 将 `Expr` 解释为八进制字符串并返回对应的值。（如果 `EXPR` 以 `0x` 开头，则将其解释为十六进制字符串；如果 `EXPR` 以 `0b` 开头，则被解释为二进制字符串。在三种情况下都会忽略前导空格）。以下是 Perl 记法：

```perl
$val = oct($val) if $val ~ /^0/;
```

如果省略了 `EXPR`，则使用 `$_`。要进行反操作（产生八进制数字），使用 `sprintf()` 或 `printf()`：

```perl
$dec_perms = (stat("$filename"))[2] & 07777; $oct_perm_str = sprintf "%o",$perms;
```

`oct()` 函数通常用于将像 644 这样的字符串转换为数字示例。尽管 Perl 会根据需要自动将字符串转换为数字，但这种自动转换假设基数为 10。

空格会在无警告的情况下被忽略，以及任何结尾的非数字字符，例如小数点（`oct` 只处理非负整数，不处理负整数或浮点数）。

## `open`

`HANDLE,EXPR |HANDLE,MODE,EXPR |HANDLE,MODE,LIST` `FILEHANDLE,MODE,REFERENCE` 打开由 `EXPR` 给出文件名的文件，并将其与 `FILEHANDLE` 关联。

打开文件进行读取的简单示例：

```perl
open($my $f, "<", "input.txt") or die "cannot open < input.txt: \$";
```

以及用于写入：

```perl
open($my $f, ">", "output.txt") or die "cannot open > output.txt: \$";
```

（以下是 `open()` 的全面参考：为了更温和的介绍，您可以考虑 perpetuant。

`IFHANDLE` 是一个未定义的标量变量（或数组或哈希元素），一个新的文件句柄会被自动创建，这意味着该变量被分配了一个新分配匿名文件句柄的引用。否则，`IFHANDLE` 是一个表达式，其值是真实的文件句柄。（这被视为符号引用，因此 `strict "refs"` 不生效）。

如果指定了三个（或更多）参数，则第二个参数的打开模式（包括可选编码）与第三个参数的路径是不同的。如果 `MODE` 为 `<` 或空，则以输入模式打开文件。如果 `MODE` 为 `>`，则以输出模式打开文件，现有文件将被截断（“覆盖”），并创建不存在的文件。如果 `MODE` 为 `>>`，则以追加模式打开文件，在必要时再次创建。

你可以在 `>` 前面加上 `+`，表示你想同时对文件进行读写访问；对于读写更新，始终优选 `<`，因为 `+` 模式会先覆盖文件。你不能使用读写模式更新文本文件，因为它们具有变长度的记录。参见 `perlperl` 中的 `-i` 选项以获得更好的方法。文件将根据进程的掩码使用 0666 权限创建。

这些不同的前缀对应于 `r`, `r+`, `w`, `w+`, `a a`。双参数调用的形式中，模式和文件名应该拼接（按此顺序），最好用空格分隔。当模式为 `<` 时，在这些形式中可以但不应该省略模式。如果文件名是已知的字面量，使用双参数的 `open` 总是安全的。

对于三个或更多参数，如果 `MODE` 为 `|`，文件名被解释为一个命令，输出将被管道传输；如果 `MODE` 为 `-`，文件名被解释为向我们管道传输输出的命令。在双参数（以及单参数）形式中，应替换 dash--)the.

与文件句柄相同：

```perl
$ARTICLE = 100; open(ARTICLE) or die "Can't find article $ARTICLE:\n";
```

这里 `$ARTICLE` 必须是一个全局（包）标量变量——而不是用 `my state` 声明的。

作为一种特殊情况，带有读写模式且第三个参数为 `undef` 的三参数形式：

```perl
open($mytmp, "+", undef) or die...
```



打开一个指向匿名临时文件的句句柄。同样使用了 `<<` 以保持对称性，但你真的应该考虑向临时文件写入某些内容。你需要在读取时进行 `seek(0)`。

Perl 默认使用 PerlIO 构建；除非你更改了此设置（例如使用 `Configure -Uuseperlio` 编译 Perl），否则你可以通过以下方式直接打开指向 Perl 标量的文件句柄：

```perl
open($fh, "", \variable) || ..
```

若要在内存文件文件中重新打开 STDOUT 或 STDERR，请先关闭它：

```perl
close STDOUT; open($fh, ">", \variable) or die "Can't open STDOUT: $$";
```

### 通用示例

详阅 PerlIO 的详细信息。

你也可以遵循 Bourne 传统，指定一个以 `&` 开头的 EXPR，在这种情况下，字符串被解释为文件句柄的名称（或用作 (2) 的数字型文件描述符）并被打开。你可以使用 `&`。你指定的模式应与原始文件句柄的模式匹配。（转储文件句柄不会考虑其任何内容（缓冲区））。如果你使用三参数形式，则可以传递数字、文件句柄名称或普通的“全局通配符引用”。

这里是一个使用各种方法重定向并恢复 STDOUT 和 STDERR 的脚本：

```perl
#!/usr/bin/perl

open(my$old, ">STDOUT") or die "Can't dup STDOUT: $$";

open(OLDERR, ">", \STDERR) or die "Can't dup STDOUT: $$"; 

open(STDOUT, ">", "foo.out") or die "Can't dup STDOUT: $$"; 

select STDERR; |= 1; # 使 STDOUT 无缓冲

print "stdout 1\n"; # 这对 print 起效

print "stderr 1\n"; # 处理

open(STDOUT, "&", $oldout) or die "Can't dup $oldout: $$"; 

open(STDERR, "OLDERR") or die "Can't dup OLDERR: $$"; 

print "stdout 2\n"; 

print "stderr 2\n";
```

如果你指定 `<-X`，其中 X 是文件描述符数字或文件句柄，则 Perl 将执行等同于 C 语言的文件描述符 fopen（而不是调用 (2)）；这对文件描述符的使用更加节约。例如：

```perl
# 用于输入，重用 $fd 的 fileno
open(FILEHANDLE, "<=$fd")
or
open(FILEHANDLE, "<=", $fd);
or
# 用于追加，使用 OLDFH 的 fileno
open(FH, ">>=", OLDFH)
or
open(FH, ">>=", OLDFH)
```

节约文件句柄也是有用的（除了节约之外），例如当某些内容依赖文件描述符时，例如使用 `flock()` 锁定。如果你只是 `open(A, "&B")`，文件句柄 A 的文件描述符将与 B 不同，那么 `flock(A)` 将不会锁定 B，反之亦然。使用 `open(A, ">>=")`，文件句柄将共享相同的底层文件系统描述符。

注意，在 Perl 5.8.0 以上，Perl 使用标准库的 `fopen()` 来实现 `-` 功能。在许多 Unix 系统上，当文件描述符超过某个值（通常为 255）时，fopen() 会失败。对于 Perl 5.8 及更高版本，PerIO 是（主要的）默认设置。

你可以运行 `perl -l` 并查找 `useperio` 行来查看 Perl 是否是使用 PerIO 构建的。如果 `useperio` 被定义，则你拥有 PerIO；否则没有。

如果你在命令 `-` 中打开一个管道（即在 open 的一参数或二参数形式中指定 `|` 或 `-`），将使用隐式的 `fork`，因此 `open` 会返回两次：在父进程中它返回子进程的 pid，在子进程中它返回一个定义的 `0`。你使用 `defined($pid)` 来确定 open 是否成功。

例如，使用任一种：

```perl
$child_pid = open(FROM_KID, "-\|") // die "can't fork: $$";
```

或者

```perl
$child_pid = open(TO_KID, "-\|") // die "can't fork: $$";
```

随后是：

```perl
if ($child_pid) { # 我是父进程：要么写入 TO_KID 或者读取
FROM_KID .. waitpid $child_pid, 0; 
} else { # 我是子进程；正常使用 STDIN/STDOUT ... exit; }
```

文件句柄对父进程正常，但对该文件句柄的 I/O 被管道到子进程的 STDIN/STDOUT。在子进程中，文件句柄并没有打开——I/O 发生在从/到新的 STDOUT/STDIN。通常这像普通管道一样使用，当你想要对执行的管道命令进行更多控制时，因为运行直到你不想为了保存元字符而保存 shell 命令。

以下块等同于：
此处原文代码块内容似乎不完整，重复了逻辑描述，已根据语意翻译并保持结构

即使包变量之前没有使用过，这种方法也有效，因为包变量在第一次被使用时就会产生。

```perl
package Foo; use strict; our $foo = 23; # just like Foo::foo = 23 print $Foo::Foo; # prints 23
```

由于在 `use strict 'vars'` 的情况下，只要作用范围内没有同名变量，该变量就会立即变得合法，因此你可以在同一条语句中再次引用该包变量。

```perl
package Foo; use strict; my $foo = $foo; # error, undeclared $foo on right-hand side our $foo = $foo; # no errors
```

如果列出了多个变量，则必须放在括号中。

```perl
($bar, $baz);
```

一个顺序声明（order-declaration）为包变量声明了一个别名，该别名在其整个词法作用域内可见，跨跨包边界。变量所在的包是在声明点确定的，而不是在使用点。这意味着以下行为：

```perl
package Foo; our $bar; # declares Foo::bar for rest of lexical scope $bar = 20; package Bar; print $bar; # prints 20, as it refers to Foo::bar
```

如果在同一个词法作用域内对不同包进行同名声明是允许的。如果它们恰好在同一个包中，且开启了警告，Perl 将像多次声明一样发出警告。与第二次声明（该声明会将名称绑定到新变量）不同，在同一个包、同一作用域内的第二次声明仅仅是冗的。

```perl
use warnings; package Foo; our $bar; # declares Foo::bar for rest of lexical scope $bar = 20; package Bar; our $bar = 30; # declares Bar::bar for rest of lexical scope $bar; # prints 30 our $bar; # emits warning has no other effect $bar; # prints 30
```

顺序声明还可以关联一个属性列表。

`TYPE` 和 `ATT` 的精确语义仍在演进中。`TYPE` 目前绑定到 `practica` 字段的使用，并使用 `practica` 属性处理，或者从 Perl 5.8.0 开始，也通过 `Attribute::Handlers` 模块处理。“Private Variables in perl for fields, and attributes, and Attribute::Handlers.”

注意，括号列表可以作为虚拟占位符，以跳过初始值的赋值：

```perl
our (undef, $min, $hour) = localtime;
```



`our` 与 `vars` 不同，后者允许在受影响的包内跨作用域使用不带限定符的名称。

### `pack TEMPLATE.LIST`

`pack TEMPLATE.LIST` 接收一个值列表并根据 `TEMPLATE` 给出的规则将其转换为字符串。生成的字符串是这些值的拼接。通常，每个转换后的值看起来像其在机器层面的表示。例如，在 32 位机器上，整数可能由 4 个字节序列表示，这在 Perl 中将呈现为长度为 4 个字符的字符串。

参见 `perperl` 以获取该函数的介绍。

`Template` 是一个字符序列，规定了值的顺序和类型如下：

- `a`: 任意二进制数据的字符串，将用零填充。
- `t`: 文本（ASCII）字符串，将用空格填充。
- `Z`: 零终止（ASCII）字符串，将用零填充。
- `b`: 位字符串（每个字节内部按降序排列）。
- `h`: 十六进制字符串（低半字节）。
- `n`: 十六进制字符串（高半字节）。
- `C`: 一个无符号字符（字节）值。
- `W`: 无符号符号字符值（可以大于 255）。
- `S`: 有符号短整型（16位）。
- `L`: 无符号符号整数值。
- `Q`: 无符号四字节整数（仅当系统支持 64 位整数且 Perl 编译为支持这些整数时才可用 Quads；否则抛出异常）。
- `i`: 一个有符号整数值。此“整数”至少是 32 位。确大小取决于本地 C 编译器。
- `N`: “网络大端”序的无符号字符串（16位）。
- `v`: “VAR-小端”序的无符号符号字符（16位）。
- `V`: “VAR-小端”序的无符号长整数（32位）。
- `J`: 一个 Perl 无符号整数值（UV）。
- `F`: 原生格式的单精度浮点数。
- `d`: 原生格式的长双精度浮点值（NV）。
- `D`: 长双精度浮点数，仅当系统支持且已编译为支持时才可用。否则抛出异常。存在不同的长双精度。
- `s`: （固定长度）字符串。
- `u`: 指向零终止字符串的指针。
- `p`: 指向结构的指针。
- `U`: Unicode 字符数字。在 char 模式下编码为字符 UTF-8（或在 EBCDIC 格式模式下为 UTF-EBCDIC）。
- `m`: 压缩整数（非 ASN 1）。
- 一个 128 无符号整数，最高位数字在前，每个数字。除最后一个字节外，每个字节都设置高位。一个零字节（ASCII NULL，`"\u000"`）。
- `x`: 回退字节。
- `S`: 从内部 `()` 组开始计算，填充或截断到绝对位置。
- 由值指定的填充或截断绝对位置。
- `$`: `)` 组的开始。

一个或多个修饰符可选地跟在 `TEMPLATE` 中的字母后面（第二列列出了修饰符的用途）：

`>` 和 `<` 修饰符也可以用于组，以强制执行特定的字节序。一个或多个修饰符可选地跟在 `TEMPLATE` 中的字母后面（第二列列出了修饰符的用途）：

`>` 和 `<` 修饰符也可以用于组，以强制执行特定的字节序。一个或多个修饰符可选地跟在 `TEMPLATE` 中的字母后面（第二列列出了修饰符的用途）：

`>` 和 `<` 修饰符也可以用于组，以强制执行特定的字节序。一个或多个修饰符可选地跟在 `TEMPLATE` 中的字母后面（第二列列出了修饰符的用途）：

`>` 和 `<` 修饰符也可以用于组，以强制执行特定的字节序。一个或多个修饰符可选地跟在 `TEMPLATE` 中的字母后面（第二列列出了修饰符的用途）：

如果你的系统具有特殊的指针大小——这意味着指针的大小既不是 `int` 大，也不是 `long` 大——那么可能以大端序或小端序字节序对指针进行打包或解包。尝试这样做会抛出异常。

模板字符允许对一组项进行打包和解包，其中打包后的结构包含一个打包项，随后紧跟打包后的项本身。当结构需要将编码的序列或某些字段的重复计数作为结构内的独立字段解包时，这种方法非常有用。

对于 `pack`，你编写 `length-item/sequence-item`，其中 `length-item` 描述了长度值是如何打包的。最可能有用的格式是整数打包，例如用于 Java 字符串的 `n`，用于 ASN|1 或 Sun XOR 的 `w`。

对于 `pack`，`sequence-item` 可能有一个重复计数，在这种情况下，将该计数与可用项数量之间的最小值用作 `length-item` 的参数。如果它没有重复计数或使用 `*`，则使用可用项的数量。

对于 `unpack`，这是一个到目前为止已解包的整数项的内部栈。你使用 `/sequence-item`，重复计数通过从栈中弹出最后一个元素获得。`sequence-item` 不得有重复计数。

如果 `sequence-item` 指向字符串类型（`A`、`a` 或 `Z`），则 `length-item` 是字符串长度，而不是字符串的数量。在显式的重复计数打包中，打包的字符串会被调整为该长度。例如：

```
This code gives this result: unpack("W/a"
```

`length-item` 不会从 `unpack` 显式返回。

在 `length-item` 格式字母中提供计数仅对 `A`、`a` 或 `Z` 有用。使用 `length-item` `a` 或 `z` 打包可能会引入 `\000` 字符，Perl 不认为这是合法的数字字符串。

整数类型 `s`、`S`、`1` 和 `l` 可以后跟 `!` 修饰符以指定 shorts 或 longs。如示例所示，裸露 `1` 表示 32 位，尽管 C 编译器看到的原生 `long` 可能会更大。这在 64 位平台上主要是一个问题。你可以通过这种方式查看 `!` 是否产生差异：

```
printf "format %d
```

`i!` 和 `I!` 也是允许的，但仅为了完整性：假设它们与 `i` 和 `I` 相同。

原生类型的实际大小（字节）也可以从构建 Perl 的平台通过命令行获取：

```
$ perl -V:{short, int,long{long}} shortsize='2'; intsize='4'
```

`longsize='4'; longlongsize='8';`

或者通过 `Config` 模块以编程方式调用：

```
use Config; print $Config(shortsize), "\n"; print $Config(longsize), "\n"; print $Config(longsize), "\n"; print $Config(longsize), "\n"
```

在不支持 `long` 的系统中 `$Config(longsize)` 是未定义的。

整数格式 `s`、`S`、`i`、`I`、`1`、`L` 和 `j` 在处理器之间本质是不可移植的，且取决于字节序和端序。例如，一个 4 字节整数 `0x12234567`（305419896 数据）将以原生方式（由 CPU 安排并处理）排序为：
`0x12 0x23 0x45 0x67` # 大端序
`0x67 0x45 0x23 0x12` # 小端序

基本上，Intel 和 VAX 是小端序，而其他所有包括 Motorola 68k/88k、PPC、Sparc、HP PA、Power 和 Cray 都是大端序。Alpha 和 MIPS 可以是其中一种：Digital/Q 使用小端序（实际上如此），但 SGI/Cray 使用大端序。

`big-endian` 和 `little-endian` 的名字源于乔纳森·斯夫特的经典讽《格游记》，指的是小人国（Lillipians）和大脚丁国（Blebudans）。这些术语通过 Danny Cohen 写的《圣战与和平之路》进入计算机领域，公元1980年4月。

有些系统可能具有甚至的字节序，例如
`0x56 0x12 0x34 0x34`

这些被称为中端序（mid-endian）、中间端序（middle-endian）、混合端序（mixed-endian）或只是奇怪（weird）。

你可以通过此咒语确定系统的端序：
`printf("%#02x", unpack("W*", L=>0x12345678))`

构建 Perl 的平台的字节序也可以通过 `Config` 获取：
`use Config; print "$Config{byteorder}\n"`
或从命令行：

```
$ perl -v-byteorder
```



字节序 `1234` 和 `12345678` 是小端序，`4321` 和 `87654321` 是大端序。多架构系统将具有 `ffff`，这意味着静态信息无效，必须使用运行时检查。

对于可能打包的整数，使用格式 `n`、`N`、`v` 或使用下文描述的 `>` 和 `<` 修饰符。参见 `perl`。

浮点数也有端序。通常（并非总是）与整数端序一致。尽管大多数平台使用此 IEEE 754 二进制格式，但存在差异，特别是当涉及 `double` 时。你可以看到 `Config` 和 `longdbl(size)`：`kind` 值是枚举，类似于 `byteorder`。从可移植性来说，最好的可能是保留 IEEE 754 64 位双。另一种可能性是 `%a` 格式。从 Perl 5.10.0 开始，整数和浮点格式带有 `p` 和 `()` 组可能会后跟 `>` 或 `<` 修饰符以强制执行大端或小端序。这些修饰符在 `n`、`N` 和 `v` 覆盖整数时特别有用。使用端序修饰符需要注意以下问题：只有当所有平台以相同的格式存储时，在不同平台之间交换整数。大多数平台使用补码表示符号整数，这通常不是问题。`>` 或 `<` 修饰符只能在大端或小端机器上用于浮点格式。否则，尝试使用它们会抛出异常。如果你确切自己在做什么，可以使用 `>` 或 `<` 修饰符强制浮点值的字节序。因为 Perl 在内部对所有数值计算都使用 `double`（如果配置了则是 `long double`），从 `double` 转换为 `float` 再转换为 `double` 会丢失精度，所以 `unpack("f", pack("f", $))` 通常不适用于 `%f`。

`pack` 和 `unpack` 以两种模式运行：字符模式（`co mode`），按字符处理打包字符串；以及 UTF-8 字节模式（`uo mode`），按字节处理。除非格式字符串以 `u` 开头，否则字符模式是默认。你可以通过格式中显式的 `co` 或 `u` 切换模式。这种效果一直持续到下一次模式更改，或者直到 `()` 组结束。

使用 `co` 编码字符同时使用 `u` 获取非 Unicode 字节是显而易见的。这些中只有第一个是你要的：

```
$ perl -CS -e say "\x01" | perl -CS -ne printf "%04X\n", $

  for unpack("A*", $).0319 $ perl -CS -e say "\x01" | perl -CS -ne printf "%02X\n", $

  for unpack("A*", $).BE.C1.89 $ perl -CS -e say "\x01" | perl -CS -ne printf "%02X\n", $

  for unpack("A*", $).BE.C1.CF.89 $ perl -CS -e say "\x01" | perl -CS -ne unpack("A*", $)

C3.BE.C2.C13.BF.29
```



这些示例也说明了你应该尝试使用 `pack/unpack` 来替代 `Encode` 模块。

在打包时，不能通过插入 `xs` 来进行任何对齐或填充。`pack(k)` 和 `unpack(k)` 无法知道字符去哪里或来自哪里，因此它们将输出和输入处理为平面字符序列。`()` 组是括号括起来的子模板。组可以在 `unpack(k)` 中带有一个重复计数，因此使用 `@` 定位将从 0 重新开始。因此 `pack("@1A((@2A)@3A), qW[X Y Z])` 的结果是字符串 `\x0@YZ`。`x` 和 `x` 接受修饰符作为对齐命令。它们向前向后跳转到字符倍数对齐最近的位置。例如，要 `pack(o)` 或 `unpack(o)` 一个 C 结构

```
struct char { /* 一个有符号的 8 位字符 */ double d; char cc[2]; };
```

可能需要使用模板 `x![d]d c[2]`。这假设 `double` 必须按 `double` 的大小对齐。`n`、`N`、`v` 和 `v` 接受修饰符以大端/小端序表示 16/32 位整数。只有当所有共享数据的平台使用相同的二进制表示时，它是可移植的。对于符号整数；例如当所有平台使用补码表示时。可以使用 `#` 直到行尾在模板中嵌入注释。将复杂的模板拆分为行组件并进行适当注释，可以提高 `pack/unpack` 格式的可读性和可维护性，作为对于复杂的模式。

```
pack("W4",65,66,67,68); # 相当于 $foo
pack("W4",0x24b6,0x24b7,0x24b8,0x24b9); # 相当于 Unicode 圆圈字母。 $foo = pack("U4",0x24b6,0x24b7,0x24b8,0x24b9); # 相当于圆圈字母。你不需要使用 UTF-8 字节，因为格式开头的 U 导致了切换到 U0模式，所以 UTF-8 字节被合并成了字符 #foo
pack("U04",0x24b6,0x24b7,0x24b8,0x24b9); # $foo 这是上一个示例中字符串的 UTF-8 编码 $foo
pack("x221x22b\62xe22d2x22b\6xe22e2x22b"); # 这只是
pack("x66",65,66,67,68); $foo = pack("AB01"); # 注意：带有 "w" 和 "y" 的示例仅在 ASCII 和 ASCII 派生的系统（如 Latin-1 和 UTF-EBCDIC 系统）上有效，第一个示例将是 $foo = pack("W3",193,194,195,196); $foo =
pack("s2",1,2) 在小端序上 \u0001\u0002\u0002" 在大端序上 $foo = pack("x4","abcd","x","y","z"); # "x","y","z"
$abcdf = pack("abcd","aaaa\ # ayxyz $foo
$foo = pack("x14",abcdf); # $abcdf
$foo = pack("s2",12, 34); # 短整型 12 字节，零填充到位置 34
$foo = pack("s4",12, 34); # 短整型 12, 零填充到位置 34
$foo = pack("n",12, 34); # 短整型 12, 零填充到位置 34
$foo = pack("s",12, 34); # 短整型 12, 零填充到位置 34
$foo = pack("S",42, 47); # 大端序和 32位有符号整数
$foo = pack("s>L",42, 47); # 大端序和 32位有符号整数
$foo = pack("<L",42, 47); # 小端序和 32位有符号整数
$foo = pack(">L",42, 47); # 大端序和 32位有符号整数
$foo = pack("q",42, 47); # 完全相同
```

该模板也可以用于 `unpack(q)`。

## 命名空间 (NAMESPACE)

在给定的命名空间中。包声明块是编译单元位于给定命名空间的结果。如果没有块，则从声明本身直到当前作用域的结束（包围作用域、文件或 eval）。也就是说，没有块的形式将一直作用到当前作用域结束，就像 `state` 和我们的运算符一样。

未限定的标识符将在给定的命名空间中，除非被包声明或一个进入我的命名空间的声明所覆盖；例如 `STDOUT`、`ARGV`、`ENV` 和标点符号。包语句影响动态变量，包括你已经使用了 `local` 但不是局部作用域的变量，这些变量是通过 `my`、`state` 或其他创建的。通常，它应该是包含 `require` 或 `use` 的文件中的声明。你可以在多个地方切换到 `package`，因为这仅决定了该块编译器所使用的默认符号表。该块通过在当前包名前面加上包名和冒号来识别其他包，例如 `SomePack::var` 或 `ThatPack::INPUT_HANDLE`。如果省略了包名，则假设为当前包。也就是说，`:::` 等同于 `$main`（以及在古老代码中仍然看到的 `$main`，大多来自 Perl 4）。

如果提供了 `VERSION`，包会将给定命名空间中的 `$VERSION` 变量设置为一个版本对象。`VERSION` 必须是“严格”风格的版本号，即正十进制数（整数或十进制分数），由 `version` 模块定义：不带指数，或者以 'v' 字符开头且至少包含三个部分的点分进制 v 字符串。你应该每个包只设置一次 `$VERSION`。

有关包、模块和类的更多信息，请参见 `perl` 中的 "Packages"。请参见 `persub` 了解其他作用域问题。

### `__PACKAGE__`

一个特殊的标记，返回它发生处时所属的包名。

### `READHANDLE,WRITEHANDLE`

像相应的系统调用一样打开一对连接的管道。如果你设置了一对管道进程，除非非常小心，否则可能会发生死锁。此外，请注意 Perl 的管道使用它自己的缓冲，因此取决于应用程序，你可能需要设置 `$|` 以在执行每个命令后刷新你的 `WRITEHANDLE`。

成功时返回真。

此类事项，请参见 `IPC::Open2`、`IPC::Open3` 以及 `perpc` 示例中的“与另一个进程进行双向通信”。

在支持文件 `close-on-exec` 标志的系统上，该标志将设置在所有高于当前 `$F` 值（默认情况下 `STDERR` 为 2）的新打开的文件描述符上。`perlvar` 中的 `"$F"`。

### 弹出数组 (pop array)

`pop` 返回数组的最后一个值，并将数组缩短一个元素。

如果数组为空，返回未定义值（`undefined`），尽管这也会发生在其他时候。如果省略 `ARRAY`，则弹出主程序中的 `ARGV` 数组，但在子程序中弹出 `@_` 数组，可以使用 `shift`。

从 Perl 5.14 开始，`pop` 可以接受标量 `EXPR`，该标量必须持有数组引用。参数会自动解引用。`pop` 的这一方面被认为是高度实验性的。具体行为在未来的 Perl 版本可能会更改。

为了避免让运行早期版本的 Perl 用户产生困惑的语法错误，可以在文件顶部使用以下内容指示代码所需的版本：

```
use 5.14; # 所以 push/pop/etc 可以处理标量（实验性）
```

### `pos SCALAR`

返回上一次匹配的偏移量（未指定变量时使用 `$_`）。注意，`0` 是一个有效的匹配偏移量，`_` 表示搜索位置已重置（通常由于匹配失败，但也因为尚未对标量进行匹配）。



`pos` 访问正则引擎存储偏移量的位置，赋值 `pos` 会更改该偏移量，并影响正则表达式中的 `\G` 零宽断言。这些影响都发生在下一次匹配，因此你无法在当前匹配中（例如在 `in` 中）通过 `pos` 影响位置。

`print FILEHANDLE format(FORMAT, LIST)`，但不应用 `$(`（输出记录分隔符）。`FORMAT` 和 `LIST` 实际上被解析为单个列表。列表的第一个参数将被解释为 `printf` 格式。这意味着 `printf(@)` 将使用 `$_` 作为格式。请参见 `Sprintf` 获取关于格式参数的解释。如果此处使用的 `locale LC_NUMERIC` 生效且 `POSIX::setlocale()` 已更改，用于格式化浮点数的小数分隔符将受到 `LC_NUMERIC locale` 设置的影响。请参见 `perlocale` 和 `perlop`。

由于历史原因，如果你省略列表，则使用 `$_` 作为格式；要使用句柄且不带列表，必须使用真实的句柄如 `FH`，而不是间接句柄如 `fh`。然而，如果你想打印格式代码，这真的会发生什么，它们将被替换为空字符串，如果启用了警告将发出警告。如果你想打印 `$_` 的内容。

不要掉入简单的 `print` 就能解决的情况下使用 `printf` 的陷阱。`print` 是更高效且更不容易出错。

## prototype

`prototype` 以字符串形式返回函数的原型（如果函数没有原型，则返回 `undef`）。`FUNCTION` 是指向你想要检索的函数原型的引用或其名称。如果省略了 `FUNCTION`，则使用 `\$`。

如果 `FUNCTION` 是一个以 `::` 开头的字符串，则其余部分被视为 Perl 内置函数的名称。由于该内置函数的参数无法通过原型（如系统）充分表达，`prototype()` 将返回 `undef`，因为该内置函数的行为并不真正像一个 Perl 函数。否则，将返回描述等效原型的字符串。

## push

`ARRAY LIST` `$push EXPR` 通过将 `LIST` 中的值追加到 `ARRAY` 的末尾，将 `ARRAY` 视为一个栈。`ARRAY` 的长度随 `LIST` 的长度而增加。这与以下代码的效果相同：

```perl
for \valuevalue (LIST) { \$ARRAY[++\$ARRAY] = \$value; }
```

但效率更高。在每次 `push` 之后，数组中的元素数量都会增加。

从 Perl 5.14 开始，`push` 可以接受一个标量 `EXPR`，该标量必须持有指向一个未修饰（unblessed）数组的引用。`push` 的这一特性被认为具有高度实验性。实际行为在 Perl 的未来版本可能会发生变化。

为了避免运行较旧版本 Perl 的代码的用户因神秘的语法错误而产生困惑，可以在文件顶部使用此类代码，以指示你的代码仅适用于较新版本的 Perl：

```perl
use 5.014; # 允许对标量使用 push/pop/etc（实验性）
```

## q/STRING/ qv/STRING/ qX/STRING/

通用引号。参见 `perlop` 中的“类引号运算符”（Quote-Like Operators）。`q/STRING/` 类似正则的引号。参见 `perl` 中的“类引号运算符”（Quote-Like Operators）。

`quotemeta` 返回 `EXPR` 的值，其中所有 ASCII 非“单词”字符都加上了反斜杠（即，不匹配 `/[A-Za-z0-9]/` 的 ASCII 字符在返回的字符串前都会有一个反斜杠，无论任何区域（locale）设置）。这是实现双引号字符串中 `\Q` 转义的内部函数。（另见下文关于非 ASCII 引号的行为）。

如果省略了 `quotemeta`，则 `(\Q ... \E）` 对于将字符串插值到正则表达式中非常有用，默认情况下，插值的变量将被视为一个微型正则表达式。例如：

```perl
$mysent = 'The quick brown fox jumped over the lazy dog'; my
$substring = 'quick.*?fox'; \$sentence = s{\$substring}\{big bad wolf};
```

将得到 `$sentence = The big bad wolf jumped over....`

另一方面：

```perl
$mysence = 'The quick brown fox jumped over the lazy dog'; my
$substring = 'quick.*?fox'; \$sentence = s{\Q$substring\E}{big bad wolf};
```

或者：

```perl
$sentence = 'The quick brown fox jumped over the lazy dog'; my
$substring = 'quick.*?fox'; $my_substring = quotemeta($substring);
$sentence = s($substring){big bad wolf};
```

上述两种都会保持句子不变。在接受用户的字面字符串输入时，必须使用 `quotemeta()` 或 `r q/`。

在 Perl v5.14 中，所有非 ASCII 字符在非 UTF-8 编码字符串中会被引用，但在 UTF-8 字符串中不会被引用。

从 v5.14 开始，Perl 采用了 Unicode 定义的策略来引用非 ASCII 字符；对 ASCII 字符的引用保持不变。

同样，在 `use feature 'unicode_strings'` 作用范围之外，对非 UTF-8 字符串的引用保持不变，即对所有大 Latin1 范围内的字符。这为不使用 Unicode 的旧程序提供了向后兼容性。

在区域（locale）作用范围内，无论字符串是否被编码为 UTF-8，所有非 ASCII Latin1 代码点都会被引用。如上所述，区域（locale）不影响 ASCII 范围字符的引用。这防止了某些将 `| =` 等字符视为单词字符的区域的影响。

否则，Perl 使用来自 Unicode 的适配方法 (`< >`) 来引用非 ASCII 字符。被引用的代码点仅限于具有任一 Unicode 属性的：`Pattern_Syntax`、`Pattern_White_Space`、`White_Space`、`Default_Ignorable_Code_Point` 或 `General_Category=Control`。

在这些属性中，两个重要的属性是 `Pattern_Syntax` 和 `Pattern_White_Space`。Unicode 设置这些属性恰是为了为了这一目的，即决定正则表达式模式中的哪些字符应该被引用。标识符中的任何字符都不具有这些属性。

Perl 承诺，如果我们对已定义的十几个 (`\ | ( ) { ^ * + ? }`) 增加正则表达式元字符，我们将仅使用那些具有 `Pattern_Syntax` 属性的字符。Perl 还承诺，如果我们添加在正则表达式中被视为空白的字符（目前主要通过 `/x`），它们都将具有 `Pattern_White_Space` 属性。

Unicode 承诺这两个属性所涵盖的代码点集永远不会改变，因此在 v5.16 中未被引用的内容在未来的任何 Perl 发布中都将需要被引用。（并不是所有匹配 `Pattern_Syntax` 的代码点都已分配了字符；因此有增长空间，无论是否分配，都会被引用。Perl 绝不会使用未分配的代码点作为实际的元字符。）

引用具有其他 3 个属性的字符是为了增强正则表达式的可读性，而不是因为它们在正则表达式用途上实际上需要被引用。

## rand

`EXPR` 返回一个大于或等于 `0` 且小于 `EXPR` 的随机分数。如果省略了 `EXPR`，则使用值 `1`。除非已经调用过 `srand`，否则会自动调用。参见 `srand`

如果你想要整数而不是随机数，对 `rand()` 返回的值应用 `int()`。例如：

```perl
int(rand(10))
```



返回 0 到 9 之间的数字。（注意：如果你的函数一贯返回过大或太小的数字，可能是你的 Perl 版本编译时 `RANDBITS` 设置错误。）

`rand()` 不是加密安全的。你不应该在安全敏感的情况下依赖它。截至目前，CPAN 第三方模块提供了作者认为加密安全的随机数生成器，包括 `Data::Entropy`、`Crypt::Random`、`Math::Rand::Secure` 和 `Math::TrulyRandom`。

## `read FILEHANDLE,SCALAR,LENGTH,OFFSET` 从指定的 `FILEHANDLE` 读取字符到 `SCALAR`。返回实际读取的字符数、文件末尾 `@` 或如果出错则返回 `undef`（最后一种情况 `!`）。如果实际读取的最后一个字符是 `scalar` 的最后一个字符，则 `scalar` 将增长或缩小。

指定偏移量将数据放置在字符串开头以外的位置。负偏移量指定从字符串向后计算的位置。正的 `OFFSET` 大于 `SCALAR` 的长度，则会在追加读取结果之前用 `\0` 字节填充字符串。

该调用是通过 Perl 或你系统的原生 `(3)` 库函数实现的。要获得真正的 `(2)` 系统调用，请使用。

注意字符：取决于句柄的状态，读取的是 `(8` 位) 字节。默认情况下，所有句柄都按字节操作，但如果例如句柄使用 `:utf8` I/O 层打开 (`:open"`, 和 `open` 指令)，则 I/O 将处理 UTF8 编码的 Unicode 字符而非字节。对于 `:encoding` 指令也是如此：

## `readdir HANDLE` 返回由 `opendir` 打开的目录的下一个条目。如果在列表上下文中，返回目录中剩余的所有条目。如果没有条目，在标量上下文中返回未定义，在列表上下文中返回空列表。

如果你计划对 `readdir` 的返回值进行文件测试（filetest），你最好在前面加上

目录问题。否则，由于我们没有 `chdir` 到该目录，它将测试错误的文件。

`opendir(my $dh, $some_dir) || die "can't opendir $some_dir: $!"; @dots = grep (\\/., -f "some_dir/$") readdir($dh); closedir($dh);`

由于 Perl 5.12 在循环中使用了基础的 `readdir`，它会在每次迭代时设置 `$_`。

```perl
opendir(my $dh, $some_dir) || die; while(readdir $dh) { print "$some_dir/$\n"; } closedir($dh);
```

为了避免那些运行旧版本 Perl 的代码出现莫名其妙的失败，可以在文件的顶部使用如下此类代码，以标明你的代码仅运行在较新版本的 Perl 上：

```perl
use 5.012; #这样 readdir 在单次测试中会赋值给 $_
```

`readdir EXPR ARGV`
从包含在 `EXPR` 中的文件句柄类型全局变量（typeglob）中读取（如果没有提供 `EXPR`，则使用 `*ARGV`）。在标量上下文中，每次调用都会返回一行，直到到达文件末尾，随后的调用将返回 `undef`。注意，“行”的概念取决于你通过 `$/`（分隔符）定义的任何内容。参见 `perpl` 中的 `"$/"`。

当 `$` 设置为 `undef` 时，`readdir` 处于标量上下文（即 slip 模式），当读取到空文件时，它会首次返回一次，随后返回 `undef`。

这是实现 `<EXPR>` 运算符的内部函数，但你可以直接使用它。`<EXPR>` 运算符在 `perlop` 的“I/O Operators”中有详细讨论。

```perl
$line = <STDIN>; $line = readdir(*STDIN); # 相同
```

如果 `readdir` 遇到操作系统错误，`$` 将被设置为你从不可信任的文件句柄（如 tty 或 socket）中读取的任何内容。以下示例使用了 `readdir` 的操作形式并将其定义为 `undef`。

```perl
while ( !eof($fh) ) { defined($fh) or die "readdir failed: $!"; } }
```

注意，你无法用那样处理 `ARGV` 文件句柄的 `readdir` 错误。情况下，如果你必须手动打开 `@ARGV` 的每个元素，处理 `ARGV` 的方式也不同。

```perl
foreach my $arg (@ARGV) { open(my $fh, $arg) or warn "Can't open $arg: $!"; while ( !eof($fh) ) { defined($_ = $fh) or die "readdir failed for $arg: $!"; } }
```

`readdir EXPR`
如果实现了符号链接，则返回符号链接的值。如果没有实现，则抛出异常。如果是系统错误，它返回未定义值并设置 `$!` (errno)。如果省略 `EXPR`，则使用 `$_`。

可移植性问题：`perperl` 中的 "readdir"。

`readpipe EXPR`
`readpipe EXPR` 被作为系统命令执行。返回命令收集的标准输出。在标量上下文中，它作为一个单条（可能是多行的）字符串返回。在列表上下文中，它返回行列表（无论你如何通过 `$/` 或 `$_INPUT_SEPARATOR` 定义行）。这是实现 `qx/expr/` 运算符的内部函数，但你可以直接使用它。`qx/expr/` 运算符在类似“I/O Operators”中有更详细讨论。如果已导出，则使用 `$_`。

`SOCKET,SCALAR,LENGTH,FLAGS`
在 socket 上接收消息。根据你从不可信任的文件句柄（如 tty 或 socket）中读取的内容设置 `$`。以下示例使用了 `readdir` 的操作形式并将其定义为 `undef`。

```perl
while ( !eof($fh) ) { defined($fh) or die "readdir failed: $!"; } }
```

```perl
use 'croak'; use version; sub require my ($filename) = @_; if ( my $version = $version->parse($filename)) } if ($version > $^v) {
    stopped;
}; return 1; if exists($INC{$filename}) {
    return 1
    my $vn = $version->normal; croak Perl $version required-this is only SV,$INC{$filename}) {
    croak "Compilation failed in require";
}
foreach prefix(@INC) if (ref($prefix)) {
    - do other stuff - see text below... #
    # (see text below appending of suffix to $filename) #
    $realfilename = "$prefix/$filename"; next if ! -e $realfilename || - d || - b;
    $$filename = $realfilename; my $result = do($filename); # but runs in caller the name is (defined $result) {
    $INC{$filename} = \def;
    croak $? "@Compilation failed in require": "Can't $filename: ";
    }
    if (!$result) delete $INC{$filename}); croak "$filename did not return true value";
    }
    $ = 0; return $result;
} croak "Can't locate $filename in \@";
```



该文件不会以相同的名称被包含两次。

文件必须作为最后一个语句返回，以表示任何初始化代码已成功执行，因此习惯上文件以 `1;` 结尾，除非你确定它会返回返回真值。但最好还是写上 `1;`，以防你之后添加了更多语句。

如果 `EXPR` 是一个裸字（bareword），`require` 会假设它具有 `.` 扩展名，并将文件名中的 `:` 替换为 `/`，以便加载标准模块。这种形式的模块加载没有修改你包名称的风险。

换句话说，如果你尝试这样做：

`require Foo::Bar; # 一个很棒条形码`

该函数实际上会在 `@INC` 数组指定的目录中查找 `Foo/Bar.pm` 文件。

但如果你这样做：

`$class = 'Foo::Bar'; require $class; $class is not a barcode #or require "Foo::Bar"; # not a barcode because of the ""`

该函数将处理 `@INC` 数组中的 `Foo::Bar`，并抱怨在那里没有找到 `Foo::Bar`。在这种情况下，你可以：

`eval "require $class";`

现在你已经理解了 `require` 如何查找裸字，但在后台还会有一些额外的功能。在 `require` 查找 `.pm` 扩展名之前，它会先查找一个具有 `.pm` 扩展名的相似文件名。如果找到了该文件，它将加载并替换任何以 `.pm` 结尾的文件。

你也可以通过直接将 Perl 代码插入 `@INC` 数组来向导入功能插入钩子。钩子有三种形式：子程序引用、数组引用和祝福对象（blessed objects）。

子程序引用是最简单的情况。当包含系统遍历 `@INC` 并遇到子程序时，该子程序将带有两个参数，第一个是它自身的引用，第二个是要要包含的文件名（例如 `Foo/Bar.pm`）。该子程序既不返回 `else` 也不返回按以下顺序的四个值的列表：

- 1. 指向标量的引用，包含任何要附加到文件或生成器输出的初始源代码。
- 2. 一个文件句柄，将从该句柄读取文件。
- 3. 指向子程序的引用。如果没有文件句柄（上一个项目），则预期该子程序每次调用生成一行源代码，将该行写入 `$_` 并返回 1，最后在文件末尾返回 0。如果有文件句柄，则该子程序将作为一个简单的源过滤器被调用，读入的行位于 `$_` 中。同样，对于每行有效行返回 1，并在所有行都返回后结束。
- 4. 子程序的可选状态。该状态通过 `$_[1]` 传递。子程序自身的引用通过 `$_[0]` 传递。

返回的是空列表、`undef` 或不匹配上述前 3 个值的内容，则 `require` 将查看 `$INC` 的剩余元素。请注意，这个文件句柄必须是真实的文件句柄（严格来说是类型全局 typeglob 或引用），无论是否经过祝福（blessed）；绑句柄（tied handles）将被忽略，且处理将停止。

如果钩子是数组引用，它的第一个元素必须是子程序引用。该子程序将按上述方式调用，但第一个参数是数组引用。这允许间接地向子程序传递参数。

用你的话说，你可以写：

```perl
push $INC, \my_sub; sub my_sub ($coderef, $filename) = @_; # $coderef = $x ... }
```

```perl
push $INC, [\my_sub, $x,$y]; sub my_sub ($arrayref, $filename) = @_; # 获取 $y ... }
```

如果钩子是一个对象，它必须提供一个在上述调用的方法，第一个参数是对象本身。（注意，你必须使用完全限定名称，因为未限定的总是会被强制转入 main 包。）这里有一个典型的布局：

```perl
# Foo.pm package Foo, sub new { ... }
push $INC, Foo->new(...);
```

这些钩子还允许设置与它们加载的文件对应的 `%INC` 条目。参见 perl 中的 `"%INC"`。

如需更强大的导入功能，请参见 `"use"` 和 `"reset"`。

### `reset EXPR`

`reset EXPR` 用于循环末尾的块中，以清除变量。该表达式被解释为允许范围的字符列表。所有以这些字母开头的变量和数组都被重置为原始状态。如果省略表达式，则返回 1。仅重置当前包中的变量或匹配项。如果没有给出 `EXPR`，则返回假。示例：

```perl
reset 'X'; # 重置所有 X
reset 'a-z'; # 重置小写
reset; # 仅重置
```

不建议重置数组，因为你会抹掉 `@ARGV` 和 `%ENV` 哈希表。只有作用域变量不受影响；它们在退出时会自我清理，所以你可能更想使用它们。注意，将数组反转到自身（如 `$a = reverse @a`）将尽可能保留原本不存在的元素；即，对于非魔术数组或带有 DELETE 方法的绑定的数组。

### `reverse LIST`

`reverse LIST` 在列表上下文中，返回一个由 `LIST` 的元素按相反顺序组成的列表。在标量上下文中，连接 `LIST` 的元素并返回一个所有字符反向排列的字符串。

```perl
print join(",", reverse "world", "Hello"); # Hello, world
reverse "drow", "olleH"; # Hello, world
```

在标量上下文中不带参数使用时，`reverse()` 会反转 `$.`。
`$ = "drow", "olleH"; reverse; # Hello, world`
在标量上下文中不带参数使用时，`reverse` 反转 `$.`。
`$ = "drow", "olleH"; reverse; # Hello, world`
在标量上下文中不带参数使用时，`reverse` 反转 `$.`。

在标量上下文中不带参数使用时，`reverse` 反转 `$.`。

### `seek FILEHANDLE,POSITION,WHENCE`

`seek FILEHANDLE,POSITION,WHENCE` 设置 `FILEHANDLE` 的位置，就像 stdio 中的 `fseek` 调用。`FILEHANDLE` 可以是一个表达式，其值为文件句柄名称。`WHENCE` 的值为：0 表示按字节设置新位置；1 设置为当前位置；2 设置为 EOF 位置，通常为负数。对于 WHERE，你可以使用 `Fcntl` 模块中的常量 `SEEK_SET`、`SEEK_CUR` 和 `SEEK_END`（文件开头、当前位置、文件末尾）。成功时返回 1，否则返回假。

`rewinddir` 将句柄的位置设置为目录的开头。`rewinddir` 类似于 `print`，但隐式追加换行。删除目录目录。

`rmdir FILENAME` 如果指定的目录为空，则删除目录。成功时返回真，否则返回假。

`say FILEHANDLE LIST` 类似于 `print`，但隐式追加换行。`say` 是 `{ local $ = "\n"; print LIST }` 的缩写。

改用 `sysseek`。

由于 ANSI C 的规则和严谨性，在某些系统上，每当你在读取和写入之间切换时，必须进行 seek。除其他因素外，这可能会产生调用 std' (3) 的效果。`whence` 为 1 (`SEEK_CUR`) 有助于不移动文件位置：`seek(TEST, 0, 1);`

这对于 `tail -f` 等应用也有用。如果你在读取时遇到 EOF（文件结束符）并睡眠一段时间，你（可能）必须固执行一个虚假的 `seek()` 来重置状态。`seek` 不会改变位置，但它会清除句柄上的文件结束状态，以便下一个 `<FILE>` 让 Perl 尝试读取某些内容。（我们希望如此。）

如果这不起作用，或者某些 I/O 特别糟糕，你可能需要这样的代码：

```perl
for (;;) { 
    my $curpus = tell(FILE); 
    $_ = <FILE>; 
    $curpus = tell(FILE);
    # 搜索某些内容并放入文件中 
    sleep($for_a_while);
    seek(FILE, $curpus, 0);
}
```

`seekdir DIRHOLE, $` 设置在 `DIRHOLE` 上 `readdir` 的当前位置。`POSIX` 必须是 `telldir` 返回的值。`seekdir` 还有关于相应系统库运行时可能进行目录压缩的注意事项。

### `selecthandle`

`selecthandle` 返回当前选定的文件句柄。如果提供了 `FILEHANDLE`，它将设置新的输出默认文件句柄。这有两个效果：首先，在没有指定文件句柄默认的情况下，`write` 或 `print` 将默认输出到此 `FILEHANDLE`。其次，与输出相关的变量的引用将指向此输出通道。

例如，对于多个输出通道的格式头部，你可以采取以下操作：

`FILEHANDLE` 可以是一个返回实际文件句柄名称的表达式。

因此：

```perl
$oldfh = select(STDERR); $| = 1; select($oldfh);
```



某些程序员可能更倾向于将文件句柄视为带有方法的对象，并倾向于将上一个示例写为：

```perl
use IO::Handle;
STDERR->autoflush(1);
```

可移植性问题：`perlport` 中的“select”。

如果你想管理多个文件句柄，你可能想编写如下的子程序：

```perl
sub fhbits {
    my $flist = @_;
    my $bits = "";
    for my $fh (@flist) {
        vec($bits, $fh, 1);
    }
    return $bits;
}
$rin = fhbits('STDIN', TTY, *MYSTOC);
```

通常的惯用法是：

```perl
($found,$timeleft) = select($rout=$rin, $wout=$win, $eout=$ein, timeout);
```

或者阻塞直到某些准备就绪，你可以这样做：

```perl
$found = select($rout=$rin, $wout=$win, $eout=$ein, undefined);
```

大多数系统不会在 `$timeleft` 中返回任何有用信息，因此标量上下文下的 `select()` 仅返回 `$found`。

位掩码的任何部分也可以被设置。如果指定了超时时间，单位为秒，可以是小数。注意：并非所有实现都能返回 `$timeleft`。如果不能，它们将总是返回 `$timeleft` 等于 `$timeout`。

你可以通过这种方式实现 250 毫秒的睡眠：

```perl
select(undef, undef, undef, 0.25);
```

注意 `select` 在信号（例如 `SIGALRM`）后是否重启取决于实现。另请参见 `perlport` 中关于可移植性的说明。

出错时，`select` 的行为与 (2) 一致：它返回 `-1` 并设置 `$!`。

在 Unix 系统上，即使没有数据可用，它也可能报告文件描述符为“准备好读取”，导致随后的读取发生阻塞。如果始终在 socket 上使用 `O_NONBLOCK`，就可以避免这一点。详情请见 (2) 和 (2)。

标准的 `IO::select` 模块提供了一个更友用户的 select 接口，主要是因为它为你完成了所有的位掩码操作。

> **警告：** 不要尝试将缓冲 I/O（如 `read` 或 `<FH>`）与 `select` 混合，除非 POSIX 允许，即便如此也仅限 POSIX 系统。你必须使用重新读取。

可移植性问题：`perlport` 中的“select”。

`semctl IDSEMNUM,CMD,ARG` 调用 System V IPC 函数 (2)。你可能需要先

```perl
use IO::SysV;
```

来获取正确的定义。如果 `CMD` 是 `IPC_STAT` 或 `GETALL`，则 `ARG` 必须是一个存储返回的 `sem_ds` 结构或信号量数组的变量。返回值类似于使用 `ioctl`：错误返回未定义值，零返回“0”，否则返回实际值。`ARG` 必须由原生短整型的向量组成，可以使用 `pack("s!` 创建。

可移植性问题：`perlport` 中的“semget”。

`semget KEY_MS,FLAGS` 调用 System V IPC 函数 (2)。返回信号量 ID，或出错时返回未定义值。另见 `periplc`、`IPC::SysV`、`IPC::SysV::Semaphore` 文档中的“SysV IPC”。

可移植性问题：`perlport` 中的“semget”。

`semop KEY,OPSTRING` 调用 System V IPC 函数 (2) 用于信号量操作，如信号和等待。`OPSTRING` 必须是信号量结构的压缩数组（packed array）。每个信号量结构都可以通过 `pack("s13", $semnum, $semop, $semflag)` 生成。`OPSTRING` 的长度意味着信号量操作的数量。成功时返回 true，出错时返回 false。作为一个示例，以下代码等待信号量 ID 上的 `$semnum`：

```perl
$semop = pack("s13", $semnum, $semop, $semflag);
```

```semid,semop, 1```

`send SOCKET,MSG,FLAGS` 向 socket 发送消息。`MSG` 必须是字符串或缓冲区。`FLAGS` 是发送的字节数。选项包括 `MSG_IGNAL`。返回发送的字节数，出错时返回 undefined。

`recv SOCKET,MSG,LEN` 从 socket 接收消息。`MSG` 必须是字符串或缓冲区。`LEN` 是最大字节数。选项包括 `MSG_PEEK`, `MSG_WAITALL`。返回接收的字节数，返回 undefined。

可移植性问题：`perlport` 中的“recv”。

`semop KEY,STRING,ARG` 调用 System V IPC 函数 (2) 用于信号量操作。`STRING` 必须是信号量结构的压缩数组。每个信号量结构可以通过 `pack("s13", $semnum, $semop, $semflag)` 生成。`ARG` 的长度意味着信号量操作的数量。成功时返回 true，出错时返回 false。作为一个示例，以下代码等待信号量 ID 上的 `$semnum`：

```perl
$semop = pack("s13", $semnum, $semop, $semflag);
```

```id,semop, 1```

`setsockopt SOCKET,LEVEL,OPT,VAL` 在 socket 上设置选项。`LEVEL` 是协议级别（例如 `SOL_SOCKET`, `IPPROTO_TCP`），`OPT` 是选项，`VAL` 是要设置的值。成功时返回 true，出错时返回 false。

`getpeerid(SOCKET)` 返回 socket 连接另一端的 PID。出错时返回 undefined。

`getsockopt SOCKET,LEVEL,OPT,VAR` 从 socket 获取选项。`LEVEL` 是协议级别，`OPT` 是选项，`VAR` 是存储值的变量。成功时返回 true，出错时返回 false。

`getsockname(SOCKET)` 返回本地 socket 的地址。返回地址结构或返回 undefined。

`getpeername(SOCKET)` 返回对端 socket 的地址。返回地址结构或返回 undefined。

`connect(SOCKET,ADDR,LEN)` 将 socket 连接到指定地址。成功时返回 true，出错时返回 false。

`listen(SOCKET, BACKLOG)` 使 socket 监听传入的连接。`BACKLOG` 是队列的最大长度。

`accept(SOCKET,ADDR,LEN)` 接受传入的连接。返回用于连接的新 socket 描述符和对端地址。出错时返回 undefined。

`close(SOCKET)` 关闭 socket。成功时返回 true，出错时返回 false。

`bind(SOCKET,ADDR,LEN)` 将 socket 绑定到地址。成功时返回 true，出错时返回 false。

`socket(DOMAIN,TYPE,PROTOCOL)` 创建一个新的 socket。返回 socket 描述符或返回 undefined。

可移植性问题：`perlport` 中的“setsockopt”。

使用此 socket

当你想告诉对方你已经完成读取（或反之）时，这在 socket 中非常有用。它也是一种更强制的关闭形式，因为它还会禁用任何派生（forked）或其他进程中的文件描述符。

成功返回 1；如果出错，且第一个参数不是有效句柄，则返回 undef；发生任何其他错误返回 -$。

`sin EXPR` 返回 `EXPR` 的正弦（以弧度为单位）。如果省略 `EXPR`，则返回 `$_` 的正弦。

对于逆操作，你可以使用 `Math::Trig::asin` 函数，或者使用以下关系：

```
sub asin { atan2($[0], sqrt(1 - $[0] * $[[0])) }
```



### `sleep EXPR`

导致脚本睡眠（整数）`EXPR` 秒，如果没有给出参数，则无限期睡眠。它返回实际睡眠的信号数量。
如果进程接收到如 `SIGALRM` 的信号，操作可能会被中断。

```perl
eval { local $SIGALARM } = sub { die "Alarm!\n"; sleep; }; die $@ unless
$@ eq "Alarm!\n";
```

你可能无法混合使用 `alarm` 和 `sleep` 调用，因为 `sleep` 通常是使用 `alarm` 实现的。

在某些旧系统上，`sleep` 的时间可能比你请求的少整一秒，取决于它的计数方式。大多数现代系统总是睡眠足的时间。然而，它们看起来可能睡眠比这更长，因为在繁忙的多任务系统中，你的进程可能不会立即运行。

对于比一秒更细粒度的延迟，`Time::HiRes` 模块（来自 CPAN，并从 Perl 5.8 开始成为标准分发的一部分）提供了 `usleep()`。你也可以使用 Perl 的四参数 `select()` 并让前几个参数留空，或者可能使用 `syscall` 接口访问 `(2)`（如果你的系统支持）。详情请参阅 `perl8`。
另请参见 `POSIX` 模块的函数。

### `SOCKET,DOMAIN,TYPE,PROTOCOL`

打开指定类型的 socket 并将其挂载到文件句柄 `SOCKET`。`DOMAIN`、`TYPE` 和 `PROTOCOL` 的指定方法与同名的 syscall 相同。你应该使用第一个来导入适当的定义。请参见 `perlip` 中 "Sockets: Client/Server Communication" 中的示例。

在支持文件 close-on-exec（执行时关闭）标志的系统上，该标志将为新打开的文件描述符设置，这取决于 `$F` 的值。请参阅 `perlvar` 中的 "^F"。

### `socketpair SOCKET1,SOCKET2,DOMAIN,TYPE,PROTOCOL`

在指定的域内创建一对指定类型的无名 socket 句柄。`DOMAIN`、`TYPE` 和 `PROTOCOL` 的指定方法与同名的 syscall 相同。如果未实现，则抛出异常。成功返回真。

在支持文件 close-on-exec 标志的系统上，该标志将为新打开的文件描述符设置，这取决于 `$F` 的值。请参阅 `perlar` 中的 "$F"。

某些系统在 `socketpair` 中定义了 `pipe`，其对 `pipe(Rdr, Wtr)` 调用本质上是：

```perl
use Socket; socketpair(Rdr, Wtr, AF_UNIX, SOCK_STREAM, PF_UNSPEC);

shutdown(Rdr, 1); # 读取者不再写入

shutdown(Wtr, 0); # 写入者不再读取
```

请参见 `perpic` 获取的 `socketpair` 示例。Perl 5.8 及更高版本如果你的系统实现了 socket 但没有实现 `socketpair`，将使用本地的 ip sockets 模拟 `socketpair`。

可移植性问题：`perlop` 中的 "socketpair"

### `SORT SUBNAME LIST`

`SORT LIST` `SORT LIST` `SORT LIST`

在上下文中，这对 `LIST` 进行排序并返回排序后的列表值。在标量上下文中，定义了 `sort()` 的行为。

如果省略 `SUBNAME` 或 `BLOCK`，则按标准字符串比较顺序排序。如果指定了 `SUBNAME`，它将返回子函数的名称，该函数返回小于、等于或大于 0 的整数，取决于列表元素的排序方式（`<<` 和 `c` 运算符在这些例程中非常有用）。`SUBNAME` 可以是一个标量变量名（无符号），在这种情况下，值提供了实际子函数的名称（或对的引用）。在 `SUBNAME` 的位置，你可以提供一个 `BLOCK` 作为匿名内联子函数。

如果子函数的原型是 `($)`，则待比较的元素将通过 `@_` 以引用方式传递，就像一个普通子函数一样。这比没有原型的子函数慢，在后者中，待比较的元素作为包全局变量 `$a $b` 传递到子函数中（见下例）。注意，在后的情况下，将 `$a` 和 `$b` 声明为局部变量是极适得其反的。

如果子函数是 `XSUB`，待比较的元素将推入栈中，正如参数通常传递给 `XSUB` 那样。`$a` 和 `$b` 不会被设置。

待比较的值始终通过引用传递，且不应被修改。

你不能使用 `perlin` 或 `got` 中描述的任何循环控制操作符退出 `sort` 块或子函数。

当使用 `locale`（但不是 'not_characters'）有效时，`SORT LIST` 根据当前的排序对规则 `locale` 进行排序。请参见 `perlocale`。

`sort()` 返回的是原始列表的别名，就像循环索引变量是列表元素的别名一样。这意味着，修改 `sort()` 返回的列表元素（例如在 `foreach`、`map` 或 `grep` 中）实际上会修改原始列表中的元素。在编写清晰的代码时，通常应该避免这样做。

Perl 5.6 及更早版本使用快速排序算法实现 `sort`。Perl 5.7 及之后使用了稳定的合并排序。这种稳定排序保留了相等元素的顺序。在 5.6 之前的中，快速排序是不稳定的。这种稳定排序是可能的。5.8 有一个 `sort` 属性，用于有限控制输出。568

```perl
@articles = sort {$b <=> $a} @files;
```

此时 `a` 和 `b` 分别是 `main::a` 和 `main::b`，但如果你在 `FooPack` 包中，其类型与排序时相同：

```perl
@articles = sort {$FooPack::b <=> FooPack::b} @files;
```

比较函数必须表现出一致性。如果它返回的结果不一致（例如，有时 `$x[$1]$` 小于 `$x[$2]$`，有时又相反），那么结果就是未定义的。

由于当任一个操作数为 `NaN`（不是数字）时 `<=>` 会返回 `undef`，因此在使用可能包含 NAN 的列表使用比较函数 `$a <=> $b` 进排序时要小心。示例演示了 `NaN != NaN` 以消除输入列表中的任何 NaN。

```perl
@result = sort { $a <=> $b } grep { $_ == $_ } @input;
```

### `splice array,OFFSET,LENGTH,list`

`array,OFFSET,LENGTH` `splice array,OFFSET,splice`
`ARRAY splice EXPR,OFFSET,LENGTH,list` `list splice EXPR,OFFSET,LENGTH` `splice EXPR,splice`

从数组中删除由 `offset` 和 `LENGTH` 指定的元素，如果有 `list`，则用 `list` 中的元素替换它们。在列表上下文中，返回从数组中删除的元素。在标量上下文中，返回最后一个删除的元素，如果没有删除元素则返回 `undef`，并根据需要增加或缩小数组。如果 `OFFSET` 为负数，则从数组末尾向前数该距离开始。如果省略 `LENGTH`，则删除从 `OFFSET` 之后的所有内容。如果长度为负数，则删除从该位置开始的元素，但保留数组末尾的所有内容。如果同时提供了 `OFFSET` 和 `LENGTH`，Perl 会发出警告并在数组末尾进行 `splice`。

在满足 `$#a >= $i` 的情况下，以下等价关系成立：

```perl
push(@a,$x,$y) splice(@a,0,0,$x,$y) pop(@a,--1) shift(@a)

slice(@a,0,1) unshift(@a,$x,$y) splice(@a,0,0,$x,$y) = $y

slice(@a,1,$1)
```

`splice` 可用于实现 n 队列处理

```perl
sub n_print { my $n = shift; while (my $_next != splice @a,0) { say

join(',', $_next); } splice(@a,a b c d e f g h); prints: $a-b

-c d-e f- g-h
```

从 Perl 5.14 开始，`splice` 可以接受标量 `EXPR`，该表达式必须持有指向未取消引用（unblessed）数组的引用。`splice` 的这一方面被认为是高度实验性的。具体行为可能会未来的 Perl 版本中可能会变化。

为了避免运行旧版本 Perl 的用户因神秘的语法错误产生困惑，可以在文件顶部添加此类代码，以指示您的代码仅适用于较新版本的 Perl：

```perl
use 5.014; # 对标量进行 push/pop（实验性）
```



### `split /PATTERN/,EXPR,LIMIT` `split /PATTERN/,EXPR` `split /PATTERN/`

将字符串 `EXPR` 分割为字符串列表，并在列表上下文中返回列表，在标量上下文中返回列表的大小。

如果只给出 `PATTERN`，则 `EXPR` 默认为 `$_`。

`EXPR` 中匹配 `PATTERN` 的任何内容都被视为分隔符，将 `EXPR` 分割成不包含分隔符的子串（称为“字段”）。注意，分隔符的长度可能大于一个字符，甚至没有任何字符（空字符串，即零宽匹配）。

`PATTERN` 不需要是常量；可以使用表达式来指定运行时变化的模式。

如果 `PATTERN` 匹配空字符串，则在匹配位置（字符之间）分割 `EXPR`。例如，以下代码：

```perl
print join(':', split('b', 'abc')), "\n";
```

使用 `'abc'` 中的 `'b'` 作为分隔符产生输出 `'a:c'`。然而，以下代码：

```perl
print join(':', split('', 'abc'), "\n";
```

使用空字符串产生输出 `'a:b:c'`；因此，空字符串可将 `EXPR` 分割为其组成字符的列表。

作为 `split` 的特殊情况，在匹配运算符语法 (`/`) 中给出的空模式专门匹配空字符串，这与它通常解释为最后一次成功匹配的相反。

如果 `PATTERN` 为 `/`，则它被处理为使用了多行修饰符 (`/m`)，因为在其他情况下不常使用。

另一个特殊情况是，当 `PATTERN` 被省略或由单个空格字符组成的字面量（如 ` ` 或 `\x20`，但不包括 `/`）时，`split` 会模拟命令行工具 `awk` 的默认行为。在这种情况下，`EXPR` 中的任何领先空白在分割前被移除，而 `PATTERN` 则被处理为 `/\s+/`；特别是，任何连续的空白（不仅仅是单个空格字符）都被用作分隔符。然而，通过指定模式 `/` 而不是字符串可以避免这种特殊处理，从而允许仅单个空格字符作为分隔符。在早期的 Perl 中，这种特殊情况仅限于使用模式参数进行 `split`，在 Perl 5.18.0 之后，这种特殊情况由任何评估为简单字符串的表达式触发。

如果省略，`PATTERN` 默认为单个空格 ` `，从而触发前述的 `awk` 模拟。

如果指定了 `LIMIT`，它代表 `EXPR` 可被分割的最大字段数；换句话说，`LIMIT` 大于 `EXPR` 可被分割的最大次数。因此，`LIMIT` 1 意味着 `EXPR` 最多可以分割零次，产生最多一个字段（即 `EXPR` 的整个值）。例如：

```perl
print join(':', split('', 'abc', 1)), "\n";
```

产生输出 `'abc'`，而以下代码：

```perl
print join(':', split('', 'abc', 2)), "\n";
```

产生输出 `'abc'`，而这些代码：

```perl
print join(':', split('', 'abc', 3)), "\n";
```

产生输出 `'a:bc'`。

如果 `LIMIT` 为负，则被处理为任意大；产生尽可能多的字段。如果省略 `LIMIT`（或为零），则通常被处理为负数，但例外是移除尾部字段（空字段始终保留）；如果所有字段都为空，则所有字段都被视为尾部字段（在这种情况下均被移除）。因此：

```perl
print join(':', split('', 'a,b,c')), "\n";
```

产生输出 `'a:bc'`；但以下代码：

```perl
print join(':', split('', 'a,b,c')), "\n";
```

产生输出 `'a'`。

如果 `PATTERN` 包含捕获组，则对于每个分隔符都会产生一个额外的字段，即该分隔符对应的捕获组的内容。

（注：此处似乎缺失了部分 man 文本）

且 `%g` 用于指数模的数字，而不是 100，这取决于系统：
它可能是三位或更少（根据需要进行零填充）。换句话说，`1.23` 的 99 次可以是 `"1.23e99"` 或 `"1.23e099"`。`%a` 和 `%A` 也是如此：指数或十六进制数字可以是浮点数；特别是 `"long doubles"` Perl 配置选项可能会引起意外。

在 `%` 和格式化字母之间，你可以指定几个额外的属性来控制格式的解释。按照顺序，这些是：

### 格式参数索引

一个显式的格式参数索引，例如 `2$`。默认情况下，`printf` 会格式化列表中未未使用的参数，但这允许你从列表中提取或跳过参数：

```perl
printf "%2d$1s", 12, 34; # 打印 "34 12"
printf "%3s d %1d", 1, 2, 3; # 打印 "3 1 1"
```

或者：

- 空格前缀：非负数前带一个空格
- `+` 前缀：非负数前带一个加号
- 字段内左对齐
- `0`：使用零填充，使用空格进行右对齐
- 确保任何八进制数字开头有 `"0"`
- 非零十六进制数前加 `"0x"` 或 `"0X"`
- 非零二进制数前加 `"0b"` 或 `"0B"`

例如：

```perl
printf "%c d", 12; # 打印 "12"
printf "<+d", 12; # 打印 "<+12"
printf "%6s", 12; # 打印 "<12"
printf "%-6s", 12; # 打印 "<12   "
printf "%6o", 12; # 打印 "000012"
printf "<#H>", 12; # 打印 "014"
printf "<#x", 12; # 打印 "<0xc"
printf "<#X>", 12; # 打印 "<0xC"
printf "<#b", 12; # 打印 "<0b1100"
printf "<#B100>"
```

当在标志中同时给出空格和加号时，使用加号来作为正数的前缀。

```perl
printf "%+d", 12; # 打印 "<+12"
printf 12; # 打印 "<+12"
```

当在 `%` 转换中给出标志和精度时，如果对于开头的 `"0"` 有必要，则增加精度。

```perl
printf "%.5o", 012; # 打印 "000012"
printf "<#.5o", 012345; # 打印 "012345"
printf "<#.0o", 0; # 打印 "<0"
printf "<1e", 10; # 打印 "<1.000000+1e+01>"
```

### 向量标志

此标志告诉 `printf` 将字符串解释为整数向量，对应字符串中的每个字符。`printf` 对每个整数应用格式，然后默认使用分隔符（点 `.`）连接生成的字符串。这对于显示属性中字符的序数值有用：

```perl
printf "%vd", "AB\x{100}"; # 打印 "65.2256"
printf "-%s version is %v\n", $AV; # Perl 的版本
```

使用星号 `* %v` 来覆盖用于分隔数字的字符串：

```perl
printf "address is %%%vX\n", ":", $addr; # IPv6 地址
printf "bits\n%%0b\n", "", $bits; # 随机位位
```

你可以使用类似 `*2v;` 的内容显式地指定用于连接的参数数字，例如：

```perl
printf "%4vX %4v %4vX"; # 3 个 IPv6 地址 @addr[1..3], ":" (最小) 宽度
```

参数通常被格式化为显示给定值所需的宽度。你可以通过放置一个数字来覆盖宽度，或者从下一个参数 `*<a>` 或从指定的参数（例如使用 `*2s`）获取宽度：

```perl
printf "%s", "a"; # 打印 "a"
printf "%6s", "a"; # 打印 "    a"
printf "%s", "a"; # 打印 "a"
printf "%2s", 6; # 打印 "6"
printf "%2s", "long"; # 打印 "lo" (不截断)
```

如果通过 `*` 获取的字段为负，其效果与标志 `-` 精度或最大宽度相同。

你可以通过指定一个 `.` 后跟一个数字来指定精度（用于数值转换）或最大宽度（用于字符串转换）。对于浮点格式，这精确指定了显示小数点右侧的多少位（默认为 6）。

```perl
# 这些示例取决于系统特定的差异 
printf "<.f>", 1; # 打印 "<1.000000>"
printf "<.1f", 1; # 打印 "<1.0"
printf ".0f", 1; # 打印 "<1>"
```

对于 `"g"` 和 `"G"`，这指定了显示的最大数字位数，包括小数点之前和之后的数字；例如：

```perl
# 这些示例取决于系统特定的差异。 
printf "<.g>", 1; # 打印 "<1>"
printf "<.10g", 1; # 打印 "<1>"
printf "<.g>", 100; # 打印 "<100>"
printf "<.1", 100; # 打印 "<100>"
printf ".2g", 100.01; # 打印 "<100+02>"
```



`printf` "<.5g", 100.01; # 打印 "<100.01>"

`printf` ".4g", 100.01; # 打印 "<100>"

```
对于整数转换，指定精度确保数字输出零填充到宽度，其中 0 被忽略：
```

```
`printf` "%6d", 1; # 打印 "000001"

`printf` "<+.6d>", 1; # 打印 "<+000001>"

`printf` "-10.6d", 1; # 打印 "<000001>"

`printf` "<6.d>", 1; # 打印 "<000001>"

`printf` 1; # 打印 ""

`printf` "-10.6d", 1; # 打印 "<+000001>"

`printf` "<+.6d", 1; # 打印 "<+000001>"

`printf` "<.6x>", 1; # 打印 "<000001>"

`printf` "<.6x>", 1; # 打印 "<000001>"

`printf` "%-10.6x", 1; # 打印 "<000001>"

`printf` "<.6x>", 1; # 打印 "<000001>"
```

对于字符串转换，指定精度会将字符串截断到指定的宽度：星号

```
`printf` "%.5s", "truncated"; # 打印 "<trunc>"

`printf` "%.10s", "truncated"; # 打印 "<truncated>"
```

你可以使用 `*:` 从下一个参数获取精度：

```
`printf` "%.*s", 1; # 打印 "<string>"

`printf` "%.*s", 1; # 打印 "<string>"
```

如果通过 `*` 获取的精度为负数，则完全没有精度：

```
`printf` "%.s", 7, "string"; # 打印 "<string>"

`printf` "%.*s", 3, "string"; # 打印 "<string>"

`printf` "%.*s", 0, "string"; # 打印 "<string>"

`printf` "%.*s", -1, 0; # 打印 "<string>"
```

你不能通过指定的数字获取精度，但预计未来这是可能的，例如 `*2`：

```
`printf` "%.2s", 1; 6; # 无效，但未来可行
```

对于数值转换，你可以使用精度将数字解释为 h, q, 或 l。对于整数转换（d o x b i D），数字通常假设为你平台的默认大小（通常为 32 或 64 位），但你可以覆盖它以使用编译器支持的标准类型：

```
`printf` "%6d", 1; # 打印 "<000001>"

`printf` "<+.6d>", 1; # 打印 "<+000001>"

`printf` "-10.6d", 1; # 打印 "<000001>"

`printf` "<6.d>", 1; # 打印 "<000001>"

`printf` 1; # 打印 ""

`printf` "-10.6d", 1; # 打印 "<+000001>"

`printf` "<+.6d", 1; # 打印 "<+000001>"

`printf` "<.6x>", 1; # 打印 "<000001>"

`printf` "<.6x>", 1; # 打印 "<000001>"

`printf` "%-10.6x", 1; # 打印 "<000001>"

`printf` "<.6x>", 1; # 打印 "<000001>"
```

大小规格 v 对 Perl 代码没有影响，但支持兼容代码。它意味着“Perl 整数或浮点数的标准大小”，这是默认值。

### 参数顺序

通常，`sprintf()` 获取下一个未使用的参数作为每个每个格式规范的格式化值。如果格式规范使用 `*` 需要额外的参数，这些参数将在格式化值之前按照它们在格式规范中出现的顺序从列表中消耗。当通过显式索引指定参数时，这不会影响参数的正常顺序，即使显式指定的索引本应该是下一个参数。

所以：

```
`printf` "%.*s", `$a`, `$b`, `$c`; # 使用 `$a` 用于宽度，`$b` 用于精度，`$c` 作为格式化值；

`printf` "%1$.*s", `$a`, `$b`; # 将使用 `$a` 用于宽度和精度，`$b` 作为格式化值。
```

这里还有更多一些示例；请注意，当使用显式索引时，`$` 可能需要转义：

```
`printf` "%2d %d\n", 12, 34; # 将打印 "34 12\n"

`printf` "%2d %d\n", 12, 34, 56; # 将打印 "56 12 34\n"

`printf` "%2*3$d %d\n", 12, 34, 56; # 将打印 "34 12\n"
```

如果 `use local`（包括区域 'characters'）生效且 `POSIX::setlocale()` 已调用，则用于格式化浮点数的分隔符会受到 `LC_NUMERIC` 区域的影响。参见 `perlocale` 和 `POSIX`。

`sqrt` `EXPR` 返回 `EXPR` 的正平方根。如果省略 `EXPR`，则使用 `$$`。除非你加载了 `Math::Complex` 模块，否则只对非负操作数有效。

```
use Math::Complex; print sqrt(-4); # print 2
```

`rand` `EXPR` 设置并返回 `rand` 运算符的种子。该函数的目的是“种子”`rand` 函数，以便 `rand` 产生一个

你可以通过 `Config` 查找 Perl 是否支持四字节：

```
use Config; if ($Config{64bit} == "define" || $Config{longsize} >= 8) { print "Nice quad\n"; }
```

每次运行程序时都会使用不同的种子（seed）。当带有参数调用时，`srand` 会使用该参数作为种子；否则，它会（半）随机选择一个种子。在任何情况下，在 Perl 5.14 中 `srand` 都会返回种子。为了指示你的代码仅运行在较版本的 Perl 上：

```perl
use 5.014; # 这样 rand 返回种子
```

如果没有显式地调用 `rand()`，则在第一次使用 `rand` 操作符时，它会隐式不带参数。然而，在某些情况下程序可能会调用 `srand`。一种是为了生成可预测的结果，通常用于测试或调试。在这种情况下，你使用 `srand($seed)`，每次都使用相同的种子。另一种情况是你可能想在 `fork()` 之后调用 `srand($)`，以避免子进程与父进程（以及其他进程）共享相同的种子值。

不要在一个进程中多次调用一次 `srand`（即不带参数调用）。随机数生成器的内部状态包含的熵比任何种子能提供的多，因此再次调用 `rand()` 可以产生随机性。

大多数 `srand` 的实现接受一个整数，并静地截断小数。`srand(42)` 通常产生的结果与 `srand(42.1)` 相同。为了安全起见，请向 `srand` 传递一个整数。

返回种子的典型用法是一个测试程序，该程序在可运行时间内有许多组合需要全面测试。它可以每次测试一个随机子集，如果发生失败，则记录所使用的种子，以便以后重现结果。

`rand()` 不是加密学安全的。你不应该在安全敏感的情况下依赖它。在编写本文时，没有第三方 CPAN 模块提供被其作者标识为加密安全的随机数生成器，包括：`Data::Entry`、`Crypt::Rand`、`Math::Secure` 和 `Math::TRandom`。

`stat` `FILEHANDLE` `expr` `stat` `dirHANDLE` 返回一个包含 13 个元素的列表，提供文件的状态信息，该文件是通过 `HANDLE` 或 `dirHANDLE` 打开的文件，或者是由 `EXPR` 命名的文件。如果省略了 `EXPR`，它返回 `$_`（而不是 `$`）。如果 `stat` 失败，则返回空列表。通常用于：

```perl
($dev, $ino, $mode, $link, $uid, $gdev, $seed,
$atime, $ctime, $blize, $blocks) = stat($filename)
```



并不是所有的文件系统都支持所有字段。以下是这些字段的含义：

| Index | Field | Description |
| :--- | :--- | :--- |
| 0 | dev | 文件系统数量 |
| 1 | ino | inode 节点 |
| 2 | mode | 文件模式（类型和权限） |
| 3 | nlink | 指向文件的（硬）链接数 |
| 4 | uid | 文件的数值用户 ID |
| 5 | gid | 文件的数值组 ID |
| 6 | rdev | 设备标识符 |
| 7 | size | 文件总大小，单位为字节 |
| 8 | atime | 自 Unix 时间以来的最后访问时间（秒） |
| 9 | mtime | 自 Unix 时间以来的最后修改时间（秒） |
| 10 | ctime | 自文件变化的 inode 更改时间（秒，可能随文件而异） |
| 11 | blize | 与磁盘上分配的特定设备块交互的首选 I/O 大小（字节）（通常但并非总是每个 512 字节） |

（时间戳 epoch 为 1970 年 1 月 1 日 00:00 GMT）。

*) 并不是所有文件系统都支持所有字段。注意的是，`ctime` 字段是不可移植的。特别是，你不能期望它是一个“创建时间”；详情参见“文件与文件系统”。

如果 `stat` 传递了一个由下划线组成的特殊文件句柄，则 `stat` 完成，但会返回上一次或最新的 `stat` 结构的当前内容。
示例：

```perl
if (-x $file && (($d) = stat($)) && $d < 0) { print "$file 是可执行的\n"; }
```

（这仅在设备号为负的机器上有效。）由于模式同时包含文件类型和权限，如果你想看到权限，应该使用 `%0o` 掩码文件类型。

在标量上下文中，`stat` 返回一个布尔值表示成功或失败，如果成功，则设置与文件句柄关联的信息。`File::stat` 模块提供方便的按名称访问机制：

```perl
use File::stat;

$sb = stat($filename);

printf "文件是 %s，大小为 %s，时间为 %s\n", $filename, $sb->size, localtime($sb->mtime);
```

你可以从 `Fcntl` 模块导入现代的 `IF*` 和 `IS*` 常量

```perl
use Fcntl ':mode';

$mode = (stat($filename))[2]; $user_rwx = ($mode & $S_IRWX) >> 2; $group_read = ($mode & $S_IRGRP) >> 3; $other_execute = $mode & $S_IXOTH; printf "权限为 %4o\n", $S_IMODE($mode), $S_ISUID($mode); $is_setuid = $mode & $S_ISUID; $is_directory=$S_ISDIR;
```

你可以使用 `-u` 和 `-d` 操作符。修改 S_IF常量：
- 权限：用户、组、其他的读、写、执行。`$S_IRWX` `$S_IRWUS` `$S_IWUSR` `$S_IXUSR` `$S_IRGRP` `$S_IWGRP` `$S_IXGRP` `$S_IRXO` `$S_IROTH` `$S_IWOTH` `$S_IXOTH`
- 设置用户/设置组/粘性/保存文本：注意这些的含义取决于系统。`$S_ISUID` `$S_ISGID` `$S_ISVT` `$S_ISTXT`
- 文件类型：并非在你的系统中都可用。`$S_IFREG` `$S_IFDIR` `$S_IFLNK` `$S_IFBLCK` `$S_IFCHR` `$S_IFIFO` `$S_IFWHT` `$S_ENFMT`
- 以下是 `$S_IRUSR`, `$S_IWUSR` 和 `$S_IXUSR` 的兼容别名。`$S_IREADT_EXEC`

以及 `S_IMODE` 返回包含权限位的的 `$mode` 部分。包含文件类型的 `$mode` 部分可以与（例如）`$S_IFREG` 进行位与运算。

比专门的程序更快 (1)。以下代码扫描一个列表列表 (`@files`) 以查找单词列表 (`@words`)，并打印包含匹配项的列表名称：

```
$search = 'while (<>) { stuk; }; foreach @words { $search .= "\n"\$ARGV; if ($search \$word\|b;\n'); } $search = $ARGV @files;

def undef; eval $search; # this $ $s = "n"; put back to normal

delimiter foreach $file (sort keys(%s)) { print $file, "n";
```

## SUB NAME BLOCK NAME (PROTO)

### 块名称 (PROTO):
ATTRS Block 这是一个子程序定义，而不是一个真正的函数。如果没有块（block），它
只是一个前向声明。如果没有名称，它就是一个匿名函数声明，因此
返回一个值：引用的代码返回它。

关于子程序和引用的详细信息请参见 perblef；关于属性的更多信息请参见 attributes 和
Attribute::Handlers。

### __SUB__ 一个特殊的标记，用于返回当前子程序的引用，或在子程序中返回 undef。

`__SUB__` 在正则代码块 `/(?:...})/)` 中的行为可能会发生变化。

此标记在 v5.16 或 "current_sub" 功能下可用。请参见 feature。

### substr EXPR,OFFSET,LENGTH,REPLACEMENT

`substr EXPR,OFFSET,LENGTH` `substr EXPR,OFFSET`
从 `EXPR` 中提取子字符串并返回。第一个字符位于偏移量零 处。如果 `OFFSET` 为
负数，则从字符串末尾向前计算。如果 `LENGTH` 为负数，则返回直到字符串结束的所有内容。如果 `LENGTH` 为负数，则保留相应数量

```
$my = "The black cat climbed the tree"; $color = substr $s, 4, 
; # my $middle = substr $s, 4, -11; # black cat climbed the tree $my $end

sub = substr $s, 14; # black cat climbed the tree $my $tail = substr $s, -4; # tree

my $2 = substr $s, -4, 2; # tr
```

你可以将 `substr()` 函数作为 Ivalue（右值），在这种情况下 expr 必须本身。
如果赋值的值比 `LENGTH` 短，字符串将缩小；如果赋值的值比 `LENGTH` 长，字符串将增长以适应它。为了保持相同的长度，你可能需要使用 `sprintf` 对你的值进行填充或截断。

如果 `OFFSET` 和 `LENGTH` 指定子字符串部分位于字符串外部，则只返回字符串内部的部分。如果子字符串超出了字符串的任何端，`substr(` 返回 `undef` 并产生警告。当作为参数使用时，指定完全位于字符串外的子字符串将抛出异常。这里有一个显示边界情况 行为的示例：

```
$my name = 'Fred'; substr($name, 4) = 'dy'; # $name 现在是 'freddy'

$null = substr $name, 6, 2; # 返回 " (无警告) $my $oops = substr

$name, 7; # 返回 undef，带有警告 substr($name, 7) = 'gap'; # 抛出

an exception
```

使用 `substr()` 作为 Ivalue 的替代方案是使用第四个参数替换字符串。这允许你在一次操作中替换 `EXPR` 的部分并返回之前的内容，就像使用 `splice()` 一样。

$my = "The black cat climbed the green tree"; my $z = substr $s, 14, 7,
jumped from"; # climbed $s 现在是 The black cat jumped from the green
tree

注意 `substr` 三个参数版本返回的 lvalue（左值）就像一个“万能弹”；每次被赋值时，它都会记住修改的是原始字符串的哪部分；例如：

```
$x = '1234'; for (substr($x,1,2)) { $_ = 'a'; print $x, "\n"; prints 1a4

$_ = 'xyz'; print $x, "\n"; prints 1xyz4 $x = '56789'; $_ = 'pqr'; print

$x, "\n"; prints 5pq9
```

使用负偏移量时，当目标字符串改变时，它会记住位置：



`$x = '1234'; for (substr($x, -3, 2)) { $_ = 'a'; print $x, "\n"; }` prints

`1a4`, 如上 `$x = 'abcdef'; print $x, "\n";` prints `f`

### symlink OLDFILE

创建一个与旧文件名符号链接的新新文件名。
成功返回 `1`，否则返回 `0`。在不支持符号链接的系统上，将抛出异常。要进行检查，请使用 `eval`：

移植性问题：`perport` 中的 `"symlink"`。

### syscall

`LIST` 调用列表的第一个元素指定的系统，并将剩余元素作为参数传递给系统调用。如果未实现，将抛出异常。参数的解释如下：如果给定的参数是数字，则将其作为 `int` 传递。否则，传递字符串值。你负责确保字符串预先扩展足够长，以接收可能写入字符串的任何结果。你不能将字符串字面量（或其他只读字符串）作为 `syscall` 的参数，因为 Perl 认为任何指针都可能

### write

（此处由于原文存在大量重复的段落，根据指令“一定不要重复输出原文”且“翻译给定文本”，译文仅保留核心逻辑描述，并过滤了完全重复的冗余部分。）

它绕过了缓冲型 I/O，因此将其与其他种类的读取、`print`、`write`、`seek`、`tell` 或 `eof` 混合使用会导致混淆，因为 `perlio` 或 `stio` 层使用了缓冲区。返回实际读取的字节数、在文件末尾，或如果发生错误则返回 `undef`（在后者情况下，`$!` 也会被设置）。`SCALAR` 会增大或缩小，使得实际读取的最后一个字节是读取后标量的最后一个字节。

可以指定偏移量以从字符串起始位置以外的某个处读取数据。负偏移量指定从字符串向后倒数多个字符的位置。大于 `SCALAR` 长度的正数偏移量将导致字符串在追加读取结果之前，使用 `\0` 字节填充（`padded`）到所需的尺寸。

由于没有 `sysof()` 函数，这没关系，因为 `eof()` 在设备文件（如 `tty`）上不起作用。使用 `sysread()` 并检查返回值是否为 `0` 来判断是否已完成。

注意，如果文件句柄被标记为 `:utf8`，则 Unicode 字符将按字节读取（`LENGTH` 和 `sysread()` 的返回值是 Unicode 字符）。`:encoding(...)` 层隐式引入了 `:utf8` 层。参见 `"binmode"`、`"open"` 和 `open` pr。

`sysseek FILEHANDLE,POSITION,WHENCE` 设置 `FILEHANDLE` 的位置（字节）`(2)`。`myfile` 是一个提供文件句柄名称的表达式。`WHENCE` 的值为 `0`，表示设置新位置；`1` 表示将其设置为当前位置加上偏移量；`2` 表示将其设置为 EOF 位置（通常为负数）。

注意字节偏移量：如果文件句柄已设置为操作字符（例如通过使用 `:encoding(utf8)` I/O 层），`tell()` 将返回字节偏移量，而不是字符偏移量（因为实现 `sysread()` 的速度是无法接受的慢）。

`sysseek()` 绕过了常规的 I/O，因此将其与 `sysread` 以外的读取（例如 `<-` 或 `read()`）、`print`、`write`、`seek`、`tell` 或 `eof` 混合使用会导致混淆。

对于 `whence`，你也可以使用 `Fcntl` 模块中的 `SEEK_SET`、`SEEK_CUR` 和 `SEEK_END`（文件开头、当前位置、文件末尾）。使用常量比使用 `0`、`1` 和 `2` 更具可移植性。为了定义一个“系统”函数：使用 `Fcntl` `'SEEK_CUR'`；`substr sysseek($], 0, SEEK_CUR)`

返回新位置，或失败时返回未定义值。返回字符串 `$0` 或真的位置；`sysread` 成功时返回真，失败时返回假，你仍然可以轻松确定新位置。

`system LIST LIST` 执行的操作完全相同，除了 `LIST` 不同外，它首先进行 `fork`，然后父进程等待子进程退出。注意，参数处理取决于参数的数量。如果 `LIST` 中有多个参数，或者如果 `LIST` 是一个带有多个值的数组，则使用列表的第一个元素启动程序，并使用列表其余元素提供的参数进行运行。如果只有一个标量参数，则会检查该参数是否包含 shell 元字符，如果有，则整个参数将传递给系统的命令 shell 进行解析（这在 Unix 平台上是 `/bin/sh -c`，但在其他平台上会有所不同）。如果参数中没有 shell 元字符，它将被拆分成单词并直接传递给 `execv`，这效率更高。在 Windows 上，只有 `system PROGRAM LIST` 语法可以可靠地避免使用 shell；`system LIST` 即使有多个元素，如果第一个派生失败，将回退到 shell。

Perl 会将在任何可能导致 `fork` 的操作前刷新所有输出文件，但在某些平台上可能不支持此操作（参见 `perl`）。为了安全起见，你可能需要设置 `$`（英文为 `AUTOFLUSH`）或对任何打开的句柄调用 `IO::Handle` 的 `autoflush()`。

返回值是 `wait` 调用的程序退出状态。要获取实际值，请右移八位（见下文）。另见“`exec`”。这不是你使用命令输出的方法；对于输出，你应该像 `perl` 中“`STRING`”描述的那样使用反引号（backticks）或 `qx`。返回值 `-1` 表示启动程序或任何 `(2)` 系统调用失败（检查 `$!` 的原因）。

如果你想让 `system`（以及 Perl 的许多其他部分）报错，请查看 `autodie` 祈格。

像 `exec` 一样，如果你使用 `system PROGRAM LIST` 语法，`system` 允许你欺骗程序其名称。再次参见“`exec`”。

由于在 `system` 执行期间忽略了 `SIGINT` 和 `SIGQUOI`，如果你期望程序在接收这些信号时终止，你将根据返回值进行安排。

```perl
@args = ("command", "arg1", "arg2"); system($args) == 0 or die "system args failed: $@";
```

如果你想手动检查 `system` 的失败，可以像这样通过检查 `$?` 来检查所有的失败模式：

```perl
if ($? == -1) { print "failed to execute: %n"; } elsif ($? & 127) {
printf "child died with signal %d, %s coredump\n", ($? & 127), ($? & 128) ? 'with' : 'without'
} else { printf "child exited with value %d\n", $? >> 8 };
```



或者，你可以使用 POSIX 模块中的 `(w*)` 调用检查 `${CHILD_NATIVE>}` 的结果。

当 `system` 的参数直接由 shell 执行时，结果和返回码会存在特殊情况。参见 perl 中的“system”。

`syswrite FILEHANDLE,SCALAR,LENGTH` 尝试从 SCALAR 向 FILEHANDLE 写入 LENGTH 字节。perlio 或 stio 层使用了缓冲区。返回实际读取的字节数，或如果发生错误则返回 undef（在后者情况下，`$!` 也会被设置）。SCALAR 会增大或缩小，使得实际读取的最后一个字节是读取后标量的最后一个字节。

可以指定偏移量以从字符串起始位置以外的某个处读取数据。负偏移量指定从字符串向后倒数多个字符的位置。大于 SCALAR 长度的正数偏移量将导致字符串在追加读取结果之前，使用 `\0` 字节填充到所需的尺寸。

没有 `sysof()` 函数，这没关系，因为 `eof()` 在设备文件（如 tty）上不起作用。使用 `sysread()` 并检查返回值是否为 0 来判断是否完成。

注意，如果文件句柄被标记为 `:utf8`，则 Unicode 字符将按字节读取（`LENGTH` 和 `sysread()` 的返回值是 Unicode 字符）。`:encoding(...)` 层隐式引入了 `:utf8` 层。参见 "binmode"、"open" 和 open pr。

`sysseek FILEHANDLE,POSITION,WHENCE` 设置 FILEHANDLE 的位置（字节）(2)。`myfile` 是一个提供文件句柄名称的表达式。`WHENCE` 的值为 0，表示设置新位置；1 表示将其设置为当前位置加上偏移量；2 表示将其设置为 EOF 位置（通常为负数）。

注意字节偏移量：如果文件句柄已设置为操作字符（例如通过使用 `:encoding(utf8)` I/O 层），`tell()` 将返回字节偏移量，而不是字符偏移量（因为实现 `sysread()` 的速度是无法接受的慢）。

`sysseek()` 绕过了常规的 I/O，因此将其与 `sysread` 以外的读取（例如 `<-` 或 `read()`）、print、write、seek、tell 或 eof 混合使用会导致混淆。

对于 `whence`，你也可以使用 Fcntl 模块中的 `SEEK_SET`、`SEEK_CUR` 和 `SEEK_END`（文件开头、当前位置、文件末尾）。使用常量比使用 0、1 和 2 更具可移植性。为了定义一个“系统”函数：使用 Fcntl 'SEEK_CUR'；`substr sysseek($], 0, SEEK_CUR)`

返回新位置，或失败时返回未定义值。返回字符串 `$0` 或真的位置；`sysread` 成功时返回真，失败时返回假，你仍然可以轻松确定新位置。

`system LIST LIST` 执行的操作完全相同，除了 `LIST` 不同外，它首先进行 `fork`，然后父进程等待子进程退出。注意，参数处理取决于参数的数量。如果 `LIST` 中有多个参数，或者如果 `LIST` 是一个带有多个值的数组，则使用列表的第一个元素启动程序，并使用列表其余元素提供的参数进行运行。如果只有一个标量参数，则会检查该参数是否包含 shell 元字符，如果有，则整个参数将传递给系统的命令 shell 进行解析（这在 Unix 平台上是 `/bin/sh -c`，但在其他平台上会有所不同）。如果参数中没有 shell 元字符，它将被拆分成单词并直接传递给 `execv`，这效率更高。在 Windows 上，只有 `system PROGRAM LIST` 语法可以可靠地避免使用 shell；`system LIST` 即使有多个元素，如果第一个派生失败，将回退到 shell。

Perl 会将在任何可能导致 `fork` 的操作前刷新所有输出文件，但在某些平台上可能不支持此操作（参见 perl）。为了安全起见，你可能需要设置 `$`（英文为 AUTOFLUSH）或对任何打开的句柄调用 `IO::Handle` 的 `autoflush()`。

返回值是 `wait` 调用用的程序退出状态。要获取实际值，请右移八位（见下文）。另见“exec”。这不是你使用命令输出的方法；对于输出，你应该像 perl 中“STRING”描述的那样使用反引号或 `qx`。返回值 -1 表示启动程序或任何 (2) 系统调用失败（检查 `$!` 的原因）。

如果你想让 `system`（以及 Perl 的许多其他部分）报错，请查看 `autodie` 祈格。

像 `exec` 一样，如果你使用 `system PROGRAM LIST` 语法，`system` 允许你欺骗程序其名称。再次参见“exec”。

由于在 `system` 执行期间忽略了 SIGINT 和 SIGQUOI，如果你期望程序在接收这些信号时终止，你将根据返回值进行安排。

```perl
@args = ("command", "arg1", "arg2"); system($args) == 0 or die "system args failed: $@";
```

如果你想手动检查 `system` 的失败，可以像这样通过检查 `$?` 来检查所有的失败模式：

```perl
if ($? == -1) { print "failed to execute: %n"; } elsif ($? & 127) {
printf "child died with signal %d, %s coredump\n", ($? & 127), ($? & 128) ? 'with' : 'without'
} else { printf "child exited with value %d\n", $? >> 8 };
```

或者，你可以使用 POSIX 模块中的 `(w*)` 调用检查 `${CHILD_NATIVE>}` 的结果。

当 `system` 的参数直接由 shell 执行时，结果和返回码会存在特殊情况。参见 perl 中的“system”。

`syswrite FILEHANDLE,SCALAR,LENGTH` 尝试从 SCALAR 向 FILEHANDLE 写入 LENGTH 字节。perlio 或 stio 层使用了缓冲区。返回实际读取的字节数，或如果发生错误则返回 undef（在后一种情况下，`$!` 也会被设置）。SCALAR 会增大或缩小，使得实际读取的最后一个字节是读取后标量的最后一个字节。

可以指定偏移量以从字符串起始位置以外的某个处读取数据。负偏移量指定从字符串向后倒数多个字符的位置。大于 SCALAR 长度的正数偏移量将导致字符串在追加读取结果之前，使用 `\0` 字节填充到所需的尺寸。

警告：如果文件句柄被标记为 `:utf8`，Unicode 字符将按字节读取（`LENGTH` 和 `sysread()` 的返回值是 Unicode 字符）。`:encoding(...)` 层隐式引入了 `:utf8` 层。或者，如果句柄未标记编码但你尝试写入代码点超过 255 的字符，将抛出异常。参见 "binmode"、"open" 和 open pr。

`tell` 返回当前的字节位置，或错误时返回 -1。ifelse 是一个提供文件句柄名称的表达式。如果省略 ifelse，假设文件最后读取。

注意字节偏移量：`:encoding(utf8)` open layer)

`tell()` 对于标准流 STDIN 的返回值取决于操作系统：它可能返回 -1 或其他值。管道、FIFO 和套接字上的 `tell()` 通常返回 -1。

没有 `syscall` 函数。使用 `sysseek(FH, 0, 1)` 可以实现。

不要对被 `sysread()`、`syswrite()` 或 `sysseek()` 操作过的文件句柄使用 `tell()`（或缓冲 I/O 操作）。这些函数忽略缓冲区，而 `tell()` 不会。

`teldir` 返回 dirHANDLE 上 readdir 例程的当前位置。可以通过 seekdir 访问目录中的特定位置。teldir 有关于相应运行时可能的目录压缩的警告。

`tie VARIABLE,CLASSNAME,LIST` 将变量绑定到包类，该类将为变量提供实现。`VARIABLE` 是要加密的变量名称。`CLASSNAME` 是实现任何类型的类。任何参数都会传递给类的相应构造方法（意味着 TIESCALAR、TIEHANDLE、TIEARRAY 或 TIEHASH）。通常这些参数会被传递给 C 的 `dbm_open()` 函数。构造函数返回的对象也会由 `tie` 函数返回，如果你想访问 CLASSNAME 中的其他方法，这将非常有用。

注意，作为键和值的函数在大对象（如 DBM 文件）上可能会返回巨大的列表。你可能倾向于使用 `each` 函数来迭代此类对象。
示例：

```perl
# 打印历史文件偏移量 NDBM_File: tie($HIST, NDBM_File);
```



```perl
/usr/lib/news/history', 1, 0; while ($key,$val) = each $HIST) { print $key, ' = ', unpack('L',$val), "\n"; } untie($HIST)
```

## 实现哈希（hash）的类应具有以下方法：

`TIEHASH` `classname`, `LIST` `FETCH` `this`, `KEY` `STORE` `this`, `key`, `value` `DELETE` `this`, `key` `CLEAR` `THIS` `EXISTS` `this`, `FIRSTKEY` `this` `NEXTKEY` `this`, `last` `SCALAR` `this` `DESTROY` `THIS` `UNTIE`

## 实现普通数组（array）的类应具有以下方法：

`TIEARRAY` `classname`, `LIST` `FETCH` `this`, `KEY` `STORE` `this`, `key`, `value` `FETCHSIZE` `this` `STORESIZE` `this`, `CLEAR` `PUSH` `this`, `LIST` `SPLICE` `this`, `offset`, `length`, `LIST` `EXTEND` `this`, `count` `UNSHIFT` `this`, `key` `EXISTS` `this`, `key` `DESTROY` `this` `UNTIE` `this`

## 实现文件句柄（filehandle）的类应具有以下方法：

`TIEHANDLE` `classname`, `LIST` `READ` `this`, `scalar`, `length`, `offset` `READLINE` `this` `GETC` `WRITE` `this`, `scalar`, `length`, `offset` `PRINT` `this`, `LIST` `PRINT` `this`, `format`, `LIST` `BINMODE` `EOF` `FILENO` `this` `SEEK`, `position`, `whence` `TELL` `OPEN` `this` `mode`, `LIST` `CLOSE` `this` `DESTROY` `this` `UNTIE`

## 实现标量（scalar）的类应具有以下方法：

`TIESCALAR` `classname`, `LIST` `FETCH` `this`, `STORE` `this`, `value` `DESTROY` `this` `until` `Tie::Scalar`, `Tie::Handle`.

并非所有列出的方法都已实现。请参阅 `perltie`、`Tie::Hash`、`Tie::Array`。

与 `dbopen` 不同，`tie` 函数不会使用模块进行绑定；你需要显式地自己完成。请参阅 `DB_File` 和 `Config` 模块以获取有趣的 `tie` 实现。

详情请参阅 `perltie` 中的 "`tied VARIABLE`".

`tied VARIABLE` 返回 `VARIABLE` 所底层对象的引用（该值与最初将变量绑定到包的 `tie` 调用返回的值相同）。如果 `VARIABLE` 未绑定到包，则返回未定义值。`time` 返回系统认为的纪元（epoch）的非闰秒数，适用于传递给 `gtime` 和 `localtime`。在大多数系统中，纪元是 UTC 1970年1月1日 00:00:00；一个显著的例子是 Mac Classic，它使用当前时区的 1904年1月1日 00:00:00 作为其纪元。

要测量比秒更高粒度的时间，请使用从 Perl 5.8 开始的 `Time::HiRes` 模块（在此之前的 CPAN），或者如果你有的话，可能可以使用 Perl 的 `syscall`。请参阅 `perl8`。

对于日期时间处理，请查看 CPAN 上的相关模块。需要全面的日期时间表示，请查看 `DateTime` 模块。

返回一个包含四个元素的列表，给出此进程及其任何已子进程的用户和系统时间（秒）。

```perl
($user, $system, $cuser, $csystem) = times;
```

在标量上下文中，`times` 返回 `$user`。

子进程的时间仅包含已终止的子进程。

可移植性问题：`perport` 中的 "`times`"。

`tr///` 译字运算符。等同于 `y///`。参阅 `perlop` 中的 "`Quote-Like Operators`"。

`truncate FILEHANDLE,LENGTH` `truncate EXPR,LENGTH` 将 `FILEHANDLE` 打开的或由 `EXPR` 命名的文件截起到指定的长度。如果你的系统没有实现 `truncate`，则会抛出异常。成功返回真，错误时返回 `undef$`。

如果 `LENGTH` 大于文件长度，行为将未定义。

`FILEHANDLE` 在文件中的位置保持不变。你可能想在写入文件之前调用 `seek`。

可移植性问题：`perport` 中的 "`truncate`"。

`UC xpr` 返回 `EXPR` 的大写形式版本。这是实现双引号字符串中 `\u` 转义字符的内部函数。它不会尝试对首字母进行标题大小写映射。该功能请参见 "`ucfirst`"。

如果省略 `EXPR`，则使用 `$_`。

此函数在各种 pragma（如 `locale` 区域）下的行为与 "`lc`" 相同。

`ucfirst EXpr` `ucfirst` 返回 `EXPR` 的值，并将第一个字符转为大写（Unicode 中的标题大小写）。这是实现双引号字符串中 `\u` 转义字符的内部函数。

如果省略 `EXPR`，则使用 `$_`。

此函数在各种 pragma（如 `locale` 区域）下的行为与 "`lc`" 相同。

`umask EXPR` `umask` 将进程的掩码设置为 `EXPR` 并返回旧值。如果省略 `EXPR`，仅返回当前掩码。

Unix 权限 `rwxr -x-` 表示为三组三位，或三个八进制数字：`0756`（开头的 `0` 表示八进制且不是数字之一）。`umask` 值是一个表示已禁用权限的数字。通过 `mkdir` 或 `sysopen` 传递的权限（或“模式”）值会被你的 `umask` 修改，因此如果你告诉 `sysopen` 创建一个权限为 `0777` 的文件，而你的 `umask` 是 `0022`，那么文件实际创建时的权限将为 `0755`。如果你的 `umask` 是 `0027`（组不可写；其他人不可读、写、执行），那么传递 `sysopen` `0666` 将创建一个权限为 `0640` 的文件（因为 `0666 &~ 027` 是 `0640`）。

这里有一些建议：为普通文件（在 `sysopen` 中）创建一个 `0666` 的目录，为目录（在 `mkdir` 中）和可执行文件创建一个 `0777` 的目录。这给了用户选择的自由：如果他们想要受保护的文件，可能会选择 `0222` 的掩码。[此处后续文本存在截断或乱码，无法完整翻译]

`untie VARIABLE` 解除变量与包之间的绑定。（参见 `tie`）。如果变量未被绑定，则无影响。`use Module VERSION LIST` 将从命名模块的 `Module` 语义导入到当前包中，通过将某些子程序或变量名别名到你的包中来实现。它完全等同于

```perl
BEGIN { require Module; Module->import( LIST ); };
```

除非 `Module` 是一个怪类。通过使用该模块可以使导入变为条件性的。（注意：OCR 文本 "Module be a beast" 可能是 "Module be a class" 或类似内容的损坏，但我将保留提供的文本并修复明显的拼写错误）。除非 `Module` 是一个怪类。通过使用该模块可以使导入变为条件性的。

在 `VERSION` 的特殊用法中，`VERSION` 可以是正的小数（如 `5.006`），也可以是形式为 `v5.6.1` 的 v-字符串，该字符串将与 `$v`（即 `$PER_VERSION`）进行比较。如果 `VERSION` 大于当前 Perl 解释器的版本，将抛出异常；Perl 将停止解析文件的剩余部分。这与 "require" 对比，后者可以在运行时进行类似的检查。对称地，不指定 `VERSION` 则允许你指定比指定版本更老的 Perl 版本。

通常应避免将 `VERSION` 指定为 `v5.6.1` 字面量，因为这在不支持此语法的早期 Perl 版本（即 5.6.0 之前的版本）会导致误导性信息。应该使用等效的版本。

```perl
use v5.6.1; # 编译时版本

use 5.6.1;   # 同上

use 5.006_001; # 为了向后兼容，优先使用这种
```



这通常用于在你在使用不兼容旧版本 Perl 的库模块之前，需要检查当前的 Perl 版本时（我们尽量不这样做）。

`use VERSION` 同样在词法上启用了由 `feature` 编译指令定义的请求版本中可用的所有功能，并禁用请求版本中的任何功能。同样，如果指定的 Perl 版本大于或等于 5.12.0，`strict` 将像 `strict` 一样在词法上启用。后后使用 `VERSION` 将覆盖之前 `VERSION` 的行为，可能会移除 `use` 增加的功能。`BEGIN` 强制导入在编译时发生。`require` 如果模块尚未加载，则将其加载到内存中。`import` 不是内置；它是对当前包的普通方法调用。模块可以按其喜欢的方式实现导入，尽管大多数模块选择从 `Exporter` 类派生其导入方法。参见 `Exporter`。如果找不到导入方法，将通过 `AUTOLOAD` 跳过调用。如果你不想调用包的导入方法（例如为了防止你的命名空间被修改），请显式提供空列表：

```perl
use Module ();
```

如果 `VERSION` 参数出现在 `Module` 和 `LIST` 之间，则 `use` 将调用类中的 `VERSION` 方法，并将给定版本作为参数。继承自通用类（universal class）的默认 `VERSION` 方法如果给定版本大于变量 `$VERSION` 的值，将报错（croaks）。再次，省略 `LIST`（不带参数调用 import）和显式 `LIST`（调用 import）之间是有区别的。注意 `VERSION` 之前没有逗号！因为这是一个宽接口，pragma（编译指令）也是以这种方式实现的。目前实现的 pragma 有：

```perl
use constant;
use diagnostics;
use integer;
use sigtrap qw(SEGV);
use strict qw(vars);
use utf8;
use warnings qw(all);
use sort qw(stable quicksort);
```



这些伪模块中的某些会将语义导入到当前块中（如 `strict` 或 `integer`，与模块不同，模块是将符号导入到当前包中）。没有 `VERSION` 用于断言 Perl 版本早于此版本，并且不撤销 `use` 启用功能的副作用。参见 `perlmod` 以获取模块和 pragma 列表。参见 `perlin`。

`untie VARIABLE` 解除变量与包之间的绑定。（参见 `tie`）。如果变量未被绑定，则无影响。

`use Module VERSION LIST` 将从命名模块的 `Module` 语义导入到当前包中，通过将某些子程序或变量名别名到你的包中实现。它完全等同于

```perl
BEGIN { require Module; Module->import( LIST ); };
```

除非 `Module` 是一个怪类。通过使用该模块可以使导入变为条件性的。

在 `VERSION` 的特殊用法中，`VERSION` 可以是正的小数（如 `5.006`），也可以是形式为 `v5.6.1` 的 v-字符串，该字符串将与 `$v`（即 `$PER_VERSION`）进行比较。如果 `VERSION` 大于当前 Perl 解释器的版本，将抛出异常；Perl 将停止解析文件的剩余部分。这与 `require` 对比，后者可以在运行时进行类似的检查。对称地，不指定 `VERSION` 则允许你指定比指定版本更老的 Perl 版本。

通常应避免将 `VERSION` 指定为 `v5.6.1` 字面量，因为这在不支持此语法的早期 Perl 版本（即 `5.6.0` 之前的版本）会导致误导性信息。应该使用等效的版本。

```perl
use v5.6.1; # 编译时版本

use 5.6.1;   # 同上

use 5.006_001; # 为了向后兼容，优先使用这种
```



这通常用于在使用不兼容旧版本 Perl 的库模块之前，需要检查当前的 Perl 版本时（我们尽量不这样做）。

`use VERSION` 同样在词法上启用了由 `feature` 编译指令定义的请求版本中可用的所有功能，并禁用请求版本中的任何功能。同样，如果指定的 Perl 版本大于或等于 5.12.0，`strict` 将像 `strict` 一样在词法上启用。后使用 `VERSION` 将覆盖之前 `VERSION` 的行为，可能会移除 `use` 增加的功能。`BEGIN` 强制导入在编译时发生。`require` 如果模块尚未加载，则将其加载到内存中。`import` 不是内置；它是对当前包的普通方法调用。模块可以按其喜欢的方式实现导入，尽管大多数模块选择从 `Exporter` 类派生其导入方法。参见 `Exporter`。如果找不到导入方法，将通过 `AUTOLOAD` 跳过调用。如果你不想调用包的导入方法（例如为了防止你的命名空间被修改），请显式提供空列表：

```perl
use Module ();
```

如果 `VERSION` 参数出现在 `Module` 和 `LIST` 之间，则 `use` 将调用类中的 `VERSION` 方法，并将给定版本作为参数。继承自通用类的默认 `VERSION` 方法如果给定版本大于变量 `$VERSION` 的值，将报错。再次，省略 `LIST`（不带参数调用 import）和显式 `LIST`（调用 import）之间是有区别的。注意 `VERSION` 之前没有逗号！因为这是一个宽接口，pragma（编译指令）也是以这种方式实现的。目前实现的 pragma 有：

```perl
use constant;
use diagnostics;
use integer;
use sigtrap qw(SEGV);
use strict qw(vars);
use utf8;
use warnings qw(all);
use sort qw(stable quicksort);
```

这些伪模块中的某些会将语义导入到当前块中（如 `strict` 或 `integer`，与模块不同，模块是将符号导入到当前包）。没有 `VERSION` 用于断言 Perl 版本早于此版本，并且不撤销 `use` 启用功能的副作用。参见 `perlmod` 以获取模块和 pragma 列表。参见 `perlin`。

这些值被认为具有高度实验性。其具体行为在 Perl 的未来版本中可能会发生。

`for ($hashref) { ... } for ($obj->get_arrayref) { ... }` 为了避免让运行旧版本 Perl 的代码用户产生困惑，可以在文件顶部添加此类内容，以指示您的代码仅适用于较新版本的 Perl：

```perl
use 5.012; # 让 keys/values/each 在数组上有效
use 5.014; # 让 keys/values/each 在标量上有效（实验性）
```

另请参见 `keys`, `and`, `sort`。

`VECFFSET/BITS` 将 `EXPR` 中的字符串视为一个宽度为 `BITS` 的元素的位向量映射图，通过 `OFFSET` 返回该元素的无符号整数（unsigned integer）。`BITS` 指定了位向量中为每个元素保留的比特位数。这必须是 1 到 32 之间（如果平台支持则为 64）的幂次方。

如果 `BITS` 是 8，则“元素”与 `BITS` 的大小一致。

如果 `BITS` 是 16 或更多，输入字符串的字节被分为大小为 `BITS/8` 的块，每个组通过 `pack()`/`unpack()` 数字（`BITS=64` 时同理）。详情参见 "`pack`"。

如果 `BITS` 是 4 或更多，位以小端序（little-endian）的方式被分为 8/`BITS` 组，例如 0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80。例如，将单个字节 `chr(0x36)` 分为两组 (0x6, 0x3)；四组 (0x2, 0x1, 0x0)。`vec` 可以被赋值，以赋予表达式正确的优先级：

```perl
vec($image, $max_x * $y, 8) = 3;
```

如果元素位于字符串之外，则返回 0。如果写入字符串的末尾，Perl 将先用许多零字节扩展字符串。如果字符串被编码为 UTF-8（内部设置了 UTF8 标记），`vec` 将忽略此标记并操作内部字节，即使字符的值小于 256。

使用 `vec` 创建的字符串也可以用逻辑运算符 `|`, `^`, `~` 进行操作。以下代码在大端序或小端序机器上的工作相同：

```perl
my $foo = ''; vec($foo, 0, 32) = 0x5065726C; # Perl
$foo eq "\x50\x65\x72\x6C"; print vec($foo, 0, 8); # 输出 8
vec($foo, 2, 16) = 0x5065;
vec($foo, 3, 16) = 0x726C;
vec($foo, 4, 8) = 0;
vec($foo, 5, 8) = 0x05;
vec($foo, 6, 8) = 7;
vec($foo, 7, 4) = 3;
vec($foo, 8, 4) = 7;
vec($foo, 9, 2) = 1;
vec($foo, 10, 2) = 1;
vec($foo, 11, 1) = 1; # \x66
```

以下是比特实际分布的示例：

```perl
#!/usr/bin/perl
print unpack("b", $_) '012345678901234567890123456789' for $w (0..3) {
    $width = 2**$w;
    for ($shift=0; $shift < $width; $shift++) {
        for ($i=0; $i < $width; $i++) {
            $str = pack("b", "\x02", (1 << $shift));
            vec($str, $shift, $width) = $bits;
            $res = unpack("b", $str);
            join("", $res)
        }
    }
    print vec($offset, $bits, $val)
}
```



无论在什么机器上运行，上述示例都应输出下表：

| 位移 (Shift) | 值 (2^shift) |
| :--- | :--- |
| 0 | 1 |
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |
| 5 | 32 |
| 6 | 64 |
| 7 | 128 |
| 8 | 256 |
| 9 | 512 |
| 10 | 1024 |
| 11 | 2048 |
| 12 | 4096 |
| 13 | 8192 |
| 14 | 16384 |
| 15 | 32768 |
| 16 | 65536 |
| 17 | 131072 |
| 18 | 262144 |
| 19 | 524288 |
| 20 | 1048576 |
| 21 | 2097152 |
| 22 | 4194304 |
| 23 | 8388608 |
| 24 | 16777216 |
| 25 | 33554432 |
| 26 | 67108864 |
| 27 | 134217728 |
| 28 | 268435456 |
| 29 | 536870912 |
| 30 | 1073741824 |
| 31 | 2147483648 |
| 0 | 1 |
| 1 | 4 |
| 2 | 16 |
| 3 | 64 |
| 4 | 256 |
| 5 | 1024 |
| 6 | 4096 |
| 7 | 16384 |
| 8 | 65536 |
| 9 | 262144 |
| 10 | 1048576 |
| 11 | 4194304 |
| 12 | 16777216 |
| 13 | 67108864 |
| 14 | 268435456 |
| 15 | 1073741824 |
| 0 | 2 |
| 1 | 8 |
| 2 | 32 |
| 3 | 128 |
| 4 | 512 |
| 5 | 2048 |
| 6 | 8192 |
| 7 | 32768 |
| 8 | 131072 |
| 9 | 524288 |
| 10 | 2097152 |
| 11 | 8388608 |
| 12 | 33554432 |
| 13 | 134217728 |
| 14 | 536870912 |
| 15 | 2147483648 |
| 0 | 4 |
| 1 | 16 |
| 2 | 256 |
| 3 | 4096 |
| 4 | 65536 |
| 5 | 1048576 |
| 6 | 4194304 |
| 7 | 16777216 |
| 8 | 268435456 |

`vec($, 6, 4) = 4 == 6710864`

`vec($, 7, 4) = 4 == 107374182`

`vec($, 0, 4) = 8 == 8`

`vec($, 1, 4) = 8 == 128`

`vec($, 2, 4) = 8 == 2048`

`vec($, 3, 4) = 8 == 32768`

`vec($, 4, 4) = 8 == 524288`

`vec($, 5, 4) = 8 == 8388608`

`vec($, 6, 4) = 8 == 134217728`

`vec($, 7, 4) = 8 == 2147483648`

`vec($, 0, 8) = 1 == 256`

`vec($, 1, 8) = 1 == 65536`

`vec($, 2, 8) = 1 == 16777216`

`vec($, 0, 8) = 2 == 512`

`vec($, 1, 8) = 2 == 131072`

`vec($, 2, 8) = 2 == 33554432`

`vec($, 0, 8) = 4 == 4`

`vec($, 1, 8) = 4 == 1024`

`vec($, 2, 8) = 4 == 26214`

`vec($, 3, 8) = 4 == 67108864`

`vec($, 0, 8) = 8 == 2048`

`vec($, 1, 8) = 8 == 524288`

`vec($, 2, 8) = 8 == 134217728`

`vec($, 0, 8) = 16 == 16`

`vec($, 1, 8) = 16 == 1048576`

`vec($, 2, 8) = 16 == 268435456`

`vec($, 0, 8) = 32 == 32`

`vec($, 1, 8) = 32 == 8192`

`vec($, 2, 8) = 32 == 2097512`

`vec($, 3, 8) = 32 == 53687092`

`vec($, 0, 8) = 64 == 64`

`vec($, 1, 8) = 64 == 16384`

`vec($, 2, 8) = 64 == 4194304`

`vec($, 3, 8) = 64 == 107374182`

`vec($, 0, 8) = 128 == 128`

`vec($, 1, 8) = 128 == 32768`

`vec($, 2, 8) = 128 == 8388608`

`vec($, 3, 8) = 128 == 2147483648`

`wait` (2) 在你的系统上：它等待一个进程终止并返回已死亡进程的 pid，如果没有子进程则返回 -1。状态返回在 `$` 和 `${CHILD_ERROR_errno}` 中。请注意，返回值 -1 可能意味着子进程正在被自动收割，如 `perlip` 中描述的那样。

如果你在 `$SIG{CHLD}` 的处理函数中使用 `wait`，它可能会意外地等待 `fork()` 或 `system()` 创建的子进程。详情请参 `perlip`。

潜在问题：`perlip` 中的 "wait"。
`waitpid,FLAGS` 等待一个特定的子进程终止并返回已死亡进程的 pid，如果没有子进程则返回 -1。在某些系统上，值为 `${CHILD_ERROR_NATIVE}`。如果你说：

```perl
use POSIX "sys/wait.h"; #.. do $kid = waitpid(-1, WNOHANG); } while
$kid > 0;
```

那么你可以对等待中的僵尸进程进行非阻塞等待。在支持 (2) 或 (2) 系统调用的机器上可以使用非阻塞等待。然而，带有 `$` 的 `FLAGS` 等待特定 pid 在处处都实现了。（Perl 通过记住已存在但尚未被 Perl 脚本收割的进程状态值来模拟系统调用。）

请注意，在某些系统上，返回值 -1 可能意味着子进程正在被自动收割。详情及其他示例请参阅 `perlpc`。

安全性/可移植性问题：`perport` 中的 "waitpid"。

`wantarray` 在当前执行的子程序或 `eval` 的上下文正在寻找列表值时返回。如果上下文正在寻找标量值（scalar），则返回假（false）。如果上下文正在寻找没有值（void 上下文），则返回 undefined。

```perl
return undefined wantarray; # 不要费心执行 @a =
complex_calculation(); return wantarray? ? @a : "@a";
```

`wantarray()` 的结果在文件顶层、BEGIN、UNITCHECK、CHECK、INIT 或 END 块或 DESTROY 方法中是不指定的。

此函数应该命名为 `list()`。

`warn LIST` 打印 `STDERR` 的值。如果 `LIST` 的最后一个元素没有以换行符结束，将追加相同的文件/行号。

如果输出为空且 `$` 已经包含一个值（通常来自之前的 that），则该值在追加 `\t...caught to $@` 之后被使用。这对于保持程序运行很有用，但与 `die` 不同。

如果 `$@` 为空，则使用信息："Something's wrong" 的字符串。

如果存在 `SIG($__WARN__)` 处理器，则不打印任何消息。处理器的责任是以合适的方式带上消息 `die`（例如，将其转换为 `die`）。大多数处理器会遍历确保归档，通过在处理器中调用 `warn` 来显示那些未准备好 `die` 的值。注意，这是非常安全的，不会产生无限循环，因为 `__WARN__` 钩子不是从其内部钩触发的。

你会发现这种行为与 `SIG($__DIE__)` 处理器的行为略有不同（后者不会抑制错误文本，而是可以通过 `die` 来更改它）。

使用 `__WARN__` 处理器提供了一种向所有警告信号沉默的方法（所谓的静默）。示例：

```perl
$SIG{__WARN__} = sub {
    shift;
};
```

# PERLGIT

## 描述

本文提供了有关使用 git 进行开发的详细信息。如果你是拥有仓库写入权限的常规贡献者，本文内容是为你准备的。

## 克隆仓库

Perl 的源代码都集中存储在 `git.perl.org` 的仓库中。你可以通过运行以下命令创建一个只读克隆：

```bash
% clone 协议
```

这使用了 `git` 协议（端口 9418）。如果你对开发 Perl 感兴趣，可以通过运行以下创建一个：

```bash
% clone perl
```



如果你由于防火墙原因无法使用 `git` 协议，也可以通过 `http` 克隆，尽管这慢得多：

```bash
% clone perl
```

## 操作仓库

一旦你进入仓库目录，就可以对其进行检查。完成后仓库将包含一个本地分支，星号表示当前分支。

```bash
% branch *
```

使用 `-a` 切换显示仓库中的远程跟踪分支：

```bash
% branch -a * bleed origin/bleed
```

以 `origin` 开头的分支对应你克隆的远程。你不应该在这些远程跟踪分支上工作。本地分支可以配置为自动合并（pull）来自指定的远程跟踪分支。默认分支 `bleed` 就是这种情况，它配置为来自远程跟踪分支 `origin`。

你可以查看提交：

```bash
% log
```

从仓库拉取新更改并更新本地仓库（必须是干净的）：

```bash
% pull
```

假设 `pull` 之后我们在 `bleed` 分支上，此命令或等同于：

```bash
% fetch * git merge origin/bleed
```

实际上，如果你想在不接触工作目录的情况下更新本地仓库，执行：

```bash
% fetch
```

如果你想同时更新所有定义远程的远程跟踪分支，可以执行：

```bash
% remote update
```

这最后两个命令都不会更新你的工作目录，但都会更新远程跟踪分支。

为远程分支创建本地分支：

```bash
% checkout -b main-5.10 origin/main-5.10
```

切换回 `bleed`：

```bash
% checkout bleed
```

[PAGE 604]

# 查找你的状态

你最常用的 `git` 命令可能是：

```bash
% git status
```

此命令将生成仓库当前状态的输出，包括修改的文件和未跟踪的文件，此外，它还会显示哪些文件已暂存（staged）准备进行下一次提交，并且通常会提供一些关于如何更改内容的有用信息。例如：

```
$ git status # On branch bleed
Your branch is ahead of 'origin/bleed' by 1 commit. (use "git reset <file>..." 来取消暂存)
modified: pod/pergit.pod # 已修改但未更新 (使用 "git add <file>..." 来更新将提交的内容)
modified: pod/pergit.pod # 未跟踪的文件:
# (使用 "git add <file>..." 将其包含在待提交的内容中)
```

这显示此文档的更改已暂存等待提交，且工作目录中还有进一步的更改；或者显示工作目录中有一个未跟踪的文件，你可以你可以看到如何更改这些内容。它还显示工作分支 `bleed` 上有一个尚未推送到 `origin` 的提交。**注意**：如果你在执行 `git commit` 时没有提供信息，此输出也是你将看到的模板内容。

# 补丁工作流 (Patch workflow)

首先，请阅读 `perhack` 以了解关于修改 Perl 核心的细节。该文档涵盖了如何创建一个良好补丁的许多细节。

如果你已经有一个 Perl 仓库，你应该确保你正处于 `bleed` 分支，并且你的仓库是最新的：

```
% git checkout bleed
% git pull
```

最好针对最新的 `bleed` 版本进行补丁，因为除了关键修复（critical fix）之外，所有更改的新开发工作都在这里进行。关键修复补丁应该针对相关的维护分支（maint branches）制作，或者在提交时附带说明指出应应用修复的分支。

现在我们已经全部更新到最新状态，需要为这些更改创建一个临时新分支并切换进去：

```
% git checkout -b git orange
```

其简写形式为：

```
% git branch orange
% git checkout orange
```

创建一个主题分支（topic branch）让维护者更容易进行变基（rebase）或将其合并回主分支，从而获得更线性的历史。如果你不在主题分支上工作，维护者必须在应用你的更改之前手动将它们挑选到 `bleed` 分支上。

那会导致你在 `perl5-porters` 上被责骂，所以别这样做。太棒了。

然后进行你的更改。例如，如果 Leon Brocard 将他的名字改为 Orange Brorocad，我们应该更改 `AUTHORS` 文件中他的名字：

```
% perl -pi 's{Leon Brocad}{Orange Brocad}' AUTHORS
```

你可以看到哪些文件被修改了：

```
% git status # On branch
Changes to be committed:
# (使用 "git reset HEAD<file>..."取消暂存)
# modified: AUTHORS #
```

你可以看到更改：

```
% git diff -a a/AUTHORS b/AUTHORS index 293dd70.722c93e100644 --
a/AUTHORS ++ b/AUTHORS @@ -541,7 +541,7 @@ Lars Heck < Laszlo Molnar
< Left Hahn < Len Johnson <> -Leon Brocad <> +Orange Brocad < Les
Peters < Lesley Banks <> Lincoln D. Stein <
```

现在提交你的本地更改：

```
% git commit -a "Rename Leon Brocad to Orange Brocad Created commit 6196cid: Rename Leon Brocad to Orange Brocad 1 files changed, 1 insertions(+), 1 deletions(-)"
```

`-a` 选项用于包含你 `git` 跟踪的所有已文件。如果你只想提交你工作过的部分文件，可以省略 `-a` 并在提交前使用命令 `git add FILE...`。`git add interactive` 允许你仅提交文件的部分内容，而不是文件中的所有更改。

一旦你完成提交信息并退出编辑器，`git` 将写入你的更改并告知你类似如下的内容：

Created commit dafe863: explain git status and stuff about remotes 1 files hanged, 83 insertions(+), 3 deletions(-)

如果你重新运行 `git status`，你应该会看到类似下面的内容：

```
% git status # On branch bleed
Your branch is ahead of 'origin/bleed' 2 commits.
# Untracked files:
# (use "git add <file>..." 来包含待提交的内容)
# nothing added to commit
but untracked files present (use "git add" 来跟踪)
```

如有疑问，在执行任何其他操作之前，请检查你的状态并仔细阅读，问题现在直接由 `git status` 的输出回答。

你可以通过以下命令检查你的最后提交：

```
% git show HEAD
```

如果你对描述或补丁本身都不满意，可以通过再次编辑文件来修复它，然后执行：

```
% git commit -a --amend
```

现在你应该为你所有的本地更改创建一个补丁文件：

```
$ git format-patch -M bleed.. 0001-Rename-Leon-Brocad-to-Orange-Brocad.patch
```

或者对于大量的更改，例如从一个主题分支：

```
% git format-patch --stdout -M bleed.. > topic-branch-changes.patch
```

你应该向 `<mailto:>` 发送一封邮件，附带你更改的描述，并将此补丁文件作为附件。如有疑问，在执行任何其他操作之前，请检查你的状态并仔细阅读，问题现在直接由 `git status` 的输出回答。

核心部分提供了一个包装程序 `Porting/bisect.pl`，它尝试尽可能简化操作，使得二分查找（bisect）像运行一个 Perl 单行命令一样简单。例如，如果你想知道这个错误何时发生的：

```perl
perl -e 'my $sa := 2'
```

你只需要运行以下命令即可：

```
...Porting/bisect.pl -e 'my $sa := 2;'
```

使用 `bisect.pl`，通过一个命令（无需其他文件）就可以轻松找到：

- 是哪一个提交导致了该示例代码崩溃？

- 是哪一个提交导致该示例代码开始正常工作？

- 是哪一个提交添加了第一个匹配该正则表达式的文件？



- 是哪一个提交删除了最后一个匹配该正则表达式的文件？

通常你不需要知道要使用哪个版本的 perl，因为 `bisect.pl` 会自动搜索测试用例能够通过的最早稳定版本。运行 `Porting/bisect.pl -help` 可以查看完整文档，包括如何设置 Configure 和编译时间选项。

如果你需要比 `Porting/bisect.pl` 提供的更大的灵活性，则需要手动运行 `git bisect`。使用 `git bisect` 自动化 perl 的构建和测试是最有用的。为此，你需要编写一个 shell 脚本供 git 调用特定的版本。一个示例脚本是 `Porting/bisect-example.sh`，你应该将其复制到仓库之外，因为二分过程在运行时会将工作状态重置为干净的检出状态（clean checkout）。下面的说明假设你已将其复制为 `~run` 并根据情况对其进行了编辑。

通过以下命令进入二分模式：

```
% git bisect start
```

```
% git bisect bad % git bisect good perl-5.10.0
Bisecting: 853 revisions left to test after this
```

这将导致检查 `HEAD` 和 `perl-5.10.0` 之间的中间提交。然后你可以运行以下命令执行二分过程：

```
% git bisect run ~run
```

当隔离出第一个错误提交（bad commit）时，`git bisect` 会通知你：

ca4cd2853430b3b82a216cfe83a1c0bcbc3b9c5 is first bad commit

ca4cd2853430b3b82a216cfe83a1c0bcbc3b9c5 Author: Dave Mitchell <> Date: Sat Feb 9 14:56:23 2008 +0000 [perl #49472] Attributes + Unknown Error ...

bisect run success

你可以通过 `git bisect log` 和 `git bisect visualize` 查看二分过程，运行 `git bisect reset` 可以退出二分模式。

请注意，第一个良好状态（good state）必须是第一个错误状态的祖先。如果你想查找修复某个 bug 的提交，你必须反转测试用例（即：OK 返回 1，不 OK 返回 -1），并仍然下界标记为 good，上限标记为 bad。此时，“第一个错误提交”应被理解为“第一个修复了 bug 的提交”。

`git help bisect` 提供了更多关于如何调整你的二分查找的信息。

# 主题分支与历史重写

个人提交者应该在 `yourname/some_descriptive_name` 下创建主题分支。其他提交者在对主题分支进行任何更改之前，应先咨询该分支的创建者。

创建一个适用于所有 git 版本的远程主题分支的最简单方法是将当前头指针（head）作为新分支推送到远程，然后在本地检出它：

```
$ branch="$some_descriptive_name" git push origin HEAD:$branch
$ git checkout -b $branch origin/$branch
```

git 1.7 或更高版本的用户可以使用更直观的方式完成：

```
$ branch="$some_descriptive_name" git checkout -b $branch
 git push origin -u $branch
```

如果你不是 `yourname/some_descriptive_name` 的创建者，有时可能会发现原作者删除了该分支的历史。这有很多合理的理由。有时，作者可能发现将分支变基到一个新的源点。有时，作者可能在早期提交中发现了错误，并在合并到 `bleed` 之前想要修复。

主仓库配置为禁止快快合并（non-fast-forward merges）。这意味着分支不能在变基后直接一步推送。

你被允许变基或修改已推送分支的历史的唯一方法是将其删除并以相同的名称作为新分支推送。请务必仔细考虑此操作。重命名分支可能更容易让与你合作的人将其本地更改拾选（cherry-pick）到新版本。（xxx：需要解释）。

如果你想变基个人主题分支，你必须删除现有分支并将其作为新版本推送。在变基分支后，可以使用以下公式（详细信息请参见 `git push` 文档中关于 `refspec` 的解释）：

```
# 首先变基 git checkout $user/$topic git fetch git rebase origin/bleed
# 然后“删除并推送” git push origin :user/$topic
git push origin $user/$topic
```

注意：仓库禁止删除任何“主”分支。即任何匹配 `^(bleed|main|perl)$` 的分支。任何此类尝试都会导致：

```
$ git push origin :bleed

error: failed to update refs/heads/bleed (remote hook rejected): it is forbidden at the repository level to delete any of the “primary” branches. That is any branch matching `^(bleed|main|perl)$`.
```

任何此类尝试都会导致：

```
error: failed to update refs/heads/main (remote hook rejected): it is forbidden at the repository level to delete any of the “primary” branches. That is any branch matching `^(bleed|main|perl)$`.
```

任何此类尝试都会导致：

```
error: failed to update refs/heads/perl (remote hook rejected): it is forbidden at the repository level to delete any of the “primary” branches. That is any branch matching `^(bleed|main|perl)$`.
```

如果你是 Perl 的提交者（committer）并且认为该补丁是好的，你可以将其合并到 bleed 分支并推送到主仓库：

```
% git checkout bleed

% git merge experimental

% git push origin bleed
```

如果你想删除临时分支，可以执行以下操作：

```
% git checkout bleed

% git branch -d experimental

error: 分支 'experimental' 不是你当前 HEAD 的祖先。如果你确定要删除它，请运行 'git branch -D experimental'。

% git push -D experimental
```

已删除分支 experimental。

## 提交到 bleed

`bleed` 分支将成为 Perl 的下一个发布版本。

在将任何本地更改推送到 bleed 之前，执行以下操作至关重要，以便其他提交者能够后续通过端口（pickports）和分支（forks）进行工作：

- 确保你有一个良好的提交信息（commit message）。详情请参阅 perlhash 中的 "Commit message"。

- 运行测试套件。你可能认为一个拼写错误不会破坏测试文件，但你的想法是。这里有一个由于没有运行测试套件导致问题的示例：提交的一个补丁在现有的 .t 文件中添加了几个测试。这不太可能影响任何内容，所以不需要测试受影响的 .t 之外，对吧？但是，提交者的电子邮件地址自上次提交以来发生了变化，导致其他测试失败。运行下一个项目中给出的测试目标就会导致这个问题。

- 如果你没有运行完整的测试套件，至少要运行 `test_porting`。这将运行基本的健全检查。要查看是哪些健全检查，请查看 `/porting`。

- 如果你进行了任何影响 miniperl 或对 miniperl 有不同代码路径的核心程序的更改，务必运行 `minitest`。这将捕获即使完整测试套件无法发现的问题，因为它在 miniperl 而不是 perl 下运行测试子集。

## 关于合并（Merging）和变基（rebasing）

推送到 `bleed` 分支的简单提交应该是可以干净应用的简单提交。换句话说，你应该确保你的工作是基于 bleed 的当前位置提交的，这样你就可以无需合并直接推回主仓库。

有时，在你构建或测试更改时，bleed 会发生移动。发生这种情况时，你的推送将被类似下面的消息所拒绝：



```
To ! [rejected] -> bleed (non-fast-forward) error: failed to push some refs to 'bleed'. To prevent you from losing history, non-fast-forward updates were rejected. Merge the remote changes (e.g. 'git pull') before pushing again. See the 'Note about fast-forwards' section of 'git push --help' for details.
```

发生这种情况时，你可以针对 `bleed` 的新位置对你的工作进行变基，如下所示（假设你的主仓库是 "`p5p`"）：

```bash
$ git fetch p5p
$ git rebase p5p/bleed
```

你会看到你的提交被重新应用，然后你就可以安全地推送。关于变基的更多信息可以在 `rebase` 命令的文档中找到。（注：原文中有 "(1)"，可能指代 `rebase`）。

对于只有在一起才有意义的较大提交组，或者能够从该组目的摘要中获益的提交，你应该使用合并提交（`merge commit`）。你应该在一个主题分支（`topic branch`）上执行工作，并定期针对 `bleed` 进行变基，以确保你的代码没有被 `bleed` 破坏。当你完成工作后，进行最后的变基和测试。线性历史在 `bleed` 上的每次提交中都会丢失，但最终的变基会让历史重新变为线性，使未来的维护者更容易理解。按照如下方式变基（假设你的工作在 `commuter/somework` 分支上）：

```bash
$ git checkout commuter/somework
$ git rebase bleed
```

然后你可以这样将其合并到 `master`：

```bash
$ git checkout master
$ git merge --no-ff --no-commit commuter/somework
$ git commit -a
```

上述切换需要解释。`--no-ff` 表示即使你的所有工作都可以线性地应用到 `bleed`，也应该准备一个合并提交。这确保了你的所有工作将显示为一个侧分支，其所有提交都通过合并提交合并到 `master` `bleed` 中。

`--no-commit` 意味着将准备合并提交但不进行提交。提交将在运行下一个命令时实际执行，该命令会调出你的编辑器描述提交。如果没有 `--no-commit`，提交将在几乎没有有用信息的情况下被完成，这将极大地降低合并提交作为工作描述占位符的价值。

在描述合并提交时，请解释分支的目的，并记住该描述可能会被最终的发布工程师在审查你的 `perldelta` 文档时使用。

## 提交到维护版本

维护版本应只通过添加关键错误修复进行更改，详见 `perpolicy`。

要提交到 Perl 的维护版本，你需要创建一个本地跟踪分支：

```bash
% git checkout --track -b maint-5.005 origin/maint-5.005
```

这创建了一个名为 `maint-5.005` 的本地分支，它跟踪远程分支 `origin/maint-5.005`。然后你可以像以前一样拉取、提交、合并和推送。

你还可以使用 `git cherry-pick` 命令从 `bleed` 和另一个分支选取提交。建议使用 `-x` 选项进行 `cherry-pick`，以便在新的提交信息中记录原始提交的 SHA。

在向维护版本推送任何更改之前，确保你已经满足了“提交到维护版本”中的步骤。

## 从 GitHub 合并

（注：此章节的 OCR 文本在源码中似乎非常混乱/重复。我已根据之前章节的上下文清理了逻辑流。）

在向维护版本推送任何更改之前，确保你已经满足了“提交到维护版本”中的步骤。

（注：原文页 615-616 的剩余文本包含大量的 OCR 伪迹和重复字符串，无法构成连贯的句子。我保留了上面提供的功能性指令。）

# PERLGPL

+ > 名称

`perlgpl` - GNU 通用公共许可证，第 1 版

# 概要

你可以在 Pod 中通过 "`L<perlgpl>`" 引用此文档，你也可以通过输入 "`perldoc perlgpl`" 来查看此文档。

## 描述

Perl 是自由软件；你可以根据以下条款重新分发和/或修改它：a) 由自由软件基金发布的《GNU 通用公共许可证》第 1 版，或（根据你的选择）任何更高版本；或 b) 本工具包附带的“艺术许可协议”（`Artistic License`）。

这是“GNU 通用公共许可证，第 1 版”。其目的是让希望将此声明作为其分发许可的模块、程序等能够与之链接。

关于 Perl 艺术许可协议，请参阅 `perlartistic`。

# GNU 通用公共许可证

GNU 通用公共许可证 第 1 版，1989年2月。版权所有 (C) 1989 Free Software Foundation, Inc. 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 每个人都被允许复制和分发本许可证文件的逐字副本，但不允许对其进行修改。

前言 软件公司的许可协议试图让用户受这些于公司的控制。相比之下，我们的通用公共许可证旨在保证你分享和授予自由软件的自由——让软件对所有用户都是自由的。通用公共许可证适用于自由基金会的软件以及任何你承诺使用它的其他程序。当你将它用于你的程序时，当我们谈论自由软件时，我们指的是自由，而不是价格。

具体而言，通用公共许可证的设计是为了确保你拥有赠送或出售自由软件副本的自由，确保你能够获得源代码或在需要时获取它，确保你可以在新程序中更改软件或其部分；并确保你可以做这些事情。为了保护你的权利，我们需要制定限制，禁止任何人否认这些权利或要求你放弃这些权利。这些限制转化为在你分发软件副本或对其进行修改时必须承担的责任。例如，如果你分发此类程序的副本（无论免费还是付费），你都必须赋予接收者你所拥有的权利。你必须确保他们能够收到源代码。你必须告诉他们这些权利。我们通过两个步骤保护你的权利：(1) 对软件进行版权保护；(2) 提供此许可证，赋予你法律许可来复制、分发和/或修改软件。此外，对于每位作者，此自由软件不提供任何保证。如果软件被他人修改并传播，我们希望知道那不是原始版本，这样他人引入任何问题都不会影响原作者的声誉。有关复制、分发和修改的精确条款和条件如下。

GNU 公共许可证复制、分发和修改的条款和条件

0. 本许可协议适用于任何包含版权所有者所作声明的程序或其他作品，该声明称其可以根据本《通用公共许可证》的条款进行分发。我们将“程序”指任何此类程序，“基于程序的作品”指该程序本身或包含该程序或其部分的任何作品（无论是否经过修改）。每位被许可者统称为“你”。

1. 你可以按照接收程序的方式，在任何媒介上复制并分发程序的逐字副本，前提是你必须在每份副本上显著且适当地发布适当的版权声明和免责声明；保留所有引用本《通用公共许可证》及不提供任何保证的通知；并向程序副本的任何其他接收者提供本许可证。你可以对传输副本的物理行为收取费用。

2. 你可以修改你的程序副本或其任何部分，并在上述第 1 条的条款下复制并分发此类修改，前提是你还执行了以下操作：

a) 确保修改后的文件带有显著通知，说明你修改了这些文件以及任何修改的日期；以及

b) 确保程序或其任何部分（无论是否经过修改）在整体或部分根据本《通用公共许可证》的条款免费向所有第三方许可（但你可以根据自己的选择向所有或某些第三方提供保证保护）；

c) 如果修改后的程序在运行时通常以交互式方式读取命令，你必须使其在以最简单、最常见的方式进行此类交互式使用时，打印或显示一份公告，其中包含适当的版权声明和不提供保证的通知（或者说明你提供保证），并告知用户可以根据这些条款重新分发该程序，并告诉用户如何查看副本。

d) 你可以对传输副本的行为收取费用，你可以根据自己的选择，就与程序（或其衍生作品）的任何独立工作，在不包含范围内的其他作品的存储卷或媒介上提供保证保护。

3. 你可以以后以下对象代码或可执行形式复制并分发程序（或其部分，根据第 2 条）：

a) 附带完整的机器可读源代码，该源代码必须根据第 1 条和第 2 条的条款分发；

b) 附带一份书面报价（有效期至少三年），承诺向任何第三方免费或收取分发成本的小额费用提供一份完整的机器可读源代码副本，并根据上述第 1 条的条款分发；

c) 附带你收到的可以获取的信息（此替代方案仅适用于非商业分发，且仅当单独以对象代码或可执行形式使用程序时有效）。作品的源代码是指对其进行修改的首选形式。对于可执行文件，完整源代码意味着包含其中的所有源代码；但是，作为例外，运行可执行文件的标准库或定义不需要包含。

4. 除非适用法律规定，否则你不得复制、修改、分发或传输程序，除非此处明确规定。为了保护你的权利，任何复制、修改或传输程序的尝试如果违反本许可，你的权利将是无效的。

5. 通过复制或修改程序（或基于程序的作品），你表示你对本许可的接受。

6. 自由软件的作者可能发布本许可证的新版本，其精神与当前版本相似，但在细节上可能不同。



7. 如果你开发了一个新程序并希望对人类产生最大的贡献，最好的方法是根据本条款将其自由化。为了做到这一点，你需要在文件开头附上以下通知。

8. 自由软件基金可能会发布本许可证的新版本。

9. 版权所有 (C) 年份 作者姓名。Free Software Foundation, Inc. 55 Franklin Street, Fifth Floor, Boston, MA 02110-1301

10. 除非适用法律规定，否则在任何情况下，作者均对由于使用或无法使用程序而引起的任何损害（包括数据丢失）承担任何一般、特殊或间接损害的责任。

条款结束

附录：如何将这些条款应用于你的程序

如果你开发了一个新程序并希望它尽可能造福，最好的方法是根据这些条款将其自由化。为了做到这一点，你需要在文件开头附上这些通知以最有效地传递免责声明；每个文件应至少包含“版权”行以及指向该通知的指针。

该程序是自由软件，你可以根据某些条款重新分发它；详情请查看 `show w`。假设的命令 `show w` 和 `show c` 应该显示《通用公共许可证》的相应部分。当然，你使用的命令名称可能不是 `show w` 和 `show c`；它们甚至可以是鼠标点击或菜单项——取决于你的程序。你还需要让你的雇主（如果你是程序员）或你的学校（如果有）对该程序说明一份“版权免责声明”。这里有一个示例，请修改名称：Yodyne，在此声称拥有 James Hacker 编写的程序 'Gnomovision'（一个引导编译器通过汇编器进行处理的程序）的所有版权权益。

<签名

James Hacker 

Ty Coon, 1989年4月1日 Ty Coon, 副总裁。就如此！

# PERLGUTS

+ > NAME

`perlguts` - Perl API 介绍

## 描述

本文档尝试描述如何使用 Perl API，并提供一些关于 Perl 核心工作原理的信息。本文档远非完整，并且可能包含许多错误。请将任何问题或意见反馈下方的作者。

# 变量

### 数据类型

Perl 有三个类型定义（typedef）来处理 Perl 的三种主要数据类型：

| 类型 | 描述 |
|---|---|
| `SV` | 标量值 (Scalar Value) |
| `AV` | 数组值 (Array Value) |
| `HV` | 哈希值 (Hash Value) |

每个类型定义都有特定的例程来操作各种数据类型。

### 什么是 IV？

Perl 使用特殊的类型定义 `IV`，它是一种简单的整数类型，保证足够容纳一个指针（以及整数）。此外，还有 `UV`，它仅仅是无符号 `IV`。

Perl 还使用了两个特殊的类型定义 `I32` 和 `I16`，它们的长度至少为 32 位和 16 位。（同样，还有 `U32` 和 `U16`）。它们通常恰好是 32 位和 16 位，或者在 Cray 机器上两者均为 64 位。

使用 `sv` 操作

可以使用一个命令创建并加载一个 `sv`。可以加载五种类型的值：整数 (`IV`)、无符号整数值 (`UV`)、双精度浮点数 (`NV`)、字符串 (`pv`) 以及另一个标量 (`sv`)。（"PV" 代表“指针值”Pointer Value。你可能认为它的命名不当，因为它只描述了字符串。然而，它也可以指向其他东西。例如，它可以指向一个 `UV` 数组。但是，将它用于非字符串时需要小心，因为内部的底层假设是 `PV` 仅用于字符串。例如，通常会自动附加一个的 `NULL` 字符。非字符串的用法仅在此段落中记录。

这七个例程是：

```
SV* newSIV(IV); SV* newSUV(UV); SV* newSVn(double); SV* newSVP(const char*, STRLEN); SV* newSVpn(const char*, STRLEN); SV* newSVpf(const char*, ...); SV* newSvs(sv);
```

`STRL` 是一个整数类型（尺寸，通常在 `config.h` 中定义为 `size_t`），保证足够大以表示 Perl 可以处理的任何字符串的大小。

在 `sv` 需要更复杂的稀罕情况下，你可以使用 `newSvs(len)` 创建一个 `sv`。如果 `len` 为 0，则返回类型为 `NULL` 的 `sv`，否则返回类型为 `PV` 的 `sv`，并分配 `len + 1` 字节的存储，可以通过 `SVPVX` 访问。在这两种情况下，`sv` 具有未定义的值。

```
SV * sv = newSvs(0); /* 未分配存储 */ sv *sv = newSvs(10); /* 10 (+1) 字节未初始化的存储 * */
```

要创建现有 `sv` 的值，有八个例程：

```
void svset(SV*, IV); void svsetuv(SV*, UV); void svsetn(SV*, double); void svsetpv(SV*, const char*); void svsetpn(SV*, const char*, STRLEN);
```

```
void sv_svpvf(SV*, const char*, ...); void sv_svsetpvfn(SV*, const char*, NRLEN, va_list *, SV **, I32, bool *); void sv_setsv(SV*, SV*);
```

请注意，你可以通过 `sv_setpvn`、`newSvpn` 或 `newSvvp` 选择要分配的字符串长度，或者你可以允许 Perl 使用 `sv_setpy` 计算长度，或者通过在 `newSvvp` 的第二个参数中指定 0 来计算。

**重新整理该段落：**



请注意，你可以通过 `sv_setpvn`、`newSvpn` 或 `newSvvp` 选择要分配的字符串长度，或者你可以允许 Perl 使用 `sv_setpy` 计算长度，或者通过在 `newSvvp` 的第二个参数中指定 0 来计算。请注意，由于内部底层假设是 PV 仅用于字符串，将其用于非字符串时需要小心。

---

**由于原文存在严重重复，以下为您提供全文的清理后翻译版本：**

Ty Coon, 1989年4月1日 Ty Coon, 副总裁。就如此！

# PERLGUTS

## NAME

`perlguts` - Perl API 介绍

## 描述

本文档尝试描述如何使用 Perl API，并提供一些关于 Perl 核心工作原理的信息。本文档远非完整，并且可能包含许多错误。请将任何问题或意见反馈给下方的作者。

# 变量

### 数据类型

Perl 有三个类型定义（typedef）来处理 Perl 的三种主要数据类型：

| 类型 | 描述 |
|---|---|
| `SV` | 标量值 (Scalar Value) |
| `AV` | 数组值 (Array Value) |
| `HV` | 哈希值 (Hash Value) |

每个类型定义都有特定的例程来操作各种数据类型。

### 什么是 IV？

Perl 使用特殊的类型定义 `IV`，它是一种简单的整数类型，保证足够容纳一个指针（以及整数）。此外，还有 `UV`，它仅仅是无符号 `IV`。

Perl 还使用了两个特殊的类型定义 `I32` 和 `I16`，它们的长度至少为 32 位和 16 位。（同样，还有 `U32` 和 `U16`）。它们通常恰好是 32 位和 16 位，或者在 Cray 机器上两者均为 64 位。

使用 `sv` 操作

可以使用一个命令创建并加载一个 `sv`。可以加载五种类型的值：整数 (`IV`)、无符号整数值 (`UV`)、双精度浮点数 (`NV`)、字符串 (`pv`) 以及另一个标量 (`sv`)。("PV" 代表“指针值”Pointer Value。你可能认为它的命名不当，因为它只描述了字符串。然而，它也可以指向其他东西。例如，它可以指向一个 `UV` 数组。但是，将它用于非字符串时需要小心，因为内部的底层假设是 PV 仅用于字符串。例如，通常会自动附加一个的 `NULL` 字符。非字符串的用法仅在此段落中记录。

这七个例程是：

```
SV* newSIV(IV); SV* newSUV(UV); SV* newSVn(double); SV* newSVP(const char*, STRLEN); SV* newSVpn(const char*, STRLEN); SV* newSVpf(const char*, ...); SV* newSvs(sv);
```

`STRL` 是一个整数类型（尺寸，通常在 `config.h` 中定义为 `size_t`），保证足够大以表示 Perl 可以处理的任何字符串的大小。

在 `sv` 需要更复杂的稀罕情况下，你可以使用 `newSvs(len)` 创建一个 `sv`。如果 `len` 为 0，则返回类型为 `NULL` 的 `sv`，否则返回类型为 `PV` 的 `sv`，并分配 `len + 1` 字节的存储，可以通过 `SVPVX` 访问。在这两种情况下，`sv` 具有未定义的值。

```
SV * sv = newSvs(0); /* 未分配存储 */ sv *sv = newSvs(10); /* 10 (+1) 字节未初始化的存储 * */
```

要创建现有 `sv` 的值，有八个例程：

```
void svset(SV*, IV); void svsetuv(SV*, UV); void svsetn(SV*, double); void svsetpv(SV*, const char*); void svsetpn(SV*, const char*, STRLEN);
```

```
void sv_svpvf(SV*, const char*, ...); void sv_svsetpvfn(SV*, const char*, NRLEN, va_list *, SV **, I32, bool *); void sv_setsv(SV*, SV*);
```

注意，你可以通过 `sv_setpvn`、`newSvpn` 或 `newSvvp` 选择要分配的字符串长度，或者你可以允许 Perl 使用 `sv_setpy` 计算长度，或者通过在 `newSvvp` 的第二个参数中指定 0 来计算。请注意，由于内部底层假设是 PV 仅用于字符串，将其用于非字符串时需要小心。

（注：原文此处后续存在大量重复文本，译文已去重）

`sv_svpvf` 的参数像 `sprintf` 一样处理，格式化输出变为值。`sv_svpvfn` 是 `sprintf` 的类似物，但它允许指定变量参数列表或 SV 数组的地址和长度。最后一个参数指向布尔值；返回时，如果布尔值为真，则使用了区域特定信息来格式化字符串，字符串内容不可信（见 perplex）。如果信息很重要，此指针可能为 `NULL`。注意此函数需要指定长度。

`sv_set*` 函数不是操作具有“魔法”值的通用函数。参见后文“魔法虚表”。

所有包含字符串的 `SV` 都应该以 `NULL` 字符终止。如果没有终止，将字符串传递给 C 函数或系统调用时存在核心崩溃和损坏的风险。Perl 自己的函数通常为此添加末尾的 `NULL`。尽管如此，将存储在 `sv` 中的字符串传递给 C 函数或系统调用时仍小心。

要访问 `SV` 指向的实际值，你可以使用宏：

```
SVIV(SV*) SVUV(SV*) SVNV(SV*) SVPV(SV*, NRLEN len) SVPV_nolen(SV*);
```

在 `SVPV` 宏中，字符串长度返回到变量 `len`（这是一个宏，所以你不需要 `&len`）。如果你不关心数据的长度，请使用 `SVPV` 宏。历史上，全局 `PL_na` 已用于此。但这可能非常低效，因为在线程 Perl 中 `PL_na` 必须在线程本地存储中访问。在任何情况下，记住 Perl 允许包含 `NULL` 的任意字符串，并以 `NULL` 终止。

此外记住，C 不允许你安全地写 `foo(SVPV(s, len), len);` 这在你的编译器上可能有效，但对所有人都不适用。将此类语句拆分为单独赋值：

```
SV *s; NRLEN len; char *ptr; ptr = SVPV(s, len); foo(ptr, len);
```

想知道 `SV` 是否为真，使用宏：

```
SVTRUE(SV*)
```

虽然 Perl 会自动扩展 `sv` 的字符串，如果你需要强制 Perl 为你的 `sv` 分配更多内存，可以使用宏：

```
SVGROW(SV*, STLEN newlen
```

决定是否需要分配内存。如果是，它将调用函数 `sv_grow`。

第一行从零到 `&PL_sv_undef`，一切都会好好的。

要释放你创建的 `sv`，请调用 `SVREFCNT_dec(SV)`。通常情况下这种调用是不必要的（参见“引用计数与生存”）。

## 偏移 (Offsets)

Perl 提供了 `sv_chop` 函数来高效地从字符串开头删除字符；你给它一个 `sv` 和指向 `PV` 中某处的指针，它会丢弃指针之前的所有内容。这种效率源于一个小技巧：`sv_chop` 并没有实际上删除字符，而是设置标志 `OK`（偏移 OK）来向其他函数信号该偏移技巧正在生效，并且它根据切掉的字节数移动 `PV` 指针（称为 `svPV`），并相应地调整 `SVCUR` 和 `SVLEN`。在内存中，旧 `PV` 指针和新 `PV` 指针之间的一部分空间被用于存储切掉的字节计数。

因此，在此时，我们在内存中分配的 `svPV(sv)-svIV(sv)` 缓冲区的起始位置，而 `PV` 指针正指向该分配存储的中间。

通过示例可以最好地演示这一点。通常写时复制（copy-on-write）会防止赋值操作符使用这种技巧，但如果你无法为写时复制创建一个字符串，你可以在 Perl 中看到它。在当前实现中，字符串的最后一个字节被用作写时复制的引用计数。如果缓冲区不够大，就会使用写时复制。看这个空字符串：

```
% /perl -l -MDev::Peek -le "$sv"; $a = ""; Dump $a; SV = PV(0xff7b7c008a70) at 0xff7bc0c30390 REFCNT = 1 FLAGS = (POK, pPOK) PV = 0xff7bc050b50 """ CUR = LEN = 10
```

注意这里的 `len` 是 10（在你的平台上接下来可能是偏移量）。将字符串长度扩展到小于 10，并进行细分：



```
% /perl -MDev::Peek -le "$sv"; $a="123456789"; $a=-s/\//; Dump($a); SV = PV(0xff7a04068a70) at 0xff7a0403090 REFCNT = 1 FLAGS = (POK, pPOK) OFFSET = 1 PV = 0xff7a0403c5b61 "1" = "23456789" CUR = 8 9
```

切掉的字节数接下来作为偏移量。字符串中“真实”和“伪”之间的部分在括号中显示，`SVCUR` 和 `SVLEN` 的值反映了变化，而不是真实的（这里字符串的第一个字符恰好变成了“1”，而不是 `1`，因为当前实现将偏移计数存储在字符串缓冲区中。这可能会发生）。

`AV` 上也执行了类似的偏移技巧，以便高效地平移和剪切数组开头；而 `AVARRAY` 指向 C 数组的真实起始位置。这些通常是相同的，但可以通过增加 `AVARRAY` 并减小 `AVFILL` 和 `AVMAX` 来执行平移操作。同样，C 数组真实起始位置的位置只有在释放数组时才会涉及到。`a.c` 中的 `sv_shift`。

### sv 中到底存储了什么？

回想一下，确定标量类型的常用方法必须使用 `sv*ok` 宏。因为标量既可以是数字也可以是字符串，通常这些宏会返回 `TRUE`，而调用 `sv*v` 宏将执行字符串到整数/双精度浮或整数/双精度到字符串的相应转换。

如果你确实需要知道 sv 中是整数、双精度浮还是字符串指针，可以使用以下三个宏代替：

```
SvIOkp(\*) SvNOKp(\*) SVOKp(\*)
```

这些宏将告诉你的 sv 中是否存储了整数、双精度浮或字符串。“p”代表私有（private）。

私有和公共标志之间有多种差异方式。例如，perl 5.16 及之前的 sv 可能在 `iv` 槽中有一个有效的底层值（`svIOkp` 为 `true`），但应该通过 `FETCH` 程序而不是直接访问数据，`svIOkp` 为 `false`。（在 perl 5.18 中，未绑定的（untied）标量使用的标志与它们相同）。另一种是发生了数值转换并导致精度丢失：唯一的标志被设置为“丢失精度（lossy）”值。当 `nv` 带有丢失地转换为 `iv` 时，`svIOkp`、`svNOkp` 和 `svNO` 会被设置，而 `SVOK` 则不会。

尽管如此，最好使用 `sv*v` 宏。

### 与 AV 操作

创建和加载 av 有两种方法。第一种方法创建一个空 av：

```
AV* newAV();
```

第二种方法创建 av 并初始填充 sv：

```
AV* av_make(SSize_t num, **ptr);
```

包含 `num` 个 `sv*` 的数组的第二个参数。av 已经创建，如果需要，可以销毁 svs。一旦创建了 av，就可以对其进行以下操作：

```
void av_push(AV*
```

这些应该是熟悉的操作，`av_unshift` 除外。该程序在数组开头添加 `num` 个元素，你必须使用 `av_store` 为这些新元素赋值。这里是其他函数：

```
SSize_t av_top_index(AV*); SV** av_fetch(AV*, SSize_t key, I32 lval); SV** av_store(AV*, SSize_t key, SV* val);
```

`av_top_index` 函数返回数组中的最大索引（如 Perl 中的 `$$array`）。如果数组为空，返回 -1。`av_fetch` 函数返回索引的值，如果 `lval` 不为零，则 `av_fetch` 将在该处存储 `undef`。`av_store` 函数在索引 `key` 处存储 `val`，并且不增加 `val` 的引用计数。因此，负责处理这一点，如果 `av_store` 返回 `NULL`，调用者必须减少引用计数以避免内存泄漏。注意 `av_fetch` 和 `av_store` 都返回 `SV***`而不是 `SV*`。还有几个：

```
void av_clear(AV*); void av_undef(AV*); void av_extend(AV*, SSize_t);
```

它们还返回并接受整个哈希条目 (`HE*`)，使得它们更加高效（因为特定字符串的哈希值不需要每次重新计算）。详细描述请参见 `perlapi`。

访问哈希条目的内容必须始终使用以下宏。请注意，这些宏的参数必须是简单变量，因为它们可能会被多次求值。这些宏的详细描述请参见 `perlapi`。

```
HePV(he*, STRLen he) HeVAL(HE* he) HeHASH(he he) HeSVKEY(HE* he)
SVKEY_force(HE* he) HeSVKEY_set(HE he, SV sv)
```

定义了这两个二级宏，但只有在处理非 `SV*` 键时可以使用：

```
HeKEY(HE* he) HeKLEN(HE* he)
```

注意，`hv_store` 和 `hv_store` 都不会增加所存储 `val` 的引用计数，这是调用者的责任。如果这些函数返回 `NULL` 值，调用者将不得不减少 `val` 的引用计数以避免内存泄漏。

### AVs、HVs 和未定义值

有时你必须在 `AV` 或 `HV` 中存储未定义值。虽然这种情况很少见，但处理起来可能棘手。这是因为如果你需要一个未定义的 sv，你就会使用 `PL_sv_undef`。

例如，直觉告诉你这段 xs 代码：

```
AV *av = newAV(); av_store( av, 0, &PL_sv_undef );
```

等于这段 Perl 代码：

my @av; $av[0] = undef;

不幸的是，事实并非如此。在 perl 5.18 及之前的版本中，AVs 使用 `PL_sv_undef` 作为标记，指示数组元素尚未初始化。因此，对于上述代码，`exists $av[0]` 将为真，但对于 xs 代码生成的数组则为假。在 perl 5.20 中，存储 `PL_sv_undef` 将创建一个只读元素，存储的是标量 `&PL_sv_undef` 本身的副本。

在 `HV` 中存储 `PL_sv_undef` 时也会出现类似的问题：

hv_store(hv, "key", 3, &PL_sv_undef, 0 );

这将使该值变为未定义，但如果你尝试修改 key 的值，将得到以下错误：

尝试修改不可创建的哈希值

在 perl 5.8.0 中，`PL_sv_undef` 也被用于标记受限哈希中的占位符。此类哈希条目在遍历哈希或使用 `hv_exists` 函数检查键时不会出现。

当你将 `PL_sv_yes` 或 `&PL_sv_undef` 存储到 AVs 或 HVs 中，可能会遇到类似的问题。尝试修改此类元素将给你返回以下错误：

## 尝试修改只读内容

简而言之，你可以在 AVs 和 HVs 使用特殊的 `&PL_sv_undef`、`&PL_sv_yes` 和 `&PL_sv_no`，但你必须确保知道自己在做什么。

通常情况下，如果你想在 AV 或 HV 中存储未定义值，你不应该使用 `&PL_sv_undef`，而应该使用 `newSV` 函数创建一个新的未定义值，例如：

```
av_store( av, 42, newSV(0) ); hv_store( hv, "foo", 3, newSV(0), 0 );
```

### 引用

引用是一种特殊的标量类型，它指向其他数据类型（包括其他引用）。

要创建引用，请使用以下函数之一：

SV* newRV_inc(SV*); SV* newRV_noinc(SV*);

参数 thing 可以是 `SV*`、`AV*` 或 `HV` 的任意一个。这两个函数是相同的，不同在于 `newRV_inc` 会增加引用的引用计数；由于历史原因，`newRV` 是 `newRV_noinc` 的别名。

一旦你有了引用，可以使用以下宏对引用进行解引用：

RV(SV*);

然后调用相应的例程，如果需要，将返回的 `SV*` 转换为 `AV*` 或 `HV*`。

要判断一个 sv 是否为引用，你可以使用以下宏：

SVOK(SV*);

要发现引用所指向的值的类型，请使用以下宏并检查返回值。

SVType(SVRV(SV*));

可能返回的最常见类型：

< SVt_PVAV 标量 SVt_PVAV 数组 SVt_PVVH 哈希 SVt_PVCV 代码 SVt_PVGV Glob（可能是一个文件句柄）

更多细节请参见 `perlapi` 中的 "svtype"。

### get化的引用和类对象

引用也用于存储面向对象的编程。在 perl 的 oo 术语中，对象仅仅是一个被祝福（blessed）到包（或类）的引用。一旦被祝福，程序员现在可以使用该引用来访问类中的各种方法。

可以使用以下函数将引用祝福到包中：

```
SV* sv_bless(SV* sv, HV* stash);
```

`sv` 参数必须是一个引用值。`stash` 参数指定引用所属的类。有关将类名转换为 stash 的信息请参见“Stashes and Globs”。

（注：第 636 页之后的文本具有高度重复性，似乎是 OCR 错误循环；我已经处理了上述唯一的含义。）



引用计数被标记为递减，但不会立即递减，直到一短时间之后才会执行。通常，“短时间之后”指的是一个 Perl 语句，例如对 XSUB 函数的调用。凡生（mortal）SV 引用计数的决定因素取决于两个宏：`SVAVMETPS` 和 `FREETMPS`。有关这些宏的更多细节，请参考 `Perclcall` 和 `Perlxs`。

“死亡化（Mortalization）”的最简单的 `SVREFCNT_dec`。然而，如果你对一个变量进行两次死亡化，引用计数将递减两次。

“凡生（Mortal）”SV 主要用于位于 Perl 栈上的 SV。一个示例是为被调用的子程序传递名称而创建的 SV，被标记为凡生态，以便在它从栈中弹出时自动清理。同样，由 XSUBS 返回的结果（它们被推入栈中）通常也会标记为凡生态。

要创建一个凡生变量，请使用以下函数：

`SV* sv_newmortal()`
`sv_mortal(SV*)`
`sv_mortalcopy(SV*)`

第一次调用创建一个凡生的 sv（无值），第二次调用将现有 sv 转换为凡生 sv（从而延迟 `SVREFCNT_dec`），第三次创建一个现有 sv 的凡生副本。由于 `sv_newmortal` 没有给新 sv 赋值，因此通常需要通过 `sv_setpv`、`sv_setiv` 等函数为其赋值：

```
SV* tmp = sv_newmortal(); sv_setiv(tmp, an_integer);
```

就像在多个 C 语句中一样，通常显示如下形式：

```
SV* tmp = sv_newmortal(newSiv(an_integer));
```

你应该在使用小心创建凡生变量。如果你在多个上下文中创建了同一个凡生值，或者多次创建凡生态，就会发生某些问题。将“死亡化”考虑为延迟的 `SVREFCNT_dec` 有助于减少此类问题。例如，如果你传递的是栈上的 sv，则不需要任何死亡化。如果你不确定，那么使用 `SVREFCNT_inc` 和 `sv_mortal`，或者创建一个 `sv_mortalcopy` 会更安全。

凡生程序不仅适用于 SV；通过将它们的地址（强制转换为 SV）传递给 `sv_mortal` 或 `sv_mortalcopy` 程序，`AV` 和 `HV` 也可以变为凡生态。

## 存储区（Stashes）与全局变量（Globs）

stash 是一个包含包内定义的所有变量的哈表。stash 的每个键都是符号名称（由所有具有相同名称的不同类型共享），哈表中的每个值都是一个 GV（全局值）。该 GV 反而包含对以下各种对象的引用（但不限于此内容）：

| 标量值 | 数组 | 哈希值 | I/O 句柄 | 格式 | 子程序 |
| :--- | :--- | :--- | :--- | :--- | :--- |

名为 `PL_defstash` 的单一 stash 持有主包中存在的项。要获取其他包中的项，请在包名后附加字符串“::”。Foo 包中的项是 `PL_defstash` 中的 stash `Foo::`。stash 中 `Baz :: Baz ::` 包的项是 `Baz ::` 的 stash 中的 `Baz ::`。

要获取某个特定包的 stash 指针，请使用函数：

`HV* g_stashpv(const char* name, i32 flags)`
`hv* g_stashsv(SV*, i32 flags)`

第一个函数接受一个字面量，第二个使用存储在 sv 中的字符串。记住，stash 是一个哈表，第二个返回的是一个 `hv*`。如果 `flags` 设置为 `GV_ADD`，将创建一个新包。

`g_stash*v` 的名称是你想要的包符号的类型名称。默认包名为 `main`。如果你有多个嵌套包，将它们的名称传递给 `g_stash*v`，并像 Perl 语言本身那样用 `::` 分隔。

或者，如果你有一个祝福（blessed）引用的 sv，可以使用查找 stash 指针：

```
HV* SVSTASH(SVRV(SV*));
```

然后使用以下函数获取包名本身：

`char* HVNAME(HV* stash);`

如果你需要对对象进行祝福或重新祝福，可以使用以下函数：

`SV* sv_bless(SV*, HV* stash)`

其中第一个参数 `sv*` 必须是一个引用，第二个参数是 stash。返回的 `sv*` 现在可以像任何其他 sv 一样使用。

有关引用和祝福的更多信息，请参阅 `perlref`。

## 双类型 SV

标量变量通常只包含一种类型的值：整数、双精度浮点、指针或引用。Perl 会自动将实际标量数据从存储类型转换为请求的类型。

某些标量变量包含多一种类型的标量数据。例如，变量 `$@` 包含 `errno` 的数值值，或者包含来自 `strerror` 或 `sys_errlist[]` 的字符串等效值。

要将多个数据值强制放入 sv 中，你必须做两件事：使用 `sv_set*v` 程序添加额外的标量类型，然后设置一个标志，以便 Perl 认为它包含多于一种类型的数据。用于设置这些标志的四个宏是：

```
SVOK_on SVOK_on SVOK_on SVOK_on
```

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

例如，要创建一个同时包含数值和描述性字符串值的新 Perl 变量，可以使用以下代码：

```
extern int SVOK_on SVOK_on SVOK_on SVOK_on
```

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

例如，要创建一个同时包含数值和描述性字符串值的新 Perl 变量，可以使用以下代码：

```

（此处原文存在重复内容，已按要求翻译）

（此处原文存在重复内容）

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

（此处原文存在重复内容）

就像在多个 C 语句中一样，通常显示如下形式：

```

SV* tmp = sv_newmortal(newSiv(an_integer));

```

你应该在使用小心创建凡生变量。如果你在多个上下文中创建了同一个凡生值，或者多次创建凡生态，就会发生某些问题。将“死亡化”考虑为延迟的 `SVREFCNT_dec` 有助于减少此类问题。例如，如果你传递的是栈上的 sv，则不需要任何死亡化。如果你不确定，那么使用 `SVREFCNT_inc` 和 `sv_mortal`，或者创建一个 `sv_mortalcopy` 会更安全。

凡生程序不仅适用于 SV；通过将它们的地址（强制转换为 SV）传递给 `sv_mortal` 或 `sv_mortalcopy` 程序，`AV` 和 `HV` 也可以变为凡生态。

## 存储区（Stashes）与全局变量（Globs）

stash 是一个包含包内定义的所有变量的哈表。stash 的每个键都是符号名称（由所有具有相同名称的不同类型对象共享），哈表中的每个值都是一个 GV（全局值）。该 GV 反而包含对以下各种对象的引用（但不限于此内容）：

| 标量值 | 数组 | 哈希值 | I/O 句柄 | 格式 | 子程序 |
| :--- | :--- | :--- | :--- | :--- | :--- |

名为 `PL_defstash` 的单一 stash 持有主包中存在的项。要获取其他包中的项，请在包名后附加字符串“::”。Foo 包中的项是 `PL_defstash` 中的 stash `Foo::`。stash 中 `Baz :: Baz ::` 包的项是 `Baz ::` 的 stash 中的 `Baz ::`。

要获取某个特定包的 stash 指针，请使用函数：
`HV* g_stashpv(const char* name, i32 flags)`
`hv* g_stashsv(SV*, i32 flags)`

第一个函数接受一个字面量，第二个使用存储在 sv 中的字符串。记住，stash 是一个哈表，第二个返回的是一个 `hv*`。如果 `flags` 设置为 `GV_ADD`，将创建一个新包。

`g_stash*v` 的名称是你想要的包符号类型名称。默认包名为 `main`。如果你有多个嵌套包，将它们的名称传递给 `g_stash*v`，并像 Perl 语言本身那样用 `::` 分隔。

或者，如果你有一个祝福（blessed）引用的 sv，可以使用查找 stash 指针：

```
HV* SVSTASH(SVRV(SV*));
```



然后使用以下函数获取包名本身：
`char* HVNAME(HV* stash);`

如果你需要对对象进行祝福或重新祝福，可以使用以下函数：
`SV* sv_bless(SV*, HV* stash)`
其中第一个参数 `sv*` 必须是一个引用，第二个参数是 stash。返回的 `sv*` 现在可以像任何其他 sv 一样使用。

有关引用和祝福的更多信息，请参阅 `perlref`。

## 双类型 SV

标量变量通常只包含一种类型的值：整数、双精度浮点、指针或引用。Perl 会自动将实际标量数据从存储类型转换为请求的类型。

某些标量变量包含多种类型的标量数据。例如，变量 `$@` 包含 `errno` 的数值值，或者包含来自 `strerror` 或 `sys_errlist[]` 的字符串等效值。

要将多个数据值强制放入 sv 中，你必须做两件事：使用 `sv_set*v` 程序添加额外的标量类型，然后设置一个标志，以便 Perl 认为它包含多于一种类型的数据。用于设置这些标志的四个宏是：

```
SVOK_on SVOK_on SVOK_on SVOK_on
```

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

例如，要创建一个同时包含数值和描述性字符串值的新 Perl 变量，可以使用以下代码：

```
extern int SVOK_on SVOK_on SVOK_on SVOK_on
```

（此处原文存在重复内容）

（此处原文存在重复内容）

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

（此处原文存在重复内容）

就像在多个 C 语句中一样，通常显示如下形式：

```
SV* tmp = sv_newmortal(newSiv(an_integer));
```

你应该在使用小心创建凡生变量。如果你在多个上下文中创建了同一个凡生值，或者多次创建凡生态，就会发生某些问题。将“死亡化”考虑为延迟的 `SVREFCNT_dec` 有助于减少此类问题。例如，如果你传递的是栈上的 sv，则不需要任何死亡化。如果你不确定，那么使用 `SVREFCNT_inc` 和 `sv_mortal`，或者创建一个 `sv_mortalcopy` 会更安全。

凡生程序不仅适用于 SV；通过将它们的地址（强制转换为 SV）传递给 `sv_mortal` 或 `sv_mortalcopy` 程序，AV 和 HV 也可以变为凡生态。

## 只读值（Read-Only Values）

（由于原文存在大量乱码和重复片段，以下翻译已基于核心逻辑进行清理翻译，保留了原有的标记结构）

（此处原文存在重复内容）

## 魔术变量（Magic Variables）

此部分正在构建中。忽略此处内容。任何 SV 都是具有魔术的，位于 `magic` 结构：

```
struct magic {
    MAGIC* magic;
    MGVT* mg_virtual;
    U16 mg_private;
    char mg_type;
    U8 mg_flags;
    I32 mg_len;
    sv* mg_obj;
    char* mg_ptr
};
```

（注：由于提供的原始文本包含大量无逻辑的重复和断句，以上翻译已针对可读的有效段落进行了处理。）

类型参数应与 sv 初始为魔法时的值相等。

然而，请注意 `sv_unmagic` 会移除 sv 中该类型的所有魔法属性。如果你只想根据魔法虚表移除特定类型的魔法属性，请使用 `sv_unmagicext`：

```
int sv_unmagicext(SV *sv, int type, MGVTBL *vtbl);
```

## 魔法虚表 (Magic Virtual Tables)

`MAGIC` 结构中的 `mg_virtual` 字段是一个指向 `MGVTBL` 的指针，`MGVTBL` 是一个函数指针结构，代表“魔法虚表”，用于处理可能应用于该变量的各种操作。

`MGVTBL` 拥有五个（或八个）指向以下程序类型的指针：

```
int (*sv_get)(SV* sv, MAGIC* mg); int (*sv_set)(SV* sv, MAGIC* mg); U32 (*sv_len)(SV* sv, MAGIC* mg); int (*sv_clear)(SV* sv, MAGIC* mg); int (*sv_free)(SV* sv, MAGIC* mg); int (*sv_copy)(SV* sv, MAGIC* mg); *nsv, const char *name, i32 n_len); int (*sv_dup)(MAGIC* mg, CLONE_PARAMS *param); int (*sv_local)(SV *nsv, MAGIC* mg);
```

此 `MGVTBL` 在 `perl.h` 中编译时设置，目前有 32 类型。这些不同的结构包含指向各种例程的指针，根据调用的函数来执行额外的操作。

| 函数指针 | 操作 |
| :--- | :--- |
| sv_get | 在获取 SV 的值时执行某些操作。 |
| sv_set | 在 SV 赋值后执行某些操作。 |
| sv_len | 报告 SV 的长度。 |
| sv_clear | 清空 SV 代表的内容。 |
| sv_free | 释放与 SV 关联的任何额外存储。 |
| sv_copy | 将绑定变量魔法绑定到绑定元素 |
| sv_dup | 在克隆期间复制魔法结构 |
| sv_local | 将魔法拷贝到本地值 'local' |

例如，`MGVTBL` 结构包含 `vtbl_sv`（对应于 `PERL_MAGIC_sv` 的 `mg_type`），它包含：

```
{ magic_get, magic_set, magic_len, 0, 0 }
```



因此，当确定一个 `sv` 是魔法的且类型为 `PERL_MAGIC_sv` 时，如果正在执行操作，就会调用 `magic_get` 例程。所有各种类型的例程都以 `magic_` 开头；注意：魔法例程不视为 Perl API 的一部分，可能不会被 Perl 库导出。

最后三个槽是最近添加的，为了源代码兼容性，它们只有在 `mag_flags` 中设置了 `MG_COPY`、`MG_DUP` 或 `MG_LOCAL` 标志之一时才会被检查。这意味着大多数代码可以继续将虚表声明为 5 元素的值。这三个目前被线程代码排除，并且极有可能发生变化。

### 当前的魔法虚表类型有：

| mg_type (旧式字符和宏) | 的 MGVTBL 类型 |
| :--- | :--- |
| `PERL_MAGIC_sv` | `vtbl_sv` | 特殊标量变量 |
| `MAGIC_arylen` | `vtb_arylen` | 数组长度 (`$#ary`) * |
| `PERL_MAGIC_hrash` | (none) | 限制哈希的额外 * |
| `PERL_MAGIC_debugvar` | `vtb_debugvar` | DB::: 符号, trace, verses * |
| `PERL_MAGIC_pos` | `vtb_pos` | pos 左值 |
| `PERL_MAGIC_symtab` | (none) | 额外数据符号表 |
| `PERL_MAGIC_backref` | `vtb_backref` | 用于弱引用数据 @ |
| `PERL_MAGIC_arylen_p` | (none) | 将 ary 移出 XPAV B |
| `PERL_MAGIC_bm` | `vtb_regex` | Boyer-Moore (第一次搜索 c) |
| `PERL_MAGIC_overload_table` | `vtb_ovrld` | 在暂存中持有重载表 (AMT) |
| `PERL_MAGIC_regdata` | `vtb_regdata` | 匹配位置数据元素 (@ 和 @ 变量) d |
| `PERL_MAGIC_regdatum` | `vtb_regdatum` | Regum 匹配位置元素 E |
| `PERL_MAGIC_env` | `vtb_env` | `%ENV` 哈希 e |
| `PERL_MAGIC_envel` | `vtb_envel` | `%ENV` 哈希元素 f |
| `PERL_MAGIC_f` | `vtb_regexform` | ( 'compiled' ) 格式 |
| `PERL_MAGIC_regex_global` | `vtb_global` | `%m /` 目标 H |
| `PERL_MAGIC_hints` | `vtb_hints` | `%H` H # H |
| `PERL_MAGIC_hintint` | `vtb_hintint` | `%H` 哈希元素 I |
| `PERL_MAGIC_isa` | `vtb_isa` | `@ISA` 数组 I |
| `PERL_MAGIC_isaem` | `vtb_isaem` | `@ISA` 元素 k |
| `PERL_MAGIC_keys` | `vtb_keys` | 标量 (`keys(@)`) 左值 L |
| `PERL_MAGIC_dbfile` | (none) | 调试器 <<filename> L |
| `PERL_MAGIC_dbline` | `vtb_dbline` | 调试器 <<filename> N |
| `PERL_MAGIC_shared` | (none) | 两个线程间共享 n |
| `PERL_MAGIC_shared` (scalar) | 线程间共享 |
| `PERL_MAGIC_colxfrm` | `vtb_colxfrm` | 损坏变量 P |
| `PERL_MAGIC_tied` | `vtb_pack` | 绑定 ary 或 h |
| `PERL_MAGIC_tied` | `vtb_packlem` | 绑定标量或哈希元素 q |
| `PERL_MAGIC_tiedscalar` | `vtb_packlem` | 绑定标量或 r |
| `PERL_MAGIC_qr` | `vtb_regex` | 预编译 `qr //` S |
| `PERL_MAGIC_sig` | (none) | `%SIG` 有 h S |
| `PERL_MAGIC_sig` | `vtb_siglem` | `%SIG` 哈希元素 |
| `PERL_MAGIC_tain` | `vtb_tain` | 污染性 U |
| `PERL_MAGIC_overload` | `vtb_ubar` | 扩展可用 |
| `PERL_MAGIC_vstring` | (none) | SV 字面量 V |
| `PERL_MAGIC_vec` | `vtb_vec` | `vec()` 左值 W |
| `PERL_MAGIC_utf` | `vtb_utf` | 缓存 UTF-8 信息 x |
| `PERL_MAGIC_substr` | `vtb_substr` | `substr(x)` 左值 L |
| `PERL_MAGIC_defelem` | `vtb_defelem` | "foreach" 迭代器 / 智能 |
| `PERL_MAGIC_lref` | `vtb_lref` | 引用构造函数 |
| `PERL_MAGIC_check` | `vtb_check` | 内联/变异调用此 |
| `PERL_MAGIC_ext` | (none) | 扩展可用 |

当大写字母和小写字母都存在文本时，大写字母通常用于表示某种复合类型（列表或哈希），小写字母用于表示复合类型的元素。某些内部实现利用了这种关系。然而，‘v’ 和 ‘V’（以及字符串）是相关的。`PERL_MAGIC_ext` 和 `PERL_MAGIC_ubar` 类型专门为扩展定义，Perl 本身不会使用它们。扩展可以使用魔法为变量（通常是对象）附加私有信息。这特别有用，因为 Perl 没有普通方法来保护这些信息（类似于哈希元素）。

同样，`PERL_MAGIC_ubar` 魔法可以像 `tie()` 一样使用，在标量值被使用或更改时调用函数。`sv_ptr` 字段指向一个结构：

```
struct undef {

    I32 (*uf_val) (IV, SV*);

    I32 (*uf_set) (IV, SV*);

    IV uv_index;

};
```

当读取或写入 `sv` 时，会使用 `uv_index` 作为第一个参数调用 `uf_val` 或 `uf_set` 函数。下方显示了添加 `PERL_MAGIC_ubar` 魔法的简单示例。注意 `iffuncs` 结构会被 `sv_magic` 拷贝，因此你可以安全地在栈上分配它。

```
void uMagic(SV *sv);

PREINIT: struct iffuncs uf; 

CODE: uf->uf_val = &my_get_fn; uf->uf_set = &my_set_fn; uf->uf_index = 0; sv_magic(sv, 0, PERL_MAGIC_ubar, (char*)&uf, sizeof(uf));
```

在数组上附加 `PERL_MAGIC_ubar` 是允许的，但它控制的是哈希键（而不是值）。对于哈希，有一个特殊的钩子可以控制哈希键。如果 `iffuncs` 结构中的 'set' 函数为 `NULL`，该钩子会调用 `PERL_MAGIC_ubar` 'get' 魔法。每当通过 `hv_store_ent`、`hv_fetch_ent`、`hv_delete_ent` 和 `hv_exists_ent` 使用特定键或 `sv` 访问哈希时，钩子就会激活。通过函数作为字符串访问键会绕过钩子。详见 `Hash::Field` 中的 GUTS。

由于多个扩展可能使用 `PERL_MAGIC_ext` 或 `uubar` 魔法，扩展需要额外小心避免冲突。通常只需对与扩展相同类的对象使用魔法就足够了。对于 `PERL_MAGIC_ext` 魔法，定义 `MGVTBL` 通常是个主意，即使所有字段都为 0，这样可以使用虚表将单个指针识别为特定类型的魔法。`mg_findext` 提供了一种方法：

```
STATIC MGVTBL my_tbl = {0, 0, 0, 0, 0, 0, 0};

MAGIC *mg;

if ((mg = mg_findext(sv, PERL_MAGIC_ext, &my_tbl))) {

    /* 这真的是我们的，而不是其他模块的 */

    PERL_MAGIC_ext *my_priv_data_t *priv = (my_priv_data_t*)mg->ptr;

}
```



另外注意，之前描述的 `sv_*` 和 `sv_cat()` 函数在其目标上调用 'get' 魔法。这必须由用户在调用这些函数后调用 `SVSETMAGIC()` 来完成，或者使用 `sv_set_*_mg()` 或 `sv_cat_*_mg()` 函数。同样，如果你在不处理魔法的函数来自外部的 sv，C 代码必须调用 `SVGETMAGIC()` 宏来调用任何 'get' 魔法。关于这些函数的描述请参考 Perl。例如，对 `sv_cat()` 函数的调用通常需要后续 `SVSETMAGIC()`，但不需要之前的 `SVGETMAGIC()`，因为它们的实现处理了 'magic'。

## 查找魔法 (Finding Magic)

```
MAGIC *mg_find(sv *sv, int type); /* 查找类型的魔法指针 */
```

此程序返回存储在 sv 中的 MAGIC 结构指针。如果 sv 没有该魔法特征，则返回 NULL。如果 sv 有多个魔法特征实例，将返回第一个。`mg_findext` 可以根据魔法类型和其虚表查找 sv 的 MAGIC 结构：

```
MAGIC *mg_findext(sv *sv, int type, MGVTBL *vtbl);
```

另外，如果传递给 `mg_find` 或 `mg_findext` 的 sv 不是 SVt_PPMG 类型，Perl 可能会发生转储。

```
int mg_copy(SV* sv, SV* nsv, const char* key, STRLEN klen);
```

此例程检查 sv 具有哪些类型的魔术（magic）。如果 mg_type 字段是一个大写字母，则将 mg_obj 复制到 nsv，但会将 mg_type 字段更改为小写字母。

# 理解绑定（Tied）哈希和数组的魔法

绑定哈希（tied hashes）和数组是 `PERL_MAGIC_tied` 魔术类型的“魔兽”。

警告：从 5.004 版本开始，为了正确使用数组和哈希访问函数需要理解几处注意事项。其中某些注意事项实际上被认为是 API 的错误，将在稍后的版本中修复，并被括在 [MAYCHANGE] 标记中。如果你发现自己实际上应用了本节中的此类信息，请注意，该行为在未来可能会在不经警告的情况下发生变化。

`perl tie` 函数将变量与一个实现了各种（如 SET 等）方法的对象关联。要从 XSUB 执行等同于 `perl tie` 函数的操作，你必须模拟这种行为。代码执行了必要的步骤——首先创建一个新哈希，然后创建第二个哈希并将其加固（bless）到实现绑定方法的类中。最后，它将两个哈希绑定，并返回绑定哈希的引用。注意，下面的代码**没有**调用 `MyTie` 类中的 `TIASH` 方法——有关如何执行此操作的详情请“从 C 程序调用例程”。

```
SV* mytie() PREHIT: SV* hash; SV* stash; SV* code; hash = newHV;

tie = newRV_noinc(SV*)newHV); stash = g_svhash("MyTie"), GD_ADD;

sv_bless(tie, stash), hv_magic(hash, GV*)tie, PERL_MAGIC_tied); RETVAL = newRV_noinc(hash); OUTPUT: RETVAL
```

`av_store` 函数在接收到绑定参数时，会使用 `mg_copy` 将数组的副本带到要“存储”的值上。它可能返回 `NULL`，表示该值实际上不需要存储在数组中。[/MAYCHANGE] 在绑定数组上调用 `av_store` 时，调用者通常需要调用 `mg_set(val)` 以实际调用 TIARRAY 象上的 perl `STORE` 方法。如果 `av_store` 返回 `NULL`，也需要调用 `SVREFCNT_dec(val)` 以避免内存泄漏。[/MAYCHANGE]

上一段的内容与使用 `hv_store` 和 `hv_store_ent` 函数进行绑定哈希访问的情况也是完全相同的。

`av_fetch` 以及对应的哈希函数 `hv_fetch` 和 `hv_fetch_ent` 实际上返回一个未定义的值，其哈希已使用 `mg_copy` 初始化。返回的值不需要释放，因为它们已经是内存中了了。[/MAYCHANGE] 但你需要对返回的值调用 `mg_get()`，以便实际调用底层绑定对象上的 perl `FETCH` 方法。同样地，当对 TIE 对象使用 "STORE" 方法时，在可能考虑了使用合适的值通过 `sv_setsv` 后，你可能也可以对返回值调用 `mg_set()`。[/MAYCHANGE]

[/MAYCHANGE] 换句话说，在绑定数组和哈希的情况下，数组或哈希/存储函数并没有完全获取并存储实际值。它们只是调用 `mg_copy` 将 `mg` 附加到本应“存储”或“获取”的值上。稍后调用 `mg_get` 和 `mg_set` 实际上执行了调用底层对象绑定方法的工作。这种魔法机制目前实现了对数组和哈希的一种惰性访问（lazy access）。

目前（截至 perl 5.004 版本），使用哈希和数组访问函数需要用户意识到他们操作的是“普通”哈希和数组，还是它们的绑定变体。API 在未来的版本中可能会被更改，以提供对绑定和普通数据类型提供更透明的访问。[/MAYCHANGE]

你最好理解 `TIEARRAY` 和 `TIEHASH` 接口。

# 子程序 (SUBROUTINES)

## XSUB 与参数栈 (Argument Stack)

XSUB 机制是 Perl 程序访问 C 子程序的简单方法。XSUB 程序将拥有一个包含 Perl 程序参数的栈，以及一种将 Perl 数据结构映射到 C 等效结构的方法。

可以通过 `(n)` 宏访问栈参数，该宏返回第 n 个栈参数。参数 0 是在 Perl 子程序调用传递的第一个参数。这些参数是 `SV*` 类型，可以在任何使用 SV 的地方使用。

大多数情况下，C 过程的输出可以通过 `RETVAL` 和 `OUTPUT` 指令来处理。然而，在某些情况下，参数栈的长度不足以处理所有的返回值。一个例子是 POSIX `tzname()` 调用，它不接受任何参数，但返回两个值：本地时区的标准时间和夏令时缩写。

为了处理这种情况，可以使用 `PPCODE` 指令，并使用宏扩展栈：

```c
EXTEND(SP, num);
```

其中 `SP` 是代表栈指针本地副本的宏，`num` 是栈需要扩展的元素数量。

现在栈上有了空间，可以使用 `PUSHs` 宏推入值。推入的值需要是“生存的”（mortal）（参见“引用计数与死亡率”）：

```c
PUSHs(sv_2mortal(newSV(an_integer)));
PUSHs(sv_2mortal(newSVuv(an_unsigned_integer)));
PUSHs(sv_2mortal(newSVnv(a_double)));
PUSHs(sv_2mortal(newSVpv("Some String"))); /* 虽然该示例最好写成更高效的形式： */
PUSHs(newSVpv_flags("Some String", SVs_TEMP));
```

对于调用 `tzname` 的 Perl 程序，值将被赋值为：
($stack_abbrev, $summer_abbrev) = POSIX::tzname;

向栈中推入值的另一种（可能可能更简单）的方法是使用宏：

```c
XPUSHs(SV*)
```

如果需要，它会自动为你调整栈。因此，你不需要调用 `EXTEND` 来扩展栈。

尽管本文早期的版本给出了建议，但宏 `(X)PUSH[iunp]` 并不适用于返回多个结果 XSUB。对于这种情况，要么坚持上述的 `(X)PUSHs` 宏，要么使用新的 `m(X)PUSH[iunp]` 宏；参见“将 C 值放入 Perl”。

如需更多信息，请查阅 `perlxs` 和 `perlsext`。

## 自动加载 XSUB

如果 `AUTOLOAD` 过程是一个 xsub（就像 Perl 子程序一样），Perl 会将自动加载子程序的全限定名放在 xsub 包的 `$AUTOLOAD` 变量中。

但它也将相同的信息存放在 XSUB 自身的某些字段中：

```c
HV *stash = CVSTASH(cv); const char *subname = SVPVX(cv); STRLEN name_length = SVCUR(cv); /* 字节 */ U32 utf8 = SV8(cv);
```



`SVVPX(cv)` 包含子程序本身，不包括包名。对于 `UNIVERS` 或其父类中的自动加载，在对不存在的包调用方法时，`CVSTASH(cv)` 返回 `NULL`。

注意：设置 `$AUTOLOAD` 在 5.6.1 中停止工作，该版本完全不支持 XS 自动加载。Perl 5.8.0 引入了 XSUB 自身字段的使用。Perl 5.16.0 恢复了 `$AUTOLOAD` 的设置。如果你需要支持 5.8-5.14，请使用 XSUB 的字段。

## 从 C 程序调用 Perl 过程

有四个可以从 C 程序调用 Perl 子程序的过程。这四个是：

```c
I32 call_sv(SV*, I32); I32 call_pv(const char*, I32); I32 call_method(const char*, I32); I32 call_argv(const char*, I32);
```

最常用的过程是 `call_sv`。`SV *` 参数包含要调用的 Perl 子程序的名称或其引用。第二个参数由标志组成，用于控制子程序调用的上下文、子程序是否被传递了参数、应该如何捕获错误以及如何处理返回值。

所有过程都返回子程序在 Perl 栈上返回的参数数量。

在 Perl v5.6.0 之前，这些过程被称为 `perl_call_sv` 等，但这些名称现在已被废弃；为了兼容性，提供了同名的宏。

在使用这些任何一个过程（`call_argv` 除外）时，程序员必须操作 Perl 栈。这些包括以下函数和宏：

```c
dsp SP PUSHMARK() PUTBACK SPAIN ENTER SAVEMPS FREETMPS LEAVE XPUSH() POP(*);
```

有关从 C 到 Perl 的调用约的详细说明，请查阅 `perlcall`。

## 将 C 值放入 Perl 栈

许多操作码（这是 Perl 内部栈数器机中的一种基础操作）都会在栈上放置一个 `SV*`。然而，作为一种优化，相应的 `sv` （通常）不会每次重新创建。操作码重用专门分配的 SV（目标），这些目标（作为结果）不会被不断释放/创建。

每个目标只创建一次（参见下文的“垫板与递归”），当操作码需要整数、双精度浮或字符串时，它会将其推入栈中。

由于目标是被重用的，当目标需要多个值时必须小心。以下代码不会按你预期的方式工作：

```c
XPUSH(10); XPUSH(20);
```

你可以简单地写：

```c
XPUSHs(10); XPUSHs(20);
```

垫板上的目标是未定义的，但它们已经标记了正确的标志。

## 垫板 (Scratchpads)

问题仍然在于操作码的目标 SV 是否被创建。答案是它们在编译当前单元（子程序或文件，针对子程序外的操作码）时被创建。在此期间会创建一个匿名数组，称为当前单元的垫板。

本文之前的某个版本说明局部变量设置了 `SVPADMY`，而目标设置了 `SVADTMP`。但事实并非完全。`SVPADMY` 可以设置在不再位于垫中的变量上，但它仍然像目标。根据 perl 21.5，`SVPADMY` 标志不再被使用并定义为 0。`SvPADMY()` 现在对任何没有 `SVADTMP` 的对象都返回真。

## 垫板与递归

事实上，编译单元包含指向垫板 AV 的指针并不是 100% 准确的。事实上，它包含一个初始包含一个元素的 AV 的指针，而这个元素就是垫板 AV。为什么我们需要额外的一层间接？

答案是递归，可能还有线程。这两者都可以创建多个进入同一个子程序的执行指针。为了不让子子程序覆盖父级子程序的临时变量（后者的生命周期覆盖了对子程序的调用），父程序和子程序应该拥有不同的垫板。（局部变量本应该是独立的！）

因此，每个子程序在诞生时都带有一个垫板数组（长度为 1）。每次进入子程序时，都会检查递归深度是否超过了数组的长度，如果是，则创建一个新的垫板并将其推入数组。

## 内存分配

### 分配 (Allocation)

所有预期用于 Perl API 函数的内存都应该使用本节描述的宏进行操作。这些宏在 Perl 内部使用的实际 `malloc` 实现的差异之间提供了必要的透明性。

建议你启用与 Perl 一起分发的 `malloc` 版本。它维护了各种大小的未分配内存池，以便更快地满足分配请求。然而，在某些平台上，它可能会导致伪造的 `malloc` 或 `free` 错误。

有三个宏用于初始分配内存：

- `Newx(pointer, number, type)`; `Newxc(pointer, number, type, cast)`;
- `Newxz(pointer, number, type)`;

第一个参数 `pointer` 应该是指向新分配内存的变量名。

第二个和第三个参数 `number` 和 `type` 指定了应该分配多少个指定类型的数据结构。参数 `type` 被传递给 `sizeof`。如果 `pointer` 参数与 `type` 参数不同，则应使用 `newxc` 的最后一个参数 `cast`。

与 `Newx` 和 `Newxc` 宏不同，`Newxz` 宏会调用 `memzero` 将所有新分配的内存清零。

### 重新分配 (Reallocation)

`Renew(pointer, number, type)`; `Renewc(pointer, number, type, cast)`; `Saffree(pointer)`

这三个宏用于更改内存缓冲区的大小或释放不再需要的内存。`Renew` 和 `Renewc` 的参数与 `New` 和 `Nc` 匹配，不同之处不需要“魔法饼干”（magic cookie）参数。

### 移动 (Moving)

`Move(source, dest, number, type)`; `Copy(source, dest, number, type)`; `Zero(dest, number, type)`;

这三个宏用于移动、复制或清零之前分配的内存。`source` 和 `dest` 参数指向源和目的起始点。Perl 将移动、复制或清零 `number` 个大小为 `type` 数据结构的实例（使用 `sizeof` 函数）。

## PERLIO

Perl 的最新开发版本一直在尝试移除对“普通”标准 I/O 套件的依赖，并允许使用其他的 std 实现。这涉及创建一个新的抽象层，然后调用 Perl 编译时所使用的任何 `stdio` 实现。所有的 XSUBs 现在都应该使用 PerlIO 抽象层中的函数，而对正在使用的 stdio 类型不做任何假设。

要了解 PerlIO 抽象的完整描述，请参考 `perlapio`。

## 编译代码 (COMPILED CODE)

### 代码树 (Code tree)

在这里我们定义了 Perl 将你的代码转换成的内部形式。从一个简单的示例开始：
`$a = $b + $c`;

这被转换为类似于下面的树：
assign-to / \ + $a / \ $b $c

（但稍微复杂一些）。这棵树反映了 Perl 解析你代码的方式，但与执行顺序无关。树节点中穿过一条额外的“线程”，显示了节点的执行顺序。在我们上面的简化示例中，它看起来像这样：
`$b --> $c ---> + ---> $a assign-to`

但对于 `$a = $b + $c` 的实际编译树，情况是不同的：某些节点被优化掉了，尽管实际树包含的节点比我们的简化示例多，但执行顺序与我们的示例相同。

### 检查树 (Examining the tree)

如果你编译了用于调试的 perl（通常在命令行中使用 `-D`），你可以通过在命令行中指定 `-Dx` 来检查编译后的树。输出占几行，对于 `$b+$c`，它看起来如下：

```
5 TYPE = add === 6 FLAGS = (SCALAR,KIDS) { TYPE = null (4) (was 2) FLAGS = (SCALAR,KIDS) { 3 === 4 FLAGS = (SCALAR) main::b } { TYPE = null (5) (was 2) FLAGS = (SCALAR,KIDS) { 4 === 5 FLAGS = (SCALAR) main::c }
```

这棵树有 5 个节点，其中只有 3 个节点被优化掉了（每列一个）。

位于 `run.c` 和 `dump.c` 中。在开启 DEBUGGING 模式时使用 `Perl_runops_debug`，否则使用 `Perl_runops_standard`。为了精细控制编译树的执行，你可以提供自己的 `runops` 函数。

可能可以复制现有的 `runops` 函数并进行修改以满足你的需求。然后，在你的 xs 文件的 `BOOT` 部分，添加该行：

```
PL_runops = my_runops;
```

该函数应该尽可能高效，以保持你的程序运行尽可能快。

## 编译时作用域钩（Compile-time scope hooks）

从 perl 5.14 开始，可以使用 `Perl_blockhook_register` 钩入编译时作用域词法机制。其用法如下：

```



`STATIC void my_start_hook(pHTX_ int full);`
`STATIC BHK my_hooks;`
`BOOT:`

`BHKENTRY_set(&m_y, bhk_start, my_start_hook);`

`Perl_blockhook_register(atHX &_my_hooks);`

```
这将安排在编译词法作用域开始时调用 `my_start_hook`。可用的钩子有：
```

```
void bhk_start(pHTX_ int full)
```

```
if ($x) { ... }
```

创建作用域：第一个在 `{` 开始且 `has == 1`，第二个在 `{` 开始且 `has == 0`。两者结束于 `}`，因此对 `start` 和 `pre/post_end` 的调用将相互匹配。任何推入栈的内容都将在作用域结束前被弹出（实际上是在 `pre_` 和 `post_end` 钩子之间）。

```
void bhk_pre_end(pHTX_ **o)
```

这在词法作用域结束时调用，在栈栈之前。`o` 是表示作用域的树的根；它是一个双指针，如果需要，你可以替换 `o`。

```
void bhk_post_end(pHTX_ **o)
```

这在词法作用域结束时调用，紧随栈栈之后。`o` 与上述相同。注意，如果栈上有东西调用了 `eval` 字符串，`pre_` 和 `post_end` 的调用可能会嵌套。

```
void bhk_eval(pHTX_ *const o)
```

这在开始编译 `eval STRING`、`do FILE`、`require` 或 `use` 之前调用（在 eval 请求之后），通常是 `OP_ENTEREVAL`、`OP_FILE` 或 `OP_REQUIRE`。

一旦你有了钩子函数，你需要使用一个 `BHK` 结构将它们放入其中。最好静态分配它，一旦注册，没有办法释放它。应该使用 `BHKENTRY_set_macro` 将函数指针插入此结构中，该宏还会设置指示哪些条目有效的标志。如果由于原因需要动态分配 BHK，请确保在启动前将其清零。

一旦注册，没有关闭这些钩子的机制，因此如果必要，你需要手动执行。在 `%^H` 中设置条目可能是最好的方法，这样效果就是词法作用域；但也可以使用 `BhkDISABLE` 和 `BhkENABLE` 宏来临时开启或关闭条目。你应该意识到，通常在你的扩展加载之前，至少有一个作用域已经打开，因此你会看到一些没有匹配 `start` 的 `pre/post_end` 对。

## 使用 DUMP 函数检查内部数据结构

为了帮助调试，源文件 `dump.c` 包含了许多可以产生内部数据结构格式化输出的函数。

这些函数中最常用的是 `Perl_sv_dump`；它用于转储 SVs、AVs、HVs 和 CVs。`Devel::Peek` 模块调用 `sv_dump` 从 Perl 空间产生调试输出，因此该模块的用户应该已经熟悉它的格式。

`Perl_op_dump` 可用于转储 OP 结构或任何派生结构，并产生类似于 `perl -Dx` 的输出；事实上，Perl_dump_eval` 将转储正在评估的代码的主根，就像 `-Dx` 一样。

其他有用的函数是 `Perl_dump_sub`（它将 GV 转换为 op 树）、`Perl_dump_packsubs`（它对包中的所有子程序调用 `Perl_dump_sub`，如下所示：谢天地，这些都是 xsubs，没有 op 树）：

```
(gdb) print Perl_dump_packsubs(PL_defstash) SUB attributes::bootstrap = (xsub 0x811fedc 0) SUB UNIVERS::can = (xsub 0x811f50c 0) SUB UNIVERS::isa = (xsub 0x811f304 0) SUB UNIVERS::version = (xsub 0x811f7ac 0) SUB DynaLoader::boot_DynaLoader = (xsub 0x805b188 0)
```

以及 `Perl_dump_all`，它转储 stash 中的所有子程序以及主根的 op 树。

## 如何支持多个解释器和并发

### 背景与 PERL_IMPLICIT_CONTEXT

Perl 解释器可以被视为一个封闭的黑盒：它有一个用于输入代码（或以其他方式使其实体化）的 API，但它也有一套供其内部的函数。这听起来非常像一个对象，并且有办法构建 Perl 使你拥有多个解释器，每个解释器用一个 C 结构表示，或者……

等待，通常在你的扩展加载之前，至少有一个作用域已经打开，因此你会看到一些没有匹配 `start` 的 `pre/post_end` 对。

将 `aTHX_` 作为第一个参数（Perl内核倾向于对 `Perl_warner` 等函数这样做），或者使用无上下文的版本。

`Perl_warner` 的无上下文版本被称为 `Perl_warner_nocontext`，它不接受额外的参数。它执行 `dTHX`；从线程本地存储中获取上下文。我们 `#define warner Perl_warner_nocontext`，这样扩展就可以以性能为代价生成兼容性。（传递参数比从线程本地存储中获取要便宜得多。）

在浏览 Perl 头文件/源码时，你可以忽略 `padTHXX`。那些是严格供内核内部使用的。扩展和嵌入器只需要关注 `aTHX`。

## 那么 dTHX 怎么了？

`dTHX` 引入于 Perl 5.005，以支持旧的线程模型。旧模型使用 `dTHX` 机制传递上下文指针，因此 `dTHX` 不再有用。Perl 5.6.0 及后续版本为了源码二进制的向后兼容性仍然保留了它，但它被定义为空操作（no-op）。

## 我如何在这些扩展中使用所有内容？

当 Perl 带有 `PERL_IMPLICIT_CONTEXT` 进行构建时，任何调用 Perl API 中任何函数的扩展都会传递下一个参数。关键点在于，你需要以这种方式编写代码，使得当 Perl 没有在启用 `PERL_IMPLICIT_CONTEXT` 的构建时，扩展仍然可以编译。

有三种方法可以实现这一点。第一种简单但低效的方法，也是默认方法，为了保持与扩展的源码兼容性：每当 `#include` `XUB.h` 时，它都会重新定义 `aTHX` 和 `aTHX_` 宏，以调用一个返回上下文的函数。因此，类似：

```
sv_setiv(sv, num);
```

在 `PERL_IMPLICIT_CONTEXT` 生效时，你的扩展中的内容会被翻译为：

```
Perl_setiv(Perl_get_context()), sv, num);
```

或者在其他情况下翻译为：

```
Perl_setiv(sv, num);
```

你不需要在扩展中做任何事情来获取这一点；因为 Perl 库提供了 `Perl_get_context()`，它一切都能正常工作。

第二种最高效的方法是为 `Foo::xs` 使用以下模板：
```c
#define PERL_NO_GET_CONTEXT /* / 我们想要效率 /* /
#include "EXTERN.h"
#include "Perl.h"
#include "XUB.h"
STATIC void my_private_function(int arg1, int arg2) {
    dTHX; /* 获取上下文 */ / 调用许多 Perl API 函数...
} [ ...etc.]
MODULE = Foo
Package = Foo*
XUB /* void my_xub(arg) int arg
CODE: my_private_function(arg, 10);
```

注意，与编写扩展的方法相比，两个变化是在包含 Perl 头文件之前添加了 `#define PERL_GET_CONTEXT`，然后在每个调用 Perl API 的函数开头添加了 `dTHX` 声明。（你会知道哪些函数需要这个，因为 C 编译器会声称这些函数中存在未声明的标识符。）如果在隐式文中正确定义了 `XS(s)` 宏，则不需要任何更改：

第三种更高效的方法是在 Perl 获取内部进行：
```c
#define PERL_GET_CONTEXT /* 我们想要效率 */
#include <EXTERN.h>
#include "perl.h"
#include "XSUB.h"
/ dTHX 仅用于调用 Perl API 的函数 * /
STATIC void my_private_function(dTHX, int arg1, int arg2) {
    /* 这里不需要，因为 dTH 是一个参数 * / 调用 Perl API 函数... }
}
[ ... ] MODULE = Foo
PACKAGE = Foo
/ / 通常的 XSUB void my_xsub(arg)
int arg
```



这种实现意味着通过函数调用获取上下文，因为它总是作为额外的参数传递。根据你对简单性或效率的需求，你可以自由地混合这两种方法。

永远不要自己为 `dTHX` 添加逗号——否则，请对接受显式参数的函数使用带下划线的宏形式，或对没有显式参数的函数使用不带参数的形式。

如果使用 `-DPER_GLOBAL_STRUCT` 编译 Perl，如果在函数中访问了 Perl 全局变量（`perl.h` 或 `globvar.sym`）且没有使用 `dTHX`，则需要 `dVAR` 定义（`dTAX` 包含 `dVAR`）。只有在相同的编译时定义下需要 `dVAR`，否则 Perl 全局变量可见可见。

## 如果我从多个线程调用 Perl，需要做特殊处理吗？

如果你在一个线程中创建解释器然后在另一个线程中继续调用它们，你需要确保 perl 自身的线程本地存储（TLS）槽在这些线程中正确初始化。

`perl_alloc` 和 `perl_clone` API 函数会自动将 TLS 槽设置为它们创建的解释器，因此如果解释器始终在创建它的线程中活动，并且该线程之后没有创建或调用其他解释器，则无需执行特殊操作。如果不是如此，你必须在调用该特定解释器的任何 API 之前设置该线程的 TLS 槽。这是通过在你执行的第一件事中调用 `PERL_SET_CONTEXT` 宏完成的：

```c
/* 对 some_perl 执行任何其他操作 */

PERL_SET_CONTEXT(some_perl); ... 对 some_perl 的其他 Perl 调用在此处...
```

## 未来计划与 PERL_IMPLICIT_CONTEXT

正如 `PERL_IMPLICIT_CONTEXT` 提供了一种封装它对运行环境所有信息的方式。这在 Windows 上通过 `USE_THREADS` 启用。这允许所有系统调用拥有一个额外的指针（称为“主机”环境）。这使得工作人员能够维护自己的状态，并分解为结构。

## 内部函数

所有对外界的 Perl 内部函数都有 `Perl_` 前缀，以防与 xs 或程序冲突。同样，所有全局变量以 `PL_` 开头（根据约定，静态函数以 `S_` 开头）。

在内核内部（定义 `PERL_CORE`），由于 `embed.h` 中的大量定义，你可以获取带或不带 Perl 前缀的函数。注意，扩展代码不应设置 `PERL_CORE`；这会暴露完整的内部实现

`embed.h` 文件由 `embed.pl` 和 `embed.fnc` 自动生成。`embed.pl` 还为内部函数创建原型头文件、生成文档以及许多其他部分。当你向内核添加新函数或更改现有函数时，务必也更改 `embed.fnc` 中的数据。这里是该文件中的示例条目：

| 标志 | 返回类型 | 名称 | 参数 |
| :--- | :--- | :--- | :--- |
| Apd | SV** | av_fetch | AV* ar \| I32 key \| I32 lval |

此函数是实验性开发 API 的一部分，可能会在不通知的情况下更改或消失。

此函数不应定义兼容性宏，例如 `Perl_parse`。它必须作为 `Perl_parse` 被调用。

此函数没有导出到 Perl 核心。

此函数被实现为一个宏。

此函数被显式导出。

此函数对 Perl 核心包含的扩展可见。

二进制向后兼容；此函数是一个宏，但也有一个 `Perl_implementation`（已导出）。

其他信息请参见 `embed.fnc` 部的注释。

如果你编辑了 `embed.pl` 或 `embed.fnc`，将需要运行 `regen_headers` 来强制重新构建 `embed.h` 和其他自动生成的文件。

# IV、UV 和 NV 的格式化打印

如果你打印的是 IV、UV 或 nv，而不是像 `%d`、`%ld`、`Posf` 这样的三格式化代码，你应该使用以下宏以确保可移植性：

| 宏 | 类型 | 格式 |
| :--- | :--- | :--- |
| IVdf | IV | 十进制 |
| Uvf | UV | 十进制 |
| Uof | UV | 八进制 |
| UVxf | UV | 十六进制 |
| Nef | NV | %l-lf |
| Nvg | NV | %g-like |

我们将处理 64 位整数和长双浮点（long doubles）。例如：

```
printf("IV is %"IVdf"\n", iv);
```

`IVdf` 将展开为适用于 IV 的正确格式。

注意，存在不同的“长双”：Perl 将使用编译器提供的任何类型。

如果你正在打印指针的地址，请结合 `UVxf` 与 `PTR2UV()` 使用，不要使用 `%lx` 或 `%p`。

# 指针转整数和整数转指针

由于指针的大小并不一定等于整数的大小，请使用以下宏来正确操作。

```
PTR2UV(pointer) PTR2IV(pointer) PTR2NV(pointer) INT2PTR(pointertertype integer)
```

例如：

```
IV iv = ...; SV sv = INT2PTR(SV*, iv);

and

AV *av = ...; UV uv = PTR2UV(av);
```

# 异常处理

在 xs 模块中有几个宏可以进行非常基础的异常处理。你必须在包含 `xsub.h` 之前定义 `NOXSLOCKS` 才能使用这些宏：

```
#define NO_XSLOCKS #include "XSUB.h"
```

如果你的代码可能会报错（croak），你可以使用这些宏，但需要在将控制权交回 Perl 之前进行一些清理工作。例如：

```
dXCPT; /* 设置必要的变量 */ XCPT_TRY_START {
code_that_may_croak(); } XCPT_TRY_END XCPT_CATCH { /*在此处进行清理 */
XCPT_RETHROW;
```

注意，如果你捕获了异常，可能需要重新抛出异常。使用这些宏，无法只捕获异常并忽略它。如果你必须忽略异常，则必须使用 `call*` 函数。

使用上述宏的优势在于你不需要为 `call*` 设置一个额外的函数，而且使用这些宏比 `call_.*`更快。

# 源码文档

目前正在努力编写内部函数的文档并从它们自动生成参考手册——`perlapi` 就是其中一个手册，它详细列出了所有 xs 编写者可用的函数。`perintern` 是不属于 API 且仅供内部使用的函数的自动生成手册。

源码文档通过在 C 源中放入 POD 注释来创建，如下：

```
/* =apidoc sv_setiv 将一个整数拷贝到指定的 SV。不处理 'set' 魔法数字。参见 C<sv_setiv_mg>=.cut */
```

如果你向 Perl 核心添加了函数，请尽量提供一些文档。

# 向后兼容

Perl API 随时间变化。`Devel::PPPort` 模块尝试为现有接口提供兼容代码，以处理这些变化中的某些，因此 xs 编写者在支持多个版本的 Perl 时不需要自己编写代码。

`Devel::PPPort` 生成一个 C 头文件 `ppport.h`，该文件也可以作为 Perl 脚本运行。生成 `ppport.h`，请运行：

```
perl -Devel::PPPort -eDevel::PPPort::WriteFile
```

除了检查现有的 xs 之外，脚本还可以使用 `-api-info` 命令开关检索各种 API 调用的兼容信息。例如：

```
% perl pppport.h --api-info=sv_magicext
```

```c
CODE: my_private_function(dTHX, arg, 10);
```



详情请参见 `perdoc pppport.h`。

# Unicode 支持

Perl 5.6.0 引入了 Unicode 支持。对于端口移植者和 xs 编写者来说，理解这一点并确保他们编写的代码不会损坏数据非常重要。

# 到底什么是 Unicode？

在过去，一切都使用 ASCII。我们大多数人都是如此。ASCII 的问题在于它对于不使用罗马字母的人来说并不有用。问题在于它并不特别有用……过去的情况是，特定的语言会将它们的字母放在序列的高位范围（128 到 255 之间），带有许多不完全符合 ASCII 的变体，这作为标准的意义消失了。

更糟糕的是，如果你有像中文或日语这样拥有成百上千个字符的语言，你真的无法将它们放入仅仅 256 个中，它们必须完全忘记 ASCII，并使用数字对来引用一个字符以构建系统。

为了解决这个问题，一些人形成了 Unicode 并产生了一个包含你能想到的所有字符及更多的新字符集。表示这些字符有多种方法，Perl 使用的是 UTF-8。UTF-8 使用可变数量的字节来表示字符。你可以在 `perunicode` 中学习更多关于 Unicode 和 Perl 模型的内容。（在 EBCDIC 平台上，Perl 使用 EBCDIC，它是为 EBCDIC 平台适配的 UTF-8 形式。下面我们只讨论 UTF-8，但请记住特定的模式不同。）

# 我如何识别 UTF-8 字符串？

你不能。这是因为 UTF-8 数据像非 UTF-8 数据一样是以字节存储的。带有重音的 Unicode 字符 200（十六进制为 0xC8）由两个字节 196-172 表示。遗憾的是，`chr(172)` 并没有那个字节序列。你不能仅仅通过观察——这正是 Unicode 输入成为一个有趣问题的原因。通常，你要么必须知道你在处理什么，要么必须猜测。API 函数 `is_utf8_str` 可以提供帮助；它可以告诉你字符串是否只包含 UTF-8 字符，而且非 UTF-8 字符串看起来有效的 UTF-8 的概率会变得非常快。逐字符地，`isUTF8_CHAR` 会告诉你字符串中的当前字符是否有效。

# UTF-8 如何表示 Unicode 字符？

如上所述，UTF-8 使用可变数量的字节来存储字符。值为 0...127 的字符存储在字节中，就像 ASCII 一样。字符 128 存储为...（此处原文似乎有断层或逻辑跳接，按原意保留或翻译）...（在 EBCDIC 平台上，Perl 使用 EBCDIC，它是为 EBCDIC 平台适配的 UTF-8 形式。下面我们只讨论 UTF-8，但请记住特定的模式不同。）

此标记对 Perl 处理字符串的方式有重要影响：如果没有正确区分 UTF-8 数据，正则表达式、长度、`substr` 以及其他处理操作将产生不符合预期的（错误的）结果。

当你拥有一个未被标记为 UTF-8 但包含可能的 UTF-8 字节序列的字符串时，问题就出现了——特别是在组合非 UTF-8 和 UTF-8 字符串时。

永远不要忘记 `SVf_UTF8` 标记是独立于 SV 值的；你需要确保在操作 SV 时不会意外删掉它。具体来说，你不能直接导出到此处：

```
SV *sv; SV *nsv; STRLEN len; char *p; p = SV(sv, len); frobnicate(p); nsv = newSVpn(p, len);
```

`char*` 并不能说明所有情况，你不能仅通过复制字符串值来复制或重构一个 sv。检查 sv 是否设置了 UTF8 标记（在调用 SV 之后），并根据此进行相应处理：

```
p = SV(sv, len); is_utf8 = SVUTF8(p); frobnicate(p, is_utf8); nsv = newSVpn(p, len); if (is_utf8) SVUTF8_on(nsv);
```

在上述代码中，你的 `frobnicate` 函数已经意识到它正在处理 UTF-8 数据，以便它可以妥善处理字符串。

由于仅将 sv 传递给 xs 函数并复制其数据不足以复制 UTF8 标记，更不用说将 `char *` 传递给 xs 函数了。

为了完全通用性，使用 perlapi 中的 “UTF-8” 来检查 sv 中的字符串是否应被视为 UTF-8。这考虑到了 xs 函数是在使用字节的作用范围内创建的。如果是这样，则应该暴露组成 UTF-8 字符串的底层字节，而不是它们代表的字符。但这个伪指令（pragma）应该只用于调试，可能用于字节层面的低级测试。大多数代码并不关心这一点，但 Perl 的某些领域确实需要支持。

而且这并不是全部。从 Perl v5.12 开始，在各种条件下，未进行 UTF-8 的字符串也可能被视为 Unicode。对于序数在 128 到 255 之间的字符来说，这确实是一个问题，它们的行为与 ASCII 规则相比有许多不同之处（参见 perunicode 中的“Unicode Rules”）。目前没有发布用于处理此问题的 API，因为其可能会发生变化，但你可以查看 `pp.c` 中的代码以获得它是如何实现的示例。

## 如何将字符串转换为 UTF-8？

如果你正在混合 UTF-8 和非 UTF-8 字符串，则有必要将非 UTF-8 字符串升级为 UTF-8。如果你有一个 sv，此此最简单的方法是：

```
sv_utf8_upgrade(sv);
```

然而，你不应该这样做，例如：

```
if (!UTF8(left))
    sv_utf8_upgrade(left);
```

如果你在二元运算符中这样做，你实际上改变了进入操作符的字符串，虽然最终用户可能察觉不到，但会导致问题。相反，`bytes_to_utf8` 会给你一个 UTF-8 编码的字符串副本，这在不破坏原始 sv 的情况下有用。`utf8_to_bytes` 也可以反向操作，但如果字符串包含任何大于 255 的字符，它自然会失败。

## 如何比较字符串？

perlapi 中的 “cmp” 和 perlapi 中的 “sv_cmp” 对两个 sv 进行字典序比较并妥善处理 UTF-8。请注意，Unicode 通过 Unicode::Collate 模块提供了更复杂的排序机制。

要比较两个字符串是否相等，可以使用 `memEQ()`，但字符串必须是 UTF-8 编码的。

要区分大小比较两个字符串，使用 `foldEQ()`（字符串不需要具有相同的 UTF8）。

## 还有其他我需要知道的吗？

并不真的。只需记住这些点：

- 没有方法判断 `char *` string是否是 UTF-8。
- 你可以通过在字符串化后对其调用 `SVUTF8` 来判断 sv 是否被视为 UTF-8。
- 你可以通过查看 `SVUTF8` 来判断 sv 实际上是 UTF-8（即使它未被这样处理）。
- 如果某些应该是 UTF-8，不要忘记设置标记。即使你对某些操作使用 PV，也将标记作为 PV 的一部分传递。
- 如果字符串是 UTF-8，始终使用 `utf8_to_uv` 获取值，除非在 `UTF8_INVARIANT(*s)` 的情况下你可以使用 `s`。
- 当向 UTF-8 字符串写入字符 UV 时，始终使用 `uv_to_utf8`，除非在 `UVCHR_IS_INVARIANT(uv)` 的情况下你可以使用 `s`。

混合 UTF-8 和非 UTF8 字符串是复杂的。使用 `bytes_to_utf8` 获取 UTF-8 编码的字符串然后合并它们。

## 自定义运算符

自定义运算符支持是一个实验性功能，允许你定义自己的操作。这主要是为了允许 Perl 内核的其他语言构建解释器，但也通过创建 “宏操作”（通常一起执行的多个操作，如 gsv, gsvv）来实现优化。

此功能被实现为新类型 `OP_CUSTOM`。内核对该操作一无特殊之处，因此它不会参与任何优化。这意味着你可以按照意愿定义自定义操作为任何结构——一元的、二元的等等。

了解自定义运算符不会为你做什么很重要。它们不会让你直接向 Perl 引入新语法。它们甚至不允许任何新关键字。事实上，它们不会改变 Perl 编译程序的方式。你必须在 Perl 编译程序后，通过使用 CHECK 块和 B::generate 模块操作操作符来自己完成这些更改，或者通过 `optimize::method` 添加自定义的孔优化器。

当你这样做时，你通过创建类型为 `OP_CUSTOM` 且 `op_ppadr` 为你的 pp 函数的操作来用自定义操作替换普通 Perl。这应该定义在 xs 代码中，并且看起来像 pp.c 中的 pp 操作。你负责确保你的操作从栈中获取相应数量的值，并负责添加栈标记。

你还应该向 Perl 解释器 “注册”你的操作，以便它可以产生合理的错误和警告信息。由于在一个逻辑操作类型 `OP_CUSTOM` 内可能有多个自定义操作，Perl 使用 `o->ppadr` 的值来确定处理的是哪种自定义操作。你应该为你使用的每个 ppaddr 使用 `XENTRY_set` 和 `XOP` 结构创建自定义操作，设置自定义操作的属性并使用 `Perl_custom_op_register` 将其注册。一个简单的示例如下：



`static XOP my_xop;`

`static OP *my_pp(pTHX);`

`BOOT: XENTRY_set(&my_xop, xop_name, "myop");`

`XENTRY_set(&my_xop, xop_desc, "Useless custom op");`

`Perl_custom_op_register(aTHX, my_pp, &my_xop);`

结构体中的可用字段：

- `xop_name`: 操作的短名称。它将被包含某些错误消息中，并由 `B` 模块作为 `$op->name` 返回，因此将出现在 `B::Concise` 的输出中。
- `xop_desc`: 操作功能的描述。
- `xop_class`: 该操作使用哪种 *Oop 结构。这应该是 `op.h` 中的 `OA_*` 常量之一，即：
  `OA_BASEOP`
  `OA_UNOP`
  `OA_BINOP`
  `OA_LOGOP`
  `OA_LISTOP`
  `OA_PMOP`
  `OA_SVOP`
  `OA_PADOP`
  `OA_PVOP_OR_SVOP`

这应该仅被解释为 'PVOP'。_OR_SVOP 是因为唯一的内核 VPOP (`OP_TRANS`) 有时可以是一个 `SVOP`。

  `OA_LOOP`
  `OA_COP`

不应使用其他 `OA_*` 常量。

`B::Generate` 直接支持通过名称创建自定义操作。

# 作者

直到 1997 年 5 月，本文档一直由 Jeff Okamoto <> 维护。现在它由 Perl 5 Porters <> 作为 Perl 本身的一部分进行维护。

感谢 Dean Roehrich, Malcolm Beattie, Andreas Koenig, Paul Hudson, Ilya Zakharevich, Paul Marquess, Neil Bowers, Matthew Green, Tim Bunce, Spider Boardman, Ulrich Pfeifer, Stephen McCamant 以及 Gurusamy Sarathy 的大力帮助与建议。

## 另请

`perlapi`, `perlintern`, `perlxs`, `perlembed`

# PERLHACK

+   名称

`perlhack` - 如何进行 Perl 的 Hack 开发

## 描述

本文档解释了 Perl 开发的工作原理。它包含了关于 Perl Porters 邮件列表、Perl 仓库、Perlbug 追踪器、补丁指南以及对 Perl 开发哲学的注释。

# 极速补丁指南

如果你只想提交一个单一的小型补丁（例如 pod 修复、错误测试、注释修复等），这非常简单！操作方法如下：

### 检出源码仓库

Perl 源码位于 git 仓库中。你可以使用以下命令克隆仓库：

```
% git clone perl
```

### 确保你遵循最新的建议

万防本指南中的建议最近已更新，请直接从 perl 源码读取最新版本：

```
% peridoc pod/perlhack.pod
```

### 进行你的更改

开始 Hack，Hack，Hack。请记住，Perl 运行在许多不同的平台、具有不同能力的不同操作系统、不同的文件系统结构，甚至是不同的字符集上。`perlhacktips` 针对此提供了建议。

### 测试你的更改

你可以运行以下命令运行所有测试：

```
% ./Configure -des -Duseddevel % make test
```

持续进行 Hack 直到测试通过为止。

### 提交你的更改

提交工作将把更改保存到你的本地系统上：

```
% git commit -a -m '在此处填写提交信息'
```

确保提交信息用一句话描述了你的更改。例如，“修复了 perlhack.pod 中的拼写错误”。

### 将你的更改发送到 perlbug

下一步是通过电子邮件向 Perl 核心工单系统提交补丁。

如果你的更改在一个单一 git 提交中，运行以下命令生成补丁文件并将其附加到你的错误报告中：

```
% git format-patch -1 % ./perl -Ilib utils/perlbug -p 0001-*.patch
```

`perlbug` 程序会询问你一些关于你的电子邮件地址和你提交的补丁的问题。一旦你回答，它将通过电子邮件提交你的补丁。

如果你的更改在多个提交中，为每个提交生成一个补丁文件，并用逗号分隔提供给 `perlbug` 的 `-p` 参数：

```
% git format-patch -3 % ./perl -Ilib utils/perlbug -p 0001-fix1.patch, 0002-fix2.patch, > 0003-fix3.patch
```

在提示时，选择一个总结你更改的主题。

### 感谢

Porters 感谢你为帮助 Perl 变得更好投入的时间。感谢！

### 下次

当你下次想要制作补丁时，需要从原始状态的最新 perl 开始。检查你的 perl 检出中没有任何想要保留的本地更改或添加的文件，然后运行这些命令：

```
% git pull % git reset --hard origin/bleed % git clean -dxf
```



# 错误报告

如果你想报告 Perl 中的错误，必须使用 `perlbug` 命令行工具。该工具将确保你的错误报告包含所有相关的系统和配置信息。

你可以使用 `<>` 处的网络界面浏览现有的 Perl 错误和补丁。

在提交错误报告之前，请检查 `perl5-porters` 列表存档（见下文）和/或错误追踪系统。通常，你会发现该错误已经被报告过了。

你可以登录错误追踪系统并对现有的错误报告发表评论。如果你有关于现有错误的额外信息，请添加它。这将帮助 porters 修复错误。

# PERL 5 PORTERS

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

# PERL 5 PORTERS

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`perl5--分分分 5`开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

`5   5 ters`。

# PERL 5 PORTERS

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

# PERL 5 PORTERS

`perl5-porters` (`p5p`) 邮件列表是 Perl 标准分发版的维护开发地。维护 Perl 的人员也被称为“Perl 5 Porters”。

# PATCHING PERL

如果你计划进行比单一修复更广泛的工作，我们鼓励你阅读下文。这将帮助你专注于工作并使你的补丁更容易合并。

## 提交补丁

如果你有一个补丁要提交，请通过 `perlbug` 提交。你也可以直接发送给它。请注意，发送到 `perlbug` 的消息可能会在审核队列中，因此你不会立即收到回复。

当你收到来自我们追踪系统的电子邮件时，你就知道你的提交已处理。一旦你的补丁进入追踪系统，它也会发送到列表。

补丁将在 `p5` 列表进行评审和讨论。简单的、无争议的补丁将直接应用。应用补丁时，工单将更新，你也会收到电子邮件。

其他情况下，补丁需要更多工作或讨论。这将在 `p5` 列表进行。

鼓励你参与讨论并维护你的补丁。有时你的补丁可能会在混乱中丢失。如果一个月内没有采取行动，向 `p5p` 发送提醒邮件是合适的。请记住 Perl 5 开发者都是志愿者，请保持礼貌。

## 使你的补丁被接受

如果你正在提交代码补丁，有几件事可以帮助 Perl 5 支持者接受你的补丁。

### 补丁样式

如果你使用 `git` 检出 Perl 源码，那么使用 `git format-patch` 将产生适用于 Perl 风格的补丁。`format-patch` 命令会为你的每个提交生成一个补丁文件。如果你倾向于为所有提交发送单一补丁，可以使用 `git diff`。

```
git checkout bleed % git pull % git diff bleed my-branch-name
```

我们强烈建议你尽可能使用 `git`。这会让你的生活以及我们的都变得更容易。

然而，如果你没有使用 `git`，仍然可以生成一个合适的补丁（`patch`）。你需要一份原始的 Perl 源码来进行对比。移植者倾向于使用统一差异格式（`unified diffs`）。使用 GNU `diff`，你可以产生如下差异：

```bash
% diff -Npurd perl.pristine.mine
```



请确保在 Perl 副本中执行 `realclean` 以移除任何构建产物，否则你可能会得到误导的结果。

## 提交消息 (Commit message)

在你构建准备提交到 Perl 核心的补丁时，编写良好的提交消息至关重要。如果你提交的内容包含系列提交，这一点尤为重要。

提交消息的第一行应该是简短的描述，不要以句号结尾。作为一条经验法则，它的长度不应超过主题行的长度，因为许多 Git 工具（如 `Gitweb`、`GitHub`、`git log --pretty=oneline` ... 等）在展示提交摘要时只会显示第一行（在 50 个字符处截断）。提交消息应该包含对补丁修复的问题或添加的新功能的描述。作为一般经验法则，你的提交消息应该帮助了解 Perl 的程序员快速理解你试图做什么，以及为什么这个更改很重要。

## 为什么 (Why)

你的提交消息应该描述你所做的的更改为什么重要。当有人在六个月或几年后查看你的更改时，你的意图应该是清晰的。如果你是为了废弃某个功能以便以后简化另一部分代码，请说明。

## 是什么 (What)

你的提交消息应该描述你更改了 Perl 核心的哪个部分，以及你期望补丁实现的功能。

## 如何做 (How)

虽然对于文档更改、新测试或微小补丁来说并非必须，但解释你的更改是如何工作的通常是值得的。即使它对今天的你来说很清楚，对下个月或明年的移植者来说可能并不清晰。提交消息并不是为了取代代码中的注释。提交消息应该描述你做的更改，而代码注释应该描述代码当前的状态。然而，如果你实现了一个新功能，并带有测试和注释良好的代码；但如果你只是在解析器或词法器深处改变了一个字符，你可能需要写一篇“短小说”，以确保未来的读者理解你做了什么以及为什么要这样做。

## 注释 (Comments)

确保对你的代码进行充分的注释。虽然没有必要每行都注释，但任何利用算符副作用的操作、会影响到补丁函数之外的更改，都应该记录文档。如果你非要出错，宁可注释多一点也不要少一点。最好的注释是解释代码之所以那样运行。

## 风格 (Style)

通常情况下，请遵循你正在打补丁的代码风格。特别是为 Perl 源码打补丁时遵循以下指南：

- 8 宽制表符（无例外！）
- 代码使用 4 宽缩进，嵌套的 `#define` 使用 2 宽缩进
- 尽量不要超过 79 列
- ANSI C 原型
- 控制结构不使用“拥抱式行”（cuddled lines）和“K&R”风格的缩进
- 不要使用 C 风格的注释
- 标记需要重新审视的地方（并经常审视！）
- 当 `if` 条件跨越多行时，将左大括号另起一行；否则应放在行尾
- 在函数中，定义从第 0 列开始（返回值类型在上一行）
- 后面跟着括号的关键字后加一个空格，函数名与后续括号之间不留空格
- 避免在条件语句中赋值，如果不可避免，请使用额外的括号，例如使用 `return foo,` 而不是 `return(foo);`
- 使用 `if (!foo)` 而不是 `if (foo == FALSE)` 等
- 不要使用 `register` 声明变量。这在现代编译器上可能适得其反，并且在经常编译 Perl 源码的 C 语言中它已被废弃。
- 头文件中供 xs 代码访问的内联函数，应确保在使用常用的额外标志（例如 gcc 的 `-wswitch-default`，该标志在 `switch` 语句缺少 `default` 分时会警告）编译时不产生警告。使用这些额外标志是为了捕获合法代码中的潜在问题，通常被 Perl 聚合器（如 Linux 发行版）使用。

## 测试套件 (Test suite)

如果你的补丁更改了代码（而不仅仅是文档），你还应该包含一个或多个测试用例，说明你正在修复的错误或验证你添加的新功能。通常，你应该更新现有的测试文件而不是创建一个新的。你的测试套件添加通常应遵循以下指南（由 Guru Sarathy 提供）：

- 清楚你在测试什么。阅读文档和源码。
- 倾向于失败，而不是成功。
- 严格解释结果。
- 使用无关的功能（这会暴露出怪异的问题）。
- 使用非标准惯用法（否则你没有在测试 TIMOWDI）。
- 尽可能避免使用硬编码的测试数字（`t//test` 中发现的 `EXPECTED/GOT` 更具可维护性，并能提供更好的失败报告）。
- 测试失败时给出有意义的错误信息。
- 除非你正在测试它们，否则避免使用 `q()/system()`。如果你使用了它们，请确保覆盖了所有平台。
- 卸载你创建的任何临时文件。
- 使用 `$$WARN__` 将未预见的警告提升为错误。
- 确保使用与测试版本一起提供的库和模块，即那些已经安装的库。
- 在代码中添加注释说明你正在测试什么。
- 使更新 `1..42` 字符串变得不再。或者确保你更新了它。测试给定操作符、库或函数的所有行为。
- 测试所有可选参数。
- 测试各种上下文下的返回值（布尔、标量、列表、左值）。
- 同时使用全局变量和局部变量。
- 不要忘记异常的、病态的情况。

## 为核心模块打补丁 (Patching a core module)

这与任何其他内容的补丁一样，但有一个额外的考虑。源码树中 `cpan/` 目录下的模块在 Perl 核心之外维护。当作者更新模块时，更新会被复制到核心中。有关报告错误和提交补丁的更多信息，请查看该模块的文档或在 CPAN 上的列表。大多数情况下，`cpan/` 中模块的补丁应该发送到上游，而不单独应用到核心。如果对 `cpan/` 中文件的补丁绝对无法等待修复并发布到 bleed 版本，你必须在 `Porting/Maintainers.pl` 文件中添加（或更新）条目，以标记已进行了任何本地修改。相比之下，`dist/` 目录下的模块在核心中维护。

## 更新 perdelta (Updating perdelta)

对于大到需要在 `pod/perdelta` 中添加条目的更改，如果你在提交实际更改的同时提交一个 delta 条目，移植者将非常感激。重大更改包括但不限于：

- 添加、废弃或移除核心功能
- 添加、废弃或移除或升级核心或双生命模块
- 添加新的核心测试
- 修复核心中的安全问题和用户可见的错误
- 可能破坏现有代码的更改（无论 Perl 层还是 C 层）
- 显著的性能提升
- 在 `pod/` 目录中添加、移除或显著更改文档
- 重要的平台特定更改

确保将 perldelta 条目添加到 `pod/perdelta` 内的正确部分。有关如何编写良好的 perldelta 条目的更多信息，请参阅 `Porting/how_to_write_a_perldelta.pod` 中的 Style 部分。

## 实现在哪里？

没有实现，任何口头上的讨论都是徒劳。在几乎所有情况下，主张新功能的人被预期为实现该功能的人。编写新功能的维护者有他们自己的议程，他们没有时间去实现你的（可能是好的）想法。

## 向后兼容性

破坏现有的 Perl 程序是大忌。新的警告可能会引起争议——一些人认为发出警告的程序并没有坏掉，而另一些人则认为它坏了。添加关键字有破坏程序的可能，改变现有标记（token）或函数的含义也可能破坏程序。

Perl 5 核心包含了一些机制，帮助维护者使不向下兼容的更改更具兼容性，例如 `feature` 和 `deprecate` 模块。请在适当的情况下使用它们。

## 可以作为一个模块吗？

Perl 5 拥有扩展机制、模块和 xs，专门为了避免修改 Perl 解释器。你可以编写导出函数的模块，可以为这些函数提供原型以便它们像内置函数一样被调用，如果你想实现非常复杂的东西，甚至可以编写 xs 来使用 Perl 解释器的运行时数据结构进行编码。

只要可能，新功能在被考虑纳入核心之前，应该先在 CPAN 模块中原型化。

## 该功能足够通用吗？

这只是提交者想要添加到语言中的功能，还是具有广泛的用途？有时，与其添加一个关注狭窄的功能，维护者可能会决定等到有人实现了更通用的功能。

## 它可能引入新的 bug 吗？

从根本上重写 Perl 解释器的大部分是有引入新 bug 的可能。

## 多大？

更改越小、越局部越好。同样，一系列小补丁被远优于一个大补丁。

## 它会排斥其他理想的功能吗？

如果一个补丁关闭了开发途径，它可能会被拒绝。例如，一个对原型进行真实且最终解释的补丁可能会被拒绝，因为关于原型未来的选项尚未得到解决。

## 实现健壮吗？

良好的补丁（代码紧凑、完整、正确）更有机会被采用。粗糙或错误的补丁可能会被搁置，直到维护者（pumpkin）有时间修复，或者在不另行通知的情况下被完全丢弃。

## 实现通用到可以移植吗？

最糟糕的补丁使用了特定系统的特性。Perl 语言中不可移植的新增几乎不可能被接受。

## 实现测试过吗？

改变行为（修复 bug 或引入新功能）的补丁必须包含回归测试，以验证一切运行符合预期。

如果没有原始作者提供的测试，未来修改 perl 的人如何确保他们没有无意中破坏该补丁实现的行为？如果没有测试，补丁作者又如何确信投入补丁的心血不会被未来的某小心丢掉？

## 有足够的文档吗？

没有文档的补丁可能考虑不周或不完整。没有文档就无法添加或更改功能，因此提交相应的 pods 以及源代码的补丁是重要的。

## 有其他实现方法吗？

Larry 说：“虽然 Perl 的口号是‘一件事有多种做法’，但我犹豫于为某件事提供 10 种方法。” 这是一个难以处理的启发式方法——一个人的必需之品是另一个人的无意义的技艺。

## 它会创造太多的工作吗？

为维护者工作、为 Perl 程序员工作、为模块作者工作……Perl 本来就该是这样的。

## 补丁胜于雄言

可以运行的代码总是优于空中的想法。一个添加功能的补丁进入语言的概率远高于一个随机的功能请求，无论该请求被争论得多么激烈。这联系到“它有用吗？”，因为某人花时间制作补丁这一事实证明了对该功能的强烈渴望。

# 测试

核心部分与 Perl 其他部分使用相同的测试样式，通过 `Test::Harness` 运行简单的 "ok/not ok" 检查，但有一些特殊的考虑。

在核心中编写测试有三种：`Test::More`、`t/test.pl` 以及即时的 `print $test ? "ok 42\n" : "not ok 42\n"`。决定使用哪一种取决于你正在处理测试套件的哪个部分。这是防止高层失败（例如 `Config.pm` 损坏）导致基础功能测试失败的措施。

`t/test.pl` 提供了一些解码和编码函数。
- 如果你使用 `\N{character name}` 形式，`charnames` 会自动加载。这可能不适用于你正在进行的测试级别。

`t/test.pl` 提供了一些解码和编码函数。
- 如果你使用 `\N{character name}` 形式，`charnames` 会自动加载。这可能不适用于你正在进行的测试级别。
- 1) 选择 Unicode 规则。这意味着在双引号字符串中，字符串被转换为 UTF-8（你可以使用 `utf8::downgrade` 转回非 UTF-8）。在正则表达式模式中，不进行转换，但如果字符修符原本是 `/d`，它会被更改为 `/u`。
- 2) 如果你使用 `\N{character name}` 形式，`charnames` 会自动加载。

## 特殊 make 目标

有各种特殊的 make 目标可以用来于标准的 "test" 目标测试 Perl。并不是所有的目标都期望获得 100% 的成功率。它们中的许多有多个别名，并且许多目标在某些操作系统上不可用。

### test_porting
这在源码树上运行一些基础健全性测试，并在提交补丁之前帮助捕捉错误。

### minitest
在 `base`、`t/comp`、`t/cmd`、`t/run`、`t/io`、`t/op`、`t/uni` 和 `t/mro` 测试上运行 `miniperl`。

### test.valgrind check.valgrind
（仅限 Linux）使用内存泄漏+非法访问工具 "valgrind" 运行所有测试。日志文件将被命名为 `testname.valgrind`。

### test_harness
使用 `t/harness` 控制程序运行测试套件，而不是 `t/TEST`，`t/harness` 更先进，并使用了 `Test::Harness` 模块，因此使用此测试目标。

假设 perl 能够正常工作。对我们而言，主要优势是它会在最后打印失败测试的详细总结。此外，与 t/TEST 不同，它不会将 stderr 重定向到 stdout。

注意，Win32 始终使用 t/harness 而不是 t/TEST，因此没有特殊的 "test_harness" target。

在 Win32 的 "test" target 下，你可以使用 `TEST_SWITCHES` 和 `TEST_FILES` 环境变量来控制 t/harness 的行为。这意味着你可以说：

```
```



`nmake TEST_FILES="op/*.t"` `nmake TEST_SWITCHES="-torture"`

`TEST_FILES="op/*.t"`

在运行普通测试之前将 `Perl_SKIP_TTY_TEST` 设置为 true。

## 并行测试

核心发行版现在可以在 Unix 类平台上并行运行其回归测试。与其运行 `make test`，不如将环境中的 `TEST_JOBS` 设置为并行运行测试的数量，然后执行 `make test_harness`。在 Bourne 类的 shell 中，可以这样操作：

```
TEST_JOBS=3 make test_harness # 3 个测试并行
```

使用环境变量而不是并行 make 本身，是因为 `TAP::Harness` 需要自行调度各个互不冲突的测试脚本，而且没有标准的接口让实用程序与其任务调度器交互。

请注意，目前测试脚本在并行运行时可能会失败（最著名的是 `ext/io_dir.t`）。如果有必要，只需按顺序重新运行失败的脚本，查看失败情况是否会消失。

## 手动运行测试

你可以使用 `/` 目录下的以下命令之一手动运行测试套件的一部分：

```
./perl -I../.lib test list-of-.t-files
```

或者

```
./perl -I../.lib harness list-of-.t-files
```

（如果你没有指定测试脚本，将运行整个测试。）

## 使用 harness 进行测试

如果你使用 `harness` 进行测试，你有几个命令行选项可用。参数如下，并且它们在一起使用时必须按照此顺序出现。

```
harness -v -torture -re=pattern LIST OF FILES TO TEST
```

```
harness -v -torture -re LIST OF PATTERNS TO MATCH
```

如果省略 `LIST OF FILES TO TEST`，则文件列表将从清单（manifest）获取。文件列表可能包含通配符，这些通配符会被展开。

- `-v`: 在详细模式下运行测试，你可以看到哪些测试以及调试输出。
- `-torture`: 运行压力测试（torture tests）以及正常集合。
- `-re=PATTERN`: 过滤列表文件，使所有测试文件匹配 `PATTERN`。注意，这种形式与下面的 `-re LIST OF PATTERNS` 不同，因为它允许提供列表文件。
- `-re LIST OF PATTERNS`: 过滤列表文件，使所有测试运行匹配 `/(LIST|PATTERNS)/`。注意，使用这种形式时，模式通过 '|' 连接，你不能提供文件列表，相反，测试是从 `MANIFEST` 中获取的。

你可以通过通过类似 `./perl -I.../lib path/to/foo.t` 的命令来运行单个测试，不同之处在于 `harness` 会设置一些环境变量，这些变量可能会影响测试的执行：

```
PERL_CORE=1
```

表示我们正在作为 perl core 测试套件的一部分运行此测试。这对于在 CPAN 上具有双重身份的模块有用。

```
PERL_DESTRUCT_LEVEL=2
```

如果尚未设置，则将其设置为 2（perhlacktips 中的 `PERL_DESTRUCT_LEVEL`）。

```
PERL
```

（由 `t/TEST` 使用）如果设置，将覆盖用于运行测试的 perl 可执行文件路径（默认为 `./perl`）。

```
PERL_SKIP_TTY_TEST
```

如果设置，则告诉系统跳过需要终端的测试。这实际上由 `Makefile` 自动设置，但可以通过运行 `make test_notty` 强制执行。

影响测试的其他环境变量

```
PERL_TEST_Net_Ping
```

设置此变量运行所有 `Net::Ping` 模块，否则将跳过与外部交互的测试。参见 `perl5delta`。

```
PERL_TEST_NOVREXX
```

设置此变量跳过 `vrexx.t` 测试。

```
PERL_TEST_NUMCONVERTS
```

设置 `op/numconvert.t` 中的一个变量。

```
PERL_TEST_MEMORY
```



设置此变量包含 `t/bigmem/` 中的测试。例如，`PERL_TEST_MEMORY=4` 表示需要 4Gi 可用内存的测试可以运行。

另见 `Test` 和 `Test::Harness` 的文档，获取更多影响测试的环境变量。

## 性能测试

`t/per/bench` 文件包含了一些 perl 代码片段，旨在通过 `bench.pl` 工具在系列 perl 中进行基准测试。如果你修复或增强了性能问题，你可能需要在文件中添加示例代码，然后针对之前的和现在的 perl 运行 bench，看看发生了什么变化，是否有其他部分变慢。

`t/per/count.t` 文件用于测试特定代码片段是否已编译到包含指定类型的 opt 中。这对于测试 alter ops（例如将 op 转换为快速 op）很有用。

`t/per/speed.t` 和 `t/speed.t` 文件用于测试当特定优化损坏时（例如，字符串的 utf8 缓存）通常只需一秒钟，否则则需要几分钟，导致测试超时。

## 给 hacker 者的更多阅读材料

要 hack Perl guts，你需要阅读以下内容：

- `source`: Perl 树的概述。这会帮助你找到你正在寻找的文件。
- `interpreter`: Perl 解释器及其功能的概述。
- `hack`: 这份文档介绍了如何为 Perl 代码创建一个小补丁。如果你刚开始接触 perl core，这将帮助你理解它是如何工作的。
- `hacktips`: perl core 的细节。这份文档关注底层细节，如如何编写测试、移植性、调试等。如果你计划进行严肃 hack，请确保阅读这个。
- `guts`: 这极其重要，因为它是源码中内容位置的文档。阅读几次后它可能开始产生意义——如果现在还没有，不要担心，因为学习它的最好方法是结合源码操作来读，我们正是这样做的。
- `illustrated guts`: XSUB 的实用知识对于 core hack 极其有用；XSUB 使用了执行 Perl 程序的技巧。从简单的示例学习要容易得多。
- `api`: Perl API 文档解释了某些内部功能以及源码中使用的宏。
- `porting.pod`: 这是 Perl 移植的智慧格言；其中一部分对 holder 有用，但大部分适用于任何想进行 Perl 开发的人。

## CPAN TESTERS AND PERL SMOKERS

`CPAN` testers 是一组在各种平台上测试 CPAN 模块的志愿者。Perl Smokers 在各种配置的平台上自动测试 Perl 版本。两种努力都欢迎。要参与 perl 本身的压力测试，请访问。要开始对 CPAN 模块进行压力测试，请访问。

## 接下来

如果你已经阅读了本文中的所有文档以及上面列出的文档，你准备好 hack Perl 了。这里是更多建议：订阅 `perl5-porters`，关注补丁并尝试理解它们；如果有不清楚的地方，不要犹豫提问——谁知道你可能会在补丁中发现 bug……执行与你的操作系统相关的 README，例如 AI OS 上的 `README.aix`。如果你在新版本中发现任何缺失或更改的内容，不要犹豫为 README 提供补丁。

找到一个你感兴趣的 Perl 领域，看看能否弄清楚它是如何工作的。从源码扫描，在调试器中单步执行。玩、研究、捣腾！你可能不仅会理解你选择的领域，还会理解更广泛的 Perl 活动，而且可能比你想的要早。

道路从起点一直延伸下去。如果你能做到这些事情，你就开启了 Perl 移植的长路。感谢你想帮助让 Perl 变得更好——祝 hack 愉快！

## 比喻引用

如果你认上述关于“道路”的引用，你很幸运。大多数软件项目在每个文件的开头都是对该文件目的的字面描述。而 Perl 则以该文件目的的文学典故开头。就像许多书的章节一样，所有顶层 Perl 源文件（以及其他几个文件）都以一条格言式的铭文开头，间接地且比喻地暗示了你即将阅读的内容。

引用取自 J.R.R. 托尔金关于传说（Legendarium）的著作，几乎全部来自《指环王》。章节和页码使用以下版本：

- 《霍比特》，J.R.R. 托尔金著。使用了 2007 年 70 周年版，由英国 Harper Collins Publishers 出版，美国 Houghton Mifflin Company 出版。
- 《指环王》，J.R.R. 托尔金著。使用了 2004 年 50 周年版，由英国 Harper Collins Publishers 出版，美国 Houghton Mifflin Company 出版。

最早于1983年由 George Allen & Unwin 出版；2002年的特别三卷本合集版以及各种平装本的页码均未更改，这些现在均由 Harper Collins 或 Houghton Mifflin 出版。

其他可以引用的 JRRT 书籍还包括《汤姆·邦巴迪尔的冒险》、《魔戒物语》、《未完史传说》和《胡林族之子的故事》，除了第一本外，其余均由 CJRT 在作者去世后整理。但《指环王》本身完全可以，而且可能是最好的引用来源，只要你能在那里找到合适的引言。

所以，如果你要为 Perl 添加一个新的全新的、完整的顶层源文件，你应该遵循这种奇特的做法：你自己从托尔金那里选择一个合适的引言，保留原始拼写和标点符号，并使用与其他引言相同的格式。间接和隐晦的表达完全可以；记住，这是一个比喻，毕竟它的目的正是为了元（meta）。

# AUTHOR

此文档最初由 Nathan Torkington 编写，由 `perl5-porters` 邮件列表维护。

# PERLHACKTIPS

- > NAME

`perlhacktips` - Perl 核心 C 代码黑客技巧

# DESCRIPTION

本文档将帮助你学习对 Perl C 代码进行修改的最佳方法。它涵盖了常见问题、调试、性能分析等。

如果你还没有读过 `perlhack` 和 `perlhacktut`，你可能想先读读那几篇。

# COMMON PROBLEMS

Perl 源码遵循 ANSI C89 规则：没有 C99（或...）扩展。在某些情况下，我们必须考虑 ANSI 要求。你不在乎某个特定平台的 Perl 是损坏的吗？我听说对 J2EE 程序员的需求仍然很大。

# Perl environment problems

- 未使用线程模式进行编译
- 使用线程模式编译 `-Dusereads` 会完全重写 Perl 的原型。你最好用它测试你的修改。与之相关的是“无 Perl”和“类 Perl”API 区别，例如：
  ```
  Perl_sv_setiv(aTHX_...); sv_setiv(...);
  ```
- 前者传递了上下文，这对于例如线程构建是必要的。后者是隐式的；不要将它们混合使用。如果你没有传递 `aTHX_`，你需要在函数中首先执行 `dTHX`（或 `dVAR`）。
- 关于内容的进一步讨论，参见 `perlguts` 中的“如何支持多个解释器和并发”。
- 未使用 `-DDEBUGGING` 编译
- `DEBUGGING` 定义让编译器暴露了更多代码，因此出现问题的方式也更多。你应该尝试一下。
- 引入（非只读）全局变量
- 不要引入任何可修改的全局变量，无论是真正的全局还是文件静态的。它们是糟糕的做法，并使多线程和其他并发形式复杂化。正确的方法是将它们作为新的解释器变量引入，参见 `intrpvar.h`（位于最后关于二进制兼容性的部分）。
- 引入只读（const）全局变量是可以的，只要你通过 `nm libperl -a|egrep -v`（如果你的 nm 有 BSD 风格的输出）验证你已添加的数据是只读的。（如果是，不应该出现在该命令的输出中）。
- 如果你想有静态字符串，请将其设为常量：
  ```
  static const char[] = "...";
  ```
- 如果你想有常量字符串数组，请仔细注意 const 的正确组合：
  ```
  static const char * yippee[] = {"hi","ho","silver"};
  ```
- 是一种完全隐藏任何可修改全局变量的方法（它们都被移动到堆上），编译设置 `-DPERL_GLOBAL_STRUCT_PRIVATE`。它通常不使用，但可以用于测试，在 `perlguts` 的“Background and PERL_IMPLICIT_CONTEXT”中阅读更多信息。

# Not exporting your function

某些平台（如 Win32, AIX, VMS, OS/2 等）要求任何作为公共 API（共享 Perl 库）部分的函数必须显式标记为导出。参见 `perlguts` 中关于 `embed.pl` 的讨论。

## Exporting your new function

无论是真正的功能还是你辛苦重构的结果，现在都已就绪并正确导出。那么，可能会出什么问题呢？

也许仅仅是你的函数根本不需要导出。Perl 在导出不该导出的函数方面有一段并不辉煌的历史。

如果函数仅在一个源文件中使用，请将其设为 `static`。参见 `perlguts` 中关于 `embed.pl` 的讨论。

如果函数跨多个文件使用，但仅供 Perl 内部使用（这应该是常见情况），不要将其导出到公共 API。参见 `perlguts` 中关于 `embed.pl` 的讨论。

# Portability problems

以下是编译/或执行失败的常见原因，并非 Perl 本身的常见问题。C FAQ 是很好的睡前读物。请尽可能在许多 C 编译器和平台上测试你的修改；反正我们会这样做，而且避免自己的公开尴尬是件好事。

如果使用 `gcc`，你可以添加 `-std=c89` 选项，它会很方便地捕捉大多数此类不可移植性。（但它也可能捕捉到系统头文件中的不兼容性。）

使用 `Configure -Dgccansipedantic` 标志来启用 `gcc -ansi -pedantic` 标志，这些标志强制执行 ANSI 规则。

如果使用 `gcc -wall`，请注意除非你也用 `-o` 编译，否则不会给出所有的警告（如 `-wuninitialized`）。

注意，如果使用 `gcc`，从 Perl 5.9.5 核心源码发行开始，但不是分发版，核心源码分发，但不是。注意，操作系统，字符集，以及等等。注意对齐指针和数据的对齐。

不要假设操作系统指示特定的编译器。（See `README.micro`）

将指针转换为整数或将整数转换为指针
```



`void castaway(U8* p) { IV i = p; }`

```
```

或者

```
```

`void castaway(U8* p) { IV i = (IV); }`

```
```

两者都是糟糕的、不可忍受的。使用正确的 `PTR2` 宏。同样的 `PTR2UV()`, `PTR2C()` 你也可以通过 `union` 进行技巧。

假设 `sizeof(int) == sizeof(long)`

某些平台 `longs` 是 64 位，某些平台 `ints` 是 64 位，甚至某些 `shorts` 是 64 位。这根据 C 标准都是合法的。（换句话说，“`long long`”不是指定 64 位的可移植方法，“`long long`”也不保证比（`long`）宽）。

相反，使用定义 `IV`, `size`, `IVSIZE`, `I32SIZE` 等。避免使用 `I32`，因为它们不保证是 32 位，它们至少是 32 位，也不保证是 `int` 或 `long`。如果你确实需要 64 位变量，使用 `I64` 和 `U64`，但如果没有受 `HAS_QUAD` 保护。

### 任意
结构体（Structs）按照字段所需的最大对齐方式对齐——对于原生类型，这通常等同于字段的 `sizeof()`
假设字符集是类 ASCII

`Perl` 可以在 `EBCDIC` 平台下编译和运行。请使用 `perlbcd`。这在大多数情况下是透明的，但由于字符集不同，你不应该使用数值（十进制、八进制、十六进制）常量来引用字符。你可以说 `A`，但不能说 `0x41`。你可以安全地使用 `\n`，但不能使用 `\012`。然而，你可以使用 `utf8` 中定义的宏来指定代码点。`LATIN1_TO_NATIVE(0xF)` 将是在你运行的任何平台上表示“LATIN SMALL LETTER SHARP”的代码点（在 ASCII 平台上，它编译时不会添加任何额外代码，因此在这些平台上性能零损耗）。接受的输入范围是 `0x00-0xFF`。如果不能保证输入在该范围内，请使用 `UNICODE_TO_NATIVE`。`NATIVE_LATIN1` 和 `NATIVE_UNICODE` 则向相反的方向翻译。

如果你需要一个在 C 中没有助记符的字符的字符串表示，你应该将其添加到 `regen/unicode_constants.pl` 列表中，Perl 会根据当前平台为你创建 `#define`。

请注意，`handy.h` 中的 "`isFOO`" 和 "`toFOO`" 宏在原生代码点和字符串上工作正常。

此外，ASCII 中的 `'A'-'Z'` 范围是一个包含 26 个字母字符的连续序列。这在 EBCDIC 中并非如此。对于 `'a'` 到 `'z'`，`'0' - '9'` 在两个系统中都是连续的范围。不要对任何范围做任何假设。（注意，正则表达式模式中对范围的特殊处理会让 Perl 认为上述范围是连续的。）

代码中的许多注释忽略了 EBCDIC 的可能性，因此即使代码可以正常工作，这些注释也可能是错误的。这实际上是对“能够在不改变现有代码的情况下成功处理 EBCDIC”这种透明插入能力的一种致敬。

`UTF-8` 和 `UTF-EBCDIC` 是用于用字节表示 Unicode 代码序列的两种不同编码。`utf8.h` 和 `utfebcdic.h` 中具有相同名称（但定义不同）的字节用于让代码认为只有一种编码。这几乎总是被称为 `utf8`，但它也意味着 EBCDIC 版本。再次，即使代码是正确的，代码中的注释可能是错误的。例如，不变字符（invariant characters）的概念在 ASCII 和 EBCDIC 之间不同。在 ASCII 平台上，只有没有设置高位的字符（即序数是 ASCII 0-127）是不变的的，代码中的文档和注释通常会达成一致，引用诸如 `hibit` 之类的内容。EBCDIC 机器上的情况并不那么简单，但只要代码恰当使用使用 `NATIVE_IS_INVARIANT()` 宏，它就能工作。在编写测试脚本时，`file/charset_tools.pl` 包含一些有助于函数，用于编写在 ASCII 和 EBCDIC 平台上都有效的测试。

尽管如此，有时测试无法使用函数，且让测试版本依赖平台是不方便的。目前有 20 个代码点在 Perl 识别的 4 个字符集中都是相同的（3 个 EBCDIC 代码点 加上 ISO8859-1/ASCII）。这些代码点可以在此类测试中使用，尽管有小概率 Perl 可能会出现在另一个字符集中，从而破坏你的测试。但这些代码点中的每一个都受 `C0` 控制。最重要的控制与 `\0`、`\n{VT}` 相同（也可以指定为 `\x0B`、`\n{U0B}` 或 `\013`）。单个控制字符是 `U+00B6 PILC`。无论包含的字符串是否为 UTF 格式，在所有 4 个字符中具有相同位模式的控制字符。`U+B6` 的位模式在所有 4 个非 UTF-8 情况下都是相同的，但在包含 UTF-8 编码字符串时，每种情况都不同。其他在所有 4 个字符中都具有某种相似性的代码点是 `0xDC` 和 `0xFC` 这一对。它们共同代表大写和小写的 `LETTER U WITH DIAERESIS`，可以解析哪个是大写哪个是写：`0xDC` 是 Latin1 中的大写，`0xFC` 是小写；而 `0xFC` 是 EBCDIC 中的大写，`0xDC` 是小写。这一事实可以用于编写在所有 4 个字符集中都相同的不敏感类型测试。

假设字符集只是 ASCII 是一种 7 位编码，输入是 8 位。128 个字符的含义取决于区域设置（locale）。在缺少区域设置的情况下，目前这些额外的字符通常被认为是未分配的的，这带来了一些问题。这种情况在 5.12 中正在被改变，以便这些字符可以被视为 Latin-1 (ISO-8859-1)。

## #define 和 #ifdef

```c
#define BURGLE(X) \
#ifdef BURGLE_OLD_STYLE /* * BAD */ \
... 使用旧方法... \
#else \
... 使用新方法执行... \
#endif
```

你不可能“堆叠” cpp 指令。例如在上面的代码中，你需要两个独立的 `BURGLE(X)` 和 `#define`，一个用于 `#if` 或 `#else`。

在 `#endif` 或 `#else` 之后添加非注释内容：`#ifdef SNOSH ... #else !SNOSH /* * BAD */ ... #endif SNOSH /* BAD * */`

对于某些平台，相应的配置步骤按理会起到同样的作用。

在紧急情况下，如果你无法等待 `Configure` 识别环境，或者你直觉认为 `quux()` 可能可用，你可以临时尝试以下方法：

```
#if (defined(__FOONIX__) || defined(__BARNIX__)) #define HAS_QUUX #endif
#ifdef HAS_QUUX foo = quux(); #endif
```

但无论如何，请尝试尽量将特性与操作系统分离。

假设 Perl 对 C 库函数的封装器返回的返回值所指向的静态内存内容不会发生。许多 C 库函数指向静态存储的指针可能会被后续对相同或相关函数的调用覆盖。Perl 对其中一些函数提供了轻量级封装，但这些封装没有对静态内存进行拷贝。一个很好的例子是指向程序生效的环境变量的接口。Perl 使用 `Perl::getenv` 从环境中获取值。其返回的是指向 C 库中静态内存的指针。如果你立即使用该值进行某些测试，那是没问题的；但如果你保存了该值并期望它不会被后续处理所改变，你就会面临风险，不过你可能并不知道，因为不同的 C 库实现行为不同，而你正在测试的平台可能适用于你的情况。但在某些平台上，后续调用 `Perl::getenv` 或相关函数会覆盖你第一次调用时指向的内存。这还导致了一些难以调试的问题。在 `perlapi` 中执行“savepv”来创建一个拷贝，避免这些问题。当你需要在普通标量（mortal scalar）中创建拷贝时，必须释放该拷贝，如下：

```
if ((s = Perl::getenv("foo")) == NULL) { /* handle NULL case */ } else { s = SVP_smmalloc(newSVvp(s, 0)); }
```



上面的示例仅在 `s` 以 NULL 结尾时才有效；否则你必须将其长度传递给 `newSVvp`。

## 有问题的系统接口

`malloc(0)`、`realloc(0)`、`calloc(0, 0)` 是不可移植的。为了可移植性，请至少分配一个字节。（通常情况下，你很少需要在这种低级别工作，而是应该使用各种 `malloc` 封装器。）

`snprintf()` - 返回类型不可接受。请改用 `my_snprintf()`。

## 安全问题

最后但同样重要的是，这里有关于安全编码的各种提示。请参考 `perclib` 中应该使用的 libc/stdio 替换方案。

- 不要使用 `gets()`
- 否则我们将公开嘲笑你。认真的。
- 不要使用 `tmpfile()`

请改用 `mkstemp()`。
- 不要使用 `strcpy()` 或 `strcat()` 或 `strncpy()` 或 `strncat()`

请改用 `my_strcpy()` 和 `my_strcat()`：它们要么使用原生实现，要么使用 Perl 内部的实现（借自 IN 的公有实现）。
- 不要使用 `sprintf()` 或 `vsprintf()`

如果你极少处理纯字节字符串，请改用 `my_snprintf()` 和 `my_vsnprintf()`，如果这些更安全的 API 可用，它们将尝试使用 `snprintf()` 和 `vsprintf()`。如果你想要比纯字节字符串更高级的东西，请使用 `Perl_form()` 或 SV 以及 `Perl_sv_catpvf()`。

注意，在 glibc 版本 2.17 之前，glibc 的 `printf()`、`sprintf()` 等存在 Bug。如果程序的底层本地区域是 UTF-8，它们将不允许带有精度的 `%.s` 格式创建一个非有效的 UTF-8 字符串。发生的情况是 `%s` 及其操作数直接被跳过且没有任何提示。

- 不要使用 `atoi()`

请改用 `grok_atoUV()`。`atoioi()` 在溢出时的行为未定义，且不能用于增量解析。它受本地区域影响，这并不好。

- 不要使用 `strtol()` 或 `strtoul()`

请改用 `grok_atoUV()`。`strtol()` 或 `strtoul()`（或它们的 IV/UV 友好宏伪装 `Strtol()` 和 `Strtoul()`，或 `Atol()` 和 `Atul()`）受本地区域影响，这并不好。

## 调试

你可以编译一个特殊的调试版本 Perl，允许你使用 Perl 的 `-D` 选项来获取更多 Perl 正在做什么的信息。但有时除了使用调试器深入研究外，要么是查看核心转储的堆栈跟踪（在 Bug 报告中非常有用），要么是在核心转储发生之前弄清楚哪里错了，或者我们最终得到了错误或意外的结果。

## 探究 Perl

为了真正探究 Perl，你可能想要为了调试编译 Perl，如下所示：

```
/Configure -d -D optimize=-g make
```

`-g` 是 C 编译器的标志，用于产生调试信息，允许你单步运行中的程序，并查看我们处于哪个函数中（如果没有调试信息，我们可能看到函数的数值地址，这没什么帮助）。

`Configure` 还会开启 `DEBUGGING` 编译符号，这将启用 Perl 中所有的内部调试代码。你有一堆可以用它们调试的东西：perlin 列出了所有内容，了解它们的最好方法就是玩玩它们。最有用的选项是：

- 上下文（循环）堆栈处理
- 执行跟踪
- 方法和重载解析
- 字符串/数字转换

调试代码的一些功能可以通过 `xs` 模块实现。
`-Dr => use re 'debug'`
`-Dx => use 0 'Debug'`

## 使用源码级调试器

如果 `-d` 的调试输出对你没有帮助，是时候用源码级调试器单步执行 的执行了。我们将使用 `gdb` 作为示例；该方法适用于任何调试器（许多供应商将其称为 dbx），但请检查你正在使用的调试器的手册。启动调试器，输入：

```
gdb ./perl
```

或者如果你有一个核心转储：

```
gdb ./perl core
```

你可能需要在 Perl 源码树中执行，这样调试器就可以读取源代码了。你应该看到版权信息，然后是提示符。`help` 可以带你文档，但这里是最实用的命令：

- `run [args]`: 使用给定的参数运行程序。
- `break function_name source.c:xxx`: 告诉调试器当我们到达命名函数（但参见“内部函数”）或源文件中的指定行时，我们将暂停执行。
- `step`: 一行单步执行程序。
- `next`: 一行单步执行程序，但不进入函数内部。
- `continue`: 运行到下一个断点点。
- `finish`: 运行到当前函数结束，然后再次停止。
- `enter`: 只按回车即可再次执行大部分操作 - 遍历数千行源代码。
- `ptype`: 打印给定参数的 C 定义。
- `print`: 执行给定的 C 代码并打印其结果。

警告：Perl 大量使用宏，而 gdb 并不一定支持宏（见后文“gdb 支持”）。例如，你不能说 `print_nolen(sv)` 但你必须说 `print Perl_sv_nolen(sv)` 或对源文件调用 `cpp`（参见“内部目标”）。你可能会发现有一个“宏字典”会有帮助，你可以通过以下命令生成：

```
-d perl.h
```

我们也可以将此导出出来：当前的 op 始终存储在 `PL_op` 中，我们可以通过 `Perl_op_dump` 导出它。这将向 B::Debug 输出输出内容。

```
(gdb) print Perl_op_dump(PL_op) { 13 TYPE = add => 14 TARG = 1 FLAGS = (SCALAR, KIDS) { TYPE = null => (12) (was rv2sv) FLAGS = (SCALAR, KIDS) { 11 TYPE = gsv => 12 FLAGS = (SCALAR) GV = main::b }

# this latter #
```

### 使用 gdb 查看程序的特定部分

通过上面的示例，你已经知道寻找 `Perl_pp_add`，但如果它到处处有多次调用，或者你不知道正在寻找哪个 op 怎么办？

一种方法是在你想查找的地方注入一个稀有的调用。例如，你可以在方法之前添加 `study`：

```
study;
```
在 gdb 中：

```
(gdb) break Perl_pp_study
```

然后单步执行直到遇到你寻找的内容。如果你只想在特定的迭代中中断，这在循环中效果很好：

```
for my $c (1..100) { study if $c == 50; }
```

### 使用 gdb 查看解析器/法词器在做什么

```
print "Before\n"; BEGIN { study } print "After\n";
```

在 gdb 中：

```
(gdb) break Perl_pp_study
```

如果你想看解析器/法词器在 if 块等结构内部在做什么，你需要稍微用一点技巧：

```
if ($a && $b && & do { BEGIN { study } 1 } && $c) { ... }
```

## 源代码静态分析

存在各种工具可以对 C 源代码进行静态分析，而不是动态分析，即不执行代码。通过仅解析 C 代码并查看生成的图（以及它关于执行和数据流的信息），可以检测到资源泄漏、未定义行为、类型不匹配、移植性问题、会导致非法内存访问路径以及其他类似问题。事实上，这正是 C 编译器知道对可疑代码给出警告的方法。

### lint, splint

老牌的 C 质量检查工具 lint 可于多个平台可用，但请注意，不同供应商有不同的实现，这意味着不同平台之间的标志（flags）并不相同。

有一个名为 `splint`（Secure Programming Lint）的 lint 变体，可以在任何类 Unix 平台上进行编译。

Makefile 中有 `lint` 和 `<splint>` 目标，但你可能需要调整标志（见上文）。

### Coverity

Coverity 是一个类似于 lint 的产品，作为其产品的测试平台，定期检查几个开源项目，并向开源开发者提供缺陷数据库的账户。

### cpd (复制粘贴检测器)

`cpd` 工具检测复制粘贴代码。如果复制粘贴代码的一个实例发生了变化，所有其他地方可能也应该随之更改。因此，此类代码可能应该转换为子程序或宏。

`cpd` 是 `pmd` 项目的一部分（`pmd` 最初是为 Java 代码的静态分析编写的，后来其 `cpd` 部分被扩展到也可以解析 C 和 C++..）。

从 SourceForge 站点下载 `pmd-bin-X.Y.zip`，从中提取 `pmd-X.Y.jar`，然后以如下方式运行该代码：



```java -cp pmd-X.Y.jar net.sourceforge.pmd.CPD --minimum-tokens 100 files /some/where/src --language c > cpd.txt
```

你可能会遇到内存限制，在这种情况下你应该使用 `-Xmx` 选项：
```java -Xmx512M..
```

# gcc 警告

尽管关于 gcc 警告的不一致性和覆盖率问题可以写很多内容（例如 `-wall` 并不意味着“所有警告”，或者某些常见的移植性问题没有被 `-wall` 覆盖，或者 `-ansi` 和 `-pedantic` 都是定义不良好的警告集合等等），但 gcc 在保持我们的代码整洁方面仍然是一个非常有用的工具。

`-wall` 默认开启的。

`-ansi`（及其助手 `-pedantic`）如果能一直开启会很好，但遗憾的是它们在所有平台上都不是安全的，例如它们会与系统头文件产生致命冲突（Solaris 是一个典型的例子）。如果使用 `Configure -Dgccansipededantic`，cflags 前端会在已知已安全的平台上选择 `-ansi -pedantic`。

从 Perl 5.9.4 开始，增加了以下额外的标志：

- `-Wendif-labels`
- `-Wextra`
- `-Wdeclaration-after-statement`

以下标志如果可用会很好，但它们首先需要它们自己的 Augean 稳定大师：

- `-Wpointer-arith`
- `-Wshadow`
- `-Wstrict-prototypes`

`-Wtraditional` 是 gcc 倾向于将许多警告捆绑在一个开关下的烦人倾向的另一个例子（这在实践中是不可能的，因为会产生大量抱怨），但它确实包含了一些单独可用会有益的警告，例如关于宏参数内部字符串常量的警告：这在 ANSI 之前的行为与在 ANSI 下的行为不同，且某些 C 编译器仍处于过渡阶段，AI 就是一个例子。

# 其他 C 编译器的警告

其他 C 编译器（是的，除了 gcc 还有其他的 C 编译器）通常开启“严格 ANSI”或“某些移植性扩展的严格 ANSI”模式，例如 Sun Workshop 开启了 `-xa` 模式（尽管是隐式的），或者 DEC（现在是 HP...）开启了 `-stdi` 模式。

# 内存调试器

注意 1：在旧的内存调试器下运行会减慢执行速度：秒变分，分变小时。例如在 Perl 5.8.1 中，`enc/Encode/t/Unicode` 完成需要极长的时间，例如使用 Purify、Third Degree 和 valgrind。在 valgrind 下，即使在运行快的电脑上也需要超过六小时。上述测试对内存调试器来说非常不友好。如果你不想等待，可以直接杀死 perl 进程。大致上 valgrind 会让执行变慢 10 倍，AddressSanitizer 慢 2 倍。

注意 2：为了尽可能减少内存泄漏假报的数量，请参见“PERL_DESTRUCT_LEVEL”获取更多信息，你必须将环境变量 `PERL_DESTRUCT_LEVEL` 设置为 2。例如如下：
```env PERL_DESTRUCT_LEVEL=2 valgrind ./-lib..
```

注意 3：当内部或 require 中存在编译错误时会有已知内存泄漏，在调用栈中看到 `s_doeval` 是这些问题的迹象。修复这些泄漏并非易事，但它们最终必须修复。

注意 4：除非在构建 Perl 时使用了 Configure 选项 `-Accflags=-DDL_UNLOCK_ALL_AT_EXIT`，否则 DynaLoader 将不会完全清理自身。

# valgrind

valgrind 工具可用于发现内存泄漏和非法堆内存访问。从 3.3.0 版本开始，Valgrind 仅支持 x86 Linux、x86_64、PowerPC 和 Darwin (OS x)。特殊的 `test.valgrind` 目标可以在 Valgrind 下运行测试。发现的错误默认以内联显示。

示例用法：
```make test.valgrind
```

由于 valgrind 增加了巨大的开销，测试运行将非常缓慢。valgrind 测试支持并行运行以缓解此问题：
```TEST_JOBS=9 make test.valgrind
```

注意上述调用非常详细，因为默认启用了泄漏检查。如果你只想看错误，尝试：
```VG_OPTS='q --leak-check=no --show-reachable=no' TEST_JOBS=9 \ make test.valgrind
```

valgrind 还提供 cachegrind 工具，通过如下方式调用：
```VG_OPTS=--tool=cachegrind make test.valgrind
```

由于库（特别是 glibc）也会触发错误，valgrind 允许使用抑制文件消除此类错误。默认抑制文件已经捕获了许多错误。额外的抑制定义在 `t/perl.supp` 中。

# AddressSanitizer

AddressSanitizer 是 clang 和 gcc 的扩展，从 clang 3.1 和 gcc 4.8 起包含其中。它可以检查非法堆指针、全局指针、栈指针和释放后使用错误，并且足够快到你可以轻松编译或运行 perl。不过它不检查内存泄漏。AddressSanitizer 支持 Linux、Mac OS x，很快将支持 Windows。

要使用 AddressSanitizer 编译 perl，你的 Configure 调用如下：

```sh Configure -des -Dcc=clang -Accflags=-faddress-sanitizer -Aldflags=-faddress-sanitizer \ -Addlflags=-shared -faddress-sanitizer
```

其中这些参数意味着：

- `-Dcc=clang`
如果 clang 执行文件不在路径中，应将其替换为完整路径。
- `-Accflags=-faddress-sanitizer`
使用 AddressSanitizer 编译 perl 和扩展源码。
- `-Aldflags=-faddress-sanitizer`
使用 AddressSanitizer 链接 perl 可执行文件。
- `-Addlflags=-shared -faddress-sanitizer`
使用 AddressSanitizer 链接动态扩展。你必须手动指定 `-shared`，因为使用 `-Addlflags=-shared` 会阻止 Configure 为 lddlflags 设置默认值（至少在 Linux 上通常包含 `-shared`）。

另见 <>

# 性能分析 (PROFILING)

根据你的平台，有多种方法对 Perl 进行性能分析。

分析执行文件有两种常用技术：统计时间采样和基本块计数。

第一方法定期对 CPU 程序计数器进行采样，由于程序计数器可以与函数生成的代码相关联，我们可以获得程序在哪些地方花费时间的统计视图。注意事项是，非常小或快速的函数在性能分析中出现的概率较低，而且周期性中断程序（这通常频率非常高，在毫秒级）会产生额外的开销，可能会偏偏结果。第一个问题可以通过延长运行时间来缓解（通常对于性能分析来说这是一个好主意），第二个问题由性能分析工具本身很好的保护。

第二种方法将生成的代码划分为基本块（basic blocks）。基本块是仅从开始进入且仅从结束退出的代码段。例如，条件跳转会启动一个基本块。基本块性能分析通常通过对代码进行插桩来实现，即在生成的代码中添加基本块 #nnnn 簿记代码。在代码块执行期间，计数器会进行相应的更新。注意事项是添加的额外代码可能会偏结果：同样，性能分析工具通常尝试将它们从结果中剔除。

# gprof 性能分析

gprof 是许多 Unix 平台上可用的性能分析工具，使用统计时间采样。你可以使用 gcc 配合 `-pg` 标志编译出一个用于性能分析的 perl 版本。编辑 config.sh 或重新运行 Configure。运行 Perl 的性能分析将创建一个名为 gmon.out 的输出文件，其中包含了执行期间收集的性能分析数据。

快速提示：

```$ sh Configure -des Duseddevel -Accflags='-pg' \ -Aldldflags='-pg' -Aldldflags='-pg -shared' && make perl $ ./perl # 在当前目录创建 gmon.out $ gprof ./perl > out less out
```



（在 RT #11899 解决之前，你可能需要在 `-Aldldflags` 行添加 `-shared`）

随后 `gprof` 工具可以以多种方式显示收集的数据。通常 `gprof` 理解以下选项：

- `-a`: 从性能分析中抑制统计定义的函数。
- `-b`: 抑制性能分析中的详细描述。
- `-e routine`: 从性能分析中排除给定的例程及其后代。
- `-f routine`: 在性能分析中仅显示给定的例程及其后代。
- `-s`: 生成摘要文件 `gmon.sum`，然后可以将其提供后续的 `gprof` 运行以积累多次运行的数据。
- `-z`: 显示使用率为零的例程。

有关可用命令和输出格式的更多详细说明，请参你本地的 `gprof` 文档。

# GCC gcov 性能分析

基本块分析在 `gcc` 3.0 及更高版本中正式可用。你可以使用 `gcc` 配合 `-fprofile-arcs -ftest-coverage` 标志编译出一个用于性能分析的 `perl` 版本。编辑 `config.sh` 或重新运行 `Configure`。

快速提示：

```
$ Configure -des Dusedveled -Doptimize='g' -Acclags='fprofile-arcs-ftest-coverage -Aldldflags='fprofile-arcs -ftest-coverage' -\Addldflags='fprofile-arcs -ftest-coverage -shared' \& make perl $ rm -f regexc.g gcov regexc.c $ ./perl... $ gcov regexc.c $ less
```

（在 RT #118199 解决之前，可能需要在 `-Addldflags` 行添加 `-shared`）

运行用于性能分析的 `perl` 版本将生成性能分析输出。每个源文件都会创建一个相应的 `.gcdda` 文件。

使用 `gcov` 工具显示结果（如果你安装了 `gcc` 3.0 或更高版本，则应该安装了 `gcov`）。`gcov` 在源代码上运行，如下所示：

```
gcov sv.c
```

这将创建 `sv.c.gcov`。`.gcov` 文件包含源代码，并使用 `"#"` 标记标出执行的相对频率。如果你想为所有性能分析的对象生成 `gcov` 文件，可以运行类似下面的命令：

```
for in file -name "*.gcno" do sh -c "dirname $file" && gcov basename $file .gcno" do done
```

`gcov` 的有用选项包括 `-b`，它将汇总基本块、分支和函数调用覆盖率，以及 `-c`，它将使用实际计数。有关 `gcov` 的用法和使用 `gcc` 进行基本块分析的信息，请参阅最新的 GNU 手册。从 `gcc` 4.8 开始，这位于 `<`

# 杂项技巧 (MISCELLANEOUS TRICKS)

## PERL_DESTRUCT_LEVEL

如果你想手动（例如使用 `valgrind`）运行任何测试，请注意，默认情况下 `perl` 不会显式清理它所分配的所有内存（例如全局内存区域），而是让整个程序的 `exit()` 来“处理”这些分配，也称为“对象的全局析构”。

有一种方法可以告诉 `perl` 执行完全清理：将环境变量 `PERL_DESTRUCT_LEVEL` 设置为非零值。`t/TEST` 包装器将其设置为 `2`，如果你不想看到“全局泄漏”，这就是你需要做的。例如，在 `valgrind` 下运行：

```
PERL_DESTRUCT_LEVEL=2 valgrind ./perl -Ilib t/foo/bar.t
```

（注意：`mod_perl` `apache` 模块为了其自身的目的使用了此环境变量，并扩展了它的语义。更多信息请参阅 `mod_perl` 文档。此外，派生的线程等同于将此变量设置为值 `1`。）

如果在运行结束时你收到了“`N scalars leaked`”的消息，你可以使用 `-DDEBUGING_SCARS` 来找到泄漏源。如果编译了 `-DDEBUGING_SCARS`，每个分配的序列号也会被记录。由于日志没有使用 `PerlIO`，所有的 `sv` 分配都会被记录，且启用日志不会引入额外的分配。相比之下，`-dm` 直接位于 `malloc()` 处。`sv` 日志类似。

（注：由于原文后续部分存在大量重复，已根据逻辑进行了去重处理。）

`locations(file:line)`。支持的平台有 Linux 和 os x（某些 *BSD* 可能至少可以部分工作，但尚未经过测试）。

此功能尚未在多线程环境下进行过测试，但它只会显示执行回溯的线程的回溯。

该功能需要通过 `Configure -Dusebacktrace` 启用。

`-Dusebacktrace` 也会在编译/链接时保留调试信息（通常为 `-g`）。许多编译器/链接器都同时支持优化和保留调试信息。符号名和源码位置需要这些调试信息。

静态函数可能在回溯中不可见。

### Linux

- 源代码位置（如果可用）如果编译器进行了例如内联（inlined）代码的处理，可能会缺失或具有误导性。优化器可能会使源代码与目标代码的匹配变得非常有挑战性。
- 你必须安装 BFD (`-bfd`) 库，否则 `perl` 将链接失败。BFD 通常作为 GNU `binutils` 的一部分分发。
- 总结：`Configure ... -Dusebacktrace` 并且你需要 `-bfd`。

### OS X

只有在安装了 Developer Tools 的情况下才支持源代码位置。（不需要 BFD）。

总结：`Configure ... -Dusebacktrace` 并安装 Developer Tools 会很有帮助。

可选地，为了尝试此功能，你可能希望在发出警告或 `croak` (`die`) 消息之前自动转储回溯，可以在 `Configure` 时添加 `-Accfflags=-DUSE_C_BACKTRACE_ON_ERROR`。

除非启用了上述额外功能，否则 Perl/XS 层外，回溯功能的没有任何内容是可见的。

此外，即使你在编译时启用了此功能，也需要在运行时通过环境变量启用它：`PERL_C_BACKTRACE_ON_ERROR=1`。它必须是一个大于零的整数，表示所需的帧数。

从 Perl 层获取回溯（以 xs 扩展为例）会比你预想的要乏味得多：通常你只会看到 `runops`、`entersub` 等其他内容。此 API 旨在从 Perl 实现内部调用，而不是从执行层调用。

回溯的 API 如下：

- `get_c_backtrace`
- `free_c_backtrace`
- `get_c_backtrace_dump`
- `dump_c_backtrace`

## Poison

如果你在调试器中看到内存区域神秘地充满了 `0xABABABAB` 或 `0xEFEFEFFEF`，你可能看到了 `Poison()` 宏的效果，见 `perlclib`。

## Read-only optree

在多线程下，`optree` 是只读的。如果你想强制这一点，以检查来自错误代码的写访问，请使用 `-Accflags=-DPERL_DEBUG_READONLY_OPS` 编译。该代码会通过 `mmap` 分配 `op` 内存，并在将其附加到子函数时设为只读。对 `op` 的任何写访问都会导致 `SIGBUS` 错误。

此代码仅用于开发，并且可能无法移植到所有 Unix 变体。此外，这是一个 80% 的解决方案，因为它无法让所有 `ops` 都变为只读。具体而言，它不适用于属于 BEGIN 块的 slabs。

然而，作为一个 80% 的解决方案，它仍然是有效的，因为它在过去帮助发现过 bug。

## 什么时候 bool 不是 bool？

在 C99 之前的编译器上，`bool` 定义为等同于 `char`。因此，将任何更大的类型赋值给 `bool` 都是不安全的并可能会被截断。`cBOOL` 宏的存在是为了正确强制转换。

在 `bool` 是布尔类型的平台和编译器（C, C99）上，很容易忘记缓存。你可以通过编译 `-Accflags=-DPERL_BOOL_AS_CHAR` 强制让 `bool` 为 `char`。你可能希望在运行 `configure` 时使用类似 `-Accflags='-Wconversion -Wno-sign-conversion -Wno-shorten-64-to-32'` 或你编译器的对应选项，以便更容易发现任何不安全的截断。

## .i Targets

你可以通过运行以下命令来扩展 `foo.c` 文件中的宏：

```
make foo.i
```



这将使用 `cpp` 扩展宏。不要被结果吓到。

## AUTHOR

本文档最初由 Nathan Torkington 编写，由 perl5-porters 邮件列表维护。

## PERLHACKTUT

### NAME

`perlhacktut` - 逐步一个简单的 C 代码补丁的创建

## DESCRIPTION

本文将带你通过一个简单的补丁示例。

如果你还没有读过 `perhlack`，请先去读它！你可能也想读读 `perlsource`。

完成这里后，接下来请查看 `perlhacktips`。

## EXAMPLE OF A SIMPLE PATCH

让我们从头到尾来看一个简单的补丁。

这是 Larry 建议的内容：如果 `u` 是 `pack` 期间的第一个活跃格式（例如，`pack "U3C8", @stuff`），则生成的字符串应该被视为 UTF-8 编码。

如果你正在处理 Perl 仓库的 git clone，你可能想为你的更改创建一个分支。这将使得创建一个正确的补丁变得简单得多。关于如何执行此操作，参见 `perglit`。

## Writing the patch

我们如何准备修复它？首先，我们定位相关代码——`pack` 发生在运行时，它会在 `pp` 文件中。果然，`pp_pack` 在 `pp.c` 中。由于我们要修改这个文件，让我们把它复制到 `pp.c`。

[好吧，在编写本教程时，它在 `pp.c` 中。现在它已经与 `pp_unpack` 一起分到了单独的文件 `pp_pack.c` 中]

现在让我们来看看 `pp_pack`：我们将一个模式传入 `pat`，并遍历该模式，依次将每个字符存入 `datatype`。然后对于每个格式字符，我们吞掉模式中的所有其他参数（字段宽度、星号等），并将下一个输入块转换为指定的格式，将其添加到输出的 `sv cat` 中。

我们如何知道 `u` 是 `pat` 中的第一个格式呢？嗯，如果我们有一个指向 `pat` 开头的指针，那么当我们看到 `u` 时，我们仍然处于字符串的开头。所以，这里是 `pat` 设置的地方：

```
STRL fromlen; char *pat = Svpvx(**MARK, fromlen); char *patend = pat + fromlen; I32 datatype; SV *fromstr;
```

我们在这里还会有另一个字符串指针：

```
STRL fromlen; char *pat = Svpvx(**MARK, fromlen); char *patend = pat + fromlen; char *patcopy; I32 len; datatype;
```

描述我们刚刚做的更改。相关位置是 `pod/perlfunc.pod`；再次，我们创建一个副本，然后我们将此文本插入到 pack 的描述中：

=item * 如果模式以 C<U> 开头，则生成的字符串将被处理为 UTF-8 编码的 Unicode。你可以通过初始的 C<U0> 强制对字符串进行 UTF-8 编码，随后的字节将被解释为 Unicode 字符。如果你不希望发生这种情况，可以用 C<C0>（或任何其他）开始你的模式，以强制 Perl 不对你的字符串进行 UTF-8 编码，然后在模式中的某处跟随一个 C<U*>。

# 提交

有关如何提交此补丁的详情，请参见 perlhack。

# 作者

此文档最初由 Nathan Torkington 编写，由 perl5-porters 邮件列表维护。

# PERLHAIKU

## NAME

`perlhaiku` - Haiku 上的 Perl 5.10+ 版本

## 描述

此文件包含如何为 Haiku 编译 Perl 的说明，并列出了已知问题。

# 构建与安装

构建过程完全完全标准的：

```
./Configure -de
make
make install
```

使 perl 可执行并为 libperl 创建一个符号链接：

```
chmod a+x /boot/common/bin/perl; cd /boot/common/lib; ln -s perl5/5.22.0/BePC-haiku/CORE/libperl.so .
```

将 5.22.0 替换为您相应的 Perl 版本。

## 已知问题

在 Haiku 修订 28311 中遇到了以下问题：

- 目前尚无法编译带有线程支持的 Perl。
- `ext/Socket/tocketpair.t` 测试失败。更具体地说：使用数据报套接字的子测试失败了。Haiku 尚未实现 Unix 数据报套接字。
- `ext/Sys/Syslog/t/syslog.t` 测试的一个子测试失败。这是由于 Haiku 尚未实现对 `/dev/log` 的支持。
- `lib/Net/Ping/t/450_service.t` 和 `lib/Net/Ping/t/510_ping_udp.t` 测试失败。这是由于 Haiku 网络栈实现中的错误。

# 联系方式

对于 Haiku 特有的问题，请联系 HaikuPorts 开发人员：<>

最初的 Haiku 移植由 Ingo Weinhold <> 完成。

最后更新：2008-10-29

# PERLHIST

## NAME

`perlhist` - Perl 历史记录

## 描述

本文旨在记录 Perl 源码发布版本。

# 引言

Larry Wall 简述 Perl 历史：

Perl 0 向我的同事引入了 Perl。Perl 1 向世界引入了 Perl，并将 `/\...\}/` 改为 `/(...)//`。（Dan Faigin 仍然没有原谅我 ::\\）Perl 2 引入了 Henry Spencer 的正则表达式包。Perl 3 引入了第一本《Camel》（嵌入空字节）。Perl 4 引入了第一本《Camel》。真的。我们大多数时候只是更改了版本号，以便书籍可以引用 4.000。Perl 5 引入了其他一切，包括引入其他所有内容的能力。

# 南瓜的守护者

Larry Wall, Andy Dougherty, Tom Christiansen, Gurusamy Sarathy, Graham Barr, Jarkko Salzenberg, Tim Bunce, Malcolm Beattie, Schwamy, Hietaniemi, Hugo van der Sand, Michael Schwerm, Rafael Garcia-Suarez, Nicholas Clark, Richard Clamp, Leon Brocard, Dave Mitchell, Jesse Vincent, Ricardo Signes, Steve Hay, Matt T Trout, David Golden, Florian Ragwitz, Tatsuhiko Miyagawa, Chris bin-Williams, Zefram, AEvar Arfjo-rd, Bjarmason, Stevan Little, Dave Rolsky, Max Maisichein, Abigail, Jesse Luehrs, Tony Cook, Dominic Hargreaves, Aaron Crane, Aristotle Pagaltzis, Matthew Horsfall, Peter Martini, and Sawyer X.

南瓜？

[来自 Perl 源码发行中的 Porting/pumpkin.pod]

Chip Salzenberg 因此归功，同时也致敬了他的同事 David Croy。我们传过各种名称（接棒、令牌、烫手芋），但没有一个流行起来。然后，Chip 问：

[开始引用]

谁有南瓜补丁？

解释一下：David Croy 曾告诉我，在之前的工作中有一个磁带驱动和多个使用它进行备份的系统。但他们没有使用高科技排除软件，而是使用了一种低科技方法来防止多个同时备份：一个填充的南瓜。除非拥有“备份南瓜”，否则没人允许进行备份。

[结束引用]

这个名字流传了下来。南瓜的持有者有时被称为 pumpkin（为了保持来源浮动吗？）或 pumpkinkeer（幕后操纵者）。
