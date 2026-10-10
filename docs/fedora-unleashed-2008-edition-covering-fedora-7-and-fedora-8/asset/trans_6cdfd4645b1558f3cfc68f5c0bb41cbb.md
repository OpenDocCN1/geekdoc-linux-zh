

# 无限循环在 Shell 程序中的应用

无限循环有时非常有用。例如，你可以使用几行脚本轻松构建一个简单的命令，以持续监控网络接口的 802.11b 链路质量：

```sh
#!/bin/sh
while :
do
/sbin/ifconfig eth0 | grep Link | tr '\n' '\r'
done
```

该脚本输出搜索结果，然后 `tr` 命令对输出进行格式化。结果是一个简单的动画，显示不断更新的单行信息：

```text
Link Quality:92/92 Signal level:-11 dBm Noise level:-102 dBm
```

这种技术也可用于创建 X 的图形监控客户端，以输出关于网络接口的流量信息和活动状态：

```sh
#!/bin/sh
xterm -geometry 75x2 -e \
bash -c \
"while :; do \
/sbin/ifconfig eth0 | \
grep 'TX bytes' | tr '\n' '\r' ; \
done"
```

这个简单示例使用 bash 命令行脚本（通过 `-c` 启用）来重复执行命令行。该命令行将 `ifconfig` 命令的输出通过管道传递给 `grep`，`grep` 搜索 `ifconfig` 的输出，然后将包含字符串 'TX bytes' 的那一行通过管道传递给 `tr` 命令。接着，`tr` 命令移除行尾的回车符，以便在 xterm X11 终端窗口中显示信息，其大小由 `-geometry` 选项自动设定：

```text
RX bytes:4117594780 (3.9268 GB) TX bytes:452230967 (431.2 MB)
```

无限循环如此有用，以至于 Linux 包含了一个可以重复执行给定命令行的命令。例如，你可以使用 `sensors` 命令快速获取系统硬件健康状况的报告。但是，与其使用 shell 脚本无限循环输出，你可以使用 `watch` 命令来重复显示信息并提供简单的动画效果：

```sh
$ watch 'sensors -f | cut -c 1-20'
```

在 bash 中，`while` 流程控制结构使用以下格式：

```text
while expression
do
    statements
done
```

如果你想要计算前五个偶数之和，可以在 bash 中使用以下 shell 程序：

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

# until 语句

`until` 语句可用于执行一系列命令，直到指定条件变为 `true`。一旦指定条件求值为 `True`，循环即终止。

在 bash 中，使用的格式如下：

```text
until expression
do
    statements
done
```

如你所见，`until` 语句的格式与 `while` 语句类似，但逻辑有所不同：在 `while` 循环中，你一直执行直到表达式迭代为 `False`；而在 `until` 循环中，你一直循环直到表达式迭代为 `True`。

如果你想要计算前五个偶数之和，可以在 bash 中使用以下 shell 程序：

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

此处的示例与 while 语句的示例完全相同，除了被测试的条件恰好是 while 语句中指定条件的相反情况。

# shift 语句

shift 语句用于从左到右逐个处理位置参数。你会记得，位置参数被标识为 $1, $2, $3，以此类推。shift 命令的效果是每个位置参数向左移动一个位置，而当前的 $1 参数丢失。

在编写用户可以传递各种选项的 shell 程序时，shift 语句非常有用。根据指定的选项，后续参数的含义可能不同，或者可能根本不存在。

shift 命令的格式如下：

```text
shift *number*
```

参数 *number* 是要移动的位数，它是可选的。如果未指定，默认为 1；即参数向左移动一个位置。如果指定了，参数将向左移动 *number* 个位置。

# if 语句

if 语句通过评估逻辑表达式来做出决定。在 bash 中，if 条件具有以下格式：

```text
if [ *expression* ]; then
    *Statements*
elif [ *expression* ]; then
    *Statements*
else
    *Statements*
fi
```

if 条件可以嵌套。也就是说，一个 if 条件可以包含另一个 if 条件。if 条件不需要有 elif 或 else 部分。如果 if 语句中指定的表达式以及后续可选的 elif 语句中的表达式都没有为真，则执行 else 部分。关键字 fi 用于表示 if 语句的结束，如果你有嵌套的 if 条件，这将非常有用。在这种情况下，你应该能够将 fi 与 if 匹配，以确保所有 if 语句都正确编码。

在以下 bash 示例中，变量 var 可以具有两个值之一：Yes 或 No。任何其他值都是无效的。可以按以下方式编码：

```sh
if [ $var = "Yes" ]; then
    echo "Value is Yes"
elif [ $var = "No" ]; then
    echo "Value is No"
else
    echo "Invalid value"
fi
```

# case 语句

case 语句用于根据与指定变量匹配的离散值或值范围来执行语句。在大多数情况下，如果你有大量条件，可以使用 case 语句代替 if 语句。

bash 中 case 语句的格式如下：

```text
case str in
    str1 | str2)
        Statements;;
    str3, str4)
        Statements;;
    *)
        Statements;;
esac
```

你可以为每个条件指定一系列离散值——例如 str1、str2 等，或者你可以指定带有通配符的值。最后一个条件应该是 *（星号），如果在其他条件都不满足时执行。对于指定的每个条件，直到双分号 ( `;;` ) 为止的所有相关语句都会被执行。

你可以编写一个脚本，如果提供月份编号作为参数，则回显月份名称。如果你提供的编号不在 1 到 12 之间，则会得到错误消息。脚本如下：

```sh
#!/bin/sh

case $1 in
    01 | 1) echo "Month is January";;
    02 | 2) echo "Month is February";;
    03 | 3) echo "Month is March";;
    04 | 4) echo "Month is April";;
    05 | 5) echo "Month is May";;
    06 | 6) echo "Month is June";;
    07 | 7) echo "Month is July";;
    08 | 8) echo "Month is August";;
    09 | 9) echo "Month is September";;
    10) echo "Month is October";;
    11) echo "Month is November";;
    12) echo "Month is December";;
    *) echo "Invalid parameter";;
esac
```

你需要在每个条件下的语句末尾加上双分号（`;;`）。如果没有这样做，下一个条件下的语句也会被执行。

最后一个条件应该是 *default*，如果在其他条件都不满足时执行。对于指定的每个条件，直到 *break* 为止的所有相关语句都会被执行。

# break 和 exit 语句

你应该了解另外两个语句：*break* 语句和 *exit* 语句。

*break* 语句可用于终止迭代循环，例如 *for*、*until* 或 *repeat* 命令。

*exit* 语句可用于退出 shell 程序。你可以在 *exit* 后可选地添加一个数字。如果当前的 shell 程序是由另一个 shell 程序调用的，调用程序可以检查代码（根据 shell 不同，为 *$?* 或 *$status* 变量）并据此做出决定。

# 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。*函数* 是 shell 程序的一部分，用于执行特定过程；你可以在 shell 程序中多次重用同一个函数。函数有助于消除在编写 shell 程序时重复代码的需求。

bash 中函数的格式如下：

```text
func() {
    Statements
}
```

你可以如下调用函数：

```text
func param1 param2 param3
```

参数 *param1*、*param2* 等是可选的。你也可以将参数作为单个字符串传递——例如，*$0*。函数可以像解析从命令行作为命令行参数传递给 shell 程序的位置参数一样解析参数，但使用脚本内部传递的值。例如，以下脚本使用了一个名为 *DisplayMonth()* 的函数，该函数显示月份名称或一个

