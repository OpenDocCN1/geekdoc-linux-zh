

## Case 语句

大多数语言提供 case 或 switch 语句，让你将一个字符串与多个可能的值进行比较，并在找到匹配时执行一段代码。Perl 没有提供，但它提供了一种实现此过程的方法。下面是一个 SWITCH 构造的示例，其中语法以粗体显示，而你需要提供的部分以普通字体显示：

```
SWITCH: {
  if ( $A eq "ls" )  { system("ls"); last SWITCH; }
  if ( $A eq "pwd" ) { system("pwd"); last SWITCH; }
  if ( $A eq "date" ) { system("date"); last SWITCH; }
  print "none of the args were very interesting. \n";
}
```

在这个示例中，如果 $A 的值为 ls，则第一个命令块将被执行。如果 $A 的值为 pwd，则第二个命令块将被执行。否则，SWITCH 子句中的其余命令将被执行。最后的 SWITCH 命令告诉 Perl 短路 SWITCH 子句中的其余内容，因此一旦其中一个条件得到满足，其他条件将被忽略。

## 循环

用 Bash 编写的 Shell 脚本可以使用 while、until 和 for 构造来实现循环或迭代。在每种情况下，只要循环退出条件未满足，就会重复执行一段代码。脚本随后从该点继续。

### While 语句

在 while 循环中，{ 和 } 大括号之间的代码块只要条件表达式为真就会被执行。可以把它理解为“只要此条件保持为真，就执行”。下面是一个示例：

```
while ($ARG) {
  print "ARG: $ARGV[0] \n";
  shift $ARGV;
}
```

这个简单的示例打印传递给 Shell 脚本的每个参数的值。翻译成英文，while 条件表示只要输入参数字符串不为空，就继续。 你可能会认为这个循环会永远不断地打印第一个参数 $ARGV[0]，因为你不期望 @ARGV 变量的值（命令行参数列表）在脚本运行过程中会发生变化。你是对的，除了我在循环体中加入了 shift 命令。

shift 所做的是丢弃第一个参数并重新分配所有 $ARG 变量——因此新的 $ARGV[0] 得到以前在 $ARGV[1] 中的值，以此类推。因此，@ARGV 中的值每次循环都会变得越来越短，直到最终变为 null，循环结束。

### UNTIL 语句

until 构造的工作方式几乎与 while 完全相同。唯一的区别是 until 只要条件表达式为假就执行循环体，而 while 只要条件表达式为真就执行循环体。可以把它理解为“执行直到此条件变为真”。

让我们用 until 循环来编写之前的示例，并通过添加一个计数器变量使其更精致一些：

```
$count=1;
until ( ! @ARGV ) {
    print "Argument number $count : $ARGV[0] \n";
    shift;
    $count++;
}
```

这里唯一的新概念是递增计数器的看起来很奇怪的那一行。 $count++ 语法等价于 $count=$count+1，但在 Perl 和 C 语言编程中前者更常见。你也可以使用 $count-- 语法来递减一个值。

### FOREACH 语句

foreach 语句提供了在 Perl 脚本中实现循环的另一种方法。for 构造的一般形式如下所示：

```
foreach $item ( in-some-array )
{
    do something with $item
}
```

每次循环，$item 变量的值都会被赋值为数组中的下一个项目。当你处理完数组中的所有项目时，循环结束。下面是一个与本章前面看到的 until 和 while 循环类似的示例：

```
foreach $var (@ARGV)
{
print "NEXT ARG: $var \n";
}
```

## 处理文件

Perl 中的一个常见操作是打开一个文本文件并逐行处理。你可能正在创建报告或只是筛选文件以查找某些字符串。此示例打开一个文件，其名称存储在 $file 变量中，然后打印以井号开头的每一行：

```
open MYFILE, $file or die "Can't open $file: $! \n";
while (<MYFILE>) {
if (/^#/) { print "MATCH: $_;" }
}
```

这里可能需要解释一些事情。open 命令将文件句柄（在本例中为 MYFILE）分配给 $file 变量中指定的文件。你可以在 open 命令中使用任何文件句柄或变量名。如果由于某种原因无法打开文件（它不存在、不可读等），则程序将终止（得益于 die 命令），并显示如下消息：

```
Can't open panda.txt: No such file or directory
```

特殊变量 $! 包含失败的原因，并被替换到错误消息中。如果文件成功打开，程序将继续，并且 <MYFILE> 构造将把文件的下一行返回到 $_ 变量中。（你会发现很多 Perl 函数都使用这个特殊的 $_ 变量。）当到达文件末尾时，<MYFILE> 将返回一个 null 值，导致循环终止。

