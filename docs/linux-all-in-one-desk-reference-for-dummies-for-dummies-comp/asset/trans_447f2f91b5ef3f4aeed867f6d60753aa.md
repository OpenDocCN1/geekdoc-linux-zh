
# while 语句

Perl 的 while 语句比 C 语言的更通用，因为几乎可以使用任何内容作为要测试的条件。例如，如果使用数组作为条件，while 循环会执行到数组中没有任何元素为止，如下面的示例所示：

```perl
# Assume @cmd_arg has the current set of command arguments
while (@cmd_arg)
{
    $arg = shift @cmd_arg; # this extracts one argument
    # Code to process the current argument
    print $arg;
}
```

shift 函数移除数组的第一个元素并返回该元素。

你可以使用 **next** 关键字跳过循环的当前迭代进入下一次迭代；**last** 关键字则退出循环。例如，下面的 while 循环对 1 到 10 的数字求和，但跳过了 5：

```perl
while (1)
{
    $i++;
    if($i == 5) { next;} # Jump to the next iteration if $i is 5
    if($i > 10) { last;} # When $i exceeds 10, end the loop
    $sum += $i;       # Add the numbers
}
# At this point $sum should be 50
```

## for 和 foreach

Perl 和 C 的 for 语句语法相似。使用 for 语句可以根据表达式的值执行语句任意次数。语法如下：

```perl
for (expr_1; expr_2; expr_3) { statement block }
```

*expr_1* 在循环开始时评估一次；语句块执行直到 *expr_2* 的值为零。第三个表达式 *expr_3* 在语句块每次执行后评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必需的。下面是一个使用 *for* 循环将 1 到 10 的数字相加的示例：

```perl
for ($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在这个示例中，相加数字的实际工作是在第三个表达式中完成的，而 *for* 循环控制的语句是一个空块 ( {})。

`foreach` 语句最适合用于数组。以下是语法：

```perl
foreach Variable (Array) { statement block }
```

`foreach` 语句将 *Array* 中的一个元素赋值给 *Variable* 并执行语句块。`foreach` 语句重复此过程，直到没有数组元素剩余。下面的 `foreach` 语句将 1 到 10 的数字相加：

```perl
foreach $i (1..10) { $sum += $i;}
```

注意，我使用范围运算符 (`..`) 声明数组。你也可以使用逗号分隔的项列表作为数组。

![](img/11709a8f88c8cd03868a929dc94c0e2b_783_0.png)

如果你省略 `foreach` 语句中的 *Variable*，Perl 会隐式使用 `$_` 变量来保存当前数组元素。因此你可以使用以下代码：

```perl
foreach (1..10) { $sum += $_;}
```

## `goto`

`goto` 语句使 Perl 跳转到由标签标识的语句。这里有一个示例，它提示用户输入值，如果值不可接受则重复请求：

```perl
ReEnter:   print "Enter offset: ";
   $offset = <STDIN>;
   chop $offset;
   unless ($offset > 0 && $offset < 512)
   {
       print "Bad offset: $offset\n";
       goto ReEnter;
   }
```

## 访问 Linux 命令

你可以以多种方式从 Perl 中执行任何 Linux 命令：

- 调用 `system` 函数，使用包含要执行的 Linux 命令的字符串。
- 将 Linux 命令包含在反引号 (``) 中，这也称为 *grave accents*。你可以通过这种方式运行 Linux 命令并捕获其输出。
- 调用 `fork` 函数以复制当前脚本，并在子进程中处理新命令。（如果一个进程启动了另一个进程，新进程被称为 *child* 进程。）
- 调用 exec 函数用新脚本或 Linux 命令覆盖当前脚本。
- 使用 fork 和 exec 来提供类似 shell 的行为。（监控用户输入并通过子进程处理每个用户输入的命令。）

在本节中，我将展示一个如何实现此任务的简单示例。

在脚本中执行 Linux 命令的最简单方法是使用 system 函数并将命令放在字符串中。在 system 函数返回后，命令的退出代码位于 $? 变量中。你可以轻松编写一个简单的 Perl 脚本，该脚本从标准输入读取字符串并使用 system 函数处理该字符串。请遵循以下步骤：

1. 使用文本编辑器输入并将以下脚本保存为名为 rcmd.pl 的文件：

```perl
#!/usr/bin/perl
# Read user input and process command
$prompt = "Command (\"exit\" to quit)"; 
print $prompt;

