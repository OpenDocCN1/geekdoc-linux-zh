
## 使用双引号解决字符串中嵌入空格的问题

如果字符串包含嵌入的空格，你可以用双引号（`""`）将该字符串括起来，这样 Shell 会将整个字符串解释为一个实体，而不是多个部分。

例如，如果你在 Shell 程序中如下将值 `abc def`（`abc` 后跟一个空格，再后跟 `def`）分配给名为 `x` 的变量，你会得到一个错误，因为 Shell 会尝试执行 `def` 作为一个独立的命令：

| 命令 | 环境 |
| :--- | :--- |
| `x=abc def` | `pdksh` 和 `bash` |
| `set x=abc def` | `tcsh` |

如果你如下用双引号包围字符串，Shell 会将该字符串作为单个命令执行：

| 命令 | 环境 |
| :--- | :--- |
| `x="abc def"` | `pdksh` 和 `bash` |
| `set x="abc def"` | `tcsh` |

双引号解析字符串内的所有变量。以下是适用于 `pdksh` 和 `bash` 的示例：

```bash
var="test string"
newvar="Value of var is $var"
echo $newvar
```

以下是适用于 `tsh` 的相同示例：

```bash
set var="test string"
set newvar="Value of var is $var"
echo $newvar
```

如果你执行包含前面三行代码的 Shell 程序，你将得到以下结果：

```
Value of var is test string
```

## 使用单引号保留未展开的变量

你可以用单引号（`''`）包围一个字符串，以阻止 Shell 展开变量或解释特殊字符。当用于后者目的时，单引号是一个转义字符，类似于反斜杠，你将在下一节中学习。在这里，你学习如何使用单引号来避免在 Shell 脚本中展开变量。未展开的变量在输出中保持其原始形式。

在下面的示例中，前面示例中的双引号已更改为单引号。

- `pdksh` 和 `bash`：

```bash
var='test string'
newvar='Value of var is $var'
echo $newvar
```

- `tsh`：

```bash
set var = 'test string'
set newvar = 'Value of var is $var'
echo $newvar
```

如果你执行包含这三行代码的 Shell 程序，你将得到以下结果：

```
Value of var is $var
```

如你所见，变量 `var` 在结果中保持其原始格式，而不是被展开。

## 使用反斜杠作为转义字符

正如你之前所学到的，反斜杠（`\`）充当转义字符，阻止 Shell 将随后的字符解释为特殊字符。假设你想将值 `$test` 分配给名为 `var` 的变量。如果你使用以下命令，Shell 会读取特殊字符 `$` 并将 `$test` 解释为变量 `test` 的值。没有值被分配给 `test`；如下所示，一个空值存储在 `var` 中：

| 命令 | 环境 |
| :--- | :--- |
| `var=$test` | `pdksh` 和 `bash` |
| `set var = $test` | `tcsh` |

不幸的是，这个赋值可能适用于 `bash` 和 `pdksh`，但如果你使用 `tcsh`，它会返回未定义变量的错误。使用以下命令正确地将 `$test` 存储在 `var` 中：

| 命令 | 环境 |
| :--- | :--- |
| `var=\$test` | `pdksh` 和 `bash` |
| `set var = '$test'` | `tcsh` |

美元符号前的反斜杠（`\$`）向 Shell 发出信号，将其解释为普通的 `$` 字符，而不赋予其任何特殊含义。你也可以在 `$test` 变量周围使用单引号（`''`）来获得相同的结果。

## 使用反引号用输出替换字符串

你可以使用反引号（`` ` ``）字符向 Shell 发出信号，在执行时用其输出替换一个字符串。当希望将命令执行的结果存储在变量中时，可以在 Shell 程序中使用此特殊字符。例如，如果你想要计算当前目录中名为 `test.txt` 的文件中的行数，并将结果存储在名为 `var` 的变量中，你可以使用以下命令：

| 命令 | 环境 |
| :--- | :--- |
| `var=`wc -l test.txt`` | `pdksh` 和 `bash` |
| `set var = `wc -l test.txt`` | `tcsh` |

## pdksh 和 bash 中表达式的比较

比较值或评估相似数据片段之间的差异——例如文件信息、字符串或数字——是一项被称为*表达式比较*的任务。表达式比较是在 Shell 程序中使用逻辑以完成任务的组成部分。两个运算符（数字或字符串）的逻辑比较方式在不同的 Shell 中略有不同。在 `pdksh` 和 `bash` 中，可以使用名为 `test` 的命令来实现表达式的比较。在 `tcsh` 中，你可以编写一个表达式来完成相同的事情。

以下章节涵盖使用 `pdksh` 或 `bash` Shell 的比较操作。在本章的后面，你将学习如何在 `tcsh` Shell 中比较表达式。

`pdksh` 和 `bash` Shell 语法提供了一个名为 `test` 的命令来比较字符串、数字和文件。`test` 命令的语法如下：

`test` *expression*

或

`[` *expression* `]`

`pdksh` 和 `bash` 以相同的方式处理 `test` 命令的这两种形式。`test` 命令支持以下类型的比较：

- 字符串比较
- 数字比较
- 文件运算符
- 逻辑运算符

## 字符串比较

以下运算符可用于比较两个字符串表达式：

- `=` — 比较两个字符串是否相等
- `!=` — 比较两个字符串是否不相等
- `-n` — 评估字符串长度是否大于零
- `-z` — 评估字符串长度是否等于零

以下是使用这些运算符在名为 `compare1` 的 Shell 程序中比较两个字符串 `string1` 和 `string2` 的一些示例：

```bash
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
fi
if [ $string2 != string1 ]; then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string2"
fi
```

```sh
if [ $string1 ]; then
    echo "string1 is not empty"
else
    echo "string1 is empty"
fi

if [ -n $string2 ]; then
    echo "string2 has a length greater than zero"
else
    echo "string2 has length equal to zero"
fi

if [ -z $string1 ]; then
    echo "string1 has a length equal to zero"
else
    echo "string1 has a length greater than zero"
fi
```

如果您执行 `compare1`，将得到以下结果：

```
string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length greater than zero
```

如果两个字符串的长度不相等，系统会在较短的字符串末尾填充空格以便进行比较。也就是说，如果 `string1` 的值为 `abc` 而 `string2` 的值为 `ab`，那么在比较目的下，`string2` 将被填充一个尾随空格——其值将变为 `"ab "`（在文本中表示为 `ab`）。

## 数字比较

可以使用以下运算符来比较两个数字：

- `-eq`——比较两个数字是否相等
- `-ge`——比较一个数字是否大于或等于另一个数字
- `-le`——比较一个数字是否小于或等于另一个数字
- `-ne`——比较两个数字是否不相等
- `-gt`——比较一个数字是否大于另一个数字
- `-lt`——比较一个数字是否小于另一个数字

以下 shell 程序比较三个数字：`number1`、`number2` 和 `number3`：
