
#

`PATH=$PATH:$(pwd)`

```
因此，变量 `PATH` 被赋值了它之前的内容、一个冒号；最后，通过命令替换，赋值了 `pwd` 命令的结果。接下来的测试运行显示，只有当在前面加点启动 `addpwd` 时，当前 shell 中 `PATH` 变量的内容才会改变。（在第一次调用 `addpwd` 时启动的 shell 内部，`PATH` 显然改变了——但这种更改在 `addpwd` 运行期间有效）。
```

```
user$ echo PATH

/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:sbin:

/usr/bin/X11:/usr/bin/bin:/usr/openbin/bin:/usr/games:

user$ ./addpwd

user$ echo PATH

/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:sbin:

/usr/bin/X11:/usr/bin/bin:/usr/openbin/bin:/usr/games::/home/mk/book
```

## shell 预定义的变量

在 shell 程序内部，可以访问 `bash` 预定义的几个变量。这些变量不能通过赋值更改；它们只能读取。变量名由各种特殊字符组成。在下面的表中，变量用其前置的 `$` 符号标出。

| 变量 | 描述 |
| :--- | :--- |
| `$?` | 上一个命令的返回值 |
| `$!` | 最近启动的后台进程的 `PID` |
| `$$` | 当前 shell 的 `PID` |
| `$0` | 当前执行的 shell 脚本的文件名（或指向该文件的符号链接名） |
| `##` | 传递给 shell 程序的参数数量 |
| `$1` 到 `$9` | 参数 `1` 到 `9` |
| `$*` 或 `$@` | 传递的所有参数总和 |

关于这些变量应用的额外说明：`$0` 到 `$9`、`##` 和 `$*` 用于评估传递给批处理程序的参数。本章中的几乎每个示例脚本都展示了它们的用法。

## bash 编程

与参数评估相关的另一个有趣的命令是 `bash` 命令 `shift`。该命令将传递的参数通过 `$1` 到 `$9` 九个变量进行移动。当你执行 `shift 9` 时，传递给程序的前九个参数将丢失；作为交换，现在可以轻松访问接下来的九个参数；每次执行 `shift` 会将参数列表向前移动一位。

`$?` 可以用于构建条件，以使程序的后续过程取决于最后处理的一个命令的结果。原则上，也可以在 `if` 中直接指定一个命令作为条件。变量 `$$` 的优点在于它能防止指令变得过长且不清晰（见第 416 页）。

变量 `$$` 包含 `PID`（进程标识符）。这个数值被 Linux 内部用于进程管理。`PID` 是唯一的，也就是说，在整个系统中，没有其他进程具有相同的数字。由于这个原因，`PID` 对于创建临时文件特别有用。例如，你可以使用 `ls > tmp.$$$..nn` 来存储文件 `$tmp.nn` 中所有文件的列表。即使同一个批处理文件在另一个终端同时运行，临时文件之间也不会发生命名冲突，因为两个 shell 具有不同的 `PID`。

## 参数替换

在“参数替换”标题下，`bash` 提供了几个命令来处理变量中的字符字符串。这种替换机制的语法是 `${var_pattern}`，其中 `_` 代表一个或两个特殊字符，用于指定替换命令的类型。请注意，指定变量名时不带前面的 `$`。但是，如果需要从变量中读取模式，则 `$` 字符必须跟在变量前面。

```
${var=default}
```

如果变量为空，该构造将产生默认设置 `a`，否则它将产生变量的内容。变量不会被改变。

```
${var:=default}
```

如上所述，但如果变量为空，则会同时更改变量的内容。

```
${var:+new}
```

如果变量为空，则它不会被改变。如果它已经被占用，则用当前内容替换为新设置。该构造返回变量的内容。

```
${var?error_message}
```

如果变量为空，则会显示变量名和错误信息，然后终止 shell 程序。否则，该构造返回变量的内容。

```
${#var}
```

返回变量中的字符数（如果变量为空，则为 `0`）。变量不会被改变。

## Shell 程序中的变量管理

`$(var*pattern)` 将变量内容的开头与指定的模式进行比较。如果识别模式，该构造返回变量的内容减去匹配搜索模式的最短文本。如果未找到模式，则返回变量的所有内容。在搜索模式中，可以使用通配符构建文件名（`*`、`?`、`[abc]`）。在任何情况下都不会更改变量：

```
user$ dat=/home/mk/book/book.tar.gz

user$ echo ${$(dat*/)}home/mk/book/book.tar.gz

user$ echo ${$(dat.*)}tar.gz
```

`$(var#pattern)` 与上所述，但现在消除了匹配模式的最长字符字符串：

```
user$ dat=/home/mk/book/book.tar.gz

user$ echo ${$(dat##)}book.tar.gz

user$ echo ${$(dat##.*)}gz
```

`$(varXpattern)` 与上所述，但模式匹配现在发生在变量的末尾。从变量末尾消除最短的字符字符串。变量本身保持不变：

```
user$ dat=/home/mk/book/book.tar.gz

user$ echo ${$(dat**/)}/home/mk/book

user$ echo ${$(datX.*)}/home/mk/book/book.tar
```

`$(var##pattern)` 与上所述，但消除了匹配模式的最长字符字符串：

```
user$ dat=/home/mk/book/book.tar.gz

user$ echo ${$(dat##*/)}

-- 输出 --

user$ echo ${$(dat##.*)}/home/mk/book
```

> 在第 421 页你会找到一个示例，它大量使用了上述引入的替换命令，用于复制或重命名组文件（`regmv *.ps *.eps`）。

# BASH 编程

```
$($!var)
```

产生变量 `var` 中包含的字符字符串名称的变量的内容。

```
user$ abc=123*

user$ efg=abc

user$ echo $($!efg)

123
```

> 注意：`$(!var)` 语法仅在 `bash` 2 版本及以上版本中允许。如果在旧版本的 `bash` 中，你想要确定一个在另一个变量中指定的变量的内容，你必须使用以下语法（该语法在版本 2 中也是允许的）：

```
user$ eval var2=\$(var)
```

# 使用 read 读取变量

你可以使用 `read` 命令在 shell 程序的执行期间接受输入。通常，你首先调用 `echo` 来显示一段短文本，告诉用户你期望输入什么（例如：`y/n`、数值等）。当你使用选项 `-n` 选项时，输入将直接紧跟在 `echo` 文本之后开始，而不是在下一行。在执行随后的 `read` 命令期间，`bash` 会等待用户输入一行内容并按回车键结束。

在下面的示例程序中，`while` 循环将执行，直到变量 `a` 中的字符字符串不再为空。一次测试运行了该微型程序的功能：

```
$user$ readvar

Enter a number: a

Invalid input, please try again

Enter a number: 12

$ readvar

: a

12
```

在通过 `read` 进行首次输入后，如果出现了不是数字、负号或空格的字符，则将通过参数替换删除变量的全部内容。这种检查显然不是完美的（字符串 `"12-34-5"` 和 `"12 34"` 是不合法的），但效率相当。关于 `while` 的信息可以查看第 419 页。

```bash
#! /bin/sh

# readvar: 读取数值

a=

while [ -z "$a" ]; do

echo -n "Enter a number: "

read a
```

```bash
a=$a#*[0-9,,'-]* # 消除包含 0-9、负号

# 或空格以外字符的字符字符串
```

```bash
if [ -z "$a" ]; then

    echo "Invalid input, please try again"

fi

echo $a
```
