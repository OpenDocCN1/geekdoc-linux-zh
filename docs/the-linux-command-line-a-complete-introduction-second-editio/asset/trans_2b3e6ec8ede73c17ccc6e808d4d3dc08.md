

```
[me@linuxbox ~]$ echo yes
```

相比之下，下面这个命令：

```
[me@linuxbox ~]$ echo $foo1
```

会展开成这样：

```
[me@linuxbox ~]$ echo
```

空变量会展开为空！这会让需要参数的命令陷入混乱。下面是一个例子：

```
[me@linuxbox ~]$ foo=foo.txt
[me@linuxbox ~]$ foo1=foo1.txt
[me@linuxbox ~]$ cp $foo $fool
cp: missing destination file operand after `foo.txt'
Try `cp --help' for more information.
```

我们为两个变量 foo 和 foo1 分配了值。然后执行 cp 但拼错了第二个参数的名称。展开后，cp 命令只收到一个参数，而它需要两个。

关于变量名的规则如下：

- 变量名可以由字母数字字符（字母和数字）和下划线字符组成。
- 变量名的第一个字符必须是字母或下划线。
- 不允许使用空格和标点符号。

单词“变量”意味着一个会变化的值，在许多应用中，变量就是这样使用的。然而，在我们的应用中，变量 title 被用作常量。常量就像变量一样，它有名称并包含一个值。不同之处在于常量的值不会改变。在执行几何计算的应用中，我们可能会将 π 定义为常量并赋值为 3.1415，而不是在整个程序中直接使用该数字。shell 并不会区分变量和常量；它们主要为了程序员的方便。一个常见的约定是使用大写字母来表示常量，而小写字母用于真正的变量。我们将修改脚本以符合这一约定：

```
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"

echo "<html>
    <head>
        <title>$TITLE</title>
    </head>
    <body>
        <h1>$TITLE</h1>
    </body>
</html>"
```

我们还借此机会通过添加 shell 变量 HOSTNAME 的值来美化标题。这就是机器的网络名称。

## NOTE

*shell 实际上确实提供了一种通过使用带有 -r（只读）选项的 declare 内置命令来强制常量不可变的方式。如果我们这样为 TITLE 赋值：*

```
declare -r TITLE="Page Title"
```

*shell 将会阻止对 TITLE 的任何后续赋值。这一特性很少使用，但在非常正式的脚本中存在。*

## Assigning Values to Variables and Constants

这里是我们关于展开的知识真正开始发挥作用的地方。正如我们所见，变量的赋值方式如下：

variable=value

其中 variable 是变量名，value 是一个字符串。与某些其他编程语言不同，shell 不关心分配给变量的数据类型；它将所有数据都视为字符串。你可以通过使用带有 -i 选项的 declare 命令来强制 shell 将赋值限制为整数，但与将变量设为只读一样，这很少被执行。

请注意，在赋值中，变量名、等号和值之间不能有空格。那么值可以包含什么呢？它可以包含任何可以展开为字符串的内容。

```
a=z                  # Assign the string "z" to variable a.
b="a string"        # Embedded spaces must be within quotes.
c="a string and $b" # Other expansions such as variables can be
                      # expanded into the assignment.
d="$(ls -l foo.txt)" # Results of a command.
e=$(($5 * 7))         # Arithmetic expansion.
f="\t\ta string\n" # Escape sequences such as tabs and newlines.
```

可以在单行上进行多个变量赋值。

```
a=5 b="a string"
```

在展开期间，变量名可以被可选的大括号 {} 包围。这在变量名因其周围上下文而变得模糊时很有用。这里，我们尝试使用变量将文件 myfile 的名称更改为 myfile1：

```
[me@linuxbox ~]$ filename="myfile"
[me@linuxbox ~]$ touch "$filename"
[me@linuxbox ~]$ mv "$filename" "$filename1"
mv: missing destination file operand after `myfile'
Try `mv --help' for more information.
```

此尝试失败，因为 shell 将 mv 命令的第二个参数解释为一个新（且为空）的变量。问题可以通过以下方式克服：

```
[me@linuxbox ~]$ mv "$filename" "${filename}1"
```

