
# 控制结构 439

第一形式是简单 `if` 结构的扩展；如果表达式为真，它会执行更多命令或一系列命令。这种形式仍然是单向分支。

第二种形式是双向分支。如果表达式为真，该结构执行第一组命令。如果为假，则执行 `else` 之后的命令组。

第三种形式类似于 Bourne Again Shell (`bash`) 的 `if...then...elif` 结构。它会一直进行测试，直到某个表达式为真，然后执行相应的命令。

此示例根据命令行参数的值为 `class` 变量赋值 0、1、2 或 3。在程序开头声明了变量 `class` 以保持清晰；你不需要在第一次使用它之前声明它。同样，为了清晰，脚本将第一行参数赋值给 `number`。第一个 `if` 语句测试 `number` 是否小于 0。如果是，脚本将 0 赋值给 `class`。如果不是，第二个 `if` 测试 `number` 是否在 0 到 100 之间。`&&` 是逻辑“与”运算符，如果表达式两边的值都为真，则结果为真。如果 `number` 在 100 到 200 之间，则将其赋值给 `class`。类似的测试确定它是否不是，最后的 `else` 将 3 赋值给 `class`。`endif` 关闭 `if` 控制结构。最后一条语句使用大括号（`{}`）将变量 `class` 与随后的句号隔离开。同样，使用大括号是为了清晰；shell 不会将标点符号视为变量名的一部分。如果你想在变量后紧跟其他字符，则需要使用大括号。

# foreach

`foreach` 内置命令并行于 Bourne Again Shell 的 `for...in` 结构。其语法为

```
foreach loop-index (argument-list)

  commands

end
```

该结构循环执行命令。在循环第一次，该结构将 `argument-list` 中第一个参数的值赋值给 `loop-index`。当控制到达 `end` 语句时，shell 将 `argument-list` 中的下一个参数赋值给 `loop-index` 并执行命令。shell 重复此过程，直到耗尽 `argument-list`。

# 440 第 12 章：TC Shell

下面的 `tc` 脚本使用 `foreach` 结构来循环遍历工作目录中的文件名包含指定字符字符串的文件，并更改该字符串。例如，可以将文件名中的字符串 `memo` 改为 `letter`。文件名 `memo.1`、`dailymemo` 和 `memories` 将分别变为 `letter.1`、`dailetter` 和 `letries`。此脚本需要两个参数：要更改的字符串和新字符串。`foreach` 结构的参数列表使用模糊的文件引用来遍历所有文件名。

```tc
cat rename

#!/bin/tcsh

# 用法: rename arg1 arg2

if ($#argv != 2) goto usage

foreach i (**)

    mv $i `echo $i | sed "s/$1/$2/"`

end

exit 0

usage:

echo "Usage: rename arg1 arg2"

exit 1
```

# 可

下一个脚本使用 `foreach` 循环将命令行参数赋值给名为 `buffer` 的数组。

```
cat foreach_l

#!/bin/tcsh

# 将 argv 填充零的例程

set buffer = (0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0)

set count = 1

#

if ($argv > 20) goto toomany

#

foreach argument ($argv[*])

    set buffer[$count] = $argument

    count++
```

# 490
# 可（续）

# 控制结构 441

```
# 将下一行的 command 替换为你想要调用的程序。

exec command $buffer

#

toomany:

echo "Too many arguments given."

echo "Usage: foreach_1 [up to 20 arguments]"

exit 1
```

此脚本调用另一个名为 `command` 的程序，其命令行保证包含20 个参数。如果调用 `foreach_1` 时参数少于 20 个，它将用零填充命令行以完成 20 个参数。参数过多会导致它显示用法消息并以错误状态退出。

# while

`while` 内置命令的语法是

```
while (expression)

    commands

end
```

该结构在表达式为真时持续循环执行命令。如果表达式为假，该结构永远不会执行命令。

```
> cat while_1

#!/bin/tcsh

# while 控制结构的演示。

# 该例程计算 1 到 n 之间的数字和，

# n 是命令行上的第一个参数。

#

set limit = $argv[1]

set index = 1

set sum = 0

#

while ($sum <= $limit)

    @ sum += $index

    @ index++

end

#

echo "The sum is $sum"
```

# 442 第 12 章：TC Shell

此程序计算到 `n` 为止的所有整数之和，其中 `n` 是命令行上的第一个参数。`+=` 操作将 `sum + index` 的值赋值给 `sum`。

## break 和 continue

你可以使用 `break` 或 `continue` 语句中断 `foreach` 或 `while` 结构。这些语句在转移控制权之前执行该行的剩余命令。`break` 语句将控制权转移到结束语句之后的语句，从而终止循环的执行。`continue` 语句将转移到结束语句，从而继续循环的执行。

## switch

`switch` 结构类似于 Bourne Again Shell (`bash`) 的 `case` 结构。

```
switch (test-string)

case pattern:

    commands

    breaksw

case pattern:

    commands

    breaksw

default:

    commands

    breaksw

endsw
```

`breaksw` 语句导致执行在 `endsw` 语句之后继续。如果你省略了 `breaksw`，控制将将到下一个命令。请参见第 389 页的表格，获取你可以在模式中使用特殊字符的列表。

```
> cat switch_1

#!/bin/tcsh

# switch 控制结构演示演示。

# 此例程测试第一个命令行参数

# 在大小写字母的任意组合中是否为 yes 或 no。

#

# 检查 argv[1] 是否存在

if ($#argv != 1) then

    echo "Usage: switch_1 [yes|no]"

    exit 1

endif
```

## 内置命令 443

```
else

# argv[1] 存在，根据其值设置 switch

switch ($argv[1])

# 情况 YES

  case [yY][eE][sS]:

    echo "Argument one is yes."

    breaksw

# 情况 NO

  case [nN][oO]:

    echo "Argument one is no."

    breaksw

# 默认情况 

  default:

    echo "Argument one is neither yes nor no."

    breaksw

  endsw

endif
```
