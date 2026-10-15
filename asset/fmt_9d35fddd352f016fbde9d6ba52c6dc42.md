
`shift` 函数移除数组的第一个元素并返回该元素。

你可以使用 `next` 关键字跳转到循环的末尾；使用 `last` 关键字退出循环。下面的 `while` 循环累加从 1 到 10 的数字，但跳过了 5：

## 第 24 章：Shell 和 Perl 脚本

```perl
while (1) {
  $i++;
  if($i == 5) { next; # 如果 $i 是 5，跳转到下一次迭代 }
  if($i > 10) { last; # 当 $i 超过 10 时，结束循环 }
  $sum += $i; # 相加数字
}
# 此时 $sum 的值应该是 50
```

### for 和 foreach

Perl 和 C 语言的 `for` 语句语法相似。使用 `for` 语句根据表达式的值执行任意次数的语句。语法如下：

```
for (expr_1; expr_2; expr_3) { statement block }
```

`expr_1` 在循环开始时评估一次；语句块一直执行，直到表达式 `expr_2` 评估结果为零。第三个表达式 `expr_3` 在每次执行完语句块后进行评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必须的。下面是一个使用 `for` 循环累加从 1 到 10 数字的示例：

```perl
for($i=1; $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在这个示例中，数字加数字的工作是在第三个表达式中完成的，而 `for` 循环控制的语句是一个空块（`{}`）。

`foreach` 语句适用于数组。语法如下：

```
foreach Variable (Array) { statement block }
```

`foreach` 语句将数组中的一个元素赋值给 `Variable` 并执行语句块。`foreach` 语句会重复此过程，直到数组没有剩余元素。下面的 `foreach` 语句累加从 1 到 10 的数字：

```perl
foreach $i (1..10) { $sum += $i; }
```

注意我使用范围运算符（`..`）声明数组。你也可以使用逗号分隔的项列表作为数组。

如果你在 `foreach` 语句中省略 `Variable`，Perl 会隐式使用 `$_` 变量来存储当前的数组元素。这时你可以使用以下代码：

```perl
foreach (1..10) { $sum += $_; }
```

### goto

`goto` 语句将控制权转移到语句标签。下面的示例提示用户输入一个值 `$i`，如果该值不可接受，则重复请求：

ReEnter:
```perl
print "Enter offset: ";
```
```perl
$offset = <STDIN>;
chomp $offset;
unless ($offset > 0 && $offset < 512) {
  print "Bad offset: $offset\n";
  goto ReEnter;
}
```

### 调用 Linux 命令

你可以通过多种方式从 Perl 中执行任何 Linux 命令：

- 调用 `system` 函数，并传入包含你想要执行的 Linux 命令的字符串。
- 使用反引号（`` ` ``，也称为重引号）将 Linux 命令括起来。你可以通过这种方式运行 Linux 命令并捕获其输出。
- 调用 `fork` 函数复制当前脚本，并在子进程中处理新命令。（如果一个进程启动另一个进程，则新的进程被称为子进程）。
- 调用 `exec` 函数，用新脚本或 Linux 命令覆盖当前脚本。
- 使用 `fork` 和 `exec` 提供类似 Shell 的行为。（监控用户输入，并通过子进程处理每个用户输入的命令。）本节节提供了一个如何完成此任务的简单示例。

执行 Linux 命令最简单的方法是使用 `system` 函数。注意 `system` 函数返回命令的退出状态。按照以下步骤操作：

- 使用文本编辑器保存以下内容：
```perl
#!/usr/bin/perl
# 此脚本执行一个 Linux 命令
system("ls -l");
```

- 使用反引号捕获输出：
```perl
$output = `ls -l`;
print $output;
```

- 使用 `fork` 运行子进程：
```perl
$pid = fork();
if ($pid == 0) {
    # 子进程
    exec("ls", "-l");
}
```

- 使用 `exec` 替换当前进程：
```perl
exec("ls", "-l");
```

