
# System Information Report

```
</HEAD>
<BODY>
<H1>System Information Report</H1>
</BODY>
</HTML>"
```

我们为报告的标题添加了一个页面标题和一个标题。

## 变量和常量

我们的脚本存在一个问题，不过。注意字符串“System Information Report”是如何重复出现的？对于我们这个小脚本来说这不是问题，但让我们想象一下我们的脚本非常长并且有多个该字符串的实例。如果我们想把标题改成其他内容，我们就必须在多个地方进行更改，这可能会很费力。如果我们能安排脚本使字符串只出现一次而不是多次会怎样？那样会使脚本的未来维护变得容易得多。我们可以这样做：

```bash
#!/bin/bash

# Program to output a system information page

title="System Information Report"

echo "<HTML>

<HEAD>

<TITLE>$title</TITLE>

</HEAD>

<BODY> <H1>$title</H1>

</BODY>

</HTML>"
```

通过创建一个名为 `title` 的变量并将其赋值为“System Information Report”，我们可以利用参数扩展并将字符串放在多个位置。

那么，我们如何创建变量呢？很简单，我们直接使用它。当 shell 遇到一个变量时，它会自动创建它。这与许多编程语言不同，在那些语言中变量必须在使用前显式声明或定义。shell 对此非常宽松，这可能导致一些问题。例如，考虑在命令行上发生的这个场景：

```bash
[me@linuxbox ~]$ foo="yes"
[me@linuxbox ~]$ echo $foo
yes
[me@linuxbox ~]$ echo $fool
[me@linuxbox ~]$
```

我们首先将值“yes”赋给变量 `foo`，然后用 `echo` 显示其值。接下来我们显示拼写错误的变量名“fool”的值，结果为空白。这是因为 shell 在遇到它时愉快地创建了变量 `fool`，并赋予它默认值，即空。从中我们了解到必须密切注意拼写！也很重要理解在这个例子中到底发生了什么。从我们之前对 shell 如何执行扩展的了解，我们知道命令：

```bash
[me@linuxbox ~]$ echo $foo
```

经过参数扩展后变为：

```bash
[me@linuxbox ~]$ echo yes
```

而命令：

```bash
[me@linuxbox ~]$ echo $fool
```

扩展为：

```bash
[me@linuxbox ~]$ echo
```

空变量扩展为空！这会让需要参数的命令大乱。这里有一个例子：

```bash
[me@linuxbox ~]$ foo=foo.txt
[me@linuxbox ~]$ fool=fool.txt
[me@linuxbox ~]$ cp $foo $fool
cp: missing destination file operand after `foo.txt'
```

```
Try `cp --help` for more information.
```

我们为两个变量 `foo` 和 `foo1` 赋了值。然后执行 `cp`，但拼错了第二个参数的名称。扩展后，`cp` 命令只收到一个参数，而它需要两个。

变量名有一些规则：

- 1. 变量名可以由字母数字字符（字母和数字）和下划线字符组成。
- 2. 变量名的第一个字符必须是字母或下划线。
- 3. 不允许使用空格和标点符号。

“变量”一词意味着一个会变化的值，在许多应用中变量就是这样使用的。然而，我们应用程序中的变量 `title` 被用作常量。常量就像变量一样，它有一个名称并包含一个值。不同之处在于常量的值不会改变。在执行几何计算的应用程序中，我们可能会将 `PI` 定义为常量，并赋值为 3.1415，而不是在整个程序中字面使用该数字。shell 对变量和常量没有区别；它们主要是为了程序员的方便。一个常见的约定是使用大写字母来表示常量，使用小写字母表示真正的变量。我们将修改脚本以符合此约定：

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

**注意：** shell 实际上确实提供了一种通过使用 `declare` 内置命令并带 `-r`（只读）选项来强制常量不可变的方式。如果我们这样为 `TITLE` 赋值：

```bash
declare -r TITLE="Page Title"
```

shell 将会阻止对 `TITLE` 的任何后续赋值。此功能很少使用，但在非常正式的脚本中存在。

### 为变量和常量赋值

这里我们的扩展知识真正开始发挥作用了。如我们所见，变量是这样赋值的：
`*variable=value*`

其中 `*variable*` 是变量名，`*value*` 是一个字符串。与某些其他编程语言不同，shell 不关心分配给变量的数据类型；它将所有数据都视为字符串。你可以通过使用带 `-i` 选项的 `declare` 命令来强制 shell 将赋值限制为整数，但与将变量设为只读一样，这很少被执行。

请注意，在赋值中，变量名、等号和值之间不得有空格。那么值可以由什么组成呢？任何可以扩展为字符串的内容：

```bash
a=z                  # Assign the string "z" to variable a.
b="a string"        # Embedded spaces must be within quotes.
c="a string and $b" # Other expansions such as variables can be expanded into the assignment.
d=$(ls -l foo.txt)    # Results of a command.
e=$((5 * 7))          # Arithmetic expansion.
f="\t\ta string\n" # Escape sequences such as tabs and newlines.
```

可以在单行上进行多个变量赋值：

```bash
a=5 b="a string"
```

在扩展期间，变量名可以被可选的大括号 `"{}"` 包围。这在变量名因其周围上下文而变得模糊时很有用。这里，我们尝试使用变量将文件名从 `myfile` 改为 `myfile1`：

```bash
[me@linuxbox ~]$ filename="myfile"
[me@linuxbox ~]$ touch $filename
[me@linuxbox ~]$ mv $filename $filename1
mv: missing destination file operand after `myfile'
Try `mv --help' for more information.
```

此尝试失败，因为 shell 将 `mv` 命令的第二个参数解释为一个新（且为空）的变量。问题可以通过以下方式克服：

```bash
[me@linuxbox ~]$ mv $filename ${filename}1
```

通过添加周围的大括号，shell 不再将尾随的 `1` 解释为变量名的一部分。

我们将借此机会向我们的报告中添加一些数据，即报告的创建日期和时间以及创建者的用户名：

```bash
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"

CURRENT_TIME=$(date +"%x %r %Z")

TIME_STAMP="Generated $CURRENT_TIME, by $USER"

echo "<HTML>
    <HEAD>
        <TITLE>$TITLE</TITLE>
    </HEAD>
    <BODY>
        <H1>$TITLE</H1>
        <P>$TIME_STAMP</P>
    </BODY>
</HTML>"
```
