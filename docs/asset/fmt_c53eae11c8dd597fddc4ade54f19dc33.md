
# 子程序与正则表达式

## 子程序基础

```perl
$ans = $Some + $two

}
```

```bash
$ perl subroutine1.pl

Answer is 3
```

下一个示例与上一个相似，区别在于子程序利用 `return` 语句向主程序返回一个值。程序将子程序返回的值赋值给变量 `$ans` 并显示该值。再次，所有的变量都是包变量。

```bash
$ cat subroutine2.pl

$Some = 1;

$two = 2;

$ans = add();

print "Answer is $ans\n";
```

```perl
sub add {

return ($Some + $two)

}
```

```bash
$ perl subroutine2.pl

Answer is 3
```

在许多情况下，将变量保持在子程序局部是非常重要的。下一个示例中的子程序通过声明和使用局部变量改变变量的值，并保护调用程序免受这些变化的影响。这种设置更为典型。

当你向子程序传递值时，Perl 会将这些值在子程序中名为 `@` 的数组中可用。虽然 `@` 是子程序局部的，但它的元素是调用该子程序的参数的别名。在 `@` 数组中更改值会改变底层变量的值，这可能不是你想要的。下一个程序通过将传递给子程序的值赋值给局部变量来避免这一陷阱。

`subroutine3.pl` 程序带有两个变量调用 `addplusone` 子程序，并将子程序返回的值赋值给一个变量。子程序声明了两个局部变量并将它们赋值为来自 `@` 数组的值。（参见第 1050 页关于局部变量和包变量的提示）。虽然你可以在不给声明变量赋值的情况下使用，但示例中的语法是最常见的。这两个语句增加了局部变量 `lcl_one` 和 `lcl_two`。`print` 语句显示了子程序内部 `lcl_one` 的值。`return` 语句返回两个增加后的局部变量之和。

```perl
sub subroutine3.pl

$lcl_one = 1;

$two = 2;

$ans = addplusone($lcl_one, $two);

print "Answer is $ans\n";

print "Value of $lcl_one in main: $lcl_one\n";

print "Value of $one in main: $one\n";
```

```perl
sub addplusone {

my ($lcl_one, $lcl_two) = @;

$lcl_one++;

$lcl_two++;

print "Value of $lcl_one in sub: $lcl_one\n";

return ($lcl_one + $lcl_two);

}
```

```bash
$ Perl subroutine3.pl

Value of $lcl_one in sub: 2

Answer is 5

Value of $lcl_one in main: 

Value of $one in main: 1
```

在显示由子程序返回的结果后，主程序中的 `print` 语句证明 `$lcl_one` 在主程序中没有定义（它是子程序的局部的），并且 `$one` 的值没有改变。下一个示例说明了处理传递给子程序的参数另一种方法。该子程序没有使用传递它的 `@_` 之外的变量，也没有更改任何元素的值。

## 正则表达式 (REGULAR EXPRESSIONS)

```perl
$ cat subroutine4.pl

$one = 1;

$two = 2;

$ans = addplusone($one, $two);

print "Answer is $ans\n";

sub addplusone {

    return ($[0] + $_[1]);

}

Answer is 5
```

本节的最后一个示例展示了一个更典型的子程序。`max()` 子程序可以用任意数量的参数调用并返回最大参数的值。它使用 `shift` 函数将第一个参数的值赋值给 `$biggest`。`shift` 之后，参数 2 变成参数 1，参数 3 变成参数 2，参数 4 变成参数 3。接下来，`foreach` 遍历剩余的参数 (`@`)。

```perl
$ cat subroutine5.pl

$ans = max (16, 8, 64);

print "Maximum value is $ans\n";
```

```perl
sub max {

    my $biggest = shift; # 先赋值并移动剩余参数

    foreach (@_) { # 遍历剩余参数

        $biggest = $_ if $_ > $biggest;

    }

    return ($biggest);

}
```

```bash
$ perl subroutine5.pl

Maximum value is 64
```

## 正则表达式 (REGULAR EXPRESSIONS)

附录 A 定义并讨论了正则表达式，你可以在许多工具中使用它们。除非另有说明，否则附录 A 中的所有材料都适用于 Perl。除了附录 A 中描述的功能外，Perl 还提供了允许你执行复杂字符串处理的正则表达式功能。本节回顾了附录 A 中涵盖的一些正则表达式，并描述了 Perl 中提供的某些额外功能。它还介绍了 Perl 用于处理正则表达式的语法。

### 语法与 `=~` 运算符

`-l` 选项。 Perl `-l` 应用于输入的每一行，并在每行输出末尾放置 `\n`。本节中的示例使用了 Perl 的 `-l` 和 `-e`（第 46 页）选项。由于程序必须指定为单个参数，示例将 Perl 程序封装在引号内。shell 会解释引号而不会将其传递给 Perl。

