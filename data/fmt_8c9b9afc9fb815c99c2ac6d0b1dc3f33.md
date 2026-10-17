
```bash
echo "number1 is less than or equal to number3"
```
else
```bash
echo "number1 is not less than or equal to number3"
```
fi

当你执行该 shell 程序时，将得到以下结果：

```
number1 is equal to number3

number1 is not equal to number2

number1 is not greater than number2

number1 is greater than or equal to number3

number1 is less than number2

number1 is less than or equal to number3
```

## 文件操作符

你可以使用以下运算符作为文件比较操作符：

- `-d` : 确定文件是否为目录
- `-f` : 确定文件是否为普通文件
- `-r` : 确定文件是否可读

## 逻辑操作符

你使用逻辑操作符通过布尔逻辑来比较表达式，使用 NOT、AND 和 OR 来比较值：

- `!` : 对逻辑表达式进行取反
- `-a` : 对两个逻辑表达式进行逻辑与
- `-o` : 对两个逻辑表达式进行逻辑或

# 编写和执行 Shell 脚本

## 数字比较

你可以使用以下运算符来比较数字：

- `>=` 比较一个数字是否大于等于另一个数字
- `<=` 比较一个数字是否小于等于另一个数字
- `>` 比较一个数字是否大于另一个数字
- `<` 比较一个数字是否小于另一个数字

以下示例在 Shell 程序 `compare2` 中比较了三个数字 `number1`、`number2` 和 `number3`：

```bash
#!/bin/tcsh

set number1=5

set number2=10

set number3=5

if (number1 > number2) then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
endif

if (number1 >= number3) then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
endif

if (number1 < number2) then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
endif

if (number1 <= number3) then
    echo "number1 is less than or equal to number3"
else
    echo "number1 is not less than or equal to number3"
endif
```

执行 Shell 程序 `compare2` 时，你会得到以下结果：
`number1 is not greater than number2`
`number1 is greater than or equal to number3`
`number1 is less than number2`
`number1 is less than or equal to number3`

# 第 12 章 自动化任务与 Shell 脚本

## 文件运算符

你可以使用以下运算符作为文件比较运算符：

- `-d`—确定文件是否为目录
- `-e`—确定文件是否存在
- `-f`—确定文件是否为普通文件
- `-o`—确定用户是否为该文件的所有者
- `-r`—确定文件是否设置了读取权限
- `-w`—确定文件是否设置了写入权限
- `-z`—确定文件是否设置了执行权限且大小为零

以下示例基于名为 `compare3` 的 Shell 程序，该程序位于当前目录下一个名为 `file` 的文件和一个名为 `dir` 的子目录中。假设 `file` 的权限为 `r-x`（读取和执行权限），`dir` 的权限为 `rwx`（读取、写入和执行权限）。

以下是 `compare3` Shell 程序的代码：

```bash
#!/bin/bash

if (-d dir) then
    echo "dir is a directory"
else
    echo "dir is not a directory"
endif

if (-f file1) then
    echo "file1 is a regular file"
else
    echo "file1 is not a regular file"
endif

if (-r file1) then
    echo "file1 has read permission"
else
    echo "file1 does not have read permission"
endif

if (-w file1) then
    echo "file1 has write permission"
else
    echo "file1 does not have write permission"
endif
```

# 编写和执行 Shell 脚本

```bash
if (-x dirl) then
    echo "dir has execute permission"
else
    echo "dir does not have execute permission"
endif
```

```bash
if (-z file1) then
    echo "file has zero length"
else
    echo "file has greater than zero length"
endif
```

如果你执行文件 `compare3`，你会得到以下结果：

- `dirl is a directory`
- `file1 is a regular file`
- `file1 has read permission`
- `file1 does not have write permission`
- `dirl has greater than zero length`

# 逻辑运算符

你可以在条件语句中使用逻辑运算符。使用以下运算符来取反逻辑表达式或执行逻辑与（AND）和或（OR）：

- `!`—取反逻辑表达式
- `&&`—逻辑与两个逻辑表达式
- `||`—逻辑或两个逻辑表达式

