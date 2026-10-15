
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
$ ./if2.pl
Enter 28: 28.0
Thank you for entering 28.
End.
```

## 表 28-2 比较运算符

| 数值运算符 | 字符串运算符 | 根据运算符前后值之间的关系返回的值 |
|---|---|---|
| == | eq | 相等则为真 |
| != | ne | 不相等则为真 |
| < | lt | 小于则为真 |
| > | gt | 大于则则为真 |
| <= | le | 小于等于则为真 |
| >= | ge | 大于等于则为真 |
| <> | cmp | 相等返回 0，大于返回 1，小于返回 -1 |

下一个程序与上一个相似，但它测试两个字符串之间的相等性。`chomp`函数（第 1067 页）删除用户输入尾部的换行符——否则此比较将永远不会匹配。`eq`比较运算符比较字符串。在本示例中，当用户输入字符串 *five* 时，字符串比较的结果为 *true*。前导或尾随空格将产生 *false* 结果，字符串 **, 也是如此，尽管这些条目中的都不会生成警告，因为它们是合法的字符串。

```
$ cat if2a.pl
```

```
!/usr/bin/perl -w

print "Enter the word 'five': ";

$entry = <>;

chomp($entry);

 ($entry eq "five") { # 使用 eq 进行字符串比较

    print "Thank you for entering 'five'.";

}

print "End.\n";
```

```
$ ./if2a.pl

Enter the word 'five': five

Thank you for entering 'five'.

End.
```

## if...else

`if...else`控制结构是一个复合语句，类似于 bash 的 `if...then...else`控制结构（第 958 页）。它使用以下语法实现二路分支：

```
if (expr) else {... }
```

下一个程序提示用户输入两个不同的数字并将这些数字存储在 `$num1` 和 `$num2` 中。如果用户两次输入相同的数字，`if`结构将执行 `die`函数，该函数将其参数发送到标准错误并终止程序执行。

如果用户输入不同的数字，`if...else`结构会报告哪个数字较大。由于 `expr`执行数值比较，程序接受包含小数点的数字。

```
$ cat ifelse.pl
```

```
!/usr/bin/perl -w

print "Enter a number: ";

$num1 = <>;

print "Enter another, different number: ";

$num2 = <>;

if ($num1 == $num2) {

    die "Please enter two different numbers.\n"

}

if ($num1 > $num2) {

    print "The first number is greater than the second number.\n"

}

else {

    print "The first number is less than the second number.\n"

}
```

```
$ ./ifelse.pl
Enter a number: 8
Enter another, different number: 8
Please enter two different numbers.
```

```
$ ./ifelse.pl
Enter a number: 5.5
Enter another, different number: 5
The first number is greater than the second number.
```

## if...elsif...else

类似于 bash 的 `...then...elif`控制结构（第 961 页），Perl 的 `if...elsif...else`控制结构是一个实现二路分支的复合语句。下一个程序与上一个相似，但它测试两个字符串之间的相等性。`chomp`函数（第 1067 页）删除用户输入尾部的换行符——否则此比较将永远不会匹配。`eq`比较运算符比较字符串。在本示例中，当用户输入字符串 *five* 时，字符串比较的结果为 *true*。前导或尾随空格将产生 *false* 结果，字符串 **, 也是如此，尽管这些条目中的都不会生成警告，因为它们是合法的字符串。

```perl
$ cat foreach1.pl
foreach $item ("one", "two", "three") {
  if ($item eq "two") {
    next;
  }
  say "$item";
}
```

```perl
$ perl foreach1.pl
one
three
```

### foreach: 语法 2

`foreach`结构的第二种语法与 C 语言结构相似：[...]

```perl
foreach|for (expr1, expr2, expr3) [...] [...]
```

`expr1`用于初始化 `foreach`循环；Perl 在执行语句块之前会对 `expr1`进行一次评估。`expr2`是终止条件；Perl 在每次执行语句块之前都会评估 `expr2`，如果 `expr2`结果为真，则执行语句块。Perl 在每次执行完语句块后评估 `expr3`——通常是为 `expr2`中的某个变量递增。

在下一个示例中，`foreach2.pl`程序提示输入三个数字：显示第一个数字；通过第二个数字不断递增该数字，显示每个结果，直到结果大于第三个数字；然后退出。有关魔法文件句柄 (`<>`) 的讨论请参见第 1066 页。

```perl
$ cat ./foreach2.pl
!/usr/bin/perl -w

print "Enter starting number: ";
$start = <>;

print "Enter ending number: ";
$end = <>;

print "Enter increment: ";
$incr = <>;

