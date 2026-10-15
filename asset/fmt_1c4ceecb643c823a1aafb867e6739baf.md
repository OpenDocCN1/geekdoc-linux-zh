
- 排序...................................................................... 1069

- 子程序............................................................ 1071

- 正则表达式................................................... 1073

- CPAN 模块........................................................... 1079

- 示例................................................................ 1081

Larry Wall 创建了 Perl（实用提取与报告语言）编程语言用于处理文本。Perl 使用来自 awk、sed、C、Bourne Shell、Smalltalk、Lisp 和英语的语法和概念。它的设计目的是从文本文件中扫描并提取信息，并根据这些信息生成报告。自1987年以来，Perl 巨大的增长——其文档也随之增长。今天，除了文本处理，Perl 还用于系统管理、软件开发和通用编程。

Perl 是可移植的，因为 Perl已经在许多操作系统上实现（见 `www.cpan.org/`）。Perl 是一种非正式、实用用、健壮、易用且完整的语言。它是一种支持过程化和面向对象编程的底层语言。它并不一定优雅。

Perl 与许多其他语言的区别之一是它的语言起源。在英语中，你会说“I will buy a car if I win the lottery”（如果我中彩票，我就买辆车）。Perl 允许我们模仿这种语法。另一个区别是 Perl 有单数和复数变量，前者持有单个值，后者持有值列表。

# 第 28 章 Perl 脚本语言

## Perl 简介

Perl 与许多其他语言的区别之一是它的语言起源。在英语中，你会说“I will buy a car if I win the lottery”。Perl 允许我们模仿这种语法。另一个区别是 Perl 有单数和复数变量，前者持有单个值，后者持有值列表。

## 1044 第 28 章 Perl 脚本语言

你也可以使用 `perld` 来显示文档：

```
$ perld pod.ex1.pl
```

POD.EX1(1) 用户贡献的 Perl 文档 POD.EX1(1)

# 一个用于说 Hi_there 的 Perl 程序。

这个简单的 Perl 程序包含了 pod 格式的文档。以下 `<cut` 命令告诉 `perld` 之后的内容不是文档。

# pod 文档通过任何 Pod 命令继续

请访问 `perld.perl.org/pod.html` 页面获取有关关于 pod 的更多信息，并访问 `perld.perl.org` 获取完整文档。

```
perl v5.10.0 2008-10-14 POD.EX1(1)
```

大多数公分发的模块和脚本以及 Perl 本身，都包含了 pod 格式的文档。例如，以下命令显示了 Perl 函数 `print` 的信息：

```
$ perld -f print
print FILEHANDLE LIST
print LIST -n 一个字符串或字符串列表。如果可访问则返回真。FILEHANDLE 包含文件 FILEHANDLE 的名称或引用，引入了一层间接。（注意：如果 FILEHANDLE 是一个变量且下一个标记是术语，它可能
```

一旦你安装了一个模块（第 1079 页），你就可以使用 `perld` 显示该模块的文档。下面的示例显示了 `perld` 显示本地安装的 `Timestamp::Simple` 的信息：

```
$ Timestamp::Simple
Timestamp::Simple(3) 用户贡献的 Perl 文档 Timestamp::Simple(3)
```

NAME

```
Timestamp::Simple - 时间戳的简单方法
```

```
SYNOPSIS
use Timestamp::Simple qw ($stamp);
print stamp, ":\n";
```

输入 `perld` 或 `perld perld` 命令来显示 `perld` 帮助页并在今天了解此内容。

# 使 Perl 程序具有可读性

提示 尽管 Perl 有许多适合一次次性编程的快捷方式，但本章介绍的代码易于理解且易于维护。

## 术语

本节定义了本章中用到的一些术语。

- `Module（模块）` Perl 模块是一个自包含的 Perl 代码块，通常包含几个协同工作的函数。模块可以从另一个模块或 Perl 程序中调用。模块必须有一个唯一的名称。为了帮助确保名称唯一，Perl 提供了一个层次化命名空间（第 1161 页），用双冒号（::）分隔名称的组件。示例模块名为 `Timestamp::Simple` 和 `WWW::Mechanize`。

- `Distribution（发行版）` Perl发行版是执行任务的一个或多个模块。你可以在 `search.cpan` 上搜索发行版和模块。发行版的示例包括 `Timestamp-Simple`（`Timestamp-Simple-01.tar.gz` 压缩文件仅包含 `Timestamp::Simple` 模块）和 `WWW-Mechanize-1.34.tar.gz` 包含 `WWW::Mechanize` 模块，支持的模块包括 `WWW::Mechanize::Link` 和 `WWW::Mechanize::Image`。

- `Package（包）` 包定义了一个命名空间。例如，名称 `WWW::Mechanize` 是 `WWW::Mechanize` 包中的标量变量，其中 "Package" 用于包名。将相同的名称（如 `WWW::Mechanize`）同时用于发行版、包可能会引起混淆。

- `Block（块）` 块是零或多个语句，由大括号（{}）界定，定义了一个作用域。作用域控制语法说明将这些元素称为注释。参见第 954 页的 *if-then-else* 结构示例。

- `Package variable（包变量）` 包变量定义在它所在的包中。其他包通过变量的全限定名称引用变量（例如，`State::columns`）。默认情况下，变量是词法变量，除非被声明为词法。

- `Lexical variable（词法变量）` 词法变量通过在变量名前加上关键字 `my` 来定义（见第 1050 页的提示），它仅定义在它所在的块或文件中。在其他语言中，词法变量被称为局部变量。Perl 4 在其语言使用了 lexical 一词。在用 bash 编程时，未导出（第 992 页）的变量是数字和字符串：

- `Array（数组）` 数组是零或多个标量的列表。以下列表有三个元素——两个数字和一个字符串：

```
(2, 4, 'zach')
```

```
@ = (2, 4, 'Zach')
```

- `Compound statement（复合语句）` 复合语句是由其他语句组成的语句。例如，if 复合语句（第 1057 页）包含一个 if，它通常在它所控制的块内包含其他语句。

## 运行 Perl 程序

有几种方法可以运行用 Perl 编写的程序。`-e` 选项允许你在命令行上输入程序：

```
$ perl -e 'print "Hi.\n"'
Hi there.
```

`-e` 选项是测试 Perl 语法和运行简短、一次性程序的好选择。该选项要求 Perl 程序以单个参数的形式出现在命令行上。该程序必须紧随其后——它是该选项的参数。编写此类程序的一种简单方法是将程序封装在引号内。

由于 Perl 属于从文件或标准输入（第 248 页）读取输入的工具类，你可以输入 `perl` 命令并输入以 0EOF（文件末尾）结束的程序。Perl 读取该程序：

```
$ perl
print "Hi.\n"
Ctrl+D
```

## Perl 5.10 版本

本章中的所有示例都在 Perl 5.10 下运行。输入以下命令查看本地系统运行的 Perl 版本：

```
$ perl -v
This is perl, v5.10.0 built for 1486-linux-gnu-thread-multi
```

`use feature 'say'` 该函数是 Perl 5.10 可用的特性。它的工作方式与 `print` 相同，但在它输出的每行末尾添加一个换行符。某些 Perl 版本需要你显式告诉 Perl 你你想使用 `say`。示例中的 `use` 函数告诉我们：尝试在没有 use 行的情况下运行此程序，查看本地 Perl 版本是否需要它。
