
10. 编写一个 shell 脚本，将计算机系统上的登录名列表作为命令行参数接收，并显示这些登录名以及拥有这些登录名的用户的全名（包含在 `/etc/passwd` 文件中），每行一个。如果登录名无效（即在 `/etc/passwd` 文件中未找到），则显示登录名但全名为空。输出行的格式为 登录名：用户名。

11. 当你运行用反引号（重音符）括起来的独立命令时，会发生什么，例如 `date`？为什么？

12. 当你输入以下 shell 命令序列时会发生什么？

- a. `name=date`
- b. `$name`
- c. `` `$name` ``

13. 查看你的 `~/.profile` 和 `/etc/profile` 文件并列出导出的环境变量及其值。每个变量的用途是什么？

14. 编写一个 Bourne shell 脚本，将登录名列表作为其参数，并显示每个用户在局域网环境中登录的终端数量。

15. 编写一个 Bourne shell 脚本 `domain2ip`，将域名列表作为命令行参数接收并显示其 IP 地址。使用 `nslookup` 命令。以下是该程序的示例运行。

```
$ domain2ip usc.edu up.edu redhat.com

Name: usc.edu

Address: 128.125.253.136

Name: up.edu

Address: 64.251.254.23
```

```
Name: redhat.com

Address: 209.132.183.105

$
```

16. 修改第 12.6.6 节中的 `case_demo` 文件中的脚本，使其允许你尝试任意数量的选项，并且只有在使用 `q` 选项时才退出。

17. 编写一个 Bourne Shell 脚本，显示以下菜单并提示你输入一个字符以调用菜单选项，如下所示：

- a. 列出当前工作目录中的所有文件
- b. 显示今天的日期和时间
- c. 调用第 14 题的 shell 脚本
- d. 显示文件是简单文件还是目录
- e. 为文件创建备份
- f. 启动安全 shell（ssh）会话
- g. 启动 ftp 会话
- h. 退出

选项 (c) 要求你输入登录名列表；对于选项 (d) 和 (e)，在调用 shell 命令/程序之前插入文件名提示。对于选项 (f) 和 (g)，在启动 ssh 或 ftp 会话之前插入域名（或 IP 地址）提示。该程序应允许你任意多次尝试任何选项，并且只有在输入选项 x 时才退出。你应采用的一种良好的编程实践是增量构建代码——即编写一个选项的代码，测试它，然后再进行下一个选项。

18. 修改第 17 题的 Bourne Shell 脚本，使其在子 shell 下执行每个选项的代码。在子 shell 启动以运行选项代码之前，显示子 shell 的 PID。

19. `echo *` 命令的用途是什么？在你的系统上运行该命令并解释命令的输出。

对两个命令组的修正版本进行适当的更改，以便在每种情况下，`date` 和 `pwd` 命令的输出都写入 `file1`，而 `who` 和 `echo` 命令的输出重定向到 `file2`。然后，证明第一组中的命令在子 shell 下执行，而第二组中的命令在当前 shell 下执行。对于第一种情况，展示两种显示子 shell PID 的方法。

# 高级 Bourne Shell 编程

### 目标

- 讨论数值数据处理
- 描述 shell 脚本中命令的标准输入如何从脚本内部的数据重定向
- 解释 Bourne shell 的信号/中断处理能力
- 描述如何使用文件描述符执行文件 I/O 以及如何在 shell 脚本内部重定向标准文件
- 解释 Bourne shell 中的函数
- 讨论 Bourne shell 脚本的调试
- 涵盖命令和原语

`|, <, >, >>, clear, exec, expr, grep, kill, more, read, sort, stty, trap`

## 13.1 引言

本章我们讨论 Bourne shell 的几个重要高级特性。它们包括数值数据处理、here 文档、信号和信号处理，以及从 shell 脚本内部重定向标准文件。我们还讨论了 Bourne shell 对函数的支持，该函数允许程序员编写通用且模块化的代码。最后，我们描述了如何调试 Bourne shell 脚本。

## 13.2 数值数据处理

所有 Bourne shell 变量的值都以字符字符串形式存储。虽然此特性使符号数据处理变得有趣且容易，但它确实使数值数据处理变得有点具有挑战性。原因在于整数数据实际上以字符字符串形式存储。为了对其执行算术和逻辑运算，您需要将它们转换为整数，对整数数据执行必要的运算，并确保结果转换回字符字符串以便正确存储在 shell 变量中。幸运的是，Bourne shell 命令 `expr` 可以做到这一点。以下是该命令的简要说明。

#### 语法

```
expr args
```

用途：计算表达式参数 `args` 并将结果发送到标准输出

常用选项/特性：

- - | 强制创建链接；如果 new-file 已存在则不提示
- - & 如果 new-file 已存在则不创建链接
- =, !=, >=, 整数比较运算符：等于、大于、大于或
- <, <=, != 等于、小于、小于或等于、不等于
- +, -, *, /, % 整数算术运算符：加、减、乘、整数除法（返回商）、余数

Shell 元字符如 `*` 必须在表达式中转义，以便将其视为字面量而不是 shell 元字符。在以下会话中，第一个 `expr` 命令将 shell 变量 `var1` 的值递增 1。第二个 `expr` 命令计算 `var1` 的平方。最后两个 `echo` 命令显示了 `expr` 命令用于对 `var1` 执行整数除法和整数余数运算的用法。

```
$ var1=10
$ var1=`expr $var1 + 1`
$ echo $var1
11
$ var1=`expr $var1 \* $var1`
$ echo $var1
121
$ echo `expr $var1 / 10`
12
$ echo `expr $var1 % 10`
1
$
```

下面的 `countup` 脚本以命令行参数的形式接收一个整数，并在同一行中按升序显示从 1 到给定数字的数字范围。在脚本中，我们使用简单的 while 循环来显示当前数字（从 1 开始），然后计算下一个数字，直到当前数字大于作为命令行参数传递的数字为止。

```
$ cat countup
#!/bin/sh
if [ $# != 1 ]
then
    echo "Usage: $0 integer-argument"
    exit 1
fi
target="$1"    # Set target to the number passed at the command
                # line
current=1       # The first number to be displayed
# Loop here until the current number becomes greater than the target
while [ $current -le $target ]
do
    echo -n "$current"
    current=`expr $current + 1`
done
echo    # Move cursor to the next line
exit 0
$ ./countup 5
1 2 3 4 5
$
```

下面的脚本 `addall` 以命令行参数的形式接收一系列整数并显示它们的和。while 循环将参数列表中的下一个数字添加到运行总和中（初始化为 0），更新已添加数字的计数，并将命令行参数向左移动一个位置。然后循环重复，直到命令行参数中的所有数字都已相加。代码后面的示例运行采用前八个完全平方数的列表并返回它们的和。
