

如果你想相加前五个偶数，可以在 pdksh 和 bash 中使用以下 shell 程序：

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

这里的示例与 while 语句的示例相同，不同之处在于测试的条件与 while 语句中指定的条件相反的。

tcsh shell 不支持 `until` 语句。

## repeat 语句 (tcsh)

repeat 语句用于固定次数地执行一个命令。

如果你想在屏幕上打印 80 个连字符 (-)，且每行一个，可以使用以下命令：

```bash
repeat 80 echo '-'
```

## select 语句 (pdksh)

如果你正在编写一个期望从用户处在线输入的 shell 程序，则 `select` 语句用于生成菜单列表。select 语句的格式如下：

```bash
select item in itemlist
do
  Statements
done
```

itemlist 是可选的。如果未提供，系统将逐个遍历项目条目。然而，如果提供了 itemlist，系统将为 itemlist 中的每个项目进行迭代，并在每次迭代将 itemlist 的当前值赋值给 item，然后该值可以作为执行的语句的一部分。

如果你想写一个能让用户选择“继续 (Continue)”或“完成 (Finish)”的菜单，可以编写以下 shell 程序：

```bash
#!/bin/ksh
select item in Continue Finish
do
if [ $item = "Finish" ]; then
  break
fi
```

当执行 `select` 命令时，系统会向用户显示一个带有数字选项的菜单——在这种情况下，1 代表 Continue，2 代表 Finish。如果用户选择 1，变量 item 包含值为 Continue；如果用户选择 2，变量 item 包含值为 Finish。当用户选择 2 时，将执行 if 语句并终止循环。

## shift 语句

shift 语句用于从左到右逐个处理位置参数。正如你记得的，位置参数被标识为 $1, $2, $3 等。`shift` 命令的作用是将每个位置参数向左移动一位，并且当前的 $1 参数会丢失。

当你编写用户可以传递各种选项的 shell 程序时，`shift` 语句非常有用。根据指定的选项，后续参数可能具有不同的含义，或者可能根本不存在。

`shift` 命令的格式如下：

```bash
shift number
```

参数数字是需要移动的位数，是可选的。如果未指定，默认值为 1；即参数向左移动一位。如果指定，参数将向左移动 number 位。

## 条件语句

条件语句在 shell 程序中用于根据指定的条件决定执行程序的哪部分。

## if 语句

`if` 语句通过求值逻辑表达式来做出决策。如果一个 if 条件在 pdksh 和 bash 中具有如下格式：

```bash-bash
if [ expression ]; then
  Statements
elif [expression ]; then
  Statements
else
  Statements
fi
```

条件可以嵌套。也就是说，一个 if 条件内部可以包含另一个条件。if 条件不一定需要有 elif 或 else 部分。如果 if 语句中指定的表达式（以及后续 elif 语句中可选的表达式）都不成立，则执行 else 部分。单词 `fi` 用于表示 if 语句的结束，如果你有嵌套条件，这非常有用。在这种情况下，你应该能够将 fi 与 if 匹配，以确保所有 if 语句都正确编写。

在以下 bash 或 pdksh 示例中，变量 var 可以取两个值之一：Yes 或 No。任何其他值都是无效的。代码可以如下：

```bash-bash
if [ Var = "Yes" ]; then
  echo "Value is Yes"
elif [ Var = "No" ]; then
  echo "Value is No"
else
  echo "Invalid value"
fi
```

在 tsh 中，if 语句有两种形式。第一种形式类似于 pdksh 和 bash 的形式，如下：

```csh
if (expression) then
  Statements
else if (expression) then
  Statements
else
  Statements
endif
```

条件可以嵌套——也就是说，一个 if 条件内部可以包含另一个条件。if 条件不一定有 else 部分。如果任何 if 语句中指定的表达式都不成立，则执行 else 部分。如果随其后的条件为真且之前的语句不成立，则执行语句的可选部分（else if (expression) then）。单词 `endif` 用于表示 if 语句的结束，如果你有嵌套条件，这非常有用。在这种情况下，你应该能够将 endif 与 if 匹配，以确保所有 if 语句都正确编写。

使用变量 var 只有两个值 Yes 和 No 的示例，在 tcsh 中的代码如下：

```csh
if ($Var == "Yes") then
  echo "Value is Yes"
else if ($Var == "No") then
  echo "Value is No"
else
  echo "Invalid value"
endif
```

tcsh 条件的第二种形式如下：

```csh
if (expression) command
```

在这种格式下，如果表达式求值为真，则只能执行单个命令。

## case 语句

case 语句用于根据匹配指定变量离散值或值范围来执行语句。在大多数情况下，如果你有大量的条件，可以使用 case 语句代替 if 语句。

pdksh 和 bash 的 case 语句格式如下：

```bash-bash
case str in
  str1 | str2)
    Statements;;
  str3|str4)
    Statements;;
  *)
    Statements;;
```

你可以为每个条件指定若干个离散值——如 str1、str2 等，或者你可以使用通配符指定一个值。最后一个条件应该是 *（星号），当没有满足其他任何条件时执行该条件。对于每个指定的条件，将执行直到双分号（;;）为止的所有关联语句。

你可以编写一个脚本，如果你提供月份数字作为参数，它将输出月份名称。如果你提供的数字不在 1 到 12 之间，将得到错误消息。脚本如下：

```bash-bash
#!/bin/sh
case $1 in
  1) echo "January";;
  2) echo "February";;
  3) echo "March";;
  4) echo "April";;
  5) echo "May";;
  6) echo "June";;
  7) echo "July";;
  8) echo "August";;
  9) echo "September";;
  10) echo "October";;
  11) echo "November";;
  12) echo "December";;
  *) echo "Invalid parameter";
esac
```

你需要在每个条件的语句结束加上双分号（;;）。如果不这样做，下一个条件下的语句也将执行。

tcsh 的 case 语句格式如下：

```csh
switch (str)
  case str1|str2:
    Statements
    break;
  case str3|str4:
    Statements
    break;
  default:
    Statements
    break;
endswitch
```

你可以为每个条件指定若干个离散值——如 str1、str2 等，或者你可以使用通配符指定一个值。最后一个条件应该是 default，当没有满足其他任何条件时执行该条件。

之前为 pdksh 和 bash 显示的给定数字输出月份的示例在 tcsh 中可以写为：

```csh
#!/bin/tcsh
set month = $1
switch ($month)
  case 1: echo "January"; break;
  case 2: echo "February"; break;
  case 3: echo "March"; break;
  case 4: echo "April"; break;
  case 5: echo "May"; break;
  case 6: echo "June"; break;
  case 7: echo "July"; break;
  case 8: echo "August"; break;
  case 9: echo "September"; break;
  case 10: echo "October"; break;
  case 11: echo "November"; break;
  case 12: echo "December"; break;
  default: echo "Oops! Month is October!"; break;
endswitch
```

## break 和 exit 语句

你应该了解两个语句：break 语句和 exit 语句。

break 语句用于终止迭代循环，例如 for 或 repeat 命令。

exit 语句用于退出 shell 程序。你可以在 exit 后跟跟一个数字。如果当前程序是由另一个 shell 程序调用的，调用程序可以检查状态码（取决于 shell，使用 $ 或 $status）并此做出决策。

## 在 Shell 脚本中使用函数

