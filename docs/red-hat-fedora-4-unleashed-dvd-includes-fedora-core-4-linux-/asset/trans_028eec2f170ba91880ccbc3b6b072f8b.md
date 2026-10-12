
## 使用双引号解析字符串中的嵌入空格

如果字符串中包含嵌入的空格，你可以用双引号（"）将字符串括起来，这样 shell 就会将整个字符串视为一个实体，而不是多个实体。

例如，如果你在 shell 程序中使用以下方法将 abc def（即 abc 后跟一个空格，再后跟 def）的值赋给名为 x 的变量，你将得到一个错误，因为 shell 会尝试将 def 作为单独的命令执行：

| 命令 | 环境 |
| --- | --- |
| x=abc def | pdksh 和 bash |
| set x=abc def | tcsh |

如果你像下面那样用双引号将字符串括起来，shell 会将该字符串作为单个命令执行：

| 命令 | 环境 |
| --- | --- |
| x="abc def" | pdksh 和 bash |
| set x="abc def" | tcsh |

双引号会解析字符串内的所有变量。以下是 pdksh 和 bash 的一个示例：

```bash
var="test string"
newvar="Value of var is $var"
echo $newvar
```

以下是 tcsh 的相同示例：

```
set var="test string"
set newvar="Value of var is $var"
echo $newvar
```

如果你执行一个包含以上三行的 shell 程序，你会得到以下结果：

Value of var is test string

## 使用单引号保持变量未展开

你可以用单引号（'）将字符串括起来，以阻止 shell 展开变量和解释特殊字符。当用于后者目的时，单引号是一个*转义字符*，类似于你在下一节中学习的反斜杠。在这里，你将学习如何使用单引号避免在 shell 脚本中展开变量。未展开的变量在输出中保持其原始形式。

在以下示例中，前面示例中的双引号已更改为单引号：

pdksh 和 bash：

```bash
var='test string'
newvar='Value of var is $var'
echo $newvar
```

tcsh：

```
set var = 'test string'
set newvar = 'Value of var is $var'
echo $newvar
```

如果你执行一个包含这三行的 shell 程序，你会得到以下结果：

```
Value of var is $var
```

如你所见，变量 var 在结果中保持了其原始格式，而不是被展开。

## 使用反斜杠作为转义字符

如前所述，反斜杠（\）充当转义字符，阻止 shell 将后续字符解释为特殊字符。假设你想将值 $test 赋给名为 var 的变量。如果使用以下命令，shell 会读取特殊字符 $，并将 $test 解释为变量 test 的值。由于没有给 test 赋值，var 中存储的是一个空值，如下所示：

| 命令 | 环境 |
| --- | --- |
| var=$test | pdksh 和 bash |
| set var=$test | tcsh |

不幸的是，这个赋值操作可能适用于 bash 和 pdksh，但如果你在 tcsh 中使用，它会返回“未定义变量”错误。使用以下命令可以正确地在 var 中存储 $test：

| 命令 | 环境 |
| --- | --- |
| var=\$test | pdksh 和 bash |
| set var = \$test | tcsh |

美元符号（\$）前的反斜杠提示 shell 将 $ 解释为与普通字符相同的含义，不要赋予其任何特殊意义。你也可以在 $test 变量周围使用单引号（'）来获得相同的结果。

## 使用反引号用输出替换字符串

