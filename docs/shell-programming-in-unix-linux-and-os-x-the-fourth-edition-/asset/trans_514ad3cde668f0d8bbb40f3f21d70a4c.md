
你可以通过将此命令序列放入一个文件——我们称之为 run——使其成为可执行文件，然后在想要打印提案的新副本时，只需键入 run 这个名字，从而节省一些输入：

```sh
$ cat run
tbl sys.caps | nroff -mm -Tlp | lp
$ chmod +x run
$ run
request id is laser1-15 (standard input)
$
```

（示例中的 request id 消息来自 lp 命令。）

对于下一个示例，假设你想编写一个名为 stats 的 shell 程序，它将打印日期和时间、当前登录用户数以及当前工作目录。你需要用来获取这些信息的三个命令序列是 date、who | wc -l 和 pwd：

```sh
$ cat stats
date
who | wc -l
pwd
$ chmod +x stats
$ stats                         Try it out
Wed Jul 10 11:55:50 EDT 2002
     13

/users/steve/documents/proposals
$
```

你可以在 stats 中添加一些 echo 命令，使输出信息更丰富一些：

```sh
$ cat stats
echo The current date and time is:
date
echo
echo The number of users on the system is:
who | wc -l
echo
echo Your current working directory is:
pwd
$ stats                         Execute it
The current date and time is:
Wed Jul 10 12:00:27 EDT 2002

The number of users on the system is:
     13

Your current working directory is:
/users/steve/documents/proposals
$
```

回想一下，不带任何参数的 echo 会输出一个空行。稍后你将看到如何将消息和命令输出显示在同一行，如下所示：

```
The current date and time is: Wed Jul 10 12:00:27 EDT 2002
```

## 注释

如果没有*注释*语句，shell 编程语言就不够完整。注释是你在程序中插入说明或注解的一种方式，这些内容对程序的执行没有任何影响。

每当 shell 遇到特殊字符 # 时，它会忽略从 # 开始到行尾的所有字符。如果 # 位于行首，则整行被视为注释。下面是有效注释的示例：

```
# Here is an entire commentary line
# who | wc -l      # count the number of users
#
# Test to see if the correct arguments were supplied
#
```

注释对于记录那些目的可能不明显或足够复杂以至于你可能会忘记它们为什么存在或做什么的命令或命令序列非常有用。明智地使用注释还有助于使 shell 程序更易于调试和维护——无论是对你，还是对可能需要维护你程序的其他人而言。

让我们回到 `stats` 程序，插入一些注释和空行以提高可读性：

```
$ cat stats
#
# stats -- prints: date, number of users logged on,
#                  and current working directory
#

echo The current date and time is:
date

echo
echo The number of users on the system is:
who | wc -l

echo
echo Your current working directory is:
pwd
$
```

额外的空行在程序空间方面消耗很少，但在程序可读性方面却增加很多。它们会被 shell 直接忽略。

## 变量

与几乎所有编程语言一样，shell 允许你将值存储在*变量*中。shell 变量以字母或下划线（_）字符开头，后跟零个或多个字母数字或下划线字符。

> **注意**
> 
> 因此，shell 变量名的正则表达式是 `[A-Za-z_][a-zA-Z0-9_]*`，对吗？

要将值存储到 shell 变量中，你需要写出变量名，后面紧跟等号 =，再紧跟要存储在变量中的值：

```
variable=value
```

例如，要将值 1 赋给 shell 变量 count，你只需编写

```
count=1
```

要将值 /users/steve/bin 赋给 shell 变量 my_bin，你编写

```
my_bin=/users/steve/bin
```

这里有几点很重要。首先，等号两侧不允许有空格。请记住这一点，特别是如果你曾经使用过其他编程语言，并且习惯于在运算符周围插入空格。在 shell 语言中，你不能加这些空格。

其次，与大多数其他编程语言不同，shell 没有*数据类型*的概念。无论你向 shell 变量赋什么值，shell 都会简单地将该值解释为字符串。因此，当你将 1 赋给变量 count 时，shell 只是将*字符* 1 存储在变量 count 中，而不会假设变量中存储的是整数值。

如果你习惯于使用 C、Perl、Swift 或 Ruby 等所有变量都必须*声明*的语言进行编程，那么你还需要进行另一项调整：由于 shell 没有数据类型的概念，变量在使用前不会被声明；当你想要使用它们时，直接为它们赋值即可。

shell 确实支持对包含有效数字字符串的 shell 变量执行整数运算，这是通过特殊的内置操作实现的，但即便如此，变量也会被不断求值以确保它是有效数字。

因为 shell 是一种解释性语言，你可以直接在终端上为变量赋值：

```sh
$ count=1                         Assign character 1 to count
$ my_bin=/users/steve/bin         Assign /users/steve/bin to my_bin
$
```

既然你现在已经知道如何为变量赋值，那这有什么用呢？问得好。

## 显示变量的值

echo 命令——我们已经用它来打印从标准输入接收的字符串等值——用于显示存储在 shell 变量中的值。要做到这一点，你只需编写

```
echo $variable
```

$ 字符对 shell 来说是一个特殊字符，当后跟一个或多个字母数字字符时尤其如此。如果 $ 后面跟着变量名，shell 会将其视为指示该变量中存储的值应在该位置进行替换。因此，当你输入

```
echo $count
```

shell 会将 $count 替换为其中存储的值；然后执行 echo 命令：

```
$ echo $count
1
$
```

请记住，shell 在执行命令*之前*进行变量替换（见图 4.1）。

![](img/29b87b4d3daf7eb41fe5066130730f4c_117_0.png)

图 4.1  `echo $count`

你可以同时替换多个变量的值：

```
$ echo $my_bin
/users/steve/bin
$ echo $my_bin $count
/users/steve/bin 1
$
```

在第二个示例中，shell 会替换 my_bin 和 count 的值，然后执行 echo 命令（见图 4.2）。

![](img/29b87b4d3daf7eb41fe5066130730f4c_117_1.png)

图 4.2  `echo $my_bin $count`

变量可以用于任何命令行上的任何位置，并会在调用特定命令之前由 shell 替换为其值，如下面的示例所示：

```text
$ ls $my_bin
mon
nu
testx
$ pwd
/users/steve/documents/memos
$ cd $my_bin
$ pwd
/users/steve/bin
$ number=99
$ echo There are $number bottles of beer on the wall
There are 99 bottles of beer on the wall
$
```

*我们在哪里？*

*切换到我的 bin 目录*

这里还有一些示例：

```text
$ command=sort
$ $command names
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
Tony
$ command=wc
$ option=-l
$ file=names
$ $command $option $file
        7 names
$
```

所以你看，甚至命令名也可以存储在变量中。由于 shell 在确定要执行的程序名及其参数之前执行替换，它会解析这一行

```text
$command $option $file
```

然后进行所有请求的替换，将实际调用的命令变为

```text
wc -l names
```

然后 shell 执行 wc，并传递两个参数 -l 和 names。

变量甚至可以赋值给其他变量，如下一个示例所示：

```text
$ value1=10
$ value2=$value1
$ echo $value2
```

