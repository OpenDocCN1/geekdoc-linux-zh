
- 文件操作 ................................................................ 1066
- 排序 ....................................................................... 1069
- 子函数 ................................................................. 1071
- CPAN 模块 ........................................................ 1073
- 示例 .................................................................... 1081

Larry Wall 创建了 Perl（实用提取和报告语言）编程语言用于处理文本。Perl 使用了 awk、sed、C、Bourne Shell、Smalltalk、Lisp 和英语的语法和概念。它的设计目的是从文件中扫描并提取信息，并根据这些信息生成报告。自从1987年引入以来，Perl 经历了巨大的扩张——其处理能力随之增长。今天，除了文本处理外，Perl 还用于系统管理、软件开发和通用编程。

Perl 代码是可移植的，因为它已经在许多操作系统上实现（见 `cpan.org/ports`）。Perl 是一种非正式、实用、健壮、易用、高效且完整的语言。它是一种支持过程和面向对象编程的粗犷语言。它并不一定优雅。

Perl 与许多其他语言的区别之一是它的语言学源。在英语中，你说：“如果我中奖了，我就买辆车。”Perl 允许你模仿这种语法。另一个区别是 Perl 拥有单数和复数变量，前者存储单个值，后者存储值列表。

# Perl 简介

手册中的几句引用揭示了 Perl 的哲学：

Perl 的许多语法元素都是可选的。它并不会要求你为每个函数调用加上括号并声明每个变量，你通常可以省略这些显式元素，Perl 经常能理解你的意图。这被称为“我的意思是吗”（Do I Mean），缩写为 `DWIM`。它允许程序员偷个懒，并以他们习惯的风格编写代码。

Perl 的格言是“实现某件事有多种方法”。至于还有多少种，留给读者自行体会。

Perl 最大的资产之一是数以千计的第三方模块支持。综合 Perl 存档（CPAN; `www.cpan.org`）是许多与 Perl 相关的模块和其他其他信息的仓库。请参阅第 1079 页有关在 Perl 中下载、安装和使用这些模块的信息。

# 安装 perl-doc

`perl-doc` 软件包包含了丰富的信息。在开始使用 Perl 之前，请安装此包；更多信息请参见下一页。

学习 Perl 的最佳方法是实践。通过复制并修改本章中的程序，直到它们对你来说变得意义明确。许多工具系统是用 Perl 编写的。大多数此类工具的第一行以 `#!/usr/bin/perl` 开头，这告诉 shell 将程序传递给 Perl 执行。以下命令使用 `grep` 递归（-r）搜索 `/usr/bin/perl` 和 `/usr/sbin` 目录中包含字符串 `/usr/bin/perl` 的文件。`/usr/sbin` 目录列出了许多用 Perl 编写的系统工具：

```bash
$ grep -r /usr/bin/perl /usr/bin /usr/sbin | head-4
/usr/bin/perl-defoma-user:#!/usr/bin/perl -w
/usr/bin/pod2latex:#!/usr/bin/perl
/usr/bin/pod2latex:  eval 'exec /usr/bin/perl -S $0 "${1}\$0}"'
/usr/bin/splain#!/usr/bin/perl
```

检查这些程序——它们展示了 Perl 在现实世界的用法。在修改系统程序之前，将其复制到你拥有的目录。除非你知道自己在做什么，否则不要以 root 权限运行系统程序。

# 更多信息

- 本地页面：查看 Perl 和 perlitoc man 页面获取 Perl 页面列表
- Perl 首页：`www.perl.com`
- CPAN：`www.cpan.org`
- 博客：`perlbuzz.com`

# 帮助

Perl 是一种宽容的语言。因此，很容易写出可以运行但执行不符合预期的 Perl 代码。Perl 包含了许多可以帮助你发现代码错误的工具 `-w` 选项和 `use warnings` 语句可以产生有用的诊断信息。`use strict` 语句（`perbib` 页面）可以通过要求在使用变量前先声明（以及其他要求）来为程序建立秩序。当所有其他方法都失败时，你可以使用 Perl 的内置调试器来逐步执行程序。更多信息请参见 `perldebug` 和 `perldebug` man。

# perldoc

在使用 `perldoc` 之前，你必须安装 `perl-doc` 软件包。

`perldoc` 工具用于利用和显示 Perl 文档。它与 `man`（第 136 页）类似，但专门针对 Perl。它处理包含 `pod`（纯旧文档，plain old documentation）行的文件，`pod` 是一种简洁清晰的文档语言。当嵌入到 Perl 程序时，`pod` 允许你在 Perl 程序中包含整个程序的文档，而不仅仅是代码级的注释。

以下是一个包含 pod 的简单 Perl 程序。`=cut` 之前的行是程序；其余部分是 pod 格式文档。

```bash
$ cat pod.ex1.pl
#!/usr/bin/perl

=head1 A Perl Program to Say Hi
Hi there.
```

