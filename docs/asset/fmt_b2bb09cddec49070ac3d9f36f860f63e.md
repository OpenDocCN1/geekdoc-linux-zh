
## 正则表达式

以下 `awk` 命令移除输入字符串中的所有数字：
```bash
$ echo "123a4b5c678" | awk '{ gsub(/[0-9]+/, ""); $0; print }'
```

### 使用 `gsub()` 函数移除字符

以下 `awk` 命令移除作为输入字符串第一个字符的字母 `t`、`h` 或 `e` 之一：
```bash
$ echo "there" | awk '{ gsub(/[the]/, "", $0); print }'
```

以下 `awk` 命令移除作为输入字符串第一个字符的字母 `t` 或 `T` 之一：
```bash
$ echo "there" | awk '{ gsub(/[tT]/, "", $0); print }'
```

以下 `awk` 命令移除作为输入字符串开头的字母 `t` 或 `T`，且其紧跟序列 `"he"`：
```bash
$ echo "there" | awk '{ gsub(/[tT]he/, "", $0); print }'
```

## 226 GREP, SED 和 AWK 快速指南

以下 `awk` 命令使用 `sub()` 函数将字母 `"a"` 的多次出现处替换为 `ABC`：
```bash
$ echo aaaabcd | awk '{ gsub(/[a]+/, "ABC"); print }'
```

### 使用 `gsub()` 函数

`gsub()` 函数允许你执行搜索并替换功能，就像你在第 2 章中学习的 `sed` 命令行工具一样。以下 `awk` 命令使用 `gsub()` 函数将输入字符串中的空格替换为横杠：
```bash
$ echo "a bc" | awk '{ gsub(/ /, "-", $0); print }'
```

以下命令在每对字符之间插入一个横杠：
```bash
$ echo "abc" | awk '{ gsub(/,/, "-", $0); print }'
```

### 使用 `gsub()` 函数移除数字

以下 `awk` 命令移除输入字符串中的数字：
```bash
$ echo "alb2c3" | awk '{ gsub(/[0-9]/, "", $0); print }'
```

以下 `awk` 命令移除输入字符串中的数字 `3` 到 `5`：
```bash
$ echo "alb2c3" | awk '{ gsub(/[3-5]/, "", $0); print }'
```

以下 `awk` 命令移除输入字符串中的第一个数字：
```bash
$ echo "1234b5c678" | awk '{ gsub(/^[0-9]/, "", $0); print }'
```

以下 `awk` 命令移除输入字符串中的所有起始数字：
```bash
$ echo "1234b5c678" | awk '{ gsub(/^[0-9]+/, "", $0); print }'
```

以下 `awk` 命令移除输入字符串中的末尾最后一个数字：
```bash
$ echo "1234b5c678" | awk '{ gsub(/[0-9]$/, "", $0); print }'
```

以下 `awk` 命令移除输入字符串中的所有末尾数字：
```bash
$ echo "1234b5c678" | awk '{ gsub(/[0-9]+$/, "", $0); print }'
```

以下 `awk` 命令通过指定字母 `ae` 作为分隔符来分割输入字符串：
```bash
$ echo "abcdef" | awk -F'ae' '{print $1, "x", $2}'
```

以下 `awk` 命令通过指定字母 `ae` 作为分隔符来分割输入字符串：
```bash
$ echo "aaabcdef" | awk -F'ae' '{print $1, "x", $2}'
```

以下 `awk` 命令通过指定范围 `[a-c]` 作为分隔符来分割输入字符串：
```bash
echo "abcdef" | awk -F'[a-b]' '{print $1, "x", $2}'
```

## 动态正则表达式

动态正则表达式是诸如 `[[:digit:]]` 这样的表达式，它们会被评估，并在需要时转换为字符串。这里列出了一些动态正则表达式：

- `[[:digit:]]` 匹配数字
- `[[:alpha:]]` 匹配大写或小写字母
- `[[:alnum:]]` 匹配字母或数字的字符
- `[[:punct:]]` 匹配标点符号

