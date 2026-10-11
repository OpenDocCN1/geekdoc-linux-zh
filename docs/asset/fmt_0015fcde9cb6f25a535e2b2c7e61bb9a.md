
```bash
$ cat test16
#!/bin/bash
# using until and while loops

var1=3

until [ $var1 -eq 0 ]
do
    echo "Outer loop: $var1"
    var2=1
    while [ $var2 -lt 5 ]
    do
        var3=$(echo "scale=4; $var1 / $var2" | bc)
        echo "    Inner loop: $var1 / $var2 = $var3"
        var2=$[ $var2 + 1 ]
    done
    var1=$[ $var1 - 1 ]
done
$ ./test16
Outer loop: 3
    Inner loop: 3 / 1 = 3.0000
    Inner loop: 3 / 2 = 1.5000
    Inner loop: 3 / 3 = 1.0000
    Inner loop: 3 / 4 = .7500
Outer loop: 2
    Inner loop: 2 / 1 = 2.0000
    Inner loop: 2 / 2 = 1.0000
    Inner loop: 2 / 3 = .6666
    Inner loop: 2 / 4 = .5000
Outer loop: 1
    Inner loop: 1 / 1 = 1.0000
    Inner loop: 1 / 2 = .5000
    Inner loop: 1 / 3 = .3333
    Inner loop: 1 / 4 = .2500
$
```

外层 `until` 循环从值 3 开始，直到值等于 0 时停止。内层 `while` 循环从值 1 开始，只要值小于 5 就继续执行。每个循环都必须更改用于测试条件的值，否则循环将陷入无限循环。

### 遍历文件数据

通常，你必须遍历存储在文件中的项目。这需要结合两种已介绍的技术：

- 使用嵌套循环
- 更改 `IFS` 环境变量

通过更改 `IFS` 环境变量，你可以强制 `for` 命令将文件中的每一行作为单独的项目进行处理，即使数据中包含空格。在从文件中提取单独一行后，你可能需要再次循环以提取包含在内的数据。

处理 `/etc/passwd` 文件中的数据是这种情况的经典示例。这要求你逐行遍历 `/etc/passwd` 文件，然后将 `IFS` 变量的值更改为冒号，以便你可以分隔每行中的各个组件。

以下是一个执行此操作的示例：

```bash
#!/bin/bash
# changing the IFS value

IFS.OLD=$IFS
IFS=$' \n'
for entry in $(cat /etc/passwd)
do
    echo "Values in $entry --"
    IFS=:
    for value in $entry
    do
        echo "     $value"
    done
done
$
```

此脚本使用两个不同的 `IFS` 值来解析数据。第一个 `IFS` 值解析 `/etc/passwd` 文件中的各个行。内层 `for` 循环随后将 `IFS` 值更改为冒号，这允许你解析 `/etc/passwd` 行内的各个值。

运行此脚本时，你会得到类似以下内容：

```text
Values in rich:x:501:501:Rich Blum:/home/rich:/bin/bash --
rich
x
501
501
Rich Blum
/home/rich
/bin/bash

Values in katie:x:502:502:Katie Blum:/home/katie:/bin/bash --
katie
x
502
502
Katie Blum
/home/katie
/bin/bash
```

内层 `loop` 解析 `/etc/passwd` 条目中的每个单独值。这也是一种处理逗号分隔数据的好方法，电子表格数据通常就是这样导入的。

### 控制循环

你可能会认为，一旦开始循环，你就被困住直到循环完成所有迭代。事实并非如此。有几个命令有助于控制循环内部发生的情况：

- `break` 命令
- `continue` 命令

每个命令在控制循环操作方面有不同的用途。以下部分描述了你如何使用这些命令来控制循环的操作。

#### `break` 命令

`break` 命令是一种从正在进行的循环中逃逸的简单方法。你可以使用 `break` 命令退出任何类型的循环，包括 `while` 和 `until` 循环。

你可以在几种情况下使用 `break` 命令。本节展示了这些方法中的每一种。

##### 跳出单个循环

当 shell 执行 `break` 命令时，它尝试跳出当前正在处理的循环：

```bash
$ cat test17
#!/bin/bash
# breaking out of a for loop

for var1 in 1 2 3 4 5 6 7 8 9 10
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration number: $var1"
done
echo "The for loop is completed"
$ ./test17
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
The for loop is completed
$
```

`for` 循环通常应该遍历列表中指定的所有值。但是，当满足 `if-then` 条件时，shell 执行了 `break` 命令，从而停止了 `for` 循环。

这种技术也适用于 `while` 和 `until` 循环：

```bash
$ cat test18
#!/bin/bash
# breaking out of a while loop

var1=1

while [ $var1 -lt 10 ]
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration: $var1"
    var1=$[ $var1 + 1 ]
done

echo "The while loop is completed"
$ ./test18
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
The while loop is completed
$
```

当满足 `if-then` 条件时，`while` 循环终止并执行了 `break` 命令。

##### 跳出内层循环

当你处理多个循环时，`break` 命令会自动终止你当前所处的最内层循环：

```bash
$ cat test19
#!/bin/bash
# breaking out of an inner loop

for( ( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for( ( b = 1; b < 100; b++ ))
    do
        if [ $b -eq 5 ]
        then
            break
        fi
        echo "    Inner loop: $b"
    done
done
$ ./test19
Outer loop: 1
    Inner loop: 1
    Inner loop: 2
    Inner loop: 3
    Inner loop: 4
Outer loop: 2
    Inner loop: 1
    Inner loop: 2
    Inner loop: 3
    Inner loop: 4
Outer loop: 3
    Inner loop: 1
    Inner loop: 2
    Inner loop: 3
    Inner loop: 4
$
```

内层循环中的 `for` 语句指定要迭代直到 `b` 变量等于 `100`。然而，内层循环中的 `if-then` 语句指定当 `b` 变量值等于 `5` 时，执行 `break` 命令。请注意，即使内层循环因 `break` 命令而终止，外层循环仍按指定方式继续工作。

##### 跳出外层循环

有时你可能处于内层循环中，但需要停止外层循环。`break` 命令包含一个命令行参数值：

```bash
break n
```

其中 $n$ 指示要跳出的循环级别。默认情况下，$n$ 为 $1$，表示跳出当前循环。如果你将 $n$ 设置为 $2$，`break` 命令将停止下一层的外层循环：
