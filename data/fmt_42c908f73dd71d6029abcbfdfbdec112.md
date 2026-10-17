
```bash
if [ -z file1 ]; then
echo "file1" has zero length
else
echo "file1" has greater than zero length
fi
```

如果你执行文件 `compare3`，将得到以下结果：

`dir1` 是一个目录

`file1` 是普通文件

`file1` 有读取权限

`file1` 没有写权限

`dir1` 具有执行权限

# 逻辑运算符

逻辑运算符用于使用布尔逻辑比较表达式，布尔逻辑使用表示非（NOT）、与（AND）和或（OR）的字符来比较值。

- `!` — 对逻辑表达式取反

- `-a` — 逻辑与两个逻辑表达式

- `-o` — 逻辑或两个逻辑表达式

这个名为 `logic_logic` 的示例使用了之前 `compare3` 示例中提到的文件和目录。

# 402 第15章 自动化任务

```sh
#!/bin/sh
while :
do
  /sbin/iwconfig eth0 | grep Link | tr '\n' ' 'r
done
```

该脚本输出结果，然后通过 `tr` 命令对输出进行格式化。结果是一个不断更新的单行信息的动画：

Link Quality:92/92 Signal level:-11 dB Noise level:-102 dBm

这种技术可以用于为 X 创建一个图形化监控客户端，输出网络接口的流量信息和活动状态：

```sh
#!/bin/sh
xterm -geometry 75x22 -e \
bash -c \
while : ; do \
  /sbin/ifconfig eth0 | \
  grep 'TX bytes' | \
  tr '\n' ' 'r; \
done
```

这个简单的示例使用了 `bash` 命令行脚本（通过 `-c` 启用）来重复执行命令。命令行将 `ifconfig` 命令的输出通过给 `grep`，`grep` 搜索 `ifconfig` 的输出，然后将包含字符串 "TX bytes" 的行传递给 `tr` 命令。`tr` 命令随后删除行尾的回车符，以便在由 `-geometry` 选项自动调整的 `/xterm` X11 窗口内显示信息：

RX bytes:4117594780 (3926.8 Mb) TX bytes:452230967 (431.2 Mb)

无限循环非常有用，因此 Linux 包含一个重复执行给定命令行的命令。例如，你可以使用 `sensors` 命令快速获取系统硬件健康状况报告。与其使用 shell 脚本无限循环输出，不如使用 `watch` 命令重复显示信息并提供简单的动画：

```bash
$ sensors -f | cut -c 1-20
```

在 `dksh` 和 `bash` 中，`while` 循环控制结构使用以下格式：

```
while expression
do
  statements
done
```

在 `tcsh` 中，使用以下格式：

```tcsh
while (expression)
  Statements
done
```

# 编写和执行 Shell 脚本

如果你想加上前五个偶数，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

```bash
#!///bash
loopcount=0
result=0
while [ $loopcount -lt 5 ]
do
  loopcount=`expr $loopcount + 1`
  increment=`expr $loopcount \* 2`
  result=`expr $result + $increment`
done
```

在 `tsch` 中，该程序可以写如下：

```tcsh
#!/bin/tsch
set loopcount = 0
set result = 0
while [ $loopcount < 5 ]
  set loopcount=`expr $loopcount + 1`
  set increment=`expr $loopcount \* 2`
  set result=`expr $result + $increment`
end

echo "result is $result"
```

## until 语句

`until` 语句用于执行一系列命令，直到指定的条件为真。一旦指定的条件求值为真，循环就会终止。

在 `pdksh` 和 `bash` 中，使用以下格式：

```bash
until expression
do
statements
done
```

可以看出，`until` 语句的格式与 `while` 语句相似，但逻辑不同：在 `while` 循环中，你一直执行到表达式为假；而在 `until` 循环中，你一直循环到表达式为真。

如果你想加上前五个偶数，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

```bash
#!//bin/bash
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

这里的示例与 `while` 语句的示例相同，区别在于测试的条件与 `while` 语句中指定的条件相反。

`tcsh` shell 不支持 `until` 语句。

# repeat 语句 (tcsh)

`repeat` 语句用于固定次数地只执行一条命令。

如果你想在屏幕上每行打印一个连字符 `-`，共80次，可以使用以下命令：

```tcsh
repeat 80 echo '-'
```

# select 语句 (pdksh)

如果你正在编写一个期望用户在线输入的 shell 程序，`select` 语句用于生成菜单列表。`select` 语句的格式如下：

```bash
select item in itemlist
do
  Statements
done
```

`itemlist` 是可选的。如果没有提供，系统将逐个遍历项目项。但如果提供了 `itemlist`，系统将为 `itemlist` 中的每个项目进行迭代，并将 `itemlist` 的当前值赋值给 `item`，该值随后可以作为执行语句的一部分。

如果你想写一个让用户选择“继续 (Continue)”或“完成 (Finish)”的菜单，可以编写以下 shell 程序：

```ksh
#!/bin/ksh
select item in Continue Finish
do
  if [ $item = "Finish" ]; then
    break
  fi
done
```

当执行 `select` 命令时，系统向用户显示一个带有数字选项的菜单——在这种情况下，1 代表 Continue，2 代表 Finish。如果用户选择 1，变量 `item` 的值为 Continue；如果用户选择 2，变量 `item` 的值为 Finish。当用户选择 2 时，执行 `if` 语句并终止循环。

# shift 语句

`shift` 语句用于从左到右逐个处理位置参数。你可能还记得，位置参数被标识为 `$1`, `$2`, `$3` 等。`shift` 命令的作用是每个位置参数都向左移动一位，并且当前的 `$1` 参数丢失。

当你编写允许用户传递各种选项的 shell 程序时，`shift` 语句非常有用。根据指定的选项，后续的参数可能具有不同的含义，或者可能完全不存在。

`shift` 命令的格式如下：

```bash
shift number
```

参数 `number` 是要移动的位数，是可选的。如果没有指定，默认值为 1；即参数向左移动一位。如果指定，参数将向左移动 `number` 位。

# if 语句

`if` 语句通过评估逻辑表达式来做出决策。在 `pdksh` 和 `bash` 中，格式为：

```bash
if [ expression ]; then
  Statements
elif [ expression ]; then
  Statements
else
  Statements
fi
```

在 `tcsh` 中，`if` 语句有两种形式。第一种形式是：

```tcsh
if (expression) then
  Statements
else if (expression) then
  Statements
else
  Statements
endif
```

`tcsh` 的 `if` 条件的第二种形式是：

```tcsh
if (expression) command
```

# case 语句

`case` 语句用于根据匹配指定变量的离散值或取值范围来执行语句。在大多数情况下，如果你有大量的条件，可以使用 `case` 语句来代替 `if` 语句。

`pdsh` 和 `bash` 的 `case` 语句格式如下所示：
