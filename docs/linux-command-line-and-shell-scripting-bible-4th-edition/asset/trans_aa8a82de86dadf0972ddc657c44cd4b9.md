

## 字符串：正则表达式

| 命令 | 描述 |
| :--- | :--- |
| `STRING : REGEXP` | 如果 REGEXP 在 STRING 中匹配某个模式，则返回该模式匹配项。 |
| `match STRING REGEXP` | 如果 REGEXP 在 STRING 中匹配某个模式，则返回该模式匹配项。 |
| `substr STRING POS LENGTH` | 返回长度为 LENGTH 的子字符串，从位置 POS（起始位置为 1）开始。 |
| `index STRING CHARS` | 返回 CHARS 在 STRING 中找到的位置；否则返回 0。 |
| `length STRING` | 返回字符串 STRING 的数值长度。 |
| `+ TOKEN` | 即使 TOKEN 是关键字，也将其解释为字符串。 |
| `(EXPRESSION)` | 返回 EXPRESSION 的值。 |

为了解决这个问题，你需要使用 shell 转义字符（反斜杠）来标识那些在传递给 `expr` 命令之前可能会被 shell 错误解释的字符：

```bash
$ expr 5 \* 2
10
$
```

这就真的开始变得很难用了！在 shell 脚本中使用 `expr` 命令同样笨重：

```bash
$ cat test6
#!/bin/bash
# 一个使用 expr 命令的示例
var1=10
var2=20
var3=$(expr $var2 / $var1)
echo 结果是 $var3
```

要将数学方程的结果分配给变量，你必须使用命令替换从 `expr` 命令中提取输出：

```bash
$ chmod u+x test6
$ ./test6
结果是 2
$
```

幸运的是，Bash shell 在处理数学运算符方面有所改进，你将在下一节中看到。

### 使用方括号

Bash shell 包含了 *expr* 命令以保持与 Bourne shell 的兼容性；然而，它也提供了一种进行数学方程计算更简单的方法。在 Bash 中，当将数学值分配给变量时，你可以使用美元符号和方括号（$[ 操作 ]）来包围数学方程：

```bash
$ var1=$[ 1 + 5]
$ echo $var1
6
$ var2=$[$var1 * 2]
$ echo $var2
12
$
```

使用方括号使 shell 数学运算比使用 *expr* 命令容易得多。同样的技术也适用于 shell 脚本：

```bash
$ cat test7
#!/bin/bash
var1=100
var2=50
var3=45
var4=$[$var1 * ($var2 - $var3)]
echo 最终结果是 $var4
$
```

运行此脚本会产生以下输出：

```bash
$ chmod u+x test7
$ ./test7
最终结果是 500
$
```

此外，请注意，使用方括号方法计算方程时，你不需要担心乘法符号或其他字符被 shell 错误解释。shell 知道它不是通配符字符，因为它位于方括号内。

在 Bash shell 脚本中进行数学运算有一个主要限制。看看这个例子：

```bash
$ cat test8
#!/bin/bash
var1=100
var2=45
var3=$[$var1 / $var2]
echo 最终结果是 $var3
$
```

现在运行它，看看会发生什么：

```bash
$ chmod u+x test8
$ ./test8
最终结果是 2
$
```

Bash shell 的数学运算符仅支持整数算术。如果你试图进行任何形式的现实世界数学计算，这是一个巨大的限制。

**注意**

z shell (zsh) 提供了完整的浮点算术操作。如果你的 shell 脚本需要浮点计算，你可能需要考虑使用 z shell（在第 23 章“使用替代 Shell”中讨论）。

## 浮点解决方案

有几种解决方案可以克服 Bash 整数限制。最流行的解决方案使用内置的 Bash 计算器，称为 `bc`。

### bc 的基础

Bash 计算器实际上是一种编程语言，允许你在命令行输入浮点表达式，然后解释这些表达式，计算它们并返回结果。Bash 计算器识别以下内容：

- 数字（包括整数和浮点数）
- 变量（包括简单变量和数组）
- 注释（以井号开头的行或 C 语言的 `/* */` 对）
- 表达式
- 编程语句（如 `if`-then 语句）
- 函数

你可以使用 `bc` 命令从 shell 提示符访问 Bash 计算器：

```bash
$ bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free
Software Foundation, Inc.
这是免费软件，绝对没有保证。
详细信息请输入 'warranty'。
12 * 5.4
64.8
3.156 * (3 + 5)
25.248
quit
$
```

