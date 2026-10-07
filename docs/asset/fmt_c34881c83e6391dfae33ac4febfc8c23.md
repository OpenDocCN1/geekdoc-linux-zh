
环境变量不能是只读的。

## 17.3.6 从标准输入读取

到目前为止，我们展示了如何在命令行静态地或通过赋值语句为 shell 变量赋值。如果你想写一个交互式 shell 脚本来提示用户进行键盘输入，你需要使用 `set` 命令将用户输入存储在 shell 变量中。

## 562 第 17 章 简介 TC Shell 编程

到目前为止，我们展示了如何在命令行静态地或通过赋值语句为 shell 变量赋值。如果你想写一个交互式 shell 脚本来提示用户进行键盘输入，你需要使用 `set` 命令将用户输入存储在 shell 变量中。

## 564 第 17 章 TC Shell 编程入门

在本节课程之后，我们将使用 `cmdargs_demo` 文件中的 shell 脚本来展示你如何如何使用这些变量。

```bash
% cat cmdargs_demo

#!/bin/tcsh

echo "The command name is: $0"

echo "The number of command line arguments are $#argv"

echo -n "The values of the command line arguments are: "

echo "$1 $2 $3 $4 $5 $6 $7 $8 $9"

echo "Another way to display values of all of the arguments: $argv[*]"

exit 0
```

```bash
% cmdargs_demo a b c d e f g h i

The command name is: cmdargs_demo.

The number of command line arguments are 9.

The values of to display values of all of the arguments are: a b c d e f g h i.

Another way to display values of all of the arguments: a b c d e f g h i.
```

```bash
% cmdargs_demo One Two Three Four 5 6

The command name is: cmdargs_demo.

The number of command line arguments are 6.

The values of the command line arguments are: One Two Three Four 5 6 .

Another way to display values of all of the arguments: One Two Three Four 5 6. 

%
```

尽管 shell 同时维护多达九个命令行参数，但你也可以编写接受超过九个参数的脚本。要实现这一点，可以使用 `shift` 命令。默认情况下，该命令会将命令行参数向左移动一位，使得 `$2` 变为 `$1`， `$3` 变为 `$2`，且 `$1` 被移出。一旦移出，参数将无法恢复到原始值。可以通过作为命令的参数来指定一次移动多个位置。以下是该命令的简要描述。

| shift [variable] | |
| :--- | :--- |
| | 将 'variable' 中的单词向左移动一位；如果未指定变量名，则默认为命令行参数 |

## 565 向 Shell 脚本传递参数

`shift_demo` 文件中的脚本展示了 `shift` 命令在隐式变量 'variable'（即命令行参数）下的语义。

`shift` 命令会将第一个参数移出，并将剩余参数向左移动一位。`echo` 命令分别用于显示程序名、所有位置参数 (`$argv[*]`) 以及前三个位置参数的值。执行结果一目易见。

```bash
% shift_demo

#!/bin/tsh

echo "The name of the program is $0"

echo "The arguments are: $argv[*]."

echo "The first three arguments are: $1 $2 $3"

shift

echo "The name of the program is $0"

echo "The arguments are: $argv[*]."

echo "The first three arguments are: $1 $2 $3"

exit 0

% shift_demo 1 2 3 4 5 6 7 8 9 10 11 12

The program name is shift_demo.

The arguments are: 1 2 3 4 5 6 7 8 9 10 11 12.

The first three arguments are: 1 2 3.

The program name is shift_demo.

The arguments are: 2 3 4 5 6 7 8 9 10 11 12.

The first three arguments are: 2 3 4.
```

位置参数的值可以通过使用 `set` 命令并将 `argv` 作为其变量参数来更改。该命令最有效的方法是结合命令替换使用。以下是该命令的简要描述。

| 语法: | set argv = [argument-list] |
| :--- | :--- |
| **目的:** | 将位置参数的值设置为 'argument-list' 中的参数 |

## 566 第 17 章 TC Shell 编程入门

以下是该命令的一个简单交互式用法。执行 `date` 命令显示输出包含六个字段。`set argv = $date` 命令将位置参数设置为 `date` 命令的输出。具体来说， `$argv[1]` 被设置为 `Sat`， `$argv[2]` 设置为 `Mar`， `$argv[3]` 设置为 `3`， `$argv[4]` 设置为 `17:12:37`， `$argv[5]` 设置为 `PST`，而 `$argv[6]` 设置为 `2001`。`echo` 命令显示所有位置参数的值。第三个 `echo` 显示常用格式的日期。

```bash
% date

Sat Mar 3 17:12:37 PST 2001

% set argv = "date"

% echo argv[*]

Sat Mar 3 17:12:59 PST 2001

% echo "$argv[2] $argv[3], $argv[6]"
```

`set_demo` 脚本展示了该命令的另一种用法。当带有文件参数运行脚本，它会生成文件名和文件的 inode 节点（以字节计）。使用 `set` 命令将 `ls -il` 的输出赋值为位置参数 `$argv[1]` 到 `$argv[9]` 的新值。我们提供了 `ls -il` 命令的输出，以防你忘记该命令的格式。