if ($start > $end || $incr < 1) {
  die("起始数字必须小于结束数字\n"
  且递增量必须大于零。\n");
}

foreach ($count = $start+0; $count <= $end; $count += $incr) {
  say "$count";
}
```

### while/until

```perl
$ ./foreach2.pl
Enter starting number: 2
Enter ending number: 10
Enter increment: 3
2
5
8
```

在提示输入三个数字后，前面的程序测试起始数字是否大于或等于结束数字，或者递增量是否小于 1。`||`是逻辑或运算符；如果 `if`后面括号中的表达式在在该运算符之前或之后的表达式评估为真，则该表达式为真。

`foreach`语句首先将 `$start+0`的值赋值给 `$count`。在字符串 `$start`上加上 0（零）会强制 Perl 在数值上下文中工作，并移除赋值时产生的末尾换行符。如果没有这个修复，程序将在输出的第一个数字后额外显示一个换行符。

`while`（第 970 页）和 `until`（第 974 页）控制结构是复合语句，使用以下语法实现条件循环：

- `while (expr) {...}`
- `until (expr) {...}`

这些结构的区别仅在于其终止条件的含义。`while`在 `expr`评估为真时重复执行语句块；`until`直到 `expr`评估为真为止（即 `while expr`保持为假）。

下面的示例演示了在没有输入时读取和处理输入的技术。虽然这个示例显示输入来自用户（标准输入），但该技术对于来自文件的输入同样有效（参见第 1068 页的示例）。用户单独单独一行输入 CTRL-D 来信号文件结束。

在此示例中，`expr`是 `$line = <>`。该语句使用魔法句柄（第 1066 页）从标准输入读取一行，并将字符串赋值给变量 `$line`。只要读取到数据，该语句就评估为真。当到达文件末尾时，该语句评估为假。只要有数据可读，`while`就会继续执行语句块（在本示例中只有一条语句）。

```perl
$ cat while1.pl
!usr/bin/perl -w
$count = 0;
while ($line = <>) {
    print ++$count, " $line";
}
print "\n输入了 $count 行。\n";
```

控制结构

```perl
$ ./while1.pl
Good Morning.
1. Good Morning.
Today is Monday.
2. Today is Monday.
CONTROL-D
```

输入了 2 行。

在前面的示例中，`$count`跟踪用户输入的行数。在变量之前使用 `++`递增运算符 (`++$count`)——称为自增运算符——会在 Perl 评估该变量之前对其增加。或者，你可以将 `$count`初始化为 1 并使用 `$count++`（后增）对其进行递增；但在最后的打印语句中，`$count`将比输入的行数多一。

`$_`变量跟踪程序读取的输入行数。使用 `$_`，你可以将之前的示例重写如下：

```perl
$ cat while1.pl
#!/usr/bin/perl -w
while ($line = <>) {
    print "$line";
}
print "\n输入了 $count 行。\n";
```

通过使用 `$_`变量，你可以利用 `$_`简化 Perl 代码。你可以在 Perl 程序的许多地方使用 `$_`——将 `$_`想象为“它”，即你正在执行的操作的对象。它是许多操作的默认操作数。例如，下节代码段使用 `$line`变量处理一行。它将一行读取到 `$line`，使用 `chop`（第 1067 页）移除 `$line`末尾的任何换行符，并检查正则表达式是否匹配 `$line`。

```perl
while (my $line = <>) {
    chomp $line;
    if ($line ~ /regex/) ...
}
```

你可以使用 `$_`替换 `$line`来重写这段代码：

```perl
while (my $_ = <>) {
    chomp $_;
    if ($_ ~ /regex/) ...
}
```

由于 `$_`是这些实例中的默认操作数，你也可以完全省略 `$_`：

```perl
while (<>) {
    chomp;
    if (/regex/) ...
}
# 读取到 $$
# chop;
# 如果 $_ 匹配正则
```

## 处理文件

打开文件并分配句柄 A 是可以在 Perl 程序中引用打开读取或写入文件的名称。当你与 shell 交互时，句柄被称为文件描述符（第 987 页）。在运行程序之前，内核会自动打开标准输入（第 243 页）、标准输出（第 243 页）和标准错误（第 297 页）句柄。程序运行结束后，内核会关闭这些描述符。

打开文件的语法是：

`open(HANDLE, MODE, FILENAME)`

模式可以是：

- `<` 用于读取
- `>` 用于写入（截断文件）
- `>>` 用于追加

常用的句柄有：

- `STDIN` 用于标准输入
- `STDOUT` 用于标准输出
- `STERR` 用于标准错误

当你打开文件时，使用句柄从文件读取或写入文件。例如：

```perl
open(my $fh, "<", "input.txt") or die "无法打开 input.txt: $!";
while (my $line = <$fh>) {
    print $line;
}
close($fh);
```

写入文件也是类似的：

```perl
open(my $fh, ">", "output.txt") or die "无法打开 output.txt: $!";
print $fh "Hello World!\n";
close($fh);
```

# 1068 第 28 章 PERL 脚本语言

此程序将 `/usr/share/dict/words`拷贝到标准输出。然后使用管道（第 170 页）将输出发送到 `head`（第 166 页），显示文件的前四行（第一行是空白）。

```perl
$ cat file2.pl
open (my $infile, "/usr/share/dict/words") or die "Cannot open dictionary: $!\n"
while ($line = <infile>) {
  print $line;
}
```

```perl
$ perl file2.pl | head -4
```

`$!`变量持有上一次系统错误。在数值语文中，它持有系统数字；在字符串语文中，它持有系统错误字符串。如果系统中不存在单词文件，file2.pl 将显示以下消息：

Cannot open dictionary: No file or directory

如果你对该文件没有读取权限，程序将显示此消息：

Cannot open dictionary: Permission denied

显示 `$!`的值比简单地说“程序无法打开文件”能提供更多关于错误的详细信息。

## 在打开文件时始终检查错误

当 Perl 程序尝试打开一个文件时，程序不会显示错误消息，除非它检查 `open`是否返回了错误。在 file2.pl 中，`open`语句中的 `or`允许 Perl 在 `open`失败时执行 `die`（第 1059 页）。`die`语句将消息 "Cannot open dictionary" 以及后续系统错误字符串发送到标准错误并终止程序。

`@ARGV`数组参数表示调用 Perl 时的命令行参数。当你使用一组文件名列表调用程序时，它会显示每个文件的第一行。如果程序无法读取某个文件，`die`（第 1059 页）会将错误消息发送到标准错误并退出。`foreach`结构循环遍历命令行参数（由 `@ARGV`表示），并将每个参数赋值给 `$filename`。`foreach`块以一个 `open`语句开始。Perl 执行 `or`操作符之前的 `open`语句，或者如果该执行失败，Perl 则执行 `or`操作符之后的语句（`die`）。结果是，Perl 要么通过 `$filename 打开文件并将 `$IN`分配为其句柄，或者如果无法打开该文件，则执行 `die`语句并退出。`print`语句显示文件名、冒号以及该文件的第一行。当它接受 `<IN`作为 `print`的参数时，Perl 会在赋值后显示 `$line`的值。从文件中读取一行后，程序会关闭该文件。

```perl
$ cat file3.pl
foreach $filename (@ARGV) {
  open (IN, $filename) or die "Cannot open file '$filename': $!\n";
  print "$filename: ", $line = <IN>;
  close(IN);
}
```

```perl
$ perl file3.pl f1 f2 f3 f4
f1: First line of file f1.
f2: First line of file f2.
Cannot open 'f3': No such file or directory
```

下一个示例与前一个相似，但它利用了若干 Perl 特性来使代码更简洁。它在读取新文件时不会退出。相反，Perl 会显示错误消息并继续。程序的第一行使用 `my`将 `$filename`描述为局部变量。接下来，`while`使用魔术文件句柄 `<>`打开并读取命令行参数文件名的每一行；`$ARGV`持有文件名。当没有更多文件可读时，`while`条件 `<<>`为假，`while`将控制权转移到 `while`块外部，程序终止。Perl 处理所有文件的打开和关闭操作；你不需要编写代码来处理这些任务。Perl 还会执行错误检查。

程序通过命令行参数显示每个文件的第一行。每次遍历 `while`块，`while`都会读取另一行。完成一个文件后，它从下一个文件开始。在 `while`块内部，它检查是否正在处理新文件。如果是，`if`块显示文件名和文件的（第一）行，然后将新文件名 `$ARGV`赋值给 `$filename`。

```perl
$ cat file3a.pl
my $filename;
while (<>) {
  if ($ARGV ne $filename) {
    print "$ARGV: $_\n";
    $filename = $ARGV;
  }
}
```

```perl
$ perl file3a.pl f1 f2 f3 f4
f1: First line of file f1.
f2: First line of file f2.
Can't open f3: No such file or directory at file3a.pl line 3, <> line 3.
f4: First line of file f4.
```

## 排序 (SORT)

`sort`函数根据 locale（第 1157 页）环境，按数字或字母顺序返回数组的元素。`reverse`函数与 `sort`无关；它按反序返回数组的元素。
