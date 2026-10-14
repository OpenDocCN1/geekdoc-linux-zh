
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

## `bc` – An Arbitrary Precision Calculator Language

我们已经看到 shell 如何处理各种整数运算，但如果我们需要执行更高阶的数学运算，甚至只是使用浮点数怎么办？答案是，我们不能。至少不能直接使用 shell 来做。为此，我们需要使用外部程序。我们可以采用几种方法。嵌入 Perl 或 AWK 程序是一种可能的解决方案，但不幸的是，这超出了本书的范围。

另一种方法是使用专门的计算器程序。Linux 系统上常见的一个程序就叫做 `bc`。

`bc` 程序读取用其自身类似 C 的语言编写的文件并执行它。`bc` 脚本可以是单独的文件，也可以从标准输入读取。`bc` 语言支持相当多的特性，包括变量、循环和程序员自定义函数。我们在这里不会完全介绍 `bc`，只是足以一窥其概。`bc` 由其 `man` 手册详细记录。

让我们从一个简单的例子开始。我们将编写一个 `bc` 脚本来计算 2 加 2：

```
/* A very simple bc script */
2 + 2
```

脚本的第一行是注释。`bc` 使用与 C 编程语言相同的注释语法。注释可以跨越多行，以 `/*` 开始，以 `*/` 结束。

## Using `bc`

如果我们将上面的 `bc` 脚本保存为 `foo.bc`，可以这样运行它：

```
[me@linuxbox ~]$ bc foo.bc
bc 1.06.94
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
4
```

仔细看，我们可以在版权信息之后的最底部看到结果。此消息可以用 `-q`（quiet）选项抑制。

`bc` 也可以交互使用：

```
[me@linuxbox ~]$ bc -q
2 + 2
4
quit
```

使用 `bc` 交互时，我们只需输入想要执行的计算，结果会立即显示。`bc` 命令 `quit` 结束交互会话。

也可以通过标准输入将脚本传递给 `bc`：

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

作为一个实际例子，我们将构建一个执行常见计算的脚本，即月度贷款还款额。在下面的脚本中，我们使用 here 文档将脚本传递给 `bc`：

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
1270.7222490000
```

此示例计算了一笔 $135,000 贷款在 7.75% APR 下 180 个月（15 年）的月供。请注意答案的精度。这由 `bc` 脚本中赋予特殊变量 `scale` 的值决定。`bc` 脚本语言的完整描述由 `bc` 的 `man` 手册提供。虽然其数学符号与 shell 略有不同（`bc` 更接近 C），但基于我们迄今所学，大部分内容会相当熟悉。

## Summing Up

在本章中，我们学习了许多可以用来在脚本中完成“实际工作”的小技巧。随着我们脚本经验的增长，有效地操作字符串和数字的能力将证明极其宝贵。我们的 `loan-calc` 脚本证明，即使是简单的脚本也可以用来做一些真正有用的事情。

## Extra Credit

虽然 `loan-calc` 脚本的基本功能已经就位，但脚本远未完成。作为额外加分，尝试通过以下功能改进 `loan-calc` 脚本：

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

- 以及我们在 `loan-calc` 脚本中使用的计算贷款付款的公式的描述：

  http://en.wikipedia.org/wiki/Amortization_calculator

## 35 – 数组

在上一章中，我们研究了 shell 如何操作字符串和数字。到目前为止我们所研究的这些数据类型在计算机科学领域被称为标量变量；也就是说，包含单个值的变量。

在本章中，我们将研究另一种称为数组的数据结构，它保存多个值。数组几乎是每种编程语言的特性。shell 也支持它们，尽管功能相当有限。即使如此，它们对于解决编程问题也非常有用。

### 什么是数组？

数组是同时保存一个以上值的变量。数组像表格一样组织。让我们以电子表格为例。电子表格就像一个二维数组。它同时具有行和列，电子表格中的单个单元格可以根据其行和列地址定位。数组的行为方式相同。数组具有称为元素的单元格，每个元素包含数据。单个数组元素使用称为索引或下标的地址进行访问。

大多数编程语言支持多维数组。电子表格就是一个具有两个维度宽度和高度的多维数组的例子。许多语言支持具有任意数量维度的数组，不过二维和三维数组可能是最常用的。

`bash` 中的数组仅限于一维。我们可以将其视为只有一个列的电子表格。即使有此限制，它们也有许多应用。数组支持首次出现在 `bash` 版本 2 中。原始的 Unix shell 程序 `sh` 根本不支持数组。

### 创建数组

数组变量的命名方式与其他 `bash` 变量相同，并在被访问时自动创建。以下是一个示例：

```
[me@linuxbox ~]$ a[1]=foo
[me@linuxbox ~]$ echo ${a[1]}
foo
```

这里我们看到了数组元素的赋值和访问的示例。通过第一个命令，数组 `a` 的元素 1 被赋值为“foo”。第二个命令显示元素 1 的存储值。第二个命令中使用大括号是为了防止 shell 对数组元素名称尝试路径名展开。

数组也可以使用 `declare` 命令创建：

```
[me@linuxbox ~]$ declare -a a
```

使用 `-a` 选项，此 `declare` 示例创建了数组 `a`。

### 为数组赋值

值可以通过两种方式之一赋值。单个值可以使用以下语法赋值：

`name[subscript]=value`

其中 `name` 是数组的名称，`subscript` 是大于或等于零的整数（或算术表达式）。请注意，数组的第一个元素的下标是零，而不是一。`value` 是分配给数组元素的字符串或整数。

多个值可以使用以下语法赋值：

`name=(value1 value2 ...)`