示例首先输入表达式 `12 * 5.4`。Bash 计算器返回答案。输入到计算器的每个后续表达式都会被评估，并显示结果。要退出 Bash 计算器，你必须输入 `quit`。

浮点算术由一个名为 `scale` 的内置变量控制。你必须将此值设置为你希望答案中的小数位数，否则你无法获得你想要的结果：

```bash
$ bc -q
3.44 / 5
0
scale=4
3.44 / 5
.6880
quit
$
```

`scale` 变量的默认值为 0。在设置 `scale` 值之前，Bash 计算器提供零位小数的答案。当你将 `scale` 变量值设置为 4 后，Bash 计算器显示四位小数的答案。`-q` 命令行参数抑制了来自 Bash 计算器的冗长欢迎横幅。除了普通数字外，Bash 计算器还理解变量：

```bash
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

一旦定义了变量值，你可以在整个 Bash 计算器会话中使用该变量。`print` 语句允许你打印变量和数字。

### 在脚本中使用 bc

现在你可能想知道 Bash 计算器将如何帮助你在 shell 脚本中进行浮点算术。还记得你的朋友反引号字符吗？是的，你可以使用命令替换字符运行 `bc` 命令并将输出分配给变量！使用的基本格式如下：

```bash
variable=$(echo "options; expression" | bc)
```

第一部分 `options` 允许你设置变量。如果你需要设置多个变量，使用分号将它们分开。`expression` 参数定义了使用 `bc` 评估的数学表达式。以下是在脚本中快速完成此操作的示例：

```bash
$ cat test9
#!/bin/bash
var1=$(echo "scale=4; 3.44 / 5" | bc)
echo 答案是 $var1
$
```

此示例将 `scale` 变量设置为四位小数，然后指定表达式的特定计算。运行此脚本将产生以下输出：

```bash
$ chmod u+x test9
$ ./test9
答案是 .6880
$
```

这很时髦！你不仅限于仅使用数字作为表达式值。你还可以使用在 shell 脚本中定义的变量：

```bash
$ cat test10
#!/bin/bash
var1=100
var2=45
var3=$(echo "scale=4; $var1 / $var2" | bc)
echo 这个的答案是 $var3
$
```

脚本定义了两个变量，这些变量用于发送给 `bc` 命令的表达式中。请记住使用美元符号来指示变量的值，而不是变量本身。此脚本的输出如下：

```bash
$ ./test10
这个的答案是 2.2222
$
```

当然，一旦将值分配给变量，该变量就可以在另一次计算中使用：

```bash
$ cat test11
#!/bin/bash
var1=20
var2=3.14159
var3=$(echo "scale=4; $var1 * $var1" | bc)
var4=$(echo "scale=4; $var3 * $var2" | bc)
echo 最终结果是 $var4
$
```

这种方法对于简短的计算运行良好，但有时你需要更深入地处理数字。如果你有超过两个计算，试图在同一命令行上列出多个表达式会变得令人困惑。

这个问题有一个解决方案。`bc` 命令识别输入重定向，允许你将文件重定向到 `bc` 命令进行处理。然而，这也可能令人困惑，因为你需要将表达式存储在文件中。

最佳方法是使用内联输入重定向，允许你直接从命令行重定向数据。在 shell 脚本中，你将输出分配给一个变量：

```bash
variable=$(bc << EOF
options
statements
expressions
EOF
)
```

`EOF` 文本字符串指示内联重定向数据的开始和结束。请记住，仍然需要命令替换字符将 `bc` 命令的输出分配给变量。

现在你可以将所有的单个 Bash 计算器元素放在脚本文件中的单独行上。这是使用此技术在脚本中的示例：

```bash
$ cat test12
#!/bin/bash

var1=10.46
var2=43.67
var3=33.2
var4=71

var5=$(bc << EOF
scale = 4
a1 = ( $var1 * $var2)
b1 = ($var3 * $var4)
a1 + b1
EOF
)

echo 这一堆 mess 的最终答案是 $var5
$
```

将每个选项和表达式放在脚本中的单独行上会使事情更整洁、更容易阅读和理解。`EOF` 字符串指示要重定向到 `bc` 命令的数据的开始和结束。当然，你需要使用命令替换字符来指示要分配给变量的命令。

在这个示例中，你还会注意到你可以在内部分配变量

