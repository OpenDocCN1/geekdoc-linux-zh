

# 高级 Bourne Shell 编程

## 目标

- 讨论数值数据处理
- 描述 shell 脚本中命令的标准输入如何从脚本内部的数据重定向
- 解释 Bourne shell 的信号/中断处理能力
- 描述如何使用文件描述符执行文件 I/O 以及如何在 shell 脚本内部重定向标准文件
- 解释 Bourne shell 中的函数
- 讨论 Bourne shell 脚本的调试
- 涵盖命令和原语

|, <, >, >>, clear, exec, expr, grep, kill, more, read, sort, stty, trap

## 13.1 引言

本章我们讨论 Bourne shell 的几个重要高级特性。它们包括数值数据处理、here 文档、信号和信号处理，以及从 shell 脚本内部重定向标准文件。我们还讨论了 Bourne shell 对函数的支持，该函数允许程序员编写通用且模块化的代码。最后，我们描述了如何调试 Bourne shell 脚本。

## 13.2 数值数据处理

所有 Bourne shell 变量的值都以字符字符串形式存储。虽然此特性使符号数据处理变得有趣且容易，但它确实使数值数据处理变得有点具有挑战性。原因在于整数数据实际上以字符字符串形式存储。为了对其执行算术和逻辑运算，您需要将它们转换为整数，对整数数据执行必要的运算，并确保结果转换回字符字符串以便正确存储在 shell 变量中。幸运的是，Bourne shell 命令 expr 可以做到这一点。以下是该命令的简要说明。

### 语法

```
expr args
```

用途：计算表达式参数 args 并将结果发送到标准输出

常用选项/特性：

- - | 强制创建链接；如果 new-file 已存在则不提示
- - & 如果 new-file 已存在则不创建链接
- =, !=, >=, 整数比较运算符：等于、大于、大于或
- <, <=, != 等于、小于、小于或等于、不等于
- +, -, *, /, % 整数算术运算符：加、减、乘、整数除法（返回商）、余数

Shell 元字符如 * 必须在表达式中转义，以便将其视为字面量而不是 shell 元字符。在以下会话中，第一个 expr 命令将 shell 变量 var1 的值递增 1。第二个 expr 命令计算 var1 的平方。最后两个 echo 命令显示了 expr 命令用于对 var1 执行整数除法和整数余数运算的用法。

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

下面的 countup 脚本以命令行参数的形式接收一个整数，并在同一行中按升序显示从 1 到给定数字的数字范围。在脚本中，我们使用简单的 while 循环来显示当前数字（从 1 开始），然后计算下一个数字，直到当前数字大于作为命令行参数传递的数字为止。

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

下面的脚本 addall 以命令行参数的形式接收一系列整数并显示它们的和。while 循环将参数列表中的下一个数字添加到运行总和中（初始化为 0），更新已添加数字的计数，并将命令行参数向左移动一个位置。然后循环重复，直到命令行参数中的所有数字都已相加。代码后面的示例运行采用前八个完全平方数的列表并返回它们的和。

```
$ cat addall
#!/bin/sh
# File Name:    ~/unixbook/examples/Bshell/addall
# Author:       Syed Mansoor Sarwar
# Written:      August 18, 2004
# Modified:     August 18, 2004, July 28, 2014
# Purpose:      To demonstrate use of the expr command in processing
#               numeric data
#
# Brief Description:
#               Maintain the running sum of numbers in a numeric
#               variable called sum, initialized to 0. Read the next
#               integer and add it to sum. When all the integers
#               specified as command line arguments have been read,
#               display the answer, and terminate the program. If
#               the program is run with no arguments, inform the
#               user of the command syntax.
if [ $# = 0 ]
```
