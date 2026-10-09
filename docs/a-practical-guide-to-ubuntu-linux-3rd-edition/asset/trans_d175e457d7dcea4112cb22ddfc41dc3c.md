

```bash
$ cat statement1.pl
$n=4;
say "Answer is ", $n + 2;
$ perl statement1.pl
Answer is 6

$ cat statement2.pl
$n = 4; say "Answer is ", $n=2;
$ perl statement2.pl
Answer is 6
```

**表达式** Perl 表达式的语法通常对应于 C 语言表达式的语法，但并不总是相同。本章通过示例涵盖了 Perl 表达式的相关说明。

**引号** 所有字符串都必须包含在单引号或双引号内。Perl 区分这两种引号的方式类似于 shell 的做法（见第 314 页）：双引号允许 Perl 对内部包含的变量进行插值，并解释特殊字符，例如 `\n`（换行符），而单引号则不会。表 28-1 列出了 Perl 的一些特殊字符。

以下示例展示了不同类型的引号以及缺失引号如何影响 Perl 在数字和字符串之间转换标量。第一条 **print** 语句中的单引号阻止 Perl 对 **$string** 变量进行插值，也阻止其解释 `\n` 特殊字符。第二条 **print** 语句开头的 `\n` 强制该语句的输出显示在新的一行。

```bash
$ cat string1.pl
$string="5"; # $string 被声明为字符串，但这并不重要

print '$string+5\n'; # 由于单引号，Perl 会按字面显示 $string+5
print "\n$string+5\n"; # 由于双引号，Perl 将 $string 的值解释为字符串
print $string+5, "\n"; # 缺少引号导致 Perl 将 $string 解释为数字变量并加上 5；
                       # \n 必须出现在双引号内

$ perl string1.pl
$string+5
5+5
10
```

**斜杠** 默认情况下，正则表达式由斜杠 (/) 分隔。以下示例测试字符串 **hours** 是否包含模式 **our**；有关 Perl 中正则表达式分隔符的更多信息，请参见第 1074 页。

```bash
$ perl -e 'if ("hours" =~ /our/) {say "yes";}'
```

本地版本的 Perl 可能需要 **use feature 'say'**（第 1047 页）才能正常工作：

```bash
$ perl -e 'use feature "say"; if ("hours" =~ /our/) {say "yes";}'
```

**反斜杠** 在由双引号包围的字符串中，反斜杠用于转义（引用）另一个反斜杠。因此，Perl 将 `\"\\n\"` 显示为 `\n`。在正则表达式中，Perl 不会展开反斜杠后面的元字符。请参见上一页的 `string1.pl` 程序。

