
程序的第一行告诉操作系统使用 Perl 来解释文件。正如你在第 7 章“高级 Shell 编程”中学学的，当程序的开头是 `#!` 时，剩余部分假设为解释器的路径。

示例程序的第二行是注释，说明了文件名。像 Shell 脚本一样，Perl 程序使用 `#` 字符标记注释的开始。注意注释中提到的程序名包含了 `.pl` 扩展名，该扩展名通常表示文件是 Perl 脚本。

程序的第三和第四行在屏幕上显示文本。在这些行中，`print` 语句将指定的字符串输出到标准输出。字符串被双引号包含。字符串末尾包含的 `\n` 表示执行换行，以便屏幕上显示的后续信息位于下一行。程序的输出如图 9-1 所示。

> 如果你需要重现此脚本或下一组示例中的其他脚本，请确保在运行之前已赋予文件可执行权限。

图 9-1 `example.pl` 的输出

# Perl 459简介

![](img/0a988e998d76ede7c21a57edbc89e490_479_0.png)

**图 9-1** 运行 `example1.pl` 脚本

在这个简单的脚本中，每个 `print` 语句都只有一个参数，并显示在屏幕上。第一个 `print` 语句显示字符串“This is a simple”，`\n` 字符将光标移动到下一行的开头。第二个 `print` 语句与第一个相似。它显示“Perl program.”然后将光标移动到下一行的开头。注意这两个 `print` 语句都以分号结尾。在 Perl 中，所有完整的的语句都以分号结束。

> 包围在 `print` 语句参数的括号是可选的。例如，这两个语句执行了相同的操作：
```perl
print ("Hello");
print "Hello";
```

看第二个 Perl 脚本，它使用了变量：
```perl
#!/usr/bin/perl
# Program name: example2.pl
$name = "Charlie";
print ("Greetings $name\n");
```

`example2.pl` 脚本使用了变量 `$name`。该变量初始化为字符串“Charlie”。注意，当 `$name` 被插入到 `print` 语句的参数中时，它会显示变量的内容，输出如下：
```bash
[ellen@localhost ~]$ ./example2.pl
Greetings Charlie
```

Perl 还可以从键盘读取输入。下一个程序是一个示例。

# 第 9 章 Perl 和 CGI 编程

```perl
#!/usr/bin/perl
# Program name: example3.pl
print("Enter a number: ");
$number = <STDIN>;
print("You output $number\n");
```
程序的输出如图 9-2 所示。

![](img/0a988e998d76ede7c21a57edbc89e490_480_0.png)

图 9-2 运行 `example3.pl` 脚本

在 Perl 中，`<STDIN>` 从键盘读取输入（记住 `stdin` 是标准输入设备）。程序使用这一行将键盘输入赋值给变量 `$number`：

`$number = <STDIN>`

像其他语言一样，Perl 提供了 `if-else` 语句作为决策结构。这是一个示例：
```perl
#!/usr/bin/perl
# Program name: example4.pl
print("Enter a number: ");
$number = <STDIN>
if ($number == 10)
{
    print("That is the number I was thinking of.\n");
} else
{
    print("You entered $number\n");
}
```

# Perl 461简介

`==` 运算符测试两个数值是否相等。`if` 语句使用 `==` 运算符来判断 `$number` 是否等于 10。如果是，则执行紧跟在 `if` 语句之后的块（由包含在在大括号内的代码行组成）。否则，执行 `else` 语句之后的块。当你运行 `example4.pl` 脚本并输入 10 时，你看到的输出是“That is the number I was thinking of.”。当你输入任何其他数字时，你在图 9-3 中看到输出“You entered”后面跟着你输入的数字。

![](img/0a988e998d76ede7c21a57edbc89e490_481_0.png)

**图 9-3** 运行 `example4.pl` 脚本

Perl 还有测试小于、小于等于、大于或大于等于关系的运算符。表 9-1 显示了 Perl 的数值关系运算符，表 9-2 列出了它的字符串关系运算符。

**表 9-1** Perl 的数值关系运算符

| 运算符 | 含义 |
| --- | --- |
| == | 等于 |
| < | 小于 |
| > | 大于 |
| <= | 小于等于 |
| >= | 大于等于 |
| != | 不等于 |

**表 9-2** Perl 的字符串关系运算符

| 运算符 | 含义 |
| --- | --- |
| eq | 等于 |
| lt | 小于 |
| gt | 大于 |

# 第 9 章 Perl 和 CGI 编程

表 9-2 Perl 的字符串关系运算符（续）
| 运算符 | 含义 |
|---|---|
| le | 小于等于 |
| ge | 大于等于 |
| ne | 不等于 |

注意，数值关系运算符是符号化的，例如用于小于等于的 `<=`，这在数值公式中常用。字符串关系运算符是基于字符的，例如用于小于等于的 `le`。下一个程序演示了存储在两个变量——`$my_name` 和 `$your_name` 中的两个字符串如何使用 `eq` 字符串关系运算符进行相等比较。
```perl
#!/usr/bin/perl
# Program name: example5.pl
$my_name = "Ellen"
$your_name = "Charlie"
if ($my_name eq $your_name) {
    print("Your name is the same as $my_name.\n");
} else {
    print("Hello. My name is $my_name\n");
}
```

`example5.pl` 的输出是：
```bash
[ellen@localhost ~]$ ./example5.pl
Hello. My name is Ellen
```

`example2.pl` 脚本使用了变量 `$name`。该变量初始化为字符串“Charlie”。注意，当 `$name` 被插入到 `print` 语句的参数中时，它会显示变量的内容，输出如下：
```bash
[ellen@localhost ~]$ ./example2.pl
Greetings Charlie
```

Perl 还可以从键盘读取输入。下一个程序是一个示例。
```perl
#!/usr/bin/perl
# Program name: example3.pl
print("Enter a number: ");
$number = <STDIN>;
print("You output $number\n");
```
程序的输出如图 9-2 所示。

在 Perl 中，`<STDIN>` 从键盘读取输入（记住 `stdin` 是标准输入设备）。程序使用这一行将键盘输入赋值给变量 `$number`：

`$number = <STDIN>`

像其他语言一样，Perl 提供了 `if-else` 语句作为决策结构。这是一个示例：
```perl
#!/usr/bin/perl
# Program name: example4.pl
print("Enter a number: ");
$number = <STDIN>
if ($number == 10)
{
    print("That is the number I was thinking of.\n");
} else
{
    print("You entered $number\n");
}
```
