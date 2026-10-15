
与之前看到的 `Dumper()` 输出相比，新的 `display()` 函数增加了缩进，有助于区分数据结构的不同层。它还增加了详细信息，提醒你在任何给定层级是在探索数组还是哈希表（hash）。

## 垃圾回收与引用计数

将本章的最后一部分视为可选阅读。你可能会发现了解 Perl 如何管理内存会有帮助。另一方面，你可能会发现这极其令人困惑。

当你使用 `my` 关键字时，你是在请求 Perl 给你一段内存。这块内会在请求时创建，并在当执行到达相同作用域内的右大括号时被返回给你的计算机。下面的无限循环会不断地分配和释放内存：

```
while (1) {

  $variable = 'something';

}
```

“底层”发生的是：与 `$variable` 关联的内存在第 2 行创建时被赋予为 1 的引用计数。当执行到第 3 行的右大括号时，引用计数减 1 变为 0。任何引用计数为 0 的内存位置都会归还给计算机。释放未使用内存的行为被称为垃圾回收。

现在让我们考虑我们在第 6.3 节中解决过的问题。具体来说，如果 `@array` 在每次循环时都重新创建，那么 `@array` 的内容是如何存在于 `@table` 中的？

```
#!/usr/bin/perl
# csv_reader.pl
use strict; use warnings;

my @table; {
while (<>) {
my @array = split(/, /, $_);
push @table, @array;
}
```

如果你使用反斜杠运算符对变量进行引用，你会将其引用计数加1。这就是为什么与 `@array` 关联的内存每次循环都不会被销毁。第 7 行与 `@array` 关联的内存引用计数等于 1。但在第 8 行，通过反斜杠计数增加到了 2。在第 9 行，当 `@array` 离开作用域时，引用计数减 1。但该内存位置仍有 1 个引用，因此它不会被释放。结果，`@table` 满了数组引用。

引用计数垃圾回收非常高效，但它在循环引用方面有问题。代码为 `$variable` 分配了自身的引用，因此它的引用计数降为 1 且永远不会变为 0。因此，`$variable` 会不断分配内存而从不释放。

```
while (1) {
my $variable;
$variable = \variable;
}
```

> 警告：这可能会导致你的计算机崩溃！

## 6.7 添加命令行选项

选项的使用也是可选的。你将使用的大多数 Unix 命令行程序都会使用控制其行为的选项。例如，Unix `ls` 命令列出当前目录，但如果你想按日期排序文件，可以使用 `ls -lt`。你的 Perl 程序也可以轻松拥有这种行为。有两个内置模块处理命令行选项：`Getopt::Std` 和 `Getopt::Long`。使用这些模块可以为你的程序添加功能。根据需要，可以使用命令行选项代替或结合 `@ARGV`。

## Getopt::Std

`Getopt::Std` 用于单字符选项。多个选项的行为与其他命令行程序一样。如果有多个选项，可以将它们合并。例如 `-lt` 可以写成 `-lt`。对于带有额外参数的选项，例如 `-o`，选项和参数之间的空格可以省略：两者含义相同。让我们看看效果。以下脚本可以作为你程序的模板。

## 示例 6.7.1

```
#!/usr/bin/perl
# getopt_std.pl
use strict; use warnings;
use Getopt::Std;

my $usage = "usage: getopt.pl [options] <arguments>";
options:
-v
-f
-p <some parameter>
""
die $usage unless @ARGV;

my $opt;
getopts('hvfp:', $opt);

if ($opt{h}) { print $usage; exit; }
if ($opt{v}) { print "1.0\n"; exit; }
if ($opt{f}) { print "flag turned on\n"; }
if ($opt{p}) { print "Parameter is: $opt{p}\n"; }

print "Other arguments were: @ARGV\n";
```

### 理解脚本

1–4 行是带有 `Getopt::Std` 的典型头部内容。6–11 行包含典型的用法说明，用于提醒用户程序支持的所有选项。`$usage` 字符串跨越了几行。如果没有给出命令行参数，第 12 行的 `die()` 将停止并打印用法说明。Perl 脚本通常需要一个或多个文件作为输入，如果你的程序不需要任何参数，应省略第 12 行。14–15 行用于从命令行移除选项并将其放入 `%opt` 变量中。字符串 `'hvfp:'` 是关键部分。四个选项：`-h`, `-v`, `-f` 和 `-p`。`p` 后面的冒号表示需要一个额外参数。其他选项不需要参数。17–20 行根据选项执行不同操作。这里是简单的单行，但在更大的程序中可能会复杂得多。此脚本包含了打印帮助信息的方法——尝试使用 `get_std.pl` 的以下选项看看结果：

```
$get_std.pl # prints usage

$get_std.pl -h # prints $usage

$get_std.pl -v # prints version

$get_std.pl -x # reports an error: there is no option -x

$get_std.pl -fp # reports flag on, -p is
```

## Getopt::Long

`Getopt::Long` 用于更长、描述性更选项，例如 `--version`。选项名以两个连字符开头。对于带有参数的选项，你不需要选项和参数之间的空格。你可以使用 `--option x` 或 `--option=x`。这里是对应的模板。

## 示例 6.7.2

```
#!/usr/bin/perl
# getopt_long.pl
use strict; use warnings;
use Getopt::Long;

my $usage = "usage: getopt.pl [options] <arguments>..."
options:
--version
--help
--flag <number>
--number <string>
--string <string>
";

my $flag; # 某些布尔标志
my $number; # 将包含一个数字
my $string; # 将包含一个字符串

GetOptions(
"flag" => \$flag,
"number-i" => \$number,
"string=s" => \$string,
"version" => sub { print "1.0\n"; exit},
"help" => sub { print \$usage; exit},
);

if ($flag) { print "flag turned on\n" }
if ($string) { print "string set: $string\n" }
if ($number) { print "number set: $number\n" }

print "Other arguments were: @ARGV\n";
```

### 理解脚本

1–4 行是典型的头部内容，但注意我们现在使用的是 `Getopt::Long` 而不是 `Getopt::Std`。6–13 行包含了熟悉的用法。

## 添加命令行选项

第 23 行和 24 行包含了用于报告版本和用法信息的匿名子程序。什么是匿名子程序？它是一个仅作为引用存在的子程序。在在这方面，它类似于匿名数组或匿名哈希表。通常情况下，我们并不使用匿名子程序，这就是为什么我们在这书中没有专门讨论子程序引用的原因。但这一个是无害且方便的。

添加了第 27–29 行来测试了哪些命令行选项。某些程序会回显所选的选项以提供额外的确认。

尝试运行以下命令行选项来实验该脚本：

```
$ get_long.pl               # 这一次没有帮助
$ get_long.pl --version      # 打印版本
$ get_long.pl --help          # 打印用法
$ get_long.pl --flag --number=2 # 开启 flag，数字为 2
$ get_long.pl --string hooray # 字符串为 hooray
```
