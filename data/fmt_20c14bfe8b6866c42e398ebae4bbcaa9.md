
```
% switch_demo
```

使用以下选项之一：

`d` 或 `D`: 显示今天的日期和当前时间

`- l` 或 `L`: 查看当前工作目录下的文件列表
- `w` 或 `W`: 查看谁正在登录
- `q` 或 `Q`: 退出此程序

输入你的选项并按下 `<Enter>`: `a`

Invalid option; try running the program again.

%

## 607 总结

每个 shell 都有一种编程语言，允许你为无法手动完成的任务编写脚本。在最简单的形式下，shell 脚本由顺序执行的命令列表组成。更高级的脚本使用控制流语句进行分支和重复。这些通常被称为 shell 脚本。变量有两种类型：环境变量和用户定义变量。环境变量在登录时初始化，可以读取和写入。用户定义变量用作临时存储。

`if` 和 `switch` 等控制语句允许分支，`foreach` 和 `while` 语句可用于循环。`continue`、`break` 和 `goto` 命令可中断循环执行。

## 问题

- 1. 什么是 shell 脚本？描述执行它的三种方法。
- 2. 什么是 变量？什么是只读变量？如何让用户定义变量变为只读？给出一个例子。
- 3. 哪个环境变量存储路径？交互式地更改它。这允许你做什么？如果你想使其永久生效，该怎么办？
- 4. 如果执行 17.6 中的脚本并给出 * 作为输入，输出是什么？

## 587 问题

- 5. 编写一个脚本，接收普通文件作为参数，如果其大小为零则删除它。进行相应的检查。
- 6. 编写一个脚本，接收目录作为必要参数，并显示其中零长度的文件。进行相应的检查。
- 7. 编写一个脚本，删除当前目录下的零长度的文件。进行相应的检查。
- 8. 修改问题 6 中的脚本，使目录成为可选参数。如果不指定参数，脚本将使用当前工作目录作为默认。
- 9. 运行第 17.6 节中的 `if_demo` 脚本及其参数。输出对你来说合理吗？为什么？
- 10. 编写一个脚本，接收登录名列表作为参数，并显示这些登录名以及拥有这些用户的全（位于 `/etc/passwd` 文件），每行一个。如果登录名无效（在 `/etc/passwd` 中未找到），则显示登录名但不显示全。输出行的格式为：用户名
- 11. 运行在反引号中的独立命令时会发生什么？为什么？
- 12. 执行以下命令序列会发生什么？
  - `set name=date`
  - `$name`
  - `` `name` ``
- 13. 查看你的 `/etc/csh.crc` `/etc/csh.login` `~/.tcshrc` `~/csh` 和 `~/login` 文件，列出导出的环境变量及其值。每个变量的作用是什么？列出只读变量的名称和值。
- 14. 编写一个脚本，接收登录名列表作为参数，显示每个用户登录到局域网的终端数量。
- 15. 编写脚本 `domain2ip`，接收域名作为命令行参数并显示它们的 IP 地址。使用 `nslookup` 命令。以下是该程序的运行示例。

```
% domain2ip up.edu redhat.com

Name: up.edu

Address: 192.220.208.9
```

# 588 第 17 章 TC Shell 编程入门

名称：redhat.com
地址：207.175.42.154

$ 
16. 修改第 17.6.5 节中 `switch_demo` 文件中的脚本，使其允许尝试任意数量的选项，并且在在使用 `q` 选项时才退出。
17. 编写一个 TC shell 脚本，显示以下菜单并提示输入单个字符以调用菜单选项，如下所示：
a. 列出当前工作目录下的所有文件
b. 显示今天的日期和时间
c. 调用处理问题 13 的 shell 脚本
d. 显示文件是否是“普通”文件或“目录”
e. 为文件创建备份
f. 启动一个 telnet 会话
g. 启动一个 ftp 会话
h. 退出

选项 (c) 要求向用户询问登录名列表。对于选项 (d) 和 (e)，在调用 shell 命令/程序之前提示用户输入文件名。对于选项 (f) 和 (g)，在启动 telnet 或 ftp 会话之前，提示用户输入域名（或 IP 地址）。程序应允许用户多次尝试任何选项，并且仅在用户输入选项 h 时才退出。

良好的编程习惯是增量地构建代码——即：为一个选项编写代码，进行测试，然后处理下一个选项。

# 第 18 章

# 高级 TC Shell 编程

## 目标

