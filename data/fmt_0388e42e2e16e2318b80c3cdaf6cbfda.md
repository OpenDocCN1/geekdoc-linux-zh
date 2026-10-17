
```bash
$ cat if2a.pl
#!/usr/bin/perl -w
print "Enter the word 'five': ";
$entry = <>;
chomp ($entry);
if ($entry eq "five") { # use eq for a string comparison
    print "Thank you for entering 'five'.\n";
}
print "End.\n";

$ ./if2a.pl
Enter the word 'five': five
Thank you for entering 'five'.
End.
```

### if...else

`if`... `else` 控制结构是一个复合语句，类似于 bash `if`... `then`... `else` 控制结构（第 892 页）。它使用以下语法实现双向分支：
`if` (`expr`) {...} `else` {...}
下一个程序提示用户输入两个不同的数字，并将这些数字存储在 `$num1` 和 `$num2` 中。如果用户两次输入相同的数字，`if` 结构将执行一个 `die` 函数，该函数将其参数发送到标准错误并中止程序执行。如果用户输入不同的数字，`if`... `else` 结构将报告哪个数字较大。由于 `expr` 执行数值比较，因此程序接受包含小数点的数字。

```bash
$ cat ifelse.pl
#!/usr/bin/perl -w
print "Enter a number: ";
$num1 = <>;
print "Enter another, different number: ";
$num2 = <>;

if ($num1 == $num2) {
    die ("Please enter two different numbers.\n");
}
if ($num1 > $num2) {
    print "The first number is greater than the second number.\n";
}
else {
    print "The first number is less than the second number.\n";
}

$ ./ifelse.pl
Enter a number: 8
Enter another, different number: 8
Please enter two different numbers.

$ ./ifelse.pl
Enter a number: 5.5
Enter another, different number: 5
The first number is greater than the second number.
```

### if...elsif...else

与 bash `if`... `then`... `elif` 控制结构（第 895 页）类似，Perl `if`... `elsif`... `else` 控制结构是一个复合语句，使用以下语法实现嵌套的 `if`... `else` 结构集合：

```perl
if (expr) {...} elsif (...) ... else {…}
```

下一个程序使用 `if`... `elsif`... `else` 结构实现前面 `ifelse.pl` 程序的功能。使用 `print` 语句代替 `die` 语句，因为程序中的最后一条语句显示错误消息；无论哪种情况，程序在执行此语句后都会终止。您可以使用 `STDERR` 句柄（第 1000 页）使 Perl 将此消息发送到标准错误而不是标准输出。

```bash
$ cat ifelsif.pl
#!/usr/bin/perl -w
print "Enter a number: ";
$num1 = <>;
print "Enter another, different number: ";
$num2 = <>;
```

## foreach/for

Perl 的 `foreach` 和 `for` 关键字是同义词；你可以在任何上下文中将一个替换为另一个。这些结构是复合语句，具有两种语法。一些程序员使用 `foreach` 配合一种语法，使用 `for` 配合另一种语法，尽管这样做并没有必要。本书使用 `foreach` 配合这两种语法。

### foreach：语法 1

`foreach` 结构的第一种语法类似于 shell 的 `for`...`in` 结构（第 901 页）：

```perl
foreach[for] $var (list) {...}
```

其中 `list` 是表达式或变量的列表。Perl 为 `list` 中的每个项目 `执行一次` 语句块，在每次迭代中依次将 `list` 中某一项的值分配给 `var`，从第一项开始。如果你未指定 `var`，Perl 会将值分配给 `$_` 变量（第 999 页）。
下面的程序演示了一个简单的 `foreach` 结构。在循环的第一次遍历中，Perl 将字符串 `Mo` 分配给变量 `$item`，然后 `say` 语句显示该变量的值后跟一个换行符（NEWLINE）。在循环的第二和第三次遍历中，`$item` 分别被分配值 `Larry` 和 `Curly`。当列表中不再有项目时，Perl 继续执行位于 `foreach` 结构之后的语句。在这种情况下，程序终止。如果该程序报告 `say` 不可用，请参见第 981 页关于 `use feature 'say'` 的内容。

```perl
$ cat foreach.pl
foreach $item ("Mo", "Larry", "Curly") {
    say "$item says hello.";
}
```

```bash
$ perl foreach.pl
Mo says hello.
Larry says hello.
Curly says hello.
```

使用 `$_`（第 999 页），你可以将程序编写如下：

```perl
$ cat foreacha.pl
foreach ("Mo", "Larry", "Curly") {
    say "$_ says hello.";
}
```

以下是使用数组的程序：

```perl
$ cat foreachb.pl
@stooges = ("Mo", "Larry", "Curly");
foreach (@stooges) {
    say "$_ says hello.";
}
```

以下是使用 foreach 后缀语法的程序：

```perl
$ cat foreachc.pl
@stooges = ("Mo", "Larry", "Curly");
say "$_ says hello." foreach @stooges;
```

循环变量（前述示例中的 `$item` 和 `$_`）引用括号内列表中的元素。当你修改循环变量时，你实际上是在修改列表中的元素。`uc` 函数返回其参数的全大写版本。下一个示例表明，修改循环变量 `$stooge` 会修改 `@stooges` 数组：

```perl
$ cat foreachd.pl
@stooges = ("Mo", "Larry", "Curly");
foreach $stooge (@stooges) {
    $stooge = uc $stooge;
    say "$stooge says hello.";
}
say "@stooges[1] is uppercase";
```

```bash
$ perl foreachd.pl
MO says hello.
LARRY says hello.
CURLY says hello.
LARRY is uppercase
```

参见第 1003 页关于遍历命令行参数的示例。

## last 和 next

Perl 的 `last` 和 `next` 语句允许你中断循环；它们类似于 Bourne Again Shell 的 `break` 和 `continue` 语句（第 910 页）。`last` 语句将控制权转移到循环结构控制的语句块之后的语句，从而终止循环的执行。`next` 语句将控制权转移到语句块的末尾，继续以下一次迭代执行循环。
在下面的程序中，`if` 结构测试 `$item` 是否等于字符串 `two`；如果是，该结构执行 `next` 命令，跳过 `say` 语句并继续循环的下一次迭代。如果你将 `next` 替换为 `last`，Perl 将从循环中退出，并且不会显示 `three`。如果该程序报告 `say` 不可用，请参见第 981 页关于 `use feature 'say'` 的内容。

```perl
$ cat foreachl.pl
foreach $item ("one", "two", "three") {
    if ($item eq "two") {
        next;
    }
    say "$item";
}
```