这个简单的 Perl 程序包含了 `<pod>` 文档。接下来的 `=cut` 命令告诉 perldoc 之后的内容是文档。

```perl
=cut
# A Perl program
print "Hi there.\n"
```

请访问 `<perldoc.perl.org/perlpod.html>` 页面获取关于 `<pod>` 的更多信息，访问 `perldoc.perl.org` 获取完整的 Perl 文档。

你可以使用 Perl 运行该程序：

```bash
$ perl pod.ex1.pl
Hi there.
```

# 第二章 The Perl 脚本语言

或者你可以使用 `perldoc` 来显示文档：

```bash
$ perldoc pod.ex1.pl
POD.EX1(1) User Contributed Perl Documentation POD.EX1(1)

# A Perl Program to Say Hi there.

这个简单的 Perl 程序包含了 pod 格式的文档。接下来的 `=cut` 命令告诉 perldoc 之后的内容不是文档。

pod Documentation Resumes with any pod Command
请访问 perdoc.perl.org/perpod.html 页面获取关于 pod 的更多信息，访问 perldoc.perl.org 获取完整的 Perl 文档。

2008-10-14 POD.EX1(1)
```

大多数公共分发的模块和脚本以及 Perl 本身都包含了嵌入的 pod 格式文档。例如，以下命令显示了关于 `print` 函数的信息：

```bash
$ perldoc -f print
print FILEHANDLE LIST
print LIST
print Prints a string or list of strings. 如果成功，则返回真。FILEHANDLE 可能是一个标量变量名，在这种情况下，变量包含句柄的名称或引用，从而引入了一层间接。（NOTE: IF the
```

```perl
in which case the variable contains the name of or a reference to the handle, thus introducing one level of indirection. (NOTE: IF the
```

（注：此处原文存在大量 OCR 识别错误和重复内容，译文已根据核心逻辑进行清理处理）

# 术语

本节定义了本章中使用的一些术语。

- Perl 模块（Perl module）：一组工作的自包含代码块。
- 分发（distribution）：执行特定任务的一个或多个模块的集合。
- 包（package）：定义命名空间。
- 块（block）：由大括号 `{}` 定义的零或多个语句，定义了作用域。
- 包变量（package variable）：定义在其所在的包内。
- 列表（list）：一组零或多个标量。
- 数组（array）：按定义顺序存储元素列表的变量。

# 运行 Perl 程序

有多种方法可以运行用 Perl 编写的程序。`-e` 选项允许你在命令行中输入程序：

```
$ perl -e 'Hi there.\n'
Hi there.
```

`-e` 选项是测试 Perl 语法和运行简短、一次性程序的良好选择。该选项要求 Perl 程序必须作为命令行上的单个参数的形式出现。程序必须紧跟在该选项之后——即它是该选项的一个参数。编写此类程序的一种简单方法是将程序包含在单引号内。

由于 Perl 属于利用文件输入或标准输入的一类（见第 248 页），你可以输入 `perl` 命令并输入以 CONTROL-D（文件结束符）终止的程序。Perl 会从标准输入读取程序：

```
$ perl
print "Hi there.\n"
CONTROL-D
Hi there.
```

上述技术对于快速、一次性的命令行程序很有用，但对于运行更复杂的程序并没有帮助。在 Perl 的大多数情况下，程序存储在文本文件中。虽然不是强制要求的，但文件通常具有 `.pl` 扩展名。以下是之前示例中使用的相同程序，存储在文件中：

```
$ cat simple.pl
print "Hi there.\n"
```

你可以通过指定其名称作为 Perl 的参数来运行此程序：

```
$ perl simple.pl
Hi there.
```

最常见的情况与大多数脚本类似，包含 Perl 程序的文件是可执行的。使用 `chmod`（见第 300 页）可以让 `simple2.pl` 变为可执行。如第 302 页所示，文件第一行开头的 `#` 告诉 shell 将文件的其余部分传递给 `/usr/bin/perl` 执行。

```
$ chmod 755 simple2.pl
$ cat simple2.pl
#!/usr/bin/perl -w
print "Hi there.\n"
```

```
$ ./simple2.pl
Hi there.
```

在这个示例中，`simple2.pl` 以 `./simple2.pl` 的形式执行，是因为工作目录不在用户的 PATH 中（见第 319 页）。`-w` 选项告诉 Perl 在识别代码中的潜在错误时发出警告信息。

# Perl 版本 5.10

本章的所有示例都是在 Perl 5.10 下运行的。输入以下命令查看本地系统运行的是哪个版本的 Perl：

```
$ perl -v
This is perl, v5.10.0 built for i686-linux-gnu-thread-multi
...
```

