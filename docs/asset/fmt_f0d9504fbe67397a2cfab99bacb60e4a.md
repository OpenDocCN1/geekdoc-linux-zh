
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

Perl 和 C 的 `for` 语句语法相似。使用 `for` 语句根据表达式的值执行语句任意次数。语法如下：

```
for (expr_1; expr_2; expr_3) { statement block }
```

`expr_1` 在循环开始时只评估一次；语句块执行直到表达式 `expr_2` 评估为零。第三个表达式 `expr_3` 在每次执行语句块后评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必需的。以下是使用 `for` 循环将 1 到 10 的数字相加的示例：

```
for($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在此示例中，实际的加法工作在第三个表达式中完成，而 `for` 循环控制的语句是一个空块 ({})。

`foreach` 语句最适合用于数组。以下是语法：

```
foreach Variable (Array) { statement block }
```

`foreach` 语句将 `Array` 中的一个元素分配给 `Variable` 并执行语句块。`foreach` 语句重复此过程直到没有数组元素剩余。以下 `foreach` 语句将 1 到 10 的数字相加：

```
foreach $i (1..10) { $sum += $i; }
```

请注意，我使用范围运算符 (`..`) 声明数组。你也可以使用逗号分隔的项目列表作为数组。

如果你在 `foreach` 语句中省略 `Variable`，Perl 会隐式使用 `$_` 变量来保存当前数组元素。因此，你可以使用以下内容：

```
foreach (1..10) { $sum += $_; }
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_824_0.png)

### goto

`goto` 语句导致 Perl 跳转到由标签标识的语句。以下是提示用户输入值并在值不可接受时重复请求的示例：

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

- 使用包含要执行的 Linux 命令的字符串调用 `system` 函数。
- 将 Linux 命令用反引号 (`) 括起来，反引号也称为重音符。你可以通过这种方式运行 Linux 命令并捕获其输出。
- 调用 `fork` 函数复制当前脚本并在子进程中处理新命令。（如果一个进程启动另一个进程，则新进程称为子进程。）
- 调用 `exec` 函数用新脚本或 Linux 命令覆盖当前脚本。
- 使用 `fork` 和 `exec` 提供类似 shell 的行为。（监控用户输入，并通过子进程处理每个用户输入的命令。）在本节中，我将介绍一个实现此任务的简单示例。

最简单的方式在脚本中执行 Linux 命令是使用 `system` 函数并将命令放在字符串中。`system` 函数返回后，命令的退出代码位于 `$?` 变量中。你可以轻松编写一个简单的 Perl 脚本，从标准输入读取字符串并使用 `system` 函数处理该字符串。请按照以下步骤操作：

### 1. 使用文本编辑器输入以下脚本并保存到名为 `rcmd.pl` 的文件中：

```
#!/usr/bin/perl
# Read user input and process command

$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
  chop;
  if ($_ eq "exit") { exit 0;}

  # Execute command by calling system
  system $_;
  unless ($? == 0) {print "Error executing: $_\n";}
  print $prompt;
}
```

### 2. 使用以下命令使 `rcmd.pl` 文件可执行：

```
chmod +x rcmd.pl
```

### 3. 在 shell 提示符下输入 `./rcmd.pl` 运行脚本。

以下是 `rcmd.pl` 脚本的示例输出（输出取决于你输入的命令）：

```
Command ("exit" to quit): ps
PID TTY TIME CMD
767 pts/0 00:00:00 bash
940 pts/0 00:00:00 rcmd.pl
945 pts/0 00:00:00 ps
Command ("exit" to quit): exit
```

你也可以在 Perl 脚本中使用 `fork` 和 `exec` 运行 Linux 命令。以下是示例脚本 — `psh.pl` — 它使用 `fork` 和 `exec` 执行用户输入的命令：

```
#!/usr/bin/perl

# This is a simple script that uses "fork" and "exec" to
# run a command entered by the user

$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
    chop;   # remove trailing newline
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

以下示例输出显示了 `psh.pl` 脚本如何执行 `ps` 命令：

```
Command ("exit" to quit): ps
PID TTY          TIME CMD
767 pts/0    00:00:00 bash
949 pts/0    00:00:00 psh.pl
950 pts/0    00:00:00 ps
Command ("exit" to quit): exit
```

Shell（例如 `Bash`）使用 `fork` 和 `exec` 组合来运行命令。

## 文件访问

你可能已经注意到本章各种示例中的 `<STDIN>` 表达式。那是 Perl 读取文件的方式。在 Perl 中，文件句柄，也称为标识符，在读取时为文件提供独特的身份。通常，文件句柄使用大写字符。`STDIN` 是一个预定义的文件句柄，表示标准输入——默认情况下为键盘。`STDOUT` 和 `STDERR` 是另外两个预定义的文件句柄。`STDOUT` 用于向终端打印，`STDERR` 用于打印错误消息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_827_0.png)

要从文件读取，请将文件句柄写在尖括号（< >）内。因此，`<STDIN>` 从标准输入读取一行。

你可以使用 `open` 函数打开其他文件。以下示例展示了如何打开 `/etc/passwd` 文件进行读取以及如何显示该文件中的行：

```
open (PWDFILE, "/etc/passwd");  # PWDFILE is the file handle
while (<PWDFILE>) { print $_; }  # By default, input line is in $_
close PWDFILE;  # Close the file
```

默认情况下，`open` 函数以读取方式打开文件。你可以在文件名开头添加特殊字符以指示其他类型的访问。 `<` 前缀用于打开文件进行写入，而 `>` 前缀用于打开文件进行追加。以下是读取 `/etc/passwd` 文件并创建一个名为 `output` 的新文件，其中列出所有没有 shell 的用户（这些用户的密码条目在每行末尾都有 :）的简短脚本：
