
示例的最后一行展示了如何使用参数调用 shell 函数。在这种情况下，hello 函数被调用时带有两个参数：Jane 和 Doe。hello 函数接收这两个参数并打印出一条内容为 Hello, Jane Doe 的行。

## 控制流程

在 Bash 脚本中，你可以通过使用 if、case、for 和 while 等特殊命令来控制执行流程——即命令执行的顺序。这些控制语句使用命令的退出状态来决定下一步做什么。当任何命令执行时，它会返回一个退出状态——一个表示命令是否成功执行的数值。按照惯例，退出状态为零表示命令执行成功。（是的，你读对了：零表示成功！）非零退出状态表示命令执行出现问题。

例如，假设你想在用 vi 编辑器编辑文件之前先制作文件的备份副本。更重要的是，如果无法制作备份，你希望避免编辑该文件。下面是一个 Bash 脚本，用于处理此任务：

```
#!/bin/sh
if cp "$1" "#$1"
then
    vi "$1"
else
    echo "Failed to create backup copy"
fi
```

此脚本说明了 if-then-else 结构的语法，并展示了 if 命令如何使用 cp 命令的退出状态来确定下一步操作。如果 cp 返回零，脚本将使用 vi 编辑文件；否则，脚本会显示错误消息并退出。顺便说一下，脚本将备份保存在一个文件中，其名称与原文件相同，只是文件名开头添加了一个井号（#）。

![](img/a7eec43a54473e95dc5ea333fec1bd7_801_0.png)

不要忘记终止 if 命令的最后的 fi。忘记 fi 是 Bash 脚本中常见的错误来源。

你可以使用 test 命令来计算任何表达式，并将表达式的值用作命令的退出状态。假设你想要一个仅在文件已存在时才编辑文件的脚本。使用 test，你可以按如下方式编写这样的脚本：

```
#!/bin/sh
if test -f "$1"
then
    vi "$1"
else
    echo "No such file"
fi
```

test 命令的简写形式是将表达式放在方括号（[ ... ]）中。使用这种简写表示法，你可以按如下方式重写前面的脚本：

```
#!/bin/sh
if [ -f "$1" ]
then
    vi "$1"
else
    echo "No such file"
fi
```

注意：方括号的两侧必须有空格。

另一个常见的控制结构是 for 循环。下面的脚本将 1 到 10 的数字相加：

```
#!/bin/sh
sum=0
for i in 1 2 3 4 5 6 7 8 9 10
do
    sum=`expr $sum + $i`
done
echo "Sum = $sum"
```

此示例还说明了使用 expr 命令计算表达式。

case 语句用于根据变量的值执行一组命令。例如，考虑以下脚本，该脚本基于你的 Red Hat Linux 系统中 /etc/init.d/functions 文件中的 confirm() 函数：

```
#!/bin/sh
echo -n "What should I do -- (Y)es/(N)o/(C)ontinue? [Y] "
read answer
case $answer in
y|Y|*)
    echo "YES"
    ;;
c|C)
    echo "CONTINUE"
    ;;
n|N)
    echo "NO"
    ;;
*) echo "UNKNOWN"
;;
esac
```

将此保存到名为 `confirm` 的文件中并输入 `chmod +x confirm` 使其可执行。然后像这样尝试：

```
./confirm
```

当脚本提示你时，输入字符 y、n 或 c 中的一个，然后按 Enter。脚本应显示 YES、NO 或 CONTINUE。例如，当我输入 c（然后按 Enter）时，会发生以下情况：

```
What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c
CONTINUE
```

脚本显示提示并读取你输入的内容。你输入的内容存储在名为 `answer` 的变量中。然后 `case` 语句根据 `answer` 变量的值执行一段代码。例如，当我输入 c 时，将执行以下命令块：

```
c|C)
  echo "CONTINUE"
;;
```

`echo` 命令导致脚本显示 CONTINUE。

从此示例中，你可以看到 `case` 命令的一般语法如下：

```
case $variable in
  value1 | value2)
    command1
    command2
    ...other commands...
  ;;
  value3)
    command3
    command4
    ...other commands...
  ;;
esac
```