**注释** 与 shell 类似，Perl 中的注释以井号 (#) 开头，并结束于行尾（即在 NEWLINE 字符之前）。

**特殊字符** 表 28-1 列出了 Perl 字符串中的一些特殊字符。当这些字符出现在双引号之间时，Perl 会解释它们；但当它们出现在单引号之间时，则不会。第 1076 页的表 28-3 列出了元字符，这些字符在正则表达式中具有特殊含义。

### 表 28-1：Perl 的部分特殊字符

| 字符 | 在双引号内时，作为什么进行插值 |
| :--- | :--- |
| **\0**xx (零) | 八进制值为 **xx** 的 ASCII 字符 |
| **\a** | 警报（铃声或哔声）字符（ASCII 7） |
| **\e** | ESCAPE（转义）字符（ASCII 27） |
| **\n** | 换行符（ASCII 10） |
| **\r** | 回车符（ASCII 13） |
| **\t** | TAB（制表符）字符（ASCII 9） |

## 变量

与人类语言类似，Perl 区分单数和复数数据。字符串和数字是单数；字符串或数字的列表是复数。Perl 提供三种类型的变量：*标量*（单数）、*数组*（复数）和 *哈希*（复数；也称为*关联数组*）。Perl 通过名称前的一个特殊字符来标识每种类型的变量。标量变量名称以美元符号 ($) 开头，数组变量以 at 符号 (@) 开头，哈希变量以百分号 (%) 开头。与 shell 标识变量的方式不同，Perl 要求每次引用变量时（包括给变量赋值时）都必须显示该前导字符：

```bash
$ name="Zach" ; echo "$name"    (bash)
Zach

$ perl -e '$name="Zach" ; print "$name\n";'  (perl)
Zach
```

变量名称是区分大小写的，可以包含字母、数字和下划线字符 (_)。除非前面带有关键字 **my**，否则 Perl 变量是包变量（第 1045 页），如果是这样，则它是一个词法变量（第 1045 页），仅在其所在的块或文件中定义。有关 Perl 变量局部性的讨论，请参见第 1071 页的“子例程”。

### 词法变量遮蔽包变量

> **注意**
> 如果一个词法变量和一个包变量具有相同的名称，则在定义该词法变量的块或文件内，该名称指的是词法变量，而不是包变量。

Perl 变量在您为其赋值时即存在——您不需要定义或初始化变量，尽管这样做可能会使程序更易于理解。通常，当引用未初始化的变量时，Perl 不会报错：

```bash
$ cat variablel.pl
#!/usr/bin/perl
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # 拼写错误，name 中少了 e

$ ./variablel.pl
Hello, , how are you?
```

**use strict**
包含 **use strict** 可以强制 Perl 要求在变量赋值前先声明它们。有关更多信息，请参见 **perldleb** 的 **man** 页。如果在上述程序中包含 **use strict**，Perl 将显示一条错误消息：

```bash
$ cat variablelb.pl
#!/usr/bin/perl
use strict;
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # 拼写错误，name 中少了 e

$ ./variablelb.pl
Global symbol "$nam" requires explicit package name at ./variablelb.pl line 4.
Execution of ./variablelb.pl aborted due to compilation errors.
```

### 使用 my：词法变量与包变量

> **提示**
> 在 **variablel.pl** 中，**$name** 通过在其名称前加上关键字 **my** 而被声明为词法变量；其名称和值仅在文件 **variablel.pl** 内已知。将变量声明为词法变量会将作用域限制在其定义的块或文件内。虽然在此情况下并非必须，但将变量声明为词法是良好的编程习惯。当编写较长的程序、子例程和包时，这种习惯尤其有用，因为此时更难保持变量名称的唯一性。当编写将由他人代码使用的例程时，将所有变量声明为词法是强制性的。这种做法允许使用您例程的人使用任何他们喜欢的变量名称，而不必考虑您在代码中使用的变量名称。
>
> Shell 和 Perl 对变量的作用域处理方式不同。在 shell 中，如果您不 **export** 一个变量，它只是局部于使用该变量的例程（第 992 页）。在 Perl 中，如果您不使用 **my** 将变量声明为词法变量，则它在其所在的包中定义。

**–w** 和 **use warnings**

–w 选项和 use warnings 语句执行相同的功能：它们使 Perl 在检测到语法错误时生成错误消息。在以下示例中，Perl 显示两条警告。第一条告诉您，变量 $name 在第三行只使用了一次，这可能表明存在错误。当您拼错变量名称时，此消息非常有用。在 Perl 5.10 下，第二条警告指定了未初始化变量的名称。这条警告指的是与第一条警告相同的问题。虽然在这个简单的程序中找出哪个变量未定义并不困难，但在复杂程序中这样做可能会花费大量时间。

```bash
$ cat variable1a.pl
#!/usr/bin/perl -w
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # 由于拼写错误和 -w，打印出警告

$ ./variable1a.pl
Name "main::nam" used only once: possible typo at ./variable1a.pl line 3.
Use of uninitialized value $nam in concatenation (.) or string at ./variable1a.pl line 3.
Hello, , how are you?
```

您还可以在命令行上使用 –w。如果同时使用 –e，请确保该选项后面的参数是您想要执行的程序（例如，–e –w 不起作用）。请参见第 1074 页的提示。

```bash
$ perl -w -e 'my $name = "Sam"; print "Hello, $nam, how are you?\n"'
Name "main::nam" used only once: possible typo at -e line 1.
Use of uninitialized value $nam in concatenation (.) or string at -e line 1.
Hello, , how are you?
```

**undef** 和 **defined**

未定义变量具有特殊值 undef，它在数字表达式中评估为零 (0)，在您打印它时扩展为空字符串 (“”)。使用 defined 函数来确定变量是否已定义。以下示例使用了本章稍后解释的构造，调用 defined 并将 $name 作为参数，然后用感叹号 (!) 否定结果。结果是，如果 $name 未定义，则执行 print 语句。

```bash
$ cat variable2.pl
#!/usr/bin/perl
if (!defined($name)) {
    print "The variable '$name' is not defined.\n"
};

$ ./variable2.pl
The variable '$name' is not defined.
```

由于 –w 选项会在引用未定义变量时使 Perl 发出警告，因此使用此选项将生成一条警告。

## 标量变量

标量变量是一个以美元符号 ($) 开头的名称，保存单个字符串或数字：它是一个单数变量。因为 Perl 在这两者之间进行转换
