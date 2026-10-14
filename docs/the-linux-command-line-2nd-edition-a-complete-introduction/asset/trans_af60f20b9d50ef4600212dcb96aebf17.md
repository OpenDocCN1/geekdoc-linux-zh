

```
[me@linuxbox ~]$ arith-loop
a   a*2   a**3
=  ====   ====
0    0     0
1    1     1
2    4     8
3    9    27
4   16    64
5   25   125
6   36   216
7   49   343
8   64   512
9   81   729
10 100  1000
```

## bc – An Arbitrary Precision Calculator Language

我们已经看到 shell 如何处理各种整数运算，但如果我们需要执行更高阶的数学运算，甚至只是使用浮点数怎么办？答案是，我们不能。至少不能直接用 shell 来做。为此，我们需要使用外部程序。我们可以采用几种方法。嵌入 Perl 或 AWK 程序是一种可能的解决方案，但不幸的是，这超出了本书的范围。

另一种方法是使用专门的计算器程序。Linux 系统上常见的一个程序就叫做 bc。

bc 程序读取用其自身类似 C 的语言编写的文件并执行它。bc 脚本可以是单独的文件，也可以从标准输入读取。bc 语言支持相当多的特性，包括变量、循环和程序员自定义函数。我们在这里不会完全介绍 bc，只是足以一窥其概。bc 由其 man 手册详细记录。

让我们从一个简单的例子开始。我们将编写一个 bc 脚本来计算 2 加 2：

```
/* A very simple bc script */
2 + 2
```

脚本的第一行是注释。bc 使用与 C 编程语言相同的注释语法。注释可以跨越多行，以 /* 开始，以 */ 结束。

## Using bc

如果我们将上面的 bc 脚本保存为 foo.bc，可以这样运行它：

```
[me@linuxbox ~]$ bc foo.bc
bc 1.06.94
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
4
```

仔细看，我们可以在版权信息之后的最底部看到结果。此消息可以用 -q（quiet）选项抑制。

bc 也可以交互使用：

```
[me@linuxbox ~]$ bc -q
2 + 2
4
quit
```

使用 bc 交互时，我们只需输入想要执行的计算，结果会立即显示。bc 命令 quit 结束交互会话。

也可以通过标准输入将脚本传递给 bc：

```
[me@linuxbox ~]$ bc < foo.bc
4
```

能够接受标准输入意味着我们可以使用 here 文档、here 字符串和管道来传递脚本。这是一个 here 字符串的例子：

```
[me@linuxbox ~]$ bc <<< "2+2"
4
```

## An Example Script

作为一个实际例子，我们将构建一个执行常见计算的脚本，即月度贷款还款额。在下面的脚本中，我们使用 here 文档将脚本传递给 bc：

```
#!/bin/bash

# loan-calc : script to calculate monthly loan payments

PROGNAME=$(basename $0)

usage () {
cat <<- EOF
Usage: $PROGNAME PRINCIPAL INTEREST MONTHS

Where:

PRINCIPAL is the amount of the loan.
INTEREST is the APR as a number (7% = 0.07).
MONTHS is the length of the loan's term.
    EOF
}

if (($# != 3)); then
    usage
    exit 1
fi

principal=$1
interest=$2
months=$3

bc <<- EOF
scale = 10
i = $interest / 12
p = $principal
n = $months
a = p * ((i * ((1 + i) ^ n)) / (((1 + i) ^ n) - 1))
print a, "\n"
EOF
```

执行时的结果如下所示：

```
[me@linuxbox ~]$ loan-calc 135000 0.0775 180
```

```
1270.7222490000
```

此示例计算了一笔 $135,000 贷款在 7.75% APR 下 180 个月（15 年）的月供。请注意答案的精度。这由 bc 脚本中赋予特殊变量 scale 的值决定。bc 脚本语言的完整描述由 bc man 手册提供。虽然其数学符号与 shell 略有不同（bc 更接近 C），但基于我们迄今所学，大部分内容会相当熟悉。

## Summing Up

在本章中，我们学习了许多可以用来在脚本中完成“实际工作”的小技巧。随着我们脚本经验的增长，有效地操作字符串和数字的能力将证明极其宝贵。我们的 loan-calc 脚本证明，即使是简单的脚本也可以用来做一些真正有用的事情。

## Extra Credit

虽然 loan-calc 脚本的基本功能已经就位，但脚本远未完成。作为额外加分，尝试通过以下功能改进 loan-calc 脚本：

- 对命令行参数进行完整验证
- 实现一个命令行选项以提供“交互”模式，提示用户输入贷款本金、利率和期限。
- 更好的输出格式。

## Further Reading

- Bash Hackers Wiki 对参数扩展有很好的讨论：
  http://wiki.bash-hackers.org/syntax/pe
- Bash 参考手册也涵盖了这一点：
  http://www.gnu.org/software/bash/manual/bashref.html#Shell-Parameter-Expansion
- Wikipedia 有一篇描述位操作的良好文章：
  http://en.wikipedia.org/wiki/Bit_operation
- 以及一篇关于三元运算的文章：
  http://en.wikipedia.org/wiki/Ternary_operation