本质上，`case` 命令以单词 `case` 开始，以 `esac` 结束。代码的各个块被变量的值包围，其后跟一个右括号并以一对分号 (;;) 终止。

## 探索 Bash 的内置命令

Bash 有超过 50 个内置命令，包括 cd 和 pwd 等常用命令，以及许多其他不常用的命令。你可以在任何 Bash 脚本或 shell 提示符下使用这些内置命令。表 3-1 描述了大多数 Bash 内置命令及其参数。查看完这些信息后，输入 help cmd 以阅读有关特定内置命令的更多信息。例如，要了解有关内置命令 test 的更多信息，请输入以下内容：

```
help test
```

这样将在我的 Red Hat Linux 系统上显示以下信息：

```
test: test [expr]
Exits with a status of 0 (true) or 1 (false) depending on
the evaluation of EXPR. Expressions may be unary or binary. Unary
expressions are often used to examine the status of a file. There
are string operators as well, and numeric comparison operators.

File operators:
-a FILE True if file exists.
-b FILE True if file is block special.
-c FILE True if file is character special.
-d FILE True if file is a directory.
-e FILE True if file exists.
-f FILE True if file exists and is a regular file.
-g FILE True if file is set-group-id.
-h FILE True if file is a symbolic link.
-L FILE True if file is a symbolic link.
-k FILE True if file has its 'sticky' bit set.
-p FILE True if file is a named pipe.
-r FILE True if file is readable by you.
-s FILE True if file exists and is not empty.
-S FILE True if file is a socket.
-t FD True if FD is opened on a terminal.
-u FILE True if the file is set-user-id.
-w FILE True if the file is writable by you.
-x FILE True if the file is executable by you.
-O FILE True if the file is effectively owned by you.
-G FILE True if the file is effectively owned by your group.
(... Lines deleted ...)
```

必要时，help 命令的在线帮助包含大量详细信息。

某些外部程序可能与 Bash 内置命令同名。如果要运行此类外部程序，必须明确指定该程序的完整路径名。否则，Bash 将执行同名的内置命令。

![](img/a7eec43a54473e95dc5ea333fec1bd7_804_0.png)

### 表 3-1 Bash Shell 中内置命令摘要

| 此功能 | 执行以下操作 |
|---|---|
| `. filename [arguments]` | 从指定的文件读取并执行命令，使用可选参数（与 source 命令的工作方式相同）。 |
| `: [arguments]` | 展开参数但不处理它们。 |
| `[ expr ]` | 计算表达式 expr，如果 expr 为真则返回零状态。 |
| `alias [name=value] ...` | 定义别名。 |
| `bg [job]` | 将指定的作业置于后台。如果未指定作业，则将当前执行的命令置于后台。 |
| `bind [-m keymap] [-lvd] [-q name]` | 将键序列绑定到宏。 |
| `break [n]` | 退出 for、while 或 until 循环。如果指定了 n，则退出第 n 个外层循环。 |
| `builtin builtin_command [arguments]` | 执行 shell 内置命令。 |
| `cd [dir]` | 将当前目录更改为 dir。 |
| `command [-pVv] cmd [arg ...]` | 使用指定的参数运行命令 cmd（忽略任何名为 cmd 的 shell 函数）。 |
| `continue [n]` | 开始 for、while 或 until 循环的下一次迭代。如果指定了 n，则开始第 n 个外层循环的下一次迭代。 |
| `declare [-frxi] [name=value]` | 声明具有指定名称的变量，并可选择为其赋值。 |
| `dirs [-l] [-/+n]` | 显示当前记住的目录列表。 |
| `echo [-neE] [arg ...]` | 在标准输出上显示参数。 |
| `enable [-n] [-all] [name ...]` | 启用或禁用指定的内置命令。 |
| `eval [arg ...]` | 连接参数并作为命令执行。 |
| `exec [command [arguments]]` | 用运行指定命令的新进程替换当前 shell 实例。 |
| `exit [n]` | 以状态码 n 退出 shell。 |
| `export [-nf] [name=word] ...` | 定义指定的环境变量并将其导出到未来进程。 |