你可以使用反引号（`` ` ``）字符提示 shell 在执行时用其输出替换字符串。这个特殊字符可用于 shell 程序中，当你希望将命令执行的结果存储在变量中时使用。例如，如果你想统计当前目录中名为 test.txt 文件的行数，并将结果存储在名为 var 的变量中，你可以使用以下命令：

| 命令 | 环境 |
| --- | --- |
| var=`wc -l test.txt` | pdksh 和 bash |
| set var = `wc -l test.txt` | tcsh |

## pdksh 和 bash 中的表达式比较

比较值或评估相似数据块（例如文件信息、字符串或数字）之间的差异被称为*表达式比较*。表达式比较是使用逻辑在 shell 程序中完成任务的重要组成部分。两个运算符（数字或字符串）的逻辑比较方式在不同 shell 中略有不同。在 pdksh 和 bash 中，可以使用名为 test 的命令来实现表达式比较。在 tcsh 中，你可以编写一个表达式来完成同样的事情。

以下章节介绍了使用 pdksh 或 bash shell 进行比较操作。在本章的后半部分，你将学习如何在 tcsh shell 中比较表达式。

pdksh 和 bash shell 语法提供了一个名为 test 的命令，用于比较字符串、数字和文件。test 命令的语法如下：

```
test expression
```

或者

```
[ expression ]
```

pdksh 和 bash 以相同的方式处理这两种形式的 test 命令。test 命令支持以下类型的比较：

- 字符串比较
- 数字比较
- 文件运算符
- 逻辑运算符

### 字符串比较

以下运算符可用于比较两个字符串表达式：

- `==`——比较两个字符串是否相等
- `!=`——比较两个字符串是否不相等
- `-n`——评估字符串长度是否大于零
- `-z`——评估字符串长度是否等于零

接下来是一些在名为 *compare1* 的 shell 程序中使用这些运算符比较两个字符串 *string1* 和 *string2* 的示例：

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

如果你执行 compare1，你会得到以下结果：

- string1 not equal to string2
- string2 not equal to string1
- string1 is not empty
- string2 has a length greater than zero
- string1 has a length greater than zero

如果两个字符串大小不相等，系统会用尾部空格填充较短的字符串以便进行比较。也就是说，如果 string1 的值为 abc，而 string2 的值为 ab，那么为了比较目的，string2 将填充一个尾部空格——它将具有值 ab（注意：原文此处可能有误，通常 abc 比 ab 长，填充的是较短的 ab，使其变为 "ab " 以便与 "abc" 比较，或者原文意指较短字符串被填充。根据上下文 "pads out the shorter string"，应该是 ab 被填充为 "ab "。但原文说 "it will have a value of ab" 可能是笔误或指填充后用于比较的形式。翻译保留原意：它将具有值 ab [填充后的状态]）。

*更正：根据原文逻辑 "if the value of string1 is abc and that of string2 is ab, string2 will be padded with a trailing space for comparison purposes—it will have a value of ab." 这里原文表述略显奇怪，通常填充后 ab 变成 "ab "。我将忠实翻译原文。*

### 数字比较

以下运算符可用于比较两个数字：

- -eq——比较两个数字是否相等
- -ge——比较一个数字是否大于或等于另一个数字
- -le——比较一个数字是否小于或等于另一个数字
- -ne——比较两个数字是否不相等
- -gt——比较一个数字是否大于另一个数字
- -lt——比较一个数字是否小于另一个数字

以下 shell 程序比较三个数字，number1、number2 和 number3：

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

if [ $number1 -ne $number2 ]; then
    echo "number1 is not equal to number2"
else
    echo "number1 is equal to number2"
fi

if [ $number1 -gt $number2 ]; then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
fi

if [ $number1 -ge $number3 ]; then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
fi

if [ $number1 -lt $number2 ]; then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
fi

if [ $number1 -le $number3 ]; then
    echo "number1 is less than or equal to number3"
else
    echo "number1 is not less than or equal to number3"
fi
```

当你执行该 shell 程序时，你会得到以下结果：

- number1 is equal to number3
- number1 is not equal to number2
- number1 is not greater than number2
- number1 is greater than or equal to number3
- number1 is less than number2
- number1 is less than or equal to number3

### 文件运算符

以下运算符可用作文件比较运算符：

- -d——确定文件是否是一个目录
- -f——确定文件是否是一个普通文件
- -r——确定文件是否设置了读权限
- -s——确定文件是否存在且长度大于零
- -w——确定文件是否设置了写权限
- -x——确定文件是否设置了执行权限

假设有一个名为 compare3 的 shell 程序位于一个目录中，该目录当前目录下有一个名为 file1 的文件和一个名为 dir1 的子目录。假设 file1 的权限为

