
```
${parameter/pattern/string}
${parameter//pattern/string}
${parameter/#pattern/string}
${parameter/%pattern/string}
```

此扩展对 `parameter` 的内容执行搜索并替换。如果找到与通配符 `pattern` 匹配的文本，则将其替换为 `string` 的内容。在普通形式中，仅替换 `pattern` 的第一次出现。在 `//` 形式中，替换所有出现。 `/#` 形式要求匹配发生在字符串的开头，而 `/%` 形式要求匹配发生在字符串的末尾。 `/string` 可以省略，这会导致 `pattern` 匹配的文本被删除。

```
[me@linuxbox ~]$ foo.JPG.JPG
[me@linuxbox ~]$ echo ${foo/JPG/jpg}
jpg.JPG
[me@linuxbox ~]$ echo ${foo//JPG/jpg}
jpg.jpg
[me@linuxbox ~]$ echo ${foo/#JPG/jpg}
JPG.JPG
[me@linuxbox ~]$ echo ${foo/%JPG/jpg}
JPG.jpg
```

参数扩展是一个值得了解的好东西。字符串操作扩展可以用作其他常见命令如 `sed` 和 `cut` 的替代品。扩展通过消除外部程序的使用来提高脚本的效率。作为示例，我们将修改上一章中讨论的最长单词程序，以使用参数扩展 `${#j}` 代替命令替换 `$(echo $j | wc -c)` 及其产生的子 shell，如下所示：

```
#!/bin/bash

# longest-word3 : find longest string in a file

for i; do
    if [[ -r $i ]]; then
        max_word=
        max_len=
        for j in $(strings $i); do
            len=${#j}
            if (( len > max_len )); then
                max_len=$len
                max_word=$j
            fi
        done
        echo "$1: '$max_word' ($max_len characters)"
    fi
    shift
done
```

接下来，我们将使用 `time` 命令比较两个版本的效率：

```
[me@linuxbox ~]$ time longest-word2 dirlist-usr-bin.txt
dirlist-usr-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)

real 0m3.618s
user 0m1.544s
sys 0m1.768s
[me@linuxbox ~]$ time longest-word3 dirlist-usr-bin.txt
dirlist-usr-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)

real 0m0.060s
user 0m0.056s
sys 0m0.008s
```

脚本的原始版本扫描文本文件需要 3.618 秒，而使用参数扩展的新版本仅需 0.06 秒——这是一个非常显著的改进。

## 大小写转换

最近版本的 `bash` 支持字符串的大小写转换。`bash` 有四种参数扩展和两个 `declare` 命令选项来支持它。

那么大小写转换有什么用呢？除了明显的美观价值外，它在编程中也有重要作用。让我们考虑数据库查找的例子。想象一下，用户在我们想要在数据库中查找的数据输入字段中输入了一个字符串。用户可能会以全大写字母或小写字母或两者组合输入该值。我们当然不想用每一种可能的上下大小写拼写变体来填充我们的数据库。那怎么办？

解决这个问题的常见方法是规范化用户的输入。也就是说，在我们尝试数据库查找之前，将其转换为标准化形式。我们可以通过将用户输入中的所有字符转换为小写或大写来实现这一点，并确保数据库条目以相同的方式进行规范化。

`declare` 命令可用于将字符串规范化为大写或小写。使用 `declare`，我们可以强制变量始终包含所需格式，无论分配给它的内容如何：

```
#!/bin/bash

# ul-declare: demonstrate case conversion via declare

declare -u upper
declare -l lower

if [[ $1 ]]; then
    upper="$1"
    lower="$1"
    echo $upper
    echo $lower
fi
```

在上面的脚本中，我们使用 `declare` 创建了两个变量 `upper` 和 `lower`。我们将第一个命令行参数（位置参数 1）的值分配给这两个变量，然后将其显示在屏幕上：

```
[me@linuxbox ~]$ ul-declare aBc
ABC
abc
```

正如我们所见，命令行参数（"aBc"）已被规范化。

有四种参数扩展执行大小写转换：

### 表 34-1：大小写转换参数扩展

| 格式 | 结果 |
|---|---|
| `${parameter,,}` | 将 `parameter` 的值扩展为全小写。 |
| `${parameter,}` | 将 `parameter` 的值扩展，仅将第一个字符更改为小写。 |
| `${parameter^^}` | 将 `parameter` 的值扩展为全大写字母。 |
| `${parameter^}` | 将 `parameter` 的值扩展，仅将第一个字符转换为大写（大写化）。 |

下面是一个演示这些扩展的脚本：

```
#!/bin/bash

# ul-param - demonstrate case conversion via parameter expansion
if [[ $1 ]]; then
    echo ${1,,}
    echo ${1,}
    echo ${1^^}
    echo ${1^}
fi
```

以下是脚本的运行情况：

```
[me@linuxbox ~]$ ul-param aBc
abc
aBc
ABC
ABc
```

再次，我们处理第一个命令行参数并输出参数扩展支持的四种变体。虽然此脚本使用第一个位置参数，但参数可以是任何字符串、变量或字符串表达式。

## 算术求值与扩展

我们在第 7 章中研究了算术扩展。它用于对整数执行各种算术运算。其基本形式为：

`$((expression))`

其中 `expression` 是一个有效的算术表达式。

这与用于算术求值（真值测试）的复合命令 `(( ))` 相关，我们在第 27 章中遇到过。

在之前的章节中，我们看到了一些常见的表达式和运算符类型。在这里，我们将查看一个更完整的列表。

### 数字进制

在第 9 章中，我们了解了八进制（基数 8）和十六进制（基数 16）数字。在算术表达式中，shell 支持任意进制的整数常量。

表 34-2：指定不同的数字进制

| 记法 | 描述 |
|---|---|
| *number* | 默认情况下，没有任何记法的数字被视为十进制（基数 10）整数。 |
| *0number* | 在算术表达式中，以零开头的数字被视为八进制。 |
| *0xnumber* | 十六进制记法 |
| *base#number* | *number* 以 *base* 为进制 |

一些示例：

```
[me@linuxbox ~]$ echo $((0xff))
255
[me@linuxbox ~]$ echo $((2#11111111))
255
```

在上面的示例中，我们打印十六进制数字 `ff`（最大的两位数字）的值和最大的八位二进制（基数 2）数字。

### 一元运算符

有两个一元运算符，`+` 和 `-`，分别用于表示数字是正数还是负数。例如，`-5`。

### 简单算术

普通的算术运算符列在下表中：

表 34-3：算术运算符

| 运算符 | 描述 |
|---|---|
| `+` | 加法 |
| `-` | 减法 |
| `*` | 乘法 |
| `/` | 整数除法 |
| `**` | 指数运算 |
| `%` | 取模（余数） |

其中大多数都是不言自明的，但整数除法和取模需要进一步讨论。

由于 shell 的算术运算只作用于整数，除法结果始终为整数：

```
[me@linuxbox ~]$ echo $(( 5 / 2 ))
2
```

这使得在除法运算中确定余数变得更加重要：

```
[me@linuxbox ~]$ echo $(( 5 % 2 ))
1
```

通过使用除法和取模运算符，我们可以确定 5 除以 2 的结果为 2，余数为 1。

计算余数在循环中很有用。它允许在循环执行期间的指定间隔执行操作。在下面的示例中，我们显示一行数字，并突出显示每个 5 的倍数：
