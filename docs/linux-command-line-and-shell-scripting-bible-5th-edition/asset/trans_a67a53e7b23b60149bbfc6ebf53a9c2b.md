
## 使用函数输出

正如你可以将命令的输出捕获到 Shell 变量中一样，你也可以将函数的输出捕获到 Shell 变量中。你可以使用这种技术从函数中获取任何类型的输出并将其赋值给变量：

```bash
result=$(dbl)
```

该命令将 `dbl` 函数的输出赋值给 `$result` Shell 变量。下面是一个在脚本中使用此方法的示例：

```bash
$ cat test5b
#!/bin/bash
# 使用 echo 返回一个值

function dbl {
    read -p "Enter a value: " value
    echo $[ $value * 2 ]
}

result=$(dbl)
echo "The new value is $result"
$ ./test5b
Enter a value: 200
The new value is 400
$ ./test5b
Enter a value: 1000
The new value is 2000
$
```

新函数现在使用 `echo` 语句来显示计算结果。脚本只是捕获了 `dbl` 函数的输出，而不是查看退出状态以获取答案。

这个例子展示了一个细微的技巧。你会注意到 `dbl` 函数实际上输出了两条消息。`read` 命令会输出一个简短的消息，询问用户输入值。Bash Shell 脚本足够智能，不会将此视为 `STDOUT` 输出的一部分，因此会忽略它。如果你使用 `echo` 语句来生成这个询问用户的消息，它也会被 Shell 变量捕获，连同输出值一起被获取。

> **注意**
> 使用这种技术，你还可以返回浮点数和字符串值，这使得该方法成为从函数中返回值的一种极其通用的方式。

## 在函数中使用变量

你可能已经注意到，在上一节的 `test5` 示例中，我在函数内使用了一个名为 `$value` 的变量来持有它处理值。当你在函数中使用变量时，你需要对如何定义和处理它们稍加小心。这是 Shell 脚本中问题的一个常见原因。本节介绍了处理变量的几种技术，既包括在 Shell 脚本函数内部，也包括在外部。

### 向函数传递参数

如前文“从函数返回值”部分所述，Bash Shell 将函数视为迷你脚本。这意味着你可以像普通脚本那样向函数传递参数（参见第 14 章“处理用户输入”）。

函数可以使用标准的参数环境变量来表示在命令行上传递给函数的任何参数。例如，函数的名称定义在 `$0` 变量中，而函数命令行上的任何参数都使用 `$1`、`$2` 等变量定义。你还可以使用特殊变量 `$#` 来确定传递给函数的参数数量。

在脚本中指定函数时，你必须在与函数相同的命令行上提供参数，例如：

```bash
func1 $value1 10
```

然后，函数可以使用参数环境变量检索参数值。下面是使用此方法向函数传递值的示例：

```bash
$ cat test6
#!/bin/bash
# 向函数传递参数

function addem {
    if [ $# -eq 0 ] || [ $# -gt 2 ]
    then
        echo -1
    elif [ $# -eq 1 ]
    then
        echo $(( $1 + $1 ))
    else
        echo $(( $1 + $2 ))
    fi
}

echo -n "Adding 10 and 15: "
value=$(addem 10 15)
echo $value
echo -n "Let's try adding just one number: "
value=$(addem 10)
echo $value
echo -n "Now try adding no numbers: "
value=$(addem)
echo $value
echo -n "Finally, try adding three numbers: "
value=$(addem 10 15 20)
echo $value
$
$ ./test6
Adding 10 and 15: 25
Let's try adding just one number: 20
Now try adding no numbers: -1
Finally, try adding three numbers: -1
$
```

`test6` 脚本中的 `addem` 函数首先检查脚本传递给它的参数数量。如果没有参数或者参数多于两个，`addem` 返回值为 -1。如果只有一个参数，`addem` 将该参数加到自身上作为结果。如果有两个参数，`addem` 将它们相加作为结果。

由于函数使用特殊的参数环境变量作为其自身的参数值，它无法直接访问脚本命令行中的脚本参数值。下面的示例失败了：

