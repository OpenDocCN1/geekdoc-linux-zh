
| 可用性 | `SUNWcsu` |

```
/usr/xpg4/bin/basename
```

| 属性类型 | 属性值 |

| :--- | :--- |

| 可用性 | `SUNWxcu4` |

## 参见

`expr(1)`, `attributes(5)`, `environ(5)`, `xpg4(5)`

# batch — 稍后执行命令

# 语法

```
/usr/bin/batch
```

## 描述

参见 `at(1)`。

# bc — 二进制计算器

### 概要

```
/usr/bin/bc [-c] [-l] [file...]
```

## 描述

`bc` 既是一个计算器也是一种类 C 语言，你可以用它来编写数值程序。`bc` 实际上是桌面计算器 `dc` 的预处理器。

使用 `bc` 命令执行工作。然而，`bc` 包含比 `bc` 多得函数，包括命名函数、逻辑运算符和数学函数，如 `sqrt`（平方根）。`bc` 使用中缀表示法，你将运算符放在其操作的数字之间。例如，`2 + 2 = 4`。

你可以从命令行执行 `bc`。它可以从命令行接受输入，或直接从文件读取，然后从命令行继续。当你使用文件名作为参数时，`bc` 会读取文件，处理其命令，然后切换到命令行获取输入。通过这样，你可以将复杂的命令和函数存储在文件中，并直接从命令行使用它们。

`bc` 会自动显示每一行的计算结果。单次计算的所有信息必须在一行内。要退出 `bc`，输入 `quit`。

## 选项

- `-c` 仅编译。
- `-l` 影响小数位数。

# 注释

注释被包含在 `/*` 和 `*/` 之间。

# 函数定义

```
define Letter ( Letter, ..., Letter ) {
auto Letter ... Letter
Statement ... Statement
return ( Expression )
}
```

# -l 库中的函数

`s(x)` 正弦。
`c(x)` 余弦。
`e(x)` 指数。
`l(x)` 对数。
`a(x)` 反正切。
`j(n,x)` 塞尔函数。

所有函数参数均按值传递。

除非主运算符是赋值，否则语句的值将被打印。你可以使用分号或换行符分隔语句。对 `scale` 的赋值影响运算运算保留的位数，类似于 `dc`。对 `ibase` 或 `obase` 设置输入和输出。

你可以同时使用同一个字母作为数组、函数和简单变量。所有变量对程序都是全局的。自动变量在函数调用期间堆栈。当数组作为函数参数或定义为自动变量时，数组名后必须跟空方括号。

## 示例

你可以使用 `bc` 进行普通算术。输入 `bc` 并按回车。不会显示提示符。要退出，输入 `quit` 或 `Control-D`。整个计算必须在同一行内。一旦按下回车，`bc` 就会显示每次计算的结果。

```
castle$ bc
2 + 2
4
Control-D
castle$
```

你可以使用负号表示负数。在以下示例中，减去一个负数等于加上它。加上一个负数等于减去它。

```
castle$ bc
1 + 2 + 3 - -3.12195
9.12195
1 + 2 + 3 + -2.14197
3.85803
```

# 96

Control-D

castle@

你可以使用 `scale` 操作符来指定计算中小数点后保留的位数。`scale` 设置在当前会话中有效。

```
castle@ bc
scale = 3
1.2345/.9876
1.250
```

Control-D

castle@

你可以通过给单个字母赋值赋值来定义并使用变量。在下面的示例中，`x` 被设置为 `7` 并在随后的计算中使用。

```
castle@ bc
x=7
5*7
35
```

Control-D

castle@

接下来的 `example.dc` 文件定义了一个计算指数函数近似值的函数，并打印前 10 个整数的近似值。

```bc
scale = 20
def e(x) {
auto a, b, c, i, s
a = 1
b = 1
s = 1
for(i=1; i<=10; i++) {
a = a*x
b = b*i
c = a/b
if(c == 0) return(s)
s = s+c
}
for(i=1; i<=10; i++) e(i)
```

