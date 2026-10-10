

`who` 命令显示当前登录的账户以及用户登录系统的时间。

### pwd
它应该按预期工作。

图片：脚本中的 who 命令

> *注意：* 顶部以注释开头的文件被指定为脚本。请注意颜色

你也可以使用绝对路径或相对路径。
接下来你需要做的是更改权限。为什么？让我们创建一个文件并检查权限。

```
jan@jan-virtual-machine:~/Desktop$ ls -l Myscript
-rw-r--r-- 1 jan jan 137 Sep 23 17:29 Myscript
```

根据结果，执行此文件的权限不足。系统将其视为脚本，但未修改权限。这取决于用户。
为了提供执行权限，可以使用 `chmod` 命令。
`chmod u+x Myscript`

```
jan@jan-virtual-machine:~/Desktop$ ls -l Myscript
-rw-r-xr-x 1 jan jan 137 Sep 23 17:29 Myscript
```

一旦此步骤完成，脚本即可准备执行。

```
jan@jan-virtual-machine:~/Desktop$ ./Myscript
jan        :0           2019-09-21 05:09 (:0)
/home/jan/Desktop
```

如果你想显示文本指南、环境变量输出等，可以使用 `echo` 命令。我们在之前的课程中学过环境变量。

## 命令别名

使用命令别名可以节省大量时间。要定义别名，必须进行简单的赋值。

语法：`alias=command(s)`

示例：
- `alias L="ls -al"`
- `alias search=grep`

## 命令替换

也可以将某个命令的输出用作变量的输入。这是一个很棒的功能，可以继续脚本并使用动态数据执行它。

为了实现这一点，必须使用 `$()`。

示例：`user_name=$(USERNAME)`

示例脚本：

```bash
#!/bin/bash
user_name=$(who)
echo "Your username is :" $user_name
```
```
jan@jan-virtual-machine:~/Desktop$ ./MyScript
"Your username is :" jan : 0 2019-09-24 03:42 (:0)
```

## 创建文件

另一个很棒的功能是你可以输出结果。你甚至可以根据需要为文件命名。这在下一个示例中进行了说明。

```bash
#!/bin/bash
mydate=$(date +%Y%m%d)
echo "Today is :" $mydate
who > log.$mydate
ls -l log.$mydate
```
```
jan@jan-virtual-machine:~/Desktop$ ./MyScript
"Today is :" 20190924
-rw-r--r-- 1 jan jan 44 Sep 24 06:19 log.20190924
```

这里，我们创建一个日期并对其进行格式化。`%Y` 是 YYYY 格式的年份。月份是数字格式（例如，09），日期也是数字格式。输出类似于 YYYYMMDD。输出被存入变量。然后我们 `echo` 该变量。最后，我们使用 `who` 命令并使用重定向运算符 `>` 将其输入重定向到新文件。文件名创建为“log”.YYYYMMDD。这就是我们创建日志以保留记录的方式。如果脚本在第二天运行，文件名将是 `log.20190925`。

重定向是一个极其有用的功能。相反于使用像 `touch` 这样的命令，你可以将输出重定向到文件。然而，你甚至可以使用 `touch` 命令从脚本创建文件。例如，

```
#!/bin/bash
mydate=$(date +%Y%m%d)
echo "Today is: "$mydate
touch log.$mydate #Creates a file and name the first part log and later using our variable
who >> log.$mydate #Append the output of 'who' command to the file.
```

![](img/e3fe187ed34a3465fc5a2628f88b7166_101_0.png)

> **提示：** `>>` 运算符用于将条目追加到文件。这是一个极其有用的命令。

你还可以反向我们使用 `>` 运算符执行的过程。这被称为输入重定向。例如，我们可以将文件的条目获取到一个新变量或命令中。以下示例详细说明了这一点。

```
#!/bin/bash
wc < log.20190924
# wc is a new command to you. It counts the number of lines, words and characters.
```

```
jan@jan-virtual-machine:~/Desktop$ ./MyScript
1 5 44
```

最后，我们将研究 `<<` 运算符。这被称为内联输入运算符。
示例：`wc << lastLine`

```
jan@jan-virtual-machine:~/Desktop$ wc << lastLine
> test
> test2
> test3
> lastline
3 3 17
```

正如你所注意到的，直到 `lastLine` 作为文本输入被输入之前，它捕获了用户输入。

其他示例：
将错误和标准输出重定向到同一个文件。你可以使用以下命令。
示例：`ls Test Test2 Test3 > dirlist 2>&1`
这里，我们尝试列出 Test 目录的属性。记住，`ls` 命令支持多个文件或目录名称。然后它列出每个文件或目录的属性。`Test` 和 `Test2` 目录在我的桌面上。`Test3` 目录不存在。我将此命令的输出以及错误重定向到一个名为 `dirlist` 的新文件。

