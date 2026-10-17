
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

### 调查数组变量与函数

现在，当你在 `func1` 函数内使用 `$temp` 变量时，它不会影响主脚本中分配给 `$temp` 变量的值。

第 5 章“理解 Shell”讨论了一种高级方法，通过使用数组，允许单个变量持有多个值。在函数中使用数组变量值有些棘手，并且有一些特殊的考量。本节描述了一种技术，允许你在函数中使用数组变量值。

#### 将数组传递给函数

将数组变量传递给脚本函数的艺术可能会令人困惑。如果你尝试将数组变量作为单个参数传递，它不会起作用：

```bash
$ cat badtest3
#!/bin/bash
# trying to pass an array variable

function testit {
    echo "The parameters are: $@"
    thisarray=$1
    echo "The received array is ${thisarray[*]}"
}
myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}"
testit $myarray
$
$ ./badtest3
The original array is: 1 2 3 4 5
The parameters are: 1
The received array is 1
$ 
```

如果你尝试将数组变量用作函数参数，该函数只会获取数组变量的第一个值。

为了解决这个问题，你必须将数组变量拆解为其各个值，并将这些值作为函数参数使用。在函数内部，你可以将所有参数重新组合成一个新数组变量。以下是一个执行此操作的示例：

```bash
$ cat test10
#!/bin/bash
# array variable to function test

function testit {
    local newarray
    newarray=("$@")
    echo "The new array value is: ${newarray[*]}"
}
myarray=(1 2 3 4 5)
echo "The original array is ${myarray[*]}"
testit ${myarray[*]}
$ ./test10
The original array is 1 2 3 4 5
The new array value is: 1 2 3 4 5
$
```

该脚本使用 `$myarray` 变量来保存所有的单个数组值，并将它们全部放置在函数的命令线上。然后，函数从命令行参数中重建数组变量。一旦进入函数内部，该数组就可以像其他任何数组一样使用：

```bash
$ cat test11
#!/bin/bash
# adding values in an array

function addarray {
    local sum=0
    local newarray
    newarray=($(echo "$*"))
    for value in ${newarray[*]}
    do
        sum=$[ $sum + $value ]
    done
    echo $sum
}
myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}"
arg1=$(echo ${myarray[*]})
result=$(addarray $arg1)
echo "The result is $result"
$ ./test11
The original array is: 1 2 3 4 5
The result is 15
$
```

`addarray` 函数遍历数组值并将它们相加。你可以在 `myarray` 数组变量中放入任意数量的值，`addarray` 函数会将它们相加。

#### 从函数返回数组

将数组变量从函数返回到 shell 脚本使用类似的技术。该函数使用 `echo` 语句按正确的顺序输出单个数组值，脚本必须将它们重新组合成一个新数组变量：

```bash
$ cat test12
#!/bin/bash
# returning an array value

function arraydblr {
    local origarray
    local newarray
    local elements
    local i
    origarray=($(echo "$1"))
    newarray=($(echo "$1"))
    elements=$[ ${#origarray[@]} - 1 ]
    for (( i = 0; i <= $elements; i++ ))
    {
        newarray[$i]=$[ ${origarray[$i]} * 2 ]
    }
    echo ${newarray[*]}
}

myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}"
arg1=$(echo ${myarray[*]})
result=$(arraydblr $arg1)
echo "The new array is: ${result[*]}"
$ ./test12
The original array is: 1 2 3 4 5
The new array is: 2 4 6 8 10
```

脚本使用 `$arg1` 变量将数组值传递给 `arraydblr` 函数。`arraydblr` 函数将数组重新组合成一个新数组变量，并为输出数组变量制作一个副本。然后，它遍历单个数组变量的值，将每个值加倍，并将其放入函数中数组变量的副本中。
