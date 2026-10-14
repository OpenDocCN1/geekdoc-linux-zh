
## Summing Up

在本章中，我们介绍了一种常见的程序设计方法，称为自顶向下设计，并看到了 shell 函数如何用于构建其所需的逐步细化。我们还看到了局部变量如何用于使 shell 函数彼此独立以及与它们所在的程序独立。这使得 shell 函数可以以可移植的方式编写并可重用，因为它们可以放置在多个程序中；这大大节省了时间。

## Further Reading

- Wikipedia 上有许多关于软件设计哲学的文章。以下是几个不错的文章：
  - http://en.wikipedia.org/wiki/Top-down_design
  - http://en.wikipedia.org/wiki/Subroutines

## 27 – Flow Control: Branching With if

在上一章中，我们遇到了一个问题。如何使我们的报告生成脚本适应运行脚本的用户权限？解决此问题的方案需要我们找到一种根据测试结果在脚本中“改变方向”的方法。在编程术语中，我们需要程序进行分支。

让我们考虑用伪代码表达的一个简单逻辑示例，伪代码是一种面向人类消费的计算机语言模拟：
`X = 5`
If `X = 5`, then:
    Say “X equals 5.”
Otherwise:
    Say “X is not equal to 5.”

这是一个分支示例。根据条件，“X 是否等于 5？”执行一件事，“说 X 等于 5”，否则执行另一件事，“说 X 不等于 5。”

### if

使用 shell，我们可以按如下方式编码上述逻辑：

```
x=5

if [ $x -eq 5 ]; then

    echo "x equals 5."

else

    echo "x does not equal 5."

fi
```

或者我们可以直接在命令行输入它，略微缩短：

```
[me@linuxbox ~]$ x=5

[me@linuxbox ~]$ if [ $x -eq 5 ]; then echo "equals 5"; else echo "does not equal 5"; fi

equals 5

[me@linuxbox ~]$ x=0

[me@linuxbox ~]$ if [ $x -eq 5 ]; then echo "equals 5"; else echo "does not equal 5"; fi

does not equal 5
```

在此示例中，我们执行了两次命令。第一次将 `x` 的值设为 5，结果输出字符串“equals 5”，第二次将 `x` 的值设为 0，结果输出字符串“does not equal 5”。

`if` 语句的语法如下：

```
if commands; then

    commands

[elif commands; then

    commands...]

[else

    commands]

fi
```

其中 `commands` 是一个命令列表。乍一看这有点令人困惑。但在澄清之前，我们必须先了解 shell 如何评估命令的成功或失败。

### Exit Status

命令（包括我们编写的脚本和 shell 函数）在终止时会向系统发出一个值，称为退出状态。该值是一个介于 0 到 255 之间的整数，表示命令执行的成功或失败。根据惯例，值为零表示成功，任何其他值表示失败。shell 提供了一个参数供我们检查退出状态。下面我们看到它的实际使用情况：

```
[me@linuxbox ~]$ ls -d /usr/bin

/usr/bin

[me@linuxbox ~]$ echo $?

0

[me@linuxbox ~]$ ls -d /bin/usr

ls: cannot access /bin/usr: No such file or directory

[me@linuxbox ~]$ echo $?

2
```

在此示例中，我们执行了两次 `ls` 命令。第一次，命令执行成功。如果我们显示参数 `$?` 的值，会看到它为零。我们第二次执行 `ls` 命令，产生错误，然后再次检查参数 `$?`。这次它包含 2，表示命令遇到错误。一些命令使用不同的退出状态值来提供错误诊断，而许多命令在失败时简单地以值为 1 退出。手册页通常包含一个名为“Exit Status”的部分，描述了使用的代码。然而，零始终表示成功。

shell 提供了两个极其简单的内置命令，它们除了以零或一的退出状态终止外什么都不做。`true` 命令总是执行成功，而 `false` 命令总是执行不成功：

```
[me@linuxbox ~]$ true

[me@linuxbox ~]$ echo $?

0

[me@linuxbox ~]$ false

[me@linuxbox ~]$ echo $?

1
```

我们可以使用这些命令来了解 `if` 语句的工作原理。`if` 语句真正做的是评估命令的成功或失败：

```
[me@linuxbox ~]$ if true; then echo "It's true."; fi

It's true.

[me@linuxbox ~]$ if false; then echo "It's true."; fi
```

当 `if` 之后的命令执行成功时，命令 `echo "It's true."` 会被执行，而当 `if` 之后的命令未执行成功时则不会执行。如果 `if` 后面跟着一系列命令，则评估该列表中的最后一个命令：

```
[me@linuxbox ~]$ if false; true; then echo "It's true."; fi

It's true.

[me@linuxbox ~]$ if true; false; then echo "It's true."; fi
```

### test

与 `if` 一起使用最多的命令当属 `test`。`test` 命令执行各种检查和比较。它有两种等价形式：

```
test expression
```

以及更受欢迎的：

```
[ expression ]
```

其中 `expression` 是一个被评估为 true 或 false 的表达式。`test` 命令在表达式为真时返回零的退出状态，在表达式为假时返回一的状态。

### File Expressions

以下表达式用于评估文件状态：

Table 27-1: test File Expressions

| Expression | Is True If: |
|---|---|
| file1 -ef file2 | file1 和 file2 具有相同的 inode 编号（两个文件名通过硬链接引用同一个文件）。 |
| file1 -nt file2 | file1 比 file2 新。 |
| file1 -ot file2 | file1 比 file2 老。 |
| -b file | file 存在且为块特殊（设备）文件。 |
| -c file | file 存在且为字符特殊（设备）文件。 |
| -d file | file 存在且为目录。 |
| -e file | file 存在。 |
| -f file | file 存在且为普通文件。 |
| -g file | file 存在且已设置组 ID。 |
| -G file | file 存在且由有效组 ID 拥有。 |
| -k file | file 存在且已设置其“粘滞位”。 |
| -L file | file 存在且为符号链接。 |
| -O file | file 存在且由有效用户 ID 拥有。 |
| -p file | file 存在且为命名管道。 |
| -r file | file 存在且可读（对 |
|  | the effective user). |
| -s *file* | *file* 存在且长度大于零。 |
| -S *file* | *file* 存在且为网络套接字。 |
| -t *fd* | *fd* 是指向/来自终端的文件描述符。这可用于确定标准输入/输出/错误是否被重定向。 |
| -u *file* | *file* 存在且已设置 setuid。 |
| -w *file* | *file* 存在且可写（对有效用户具有写权限）。 |
| -x *file* | *file* 存在且可执行（对有效用户具有执行/搜索权限）。 |

Here we have a script that demonstrates some of the file expressions:

```
#!/bin/bash

# test-file: Evaluate the status of a file

FILE=~/.bashrc

if [ -e "$FILE" ]; then

    if [ -f "$FILE" ]; then

        echo "$FILE is a regular file."

    fi

    if [ -d "$FILE" ]; then
