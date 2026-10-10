
## 23.5 使用 read 语句进行输入

假设你通过输入以下命令行来运行脚本：

```
$ echo.args We like UNIX. (Return)
```

Shell 会将命令名称（"echo.args"）存储在参数 $0 中；它将参数 "We" 放入参数 $1；将 "like" 放入参数 $2，将 "UNIX." 放入参数 $3。由于这就处理了所有参数，其余的参数保持为空。然后脚本打印变量的内容：

```
echo.args We like UNIX.
```

如果用户输入了超过九个参数会怎样？位置参数 $* 包含所有参数 $1, $2, $3, ..., $9，以及这九个参数之外的任何参数。因此，我们可以重写 echo.args 以处理任意数量的参数：

```
#!/bin/sh
# Illustrate the use of positional parameters
echo $*
```

参数 $# 包含用户输入的参数量。我们可以再次修改脚本 echo.args 以使用此参数：

```
#!/bin/sh
# Illustrate the use of positional parameters
echo You typed $# arguments: $*
```

假设我们随后输入以下命令行

```
$ echo.args To be or not to be (Return)
```

计算机将回应

```
You typed 6 arguments: To be or not to be
```

> $* 不包含 $0，因此 echo.args 既不被计数也不被打印。

位置参数对于捕获命令行参数很有用，但它们有一个限制：一旦脚本开始运行，位置参数就不能用于从标准输入获取更多信息。为此，你必须使用 read 语句。让我们修改前面的程序以使用 read：

```
#!/bin/sh
# Illustrate the use of positional parameters, user-defined
# variables and the read command.
echo 'What is your name?'
read name
echo "Well, $name, you typed $# arguments:"
echo "$*"
```

在这个脚本中，`name` 是一个用户定义的变量。`read` 命令获取用户的响应并将其存储在 `name` 中。通过此修改，脚本 `echo.args` 的工作方式大致如下：

```
$ echo.args To be or not to be (Return)
```

Shell 脚本会通过提示你输入姓名来回应：

What is your name?

假设你输入

Rumpelstiltskin (Return)

计算机将回应

```
Well, Rumpelstiltskin, you typed 6 arguments:
To be or not to be
```

## 23.6 set 命令

你输入的位置参数有时被称为*只读变量*，因为当你向脚本输入参数时，shell 为你设置了它们的值。然而，你也可以使用 `set` 命令来设置它们的值。为了说明这一点，考虑以下 shell 脚本，我们假设它位于文件 `setdate` 中：

```
#!/bin/sh
# Demonstrate the set command
set `date`
echo "Time: $4 $5"
echo "Day: $1"
echo "Date: $3 $2 $6"
```

假设 `setdate` 已通过 `chmod` 命令被设为可执行，我们可以通过输入命令来运行该脚本

```
$ setdate (Return)
```

输出看起来会像这样：

```
Time: 10:56:08 EST
Day: Fri
Date: 13 Aug 1999
```

发生了什么？考虑以下命令行

```
set `date`
```

反引号运行 `date` 命令，产生的输出类似于：

```
Fri Aug 13 10:56:08 EST 1999
```

这不会出现在屏幕上。相反，**set** 命令捕获输出并将其存储在位置参数 **$1** 到 **$6** 中：

```
$1  contains  Fri
$2  contains  Aug
$3  contains  13
$4  contains  10:56:08
$5  contains  EST
$6  contains  1999
```

## 23.7 使用 expr 工具进行算术运算

Shell 并非为数值工作设计——如果你需要进行大量计算，应考虑使用 C、FORTRAN 或 Pascal。尽管如此，**expr** 工具可用于对整数执行简单的算术运算。（**expr** 不是一个 shell 命令，而是一个独立的 UNIX 工具；不过，它最常出现在 shell 脚本中。）要在 shell 脚本中使用它，你只需在表达式周围加上反引号。例如，让我们编写一个简单的脚本 **add**，用于将作为参数输入的两个数字相加：

```
#!/bin/sh
#  Add  two  numbers
sum=`expr  $1  +  $2`
echo  $sum
```

在这里，我们定义了一个变量 **sum** 来保存操作结果。（注意加号周围的空格，但等号周围没有。）要运行此脚本，我们可以输入以下行：

```
$  add  4  3<Return>
```

