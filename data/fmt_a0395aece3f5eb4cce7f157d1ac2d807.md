
```bash
${parameter#pattern}
${parameter##pattern}
```

这些扩展会删除参数包含的字符串中由 `pattern` 定义的开头部分。`pattern` 是通配符模式，类似于路径名扩展中使用的模式。两种形式的区别在于：`#` 形式移除最短匹配项，而 `##` 形式移除最长匹配项。

```
[me@linuxbox ~]$foo=file.txt.zip
```

# 参数扩展

```
[me@linuxbox ~]$ echo ${foo#*.}
txt.zip
[me@linuxbox ~]$ echo ${foo##*}
zip
```

```bash
${parameter%pattern}
${parameter%%pattern}
```

这些扩展与之前的 `#` 和 `##` 扩展相同，不同之处它们是从参数包含的字符串末尾而不是开头删除文本。

```
[me@linuxbox ~]$ foo=file.txt.zip
[me@linuxbox ~]$ echo ${foo%.*}
file.txt
[me@linuxbox ~]$ echo ${foo%%.*}
file
```

```bash
${parameter/pattern/string}
${parameter//pattern/string}
${parameter#pattern/string}
${parameter/%pattern/string}
```

这些扩展对参数的内容执行查找替换操作。如果找到匹配通配符模式的文本，将其替换为 `string` 内容。在普通形式下，只替换 `pattern` 的第一次出现。在 `//` 形式下，替换所有出现的地方。`#` 形式要求匹配发生在字符串开头，而 `%` 形式要求匹配发生在字符串末尾。在每种形式中，`string` 都可以省略，导致 `pattern` 匹配的文本被删除。

```
[me@linuxbox ~]$ foo=JPG.JPG
[me@linuxbox ~]$ echo ${foo/JPG/jpg}
jpg.JPG
[me@linuxbox ~]$ echo ${foo//JPG/jpg}
jpg.jpg
[me@linuxbox ~]$ echo ${foo#*JPG/jpg}
jpg.JPG
[me@linuxbox ~]$ echo ${foo/%*JPG/jpg}
JPG.jpg
```

了解参数扩展是非常有用的。字符串操作可以作为 `sed` 和 `cut` 等常用命令的替代方案。扩展可以通过消除对外部程序的使用来提高脚本效率。例如，我们将修改上一节中讨论的最长单词程序，使用参数扩展 `${j}` 来替换命令替换 `$(echo n | wc -c)` 及其产生的子 shell：

```bash
#!/bin/bash

# longest-word3: 查找文件中最长的字符串

for i; do
    if [[ -r "$i" ]]; then
        max_word=
        max_len=0
        for j in ${i}; do
            if (( len > max_len )); then
                max_len=$len
                max_word="$j"
            fi
        done
        echo "$i: $max_word ($max_len characters)"
    fi
done
```

接下来我们将通过 `time` 命令比较两个版本的效率。

```
[me@linuxbox ~] time longest-word2 list.txt
i: This string is long. (20 characters)

real    0m0.000
user    0m0.000
sys     0m0.000
[me@linuxbox ~] time longest-word3 list.txt
i: This string is long. (20 characters)

real    0m0.000
user    0m0.000
sys     0m0.000
```

# 大小转换

`declare` 命令可将字符串规范化为大写或小写。通过 `declare`，我们可以强制变量无论赋值了什么都包含期望的格式。

```bash
#!/bin/bash

# ul-declare: 通过 declare 展示大小转换

declare -u
declare -l

if [[ $1 ]]; then
    upper="$1"
    lower="$1"
    echo "$upper"
    echo "$lower"
fi
```

在前面的脚本中，我们使用 `declare` 创建了两个变量：`upper` 和 `lower`。我们将第一个命令行参数（位置参数 `1`）的值赋值给每个变量并在屏幕上显示它们。除了 `declare` 之外，还有四种执行大/小写的扩展，如表 34-1 所示。