* 讨论数值数据处理
* 描述数组处理
* 讨论如何将 shell 脚本命令的标准输入重定向到脚本内部的数据
* 解释 TC shell 的信号/中断处理能力
* 涵盖以下命令和原语 `=\`, `+=`, `-=`, `/`, `%`, `< >`, `|`, `&`, `()`, `<<`, `@ <Ctrl-Z>`, `clear`, `onintr`, `set`, `stty`

## 18.1 引言

我们在第 17 章中没有讨论 TC shell 编程的四种功能：数值数据处理、数组处理、在此文档中（here document）功能以及中断处理。在本章中，我们将讨论这些功能，并提供一些使用它们的示例脚本。我们还描述了如何调试 TC shell 脚本。

# 18.2 数值数据处理

TC shell 具有内置的数值处理能力。它允许对数值整数进行算术和逻辑操作，而无需显式将字符串数据转换为数值数据，反之亦然。你可以使用 `@command` 来声明数值变量（包含整数数据的变量）。该命令仅允许声明局部变量。当不带参数使用时，`@command` 显示所有 shell 变量的名称和值（类似于 `set` 命令）。以下是该命令的简要描述。

```
@variable1 operator expression1] [variable2 operator expression2] ...
```

> 目的：将 '`variable1`' 声明为数值变量，求算术表达式 '`expression1`'并将 '`operator`' 中指定的运算符应用于 '`variable1`' 的当前值；'`variable2`' 和 '`expression1`' 的值将结果赋值给 '`variable2`'，后续变量以类似的方式赋值数值值。

表达式通过之前表 17.4 中总结的算术和逻辑运算符形成。虽然可以使用以 0 开头的八进制数在表达式中，但算术表达式的最终值始终以十进制数值表示。算术表达式的元素之间必须用一个或多个空格分隔，除非元素是 `(`, `)`, `&`, `<`, 和 `>`。表 18.1 描述了可以作为 '`operator`' 使用的赋值运算符。

在接下来的交互会话中，数值变量 `value1` 和 `value2` 分别初始化为 10 和 15，使用 `echo` 命令显示赋值正常工作。

```
% value1 = 10

% value2 = 15

echo "$value1 $value2"
```

# 表 18.1 @ 命令的赋值运算符

| 运算符 | 含义 |
|---|---|
| = | 将 = 右侧表达式的值赋值给其左侧变量 |
| += | 将 = 右侧表达式的值加到左侧变量的当前值上，并将结果赋值给该变量 |
| -= | 从 = 左侧变量的当前值中减去 右侧表达式的值，并将结果赋值给该变量 |
| *= | 将 右侧表达式的值乘以左侧变量的当前值，并将结果赋值给该变量 |
| /= | 将 = 左侧变量除以 = 右侧表达式的值，并将结果（商）赋值给该变量 |
| %= | 将 = 左侧变量除以 = 右侧表达式的值，并将余数赋值给该变量 |

10 15

在接下来的会话中，`@` 命令声明了两个变量 `difference` 和 `sum`，并将它们初始化为表达式的值。这些变量 `difference` 和 `sum` 的取值分别为 -5 和 25。

```
@ @ difference = ($value1 - $value2) sum = ($value1 + $value2)

@ echo $difference $sum

-5 25
```

你可以使用 `++` 和 `--` 运算符将变量的值加1 或 减1。例如，以下三个命令是等价的，都会将 `results` 变量加 1。

```
@ results++

@ results--

@ results = results + 1
```

（注：原文中存在大量重复段落，译文已按要求去重保留核心逻辑）

# 594 第 18 章 高级 TC Shell 编程

```
% echo $students

David Mansoor Sarwar Jeremy Brian Art Charlie

% echo $students[2]

Mansoor Sarwar

% echo $students[3-5]

Jeremy Brian Art
```

与其他变量一样，数组变量可以使用 `unset` 命令从环境中移除。在接下来的会话中，将使用 `unset` 命令来释放 `students` 数组。使用 `echo` 命令来确认该数组已实际释放。

```
% unset students

% echo $students

students: Undefined variable.
```

因此，任何使用 `set` 命令分配多个值的 shell 变量都会变成数组变量。因此，当将命令的多变量输出作为值赋值给一个变量时，它就会变成一个数组变量，并将输出的每个字段包含在独立的数组中。在接下来的会话中，`files` 是一个数组，其元素是当前工作目录下所有文件的名称。`numfiles` 变量包含当前目录下的文件数量。`echo $files[3]` 命令显示数组的第三个元素。

```
% set files = ~ls numfiles = ~ls | wc -w

% echo $files

cmdargs_demo foreach_demol if_demol if_demo2 keyin_demo 5

% echo $numfiles

% echo $files[3]

