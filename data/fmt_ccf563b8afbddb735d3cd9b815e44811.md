
```
real 0.060s
user 0.056s
sys 0.008s
```

脚本原始版本扫描文本文件需要 3.618 秒，而使用参数扩展的新版本仅需 0.06 秒——这是一个非常显著的。

# 算术求值与扩展

我们在第 7 章学习了算术扩展。它用于对整数执行各种算术操作。它的基本形式是

`$((expression))`

其中 `expression` 是一个有效的算术表达式。这与我们在第 27 章遇到的用于算术求值（真值测试）的复合命令 `((` 有关。在之前的章节中，我们看到了一些常见的表达式和运算符类型。在这里，我们将查看更完整的列表。

## 进制

在第 9 章中，我们了解了八进制（8进制）和十六进制（16进制）。在算术表达式中，shell 支持任何进制的整数常量。表 34-1 显示了用于指定进制的记法。

### 表 34-1：指定不同的进制

| 记法 | 说明 |
| --- | --- |
| Number | 默认情况下，没有任何记法的数字被视为十进制（10进制）整数。 |
| Onumber | 在算术表达式中，前导为零的数字被视为八进制。 |
| Oxnumber | 十进制表示 |
| base8number | 数字是进制。 |

一些示例：

```
me@linux ~$ echo $((xff))
255
me@linux ~$ echo $((2#11111111))
255
```

在这些示例中，我们打印十六进制数 `ff`（最大的两位数）和最大的八位二进制（2进制）数。

## 一元运算符

有两个一元运算符 `+` 和 `-`，分别用于表示数字是正还是负的。

## 简单算术

普通的算术运算符列在表 34-1 中。

### 表 34-2：算术运算符

| 运算符 | 说明 |
| --- | --- |
| + | 加法 |
| - | 减法 |
| * | 乘法 |
| / | 整数除法 |
| ** | 幂运算 |
| % | 取模 |

$${parameter}pattern}

${parameter##pattern}

这些扩展会移除 `parameter` 中由 `pattern` 定义的部分字符串。`pattern` 是一个通配符模式，类似于文件名扩展中使用的模式。这两种形式的区别是：`#` 删除最短匹配，而 `##` 形式删除最长匹配。

$${parameter%pattern}

${parameter%%pattern}

这些扩展与上述的 `#` 和 `##` 相同，但它们是从 `parameter` 字符串的结尾删除文本，而不是开头。

```
$${parameter/pattern/string}
${parameter*/pattern/string}
${parameter##pattern/string}
${parameter%%pattern/string}
```

此扩展对 `parameter` 的内容执行搜索并替换。如果找到匹配通配符模式的文本，将其替换为 `string` 的内容。在普通形式下，只替换 `pattern` 的第一次出现。在 `//` 形式下，所有出现的地方都会替换。`#` 形式要求匹配发生在字符串开头，`/%` 要求匹配发生在字符串结尾，`/string` 可以省略，这会导致 `pattern` 被删除。

了解参数扩展是一件很有帮助。字符串处理扩展可以作为 `sed` 和 `cut` 等其他常用命令的替代。扩展通过消除对外部程序的使用，提高了脚本的效率。例如，我们将修改上一章讨论的“最长单词”程序，使用参数扩展

用 `$(#j)` 代替命令替换 `$(echo j | wc -c)` 及其产生的子壳，如下所示：

```bash
#!/bin/bash

# longest-word3 : 在文件中查找最长字符串

for i; do
    if [[ -r i ]]; then
        max_word=
        max_len=
        for j in $(strings i); do
            len=$(#j)
            if (( len > max_len )); then
                max_len=$len
                max_word=$j
            fi
        done
        shift
        echo "$ '$max_word' ($max_len characters)"
    fi
done
```

接下来，我们将使用以下命令比较两个版本的效率：

```
[me@linux]$ time longest-word2 dirlist-usr-bin.txt
dirlist-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)
```

```
real 0.318s
user 0.154s
sys 0.768s
[me@linux]$ time longest-word3 dirlist-usr-bin.txt
dirlist-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)
```

```
real 0.060s
user 0.056s
sys 0.008s
```

脚本原始版本扫描文本文件需要 3.618 秒，而使用参数扩展的新版本仅需 0.06 秒——这是一个非常显著的。

语言，并已被其他几种编程语言吸纳，包括 bash。

运算符可能出现在参数的开头，也可能出现在末尾。虽然它们会将参数增加或减少 1，但这两种放置方式存在细微的。如果放置在参数前面，则会在返回参数之前对参数进行递增（或递减）。如果放置在后面，则会在返回参数后执行操作。这看起来相当奇怪，但这是其预期的行为。示例如所示：

```
me@linux ~$ foo=1
me@linuxbox ~$ echo $((foo))
1
me@linuxbox ~$ echo $foo
```

如果我们把值 1 赋值给变量 `foo`，并使用放在参数名后的 `++` 运算符对其进行递增，返回的 `foo` 值为 1。然而，如果我们第二次查看变量的值，就会看到增加后的值。如果把 `++` 运算符放在参数前面，我们就能得到这种预期的行为：

```
me@linuxbox ~$ foo=1
me@linuxbox ~$ echo $((foo))
2
me@linuxbox ~$ echo $foo
```

对于大多数 shell 应用来说，将运算符作为前缀是最有用的。

`++` 和 `--` 运算符通常与循环配合使用。我们将对取模脚本进行一些改进，使其更加紧凑：