`use feature 'say'` `say` 函数是 Perl 6 的特性，在 Perl 5.10 中可用。它的工作方式与 `print` 相同，会在输出的每行末尾添加换行符 (\n)。某些版本的 Perl 要求你显式告诉 Perl 你想使用它。示例中的 `say` 函数告诉 Perl 启用 `say`。在不使用该行的情况下运行此程序，查看本地 Perl 版本是否需要它。

```
$ cat 5.10.pl
use feature 'say';
say 'Output by say.';
print 'Output by print.';
say 'End.'
$ perl 5.10.pl
Output by say.
Output by print.End.
$
```

旧版本的 Perl 如果你运行较早版本的 Perl，需要将本章示例中的 `say` 替换为 `print`，并用带引号的 \n 终止 `print` 语句：

```
$ cat 5.8.pl
print 'Output by print in place of say.', "\n";
print 'Output by print.';
print 'End.', "\n"
```

```
$ perl 5.8.pl
Output by print in place of say.
Output by print.End.
```

# 语法

语句（Statements）描述了 Perl 程序的主要组成组件。一个 Perl 程序包含一个或多个语句，每条语句都以分号（;）结束。除了引号字符串内的空白字符外，这些语句在空白字符（空格、制表符等）方面是自由形式的（见第 1180 页）。多条语句可以出现在同一行，每条都以分号结束。以下程序是等价的。第一个占两行，第二个只占一行；请注意等号和加号周围间距的差异。如果这些程序抱怨 `say` 不可用，请使用 `use feature 'say'`（见上文）。

```
$ cat statement1.pl
$n=4;
say "Answer is $n + 2";
$ perl statement1.pl
Answer is 6
```

```
$ cat statement2.pl
$n = 4; say "Answer is $n+2";
$ perl statement2.pl
Answer is 6
```

Perl 表达式的语法通常对应 C 表达式的语法，但并不总是相同。Perl 表达式在本章的示例中都有涵盖。

引号所有字符串必须包含在单引号或双引号内。Perl 区分两种引号的方式与它处理的方式类似（见第 314 页）：双引号允许 Perl 插值包含在内的变量并解释特殊字符（如 \n，换行符），而单引号则不会。表 28-1 列出了 Perl 的一些特殊字符。

以下示例演示了不同类型的引号以及省略引号如何影响 Perl 在标量在数字和字符串之间的转换。第一条 `print` 语句中的单引号阻止了 Perl 插值 `$string` 变量并解释 `$n`。

```
$string = "hello";
print '$string';
print "$string\n";
```

与 shell 一样，Perl 中的注释以井号（#）开始，到行尾（换行符之前）结束。

表 28-1 列出了 Perl 中一些特殊字符。当这些字符出现在双引号内时，Perl 会进行插值，但当出现在单引号内时不会。第 176 页的表 28-3 列出了在正则表达式中特殊的字符。

表 28-1 特殊字符

| 字符 | 在双引号内，插值为 |
|---|---|
| \xx (零) | 进制值为 xx 的 ASCII 字符 |
| \a | 警报（蜂鸣声）字符 (ASCII 7) |
| \e | 转义字符 (ASCII 27) |
| \n | 换行符 (ASCII 10) |
| \r | 回车 (ASCII 13) |
| \t | 制表符 (ASCII 9) |

# 变量

人类语言一样，Perl 区分单数和复数。字符串和数字是单数的；字符串或数字列表是复数的。Perl 提供三种类型的变量：标量（单数）、数组（复数）和哈希（复数；也称为关联数组*）。Perl 通过名称前的特殊字符来识别每种类型。标量变量名称以美元符号（$）开始，哈希变量以 符号（@）开始。变量名称区分大小写，可以包含字母、数字和下划线字符（）。Perl 变量是包变量（见第 1045 页），除非它的前面有

关键字 `my` 在这种情况下是一个词法变量（第 1045 页），它仅在它出现的块或文件中定义。请参阅第 1071 页的“子程序”部分以讨论 Perl 变量的局部性。

## 词法变量会遮蔽包变量

如果一个词法变量和一个包变量（package variable）具有相同的名称，在定义该词法变量的块或文件中，该名称将指向词法变量而不是包变量。

当你给 Perl 变量赋值时，它就会存在——你不需要定义或初始化变量，尽管这可能会使程序更易于理解。通常情况下，Perl 在引用未初始化的变量时不会报错：

```
$ cat variable1.pl
#!/usr/bin/perl
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # 错误，漏掉了 name
```

```
$ perl variable1.pl
Hello, how are you?
```

使用 `strict` 可以强制 Perl 在变量赋值之前必须对其进行声明。更多信息请参见 `perldebug` 手册。当在前面的程序中包含 `strict` 时，Perl 会显示错误消息：

```
$ cat variable1b.pl
#!/usr/bin/perl
use strict;
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # 错误，漏掉了 name
```

```
$ perl variable1b.pl
Global symbol "nam" requires explicit package name at /variable1b.pl line 4.
Execution of /variable1b.pl aborted to compilation errors.
```
