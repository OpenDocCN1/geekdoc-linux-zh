
```
  result=`expr $result + $increment`
done
echo "result is $result"
```

在 `tcsh` 中，该程序可以写如下：

```tcsh
#!/bin/tcsh

set loopcount =0

set result =0

while ($loopcount < 5)
  set loopcount = `expr $loopcount + 1`
  set increment = `expr $loopcount \* 2`
  set result = `expr $result + $increment`
end

echo "result is $result"
```

# until 语句

`until` 语句用于执行一系列命令，直到指定的条件为真（true）。

## 迭代语句

一旦指定的条件评估为真（True），循环就会终止。

在 `pdksh` 和 `bash` 中，使用以下格式：

```
until expression
do
  statements
```

如你所见，`until` 语句的格式与 `while` 语句相似，但逻辑不同：在 `while` 循环中，你执行直到表达式为假；但在 `until` 循环中，你一直循环直到表达式为真。

如果你想计算前五个偶数之和，可以在 `pdksh` 和 `bash` 中使用以下 Shell 程序：

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

这里的示例与 `while` 语句的示例相同，区别在于测试的条件仅仅是 `while` 语句中指定的条件的相反。

`tcsh` Shell 不支持 `until` 语句。

# repeat 语句 (pdksh)

`repeat` 语句用于执行固定次数的某一个命令。

如果你想在屏幕上打印 80 次连字符（-），每行一个字符，可以使用以下命令：

```
repeat 80 echo '-'
```

# select 语句 (pdksh)

`select` 语句用于在你编写一个期望在线用户输入的 Shell 程序时生成一个菜单列表。`select` 语句的格式如下：

```
select item in itemlist
do
    Statements
done
```

`itemlist` 是可选的。如果未提供，系统将逐个迭代项目项。然而，如果提供了 `itemlist`，系统将为 `itemlist` 中的每个项目进行迭代，并在每次迭代中将 `itemlist` 的当前值赋值给 `item`，然后该值可以作为被执行的语句的一部分。

如果你想写一个让用户选择“继续”（Continue）的菜单，可以使用以下代码：

```bash
select item in Continue Exit
do
    if [ $item = "Exit" ]; then
        break
    fi
    echo "You chose $item"
done
```

## 条件语句

你可以编写一个脚本，当你提供月份数字作为参数时，它会输出该月份名称。如果你提供的数字不在 1 到 12 之间，你将得到一个错误消息。脚本如下：

```
#!/bin/sh
case $1 in
  01) echo "Month is January";
  02) echo "Month is February";
  03) echo "Month is March";
  04) echo "Month is April";
  05) echo "Month is May";
  06) echo "Month is June";
  07) echo "Month is July";
  08) echo "Month is August";
  09) echo "Month is September";
  10) echo "Month is October";
  11) echo "Month is November";
  12) echo "Month is December";
  *) echo "Invalid parameter";
esac
```

你需要在每个条件下的语句结束以双分号（;;）结束。如果不这样做，下一个条件下的语句也会被执行。

`tsh` 的 `case` 语句格式如下：

```
switch (str)
  case str1|str2)
    Statements
    breaksw
  case str3|str4)
    Statements
    breaksw
  default)
    Statements
    breaksw
endsw
```

你可以为每个条件指定若干个离散值——例如 `str1`、`str2` 等——也可以指定一个带有通配符的值。最后一个条件应该是默认的（default），并在不满足其他任何条件时执行。对于每个指定的条件，在遇到 `breaksw` 之前的所有相关语句都将被执行。

上文提到的在给定数字时输出月份的示例（之前在 `pdksh` 和 `bash` 中显示过）在 `tsh` 中可以写如下：

```
#!/bin/tcsh
set month = 5
switch ( $month )
  case 1: echo "Month is January" ; breaksw
  case 2: echo "Month is February" ; breaksw
  case 3: echo "Month is March" ; breaksw
  case 4: echo "Month is April" ; breaksw
  case 5: echo "Month is May" ; breaksw
  case 6: echo "Month is June" ; breaksw
  case 7: echo "Month is July" ; breaksw
  case 8: echo "Month is August" ; breaksw
  case 9: echo "Month is September" ; breaksw
  case 10: echo "Month is October" ; breaksw
  case 11: echo "Month is November" ; breaksw
  case 12: echo "Month is December" ; breaksw
  default: echo "Oops! Month is October!" ;
esac
```

你需要在每个条件下的语句结束以 `breaksw` 结束。如果不这样做，下一个条件下的语句将被将被执行。

## break 和 exit 语句

你应该注意另外两个语句：`break` 语句和 `exit` 语句。

`break` 语句可以终止迭代循环，例如 `for`、`until` 或 `repeat` 命令。

`exit` 语句可用于退出 shell 程序。你可以可选地在 `exit` 后面使用一个数字。如果当前 shell 程序是由另一个 shell 程序调用的，调用程序可以检查状态码（取决于 shell 类型，使用 `$?` 或 `$status` 变量）并据此做出决定。

## 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。函数是执行特定过程的 shell 程序片段；你可以在 shell 程序中多次复用同一个函数。函数有助于在编写 shell 程序时消除编写重复代码的需求。

以下是 `pdksh` 和 `bash` 中函数的格式：

```
func(){
  Statements
}
```

你可以这样调用函数：

`func param1 param2 param3`

参数 `*param1, param2, $*` 等* 是可选的。你也可以将参数作为单个字符串传递——例如，函数可以解析参数，就像它们是从命令行作为命令行参数传递给 shell 程序的顺序参数一样，但使用的是脚本内部传递的值。例如，以下脚本使用了一个名为 `Displaymonth()` 的函数，它可以显示月份名称，或者如果你传递超出 1 到 12 范围的月份数字，它会显示错误消息。此示例在 `pdksh` 和 `bash` 中均有效：

```
#!/bin/sh
DisplayName() {
  case $1 in
    01) echo "Month is January";
    02) echo "Month is February";
    03) echo "Month is March";
```
