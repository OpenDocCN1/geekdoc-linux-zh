
## for
循环的开始条件在循环开始时设置。每次执行循环时，都会执行增量函数，直到满足结束条件为止。这看起来很像传统的 for/next 循环。以下代码是 for 循环的示例：

```perl
for ($i=1; $i<=10; $i++) {
	print "$i\n"
}
```

## foreach
foreach 结构会对列表或数组中的每个元素执行一个语句块：

```perl
@names = ("alpha","bravo","charlie");
foreach $name (@names) {
	print "$name sounding off!\n";
}
```

循环变量（示例中的 $name）不仅仅是被设置为数组元素的值；它被别名指向该元素。这意味着如果你修改了循环变量，实际上你就修改了数组。如果未指定循环数组，可以使用 Perl 的默认变量 $_：

```perl
@names = ("alpha","bravo","charlie");
foreach (@names) {
	print "$_ sounding off!\n";
}
```

这种语法非常方便，但也可能导致代码可读性差。请考虑一下那些将要维护你代码的人的感受（很可能就是你自己）。

> **注意**
> foreach 常被缩写为 for。

## while
while 在特定条件为真时执行一个语句块：

```perl
while ($x<10) {
	print "$x\n";
	$x++;
}
```

请记住，条件可以是任何返回真或假值的表达式。例如，它可以是一个函数调用：

```perl
while ( InvalidPassword($user, $password) )   { 
print "You've entered an invalid password. Please try again.\n";
$password = GetPassword;
}
```

## until
until 是 while 语句的完全相反。它在特定条件为假时执行一个语句块——或者更准确地说，直到条件变为真时停止：

```perl
until (ValidPassword($user, $password)) {
print "You've entered an invalid password. Please try again.\n";
$password = GetPassword;
}
```

## last 和 next
你可以使用 last 语句强制 Perl 提前结束循环。last 类似于 C 语言中的 break 命令——循环将被退出。如果你决定需要跳过循环剩余的内容而不结束循环本身，可以使用 next，它类似于 C 语言中的 continue 命令。不幸的是，这些语句不能与 do . . . while 一起使用。

另一方面，你可以使用 redo 跳转到一个循环（由标签标记）或调用它的循环内部：

```perl
$a = 100;
while (1) {
print "start\n";
TEST: {
if (($a = $a / 2) > 2) {
print "$a\n";
if (--$a < 2) {
exit;
}
}
redo TEST;
}
}
```

在这个简单的示例中，变量 $a 在无限循环中被反复操作和测试。“start” 这个词只会被打印一次。

## do . . . while 和 do . . . until
while 和 until 循环首先评估条件。通过在条件前应用 do 块，行为会发生变化。使用 do 块时，条件是在最后评估的，这导致块中的内容总是至少执行一次（即使条件为假）。这类似于 C 语言的 do ... while (conditional) 语句。

## 正则表达式
Perl 最大的优势在于文本和文件操作，这是通过使用正则表达式（regex）库实现的。正则表达式与 shell 的通配符处理和文件名扩展功能（参见第 14 章）大不相同，允许高效且轻松地执行复杂的模式匹配和替换。

例如，下面这行代码将文本行中所有出现的字符串 bob 或字符串 mary 替换为 fred：

```perl
$string =~ s/bob|mary/fred/gi;
```

不深入太多细节，表 29.7 解释了上述代码的含义。

表 29.7 解释 $string =~ s/bob|mary/fred/gi;

| 元素 | 解释 |
| :--- | :--- |
| $string =~ | 对变量 $string 中找到的文本执行此模式匹配。 |
| s | 替换。 |
| / | 开始要匹配的文本。 |
| bob\|mary | 匹配文本 bob 或 mary。你应该记得，它查找的是文本 mary，而不是单词 mary；也就是说，它也会匹配单词 maryland 中的文本 mary。 |
| / | 结束要匹配的文本；开始替换文本。 |
| fred | 将匹配到的内容替换为文本 fred。 |
| / | 结束替换文本。 |
| g | 全局执行此替换；也就是说，在字符串中匹配到的任何位置替换匹配文本（不限次数）。 |
| i | 搜索文本不区分大小写。它匹配 bob、Bob 或 bOB。 |
| ; | 表示代码行的结束。 |

