
大于号，后跟要捕获输出数据的文件名。通过使用两个大于号，你可以将输出数据追加到现有文件中。小于号用于将输入重定向到命令。你可以将输入从文件重定向到命令。

Linux 管道命令（断字符符号）允许你将一个命令的输出直接重定向到另一个命令的输入。Linux 系统同时运行这两个命令，将第一个命令的输出发送到第二个命令的输入中，而无需使用任何重定向文件。

Bash shell 提供了几种方法供你在 shell 脚本中执行数学运算。expr 命令是一种执行整数运算的简单方法。在 Bash shell 中，你还可以通过在方括号内包裹等式（并以美元符号开头）来执行基本数学计算。若要执行浮点算术，你需要使用 bc 计算器命令，将输入重定向自内联数据，并将输出存储在一个用户变量中。

最后，我们讨论了如何在 shell 脚本中使用退出状态。每个在 shell 中运行的命令都会产生一个退出状态。退出状态是介于 0 和 255 之间的整数值，用于指示命令是否成功完成，如果没有成功，则可能说明原因。退出状态为 0 表示命令成功完成。你可以在 shell 脚本中使用 exit 命令来声明脚本完成时的特定退出状态。

到目前为止，你的 shell 脚本中的事情都按顺序从一个命令平稳地过渡到下一个命令。在下一章中，你将了解如何使用某些逻辑流程控制来更改脚本中执行哪些命令。

# 第 12 章

# 使用结构化命令

## 本章内容

- 处理 if-then 语句
- 嵌套 if
- 理解 test 命令
- 测试复合条件
- 使用双括号和圆括号
- 查看 case

在第 11 章“基本脚本构建”中，shell 按照命令在 shell 脚本中出现的顺序处理每个单独的命令。虽然这对于顺序操作来说运行良好，但许多程序需要脚本中命令之间的某种逻辑流程控制。

有一整个命令类允许 shell 根据测试条件跳过脚本部分并改变操作流。这些命令通常被称为结构化命令。

Bash shell 中有许多可用的结构化命令，因此我们将它们划分为不同的章节。在本章中，我们查看 if-then 和 case 语句。

## 处理 if-then 语句

最基本的结构化命令类型是 if-then 语句。if-then 语句具有以下格式：

```bash
if command
then commands
fi
```

如果你在其他编程语言中使用过 `if`-`then` 语句，这种格式可能会让你有些困惑。在其他编程语言中，`if` 语句后的对象是一个等式，用于评估 `true` 或 `false` 值。Bash shell 的 `if` 语句并非如此工作。

Bash shell 的 `if` 语句会执行定义在 `if` 行上的命令。如果命令的退出状态（见[第 11 章](Chapter11)）为零（命令成功完成），则执行列在 `then` 部分下的命令。如果命令的退出状态不是零，则不执行 `then` 命令，Bash shell 继续执行脚本中的下一个命令。`fi` 语句标记了 `if`-`then` 语句的结束。

下面是一个简单的示例，用来说明这个概念：

```bash
$ cat test1.sh
#!/bin/bash
# testing the if statement
if pwd
then
  echo "It worked"
fi
$
```

此脚本在 `if` 行中使用了 `pwd` 命令。如果命令成功完成，`echo` 语句应显示该文本字符串。当我们从命令行运行此脚本时，得到以下结果：

```bash
$ ./test1.sh
/home/christine/scripts
It worked
$
```

shell 执行了列在 `if` 行上的 `pwd` 命令。由于退出状态为零，它还执行了列在 `then` 部分中的 `echo` 语句。

这是另一个示例：

```bash
$ cat test2.sh
#!/bin/bash
# testing an incorrect command
if IamNotaCommand
then    echo "It worked"
fi
echo "We are outside the if statement"
$
./test2.sh
./test2.sh: line 3: IamNotaCommand: command not found
We are outside the if statement
$
```

在此示例中，我们在 `if` 语句行中故意使用了一个不存在的命令 IamNotaCommand。由于这是一个错误的命令，它会产生非零的退出状态。因此，Bash shell 跳过了 `then` 部分中的 `echo` 语句。还要注意，尽管是从 `if` 语句中的命令运行中产生的，错误消息仍然显示在脚本的输出中。有时你可能不希望错误声明出现。第 15 章“呈现数据”讨论了如何避免这种情况。

> ### 注意
>
> 你可能会在某些脚本中看到 `if-then` 语句的替代形式：
>
> ```
> if command; then
>    commands
> fi
> ```
>
> 通过在要评估的命令末尾加上分号（`;`），你可以将 `then` 语句包含在同一行上，这看起来更接近某些其他编程语言处理 `if-then` 语句的方式。

`then` 部分并不限于仅一个命令。你可以像在 shell 脚本的其他部分一样列出命令。Bash shell 将这些命令视为一个块，当 `if` 语句行中的命令返回零退出状态时执行所有命令，或当命令返回非零退出状态时跳过所有命令：

```bash
$ cat test3.sh
#!/bin/bash
# testing multiple commands in the then block
#
testuser=christine
#
if grep $testuser /etc/passwd
then
    echo "This is my first command in the then block."
    echo "This is my second command in the then block."
    echo "I can even put in other commands besides echo:"
    ls /home/$testuser/*.sh
fi
echo "We are outside the if statement"
```

if 语句行使用 grep 命令搜索 /etc/passwd 文件，以查看系统中是否正在使用特定的用户名。如果存在具有该登录名的用户，脚本将显示一些文本，然后列出用户 $HOME 目录中的 Bash 脚本：

```bash
$ ./test3.sh
christine:x:1001:1001::/home/christine:/bin/bash
This is my first command in the then block.
This is my second command in the then block.
I can even put in other commands besides echo:
/home/christine/factorial.sh
We are outside the if statement
$
```

但是，如果你将 testuser 变量设置为系统中不存在的用户，则 then 代码块内的内容都不会执行：

```bash
$ cat test3.sh
#!/bin/bash
# testing multiple commands in the then block
#
testuser=NoSuchUser
#
if grep $testuser /etc/passwd
then
    echo "This is my first command in the then block."
    echo "This is my second command in the then block."
    echo "I can even put in other commands besides echo:"
    ls /home/$testuser/*.sh
fi
echo "We are outside the if statement"
$ ./test3.sh
We are outside the if statement
$
```

这并不那么令人兴奋。如果我们能显示一条简短的消息，说明在系统中未找到该用户名，那就好了。当然可以，我们可以使用 if-then 语句的另一个特性来实现。

## 探索 if-then-else 语句

在 if-then 语句中，对于命令是否成功你只有一个选项。如果命令返回非零退出状态码，Bash shell 只是继续执行脚本中的下一个命令。在这种情况下，能够执行另一组命令将是很好的。这正是 if-then-else 语句的作用所在。

if-then-else 语句在语句中提供了另一组命令：

```bash
if command
then
commands
else
commands
fi
```

当 if 语句行中的命令返回零退出状态码时，列在 then 部分中的命令会被执行，正如普通的 if-then 语句那样。当 if 语句行中的命令返回非零退出状态码时，Bash shell 执行 else 部分中的命令。

现在你可以复制并修改测试脚本，以包含一个 else 部分：

```bash
$ cp test3.sh test4.sh
$
$ nano test4.sh
$
$ cat test4.sh
#!/bin/bash
# testing the else section
#
testuser=NoSuchUser
```