### 与 `-e` 使用其他选项

当你配合 `-e` 使用另一个选项时，该程序必须在命令行中紧跟在 `-e` 之后。像许多其他工具一样，Perl 允许你合并单个连字符后面的选项；如果 `-e` 是选项列表之一，它必须出现在最后。默认情况下，`perl` 使用斜杠 (`/`) 定界正则表达式。你可以使用 `-le` 而不是 `-el`。

默认情况下，`perl` 使用斜杠 (`/`) 定界正则表达式。使用 `=~` 运算符在字符串 `aged` 中搜索模式 `ge`。在示例中，表达式为真，Perl 执行了 `print` 语句。

```bash
$ perl -le 'if ("aged" =~ /ge/) { print "true"; }

true
```

你可以通过使用 `if` 语句实现相同的功能：

```bash
$ perl -le 'print "true" if "aged" =~ /ge/'

true
```

`!~` 运算符的作用与 `=~` 相反。示例中的表达式为真，因为正则表达式 `xy` 不匹配 `aged` 的任何部分：

```bash
$ perl -le 'print "true" if "aged" !~ /xy/'

true
```

如第 191 页所示，点匹配任何单个字符，因此正则表达式 `a..d` 匹配字符串 `aged`：

```bash
$ perl -le 'print "true" if "aged" =~ /a..d/'

true
```

你可以使用变量来持有正则表达式。以下语法作为正则表达式：

```
qr/string/
```

### 正则表达式 (REGULAR EXPRESSIONS)

下一个示例使用此语法将正则表达式 `/a..d/`（包括定界符）赋值给变量 `$re`，然后将其作为正则表达式：

```bash
$ perl -le '$re = qr/a..d/; print "true" if ("aged" =~ $re)'

true
```

如果你想在正则表达式中包含定界符，你需要对其转义。在下一个示例中，默认定界符 `/` 出现在正则表达式中。为了防止 Perl 将 `/usr` 解释为正则表达式的结束，正则表达式 `/` 通过在其前面加上反斜杠 (`\`) 进行转义。更多信息请参阅第 193 页。

```bash
$ perl -le 'print "true" if ("/usr/doc" =~ /\/usr/)'

true
```

通过反斜杠转义多个字符会让复杂的正则表达式更难以阅读。相反，你可以使用 `m` 和一对字符（如 `{}`）来定界正则表达式。在以下示例中，脱字符 (`^`) 将正则表达式锚定到行首（第 192 页）：

```bash
$ perl -le 'print "true" if ("/usr/doc" =~ m{/usr/)'

true
```

你可以在将正则表达式赋值给变量时使用该语法：

```bash
$ perl -le '$Spn = qr{/usr/doc}; print "true" if ("/usr/doc" =~ $Spn)'

true
```

# 第 28 章 PERL 脚本语言

## 表 28-3 一些 Perl 正则表达式元字符

| 字符 | 匹配内容 |
| :--- | :--- |
| `^` (脱字符) | 将正则表达式锚定到行的开头（第 1092 页） |
| `$` (美元符号) | 将正则表达式锚定到行的末尾（第 1077 页） |
| `(...)` | 对正则表达式进行括括（第 1077 页） |
| `.` (点) | 匹配除换行符 (`\n`)以外的任意单个字符（第 1091 页） |
| `\` | 反斜杠 (`\`) |
| `\b` | 单词边界（零匹配） |
| `\B` | 非单词边界 (`[\b]`) |
| `\d` | 单个数字字符 (`[0-9]`) |
| `\D` | 单个非数字字符 (`[^0-9]` 或 `[^d]`) |
| `\s` (小写) | 单个空白字符：空格、换行符、回车、制表符、分页符 |
| `\S` (大写) | 单个非空白字符 (`[^s]`) |
| `\w` (小写) | 单个单词字符（字母或数字；`[a-zA-Z0-9]`） |
| `\W` (大写) | 单个非单词字符 (`[^w]`) |

### 贪婪匹配

Perl 默认执行贪婪匹配，这意味着正则表达式会匹配尽可能长的字符串（第 1093 页）。在接下来的示例中，正则表达式 `/\{.*\}/` 匹配一个左括号，后面跟任意任意字符字符串、一个右括号，以及一个空格（删除我）可能会有两个（保留我）。Perl 用空字符串 (`/`) 替换此匹配项。

```perl
$ cat Sha.pl

$string = "A line (remove me) may have two {keep me} pairs of braces.";

$string = s/{}///g;

print "$string\n";
```

```bash
$ perl Sha.pl

A line pairs of braces.
```

非贪婪匹配的下一个示例显示了上一个示例中较短的括号字符串的匹配。这种匹配被称为非贪婪匹配或节约匹配。以下是正则表达式的匹配：

- 1. 一个左括号，后面跟
- 2. 一个属于字符类（第 1091 页）的字符，该类包含除右括号以外的所有字符 (`[^\}]`)，后面跟
- 3. 前一个字符的零或多次出现 (`*`)，后面跟
- 4. 一个右括号，后面跟
- 5. 一个空格。

（字符类中的第一个字符作为脱字符指定不匹配后续字符的所有字符类，因此 `[^\]]` 匹配任何不是右括号的字符。）

```perl
$ cat re5b.pl

