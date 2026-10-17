
此选项非常有用，因为在搜索 `"he"` 时；我们还会找到单词 `"the"` 的出现。`-w` 选项将搜索仅限制为匹配的单词，因此不会产生对 `"he"` 的匹配结果。

## 总结

在本章中，我们探索了 GNU/Linux shell 命令操作的一些基础知识。研究了标准输入和输出描述符（`stdin`、`stdout` 和 `stderr`），以及重定向和命令管道。我们还看了调用 shell 脚本的方法，包括将当前工作目录添加到默认搜索路径中。最后，我们演示了一些实用的 GNU/Linux 命令，包括 `tar`（文件存档）、`find`（文件搜索）、`grep`（字符串搜索）以及其他实用的文本处理命令（`out`、`paste` 和 `sort`）。

## 20 Bourne-Again Shell (bash)

- 本章内容
- Bash 脚本简介
- 脚本编写与交互式 Shell 使用
- 用户变量与环境变量
- Bash 中的算术运算
- Bash 中的测试、条件判断和循环
- 脚本输入与输出
- 有用脚本解析

## 引言

在本章中，我们将探索 Bourne-Again Shell（又称为 `bash`）中的脚本编程。`bash` 是 Linux 和其他 UNIX 系统上事实标准的命令和 shell 脚本语言。我们将研究 `bash` 的一些主要语言特性，包括变量、算术运算、控制结构、输入输出和函数创建。这遵循书中所有其他脚本章节的流程，让读者能够轻松理解所涉及语言的相似之处。

## 准备工作

在开始使用 `bash` 编写脚本之前，让我们来看运行 `bash` 脚本所需的某些准备工作。你可以通过查询 `SHELL` 环境变量来判断当前正在使用的 shell：

```bash
$ echo $SHELL
```

此命令的结果是你当前正在使用的 shell 的路径。

`wc` 工具对于统计文件中的字符数、单词数或行数非常有用。
以下示例说明了 `wc` 工具的各种用法。

```
wc -m file.txt # Count file.txt 中的字符
wc -w file.txt # 统计 file.txt 中的单词
wc -l file.txt # 统计 file.txt 中的行数
```

这三者都可以通过累计参数输出，例如：
无论标志的顺序如何，计数输出的顺序总是行、然后是单词，最后是字符。

```bash
wc -l -w -m file.txt
```

## grep

`grep` 命令允许在一个或多个文件中搜索指定的模式。`grep` 命令的格式可以很复杂，但简单的示例非常有用。让我们来看几个简单的示例并讨论它们实现的功能。
在最简单的形式，我们可以在单个文件中搜索特定的搜索字符串，例如：

```
grep "the" file.txt
```

此示例的结果是向标准输出（`stdout`）打印每个包含单词 `"the"` 的行。与其指定单个文件，不如我们使用通配符来检查多个文件，例如：

```
grep "the" *.txt
```

在这种情况下，当前子目录下所有以 `.txt` 结尾的文件都会被检查是否包含搜索字符串。

### 344 GNU/Linux 编程

当使用通配符时，找到搜索字符串的文件名将在输出到标准输出的每一行之前输出。

如果找到搜索字符串的文件位置很重要，可以使用 `-n` 选项。

```bash
grep -n "the" *.txt
```

每次找到搜索字符串，文件名和该字符串所在的行号都会在行之前输出。如果我们只关心文件中是否找到了特定的字符串，可以使用 `-l` 选项仅输出文件名，而不是找到字符串的行内容：

```bash
grep -l "the" *.txt
```

当我们专门在文件中搜索单词时，`-w` 选项可以帮助将搜索限制为整个单词：

```bash
grep -w "he" *.txt
```

此选项非常有用，因为在搜索 `"he"` 时；我们还会找到单词 `"the"` 的出现。`-w` 选项将搜索仅限制为匹配的单词，因此不会产生对 `"he"` 的匹配结果。

## 总结