如果你对细节感兴趣，可以通过手册中的 regex (7) 部分获取更多信息。

虽然用一个字符串替换另一个字符串可能看似一个相当琐碎的任务，但在其他语言（例如 C）中实现相同功能所需的代码是相当令人望而生畏的，除非有外部库中的附加子程序支持。

## 访问 Shell
Perl 对于管理功能很有用，因为它可以访问 shell。这意味着 Perl 可以为你执行任何通常通过向 shell 输入命令来执行的过程。要在你的 Perl 程序中运行 Linux 命令，使用 ` ` 语法。例如，清单 29.4 中的代码打印目录列表。

### 清单 29.4 使用反引号访问 Shell

```perl
$curr_dir = `pwd`;
@listing = `ls -al`;
print "Listing for $curr_dir\n";
foreach $file (@listing) {
    print "$file";
}
```

> **注意**
> ` ` 符号使用的是 Tab 键上方的反引号（在大多数键盘上），而不是单引号。

你也可以使用 Shell 模块来访问 shell。Shell 是随 Perl 提供的标准模块之一；它允许创建和使用类似 shell 的命令行。查看以下代码作为一个示例：

```perl
use Shell qw(cp);
cp ("/home/httpd/logs/access.log", "/tmp/httpd.log");
```

这段代码看起来好像直接将命令行函数导入到 Perl 中。虽然实际上并不是这样，但你可以假装代码类似于命令行，并在你的 Perl 程序中使用这种方法。

访问 shell 的第三种方法是使用 system 函数调用：

```perl
$rc = 0xffff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded \n";
}
else {
    print "system cp failed $rc\n";
}
```

该调用也可以与 or die 子句一起使用：

```perl
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0
    or die "system cp failed: $?"
```

但是，你无法捕获通过 system 函数执行的命令的输出。

> **注意**
> 在 shell 脚本语言中，访问命令行相当常见，但在高级编程语言中则不太常见。

## 开关
Perl 有多种命令行选项（*开关*），可用于更改 Perl 行为的一个或多个方面。有些开关会更改输入数据的处理方式（例如行尾字符），而另一些则切换 Perl 的内部行为（例如开启调试）。这些开关可以出现在命令行上，也可以放在 Perl 程序开头的 `#!` 行上。

> **注意**
> 可以叠加多个命令行开关，因此 `-pie` 等同于 `-p -i -e`。

以下列表描述了所有可用的命令行开关：

- `-0 [digits]`—将输入记录分隔符（$/）指定为八进制数。$/ 通常是一个换行符，因此每条记录一行。例如，如果你将一个文件读入数组，这将给你一个数组元素一行。值 `00` 是一种特殊情况，它使 Perl 按段落读取文件，每段一条记录。
- `-a`—与 `-n` 或 `-p` 一起使用时，开启自动拆分（Autosplit）模式。这意味着输入的每一行都自动拆分到 `@F` 数组中。
- `-C`—为宽字符（多字节字符集）启用原生支持和系统接口。
- `-c`—告诉 Perl 对指定的 Perl 程序执行语法检查而不执行它。这非常有价值，给出的错误消息信息丰富、可读，并告诉你从哪里开始查找问题，这在错误消息中是罕见的。
- `-Debugs`—设置调试标志。更多细节请参阅 perlrun。
- `-d`—在 Perl 调试器下运行脚本。更多信息请参阅 perldebug。
- `-d:foo`—在作为 `Devel::foo` 安装的调试或跟踪模块控制下运行脚本。例如，`-d:Dprof` 使用 `Devel::Dprof` 分析器执行脚本。关于 Perl 调试器的更多信息请参阅 perldebug。
- `-e commandLine`—指示后续内容为 Perl 代码。这使你可以直接在命令行上输入 Perl 代码，而不是运行包含在文件中的代码：
  ```perl
  $ perl -e 'print join " ", keys %ENV;'
  ```
- `-Fpattern`—指定当 `-a` 也生效时用于拆分的模式。默认为 ""，而 `-F` 允许你将其设置为适合你的任何内容，例如 `','`、`';'`。模式可以包围在 `//`、`""` 或 `''` 中。
- `-h`—输入 `perl -h` 列出所有可用的命令行开关。