表 34-1: 大小转换扩展

| 格式 | 结果 |
| :--- | :--- |
| `${parameter,,pattern}` | 将参数的值转换为全小写。`pattern` 是可选的 shell 通配符（例如 `[A-F]`），它将限制转换的字符。完整的模式说明请参 bash man page。 |
| `${parameter,pattern}` | 将参数的值，仅将第一个字符转换为小写。 |
| `${parameter^^pattern}` | 将参数的值转换为全大写字母。 |
| `${parameter^pattern}` | 将参数的值，仅将第一个字符转换为大写（首字母大写）。 |

```
[me@linuxbox ~]$ ul-param aBc
abc
aBC
ABC
ABC
```

再次，我们处理第一个命令行参数，并输出参数扩展所支持的四种变体。虽然此脚本使用了第一个位置参数，但参数可以是任何字符串、变量或字符串表达式。

## 算术评估与扩展

我们在第 7 章中查看了算术扩展。它用于对整数执行各种算术操作。其基本形式如下，其中 `expression` 是一个有效的算术表达式：

这与我们在第 27 章遇到的用于算术评估（真值测试）的复合命令 `(( ))` 相关。

在之前的章节中，我们看到了一些常见的表达式和运算符类型。在这里，我们将查看更完整的列表。

### 进制

在第 9 章中，我们了解了八进制（8 进制）和十六进制（16 进制）。在算术表达式中，shell 支持任何进制的整数常量。表 34-2 列出了用于指定进制的符号。

表 34-2：指定不同的进制

| 符号 | 描述 |
| --- | --- |
| number | 默认情况下，没有任何符号的数字被视为十进制（10 进制）整数。 |
| @number | 在算术表达式中，前导为零的数字被视为八进制。 |
| Oxnumber | 十进制进制法。 |
| base#number | number 位于 base |

以下是一些示例：

### 34 – 字符串与数字

```bash
[me@linuxbox ~] echo $((0xff))
255
[me@linuxbox ~] echo $((2#11111111))
255
```

在之前的示例中，我们打印了十六进制数 `ff`（最大的两位数）的值，以及最大的八位二进制（2 进制）数的值。

### 一元运算符

有两个一元运算符 `+` 和 `-`，分别用于表示数字是正数还是负数。例如 `-5`。

### 简单算术

普通的算术运算符列在表 34-3 中。

表 34-3：算术运算符

| 运算符 | 描述 |
| --- | --- |
| + | 加法 |
| - | 减法 |
| * | 乘法 |
| / | 整数除 |
| ** | 幂 |
| % | 取模（余数） |

这些大部分是自言自明的，但整数除和取模需要进一步讨论。

由于 shell 的算术运算只对整数进行，因此除法的结果总是整数。

```bash
[me@linuxbox ~] echo $(( 5 / 2 ))
2
```

这使得除法操作中余数的确定变得更加重要。

```bash
[me@linuxbox ~]$ echo $(( 5 % 2 ))
1
```

通过使用除法取模运算符，我们可以确定 `5` 除以 `2` 的结果是 `2`，余 `1`。

计算余数在循环中用。它允许在循环执行期间指定的间隔执行操作。在下面的示例中，我们显示了一行数字，突出显示每个 5 的倍数：

```bash
#!/bin/bash

# 展示取模运算符

for (i = 0; i <= 20; i = i + 1); do
  remainder=$((i % 5))
  if (( remainder == 0 )); then
    printf "%<d" "$i"
  else
    printf "%%d" "$i"
  fi
done
printf "\n"
```

执行时，结果看起来所示：

```bash
[me@linuxbox ~]$ modulo
<0> 1 2 3 4 <5> 6 7 8 9 <10> 11 12 13 14 <15> 16 17 18 19 <20>
```

### 赋值

