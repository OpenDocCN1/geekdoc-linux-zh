

## 术语

本节定义了本章中使用的一些术语。

Perl *模块* 是一组自包含的 Perl 代码，通常包含几个协同工作的函数。模块可以从另一个模块或 Perl 程序中被调用。模块必须具有唯一的名称。为了帮助确保名称唯一性，Perl 为模块提供了一个层级式*命名空间*（第 1095 页），使用双冒号 (::) 分隔名称的组成部分。示例模块名称包括 `Timestamp::Simple` 和 `WWW::Mechanize`。

Perl *发行版* 是一组执行特定任务的一个或多个模块。你可以在 search.cpan.org 上搜索发行版和模块。发行版的示例包括 `Timestamp-Simple`（`Timestamp-Simple-1.01.tar.gz` 归档文件仅包含 `Timestamp::Simple` 模块）和 `WWW-Mechanize`（`WWW-Mechanize-1.34.tar.gz` 包含 `WWW::Mechanize` 模块，以及包括 `WWW::Mechanize::Link` 和 `WWW::Mechanize::Image` 在内的支持模块）。

*包* 定义了一个 Perl 命名空间。例如，在名为 `$WWW::Mechanize::ex` 的变量中，`ex` 是 `WWW::Mechanize` 包中的一个标量变量，其中“包”一词用于指代命名空间。如果对发行版、包和模块使用相同的名称（例如 `WWW::Mechanize`），可能会造成混淆。

