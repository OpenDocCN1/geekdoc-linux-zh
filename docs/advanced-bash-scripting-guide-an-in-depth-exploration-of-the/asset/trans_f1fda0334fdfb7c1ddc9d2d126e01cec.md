

# 第 7 章. 测试

任何相当完整的编程语言都可以测试条件，并根据测试结果执行操作。Bash 引入了 `test` 命令、各种括号和括号运算符以及 `if/then` 结构。

## 7.1. 测试结构

- `if/then` 结构测试一组命令列表的退出状态是否为 0（在 UNIX 环境中，0 表示“成功”），如果是，则执行一个或多个命令。
- 存在一个名为 `[` 的专用命令。它是 `test` 的同义词，出于效率考虑，它是一个内置命令。该命令将其参数视为比较表达式或文件测试，并返回与比较结果对应的退出状态（0 为真，1 为假）。
- 从 2.02 版本开始，Bash 引入了 `[[` 扩展测试命令，它以一种更让其他语言程序员感到熟悉的方式进行比较。注意 `[[` 是一个关键字，而不是命令。

Bash 将 `[[ $a -lt $b ]]` 视为单个元素，并返回一个退出状态。

`(( ))` 和 `let` 结构根据它们评估的算术表达式是否为非零值来返回退出状态。因此，算术扩展结构可用于执行算术比较。

```bash
(( 0 & 1 ))
echo $? # 1 ***
# And so ...
let *num = (( 0 & 1 ))
echo $num # 0
# But ...
let *num = (( 0 & 1 ))
echo $? # 1 ***
```

```bash
(( 200 | 11 ))
echo $? # 0 ***
let *num = (( 200 | 11 ))
echo $num # 1
let *num = (( 200 | 11 ))
echo $? # 0 ***
```

```bash
(( 200 | 11 ))
echo $? # 0 ***
let *num = (( 200 | 11 ))
echo $num # 203
let *num = (( 200 | 11 ))
echo $? # 0 ***
```

"let" 结构返回与双括号算术扩展相同的退出状态。

# 高级 Bash 脚本指南

再次注意，算术表达式的退出状态并不是错误值。

```bash
var=2 (( (var+=2 ))
echo $? # 1
var=2 (( (var+=2 )) echo $var
                                # 不输出 $var!
```

`if` 可以测试任何命令，而不仅仅是包含在括号内的条件。

```bash
if cmp a b /dev/null # 抑制输出。
then echo "Files a and b are identical."
else echo "Files and b differ."
fi

# 非常用的 "if-grep" 结构：
#
if grep -q Bash file
then echo "File contains at least one occurrence of Bash."
fi

word-linux
letter_sequence-inu
if echo $word | grep -q "$letter_sequence"
# grep 的 -q 选项抑制输出。
then
echo "$letter_sequence found in $word"
else
echo "$letter_sequence not found in $word"
fi

if COMMAND_WHOSE_EXIT_STATUS_IS_0_UNLESS_ERROR_OCCURRED
then echo "Command succeeded."
else echo "Command failed."
fi
```

- 这两个示例由 Stéphane Chazels 提供。

# 示例 7-1. 什么是真？

```bash
#!/bin/bash

# 提示：
# 如果你不确定某个条件可能如何求值，
# 请在 if-测试中测试它。

echo
echo "Testing \"*\""
if [ 0 ] # zero
then
echo "0 is true."
else # 0 else ...
echo "0 is false."
fi # 0 is true.

echo
```

# 第 7 章. 测试

# 高级 Bash 脚本指南

```bash
echo "Testing \"1\""
if [ 1 ]      # one
then
    echo "1 is true."
else
    echo "1 is false."
fi
      # 1 is true.
```

```bash
echo
echo "Testing \"-1\""
if [ -1 ]      # minus one
then
    echo "-1 is true."
else
    echo "-1 is false."
fi
      # -1 is true.
```

```bash
echo
echo "Testing \"NULL\""
if [ ]      # NULL (empty condition)
then
    echo "NULL is true."
else
    echo "NULL is false."
fi
      # NULL is false.
```

```bash
echo
echo "Testing \"xyz\""
if [ xyz ]      # string
then
    echo "Random string is true."
else
    echo "Random string is false."
fi
      # Random string is true.
```

```bash
echo
echo "Testing \"\$xyz\""
if [ $xyz ]      # 测试 $xyz 是否为空，但...
      # 它只是一个未初始化的变量
then
    echo "Uninitialized variable is true."
else
    echo "Uninitialized variable is false."
fi
      # Uninitialized variable is false.
```

```bash
echo
echo "Testing \"-n $xyz\""
if [ -n "$xyz" ] # 更加严谨的做法。
then
    echo "Uninitialized variable is true."
else
    echo "Uninitialized variable is false."
fi
      # Uninitialized variable is false.
```

7 章. 测试

# 高级 Bash 脚本指南

```bash
xyz= # 已初始化，但设置为空值。
echo Testing \"-n $xyz\"
if [ -n "$xyz" ]
then
    echo "Null variable is true."
else
    echo "Null variable is false."
fi # Null variable is false.
```

# 什么时候 "false" 是真的？

```bash
echo Testing \"false\"" # 看起来 "false" 只是一个字符串
if [ "false" ]
then
    echo \"false\" is true. # 它测试为真。
else
    echo \"false\" is false.
fi # "false" is true.
```

```bash
echo Testing \"\$false\"" # 再次，未初始化的变量。
if [ "$false" ]
then
    echo \"$false\" is true.
else
    echo \"$false\" is false.
fi # "$false" is false. # 现在我们得到了预期的结果。
```

# 如果测试未初始化的变量 $true 会发生什么？

```bash
exit 0
```

**练习。**

