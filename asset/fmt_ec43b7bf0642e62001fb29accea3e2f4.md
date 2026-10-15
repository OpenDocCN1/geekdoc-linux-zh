
```tcsh
#!/bin/tcsh
foreach filename (`/bin/ls`)
    cp $filename backup/$filename
    if ($? != 0) then
        echo "copy for $filename failed"
    endif
end
```

## `while` 语句

当指定条件为真时，`while` 语句可用于执行一系列命令。一旦指定条件求值为假，循环就会终止。如果指定条件在开始时求值为假，则循环可能根本不会执行。你应该小心使用 `while` 命令，因为如果指定条件永远不为假，循环将永远不会终止。

在 `pdksh` 和 `bash` 中，使用以下格式：

```bash
while expression
do
    statements
done
```

在 `tcsh` 中，使用以下格式：

```tcsh
while (expression)
    Statements
end
```

如果你想要计算前五个偶数的和，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

```bash
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

在 `tcsh` 中，该程序可以写成如下形式：

```tcsh
#!/bin/tcsh
set loopcount = 0
set result = 0
while ($loopcount < 5)
set loopcount = `expr $loopcount + 1`
set increment = `expr $loopcount \* 2`
set result = `expr $result + $increment`
end
echo "result is $result"
```

## `until` 语句

当指定条件为真时，`until` 语句可用于执行一系列命令。一旦指定条件求值为真，循环就会终止。

在 `pdksh` 和 `bash` 中，使用以下格式：

```bash
until expression
do
   statements
done
```

正如你所见，其格式与 `while` 语句类似。

如果你想要计算前五个偶数的和，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

```bash
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

这里的示例与 `while` 语句的示例完全相同，只是测试的条件与 `while` 语句中指定的条件相反。

`tcsh` 命令不支持 `until` 语句。

## `repeat` 语句 (tcsh)

`repeat` 语句用于将一条命令执行固定的次数。

如果你想在屏幕上打印 80 次连字符 `-`，可以使用以下命令：

# 第四部分

## `select` 语句 (pdksh)

如果你正在编写一个期望用户在线输入的 shell 程序，`select` 语句用于生成一个菜单列表。`select` 语句的格式如下：

```bash
select item in itemlist
do
    Statements
done
```

`itemlist` 是可选的。如果未提供，系统将依次遍历 `item` 中的条目。然而，如果提供了 `itemlist`，系统将遍历 `itemlist` 中的每个条目，并且 `itemlist` 的当前值会在每次迭代中赋值给 `item`，然后可以将其用作正在执行的语句的一部分。

如果你想编写一个菜单，让用户选择 `Continue`（继续）或 `Finish`（结束），你可以编写以下 shell 程序：

```bash
#!/bin/bash
select item in Continue Finish
do
    if [ $item = "Finish" ]; then
        break
    fi
done
```

当执行 `select` 命令时，系统会向用户显示带有数字选项的菜单——在这种情况下，1 代表 `Continue`，2 代表 `Finish`。如果用户选择 1，变量 `item` 的值为 `Continue`；如果用户选择 2，变量 `item` 的值为 `Finish`。当用户选择 2 时，会执行 `if` 语句，循环终止。

## `shift` 语句

`shift` 语句用于从左到右依次处理位置参数。如你所记得的，位置参数被标识为 `$1`、`$2`、`$3` 等。`shift` 命令的效果是使每个位置参数向左移动一个位置，并且当前的 `$1` 参数会丢失。

`shift` 命令的格式如下：

```bash
shift number
```

参数 `number` 是要移动的位数，是可选的。如果未指定，默认为 1；也就是说，参数向左移动一个位置。如果指定了，参数将向左移动 `number` 个位置。

当你编写允许用户传递各种选项的 shell 程序时，`shift` 命令非常有用。根据指定的选项，后续参数的含义可能不同，或者根本不存在。

## 条件语句

条件语句在 shell 程序中用于根据指定条件决定执行程序的哪一部分。

### `if` 语句

`if` 语句通过评估逻辑表达式来进行决策。在 `pdksh` 和 `bash` 中，`if` 条件的格式如下：

```bash
if [ expression ]; then
    Statements
elif [expression ]; then
    Statements
else
    Statements
fi
```

`if` 条件可以嵌套。也就是说，一个 `if` 条件内部可以包含另一个 `if` 条件。`if` 条件不一定需要有 `elif` 或 `else` 部分。如果 `if` 语句中指定的所有表达式以及后续 `elif` 语句中可选的表达式都为假，则执行 `else` 部分。单词 `fi` 用于表示 `if` 语句的结束，这在存在嵌套 `if` 条件时非常有用。在这种情况下，你应该能够将 `fi` 与 `if` 匹配，以确保所有 `if` 语句都正确编码。

在以下示例中，变量 `var` 可以有两个值之一：`Yes` 或 `No`。其他任何值都是无效值。可以按以下方式编码：

```bash
if [ $var = 'Yes' ]; then
    echo 'Value is Yes'
elif [ $var = 'No' ]; then
    echo 'Value is No'
else
    echo 'Invalid value'
fi
```

在 `tcsh` 中，`if` 语句有两种形式。第一种形式类似于 `pdksh` 和 `bash` 的形式，如下所示：

```tcsh
if (expression) then
    Statements
else if (expression) then
    Statements
```

```
else
    语句
endif
```

`if` 条件可以嵌套——也就是说，一个 `if` 条件内部可以包含另一个 `if` 条件。`if` 条件不一定要有 `else` 部分。如果所有在任意 `if` 语句中指定的表达式都不为真，则执行 `else` 部分。该语句中可选的 `if` 部分（`else if (expression) then`）在其后的条件为真且前一个 `if` 语句不为真时执行。`endif` 一词用于表示 `if` 语句的结束，如果你嵌套了多个 `if` 条件，这非常有用。在这种情况下，你应该能够匹配 `endif` 和 `if`，以确保所有 `if` 语句都正确编写。

还记得变量 `var` 只有两个值 `Yes` 和 `No` 的 `pdksh` 和 `bash` 的示例吗？以下是它在 `tcsh` 中的编码方式：

```
if ($var == "Yes") then
    echo "Value is Yes"
else if ($var == "No") then
    echo "Value is No"
else
    echo "Invalid value"
endif
```

`tcsh` 中 `if` 条件的第二种形式如下：