if_demol
```

你也可以使用用 `set` 命令定义的数组来包含数值数据。在接下来的会话中，`num_array_demo` 文件包含一个脚本，该脚本使用名为 `Fibonacci` 的整数数组，计算数组中整数的和，并在屏幕上显示总和。`Fibonacci` 数组包含斐波那契数列的前 10 个数字。如果你不熟悉斐波那契数列，该数列的前两个数字是 0 和 1，下一个斐波那契数通过将前两个数相加得到。因此，斐波那契数列的前 10 个数字是 0, 1, 1, 2, 3, 5, 8, 13, 21 和 34。斐波那契数列可以用数学公式表示为：

```
F_1 = 0, F_2 = 1, and F_n = F_{n-1} + F_{n-2} (for n ≥ 3)
```

`num_array_demo` 文件中的以下脚本文档齐全，相当容易理解。它显示了前 10 个斐波那契数的和。脚本的示例运行结果在代码之后：

```bash
# cat num_array_demo

# File Name: ~/linux/examples/Tcsh/num_array_demo

# Author: Syed Mansoor Sarwar

# Written: August 16, 1999

# Last Modified: March 4, 2001

# Purpose: 演示对数值数组的操作

# Brief Description: 在一个名为 sum 的数值变量中维护数字的运行和，从 0 开始。读取下一个数组值并将其加到 sum 中。当所有元素都被完毕后，停止并显示答案。

#!/bin/tcsh
```

```bash
# 初始化 Fibonacci 数组为任意数量的斐波那契数 - 本例中为前十个

set Fibonacci = ( 0 1 1 2 3 5 8 13 21 34 )

# size = $Fibonacci # Fibonacci 数组的大小

# index = 1 # 数组索引初始化指向第一个元素

# sum = 0 # 运行和初始化为 0

while ( index <= $size )
    @ sum = $sum + $Fibonacci[$index]    # 更新运行和
    @ index++                            # 数组索引加 1
end

echo "The sum of the given $Fibonacci numbers is $sum."
exit 0
```

```
# num_array_demo

The sum of the given 10 numbers is 88.

%
```

虽然这个示例清楚地解释了数值数组的处理，但它并没有什么实际用途。我们现在展示一个更有实用的例子，其中 `fs` 文件包含一个脚本，该脚本接受目录作为可选参数，并返回其内部所有普通文件的大小（字节）。如果命令行上没有给出目录名称，脚本将采用当前目录。

当你不带任何命令行参数运行该程序时，它会将你的当前目录视为参数。如果你指定了多个参数，脚本将显示错误信息并终止。当仅带非目录参数执行时，程序将再次显示错误并退出。当带有一个参数且该参数为目录时，程序将使用命令替换或 `$directory` 将字符串数组变量初始化为指定目录（如果未指定则为当前目录）中所有文件的名称。使用 `@ nfiles=$files` 初始化数值 `nfiles` 为当前目录的文件数。然后，`files` 数组中每个普通文件的大小初始化为 0。当 `files` 数组中没有剩余名称时，程序将显示目录下所有普通文件使用的总空间（字节）并终止。

```bash
# fs

# File Name: ~/linuxbook/examples/Tcsh/fs

# Author: Syed Mansoor Sarwar

# Written: Mar 4, 2001

# Modified: August 16, 1999; May 11, 2000; March 4, 2001

# Purpose: 将命令行参数传递的目录中所有文件的大小相加

# Brief Description: 在一个名为 sum 的数值变量中维护数字的运行和，从 0 开始。读取下一个数组值并将其加到 sum 中。当所有元素都被完毕后，停止并显示答案。

if ( $argv == 0 ) then
    directory = "."
else if ( $argv > 1 ) then
    echo "Usage: $0"
    exit 1
else
    directory = $argv[1]
endif

if ( !d $directory ) then
    echo "$directory is not a directory"
    exit 1
endif

set files = (~ls $directory)
set nfiles = $#files
set total = 0

foreach file in ($files)
    set size = `ls -l $directory/$file`
    @ total = $total + $size
end

echo "The total size of all files in $directory is $total bytes."
```

## 18.4 HERE DOCUMENT

shell 的 here document 功能允许从文档重定向命令的标准输入。以下是 here document 的简单描述：

```
Syntax: command <<input_marker

...
待处理的输入
...
input_marker
```

以下脚本更好地使用了 here document 功能。该脚本 `dext`（目录专家）维护了一个包含名称、电话号码和电子邮件的目录。脚本带命令行参数运行，并使用 `grep` 命令显示与名称对应的目录项。`grep` 命令使用了 `-i` 选项以忽略字母大小写。反斜杠用于延续 `grep` 命令并在视觉上与目录数据隔离开。

```bash
# more dext
!/bin/tcsh

if ( $argv == 0 ) then
    echo "Usage: $0 name"
endif
```

exit 1
else
  set user_input = "$argv[1]"
  grep -i "$user_input" \
```

<< Directory_Data
John Doe 555.232.0000 johnd@somedomain.edu

Jenny Great 444.656.1111 jg@new.somecollege.edu

David Nice 999.111.3333 david_nice@xyz.org

Jim Davis 777.000.9999 davis@great.advisor.edu

Art Pohm 333.000.8888 art.pohm@great.professor.edu
