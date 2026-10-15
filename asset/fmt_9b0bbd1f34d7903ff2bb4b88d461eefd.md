
#!/usr/bin/perl -w

print "Entry: 28";

$Sentry = <>

if ($Sentry == 28) { # 使用 == 进行数值比较

    print "Thank you for entering 28.\n";

}
```
$ ifl2.pl
Entry 28: 28.0
Thank you for entering 28.
End.

### 表 28-2 比较操作符

| 数值操作符 | 字符串操作符 |
| :--- | :--- |
| = | eq |
| != | ne |
| < | lt |
| > | gt |
| <= | le |
| >= | ge |
| == | cmp |
| != | ucmp |

由于 Perl 会自动对操作符左侧的单个单词加引号，你不需要在该程序的第三行中为 `boat` 加引号。然而，去掉 `number five` 周围的引号将产生错误，因为该字符串包含空格。

## 控制结构

控制流语句改变 Perl 程序中语句的执行顺序。从第 954 页开始，第 27 节详细讨论了 bash 控制结构并包含了流程图。Perl 控制结构使用了与其对应的 bash 结构，尽管这两种语言使用的语法不同。本节中对每个控制结构的描述均对应于 bash 中相同控制结构的讨论。

在本节中，语法描述中粗体加斜体的单词是你必须提供给该结构的项目；非斜体单词是 Perl 用于识别控制结构的关键字，而 `[...]` 表示一个语句块。第 1045 页。这些中的许多结构使用一个表示为 `expr` 的表达式来控制它们的执行。请参见 `if/unless` 以获取语法描述的示例和解释。

### if/unless

`if` 和 `unless` 控制结构是复合语句，具有以下语法：

- `if (expr) [...]`
- `unless (expr) [...]`

这些结构仅在于它们所执行的测试含义不同。`if` 结构在 `expr` 评估为真时执行语句块；`unless` 在 `expr` 评估为真时不执行，即当 `expr` 为假时执行语句块。

关键字以非粗体类型出现，因为它是一个关键字；它必须与所示完全一致。`expr` 是一个表达式；如果表达式的评估结果符合控制结构的要求，Perl 就会评估并执行由 `[...]` 表示的语句块。第 1045 页。

在接下来的示例中 `expr` `-r mem1` 使用 `-r` 文件操作符来判断工作目录中是否存在名为 `mem1` 的文件，以及该文件是否可读。尽管该操作符仅测试你对该文件是否有读取权限，但要获得读取权限，文件必须存在；因此它隐式地测试了文件是否存在。Perl 与 bash 使用相同的文件测试操作符；参见第 957 页的表 27-1。如果此表达式评估为真，Perl 将执行大括号之间的语句块，此情况下为一个。如果表达式评估为假，Perl 将跳过语句块。无论何种情况，Perl 都会退出并将控制权交还给 shell。

```perl
$ ifl1.pl

#!/usr/bin/perl -w

if (-r "memol") {

    say "The file 'memol' exists and is readable.";

}
```
$ ifl1.pl
The file 'memol' exists and is readable.

使用后置语法编写的示例程序。使用哪种语法取决于语句的哪个部分对代码阅读者更重要。

```perl
$ ifla.pl

#!/usr/bin/perl -w

say "The file 'memol' exists and is readable." if (-r "memol");
```

下一个示例使用 `print` 语句在标准输出上显示提示符，并使用语句 `$Sentry <>` 从标准输入读取并将行赋值给变量 `$Sentry`。从标准输入读取、与其它文件操作以及使用文件句柄 `<>` 读取命令行指定的文件的内容见第 1066 页。

Perl 用于比较数字的运算符与用于比较字符串的运算符不同。表 28-2 列出了数值和字符串比较操作符。在接下来的示例中，表达式使用 `==` 数值比较操作符来比较用户输入的 `28`、`28.0` 或 `00028`，所有情况下 Perl 都会执行数值比较，因此用户输入的任何比较结果都为真。此外，因为比较是数值型的，Perl 会忽略用户输入周围的空格和随后的换行符。`-w` 选项允许在用户输入非数值且程序在算术表达式中使用它时由 Perl 发出警告；如果没有此选项，Perl 将将表达式评估为假。

```perl
$ ifl2.pl

#!/usr/bin/perl -w

print "Entry: 28";

$Sentry = <>

if ($Sentry == 28) { # 使用 == 进行数值比较

    print "Thank you for entering 28.\n";

}
```
$ ifl2.pl
Entry 28: 28.0
Thank you for entering 28.
End.

### 表 28-2 比较操作符

| 数值操作符 | 字符串操作符 |
| :--- | :--- |
| = | eq |
| != | ne |
| < | lt |
| > | gt |
| <= | le |
| >= | ge |
| == | cmp |
| != | ucmp |

由于 Perl 会自动对操作符左侧的单个单词加引号，你不需要在该程序的第三行中为 `boat` 加引号。然而，去掉 `number five` 周围的引号将产生错误，因为该字符串包含空格。

## foreach/for

```
if ($num1 > $num2) {

    print "The first number is greater than the second number.\n";

} elsif ($num1 < $num2) {

    print "The first number is less than the second number.\n";

} else {

    print "Please enter two different numbers.\n";

}
```

Perl 中的 `foreach` 和 `for` 关键字是同义词；你可以在任何上下将它们互相替换。这些结构是具有两种语法的复合语句。有些程序员会在一种语法上使用 `foreach`，在另一种语法上使用 `for`，尽管没有必要这样做。本书在两种语法中均统一使用 `foreach`。

### foreach: 语法 1

`foreach` 结构的第一种语法类似于 shell 的 `for...in` 结构，见第 967 页：

```
foreach [var] (list) {...}
```

这是一个表达式或变量的列表。Perl 会为 `list` 中的每个项目执行语句块，在每次迭代中依次将 `var` 赋值为 `list` 中某项的值，并从第一个项目开始。如果你没有指定 `var`，Perl 将值赋值给变量 `$_`，见第 1065 页。

下面的程序演示了一个简单的 `foreach` 结构。在循环第一次通过中，Perl 将字符串 `Mo` 赋值给变量 `$item`，并通过 `say` 显示该变量的值。在循环的第二次和第三次通过中，`$item` 被赋值为 `Larry` 和 `Curly`。当列表中没有剩余项目时，Perl 继续执行该结构之后的语句。在这种情况下，程序终止。如果此程序抱怨 `say` 不可用，请参阅第 1047 页的 `feature 'say'`。

```
$ cat foreach.pl

foreach $item ("Mo", "Larry", "Curly") {

    say "$_ says hello.";

}
```
```
$ perl foreach.pl

Mo says hello.

Larry says hello.

Curly says hello.
```

使用 `$_`，见第 1065 页，你可以如下编写该程序：

```
$ cat foreach.pl

foreach ("Mo", "Larry", "Curly") {

    say "$_ says hello.";

}
```

# 第 28 章 Perl 脚本语言

以下是使用数组的程序：

```
$ cat foreachb.pl

@stooges = ("Mo", "Larry", "Curly");

foreach (@stooges) {

    say "$_ says hello";

}
```

以下是使用 `foreach` 后置语法的程序：

```
$ cat foreachc.pl

@stooges = ("Mo", "Larry", "Curly");
```
