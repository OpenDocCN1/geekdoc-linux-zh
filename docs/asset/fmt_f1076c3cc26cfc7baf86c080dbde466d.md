
- `do-while` 循环与 `while` 循环类似，除了它在循环块的末尾而不是开始处检查循环表达式，从而保证循环块至少执行一次。

- 参见第 7.3.3 节，“`do/while` 和 `do/until` 循环”。

### 格式

```perl
do {
    code block A
} while (expression);
```

## 2.1 快速入门，快速参考

### 表 2.1 Perl 语法和结构（续）

#### do 循环

当需要至少执行一次代码块时，`do` 循环非常有用。它常用于输入/输出场景。

参见 7.3.3 节，“`*do*` 循环”。

**格式**

```perl
do {
    block of code
} while (conditional expression);
```

**示例**

```perl
$count = 0; # Initial value
do {
    print "$n ";
    $count++; # Increment value
} while ($count < 10); # Test
```

#### for 循环

`for` 循环包含三个需要求值的表达式，每个表达式之间用分号分隔。第一个表达式用于初始化变量，且只执行一次。第二个表达式测试该值是否为真；如果为真，则进入代码块；否则，退出循环。当语句块执行完毕后，控制返回到第三个表达式，该表达式会修改变量的值。然后再次测试第二个表达式，如此循环往复。

参见 7.3.4 节，“`*for*` 循环（三部分循环）”。

**格式**

```perl
for(initialization; conditional_expression; increment/decrement) {
    block of code
}
```

**示例**

```perl
for($count = 0; $count < 10; $count++){
    print "$count\n";
}
```

#### foreach 循环

`foreach` 仅用于遍历列表，每次设置一个项目，将 `$_` 或命名变量依次设置为列表的每个元素。它本质上是在列表上下文中使用的 `for` 循环。实际上，以下示例可以使用 `for` 或 `foreach` 来编写。

参见 7.3.5 节，“`*foreach*` (`*for*`) 循环”。

**格式**

```perl
foreach (1 . . 5){
    print "$_\n"; # prints 1 2 3 4 5
}
foreach $item ( @list ) {
    print $item, "\n";
}
```

**示例**

```perl
@dessert = ("ice cream", "cake", "pudding", "fruit");
foreach $choice (@dessert){ # iterates through each element in array
    print "Dessert choice is: $choice\n";
}
```

#### 循环控制

`last` 语句用于在循环块内部跳出循环。它常用于退出无限循环。`next` 语句用于跳过循环块中剩余的语句，并重新开始循环顶部的执行。

参见 7.4.3 节，“循环控制。”

**示例**

```perl
$n=0;
while( $n < 10) {
    print $n;
    if ($n == 3) {
        last;      # Break out of loop
    }
    $n++;
}
print "Out of the loop.\n";
```

**示例**

```perl
for($n=0; $n < 10; $n++) {
    if ($n == 3) {
        next;     # Start at top of loop;
    }             # skip remaining statements in block
    echo "\$n = $n\n";
}
print "Out of the loop.\n";
```

#### 子程序/函数

函数是执行任务的代码块，可以从程序的其他部分调用。数据可以通过参数传递给函数。函数可以返回也可以不返回值。任何有效的 Perl 代码都可以组成函数的定义块。函数外部的变量在函数内部也是可用的。`my` 运算符将使指定的变量成为词法变量，在其创建所在的块内可见。

参见第 11 章，“子程序是如何工作的？”

**格式**

```perl
sub function_name{
    block of code
}
```

**示例**

```perl
sub greetings() {
    print "Welcome to Perl!\n";  # Function definition
}
&greetings(); # Function call
greetings();  # Function call most commonly used
```

#### 文件

Perl 提供了 `open` 函数来打开文件和管道，以进行读取、写入和追加操作。`open` 函数接受用户定义的文件句柄作为其第一个参数，以及一个包含读写/追加符号后跟系统文件实际路径的字符串。

参见第 10 章，“掌握文件句柄。”

**示例**

要打开文件进行读取：

```perl
open (my $fh, "<", *filename*"); # Opens *filename* for reading. 
open (my $fh, "/home/ellie/myFile") or die "Can't open file: $!";
```

要打开文件进行写入：

```perl
open (my $fh, ">", *filename*"); # Opens *filename* for writing. 
# Creates or truncates file.
```

要打开文件进行追加：

```perl
open (my $fh, ">>", *filename*"); # Opens *filename* for appending. 
# Creates or appends to file.
```

要打开文件进行读写：

```perl
open (my $fh, "+<", *filename*");
```

关闭文件：

```perl
close($fh);
```

从文件读取：

```perl
while(<$fh>){ print; } # Read one line at a time from file.

@lines = <$fh>;
# Slurp all lines into an array.
print @lines."\n";
```

向文件写入：

```perl
open($fh, ">","$file") or die "Can't open file: $!\n";
print $fh "This line is written to the file just opened.\n";
print $fh "And this line is also written to the file just opened.\n";
```

#### 管道

管道可用于将系统命令的输出作为输入传递给 Perl，并将 Perl 的输出作为输入传递给系统命令。要创建管道（也称为过滤器），需要使用 `open` 系统调用。它接受两个参数：一个用户定义句柄和一个操作系统命令，该命令前缀或后缀带有 `|` 符号。如果命令前带有 `|`，则操作系统命令读取 Perl 的输出。如果命令后带有 `|` 符号，则 Perl 从管道读取；如果命令前带有 `|`，则 Perl 向管道写入。

参见第 10 章，“掌握文件句柄。”

### 正则表达式

正则表达式是一组通常被前向斜杠包围的字符。它们用于匹配文本中的模式，并细化搜索和替换。Perl 以其模式匹配功能而闻名（参见第 8 章，“正则表达式——模式匹配”）。表 2.2 列出了元字符及其在正则表达式中的含义。

#### 表 2.2 一些正则表达式元字符

| 元字符 | 表示含义 |
| :--- | :--- |
| `^` | 匹配行首 |
| `$` | 匹配行尾 |
| `a.c` | 匹配 a、任意单个字符和 c |
| `[abc]` | 匹配 a 或 b 或 c |
| `[^abc]` | 匹配不是 a、b 或 c 的字符 |
| `[0-9]` | 匹配 0 到 9 之间的一个数字 |
| `ab*c` | 匹配 a，后跟零个或多个 b 和一个 c |
| `ab+c` | 匹配 a，后跟一个或多个 b 和一个 c |
| `ab/?c` | 匹配 a，后跟零个或一个 b 和一个 c |
| `(ab)+c` | 匹配组 ab 的一个或多个出现，后跟 c |
