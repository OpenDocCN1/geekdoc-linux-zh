
```
value is 5 before the function
$1 is 2 before the function
value is 4 within the function
$1 is 5 within the function
value is 5 after the function
$1 is 2 after the function
```

**提示：** 你可以使用 `. ./common.sh` 从当前目录中名为 `common.sh` 的脚本中导入函数。下面显示了一个快速示例。首先是 `test.sh`：

```sh
#!/bin/sh
. ./common.sh
if [ "$1" = "" ]; then
    echo "USAGE:"
    echo "sh test.sh type"
    exit
fi

if validtype $1; then
    echo "Valid type"
else
    echo "Invalid type"
fi
```

## 这是 `common.sh`：

```sh
#!/bin/sh
validtype() {
    if [ "$1" = "TYPEA" ] ||
       [ "$1" = "TYPEB" ] ||
       [ "$1" = "TYPEC" ] ||
       [ "$1" = "TYPED" ] ||
       [ "$1" = "TYPEE" ];
    then
        exit 0
    else
        exit 1
    fi
}
```

# 第十一章：SHELL 基本运算符

每种 Shell 都支持各种运算符。本章基于默认 Shell（`Bourne`），因此我们将在此教程中介绍所有重要的 `Bourne` Shell 运算符。

我们将讨论以下运算符：

- 算术运算符。
- 关系运算符。
- 布尔运算符。
- 字符串运算符。
- 文件测试运算符。

`Bourne` Shell 最初没有执行简单算术的机制，但它使用外部程序，要么是 `awk`，要么是更简单的程序 `expr`。

这是一个添加两个数字的简单示例：

```sh
#!/bin/sh
val=`expr 2 + 2`
echo "Total value : $val"
```

这会产生以下结果：

```
Total value : 4
```

**注意：**

- 运算符和表达式之间必须有空格；例如，`2+2` 不正确，应写为 `2 + 2`。
- 完整的表达式应包含在倒引号（反引号）中。

## 算术运算符

以下是 `Bourne` Shell 支持的算术运算符。

假设变量 `a` 保存 10，变量 `b` 保存 20，那么：

使用所有算术运算符的示例：

### Shell 算术运算示例

以下脚本演示了基本的算术操作：

```sh
#!/bin/sh

a=10
b=20
val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
  echo "a is equal to b"
fi

if [ $a != $b ]
then
  echo "a is not equal to b"
fi
```

输出结果：

```text
a + b : 30
a - b : -10
a * b : 200
b / a : 2
b % a : 0
a is not equal to b
```

注意：

- 操作符和表达式之间必须有空格，例如 `2+2` 是错误的，应写作 `2 + 2`。
- 完整的表达式应被反引号（inverted commas，即 `` ` `` 和 `` ` ``）或引号包围。
- 乘法运算中使用 `\*` 代替 `*` 符号。
- `if...then...fi` 语句是决策语句，将在下一章解释。

算术运算符表：

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `+` | 加法 - 将操作符两侧的值相加 | `expr $a + $b` 结果为 30 |
| `-` | 减法 - 从左手操作数中减去右手操作数 | `expr $a - $b` 结果为 -10 |
| `\*` | 乘法 - 将操作符两侧的值相乘 | `expr $a \* $b` 结果为 200 |
| `/` | 除法 - 左手操作数除以右手操作数 | `expr $b / $a` 结果为 2 |
| `%` | 取模 - 左手操作数除以右手操作数并返回余数 | `expr $b % $a` 结果为 0 |
| `=` | 赋值 - 将右手操作数赋值给左手操作数 | `a=$b` 将 `b` 的值赋给 `a` |
| `==` | 相等 - 比较两个数字，如果相同则返回 `true` | `[ $a == $b ]` 返回 `false` |
| `!=` | 不等 - 比较两个数字，如果不同则返回 `true` | `[ $a != $b ]` 返回 `true` |

请注意，所有条件表达式都必须放在方括号内，且周围需有一个空格，例如 `[ $a == $b ]` 是正确的，而 `[$a== $b]` 是错误的。

所有算术计算均使用长整型（`long` integers）。

## 关系运算符

`Bourne` Shell 支持以下关系运算符，它们仅适用于数值。这些运算符不适用于字符串值，除非其值为数字。例如，以下运算符检查 10 和 20 之间的关系，也检查 "10" 和 "20" 之间的关系，但不检查 "ten" 和 "twenty" 之间的关系。假设变量 `a` 持有 10，变量 `b` 持有 20：

此示例使用了所有关系运算符：

```sh
#!/bin/sh

a=10
b=20

if [ $a -eq $b ]
then
echo "$a -eq $b : a is equal to b"
else
echo "$a -eq $b: a is not equal to b"
fi

if [ $a -ne $b ]
then
echo "$a -ne $b: a is not equal to b"
else
echo "$a -ne $b : a is equal to b"
fi

if [ $a -gt $b ]
then
echo "$a -gt $b: a is greater than b"
else
echo "$a -gt $b: a is not greater than b"
fi

if [ $a -lt $b ]
then
echo "$a -lt $b: a is less than b"
else
echo "$a -lt $b: a is not less than b"
fi

if [ $a -ge $b ]
then
echo "$a -ge $b: a is greater or equal to b"
else
echo "$a -ge $b: a is not greater or equal to b"
fi

if [ $a -le $b ]
then
    echo "$a -le $b: a is less or equal to b"
else
    echo "$a -le $b: a is not less or equal to b"
fi
```

输出结果：

```text
10 -eq 20: a is not equal to b
10 -ne 20: a is not equal to b
10 -gt 20: a is not greater than b
10 -lt 20: a is less than b
10 -ge 20: a is not greater or equal to b
10 -le 20: a is less or equal to b
```

注意：

- 操作符和表达式之间必须有空格，例如 `2+2` 是错误的，应写作 `2 + 2`。
- `if…then…else…fi` 语句是决策语句，将在下一章解释。

关系运算符表：

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `-eq` | 检查两个操作数的值是否相等，如果是则条件为 `true` | `[ $a -eq $b ]` 不为 `true` |
| `-ne` | 检查两个操作数的值是否相等，如果不等则条件为 `true` | `[ $a -ne $b ]` 为 `true` |
| `-gt` | 检查左手操作数的值是否大于右手操作数的值，如果是则条件为 `true` | `[ $a -gt $b ]` 不为 `true` |
| `-lt` | 检查左手操作数的值是否小于右手操作数的值，如果是则条件为 `true` | `[ $a -lt $b ]` 为 `true` |
