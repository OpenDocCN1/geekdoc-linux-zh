

# 高级 Bash 脚本指南

有一个名为 `command_not_found_handle` 的新内置错误处理函数。

```bash
#!/bin/bash
command_not_found_handle () {
  # 接收参数。
  echo "The command is not valid: \"\$1\""
  echo "With the following argument (s): \"\$2\" \"\$3\"" # $4, $5, ...
}
# $1, $2 等没有明确传递给函数。
bad_command arg1 arg2
```

输出：
`# The command is not valid: "bad_command"`
`# With the following argument (s): "arg1" "arg2"`

编辑评论

关联数组？协进程？我们曾经熟悉并喜爱的那个精简高效的 Bash 到底去哪儿了？它是否正遭受着（可怕的！）“功能膨胀”，或者可能是由于对 Korn shell 的嫉妒？

给 Chet Ramey 的建议：在未来的 Bash 版本中仅添加本质功能——也许是 `each` 循环和对多维数组的支持。大多数 Bash 用户不需要、不会使用，且可能不会非常欣赏内置调试器、Perl 接口以及附加的火箭助推等“功能”。

## 37.3.1. Bash 4.1 版本

2010 年 5 月发布的 Bash 4.1 版本主要是一个修复 Bug 更新。

- `printf` 命令接受 `-v` 选项来设置数组索引。
- 在双括号内，`>` 和 `<` 字符串比较运算符现在符合区域设置（locale）。由于区域设置可能会影响字符串表达式的排序，这会对 `[[ ... ]]` 内的比较测试产生副作用。
- `read` 内置命令接受 `-N` 选项（`read -N chars`），它会导致读取在达到指定的字符后终止。

示例 37-8. 读取 N 个字符

```bash
#!/bin/bash
# 要求 Bash 版本 -ge 4.1 ...
num_chars=61
read -N $num_chars var < $0 # 读取脚本的前 61 个字符！
echo "$var"
exit
```

脚本输出：
```bash
#!/bin/bash
# Requires Bash version -ge 4.1 ...
num_chars=61
```

第 37 章 Bash 2、3、4 版本

# 高级 Bash 脚本指南

- 嵌入在 `$$( ... )` 命令替换结构中的 **here documents**（在此在此文档）可以使用简单的 `)` 终止。

示例 37-9. 使用 here document 设置变量

```bash
#!/bin/bash
# here-comsub.sh
# 要求 Bash 版本 -ge 4.1

multi_line_var=$(<<END
This is line 1 of the variable
This is line 2 of the variable
This is line 3 of the variable
END
)
# 而 Bash 4.0 要求的是：终止字符串必须单独行。
echo "$multi_line_var"
# 虽然 Bash 仍然会发出警告：文件末尾在此-document。
```

## 37.3.2. Bash 4.2 版本

2011 年2 月发布的 Bash 4.2 版本除了修复 Bug 外还包含了新功能和增强。

- Bash 现在支持 `\x` 和 `\U` Unicode 转义字符，这是一种对数值和图形符号进行编码的跨平台标准。这允许表示和显示外语字母中的字符。

```bash
echo -e '\u2630' # 水平线字符。
# 等同于更复杂的写法：早期 Bash 版本识别。
echo -e '\u2200' # PI（希腊字母和数学符号）
echo -e '\u0416' # 大写 "Z"（西里尔字母）
echo -e '\u2708' # 飞机（Dingbat 字体）
echo -e '\u2622' # 三叶叶草符号——需要 100% 上拉电阻。
```

第 37 章 Bash 2、3、4 版本

# 高级 Bash 脚本指南

```bash
unicode_var='♀'
echo -e "$unicode_var" # 带有换行的女性符号

# 还有更复杂的内容……在关联数组中存储 Unicode 符号，然后通过名称检索它们。
# 在大字体终端中运行此以获得更好的可读性。
declare -A array
array[E]="E"
array[F]="F"
array[J]="J"
array[M]="M"
array[R]="R"
array[T]="T"
array[A]="A"
array[O]="O"
array[C]="C"

echo -n "${array[E]}"
echo -n "${array[F]}"
echo -n "${array[J]}"
echo -n "${array[M]}"
echo -n "${array[R]}"
echo -n "${array[T]}"
echo -n "${array[A]}"
echo -n "${array[O]}"
echo -n "${array[C]}"
```

- 上述示例使用了 `${...}` 字符串扩展。当设置 `lastpipe` 选项时，管道中的最后一个命令不会在子 shell 中运行。

示例 37-10. 将输入管道到 read

```bash
#!/bin/bash
# lastpipe-option.sh

line='' # 空值。
head -l 1 | read line
echo "Exit status of attempting to set lastpipe option is $?"
# 如果 Bash 版本 -lt 4.2，否则为 0。
echo "$line"
```

第 37 章 Bash 2、3、4 版本

# 高级 Bash 脚本指南

## 37-11. 负索引

负索引允许从末尾开始计数。

```bash
#!/bin/bash
# negative-index.sh
# 要求 Bash 版本 -ge 4.2

array=(abcdefg)
echo "${array[-1]}" # g
echo "${array[-3]}" # e
echo "${array: -3:2}" # ef
```

注意：在 Bash 4.2 之前，负索引在字符串扩展中是可用的。如果你在较旧版本中使用，可能需要通过长度计算来索引，例如 `${array[${#array[@]}-1]}`。

## 37-12. 字符串中的负参数

字符串扩展中的负参数允许从字符串的末尾开始计数。

```bash
#!/bin/bash
# string-expansion-negative-param.sh
# 要求 Bash 版本 -ge 4.2

str="abcdefg"
echo "${str: -1}" # g
echo "${str: -3:2}" # ef
```