你可以在网上找到更多信息：https://support.google.com/a/answer/137415?hl=en。

### 列表 6.10: `dynamic_regex1.sh`

```bash
echo "123" | awk '
BEGIN {
  digits_regexp = "[[:digit:]]+"
}
$0 { print }'
```

列表 6.10 包含一个带有 `BEGIN` 块的 `awk` 命令，该块将变量 `digits_regexp` 初始化为一个或多个数字的模式。下一个片段检查 `$0` 是否匹配 `digits_regexp` 中模式，如果是，则打印 `$0` 的内容。运行列表 6.10 中的代码，你将看到以下输出：
```
123
```

### 列表 6.11: `dynamic_regex2.sh`

```bash
echo "abc123" | awk '
BEGIN {
    alpha_regexp = "[[:alpha:]]+"
}
$0 { print }'
```

列表 6.11 包含一个带有 `BEGIN` 块的 `awk` 命令，该块将变量 `alpha_regexp` 初始化为一个或多个字母数字字符的模式。下一个片段检查 `$0` 是否匹配 `alpha_regexp` 中的模式，如果是，则打印 `$0` 的内容。运行列表 6.11 中的代码，你将看到以下输出：
```
abc
```

### 列表 6.12: `dynamic_regex3.sh`

```bash
echo "!@#" | awk '
BEGIN {
    punct_regexp = "[[:punct:]]+"
}
$0 { print }'
```

列表 6.12 包含一个带有 `BEGIN` 块的 `awk` 命令，该块将变量 `punct_regexp` 初始化为一个或多个标点符号的模式。下一个片段检查 `$0` 是否匹配 `punct_regexp` 中的模式，如果是，则打印 `$0` 的内容。运行列表 6.12 中的代码，你将看到以下输出：
```
!@#
```

## 涉及文本文件的正则表达式

前面的章节展示了如何执行许多涉及文本文件的任务。本节包含带有 `awk` 命令的子节，这些命令可以显示匹配字符的行、匹配多个字符的行等。代码示例依赖基本的元字符，例如作为“开头”的 `^`，以及作为 `OR` 运算符的正则表达式 `|` 以及作为 `NOT` 运算符的 `!`。

## 使用正则表达式计数注释

### 列表 6.13: `comments.txt`

```
# this is an awk and Python style comment
// this is C-style comment
x = 1
y = 3
# pound-style comment two
// another C-style comment
# pound-style comment three
// a third C-style comment
/* python style comment */
```

### 列表 6.14: `comments.sh`

```bash
awk '
BEGIN {
  c_count = 0; awk_count = 0;
  c_count2 = 0; awk_count2 = 0
  py_count = 0
}

if($0 ~ /^\/) { awk_count++ }
else if ($0 ~ /\/) { c_count++ }
else if ($0 ~ /\*/) { py_count++ }
else if ($0 ~ /^#/) { awk_count2++ }
else if ($0 ~ /^*\*/) { c_count++ }
END {
  print "C-style comments:",c_count
  print "awk-style comments:",awk_count
  print "C-style comments:",c_count2
  print "awk-style comments:",awk_count2
  print "python-style comments:",py_count
}'
```

列表 6.14 包含一个 `awk` 脚本，`BEGIN` 块初始化了几个标量变量，用于计数不同类型的注释语句。列表 6.14 包含主执行块，包含了 `$0` 中的第一个字符 `"""`、`#` 和 `//`，它们分别是 C、Python、`awk` 和再次的 C 的注释语句。每个条件代码匹配这些字符串时，对应的标量变量递增。列表 6.14 的最后部分包含一个 `END` 块，打印各种标量变量的值。运行列表 6.14 中的代码，你将看到以下输出：
```
C-style comments: 1
awk-style comments: 1
C-style comments: 2
awk-style comments: 2
python-style comments: 1
```

## grep 与 awk

### 列表 6.15: `comments.txt`