```
jan@jan-virtual-machine:~/Desktop$ ls Test Test2 Test3 > dirlist 2>&1
jan@jan-virtual-machine:~/Desktop$ cat dirlist
ls: cannot access 'Test3': No such file or directory
Test:
File5.txt
Test2:
File6.txt
```

## 标准文件描述符

我们再次回顾文件描述符。
标准输入 - 0: STDIN
标准输出 - 1: STDOUT
标准错误 - 2: STDERR

第一个是标准输入，接下来是标准输出和标准错误。数值是文件描述符。

除了这些技术之外，管道在脚本中被广泛使用。

## 管道

当需要一个命令的输出作为另一个命令的输入时，管道是有用的。这是我们到目前为止学过的。使用的运算符是 `|`。

示例：

```
#!/bin/bash
cat employee.txt | sort -nr -k 2
```
# 我们将获得的重定向文件条目重定向到 sort 函数。它按数值排序，逆序排列并按列 ID（第 2 列）排序。

![](img/e3fe187ed34a3465fc5a2628f88b7166_103_0.png)

## 脚本构建中的数学运算

任何脚本都可以用于执行某些计算。Linux 中有一些内置命令。我们来看看命令 `expr`。它代表表达式。这些是 `expr` 命令的运算符。

| 运算符 | 描述 |
| :--- | :--- |
| ARG1 \| ARG2 | 如果 ARG1 既不是空也不是 0，则为 ARG1，否则为 ARG2 |
| ARG1 & ARG2 | 如果两个参数都不是空或 0，则为 ARG1，否则为 0 |
| ARG1 < ARG2 | ARG1 小于 ARG2 |
| ARG1 <= ARG2 | ARG1 小于或等于 ARG2 |
| ARG1 = ARG2 | ARG1 等于 ARG2 |
| ARG1 != ARG2 | ARG1 不等于 ARG2 |
| ARG1 >= ARG2 | ARG1 大于或等于 ARG2 |
| ARG1 > ARG2 | ARG1 大于 ARG2 |
| ARG1 + ARG2 | ARG1 和 ARG2 的算术和 |
| ARG1 - ARG2 | ARG1 和 ARG2 的算术差 |
| ARG1 * ARG2 | ARG1 和 ARG2 的算术积 |
| ARG1 / ARG2 | ARG1 除以 ARG2 的算术商 |
| ARG1 % ARG2 | ARG1 除以 ARG2 的算术余数 |
| STRING : REGEXP | REGEXP 在 STRING 中的锚定模式匹配 |
| match STRING REGEXP | 与 STRING : REGEXP 相同 |
| substr STRING POS LENGTH | STRING 的子字符串，POS 从 1 开始计数 |
| index STRING CHARS | 在 STRING 中找到任何 CHARS 的索引，或 0 |
| length STRING | STRING 的长度 |
| + TOKEN | 将 TOKEN 解释为字符串，即使它是像 'match' 这样的关键字或像 '/' 这样的运算符 |

图片：expr 运算符

> 注意：虽然这是一个有用的命令，但在某些情况下其操作有些令人困惑。

### 示例

```
jan@jan-virtual-machine:~/Desktop$ expr 1+1
1+1
jan@jan-virtual-machine:~/Desktop$ expr 1 + 1
2
jan@jan-virtual-machine:~/Desktop$ expr 2 - 1
1
jan@jan-virtual-machine:~/Desktop$ expr 2 * 2
expr: syntax error
jan@jan-virtual-machine:~/Desktop$ expr 2 \* 2
4
jan@jan-virtual-machine:~/Desktop$ expr 6 / 3
2
```

> 注意：`2 * 2` 表达式返回语法错误。我们必须使用转义字符来解决这个问题。

与其使用 `expr` 命令，使用括号更方便。

```
#!/bin/bash
var1=2
var2=6
var3=3
var4=$(expr $var1 \* $var2)
echo $var4
var5=[ $(($var1 * $var2))/$var3]
echo $var5
```
```
jan@jan-virtual-machine:~/Desktop$ ./Myscript
12
4
```

## Bash 计算器

当你想要执行更复杂的数学函数时，有一个内置的 bash 工具可以执行此操作。它就是 bash 计算器。命令是 `bc`。

```
jan@jan-virtual-machine:~/Desktop$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
quit
```

> 提示：要退出此工具，请输入 `quit` 并按回车。在 `bc` 中，你可以执行数学运算。

Bash 计算器支持以下内容。
- 数值（整数和浮点数）。
- 变量。
- 表达式。

