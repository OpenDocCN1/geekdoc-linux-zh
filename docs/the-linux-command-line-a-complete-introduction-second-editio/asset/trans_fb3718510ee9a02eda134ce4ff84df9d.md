

## 28
读取键盘输入

![](img/314a0280bc10c5c0d45be132de172677_482_0.png)

我们迄今为止编写的脚本缺少大多数计算机程序中常见的功能：*交互性*，即程序与用户交互的能力。虽然许多程序不需要交互，但一些程序从能够直接接受用户输入中受益。例如，上一章中的这个脚本：

```
#!/bin/bash

# test-integer2: evaluate the value of an integer.

INT=-5

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [ "$INT" -eq 0 ]; then
        echo "INT is zero."
    else
        if [ "$INT" -lt 0 ]; then
            echo "INT is negative."
        else
            echo "INT is positive."
        fi
        if [ $((INT % 2)) -eq 0 ]; then
            echo "INT is even."
        else
            echo "INT is odd."
        fi
    fi
```
```
fi
else
  echo "INT is not an integer." >&2
  exit 1
fi
```

每次我们想要更改 INT 的值时，都必须编辑脚本。如果脚本能够询问用户输入值会更有用。在本章中，我们将开始研究如何为我们的程序添加交互性。

## read—从标准输入读取值

read 内置命令用于读取标准输入的一行。此命令可用于读取键盘输入，或在重定向使用时，从文件中读取一行数据。该命令具有以下语法：

```
read [-options] [variable...]
```

其中 options 是稍后在表 28-1 中列出的可用选项中的一个或多个，variable 是用于保存输入值的一个或多个变量的名称。如果没有提供变量名，则 shell 变量 REPLY 包含数据行。

基本上，read 将标准输入的字段分配给指定的变量。如果我们修改整数评估脚本以使用 read，它可能看起来像这样：

```
#!/bin/bash

# read-integer: evaluate the value of an integer.

echo -n "Please enter an integer -> "
read int

if [[ "$int" =~ ^-?[0-9]+$ ]]; then
  if [ "$int" -eq 0 ]; then
    echo "$int is zero."
  else
    if [ "$int" -lt 0 ]; then
      echo "$int is negative."
```
```
else
    echo "$int is positive."
fi
if [ $((int % 2)) -eq 0 ]; then
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

我们使用带有 -n 选项的 echo（该选项抑制输出末尾的换行符）来显示提示，然后使用 read 为变量 int 输入值。运行此脚本的结果如下：

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

在本脚本中，我们分配并显示最多五个值。请注意 read 在给定不同数量的值时的行为，如下所示：

```
[me@linuxbox ~]$ read-multiple
Enter one or more values > a b c d e
var1 = 'a'
var2 = 'b'
var3 = 'c'
```
```
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

如果 read 接收到的值少于预期数量，多余的变量为空，而过多的输入会导致最终变量包含所有额外输入。

如果 read 命令后没有列出变量，则 shell 变量 REPLY 将被分配所有输入。

```
#!/bin/bash

# read-single: read multiple values into default variable
echo -n "Enter one or more values > "
read
echo "REPLY = '$REPLY'"
```

运行此脚本的结果如下：

```
[me@linuxbox ~]$ read-single
Enter one or more values > a b c d
REPLY = 'a b c d'
```

## 选项

read 支持表 28-1 中描述的选项。

表 28-1: read 选项