在本章中，我们探索了 GNU/Linux shell 命令操作的一些基础知识。研究了标准输入和输出描述符（`stdin`、`stdout` 和 `stderr`），以及重定向和命令管道。我们还看了调用 shell 脚本的方法，包括将当前工作目录添加到默认搜索路径中。最后，我们演示了一些实用的 GNU/Linux 命令，包括 `tar`（文件存档）、`find`（文件搜索）、`grep`（字符串搜索）以及其他实用的文本处理命令（`out`、`paste` 和 `sort`）。

```
$ ./env.sh
欢迎运行 linux-gnu 的家 shell。
您是用户 mtj，您的主目录是 /home/mtj。
本系统运行的 bash 版本为 2.05b.0(1)-release。
此脚本已运行了 1 秒(s)。
$
```

注意，我们在脚本中添加了一个无用的 `sleep` 调用（为了让它暂停一秒），这样我们就可以看到 `SECONDS` 变量正在工作。同样注意，`SECONDS` 变量可以从命令行输出，但该值代表 shell 运行的秒数。
Bash 提供了许多其他特殊变量。其中一些重要的变量如表 20.1 所示。可以通过 `echo` 它们来了解其格式。

# 表 20.1 有用的环境变量

| 变量 | 描述 |
| :--- | :--- |
| `$PATH` | 二进制执行文件的默认路径 |
| `$PWD` | 当前工作目录 |
| `$OLDPWD` | 上一个工作目录 |
| `$PPID` | 解释器（或脚本）的进程 ID |
| `$#` | 参数个数 |
| `$0`, `$1`, `$2`, ... | 参数 |
| `$*` | 作为单个单词形式的所有参数 |

关于 `bash` 变量的最后一点，然后我们将转移到一些实际编程。例如，我们可以在 `bash` 中声明变量并提供某种形式的类型。我们可以声明一个常量变量（定义后无法更改），或者声明一个整数，甚至是一个范围超出脚本的变量。下面通过交互方式展示了这些整数的示例：

```bash
$ x=1
$ declare -r x
$ x=2
-bash: x: readonly variable
$ echo x
1
$ y=2
$ declare -i y
```

# 350 GNU/Linux 编程

```bash
$ echo sy
2
$ persist='PWD'
$ declare -x persist
$ export | grep "mtj"
declare -x persist="/home/mtj"
```

最后一项可能需要稍作讨论。在例例中，我们创建了一个变量 `persist` 并将当前的工作子目录赋值给它。我们声明了要在环境外部导出，这意味着如果是在脚本中执行，该变量在脚本完成后将仍然存在。这对于允许脚本修改环境或返回变量非常有用。

# 简单算术

我们可以对变量进行简单的算术运算，但它与我们刚刚回顾的普通赋值有所不同。考虑列表 20.3 中的源码。

列表 20.3 展示变量算术的简单脚本（位于光盘 `/source/ch20/arith.sh`）

```bash
1: #bin/bash
2:
3: x=10
4: y=5
5:
6: let sum=$x+$y
7: diff=$((x - $y))
8: let mul=$x*$y
9: let div=$x/$y
10: let mod=$x%y
11: let exp=$x**y
12:
13: echo "$x + $y = $sum"
14: echo "$x - $y = $diff"
15: echo "$x * $y = $mul"
16: echo "$x / $y = $div"
17: echo "$x ** $y = $exp"
18: exit
```

在第 3 行和第 4 行，我们创建了两个名为 `x` 和 `y` 的局部变量并为它们赋值。然后我们将使用两种不同的形式演示简单的数学求值。第一种形式使用 `let` 命令将求值后的表达式赋值给新变量。这种形式不允许出现空格。第二个示例使用了 `$( <expr> ))` 形式。注意，在这种情况下是允许出现空格的，这可能使表达式更易读。

## 位运算符

`bash` 中也提供了标准的位运算符。这些包括位左移 (`<<`)、位右移 (`>>`)、位与 (`&`)、位或 (`|`)、位取反 (`-`)、位非 (`!` - 注意：`bash`中通常指逻辑取反) 和位异或 (`^`)。下面的交互式会话演示了这些运算符：