将文件读入 `bc` 会产生以下结果。

```
castle@ bc example.bc
2.71828182845904523526
7.38905609893065022713
20.0855369231876674083
54.59815003314423907790
148.41315910275660342091
403.42879349273512620821
1096.63315842485859926350
2980.95798704172827474335
8103.08392275738400770974
22026.45759480671651695755
```

文件处理后，你仍处于 `bc` 中，可以进行额外的计算，或者你可以按 `Ctrl-D`，或者输入 `quit` 并按回车退出。

## 环境变量

查看 `environ(5)` 获取以下影响 `bc` 执行的环境变量的描述：`LC_CTYPE`、`LC_MESSAGES` 和 `NLSPATH`。

## 退出状态

- `0` 所有输入文件均已成功处理。
- `unspecified` 发生了错误。

## 文件

- `/usr/lib/lib.bc`: 数学库。
- `/usr/include/limits.h`: 用于定义 `BC_parameters`。

## 属性

查看 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |

|---|---|

| 可用性 | `SUNWesu` |

## 相关

`awk(1)`, `dc(1)`, `attributes(5)`

# 98

# biff — 大文件差异工具

### 概要

```
/usr/bin/biff filename1 filename2 [n] [-s]
```

`biff` 类似于 `diff`，不同之处在于你可以用它处理大到 `diff` 无法处理的文件。大文件是指大小大于等于 `2 Gbytes (2^31 bytes)` 的普通文件。小文件是指大小小于 `2 Gbytes` 的普通文件。

如果 `filename1(filename2)` 为 `-`，则读取标准输入。`biff` 会忽略两个文件开头的相同行，将每个文件的剩余部分分成 `n` 行一个段，并在相应的分段上调用 `diff`。如果指定了两个可选参数，你必须按照上述指示顺序使用它们。

`biff` 的输出与 `diff` 完全相同，但行号经过了调整，使其就像文件是作为整体处理的一样。`biff` 输出的第一部分列出两个文件中不同的行，并用 `c` 分隔已更改。来自第一个文件的行标记为 `<`，第二个文件的行标记为 `>`。

> 注意 — 由于对文件进行了分段，`biff` 不一定能找到文件差异的最小充分分集。

## 选项

- `-n` 指定行段数。默认情况下，`n` 的值为 `3500`。当 `3500` 行的分段对于 `diff` 来说太大并导致其失败时，此选项非常有用。
- `-s` 不打印 `biff` 诊断信息（静默选项）。此选项不会抑制 `biff` 调用的 `diff` 可能产生的诊断消息。

## 使用

查看 `largefile(5)` 获取 `biff` 遇到大于或等于 `2 Gbytes (2^31 bytes)` 文件时的行为描述。

## 示例

在下面的示例中，首先用 `cat` 命令显示两个（小）文件，然后用 `biff` 比较这两个文件。你可以在小文件上使用 `biff`；然而，`diff` 提供了更多用于比较小文件的选项。

```
cat kookaburral
```

Kookaburra sits in the old gum tree

Merry merry king of the bush is he

Laugh, kookaburra, laugh

Gay your life must be.

Kookaburra sits in the old gum tree

Eating all the gumdrops

Laugh, kookaburra, laugh

Leave some there for me.

Kookaburra sits in the old gum tree

Eating all the gumdrops

Laugh, kookaburra, laugh

Leave some there for me.

Kookaburra sits in the old gum tree

Eating all the gumdrops

Laugh, kookaburra, laugh

Leave some there for me.

```bash
cat kookaburral > /tmp/file1
```

Kookaburra sits in the old gum tree

Eating all the gumdrops

Laugh, kookaburra, laugh

Leave some there for me.

Kookaburra sits in the old gum tree

Eating all the gumdrops
