
在上面的示例中，会为每个文件创建备份副本。如果副本创建失败，系统将生成一条消息。

以下是在 tcsh 中的相同示例：

```tcsh
#!/bin/tcsh
foreach filename (`/bin/ls`)
    cp $filename backup/$filename
    if ($? != 0) then
        echo "copy for $filename failed"
    endif
end
```

## The while 语句

while 语句可以在指定条件为真时执行一系列命令。一旦指定条件计算结果为假，循环立即终止。如果指定条件最初计算结果为假，那么循环可能完全不执行。你应该谨慎使用 while 命令，因为如果指定条件永远不计算为假，循环将永远不终止。

**无尽循环在 Shell 程序中有其用武之地**

无尽循环有时是有用的。例如，你可以使用几行脚本轻松构建一个简单的命令，该命令不断监视网络接口的 802.11b 链路质量：

```bash
#!/bin/sh
while :
do
    /sbin/ifconfig eth0 | grep Link | tr '\n' '\r'
done
```

脚本输出搜索，然后 tr 命令对输出进行格式化。结果是一个简单的动画，显示一条不断更新的信息行：

Link Quality:92/92  Signal level:-11 dBm  Noise level:-102 dBm

这种技术还可以用于创建 X 的图形监控客户端，输出关于网络接口的流量信息和活动：

```bash
#!/bin/sh
xterm -geometry 75x2 -e \
bash -c \
"while :; do \
    /sbin/ifconfig eth0 | \
    grep 'TX bytes' | \
    tr '\n' '\r' ; \
done"
```

这个简单示例使用 bash 命令行脚本（通过 -c 启用）来反复执行一条命令行。该命令行将 ifconfig 命令的输出通过 grep 管道传递，grep 搜索 ifconfig 的输出，然后包含字符串 "TX bytes" 的行通过管道传递给 tr 命令。tr 命令随后移除行尾的回车，以在由 -geometry 选项自动调整大小的 xterm X11 终端窗口中显示信息：

```
RX bytes:4117594780 (3926.8 Mb) TX bytes:452230967 (431.2 Mb)
```

无尽循环是如此有用，以至于 Linux 包含一个命令，可以反复执行给定的命令行。例如，你可以使用 sensors 命令快速了解系统硬件健康状况的报告。但是，不使用 shell 脚本无限制地循环输出信息，你可以使用 watch 命令重复信息并提供简单的动画：

```bash
$ watch "sensors -f | cut -c 1-20"
```

在 pdksh 和 bash 中，while 流程控制结构使用以下格式：

```bash
while expression
do
    statements
done
```

在 tcsh 中，使用以下格式：

```tcsh
while (expression)
    Statements
end
```

如果你想添加前五个偶数，你可以在 pdksh 和 bash 中使用以下 shell 程序：

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

在 tcsh 中，该程序可以写成如下形式：

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

### until 语句

until 语句可以在指定条件为真之前执行一系列命令。

一旦指定条件计算结果为**真**，循环即终止。

在 `pdksh` 和 `bash` 中，使用以下格式：

```bash
until expression
do
    statements
done
```

可以看出，until 语句的格式与 while 语句相似，但逻辑不同：在 while 循环中，你执行直到表达式为**假**，而在 until 循环中，你循环直到表达式为**真**。

如果你想添加前五个偶数，你可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：

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

这里的示例与 while 语句的示例完全相同，除了测试的条件只是 while 语句中指定条件的相反。

`tcsh` shell 不支持 until 语句。

## repeat 语句（tcsh）

repeat 语句用于将单一命令执行固定次数。

如果你想在屏幕上每行打印一个连字符 (-) 共 80 次，可以使用以下命令：

```bash
repeat 80 echo '-'
```

## select 语句（pdksh）

select 语句用于在你编写期望用户在线输入的 shell 程序时生成菜单列表。select 语句的格式如下：

```ksh
select item in itemlist
do
    Statements
done
```

itemlist 是可选的。如果未提供，系统将依次遍历每个条目。但是，如果提供了 itemlist，系统将遍历 itemlist 中的每个条目，并且每次迭代都会将 itemlist 的当前值分配给 item，该值随后可以作为被执行语句的一部分使用。

如果你想编写一个菜单，让用户选择继续（Continue）或结束（Finish），可以编写以下 shell 程序：

```bash
#!/bin/ksh
select item in Continue Finish
do
    if [ $item = "Finish" ]; then
        break
    fi
done
```

当 select 命令执行时，系统向用户显示带有数字选项的菜单——在此情况下，1 代表 Continue，2 代表 Finish。如果用户选择 1，变量 item 包含值为 Continue；如果用户选择 2，变量 item 包含值为 Finish。当用户选择 2 时，执行 if 语句并终止循环。

## shift 语句

shift 语句用于从左到右逐个处理位置参数。如你回忆的那样，位置参数被标识为 $1、$2、$3，等等。shift 命令的效果是每个位置参数向左移动一个位置，而当前的 $1 参数丢失。

`shift` 语句在你编写用户可以传递各种选项的 shell 程序时很有用。根据指定的选项，后面的参数可能具有不同的含义，或者根本不存在。

`shift` 命令的格式如下：

```bash
shift    number
```

参数 `number` 是要移动的位置数，是可选的。如果未指定，默认值为 1；即参数向左移动一个位置。如果指定，则参数向左移动 `number` 个位置。

## if 语句

`if` 语句评估逻辑表达式以做出决策。在 `pdksh` 和 `bash` 中，`if` 条件的格式如下：

```bash
if [ expression ]; then
    Statements
elif [ expression ]; then
    Statements
else
    Statements
fi
```

`if` 条件可以嵌套。也就是说，一个 `if` 条件可以包含另一个 `if` 条件。`if` 条件不需要有 `elif` 或 `else` 部分。如果 `if` 语句中指定的表达式（在后续可选的 `elif` 语句中也是可选的）都不为真，则执行 `else` 部分。单词 `fi` 用于指示 `if` 语句的结束，如果在嵌套的 `if` 条件中非常有用。在这种情况下，你应该能够将 `fi` 与 `if` 配对，以确保所有 `if` 语句都正确编码。

在以下 `bash` 或 `pdksh` 的示例中，变量 `var` 可以具有两个值之一：Yes 或 No。其他值都是无效的。可以按如下方式编码：

```bash
if [ $var = "Yes" ]; then
    echo "Value is Yes"
elif [ $var = "No" ]; then
    echo "Value is No"
else
    echo "Invalid value"
fi
```

在 `tcsh` 中，`if` 语句有两种形式。第一种形式类似于 `pdksh` 和 `bash` 中的形式，如下所示：

```tcsh
if (expression) then
    Statements
```