```bash
$ cat badtest1
#!/bin/bash
# 尝试在函数内部访问脚本参数

function badfunc1 {
    echo $(( $1 * $2 ))
}

if [ $# -eq 2 ]
then
    value=$(badfunc1)
    echo "The result is $value"
else
    echo "Usage: badtest1 a b"
fi
$
$ ./badtest1
Usage: badtest1 a b
$ ./badtest1 10 15
./badtest1: * : syntax error: operand expected (error token is "* " )
The result is
$
```

即使函数使用了 `$1` 和 `$2` 变量，它们也不是主脚本部分可用的同一个 `$1` 和 `$2` 变量。相反，如果你想在函数中使用这些值，你必须在调用函数时手动传递它们：

```bash
$ cat test7
#!/bin/bash
# 尝试在函数内部访问脚本参数

function func7 {
    echo $(( $1 * $2 ))
}

if [ $# -eq 2 ]
then
    value=$(func7 $1 $2)
    echo "The result is $value"
else
    echo "Usage: test7 a b"
fi
$
$ ./test7
Usage: test7 a b
$ ./test7 10 15
The result is 150
$
```

当你将 `$1` 和 `$2` 变量传递给函数时，它们变得可供函数使用，就像其他任何参数一样。

### 处理函数中的变量

让 Shell 脚本程序员感到困惑的一件事是变量的作用域。作用域是变量可见的范围。在函数中定义的变量可能具有与普通变量不同的作用域——也就是说，它们可能对脚本的其余部分隐藏。

函数使用两种类型的变量：

-   全局变量
-   局部变量

接下来的部分描述了如何在函数中使用这两种类型的变量。

### 全局变量

全局变量是在 Shell 脚本任何地方都有效的变量。如果你在脚本的主部分定义了一个全局变量，你可以函数内部检索其值。同样，如果你在函数内部定义了一个全局变量，你可以在脚本的主部分检索其值。

默认情况下，你在脚本中定义的任何变量都是全局变量。在函数外部定义的变量可以在函数内部正常访问：

```bash
$ cat test8
#!/bin/bash
# 使用全局变量传递值

function dbl {
    value=$(( $value * 2 ))
}

read -p "Enter a value: " value
dbl
echo "The new value is: $value"

$ ./test8
Enter a value: 450
The new value is: 900
$
```

`$value` 变量在函数外部定义，并在函数外部赋值。当调用 `dbl` 函数时，该变量及其值在函数内部仍然有效。当在函数内部为变量分配新值时，当脚本引用该变量时，新值仍然有效。

然而，这种做法可能很危险，特别是如果你打算在不同的 Shell 脚本中使用你的函数。它要求你确切知道函数中使用了哪些变量，包括用于计算未返回给脚本的值的任何变量。下面是事情可能出错的示例：

```bash
$ cat badtest2
#!/bin/bash
# 演示变量的错误使用

function func1 {
    temp=$(( $value + 5 ))
    result=$(( $temp * 2 ))
}

temp=4
value=6

func1
echo "The result is $result"
if [ $temp -gt $value ]
then
    echo "temp is larger"
else
    echo "temp is smaller"
fi
$
$ ./badtest2
The result is 22
temp is larger
$
```

由于 `$temp` 变量在函数中被使用，其在脚本中的值被破坏，导致产生了你可能非预期的结果。在下一节中展示了如何在函数中轻松解决此问题的方法。

### 局部变量

与其在函数中使用全局变量，不如将函数内部使用的任何变量声明为局部变量。为此，只需在变量声明前添加 `local` 关键字：

```bash
local temp
```

你还可以在将值赋值给变量的赋值语句中使用 `local` 关键字：

```bash
local temp=$(( value + 5 ))
```

`local` 关键字确保该变量仅限于函数内部使用。如果脚本中函数外部出现了同名的变量，Shell 会将两个变量的值分开保持。这意味着你可以轻松地将函数变量与脚本变量分开，并仅共享你想要共享的那些：

```bash
$ cat test9
#!/bin/bash
# 演示 local 关键字

function func1 {
    local temp=$(( value + 5 ))
    local result=$(( temp * 2 ))
}

temp=4
value=6

func1
echo "The result is $result"
if [ $temp -gt $value ]
then
    echo "temp is larger"
else
    echo "temp is smaller"
fi
$
$ ./test9
The result is 22
temp is smaller
$
```
