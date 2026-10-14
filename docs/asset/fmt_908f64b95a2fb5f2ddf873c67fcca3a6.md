
Value of `var` is `$var`

如你所见，变量 `var` 在结果中保持了其原始格式，而不是被扩展。

# 使用反斜杠作为转义字符

正如你所学的，反斜杠（`\`）作为转义字符，停止 shell 将其后的字符解释为特殊字符。假设你想将值 `$test` 赋值给名为 `var` 的变量。如果你使用以下命令，shell 会读取特殊字符 `$` 并将 `$test` 解释为变量 `test` 的值。没有值被赋值给 `test`；`var` 中存储了一个空值，如下：

| 命令 | 环境 |
|---|---|
| `var=$test` | `pdksh` and `bash` |
| `set var=$test` | `tcsh` |

遗憾的是，这种赋值在 `bash` 和 `pdksh` 中可能有效，但如果你在 `tcsh` 中使用它，会返回“undefined-variable”错误。使用以下命令可以将 `$test` 正存储在 `var` 中：

| 命令 | 环境 |
|---|---|
| `var=\$test` | `pdksh` and `bash` |
| `set var = \test` | `tcsh` |

美元符号前的反斜杠（`\$`）指示 shell 将 `$` 解释为普通普通字符，而不赋予它任何特殊含义。你也可以在 `$test` 变量周围使用单引号（`''`）来获得结果。

## 使用反引号替换字符串为输出

你可以使用反引号（`` ` ``）字符来指示 shell 将字符串替换为执行后的输出。这被称为命令替换。当你想要将命令的执行结果存储在变量中，可以在 shell 程序中使用这个特殊字符。例如，如果你想统计当前目录下文件 `test.txt` 的行数并将结果存储在 `var` 中，可以使用以下命令：

| 命令 | 环境 |
|---|---|
| `var=`wc -l test.txt`` | `pdksh` and `bash` |
| `set var = `wc -1 test.txt`` | `tcsh` |

# pdksh 和 bash 中表达式的比较

比较值或评估相似数据片段之间的差异——例如文件信息、字符串或数字——是一项被称为表达式比较的任务。表达式比较是在 shell 程序中使用逻辑来完成任务的不可或缺的一部分。两个逻辑操作符（数字或字符串）的逻辑比较在不同的 shell 中略有不同。在 `pdksh` 和 `bash` 中，可以使用名为 `test` 的命令来实现表达式的比较。在 `tcsh` 中，你可以编写一个表达式来实现相同的功能。

本节涵盖了使用 `pdksh` 或 `bash` shell 时的比较操作。在随后的章节中，你将学习如何在 `tcsh` shell 中比较表达式。

`pdksh` 和 `bash` 语法提供了名为 `test` 的命令来比较字符串、数字和文件。`test` 命令的语法如下：

```
test expression
or
[ expression ]
```

两种形式的 `test` 命令都被 `pdksh` 和 `bash` 以相同的方式处理。`test` 命令支持以下类型的比较：

- 字符串比较
- 数字比较
- 文件操作符
- 逻辑操作符

## 字符串比较

你可以使用以下运算符比较两个字符串表达式：

- `=` 比较两个字符串是否相等
- `!=` 比较两个字符串是否相等
- `-n` 评估字符串长度是否大于零
- `-z` 评估字符串长度是否为零

接下来是在比较字符串 `string1` 和 `string2` 时使用这些操作符的示例，名为 `compare` 的程序：

```bash
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
fi
if [ $string2 != $string1 ]; then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string2"
fi
if [ $string1 ]; then
    echo "string1 is not empty"
else
    echo "string1 is empty"
fi
if [ -n $string2 ]; then
    echo "string2 has length greater than zero"
else
    echo "string2 has length equal to zero"
fi
```

```bash
if [ -z $string1 ]; then
    echo "string1 has length equal to zero"
else
    echo "string1 has length greater than zero"
fi
```

如果你执行 `compare`，得到以下结果：

`string1 not equal to string2`

`string2 not equal to string1`

`string1 is not empty`

`string2 has length greater than zero`

`string1 has length greater than zero`

如果两个字符串的大小不等，系统会填充较短的字符串进行比较。也就是说，如果 `string1` 的值为 `"abc"` 而 `string2` 的值为 `"ab"`，为了比较，`string2` 会填充为 `"ab "`（带有空格）。

## 数字比较

可以使用以下运算符比较数字：

- `-eq` 比较两个数字是否相等
- `-ge` 比较一个数字是否大于等于另一个数字
- `-le` 比较一个数字是否小于等于另一个数字
- `-ne` 比较两个数字是否不等
- `-gt` 比较一个数字是否大于另一个数字
- `-lt` 比较一个数字是否小于另一个数字

以下 shell 程序比较三个数字 `number1`, `number2` 和 `number3`：

```bash
#!/bin/sh
number1=5
number2=10
number3=5
if [ $number1 -eq $number3 ]; then
    echo "number1 is equal to number3"
else
    echo "number1 is not equal to number3"
fi

if [ $number2 -ge $number1 ]; then
    echo "number2 is greater or equal to number1"
else
    echo "number2 is less than number1"
fi

if [ $number3 -le $number2 ]; then
    echo "number3 is less or equal to number2"
else
    echo "number3 is greater than number2"
fi

if [ $number1 -ne $number2 ]; then
    echo "number1 is not equal to number2"
else
    echo "number1 is equal to number2"
fi

if [ $number2 -gt $number3 ]; then
    echo "number2 is greater than number3"
else
    echo "number2 is not greater than number3"
fi

if [ $number3 -lt $number2 ]; then
    echo "number3 is less than number2"
else
    echo "number3 is not less than number2"
fi
```

（注：数字比较程序的 OCR 文本是碎片化的；我根据提供的操作符和上下文重建了逻辑。）

# 编写和执行 Shell 脚本 253

# 使用 tcsh 比较表达式

与之前，`tcsh` 中比较表达式的方法与 `pdsh` 和 `bash` 下使用的方法不同。本节演示的比较使用了 `tcsh` shell 环境所需的语法。

## 文件操作符

你可以使用以下运算符作为文件比较：

- `-d` 确定一个文件是否为目录
- `-f` 确定一个文件是否为普通文件
- `-r` 确定文件是否设置了读取权限
- `-s` 确定文件是否存在且长度大于零

```
dirl is a directory
filel is a regular file
filel has read permission
filel does not have write permission
dirl has execute permission
```

## 逻辑操作符

你使用逻辑操作符通过布尔逻辑比较表达式——即使用代表 NOT、AND 和 OR 的字符来比较值：

- `!` 取反逻辑表达式
- `-a` 逻辑与两个逻辑表达式
- `-o` 逻辑或两个逻辑逻辑表达式
