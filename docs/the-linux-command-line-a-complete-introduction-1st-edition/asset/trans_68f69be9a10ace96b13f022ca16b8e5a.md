

# 28

## READING KEYBOARD INPUT

我们迄今为止编写的脚本缺少大多数计算机程序共有的一个特性——*交互性*，即程序能够与用户交互的能力。虽然许多程序不需要交互，但一些程序从能够直接接受用户输入中受益。例如，上一章中的这个脚本：

```
#!/bin/bash

# test-integer2: evaluate the value of an integer.

INT=-5

if [[ "$INT" =~ ^-[0-9]+$ ]]; then
        if [ $INT -eq 0 ]; then
                echo "INT is zero."
        else
                if [ $INT -lt 0 ]; then
                        echo "INT is negative."
                fi
        fi
fi
```

```
else
    echo "INT is positive."
fi
if [ $((${INT} % 2)) -eq 0 ]; then
    echo "INT is even."
else
    echo "INT is odd."
fi
fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

每次我们想更改 INT 的值时，都必须编辑脚本。如果脚本能够询问用户输入一个值，将会更有用。在本章中，我们将开始研究如何为程序添加交互性。

## read—Read Values from Standard Input

read 内置命令用于读取标准输入的一行。此命令可用于读取键盘输入，或在重定向时从文件中读取一行数据。该命令的语法如下：

read [-options] [variable...]

其中 options 是表 28-1 中列出的可用选项中的一个或多个，variable 是用于保存输入值的变量名的一个或多个。如果没有提供变量名，shell 变量 REPLY 将包含数据行。

### Table 28-1: read Options

| Option | Description |
|---|---|
| -a array | 将输入分配给 array，从索引零开始。我们将在第 35 章介绍数组。 |
| -d delimiter | 字符串 delimiter 中的第一个字符用于指示输入结束，而不是换行符。 |
| -e | 使用 Readline 处理输入。这允许以与命令行相同的方式编辑输入。 |
| -n num | 读取 num 个字符的输入，而不是整行。 |
| -p prompt | 使用字符串 prompt 显示输入提示。 |
| -r | 原始模式。不要将反斜杠字符解释为转义字符。 |
| -s | 静默模式。输入时不要将字符回显到显示屏。这在输入密码和其他机密信息时很有用。 |
| -t seconds | 超时。在 seconds 后终止输入。如果输入超时，read 将返回非零退出状态。 |
| -u fd | 使用文件描述符 fd 的输入，而不是标准输入。 |

基本上，read 将标准输入的字段分配给指定的变量。如果我们修改整数评估脚本以使用 read，它可能看起来像这样：

```
#!/bin/bash

# read-integer: evaluate the value of an integer.

echo -n "Please enter an integer -> "
read int

if [[ "$int" =~ ^-?[0-9]+$ ]]; then
    if [ $int -eq 0 ]; then
        echo "$int is zero."
    else
        if [ $int -lt 0 ]; then
            echo "$int is negative."
        else
            echo "$int is positive."
        fi
        if [ $(($int % 2)) -eq 0 ]; then
            echo "$int is even."
        else
            echo "$int is odd."
        fi
    fi
else
    echo "Input value is not an integer." >&2
    exit 1
fi
```

我们使用 -n 选项 echo 以显示提示而不输出尾随换行，然后使用 read 为变量 int 输入值。运行此脚本的结果如下：

```
[me@linuxbox ~]$ read-integer
Please enter an integer -> 5
5 is positive.
5 is odd.
```

read 可以将输入分配给多个变量，如本脚本所示：

```
#!/bin/bash

# read-multiple: read multiple values from keyboard
echo -n "Enter one or more values > "
read var1 var2 var3 var4 var5
echo "var1 = '$var1'"
echo "var2 = '$var2'"
echo "var3 = '$var3'"
echo "var4 = '$var4'"
echo "var5 = '$var5'"
```

在此脚本中，我们分配并显示最多五个值。请注意 read 在给定不同数量的值时的行为：

```
[me@linuxbox ~]$ read-multiple
Enter one or more values > a b c d e
var1 = 'a'
var2 = 'b'
var3 = 'c'
var4 = 'd'
var5 = 'e'
[me@linuxbox ~]$ read-multiple
Enter one or more values > a
var1 = 'a'
var2 = ''
var3 = ''
var4 = ''
var5 = ''
[me@linuxbox ~]$ read-multiple
Enter one or more values > a b c d e f g
var1 = 'a'
var2 = 'b'
var3 = 'c'
var4 = 'd'
var5 = 'e f g'
```

如果 read 接收到的值少于预期数量，额外的变量为空，而过多的输入会导致最后一个变量包含所有额外输入。

如果 read 命令后没有列出变量，shell 变量 REPLY 将被分配所有输入：

```
#!/bin/bash

# read-single: read multiple values into default variable
echo -n "Enter one or more values > "
read
echo "REPLY = "$REPLY""
```