虽然可能并不立即明显，但算术表达式可以执行赋值。我们已经执行过许多赋值，尽管在不同的上下文中。每当我们改变变量值时，我们都在执行赋值。我们也可以在算术表达式中这样做。

```bash
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo "$foo"
```

### 34 – 字符串与数字

```bash
[me@linuxbox ~]$ if (( foo = 5 )); then echo "It is true."; fi
It is true.
[me@linuxbox ~]$ echo foo
```

在前面的示例中，我们首先给变量 `foo` 分配一个空值，并验证它确实是空的。接下来，我们执行带有复合命令 `(( foo = 5 ))` 的 `if`。这个过程做了两件有趣的事：它将值 `5` 分配给变量 `foo`，并且它的结果为真，因为 `foo` 被分配了一个非零值。

> 注意：记住前面示例中 `=` 的确切含义非常重要。单个 `=` 执行赋值。`foo = 5` 的意思是“让 `foo` 等于 `5`”，而 `==` 等价性。`foo == 5` 表示“`foo` 等于 `5` 吗？”这是许多编程语言的共同特征。在 shell 中，这可能会有点混乱，因为 `test` 命令接受单个 `=` 字符串等价性。这是使用更现代的 `[[ ]]` 和 `(( ))` 命令代替 `test` 的另一个原因。

除了 `=` 符号外，shell 还提供了执行某些有用赋值的符号，如表 34-4所示。

表 34-4：赋值

| 符号 | 描述 |
| --- | --- |
| parameter = value | 简单赋值。 |
| parameter += value | 加赋值。 |
| parameter -= value | 减赋值。 |
| parameter *= value | 乘赋值。 |
| parameter /= value | 整数除赋值。 |
| parameter %= value | 取模赋值。 |
| parameter++ | 后置增。 |
| ++parameter | 前置增。 |
| parameter-- | 后置减。 |
| --parameter | 前置减。 |

### 算术评估与扩展

`++` 和 `--` 运算符通常结合循环使用。我们将对取模脚本进行一些改进。对于大多数 shell 应用，前置运算符将是最用的。

`++` 和 `--` 运算符可以出现在参数的前面或后面。这种符号风格源自 C 语言，并被许多其他语言采用。虽然它们都增加或减少参数一个，但两种位置有微妙的区别。这里有一个返回参数的示例：

```bash
[me@linuxbox ~]$ foo=1
[me@linuxbox ~]$ echo $((foo++))
1
[me@linuxbox ~]$ echo foo
2
```

如果我们给变量赋值1，然后使用放在参数后面的 `++` 运算符对其递增，返回的是值1。然而，如果我们第二次查看变量的值，就会看到增加后的值。如果我们把 `++` 运算符放在参数前面，就能得到更期的行为。

```bash
[me@linuxbox ~]$ foo=1
[me@linuxbox ~]$ echo $((++foo))
2
[me@linuxbox ~]$ echo foo
2
```

### 位运算

一类运算符以异常的方式处理数字。这些运算符在位级上工作。它们用于某些低级任务，通常涉及设置或读取位标志。位运算符列在表 34-5 中。

表 34-5：位运算符

| 运算符 | 描述 |
| --- | --- |
| ~ | 位取反。反转数字的位。 |
| << | 左移。将数字的位向左移动。 |
| >> | 右移。将数字的位向右移动。 |
| & | 位与。对两个数字的所有位执行与逻辑运算。 |
| | | 位或。对两个数字的所有位执行或逻辑运算。 |
| ^ | 位异或。对两个数字的所有位执行异异或逻辑运算。 |

请注意，除了位取反外，所有运算符都有对应的赋值运算符（例如 `<=`）。

# 算术求值与扩展

在这里我们将演示如何使用左位移位运算符生成一个 2 的幂列表：

```
me@linuxbox ~] $ for ((i=0;i<8;++i)); do echo $((1<<i)); done
1
2
4
8
16
32
64
128
```