此示例名为 `logic` 的示例使用了之前 `compare3` 示例中提到的文件和目录：

```tcsh
#!/bin/tcsh

if (-x file1 && -x dirl ) then
    echo file1 and dirl are executable
else
    echo at least one of file1 or dirl are not executable
endif
```

```tcsh
if (-w file1 || -w dirl ) then
    echo file1 or dirl are writable
else
    echo neither file1 or dirl are executable
endif
```

```tcsh
if ( ! -w file ) then
    echo file is not writable
else
    echo file is writable
endif
```

如果你执行 `logic`，它会产生以下结果：

```
file1 and dirl are executable
file1 or dirl are writable
file1 is not writable
```

# for 语句

你使用 `for` 语句在每次指定条件为真时执行一组命令。`for` 语句有多种格式。`pdksh` 和 `bash` 使用的第一种格式如下：

```bash
curvar in list
do
    statements
```

如果你想对 `list` 中的每个值执行一次语句，应该使用这种形式。在每次迭代中，`list` 的当前值会被赋值给 `vcurvar`。`list` 可以是一个包含多个项目的变量，也可以是空格分隔的值列表。第二种格式如下：

```bash
curvar
do
    statements
```

在这种形式中，`list` 的当前值会被赋值给 `vcurvar`。

# 编写和执行 Shell 脚本

在 `tcsh` 中，`for` 语句被称为 `foreach`。其格式如下：

```tcsh
foreach var list
    statements
end
```

# while 语句

你可以使用 `while` 语句在每次指定条件为真时执行一组命令。一旦指定条件的求值为为假，循环立即终止。

```bash
while condition
do
    statements
done
```

## 编写和执行 Shell 脚本

如果你想相加前五个偶数，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

```
#!/bin/bash
loopcount=0
result=0
while [ $loopcount -lt 5 ]
do
  loopcount=`expr $loopcount + 1`
  increment=`expr $loopcount \* 2`
  result=`expr $result + $increment`
done
echo "result is $result"
```

在 `tcsh` 中，你可以如下编写该程序：

```
#!/bin/tcsh
set loopcount=0
set result=0
while ($loopcount < 5)
  set loopcount=`expr $loopcount + 1`
  set increment=`expr $loopcount \* 2`
  set result=`expr $result + $increment`
end
echo result is $result
```

## until 语句

你可以使用 `until` 语句执行一系列命令，直到指定的条件为真。

一旦条件求值为真，循环就会终止。
在 `pdksh` 和 `bash` 中，格式如下：

```
until expression
do
  statements
done
```

如你所见，`until` 语句的格式与 `while` 语句相似，但逻辑不同：在 `while` 循环中，你执行表达式直到其为假；而在 `until` 循环中，你循环执行表达式直到其为真。这种区别的一个重要部分是，`while` 执行零次或多次（可能完全不执行），而 `until` 重复一次或多次，意味着它至少会被执行一次。

## 第 12 章 任务自动化与 Shell 脚本

如果你想相加前五个偶数，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

```
#!/bin/bash
loopcount=0
result=0
until [ $loopcount -ge 5 ]
do
  loopcount=`expr $loopcount + 1`
  increment=`expr $loopcount \* 2`
  result=`expr $result + $increment`
done
echo "result is $result"
```

这里的示例与 `while` 语句的示例相同，区别在于测试的条件与 `while` 语句中指定的条件完全相反。

`tcsh` shell 不支持 `until` 语句。

## repeat 语句 (tcsh)

你使用 `repeat` 语句按固定次数执行某一个命令。如果你想在屏幕上打印 80 个连字符 `-`，且每行一个，可以使用以下命令：

```
repeat 80 echo '-'
```

## select 语句 (pdksh)

如果你正在编写一个期望用户在线输入的 shell 程序，你可以使用 `select` 语句来生成菜单列表。`select` 语句的格式如下：

```
select item in itemlist
do
  Statements
Done
```

`itemlist` 是可选的。如果没有提供，系统将逐个遍历条目。然而，如果提供了 `itemlist`，系统将对 `itemlist` 中的每个项目进行迭代，并在每次迭代中将 `itemlist` 的当前值赋值给 `item`，然后它可以作为被执行语句的一部分。