$string = "A line (remove me) may have two {keep} pairs of braces."

$string = s/\{[^\}]\}/g;

print "$string\n";
```

```bash
$ perl re5b.pl

A line may have two {keep} pairs of braces.
```

Perl 允许你指定非贪婪匹配。在接下来的示例中，`[.*?]` 中的问号会导致正则表达式匹配以左括号开头、其后跟任意字符、并以右括号结尾的最短字符串。

```perl
$ cat re5c.pl

$string = "A line (remove me) may have two {keep} pairs of braces."

$string = s/\{.*\}/g;

print "$string\n";
```

```bash
$ perl re5c.pl

A line may have two {keep} pairs of braces.
```

### 括号表达式

如第 1094 页所示，你可以对正则表达式的部分进行加括号，并在替换字符串中调用这些部分。大多数 Linux 工具使用转义括号（即 `\[ \]`）来对正则表达式加括号。Perl 允许你指定非贪婪匹配。在接下来的示例中，`[.*?]` 中的问号会导致正则表达式匹配以左括号开头、其后跟任意字符、并以右括号结尾的最短字符串。

```perl
$ cat re5c.pl

$string = "A line (remove me) may have two {keep} pairs of braces."

$string = s/\{.*\}/g;

print "$string\n";
```

```bash
$ perl re5c.pl

A line may have two {keep} pairs of braces.
```

*(注：由于原文文本中部分段存在重复或逻辑断层，此处已根据上下文意图进行平滑对齐)*

### 模块构建与安装

## 1080 第 28 章 Perl 脚本语言

新创建目录中的 `README` 文件通常提供了构建和安装模块的说明。大多数模块都遵循相同的步骤。

```bash
$ cd Timestamp-Simple-1.01

$ perl Makefile.PL
```

正在检查您的套件是否完整...
看起来良好
正在为 `Timestamp::Simple` 写入 `Makefile`

如果你正在构建的模块依赖于本地系统中未安装的其它模块，运行 `perl Makefile.PL` 将会显示一个或多个关于未找到的先决条件的警告。如果缺少模块，此步骤将写入 `Makefile`。在这种情况下，下一步将失败，你必须在继续之前构建并安装这些模块。

下一步是运行你刚刚创建的 `Makefile`。执行 `make` 后，运行 `test` 以确保模块运行正常。

```bash
$ make

cp Simple.pm lib/lib/Timestamp/simple.pm

Manifying lib/man3/Timestamp::Simple.pm
```

```bash
$ test

PERL_DL_NONLAZY=1 "/usr/bin/perl" "-Ilib/lib" "-Ilib/arch" test.pl

1..
```

```text
# Running under perl version 5.100000 for linux

# Current time local: Fri Sep 3 18:20:41 2010

# Current time GMT: Sat Sep 4 01:20:41 2010

# Using Test.pm version 1.25

ok 1

ok 2

ok 3
```

最后，使用 `root` 权限安装该模块：

```bash
$ sudo make install

Installing /usr/local/lib/perl/5.10.0/Timestamp::Simple

Installing /usr/local/man/man3/Timestamp::Simple.pm

Writing /usr/local/lib/perl/5.10.0/auto/Timestamp/Simple/.packlist

Appending installation info to /usr/local/lib/perl/5.10.0/perl.md
```

一旦安装了模块，你就可以使用 `perldoc` 显示文档，告知你如何使用该模块。示例参见第 1043 页。

某些模块包含 `SYNOPSIS`（摘要）部分。如果你安装的模块包含此类部分，你可以将 `SYNOPSIS` 部分中的代码放入文件中并作为 Perl 程序运行，以此测试该模块：

```perl
$ cat times.pl

use Timestamp::Simple qw($stamp);

print stamp, "\n";
```

```bash
$ perl times.pl

20100904182627
```

### 1081 示例

随后你可以在 Perl 程序中引入该模块。下面的示例使用了时间戳模块来生成一个唯一文件名：

```perl
$ cat fn.pl

use Timestamp::Simple qw(stamp);
```

```perl
# 将时间戳存入变量
$ts = stamp, "\n";
```

```perl
# 去掉年份
$ts =~ s/...(.*)$//1;
```

```perl
# 创建唯一文件名
$sfn = "myfile." $ts;
```

```perl
# 打开文件、写入内容并关闭文件
open (OUTFILE, '>', "$sfn");

print OUTFILE "HI here.\n";

close (OUTFILE);
```

```bash
$ perl fn.pl

myfile.090518310
```