while (<STDIN>)
{
        chomp;
        if ($_ eq "exit") { exit 0;}

        # Execute command by calling system
        system $_;
        unless ($? == 0) {print "Error executing: $_\n";}
        print $prompt;
}
```

2. 使用以下命令使 rcmd.pl 文件可执行：
   ```bash
   chmod +x rcmd.pl
   ```

3. 在 shell 提示符下键入 `./rcmd.pl` 来运行脚本。

以下是 rcmd.pl 脚本的一个示例输出。（输出取决于你输入的命令）

```text
Command ("exit" to quit): ps
  PID TTY          TIME CMD
 3128 pts/2    00:00:00 bash
 3314 pts/2    00:00:00 rcmd.pl
 3315 pts/2    00:00:00 ps
Command ("exit" to quit): exit
```

你可以在 Perl 脚本中使用 fork 和 exec 来运行 Linux 命令。以下是一个使用 fork 和 exec 执行用户输入命令的示例脚本 — psh.pl：

```perl
#!/usr/bin/perl
# This is a simple script that uses "fork" and "exec" to
# run a command entered by the user
$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
    chomp;     # remove trailing newline
    if($_ eq "exit") { exit 0;}

    $status = fork;
    if($status)
    {
        # In parent... wait for child process to finish...
        wait;
        print $prompt;
        next;
    }
    else
    {
        exec $_;
    }
}
```

以下示例输出展示了 psh.pl 脚本如何执行 ps 命令：

```text
Command ("exit" to quit): ps
    PID TTY          TIME CMD
    3128 pts/2    00:00:00 bash
    3321 pts/2    00:00:00 psh.pl
    3322 pts/2    00:00:00 ps
Command ("exit" to quit): exit
```

Shell（如 bash）使用 fork 和 exec 组合来运行命令。

# 文件访问

你可能已经注意到本章各个示例中使用的 `<STDIN>` 表达式。这是 Perl 从文件读取的方式。在 Perl 中，*文件句柄*，也称为 *标识符*，在读取文件时赋予文件独特的身份。通常，文件句柄使用大写字母。**STDIN** 是预定义的文件句柄，表示标准输入 — 默认情况下是键盘。**STDOUT** 和 **STDERR** 是另外两个预定义的文件句柄。**STDOUT** 用于打印到终端，而 **STDERR** 用于打印错误消息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_785_0.png)

要从文件读取，请将文件句柄写在尖括号 (< >) 内。因此，`<STDIN>` 从标准输入读取一行。

你可以使用 open 函数打开其他文件。以下示例展示了如何打开 /etc/passwd 文件进行读取以及如何显示该文件中的行：

```perl
open (PWDFILE, "/etc/passwd"); # PWDFILE is the file handle
while (<PWDFILE>) { print $_;} # By default, input line is in $_
close PWDFILE;           # Close the file
```

默认情况下，open 函数以读取模式打开文件。你可以在文件名开头添加特殊字符来指示其他类型的访问。`>` 前缀以写入模式打开文件，而 `>>` 前缀以追加模式打开文件。下面是一个简短的脚本，它读取 /etc/passwd 文件并创建一个名为 output 的新文件，其中列出了所有没有实际 shell 的用户。（这些用户的密码条目在每行末尾都有 :/bin/false。）

```perl
#!/usr/bin/perl
# Read /etc/passwd and create list of users without any
# shell

open (PWDFILE, "/etc/passwd");
open (RESULT, ">output");    # open file for writing
while (<PWDFILE>)
{
	if ($_ =~ /\/bin\/false\n/) {print RESULT $_;}
}
close PWDFILE;
close RESULT;
```

执行此脚本后，你会在当前目录中找到一个名为 output 的文件。

# 带有管道前缀的文件名

一个有趣的文件名前缀是管道字符 — 竖线 (|)。如果你调用 open 并使用以 | 开头的文件名，文件名的其余部分将被视为命令。Perl 解释器执行该命令，你可以使用 print 调用向此命令发送输入。下面的 Perl 脚本使用 mail 命令向用户列表发送电子邮件：

```perl
#!/usr/bin/perl
# Send mail to a list of users
foreach ("root", "naba")
{
    open (MAILPIPE, "| mail -s Greetings");
    print MAILPIPE "Remember to send in your weekly report today!\n";
    close MAILPIPE;
}
```

如果文件名以管道字符 (|) 结尾，该文件名将作为命令执行；你可以使用尖括号 (<...>) 读取该命令的输出，如下面的示例所示：

Book VII  Chapter 4  Programming in Perl
