
`at` 允许你调度一次性执行的命令或脚本。时间格式为 HH:MM，后跟可选的 am/pm 标识，日期使用星期或月份的前三个字母写出。关键词“now”和“tomorrow”可以代替时间。如果未提供日期，`at` 使用以下规则：

- 如果时间是当前时间，日期假设为“今天”。
- 如果时间在当前时间之前，日期假设为“明天”。

指定的时间可以增加一个增量，这是一个数字，后跟“minutes”、“hours”、“days”、“weeks”、“months”或“years”。

脚本由 `SHELL` 环境变量指定的 shell 执行，如果没有设置此变量，则使用 Bourne shell。来自脚本 的所有标准输出将通过邮件发送给用户。

这里是一些有效的 `at` 时间格式示例：

```
0934am Sep 18 at.csh
9:34 Sep 18, 1994 at.csh
11:00pm tomorrow at.csh
now + 1 day at.csh
9pm Jan 13 at.csh
10pm Wed at.csh
```

如果你省略了脚本名称，`at` 将显示提示并等待从标准输入输入的命令列表。`-r` 选项从队列中移除指定的作业，`-l` 列出等待中的作业。作业在执行后将从 `at` 队列中移除。

## 可编程的文本处理：awk

`awk` 实用程序扫描一个或多行，并对所有匹配模式模式的行执行操作。这些操作和条件由 awk 程序描述，范围从简单到复杂。

可编程文本处理：awk 109

`awk` 的名字源于其作者姓氏的首字母组合：Aho, Weinberger 和 Kernighan。它从 C 语言中借用了控制结构和语法。如果你已经熟悉 C 语言，那么学习 `awk` 将非常简单。

`awk` 是一个功能非常强大的工具——事实上，它是如此强大以至于甚至有一本关于它的书！因此，我尝试只描述 `awk` 的主要功能和选项：然而，我认为在本节中描述的内容将允许你编写许多实用的 `awk` 程序。3.20 提供了 `awk` 的概览。

```
Utility: awk -Fc [ f fileName ] program {variable=value}*{fileName*}
```

`awk` 是一种可编程的文本处理工具，它扫描输入行，并对每一行匹配特定准的行执行操作。`awk` 程序可以包含在命令行，这种情况下它应该用单引号括起来；或者，也可以存储在文件中并使用 `-f` 选项指定。变量的初始值在命令行上指定。默认字段分隔符是制表符和空格。要覆盖此默认值，请使用 `-F` 选项后跟新的字段分隔符。如果没有指定文件名，`awk` 将从标准输入读取。

图 3.20

`awk` 命令的描述。

### awk 程序

`awk` 程序可以在命令行提供，但更常见的方法是将其放在文本文件中并使用 `-f` 选项指定文件。如果你决定将 `awk` 程序放在命令行上，请用单引号将其括起来。

当 `awk` 读取一行时，它将其拆分为由制表符或空格分隔的字段。字段分隔符可以通过使用 `-F` 选项来覆盖，正如你将在后的章节中看到的那样。`awk` 程序是一个一个或多个如下形式的命令列表：

```
[ condition ] ( \ action \ )
```

其中 `condition` 是以下之一：

- 特殊标记 `BEGIN` 或 `END`
- 涉及逻辑运算符、关系运算符和正则表达式任意组合的表达式

而 `action` 是一个或多个以下类 C 风格语句的列表，以分号结束：

- `if (conditional) statement [ else statement ]`
- `while (conditional) statement`
- `for (expression: conditional; expression) statement`
- `break`
- `continue`
- `variable=expression`
- `print [ list of expressions ] [ > expression ]`
- `printf format [. , list of expressions ] [ > expression ]`
- `next` (跳过当前行上的剩余模式)
- `exit` (跳过当前行的剩余部分)
- `{ list of statements }`

`action` 在每一行匹配 `condition` 时都会执行。如果缺少 `condition`，则对每一行执行 `action`。如果缺少 `action`，则匹配的行将直接发送到标准输出。`awk` 程序中的语句可以使用空格、制表符和换行进行缩进和格式化。

### 访问字段

当前行的第一个字段可以通过 `$1` 访问，第二个字段可以通过 `$2` 访问，依此类推。`$0` 代表整行。内置变量 `NF` 等于当前行的字段数。在接下来的示例中，我在文本文件 `"float"` 上运行了一个简单的 `awk` 程序，以将字段数插入到每行中：

```
$ cat float ...查看原始文件。
Wish I was floating across the sky,
My imagination is strong,
And often visit the days
When everything seemed clear.
Now I wonder what I'm doing here at all...
$ awk '{ print NF, $0 }' ...执行该命令。
9 Wish was floating across the sky,
4 My imagination is strong,
6 And often visit the days
5 When everything seemed clear.
9 Now I wonder what I'm doing here at all...
$ _
```

### Begin 和 End

特殊条件 `BEGIN` 在读取第一行之前触发，特殊条件 `END` 在读取完最后行之后触发。当在 `print` 语句中列出表达式时，它们之间不留空格，并且默认打印换行符。内置变量 `FILENAME` 等于输入文件的名称。在接下来的示例中，我运行了一个程序，显示每行的第一个、第三个和最后一个字段：

```
$ cat awk2 ...查看 awk 脚本。
BEGIN { print "Start of file:", FILENAME }
{ print $1 $3 $NF ...打印第 1、第 3 和最后一个字段。
END { print "End of file" }
$ awk -f awk2 ...执行脚本。
Start of file: float
Wishwas,
Mystrong,
Andoftendays
Whenseemedclear.
Nowwonderall...
$ -
```

### 运算符

在 `print` 语句的表达式之间放置逗号时，会打印一个空格。`awk` 提供了所有通常的 C 语言运算符。内置变量 `NR` 包含当前行号。在下一个示例中，我运行了一个程序，显示 `"float"` 中第 2 到 3 行的第一个、第三个和最后一个字段：

```
$ cat awk3 ...查看 awk 脚本。
NR > 1 && NR < 4 { print NR, $1, $3, $NF }
$ awk -f awk3 ...执行脚本。
2 My is strong,
3 And often days
$ -
```

### 变量

`awk` 支持用户定义变量。不需要声明变量。变量的初始值为零，取决于你如何使用。在下一个示例中，我统计了文件的行数并输出：

```
$ cat float ...查看 awk 脚本。
{ count++ }
END { print "Total lines:", count }
$ awk -f awk4 ...执行脚本。
Total lines: 5
```

### 控制结构

`awk` 支持大多数控制结构。在接下来的示例中，我打印了字段：

```
$ cat float ...查看原始文件。
for (i=1; i<=NF; i++) print i, $i
$ awk -f awk5 ...执行脚本。
1 Wish 2 was 3
```

### 正则表达式

`condition` 可以正则表达式，必须放置在斜杠之间。在下一个示例中，我显示了字符序列：

```
$ cat float ...查看原始文件。
/strong|clear/ { print $0 }
$ awk -f awk6 ...执行脚本。
```

### 条件范围

`condition` 可以由逗号分隔的两个表达式。在这种情况下，`awk` 从第一行到第二个 `condition` 执行 `action`：

```
$ cat float ...查看原始文件。
/strong/, /clear/ { print $0 }
$ awk -f awk7 ...执行脚本。
```

### 字段分隔符

如果字段分隔符不是空格，使用 `-F` 选项指定字符。在下一个示例中，我处理了冒号分隔的字段：