```bash
% set_demo

!/bin/tcsh

set filename = $argv[1]

set argv = `ls -il $filename`

echo "The command line arguments are: echo $argv[*]"

set inode = $argv[1]

echo "The command line arguments are: $argv[*]"

echo "Inode: $argv[1]"

echo "Size: $argv[2]"

exit 0
```

## 程序控制流命令 569

```
Syntax: if (expression) then then-command-list [else if (expression) then then-command-list ... else else-command-list] 
if
```

**目的：** 实现双向或多路分支

在这里，“expression” 是一系列命令列表。'expression' 的执行返回真（成功）或假（失败）的状态。单词 **then** 必须与单词 if 出现在同一行；否则，你将收到错误信息 if: **Empty** if。我们将通过展示 if 语句的三个版本，来讨论 if 语句的完整语法和语义。if 语句最基本的用法是不带任何可选功能的，其语句的语法如下，该语法通常用于双向分支。

```
Syntax: if (expression) then then-commands endif
```

**目的：** 实现双向分支

如果 'expression' 为真，则执行 'then-commands'；否则，执行 **endif** 之后的命令。该语句的语义如图 17.1 所示。

你可以使用许多运算符来构造表达式，用于测试文件、测试和比较整数以及字符串，并逻辑上连接两个或多个表达式以形成复杂的表达式。表 17.4 描述了可以构造表达式的运算符及其含义。与文件相关的运算符按其优先级（从高到低）列出：括号、算术、移位、关系、位运算和逻辑。==、!=、= 和 ~ 操作将其参数作为字符串进行比较；所有其他均对数字操作。

## 570 第 17 章 TC Shell 编程入门

![](img/d16a56b1b2a540facbf3aae233584428_591_0.png)

图 17.1 if-then-endif 语句的语义

我们使用上述 if 命令的语法来修改 set-demo 文件中的脚本，使其仅接受一个命令行参数，并检查该参数是文件还是目录。如果运行脚本时没有命令行或多于一个命令行参数，或者命令行参数不是普通文件，则脚本将返回错误信息。脚本文件名为 if_demol。

```
# cat if_demol

#!/bin/tcsh

if ( ($argv == 0) || ($argv > 1) ) then
    echo "Usage: $0 ordinary_file"
    exit 1
endif

if ( -f argv[1] ) then
    set filename = $argv[1]
    set fileinfo = `ls -il $filename`
    set inode = $fileinfo[1]
    set size = $fileinfo[5]
    echo "Name\tinode\tSize"
    echo "$filename\tinode\tsize"
    exit 0
endif
```

## 表 17.4 用于构造表达式的 TC Shell 运算符

| 运算符 | 功能 | 运算符 | 功能 |
| :--- | :--- | :--- | :--- |
| 括号 () | 改变计算顺序 | 关系运算符 | > 大于<br>< 小于<br>=> 大于<br<= 小于<br>!= 不相等（字符串比较）<br>== 等于（字符串比较） |
| 一元运算符 | - 一元负号<br>- 取反码<br>- 逻辑非 (NOT) | 位运算符 | & 与 (AND)<br>\| 异或 (XOR) |
| 算术运算符 | % 取余<br>/ 除以<br>* 乘<br>- 减 | 逻辑运算符 | && 与 (AND)<br>|| 或 (OR) |

移位运算符 >> 右移
<< 左移

| 运算符 | 功能 | 运算符 | 功能 | 运算符 | 功能 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| -b file | 若 'file' 是块设备文件 | -c file | 若 'file' 是字符设备文件 | -d file | 若 'file' 是目录 |
| -e file | 若 'file' 存在 | -f file | 若 'file' 是普通文件 | -l file | 若 'file' 是符号链接 |
| -o file | 若用户拥有 'file' | -r file | 若 'file' 可读 | -u file | 若 'file' 设置了 SUID 位 |
| -w file | 若 'file' 可写 | -x file | 若 'file' 可执行 | -z file | 若 'file' 长度为 0 字节 |

## 572 第 17 章 TC Shell 编程入门

```
echo "$0: argument must be an ordinary file"
exit 1

% if_demol

Usage: if_demol ordinary_file

% if_demol lab3 lab4

Usage: if_demol ordinary_file

% if_demol dirl

if_demol: argument must be an ordinary file

% if_demol lab3
```

在前面的脚本中，if 语句的第一版本包含一个复合表达式，如果你在运行脚本时没有命令行参数或多于一个参数，它将显示错误信息并退出程序。如果第一个 if 的条件为假，则执行第二个 if，也就是说，如果你只带一个命令行参数运行脚本。这个 if 语句产生结果，该语句的条件是命令行参数是一个普通文件。如果传递的参数不是普通文件，第二个 if 的条件为假，并显示错误信息 []: be an ordinary file。注意，当脚本因为错误退出时，其退出状态为 1。

编写脚本时一个重要的习惯是正确缩进命令。良好的缩进使程序更容易理解。if 语句的第二个版本允许双向分支。这是 if 语句的简要描述。

```
Syntax: if (expression) then then-commands endif
```
