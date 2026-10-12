

你会得到以下结果：

```
Number of parameters is 2
Program name is myprog2
Parameters as a single string is Sanjiv Guha
```

## 特殊字符

某些字符在 Linux Shell 中具有特殊含义，因此将它们用作变量名或字符串的一部分会导致程序行为异常。如果字符串中包含这些字符，你还必须使用转义字符（反斜杠）来表示这些特殊字符不应被当作特殊字符处理。表 25.2 中展示了一些这样的字符。

**表 25.2 特殊 Shell 字符**

| 字符 | 说明 |
| :--- | :--- |
| $ | 表示 Shell 变量名的开始 |
| \| | 将标准输出通过管道传输到下一个命令 |
| # | 开始一个注释 |
| & | 在后台执行进程 |
| ? | 匹配一个字符 |
| * | 匹配一个或多个字符 |
| > | 输出重定向运算符 |
| < | 输入重定向运算符 |
| ` | 命令替换（反引号或回格符——大多数键盘上 Tab 键上方的键） |
| >> | 输出重定向运算符（用于追加到文件） |
| << | 等待直到后续输入结束字符串（`HERE` 运算符） |
| [ ] | 列出一组字符范围 |
| [a-z] | a 到 z 的所有字符 |
| [a,z] | 字符 a 或 z |
| . `filename` | 执行（“来源”）文件 `filename` |
| 空格 | 两个单词之间的分隔符 |

有几个字符值得特别说明。它们是双引号（`"`）、单引号（`'`）、反斜杠（`\`）和反引号（`` ` ``），将在以下各节中讨论。请注意，你也可以在 Shell 脚本内部使用输入和输出重定向。在测试你的 Shell 程序时，请务必小心使用输出重定向，因为很容易覆盖文件！

## 双引号

如果字符串包含嵌入式空格，你可以用双引号（`"`）包围该字符串，以便 Shell 将整个字符串解释为一个实体，而不是多个部分。例如，如果你在 Shell 程序中将 abc_def（abc 后跟一个空格，再后跟 def）的值分配给名为 x 的变量，如下所示，你会得到一个错误，因为 Shell 会尝试将 def 作为单独的命令执行。

| 命令 | 环境 |
| --- | --- |
| x=abc def | pdksh 和 bash |
| set x = abc def | tcsh |

你需要做的是用双引号包围字符串：

| 命令 | 环境 |
| --- | --- |
| x="abc def" | pdksh 和 bash |
| set x = "abc def" | tcsh |

双引号会解析字符串内的所有变量。以下是 pdksh 和 bash 的示例：

```
var="test string" 
newvar="Value of var is $var" 
echo $newvar
```

以下是 tcsh 的相同示例：

```
set var = "test string" 
set newvar = 'Value of var is $var' 
echo $newvar
```

如果你执行包含这三行的 Shell 程序，你会得到以下结果：

Value of var is test string

## 单引号

你可以用单引号（`'`）包围字符串，以阻止 Shell 解析变量。在以下示例中，前面示例中的双引号已更改为单引号。

pdksh 和 bash：

```
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

如果你执行包含这三行的 Shell 程序，你会得到以下结果：

Value of var is $var

正如所见，变量 var 没有被插值。

## 反斜杠

你可以在字符前使用反斜杠（`\`）来阻止 Shell 将后续字符解释为特殊字符。假设你想将值 $test 分配给名为 var 的变量。如果你使用以下命令，var 中存储的是一个空值：

| 命令 | 环境 |
| --- | --- |
| var=$test | pdksh 和 bash |
| set var = $test | tcsh |

这是因为 Shell 将 $test 解释为变量 test 的值。由于没有给 test 赋值，所以 var 包含空值。你应该使用以下命令来正确地将 $test 存储在 var 中：

| 命令 | 环境 |
| --- | --- |
| var=\$test | pdksh 和 bash |
| set var = \$test | tcsh |

美元符号（`$`）前的反斜杠（`\`）指示 Shell 将 $ 解释为其他普通字符，而不赋予其任何特殊含义。

## 反引号

你可以使用反引号（`` ` ``）字符来指示 Shell 执行由反引号包围的字符串。当希望将命令执行的结果存储在一个变量中时，这在 Shell 程序中非常有用。例如，如果你想计算当前目录中名为 test.txt 文件中的行数，并将结果存储在名为 var 的变量中，可以使用以下命令：

| 命令 | 环境 |
| --- | --- |
| var=`wc -l test.txt` | pdksh 和 bash |
| set var = `wc -l test.txt` | tcsh |

# 第四部分

## 表达式比较

两个操作符（数值或字符串）的逻辑比较方式在不同的 Shell 中略有不同。在 `pdksh` 和 `bash` 中，可以使用名为 **test** 的命令来实现表达式比较。在 `tcsh` 中，你可以编写表达式来完成同样的事情。

### `pdksh` 和 `bash`

本节介绍使用 `pdksh` 或 `bash` Shell 进行的比较。在本章的后半部分，**“tcsh”** 部分包含对 `tcsh` Shell 的类似讨论。

**test** 命令的语法如下：

```
test expression
或
[ expression ]
```

两种形式的 **test** 命令在 `pdksh` 和 `bash` 中的处理方式相同。**test** 命令支持以下类型的比较：

- 字符串比较
- 数值比较
- 文件运算符
- 逻辑运算符

### 字符串比较

以下运算符可用于比较两个字符串表达式：

| 运算符 | 描述 |
| -------- | ----------- |
| `=` | 用于比较两个字符串是否相等 |
| `!=` | 用于比较两个字符串是否不相等 |
| `-n` | 用于评估字符串长度是否大于零 |
| `-z` | 用于评估字符串长度是否等于零 |

接下来是一些在名为 **compare1** 的 Shell 程序中将两个字符串 `string1` 和 `string2` 进行比较的示例：

```shell
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

string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length greater than zero

如果两个字符串大小不相等，系统会在较短的字符串末尾填充空格以便进行比较。也就是说，如果 string1 的值是 abc，而 string2 的值是 ab，那么 string2 会在末尾填充一个空格以便进行比较——它的值将是 ab（后跟一个空格）。

### 数值比较

以下运算符可用于比较两个数值：

- -eq 用于比较两个数值是否相等
- -ge 用于比较一个数值是否大于或等于另一个数值
- -le 用于比较一个数值是否小于或等于另一个数值
- -ne 用于比较两个数值是否不相等
- -gt 用于比较一个数值是否大于另一个数值
- -lt 用于比较一个数值是否小于另一个数值

以下示例在名为 compare2 的 Shell 程序中对两个数值 number1 和 number2 进行比较：

```
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

当你执行 Shell 程序 compare2 时，你会得到以下结果：

```
number1 is equal to number3
number1 is not equal to number2
number1 is not equal to number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3
```