第一个参数 (4) 存储在 **$1** 中，第二个参数 (3) 存储在 **$2** 中。然后 **expr** 工具将这些量相加，并将结果存储在 **sum** 中。最后，**sum** 的内容在屏幕上回显：

```
7
$
```

**expr** 命令仅适用于整数（即整数）。它可以执行加法 (+)、减法 (-)、乘法 (*)、整数除法 (/) 和整数取模 (%)。

## 23.8 控制结构

通常，shell 按顺序处理脚本中的命令，按照它们在文件中书写的顺序一个接一个地处理。然而，通常你会希望改变命令的处理方式。你可能希望根据情况选择运行某个命令或另一个命令；或者你可能希望多次运行某个命令。

为了改变命令的正常顺序执行，shell 提供了多种控制结构。有两种*选择结构*，允许在替代命令之间进行选择：

- * if/then/elif/else/fi
- * case

有三种*重复或迭代结构*用于多次执行命令：

- * for
- * while
- * until

## 23.9 if 语句和 test 命令

if 语句允许你根据某些条件选择是否运行某个特定命令（或命令组）。这种结构的最简单版本具有通用形式

```
if conditional expression
then
    command(s)
fi
```

当 shell 遇到这样的结构时，它首先检查条件表达式是否为真。如果是，shell 运行在 then 和 fi（只是 if 反向拼写）之间发现的任何命令。如果条件表达式不为真，shell 跳过 then 和 fi 之间的命令。这是一个使用简单 if 语句的 shell 脚本示例：

```
#!/bin/sh
set 'date'
if test $1 = Fri
then
    echo "Thank goodness it's Friday!"
fi
```

在这里，我们在条件表达式中使用了 `test` 命令。表达式

```
test $1 = Fri
```

检查参数 `$1` 是否包含 `Fri`；如果包含，`test` 命令报告条件为真，并打印该消息。

`test` 命令可以执行多种测试；它所接受的一些参数如下所列：

| 参数 | 测试为真如果... |
| :--- | :--- |
| `-d file` | file 是一个目录 |
| `-f file` | file 是一个普通文件 |
| `-r file` | file 可读 |
| `-s file` | file 大小大于零 |
| `-w file` | file 可写 |
| `-x file` | file 可执行 |
| `n1 -eq n2` | 整数 n1 等于整数 n2 |
| `n1 -ge n2` | 整数 n1 大于或等于整数 n2 |
| `n1 -gt n2` | 整数 n1 大于整数 n2 |
| `n1 -le n2` | 整数 n1 小于或等于整数 n2 |
| `n1 -ne n2` | 整数 n1 不等于整数 n2 |
| `n1 -lt n2` | 整数 n1 小于整数 n2 |
| `s1 = s2` | 字符串 s1 等于字符串 s2 |
| `s1 != s2` | 字符串 s1 不等于字符串 s2 |

## 23.10 elif 和 else 语句

通过将 if 与 **elif**（“否则如果”）和 **else** 语句结合，我们可以使选择结构变得更加复杂。这是一个简单的例子：

```
#!/bin/sh
set 'date'
if test $1 = Fri
then
    echo "Thank goodness it's Friday!"
elif test $1 = Sat || test $1 = Sun
then
    echo "You should not be here working."
    echo "Log off and go home."
else
    echo "It is not yet the weekend."
    echo "Get to work!"
fi
```

在这里，首先测试第一个条件表达式以查看这一天是否是星期五。如果是，则打印消息“Thank goodness it's Friday!”，并且 shell 脚本结束。如果不是，则测试第二个条件表达式。注意，我们在这个表达式中使用了 OR 运算符 (||) 来测试这一天是否是星期六或星期日，在这种情况下，将打印第二组消息，脚本结束。否则，打印第三组消息。

我们可以通过包含更多 **elif** 子句来制作更复杂的选择结构。关于此类结构需要注意的重要事情是，只能选择其中一个选项；一旦选定，其余选项被跳过。

## 23.11 case 语句

Shell 提供了另一种选择结构，在某些 UNIX 系统上可能比 **if** 语句运行得更快。这就是 **case** 语句，它具有以下通用形式：

```
case word in
pattern1    command(s) ;
pattern2    command(s) ;
...
patternN    command(s) ;
endcase
```

**case** 语句将 word 与 pattern1 进行比较；如果匹配，shell 运行第一行上的命令(s)。否则，shell 逐个检查剩余的模式，直到找到一个与 word 匹配的模式；然后运行该行上的命令(s)。

