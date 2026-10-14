
```text
[me@linuxbox ~]$ foo="yes"
[me@linuxbox ~]$ echo $foo
yes
[me@linuxbox ~]$ echo $foo1
[me@linuxbox ~]$
```

我们首先将值 `yes` 分配给变量 `foo`，然后用 `echo` 显示其值。接下来我们显示拼写错误为 `foo1` 的变量名的值，结果为空。这是因为 shell 在遇到它时愉快地创建了变量 `foo1`，然后将其赋予默认值，即空或无。从中我们了解到，我们必须密切注意拼写！也很重要理解在这个例子中到底发生了什么。从我们之前对 shell 如何执行扩展的了解，我们知道命令

```text
[me@linuxbox ~]$ echo $foo
```

会进行参数扩展并变成

```text
[me@linuxbox ~]$ echo yes
```

另一方面，命令

```text
[me@linuxbox ~]$ echo $foo1
```

会扩展成

```text
[me@linuxbox ~]$ echo
```

空变量会扩展为空！这会让需要参数的命令陷入混乱。这里有一个例子：

```text
[me@linuxbox ~]$ foo=foo.txt
[me@linuxbox ~]$ foo1=foo1.txt
[me@linuxbox ~]$ cp $foo $fool
cp: missing destination file operand after 'foo.txt'
Try 'cp --help' for more information.
```

我们为两个变量 `foo` 和 `foo1` 分配了值。然后我们执行 `cp` 但拼错了第二个参数的名称。扩展后，`cp` 命令只收到一个参数，而它需要两个。

变量名有一些规则：

- 变量名可以由字母数字字符（字母和数字）和下划线字符组成。
- 变量名的第一个字符必须是字母或下划线。
- 不允许使用空格和标点符号。

单词变量意味着一个会改变的值，在许多应用中，变量就是这样使用的。然而，我们应用中的变量 `title` 被用作常量。常量就像变量一样，它有一个名称并包含一个值。不同之处在于常量的值不会改变。在执行几何计算的应用中，我们可能会将 `PI` 定义为常量并赋值为 `3.1415`，而不是在整个程序中字面使用该数字。shell 并不会区分变量和常量；这些术语主要是为了程序员的方便。一个常见的约定是使用大写字母来表示常量，而使用小写字母表示真正的变量。我们将修改脚本以符合此约定：

```bash
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"

echo "<HTML>

        <HEAD>

                <TITLE>$TITLE</TITLE>

        </HEAD>

        <BODY>

                <H1>$TITLE</H1>

        </BODY>

</HTML>"
```

我们还借此机会通过添加 shell 变量 `HOSTNAME` 的值来美化我们的标题。这就是机器的网络名称。

> **注意：** *shell 实际上确实提供了一种通过使用 `declare` 内置命令并带 `-r`（只读）选项来强制常量不可变性的方式。如果我们这样为 `TITLE` 赋值：*
>
>     declare -r TITLE="Page Title"
>
> *shell 将会阻止对 `TITLE` 的任何后续赋值。此功能很少使用，但在非常正式的脚本中存在。*

## 为变量和变量赋值

这里就是我们对扩展的知识真正开始发挥作用的地方。如我们所见，变量是这样赋值的：

`variable=value`

其中 `variable` 是变量名，`value` 是一个字符串。与某些其他编程语言不同，shell 不关心分配给变量的数据类型；它将所有数据都视为字符串。你可以通过使用 `declare` 命令并带 `-i` 选项来强制 shell 将赋值限制为整数，但与将变量设为只读一样，这很少被执行。注意在赋值中，变量名、等号和值之间不得有空格。那么值可以由什么组成？任何可以扩展为字符串的东西。

```bash
a=z                         # Assign the string "z" to variable a.
b="a string"                # Embedded spaces must be within quotes.
c="a string and $b"         # Other expansions such as variables can be
                            # expanded into the assignment.
d=$(ls -l foo.txt)           # Results of a command.

e=$(( 5 * 7))        # Arithmetic expansion.
f="{\t value string\n"  # Escape sequences such as tabs and newlines.
```

一次行上可以进行多个变量赋值：

```text
a=5 b="a string"
```

在展开期间，变量名可以被可选的大括号 `{}` 包围。这在变量名因其周围上下文而变得模糊时很有用。这里，我们尝试使用变量将文件 `myfile` 的名称更改为 `myfile1`：

```text
[me@linuxbox ~]$ filename="myfile"
[me@linuxbox ~]$ touch $filename
[me@linuxbox ~]$ mv $filename $filename1
mv: missing destination file operand after 'myfile'
Try 'mv --help' for more information.
```

此尝试失败，因为 shell 将 `mv` 命令的第二个参数解释为一个新（且为空）的变量。可以通过以下方式克服该问题：

```text
[me@linuxbox ~]$ mv $filename ${filename}1
```

通过添加周围的大括号，我们确保 shell 不再将尾随的 1 解释为变量名的一部分。

我们将借此机会向我们的报告中添加一些数据，即报告创建的日期和时间以及创建者的用户名：

```bash
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report for $HOSTNAME"

CURRENT_TIME=$(date "+%x %r %Z")

TIME_STAMP="Generated $CURRENT_TIME, by $USER"

echo "<HTML>"
	<HEAD>
		<TITLE>$TITLE</TITLE>
	</HEAD>
	<BODY>
		<H1>$TITLE</H1>
		<P>$TIME_STAMP</P>
	</BODY>
</HTML>"
```

## Here Documents

我们已经研究了两种输出文本的不同方法，两者都使用 `echo` 命令。第三种方法称为 *here document* 或 *here script*。Here document 是 I/O 重定向的另一种形式，我们在其中将一段文本嵌入到脚本中并将其馈送到命令的标准输入中。它的工作方式如下：

```text
command << token
text
token
```

其中 `command` 是接受标准输入的命令的名称，`token` 是用于指示嵌入文本结束的字符串。我们将修改脚本以使用 here document：

```bash
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"

CURRENT_TIME=$(date '+%Y %x %Z')

TIME_STAMP="Generated $CURRENT_TIME, by $USER"

cat << _EOF_
<HTML>
<HEAD>
<TITLE>$TITLE</TITLE>
</HEAD>
<BODY>
<H1>$TITLE</H1>
<P>$TIME_STAMP</P>
</BODY>
</HTML>
_EOF_
```
