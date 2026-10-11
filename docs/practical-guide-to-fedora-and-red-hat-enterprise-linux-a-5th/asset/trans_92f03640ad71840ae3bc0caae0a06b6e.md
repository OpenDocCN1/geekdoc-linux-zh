

## 反斜杠

在由双引号包围的字符串中，反斜杠用于转义（引用）另一个反斜杠。因此，Perl 将 `"\n"` 显示为 `\n`。在正则表达式中，Perl 不会展开位于反斜杠之后的元字符。请参阅前页中的 string1.pl 程序。

## 注释

与 Shell 一样，Perl 中的注释以井号 (#) 开头，并在行末（即换行符 NEWLINE 之前）结束。

## 特殊字符

表 28-1 列出了 Perl 字符串中的一些特殊字符。当这些字符出现在双引号之间时，Perl 会对其进行插值；但当它们出现在单引号之间时，则不会。第 1010 页的表 28-3 列出了元字符，它们在正则表达式中具有特殊含义。

### 表 28-1：一些 Perl 特殊字符

| 字符 | 在双引号内时，被插值为 |
| :---- | :---- |
| \0xx (零) | 八进制值为 xx 的 ASCII 字符 |
| \a | 报警符（铃声或哔声）字符（ASCII 7） |
| \e | 转义字符 ESCAPE（ASCII 27） |
| \n | 换行符 NEWLINE 字符（ASCII 10） |
| \r | 回车符 RETURN 字符（ASCII 13） |
| \t | 制表符 TAB 字符（ASCII 9） |

# 变量

与人类语言类似，Perl 区分单数数据和复数数据。字符串和数字是单数的；字符串或数字的列表是复数的。Perl 提供三种类型的变量：*标量*（单数）、*数组*（复数）和*哈希*（复数；也称为*关联数组*）。Perl 通过位于变量名前的特殊字符来标识每种变量类型。标量变量的名称以美元符号 ($ ) 开头，数组变量以 at 符号 (@) 开头，哈希变量以百分号 (%) 开头。与 Shell 识别变量的方式不同，Perl 要求每次引用变量时（包括给变量赋值时）都必须包含前导字符：

```bash
$ name="Zach" ; echo "$name"
Zach
```

```perl
$ perl -e '$name="Zach" ; print "$name\n";'
Zach
```

变量名区分大小写，可以包含字母、数字和下划线字符 (_)。除非变量前有关键词 *my*，否则 Perl 变量是包变量（第 979 页），如果有关键词 *my*，则它是词法变量（第 979 页），仅在定义它的块或文件中有效。有关 Perl 变量局部性的讨论，请参阅第 1005 页的“子例程”。

## 词法变量遮蔽包变量

> 如果一个词法变量和一个包变量具有相同的名称，那么在定义该词法变量的块或文件内，该名称指的是词法变量，而不是包变量。

Perl 变量在您为其赋值时即开始存在——您不需要定义或初始化变量，尽管这样做可能会使程序更易于理解。通常，当引用未初始化变量时，Perl 不会发出警告：

```bash
$ cat variable1.pl
#!/usr/bin/perl
my $name = 'Sam';
print "Hello, $name, how are you?\n"; # 拼写错误，name 中少了 e

$ ./variable1.pl
Hello, , how are you?
```

**use strict** 包含 **use strict** 可以强制 Perl 要求在赋值前声明变量。有关更多信息，请参阅 **perldebtut man 页面**。当您在上述程序中包含 **use strict** 时，Perl 会显示一条错误消息：

```bash
$ cat variable1b.pl
#!/usr/bin/perl
use strict;
my $name = 'Sam';
print "Hello, $name, how are you?\n"; # 拼写错误，name 中少了 e

$ ./variable1b.pl
Global symbol "$name" requires explicit package name at ./variable1b.pl line 4.
Execution of ./variable1b.pl aborted due to compilation errors.
```

## 使用 *my*：词法变量与包变量

> 在 *variable1.pl* 中，通过在 $name 前加上关键词 **my**，将其声明为词法变量；其名称和值仅在文件 *variable1.pl* 内已知。将变量声明为词法变量将其作用域限制在定义它的块或文件中。虽然在此情况下并非必要，但将变量声明为词法变量是一种好习惯。当编写较长的程序、子例程和包时，这种习惯变得尤为有用，因为在那时更难保持变量名的唯一性。当您编写将被他人编写的代码使用的例程时，强制将所有变量声明为词法变量是必须的。这种做法允许使用您的例程的人使用任何他们喜欢的变量名称，而无需考虑您代码中使用的变量名称。
> 
> Shell 和 Perl 对变量的作用域处理不同。在 Shell 中，如果您没有 **export**（导出）变量，则该变量仅在使用它的那个例程内有效（第 926 页）。在 Perl 中，如果您不使用 **my** 将变量声明为词法变量，则该变量在其所属的包中定义。

## 标量变量

**\-w** 选项和 **use warnings** 语句执行相同的功能：它们使 Perl 在检测到语法错误时生成错误消息。在以下示例中，Perl 显示两个警告。第一个警告告诉您，您在第 3 行使用了名为 **$nam** 的变量，这可能表明存在错误。当您弄错变量名称时，此消息很有帮助。在 Perl 5.10 下，第二个警告指定了未初始化变量的名称。此警告指的是与第一个警告相同的问题。虽然在这个简单程序中弄清楚这两个变量中哪一个是未定义的不难，但在复杂程序中这样做可能需要大量时间。

```bash
$ cat variable1.pl
#!/usr/bin/perl -w
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # 由于拼写错误和 -w 产生警告
```

```bash
$ ./variable1.pl
Name "main::nam" used only once: possible typo at ./variable1.pl line 3.
Use of uninitialized value $nam in concatenation (.) or string at ./variable1.pl line 3.
Hello, , how are you?
```

您还可以在命令行上使用 **\-w**。如果您也使用 **\-e**，请确保该选项后面的参数是您想要执行的程序（例如，**\-e \-w** 不起作用）。请参阅第 1008 页的提示。

```bash
$ perl -w -e 'my $name = "Sam"; print "Hello, $nam, how are you?\n"'
Name "main::nam" used only once: possible typo at -e line 1.
Use of uninitialized value $nam in concatenation (.) or string at -e line 1.
Hello, , how are you?
```

未定义变量具有特殊值 **undef**，它在数值表达式中评估为零 (0)，在打印时扩展为空字符串 ("")。使用 **defined** 函数来确定变量是否已定义。以下示例使用了本章稍后解释的结构，它调用 **defined** 并以 **$name** 为参数，并用感叹号 (!) 取反结果。其结果是，如果 **$name** *未*定义，则执行 **print** 语句。

```bash
$ cat variable2.pl
#!/usr/bin/perl
if (!defined($name)) {
    print "The variable '$name' is not defined.\n";
}

$ ./variable2.pl
The variable '$name' is not defined.
```

由于 **\-w** 选项会在您引用未定义变量时警告您，因此使用此选项将生成一条警告。

标量变量的名称以美元符号 ($) 开头，并包含单个字符串或数字：它是单数变量。由于 Perl 在必要时会在两者之间进行转换，您可以互换使用字符串和数字。当将标量变量解释为字符串有意义时，Perl 将其解释为字符串；当将其解释为数字有意义时，则解释为数字。在这些问题上，Perl 的判断通常是很好的。

以下示例展示了标量变量的一些用法。代码的前两行（第 3 行和第 4 行）分别将字符串 Sam 赋值给标量变量 $name，将数字 5 和 2 赋值给标量变量 $n1 和 $n2。在此示例中，多个语句（每个语句以分号 (;) 结尾）出现在同一行上。如果此程序抱怨说 `say` 不可用，请参阅第 981 页关于 `use feature 'say'` 的内容。

```bash
$ cat scalars1.pl
#!/usr/bin/perl -w

$name = "Sam";
$n1 = 5; $n2 = 2;

say "$name $n1 $n2";
say "$name $n1 $n2";
say $n1 + $n2, "", $n1 * $n2;
say $name + $n1;

$ ./scalars1.pl
Sam 5 2
$name $n1 $n2
7 10
5
```

双引号 第一个 say 语句将双引号包围的字符串发送到标准输出（除非重定向，否则是屏幕）。在双引号内，Perl 将变量名称扩展为指定变量的值。因此，第一个 say 语句显示三个变量的值，它们彼此之间用空格分隔。第二个 say 语句包含一个加号 (+)。Perl 不识别双引号或单引号内的 + 等运算符。因此，Perl 在两个变量的值之间显示加号。

单引号 第三个 say 语句将单引号包围的字符串发送到标准输出。在单引号内，Perl 按字面意思解释所有字符，因此它准确地显示单引号之间的字符串。

在第四个 say 语句中，运算符未被加引号，Perl 执行指定的加法和乘法。如果没有加引号空格，Perl 将连接这两个数字 (710)。最后一个 say 语句尝试将字符串和数字相加；-w 选项使 Perl 在显示 5 之前显示一条错误消息。这个 5 是将 Sam 加到数字 5 上得到的结果，Perl 在数值上下文中将 Sam 评估为 0 (0 + 5 = 5)。

