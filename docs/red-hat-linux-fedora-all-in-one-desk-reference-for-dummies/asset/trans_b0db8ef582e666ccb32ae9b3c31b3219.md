
(=~) 和 (!~) 操作符用于测试字符串。你可以编写一个 Perl 脚本，其执行与本节前面使用 grep 完成的相同搜索。按照以下步骤完成此任务：

1. 使用文本编辑器输入并保存以下脚本到名为 lookup 的文件中：

```
#!/usr/bin/perl

while (<STDIN>)
{
    if ( $_ =~ /[bB]laster/ ) { print $_; }
}
```

2. 使用以下命令使 lookup 文件可执行：

```
chmod +x lookup
```

3. 使用以下命令尝试该脚本：

```
cat /usr/src/linux*/drivers/cdrom/sbpcd.c | ./lookup
```

在此情况下，cat 命令将特定文件的内容（正如你从 grep 示例中知道的，该文件包含一些带有正则表达式的行）馈送给 lookup 脚本。脚本 simply 应用 Perl 的正则表达式匹配操作符 (=~) 并打印任何匹配的行。输出应与使用以下命令显示的 grep 命令类似：

```
grep "[bB]laster" /usr/src/linux*/drivers/cdrom/sbpcd.c
```

lookup 脚本中的 $_ 变量需要一些解释。 <STDIN> 表达式从标准输入获取一行，默认情况下将该行存储在 $_ 变量中。在 while 循环内部，正则表达式与 $_ 字符串进行匹配。以下单个 Perl 语句完成了 lookup 脚本的工作：

```
if ( $_ =~ /[bB]laster/ ) { print $_; }
```

```
while (<STDIN>)
{
    if ( $_ =~ /\\n/ && $_ =~ /^ {7}\S/ ) { print $_; }
}
```

## 流程控制语句

到目前为止，你看到的 Perl 语句旨在按串行方式执行，一个接一个。Perl 还包括能够控制语句执行流程的语句。你已经看到过 if 语句和 while 循环。Perl 包含一套完整的流程控制语句，就像 C 中的一样，但有一些额外的特性。

在 Perl 中，所有条件语句采用以下形式：

```
conditional-statement
{ Perl code to execute if conditional is true }
```

请注意，你必须用大括号 ({...}) 括起条件语句后面的代码。条件语句检查表达式的值以确定是否执行大括号内的代码。在 Perl 中，与 C 相同，任何非零值都被视为逻辑真，而零值则为假。

接下来我简要描述 Perl 中主要条件语句的语法。

### if 和 unless

Perl 的 if 语句类似于 C 的 if 语句。例如，if 语句可以检查计数是否超过阈值，如下所示：

```
if ( $count > 25 ) { print "Too many errors!\n"; }
```

你可以向 if 语句添加 else 子句，如下所示：

```
if ($user eq "root")
{
    print "Starting simulation...\n";
}
else
{
    print "Sorry $user, you must be \"root\" to run this program.\n";
    exit;
}
```

如果你熟悉 C，你可以看到 Perl 的语法与 C 非常相似。if 语句的条件可以有零个或多个 elsif 子句以处理更多备选情况，如下所示：

```
print "Enter version number:"; # prompt user for version number

$os_version = <STDIN>;   # read from standard input
chop $os_version; # get rid of the newline at the end of the line
# Check version number
if ($os_version > 10 ) { print "No upgrade necessary\n";}
elsif ($os_version > 6 && $os_version < 9)
{ print "Standard upgrade\n";}
elsif ($os_version > 3 && $os_version < 6 ) { print "Reinstall\n";}
else { print "Sorry, cannot upgrade\n";}
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_822_0.png)

unless 语句是 Perl 独有的。该语句的形式与 if 相同，包括使用 elsif 和 else 子句。不同之处在于 unless 仅在条件为假时执行其语句块。例如，你可以在以下代码中使用 unless：

```
unless ($user eq "root")
{
    print "You must be \"root\" to run this program.\n";
    exit;
}
```

在这种情况下，除非字符串 user 是 "root"，否则脚本会退出。

### while

使用 Perl 的 while 语句进行循环——在现有条件变为逻辑假之前重复某些处理。要逐行从标准输入读取并处理该行，可以使用以下 while 循环：

```
while ($in = <STDIN>)
{
# Code to process the line
    print $in;
}
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_822_1.png)

如果你在不带任何参数的情况下从标准输入读取，Perl 会将标准输入的当前行分配给 $_ 变量。因此，你可以按如下方式编写前面的 while 循环：

```
while (<STDIN>)
{
# Code to process the line
    print $_;
}
```

Perl 的 while 语句比 C 的更灵活，因为你可以用几乎任何东西作为要测试的条件。例如，如果你使用数组作为条件，while 循环会一直执行直到数组没有元素剩余，如以下示例所示：

```
# Assume @cmd_arg has the current set of command arguments
while (@cmd_arg)
{
$arg = shift @cmd_arg; # this extracts one argument
# Code to process the current argument
print $arg;
}
```

shift 函数移除数组的第一个元素并返回该元素。

你可以使用 next 关键字跳到循环的末尾；last 关键字退出循环。例如，以下 while 循环将 1 到 10 的数字相加，跳过 5：

```
while (1)
{
$i++;
if($i == 5) { next; } # Jump to the next iteration if $i is 5
if($i > 10) { last; } # When $i exceeds 10, end the loop
$sum += $i; # Add the numbers
}
# At this point $sum should be 50
```

### for 和 foreach

Perl 和 C 的 for 语句语法相似。使用 for 语句根据表达式的值执行语句任意次数。语法如下：

```
for (expr_1; expr_2; expr_3) { statement block }
```

expr_1 在循环开始时只评估一次；语句块执行直到表达式 expr_2 评估为零。第三个表达式 expr_3 在每次执行语句块后评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必需的。以下是使用 for 循环将 1 到 10 的数字相加的示例：

```
for($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在此示例中，实际的加法工作在第三个表达式中完成，而 for 循环控制的语句是一个空块 ({})。

foreach 语句最适合用于数组。以下是语法：

```
foreach Variable (Array) { statement block }
```

foreach 语句将 Array 中的一个元素分配给 Variable 并执行语句块。foreach 语句重复此过程直到没有数组元素剩余。以下 foreach 语句将 1 到 10 的数字相加：

```
foreach $i (1..10) { $sum += $i; }
```

请注意，我使用范围运算符 (..) 声明数组。你也可以使用逗号分隔的项目列表作为数组。

如果你在 foreach 语句中省略 Variable，Perl 会隐式使用 $_ 变量来保存当前数组元素。因此，你可以使用以下内容：

```
foreach (1..10) { $sum += $_; }
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_824_0.png)

### goto

goto 语句导致 Perl 跳转到由标签标识的语句。以下是提示用户输入值并在值不可接受时重复请求的示例：

```
ReEnter:
print "Enter offset: ";
$offset = <STDIN>;
chop $offset;
unless ($offset > 0 && $offset < 512)
{
    print "Bad offset: $offset\n";
    goto ReEnter;
}
```

### 访问 Linux 命令

你可以通过以下几种方式从 Perl 执行任何 Linux 命令：

- 使用包含要执行的 Linux 命令的字符串调用 system 函数。
- 将 Linux 命令用反引号 (`) 括起来，反引号也称为重音符。你可以通过这种方式运行 Linux 命令并捕获其输出。
- 调用 fork 函数复制当前脚本并在子进程中处理新命令。（如果一个进程启动另一个进程，则新进程称为子进程。）