```bash
$ a=4
$ let b="$a<<1"
$ echo $b
8
$ b=8
$ c=4
$ echo $((c|$d))
12
$ echo $((0xc^0x3))
15
$
```

## 逻辑运算符

在 `bash` 中也可以找到传统的逻辑运算符。这些包括逻辑与 (`&&`) 和逻辑或 (`||`)。下面的交互式会话演示了这些运算符：

```bash
$ echo $((2 && 0))
0
$ echo $((4 && 1))
1
$ echo $((3 || 0))
1
$ echo $((0 || 0))
0
```

在下一节中，我们将研究这些如何用于条件判断的决策点。

## 条件结构

Bash 提供了典型的条件构造。在本节中，我们将探索这些构造，并研究一些其他可用的条件表达式。

# 352 GNU/Linux 编程

## 条件

在本节中，我们将查看条件语句。`if/then` 构造在评估测试构造后提供一个决策点。测试构造返回一个值作为结果。测试构造的结果为零表示真（测试成功并执行后续命令），非零表示假（测试失败，执行 `else` 部分，如果存在）。让我们来看一个简单的示例来说明（见列表 20.4）。

# 列表 20.4 展示 if/then 的简单脚本（见列表 20.5）

```bash
1: #bin/bash
2:
3: a=1
4: b=2
5: if [ $a -eq $b ]
6:   then
7:     echo "equal"
8:   else
9:     echo "unequal"
10: fi
```

注意测试构造的结果为零表示真（测试成功并执行后续命令），非零表示假（测试失败，执行 `else` 部分，如果存在）。

# 列表 20.5 展示 if/then/elif 的简单脚本（位于光盘 `/source/ch20/cond.sh`）

```bash
1: #!bin/bash
2: str="ernie"
3: if [[ $str == "Ernie" ]]
4:   then
5:     echo "It's Ernie"
6: elif [[ $str == "oscar" ]]
7:   then
8:     echo "It's Oscar"
9:   else
10:    echo "It's someone else"
11: fi
```

在第 2 行创建字符串变量后，我们对常量字符串进行测试。=` 操作测试字符串相等。在第 9 行，我们看到了一种形式不同的 `if/then` 构造。由于它表示在一行内，因此使用分号来分隔各个命令。

### 表 20.2 整数比较

| 运算符 | 描述 |
| :--- | :--- |
| `-eq` | 等于 |
| `-ne` | 不等于 |
| `-gt` | 大于 |
| `-ge` | 大于等于 |
| `-lt` | 小于 |
| `-le` | 小于等于 |

### 表 20.3 字符串比较

| 运算符 | 描述 |
| :--- | :--- |
| `=` | 等于 |
| `==` | 等于 |
| `!=` | 不等于 |
| `<` | 字母序小于 |
| `>` | 字母序大于 |
| `-z` | 空 |
| `-n` | 非空 |

# 列表 20.7 使用文件测试运算符确定文件属性（位于光盘 `/source/ch20/fileatt.sh`）

```bash
1: #!bin/sh
2: thefile="test.sh"
3:
4: if [ -e $thefile ]
5:   then
6:     echo "File Exists"
7:
8:   if [ -f $thefile ]
9:     then
10:      echo "regular file"
11:  elif [ -d $thefile ]
12:    then
13:      echo "directory"
14:  elif [ -h $thefile ]
15:    then
16:      echo "symbolic link"
17:  fi
18:
19:  else
20:    echo "File not present"
21:  fi
```

```bash
if [ $file1 -nt $file2 ]
then
  echo "$file1 is newer than $file2"
elif [ $file1 -ot $file2 ]
then
  echo "$file1 is older than $file2"
fi
```

# 356 GNU/Linux 编程

文件测试运算符 `-nt` 测试第一个文件是否比第二个文件新，而 `-ot` 测试第一个文件是否比第二个文件旧。

如果你对测试的反向操作感兴趣，例如判断一个文件是否不是目录，可以使用 `!` 运算符。下面的代码段说明了这一点：

```bash
if [ -d $file1 ]
then
  echo "File is not a directory"