如果你想写一个让用户选择“继续 (Continue)”或“完成 (Finish)”的菜单，可以编写以下 shell 程序：

## 编写和执行 Shell 脚本

```
#!/bin/ksh
select item in Continue Finish
do
  if [ $Item = "Finish" ]; then
    break
  fi
done
```

当执行 `select` 命令时，系统会向用户显示一个带有数字选项的菜单——即，选择 1 继续，选择 2 完成。如果用户选择 1，变量 `item` 包含值 Continue；如果用户选择 2，变量 `item` 包含值 Finish。当用户选择 2 时，将执行 `if` 语句并终止循环。

## shift 语句

你使用 `shift` 语句从左到右一次一次处理位置参数。回想，位置参数被标识为 `$1`, `$2`, `$3` 等。`shift` 命令的效果是每个位置参数都向左移动一位，并且当前的 `$1` 参数将丢失。

当你编写用户可以传递各种选项的程序时，`shift` 语句非常有用。根据指定的选项，后续参数可能具有不同的含义，或者完全没有意义。

`shift` 命令的格式如下：

```
shift number
```

参数 `number` 是要移动的位数，是可选的。如果没有指定，默认值为 1；即参数向左移动一位。如果指定了，参数将向左移动 `number` 位。

## if 语句

`if` 语句通过评估逻辑表达式来做出决策。在 `pdksh` 和 `bash` 中，`if` 条件的格式如下：

```
if [ expression ]; then
  Statements
elif [ expression ]; then
  Statements
else
  Statements
fi
```

`if` 条件可以嵌套。也就是说，一个 `if` 条件内部可以包含另一个条件。`if` 条件并不一定需要有 `elif` 或 `else` 部分。如果 `if` 语句中指定的任何表达式（以及后续 `elif` 语句中指定的表达式，它们是可选的）都不为真，则执行 `else` 部分。单词 `fi` 用来表示 `if` 语句的结束，如果你有嵌套的 `if` 条件则是如此。

在以下 `bash` 或 `pdksh` 示例中：

```
if [ $var = "Yes" ]; then
  echo "Yes"
elif [ $var = "No" ]; then
  echo "No"
else
  echo "Invalid"
fi
```

## case 语句

你使用 `case` 语句将变量的值与多个模式进行匹配。它类似于一系列 `if-elif-else` 语句。`case` 语句的格式如下：

```
case variable in
  pattern1)
    statements
    ;;
  pattern2)
    statements
    ;;
  *)
    statements
    ;;
esac
```

变量按顺序与每个模式进行匹配。当找到匹配项时，执行相应的语句，`;;` 符号表示该 `case` 的结束。星号 (`*`) 模式是一个通配符，如果之前的没有任何模式匹配成功，它可以作为任何值的通捕获器。

- `itemlist` 是可选的。如果没有提供，系统将逐个遍历条目。然而，如果提供了 `itemlist`，系统将对 `itemlist` 中的每个项目进行迭代，并在每次迭代中将 `itemlist` 的当前值赋值给 `item`，然后它可以作为被执行语句的一部分。

# 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。函数是 shell 程序中执行特定过程的一个部分；你可以在 shell 程序中多次复用同一个函数。函数可以帮助你在编写 shell 脚本时避免代码重复。

以下是函数在 `pdksh` 和 `bash` 中的格式：

```
func() {
  Statements
}
```

你可以按照如下方式调用函数：

```
func param1 param2 param3
```

参数 `param1`、`param2` 等是可选的。你也可以将参数作为单个字符串传递——例如 `$@`。函数可以像解析它们是 shell 程序内部的顺序参数一样，解析从命令行作为命令行参数的参数，但使用的是脚本内部传递的值。例如，以下脚本使用了一个名为 `Displaymonth()` 的函数，它可以显示月份名称，如果你传递了超出 1 到 12 范围的数字，它会显示错误信息。此示例在 `pdksh` 和 `bash` 中有效：

```bash
#!/bin/sh
Displaymonth() {
  case $1 in
    01 | 1) echo "Month is January";
```
