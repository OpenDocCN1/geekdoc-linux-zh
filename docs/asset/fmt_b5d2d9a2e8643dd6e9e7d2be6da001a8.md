
| `ARG1 % ARG2` | 返回 `ARG1` 除以 `ARG2` 的算术余数 |

| `STRING : REGEXP` | 如果 REGEXP 匹配 `STRING` 中的某个模式，则返回该模式匹配 |

| `match STRING REGEXP` | 如果 REGEXP 匹配 `STRING` 中的某个模式，则返回该模式匹配 |

| `substr STRING POS LENGTH` | 从位置 `POS`（从 1 开始）开始，返回长度为 LENGTH 个字符的子字符串 |

| `index STRING CHARS` | 返回在 `STRING` 中找到 `CHARS` 的位置；否则，返回 0 |

| `length STRING` | 返回字符串 `STRING` 的数值长度 |

| `+ TOKEN` | 即使 `TOKEN` 是关键字，也将其解释为字符串 |

| `(EXPRESSION)` | 返回 `EXPRESSION` 的值 |

标准运算符在 `expr` 命令中工作正常，但当在脚本或命令行中使用它们时会出现问题。许多 `expr` 命令运算符在 shell 中还有其他含义（例如星号）。在 `expr` 命令中使用它们会产生奇怪的结果：

```
$ expr 5 * 2
expr: syntax error
$
```

为了解决这个问题，你需要使用 shell 转义字符（反斜杠）来标识可能在传递给 `expr` 命令之前被 shell 错误解释的任何字符：

```
$ expr 5 \* 2
10
$
```

这下真的开始变得丑陋了！在 shell 脚本中使用 `expr` 命令同样麻烦：

```
$ cat test6
#!/bin/bash
# An example of using the expr command
var1=10
var2=20
var3=$(expr $var2 / $var1)
echo The result is $var3
```

要将数学方程的结果赋值给变量，你必须使用命令替换从 `expr` 命令中提取输出：

```
$ chmod u+x test6
$ ./test6
The result is 2
$
```

幸运的是，Bash shell 在处理数学运算符方面有所改进，你将在下一节中学习。

### 使用方括号

Bash shell 包含了 `expr` 命令以保持与 Bourne shell 的兼容性；然而，它还提供了执行数学方程的一种更简单的方法。在 Bash 中，当将数学值赋值给变量时，你可以使用美元符号和方括号（`$[ operation]`）来包围数学方程：

```
$ var1=$[1 + 5]
$ echo $var1
6
$ var2=$[$var1 * 2]
$ echo $var2
12
$
```

使用方括号比使用 `expr` 命令进行 shell 数学运算更容易。同样的技术也适用于 shell 脚本：

```
$ cat test7
#!/bin/bash
var1=100
var2=50
var3=45
var4=$[$var1 + ($var2 - $var3)]
echo The final result is $var4
$
```

运行此脚本会产生以下输出：

```
$ chmod u+x test7
$ ./test7
The final result is 500
$
```

另外请注意，当使用方括号方法计算方程时，你不需要担心乘号或其他字符被 shell 错误解释。Shell 知道它不是一个通配符字符，因为它在方括号内。

在 Bash shell 脚本中执行数学运算有一个主要的限制。看看这个例子：

```
$ cat test8
#!/bin/bash
var1=100
var2=45
var3=$[var1 / $var2]
echo The final result is $var3
$
```

现在运行它并看看会发生什么：

```
$ chmod u+x test8
$ ./test8
The final result is 2
$
```

Bash shell 的数学运算符只支持整数算术。如果你试图进行任何类型的实际数学计算，这是一个巨大的限制。

> **注意**
>
> *z* shell（*zsh*）提供完整的浮点数算术运算。如果你在 shell 脚本中需要浮点数计算，你可能需要考虑使用 *z* shell（在第 23 章“*zsh* Shell”中讨论）。

### 浮点数解决方案

有几种解决方案可以克服 Bash 的整数限制。最流行的解决方案是使用内置的 Bash 计算器，称为 *bc*。

#### *bc* 的基础

Bash 计算器实际上是一种编程语言，它允许你在命令行输入浮点数表达式，然后解释表达式、计算它们并返回结果。Bash 计算器识别以下内容：

- 数字（整数和浮点数）

- 变量（简单变量和数组）

- 注释（以磅符号或 C 语言 `/* */` 对开头的行）

- 表达式

- 编程语句（例如 if-then 语句）

- 函数

你可以从 shell 提示符使用 `bc` 命令访问 Bash 计算器：

```
$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free
Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty'.
12 * 5.4
64.8
3.156 * (3 + 5)
25.248
quit
$
```

该示例以输入表达式 `12 * 5.4` 开始。Bash 计算器返回答案。输入到计算器中的每个后续表达式都会被评估，并显示结果。要退出 Bash 计算器，你必须输入 `quit`。

浮点数算术由一个名为 `scale` 的内置变量控制。你必须将此值设置为你希望答案中的小数位数，否则你不会得到你想要的结果：

```
$ bc -q
3.44 / 5
0
scale=4
3.44 / 5
.6880
quit
$
```

`scale` 变量的默认值为 0。在设置 `scale` 值之前，Bash 计算器提供零位小数的答案。在你将 `scale` 变量的值设置为 4 之后，Bash 计算器显示四位小数的答案。`-q` 命令行参数抑制了 Bash 计算器的冗长欢迎横幅。

除了常规数字之外，Bash 计算器还理解变量：

```
$ bc -q
var1=10
var1 * 4
40
var2 = var1 / 5
print var2
2
quit
$
```

## 第二部分：Shell 脚本基础

一旦定义了变量值，你就可以在整个 Bash 计算器会话中使用该变量。`print` 语句允许你打印变量和数字。

#### 在脚本中使用 bc

现在你可能想知道 Bash 计算器如何帮助你在 shell 脚本中进行浮点算术运算。你还记得你的朋友——反引号字符吗？是的，你可以使用命令替换字符来运行 `bc` 命令并将输出赋值给变量！使用的基本格式如下：

```bash
variable=$(echo "options; expression" | bc)
```

第一部分 *options*（选项）允许你设置变量。如果你需要设置多个变量，请使用分号将它们分开。*expression*（表达式）参数定义了使用 `bc` 评估的数学表达式。下面是在脚本中执行此操作的一个快速示例：

```bash
$ cat test9
#!/bin/bash
var1=$(echo " scale=4; 3.44 / 5" | bc)
echo The answer is $var1
$
```

这个示例将 `scale`（精度）变量设置为四位小数，并指定了 `expression` 的一个具体计算。运行该脚本将产生以下输出：

```bash
$ chmod u+x test9
$ ./test9
The answer is .6880
$
```

这很酷炫！你并不局限于仅使用数字作为表达式的值。你还可以使用在 shell 脚本中定义的变量：

```bash
$ cat test10
#!/bin/bash
var1=100
var2=45
var3=$(echo "scale=4; $var1 / $var2" | bc)
echo The answer for this is $var3
$
```

该脚本定义了两个变量，它们被用于发送给 `bc` 命令的表达式中。请记住，要使用美元符号 `$` 来表示变量的值，而不是变量本身。该脚本的输出如下所示：

```bash
$ ./test10
The answer for this is 2.2222
$
```

当然，一旦将值赋值给变量，该变量就可以用于另一次计算：

```bash
$ cat test11
#!/bin/bash
var1=20
```

## 第 11 章：基本脚本构建