*代码块* 是由大括号 ({} 定义的一组语句（零条或多条），它们定义了一个作用域。Shell 控制结构语法说明将这些元素称为*命令*。请参阅第 888 页上的 if...then 控制结构以获取示例。

*包变量* 在其所属的包内定义。其他包可以通过使用变量的完全限定名称（例如，`$Text::Wrap::columns`）来引用包变量。除非你将变量定义为词法变量，否则变量默认是包变量。

*词法变量* 通过在变量名称前加 `my` 关键字进行定义（参见第 984 页的技巧），它仅在其出现的代码块或文件中有效。其他语言将词法变量称为局部变量。由于 Perl 4 使用了具有不同含义的 `local` 关键字，Perl 5 使用关键字*词法*来替代它。在使用 `bash` 编程时，未导出的变量（第 926 页）是其所使用的程序的局部变量。

*列表* 是由零个或多个标量组成的序列。以下列表有三个元素——两个数字和一个字符串：

```
    ( 2, 4, 'Zach' )
```

*数组* 是一个变量，它以定义的顺序保存一组元素。在下一行代码中，`@a` 是一个数组。有关数组变量的更多信息，请参见第 987 页。

```
    @a = ( 2, 4, 'Zach' )
```

*复合语句* 是由其他语句组成的语句。例如，`if` 复合语句（第 991 页）包含一个 `if` 语句，该语句通常在其控制的代码块内包含其他语句。

## 运行 Perl 程序

有几种方法可以运行用 Perl 编写的程序。-e 选项允许你在命令行中输入程序：

```
$ perl -e 'print "Hi there.\n"'
Hi there.
```

-e 选项是测试 Perl 语法和运行简短的一次性程序的不错选择。此选项要求 Perl 程序作为单个参数出现在命令行上。程序必须紧跟在此选项之后——它是该选项的一个参数。编写此类程序的一种简单方法是将程序包裹在单引号中。

由于 Perl 属于从文件或标准输入（第 234 页）获取输入的一类实用工具，你可以输入命令 perl 并键入程序，以 CONTROL-D（文件结束符）终止。Perl 从标准输入读取程序：

```
$ perl
print "Hi there.\n";
CONTROL-D
Hi there.
```

上述技术适用于快速的一次性命令行程序，但对于运行更复杂的程序没有帮助。大多数时候，Perl 程序存储在文本文件中。虽然并非必须，但文件通常具有 .pl 文件扩展名。以下是在前几个示例中使用的相同简单程序，存储在一个文件中：

```
$ cat simple.pl
print "Hi there.\n";
```

你可以通过将其名称指定为 Perl 的参数来运行此程序：

```
$ perl simple.pl
Hi there.
```

与大多数 shell 脚本类似，包含 Perl 程序的文件通常具有可执行权限。在以下示例中，chmod（第 287 页）使 simple2.pl 文件具有可执行权限。如第 288 页所述，文件第一行开头的 #! 指示 shell 将文件的其余部分传递给 /usr/bin/perl 执行。

```
$ chmod 755 simple2.pl
$ cat simple2.pl
#!/usr/bin/perl -w
print "Hi there.\n";

$ ./simple2.pl
Hi there.
```

在此示例中，simple2.pl 程序作为 ./simple2.pl 执行，因为工作目录不在用户的 PATH（第 306 页）中。-w 选项指示 Perl 在识别代码中潜在错误时发出警告消息。

## PERL 版本 5.10

本章中的所有示例都是在 Perl 5.10 下运行的。请执行以下命令查看本地系统正在运行哪个版本的 Perl：

```
$ perl -v
This is perl, v5.10.0 built for i486-linux-gnu-thread-multi
...
```

say 函数是一个 Perl 6 特性，在 Perl 5.10 中可用。它的工作方式与 print 相同，只是它在输出的每一行末尾添加了一个 NEWLINE (\n)。某些版本的 Perl 需要你明确告诉 Perl 你想使用 say。以下示例中的 use 函数告诉 Perl 启用 say。尝试在没有 use 行的情况下运行此程序，以查看本地版本的 Perl 是否需要它。

```
$ cat 5.10.pl
use feature 'say';
say 'Output by say.';
print 'Output by print.';
say 'End.'

$ perl 5.10.pl
Output by say.
Output by print.
Output by say.End.
```

如果你正在运行较早版本的 Perl，你需要将本章示例中的 say 替换为 print，并用引号括起的 \n 终止 print 语句：

```
$ cat 5.8.pl
print 'Output by print in place of say.', "\n";
print 'Output by print.';
print 'End.', "\n";

$ perl 5.8.pl
Output by print in place of say.
Output by print.
Output by End.
```

## 语法

本节描述了 Perl 程序的主要组成部分。

Perl 程序由一个或多个*语句*组成，每个语句以分号 (;) 结尾。就*空白字符*（第 1115 页）而言，这些语句是自由格式的，但引号内的字符串中的空白字符除外。多个语句可以出现在同一行上，每个语句以分号结尾。以下程序是等效的。第一个占两行，第二个只占一行；请查看加号和等号周围间距的差异。如果这些程序抱怨 say 不可用，请参阅**use feature 'say'**（上述部分）。

```
$ cat statement1.pl
$n = 4;
say "Answer is ", $n + 2;
$ perl statement1.pl
Answer is 6
```

```
$ cat statement2.pl
$n = 4; say "Answer is ", $n+2;
$ perl statement2.pl
Answer is 6
```

Perl 表达式的语法通常对应于 C 表达式的语法，但并非总是相同。Perl 表达式在本章的各个示例中都有涉及。

所有字符字符串都必须包裹在单引号或双引号中。Perl 区分这两种引号的方式类似于 shell 的方式（第 301 页）：双引号允许 Perl 对括在其中的变量进行插值，并解释 `\n` (**NEWLINE**) 等特殊字符，而单引号则不允许。表 28-1 列出了 Perl 的一些特殊字符。

以下示例展示了不同类型的引号以及没有引号如何影响 Perl 在数字和字符串之间转换标量。第一个 **print** 语句中的单引号阻止 Perl 对 **$string** 变量进行插值，并解释 `\n` 特殊字符。第二个 **print** 语句开头的 `\n` 强制该语句的输出出现在新的一行。

```
$ cat stringl.pl
$string="5";     # $string 声明为字符串，但这并不重要

print '$string+5\n';    # 由于单引号，Perl 字面显示 $string+5
                       #
print "\n$string+5\n";     # 由于双引号，Perl 将 $string 的值作为字符串插值
                       #
print $string+5, "\n"; # 缺少引号导致 Perl 将
                       # $string 解释为数值变量并加 5；
                       # \n 必须出现在双引号之间

$ perl stringl.pl
$string+5\n
5+5
10
```

默认情况下，正则表达式由斜杠 (//) 分隔。以下示例测试字符串 **hours** 是否包含模式 **our**；有关 Perl 中正则表达式定界符的更多信息，请参见第 1008 页。

```
$ perl -e 'if ("hours" =~ /our/) { say "yes";}'
```

本地版本的 Perl 可能需要 **use feature** 'say'（第 981 页）才能正常工作：

```
$ perl -e 'use feature "say"; if ("hours" =~ /our/) { say "yes";}'
```