# 第 24 章：Shell 和 Perl 脚本编程

```
mail:x:8:12:mail:/var/spool/mail/
news:x:9:13:news:/var/spool/news/
uucp:x:10:14:uucp:/var/spool/uucp/
operator:x:11:0:operator:/root/
games:x:12:100:games:/usr/games/
gopher:x:13:30:gopher:/usr/lib/gopher-data/
ftp:x:14:50:FTP :/var/ftp/
nbody:x:99:99:Nobody/:
```

## 子程序 (Subroutines)

尽管 Perl 包含了大量的内置函数，但你也可以以子程序的形式添加自己的代码模块。事实上，Perl 分发版带了大量的子程序。下面是一个简单的脚本，用于阐述 Perl 中子程序的语法：

```perl
#!/usr/bin/perl
sub hello
{
  # 从 @_ 数组中创建参数的本地副本
  local ($first,$last) = @_;
  print "Hello, $first $last\n"
}
$a = "Jane";
$b = "Doe";
&hello($a, $b);
# 调用子程序
```

## 管道化 Perl文件名 (Piping Perl Filenames)

一个有趣的文件名名前缀是字符——竖线 (`|`)。如果你在调用 `open` 时使用以 `|` 开头的文件，文件名其余部分将被视为命令。Perl 解释器会执行该命令，你可以使用 `print` 调用向该命令发送输入。下面的 Perl 脚本向用户列表发送了一条邮件消息：

```perl
#!/usr/bin/perl
# 向用户列表发送邮件
foreach ("root", "naba") {
  open (MAILPIPE, "| mail -s\n  Greetings $_;");
  print MAILPIPE "Remember to send in your weekly report today!\n";
  close MAILPIPE;
}
```

如果文件名以管道字符 (`|`) 结尾，该文件名将作为命令执行；你使用角括号 `<>` 读取该命令的输出，如下例所示：

```perl
open (PSPIPE, "ps ax |");
while (<PSPIPE>) {
  # 处理 ps 命令的输出
  # 此示例简单地打印每一行
  print $_;
}
```

# 第五部分：为 Red Hat Linux

当你运行上述脚本时，它会显示以下输出：
Hello, Jane Doe

注意关于子程序的以下几点：

- 子程序在数组 `@_`（at 符号后跟下划线字符）中接收其参数。
- 子程序中使用的变量默认是全局的。使用 `local` 函数来创建一组变量。
- 通过在名称前放置 ampersand (`&`) 来调用子程序。因此，通过输入 `&hello` 来调用子程序 `hello`。

如果你愿意，可以将子程序放在它单独的文件中。例如，`hello` 子程序可以位于名为 `hello.pl` 的文件中。当你将子程序放在文件中时，记住在文件末尾添加一个返回值——只需在末尾输入 `1;` 即可返回 1。因此，`hello.pl` 文件内容如下：

```perl
sub hello
(
  # 从 @_ 数组中创建参数的本地副本
  local($first,$last) = @_;
  print "Hello, $first $last\n"
)
1;  #返回值
```

然后，你必须编写使用 `hello` 子程序的脚本，如下：

```perl
#!/usr/bin/perl
require 'hello.pl'; # 包含包含子程序的文件
$a = "Jane";
$b = "Doe";
hello($a, $b); # 调用子程序
```

此脚本使用 `require` 函数来包含包含 `hello` 子程序定义的 `hello.pl` 文件。

## Perl 中的内置函数

Perl 拥有近 200 个内置函数（也称为 Perl 函数），包括类似于 C 运行时库中函数的函数，以及访问操作系统的函数。你真的需要浏览一遍函数列表，以体会 Perl 提供的广泛功能范围。表 24-3 简要描述了每个函数。

本章没有足够的空间涵盖这些函数，但你可以通过将万维网浏览器指向以下地址来学习 Perl 函数：

```
http://www.perl.com/CPAN/doc/manual/html/perl/func.html
```
