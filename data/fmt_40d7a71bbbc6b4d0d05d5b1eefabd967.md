
现在使用 `export` 命令让 `count` 变量对子 shell 可：

- `% export count=19` <- 给 `count` 赋值并导出它。
- `% bash` <- 启动一个子 shell。
- `% echo $count` <- 显示 `count` 的值。

`19` <- 值已显示。
- `% exit` <- 退出子 shell。

注意，`export` 命令可以作为赋值命令的一部分。这一功能有助于简化脚本并减少交叉引用。如果 `export` 命令在脚本稍后运行，而你正试图理解脚本在做什么，你需要检查赋值命令以查看它的值是什么。

结论是，在修改变量时需要小心，以确保让正确的 shell 访问它们。

### 列表 2.4 case_sensitive—变量名大小写敏感

```bash
#!/bin/bash
logfile="one.txt"
Log="two.txt"
LOG="three.txt"
echo $logfile
echo $Log
echo $LOG
```

`logfile` is www.log

`logfile` is .

`$(logfile:=inet.log)` Example:

`logfile` is inet.log

`logfile` is inet.log

`$(logfile:+The logfile variable is set.)` Example:

Thefile variable is set.

下一行是空的，因为 `logfile` 未设置。

`${#logfile}` Example:

'web.log' 有 7 个字符。

`$(logfile:?Please specify a logfile name!)` Example:

`varsub: Please specify a logfile name!`

`Listing 2.5` 中的脚本使用了所有五种 `$()` 符号类型。请注意，`$logfile:www.log` 示例让 `logfile` 变量处于未设置状态；`echo` 命令没有显示 `logfile` 的值。另一方面，`$(logfile:=inet.log)` 示例确实为 `logfile` 分配了一个值，正如下一个 `echo` 命令所所示，该命令显示了 `logfile` 的值。

如果你需要根据另一个变量是否已设置来设置一个变量，那么 `$(:+)` 符号可能会很有用。例如：

`bSendEmail=$(emailAddr:+true)`

在你的脚本中，你可以使用 `bSendEmail` 的值来确定是否应该发送邮件。以下代码段：

```
if [ bSendEmail = "true" ]
then
  # send email
fi
```

比这个更容易理解：

```
if [ -n emailAddr ]
then
  # send email
fi
```

只要可能，请明智地使用变量名来创建自文档型脚本。

## 位置变量

关于位置变量本身的的更多信息，请参阅第 4 章中的“The if 命令”，以及第 74 页的“脚本执行命令”。

> 我喜欢让那些只取 true 或 false 的变量名以小写 b 开头，以指示它们的布尔属性。

`shell` 使用位置变量（position variables）来访问脚本参数。如果你创建一个创建一个处理两个文件的脚本，你可能需要找到要处理的文件名。文件名存储在变量 `$1` 和 `$2` 中。你只需要通过在相关数字前面加上美元符号，即可访问任意数量的参数。在访问第十个之后的参数时，你需要在数字周围使用花括号。例如，`${14}` 和 `${19}`。

### Listing 2.6 display_parameters—使用位置变量显示脚本参数

```
#!/bin/bash

echo "$0 = $*0*"
echo "$1 = $*1*"
echo "$2 = $*2*"
echo "$3 = *$3*"
```

这里是该脚本运行的示例：

```
% chmod +x process
% ./process one.dat two.dat
$0 = *process*
$1 = *one.dat*
$2 = *two.dat*
$3 = **
```

该脚本说明了两个主要点。首先，有时用星号括起值是有用的，这样你就可以更容易地判断变量是否为空。注意到 `$3` 是空的。这很有道理，因为传递给脚本的只有两个参数。

其次，`$0` 变量持有脚本本身的名字。该变量可能被用于创建与脚本易关联的日志文件。

还有三个变量与位置变量相关：

- `$*` 此变量包含参数列表。
- `$@` 此变量包含参数列表。
- `$#` 此变量包含参数的数量。

`Bash` 同时维护 `$*` 和 `@@` 变量，以便于从其他 shell 程序发布脚本。

### Listing 2.7 listparam—使用 *, @@, 和 ## 变量

```
#!/bin/bash

echo "There are $$ parameters."
echo "The parameters are $*($#)**"
echo "The parameters are $@*"
```

这里是该脚本运行的示例：

```
% chmod +x listparam
% ./listparam one two
There are 2 parameters.
The parameters are one two(2)
The parameters are one two
```

以下系列命令展示了引号规则的工作原理：

```
% echo \"Well said,\" said she.
"Well said," said she.
% echo \"Well said,\" said she.
% echo The value of \logfile is $logfile.
The value of \logfile is $logfile.
% echo Yesterday was `date+%8d` --date 1 day ago`'.
Yesterday was `date+%8d` --date 1 day ago`
```

这些示例表明，即使在单引号内，美元符号和反引号字符也会失去它们的特殊含义。由于在双引号和单引号示例中都使用了反引号，因此不再需要额外的反引号示例。

## 运算符

运算符告诉计算机要执行哪些操作。`Shell`（壳）像大多数语言一样，有许多运算符。本章前面的示例使用了赋值运算符。当你阅读其他运算符时，你无疑会发现你对其中一些已经熟悉了。请相信你的直觉，你已经知道的定义可能仍然正确。

运算符是你提供给计算机的指令，以便它执行某些任务。所有运算符都会对操作数执行某些操作。操作数可以是字面量（如 `3` 或 `23.3`）、变量（如 `$count`）或表达式（如 `$count + 1`）。表达式的良好定义是运算符和操作数的某种组合，并作为一个单元求值。

操作数本质上是递归的。表达式 `1 + 9`（两个操作数和一个加运算符）可以被视为一个值为 `10` 的操作数。例如，`(1 + 9) - 2` 是一个由两个操作数相减得到的表达式。第一个操作数是 `(1 + 9)`，第二个操作数是 `2`。

理解优先级是解析表达式的关键。优先级指示每个表达式或子表达式中应该先求值哪个操作数。我喜欢像给司机指令一样思考运算符。我说“左转”或“右转”。

这些命令可以被视为方向运算符，就像 `+` 和数学运算符说“加上这个”或“减去这个”一样。另一方面，如果我在移动时大喊“停止”，它应该取代其他命令。这意味着“停止”的优先级高于“左转”和“右转”。

表 2.2 按优先级从高到低出了 Shell 使用的所有运算符。高优先级的运算符会在低优先级的运算符之前求值。

### 表 2.2 Shell 运算符及其优先级

| 等级 | 运算符 | 描述 |
| --- | --- | --- |
| 13 | -, + | 一元取负、一元正 |
| 12 | !, ~ | 逻辑取反、按位取反或反码 |
| 11 | *, /, % | 乘法、除法、取模 |
| 10 | +, - | 加法、减法 |
| 9 | <<, >> | 按位左移、按位右移 |
| 8 | <=, >=, < > | 小于等于、大于等于、小于、大于 |
| 7 | =, != | 等于、不等于 |
| 6 | & | 按位与 |
| 5 | ^ | 按位异或 |
| 4 | | | 按位或 |
| 3 | && | 逻辑与 |
| 2 | || | 逻辑或 |
| 1 | +=, -=, *=, /=, %, &=, <=, <<, >= | 赋值、求值运算符后赋值 |

> 你可能认为表 2.2 列出了很多运算符。你错了；这个列表其实相当克制。例如，Shell 不支持幂运算符。对于这些以及更高级的运算符，你需要使用 Perl 或 Tcl。

在讨论一些更晦涩的运算符之前，让我们来看优先级如何影响表达式求值：