# 逻辑

正如我们在第 27 章中发现的，`(( ))` 复合命令支持多种比较运算符。还有几个可以用于逻辑评估。表34-6 提供了完整的列表。

表 34-6: 比较运算符

| 运算符 | 描述 |
| :--- | :--- |
| <= | 小于等于。 |
| >= | 大于等于。 |
| < | 小于。 |
| > | 大于。 |
| == | 等于。 |
| != | 不等于。 |
| && | 逻辑与 (AND)。 |
| || | 逻辑或 (OR)。 |
| expr1?expr2:expr3 | 比较（三元）运算符。如果表达式 expr1 求值为非零（算术真），则执行 expr2；否则执行 expr3。 |

当用于逻辑操作时，表达式遵循算术逻辑规则；即：求值为零的表达式被视为假，而非零表达式被视为真。`(( ))` 复合命令将结果映射到 shell 的正常退出状态。

```
me@linuxbox ~]$ if ((1)); then echo "true"; else echo "false"; fi true
me@linuxbox ~]$ if ((0)); then echo "true"; else echo "false"; fi false
```

逻辑运算符中最奇的是三元运算符。该运算符（模仿了 C 语言中的三元运算符）执行一个独立的逻辑测试。它可以作为一种 if/then/else 语句。它作用于三个算术表达式（这种写法不起作用），如果第一个表达式为真（或非零），则执行第二个表达式；否则执行第三个表达式。我们可以在命令行尝试一下：

```
me@linuxbox ~]$ a=0
me@linuxbox ~]$ ((a<1++?-a--))
me@linuxbox ~]$ echo a
1
me@linuxbox ~]$ ((a<1++?-a--))
me@linuxbox ~]$ echo a
0
```

在这里我们看到了三元运算符的用法。这个示例实现了一个切换。每执行一次该运算符，变量的值就会从零切换到一，或反之。

请注意，在表达式内部进行赋值并不是简单的。当尝试这样做时，bash 会报告错误。

```
me@linuxbox ~]$ a=0
me@linuxbox ~]$ ((a<1?a+=1:a=-1))
bash: (: a<1?a+=1:a=-1): attempted assignment to non-variable (error token is "-1")
```

可以通过用括号包围赋值表达式来缓解这个问题。

```
me@linuxbox ~]$ ((a<1?(a+=1):(a=-1)))
```

# 算术求值与扩展

接下来是一个更完整的示例，它在脚本中使用算术运算符生成了一个简单的数字表格。

```bash
#!/bin/bash

# arith-loop: 演示算术运算符的脚本

finished=0
a=0
printf "\a*2\ta*3\n"
printf "\t====\t====\n"

until ((finished)); do
	b=$((a*2))
	c=$((a*3))
	printf "%d\t%d\t%d\n" "$a" "$b" "$c"
	a((a<=10?+:(finished=1)))

done
```

在这个脚本中，我们根据 `finished` 变量的值实现了一个 `until` 循环。初始时，变量设置为零（算术假），持续循环直到它变为非零。在循环内部，我们计算计数器变量 `a` 的平方和立方。在循环结束时，评估计数器的值。如果它小于10（最大迭代次数），则加1，否则给变量 `finished` 赋值为，使其在算术上为真，从而终止循环。运行脚本得到以下结果：

```
[me@linuxbox ~]$ arith-loop
a a**2 a**3
====
0 0 0
1 1 1
2 4 8
3 9 27
4 16 64
5 25 125
6 36 216
7 49 343
8 64 512
9 81 729
10 100 1000
```

# 逗号运算符

我们将看到的最后一个运算符是逗号运算符。它允许我们在评估中放置多个表达式，如下所示：`(( expr, expr, expr ))`。当我们想要将多个操作合并到单个评估中时，可以使用它。为了演示这一点，我们将修改 `arithmetic-loop` 脚本，使用逗号运算符来简化它。
