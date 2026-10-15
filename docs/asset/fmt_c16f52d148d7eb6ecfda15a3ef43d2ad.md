
the priority works the other way: these metacharacters have a higher precedence than concatenation. In some languages, precedence goes left to right, or right

在某些语言中，优先级是从左到右的，或者从右到左。

```bash
the priority works the other way: these metacharacters have a higher precedence than concatenation. In some languages, precedence goes left to right, or right
```

在某些语言中，优先级是从左到右的，或者从右到左。

```
the priority works the other way: these metacharacters have a higher precedence than concatenation. In some languages, precedence goes left to right, or right
在某些语言中，优先级是从左到右的，或者从右
到左。
```

Here we would match sequences as "*&!!&*" as well as the more familiar palindromes.

在这里，我们将匹配诸如 "*&!!&*" 这样的序列以及更熟悉的回文。

A more practical example would be searching for any repeated adjacent strings to-trap common typing errors as "the the". Consider:

一个更实用的例子是搜索任何重复的相邻字符串，以捕获如 "the the" 等常见的输入错误。考虑：

`grep -f '\(.*\)\1' essay`

The tagged expression `..*` matches any string with at least one character. The whole pattern therefore matches "xxxx xxxx" and so on. Note that the expression `\n` can be used anywhere in the pattern, even before the nth tagged expression occurs.

标记表达式 `..*` 匹配任何至少包含字符的字符串。因此，整个模式匹配 "xxxx xxxx" 等。注意，表达式 `\n` 可以用于模式中的任何地方，甚至在第 $n$ 个标记表达式出现之前。例如：

```
'\2\1\(.\)\.\.(.)'
```

![](img/0aad0e0ec0359d5e535f4b2e4c2df9e9_310_0.png)

# 第十四章

是合法的。这将匹配："xyxy"、"abba" 等。原因是 grep（此处指逻辑）会扫描整个模式，并预先知道所有标记表达式的位置。

# THE FGREP 命令

`fgrep` 是 `grep` 的简化版本，仅用于搜索固定字符串。`fgrep` 不允许正则表达式，但它通过两种方式弥补了这一缺陷：第一，它比 `grep` 快得多，特别是在处理大文件时；第二，你可以在一个 `fgrep` 命令中包含任意数量的搜索字符串。这些字符串既可以在命令行中输入（用换行符分隔），也可以存储在表达式文件中（这就是名字 `fgrep`: file grep 的来源，尽管有些地方认为是 fast grep）。你将表达式文件名作为参数提供，`fgrep` 会逐行从中提取模式字符串。`fgrep` 是并行搜索，因此每一行都会与给定的每个字符串进行匹配扫描。让我们来看看语法：

```
fgrep [options] 'strings' [-f expfile] [filenames] >out_file
```

`fgrep` 的选项与 `grep` 的选项略有不同。`-h`, `-b`, `-c`, `-i`, `-y`, `-n` 和 `-v` 的作用都与 `grep` 相同。`-s` 选项（抑制错误消息）在 `fgrep` 中不可用，但 `fgrep` 有一个 `grep` 没有的 `-x` 选项。`-x` 选项将匹配限制在精确的整行匹配上。

一个很好的应用是简单的、个性化的拼写检查器。我们都有经常会写错的“问题”单词。你可以使用你经常使用的错误词汇创建一个包含此类单词的文件，每行一个。然后你让 `fgrep` 检查你的文章：

```bash
$ cat mywatch.words
superde
abreviate
alimoney
allimony
allimony
committee
embarrassment
over
```

```
$ fgrep -x -f mywatch.words essay
```

这将匹配："xyxy"、"abba" 等。

# grepping, sed, and awk

289: 已经被 C++ 取代。这意味着

36: Fortran/awk 结束了。你也可以直接在命令行中输入多个搜索字符串：

```bash
$ fgrep -c 'Unix'
> AIX
> chap
```

注意，你必须以引号（单引号或双引号）开头，在每个搜索条目后输入换行，最后在输入文件名之前关闭引号。记住 `fgrep` 不允许使用正则表达式进行花哨搜索。它的主要应用是快速在文件中搜索多个单词。对于一个大型表达式文件，`fgrep` 在消化内容时会有一个明显的初始停顿，但随后的搜索与字符串的数量无关。

# THE EGREP 命令

`grep` 家族的最后一个成员是 `egrep`（代表 exponential）。`egrep` 允许使用 `-f` 选项。然而，与 `fgrep` 不同，`egrep` 使用正则表达式。表14.1: 正则表达式优先级

| REGULAR EXPRESSION | MATCHES |
| :--- | :--- |
| r* | Zero or more of r |
| r+ | One or more of r |
| r? | Zero or one of r |
| r1\|r2 | Either r1 or r2 |
| (r1\|r2)* | Either r1 or r2 repeated |
| (r1\|r2)+ | Either r1 or r2 repeated one or more times |

# 谁决定优先级？

在某些语言中，优先级是从左到右的，或者从右到左...

# 292 第十四章