fi
```

需要注意的一个特殊情况是，当你根据给定测试结构的成功与执行单个命令时。考虑以下内容：

```bash
[ -r myfile.txt ] && echo "the file is readable."
```

测试成功（`myfile.txt` 可读），则执行随后的命令。测试与命令之间的逻辑与（AND）运算符确保了只有当初始测试结构为真时，才会执行随后的命令。如果测试结构为假，则该行的其余部分将被忽略。

这是对某些 `bash` 测试运算符的快速介绍。本章末的“资源”部分提供了进一步研究的信息。

## case 结构

让我们看看另一种条件结构，它在处理大量项目时比标准的 `if` 测试具有某些优势。`case` 命令允许使用整数或字符串的序列测试结构。考虑列表 20.8 所示示例。

> **列表 20.8** `case/esac` 结构的简单示例（位于 CD-ROM 的 `/source/ch20/case.sh`）

```bash
1:   #!/bin/bash
2:   var=2
3:
4:   case "$var" in
5:   0) echo "The value is 0";;
6:   1) echo "The value is 1";
7:   2) echo "The value is 2";
8:   *) echo "The value is not 0, 1, or 2"
9:   esac
10:
11:  exit
```

列表 20.8 显示的 `case` 结构说明了在多个值中进行整数测试。在第 4 行，我们使用 `$var` 建立 `case` 结构。在第 5 行，执行对 0 的测试，如果成功，则执行随后的命令。第 6 和第 7 行测试值 1 和 2。最后在第 8 行，默认的 `*` 表示如果所有之前的测试都失败，将执行此行。在第 9 行，`case` 结构关闭。

注意测试内部的命令列表以 `;;` 结尾。这告诉解释器 `case` 结构已结束，后续将是另一个 case 测试或 `case` 结构的关闭。注意 `case` 测试的顺序很重要。考虑如果第 8 行在最后一个测试之前会怎样。在这种情况下，默认项将始终成功，这并不是我们想要的。考虑列表 20.9 所示的脚本，它测试了范围 0-5 和 6-9。特殊形式 `[0-5]` 用于定义 0 到 5 之间（包含边界）的值范围。

# **列表 20.9** `case/esac` 结构的简单示例（位于 CD-ROM 的 `./source/ch20/case2.sh`）。

```bash
1: #!/bin/bash
2: var=2
3:
4: case $var in
5: [0-5]) echo The value is between 0 and 5 ;;
6: [6-9]) echo The value is between 6 and 9 ;;
7: *) echo It's something else...
8: esac
9:
10: exit
```

`case` 结构也可以用于测试字符类。列表 20.10 所示的脚本说明了字符测试。同时展示了范围拼接，这里 `[a-zA-Z]` 测试大小写字母字符。

# **列表 20.10** 阐明范围的 `case/esac` 结构的另一个示例（位于 CD-ROM 的 `./source/ch20/case3.sh`）。

```bash
1: #!/bin/bash
2:
3: char=f
4:
5: case $char in
6: [a-zA-Z]) echo An Anper or lower case character ;;
7: [0-9]) echo A number ;;
8: *) echo Something else ;;
9: esac
10:
11: exit
```

最后，也可以用 `case` 结构测试字符串。列表 20.11 显示了一个简单的示例。在这个示例中，对字符串进行了四种检查。注意在第 7 行，测试结构由两个不同的测试组成。如果名字是 Marc 或 Tim，则满足测试。在这种情况下我们使用了逻辑或（OR）运算符，这在 `case` 测试结构中是合法的。

列表 20.11 `case/esac` 结构的简单字符串示例（位于 CD-ROM 的 `/source/ch20/case4.sh`）

```bash
1: #!/bin/bash
2:
3: name=Tim
4:
5: case $name in
6: Dan ) echo It's Dan. ;;
7: Marc | Tim ) echo It's me. ;;
8: Ronald ) echo It's Ronald. ;;
9: *) echo don't know you. ;;
10: esac
11:
12: exit
```
