

## 调查数组变量与函数

现在，当你在 `func1` 函数内使用 `$temp` 变量时，它不会影响主脚本中分配给 `$temp` 变量的值。

第 5 章“理解 Shell”讨论了一种高级方法，通过使用数组，允许单个变量持有多个值。在函数中使用数组变量值有些棘手，并且有一些特殊的考量。本节描述了一种技术，允许你在函数中使用数组变量值。

### 将数组传递给函数

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

### 从函数返回数组

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

然后，`arraydblr` 函数使用 `echo` 语句输出数组变量值的各个值。脚本使用 `arraydblr` 函数的输出来将值重新组合成一个新的数组变量。

## 考虑函数递归

局部函数变量提供的特性之一是*自我封闭性*。自我封闭的函数不使用函数外部的任何资源，*除了*脚本通过命令行传递给它的变量。

这一特性使函数可以被*递归*调用，这意味着函数调用自身以得出答案。通常，递归函数有一个基准值，最终会迭代到该值。许多高级数学算法使用递归，反复将复杂方程降低一级，直到达到由基准值定义的水平。

递归算法的经典例子是计算阶乘。一个数的阶乘是前面所有数与该数的乘积。因此，要找到 5 的阶乘，你需要执行以下方程：

`5! = 1 * 2 * 3 * 4 * 5 = 120`

使用递归，方程被简化为以下格式：

`x! = x * (x-1)!`

或者用英语来说，x 的阶乘等于 x 乘以 x-1 的阶乘。这可以用一个简单的递归脚本来表达：

```bash
function factorial {  
    if [ $1 -eq 1 ]  
    then  
        echo 1  
    else  
        local temp=$[ $1 - 1 ]  
        local result=$(factorial $temp)  
        echo $[ $result * $1 ]  
    fi  
}
```

`factorial` 函数使用自身来计算阶乘的值：

```bash
$ cat test13  
#!/bin/bash  
# using recursion  
function factorial {  
    if [ $1 -eq 1 ]  
    then  
        echo 1  
    else  
        local temp=$[ $1 - 1 ]  
        local result=$(factorial $temp)  
        echo $[ $result * $1 ]  
    fi  
}  
read -p "Enter value: " value  
result=$(factorial $value)  
echo "The factorial of $value is: $result"  
$ ./test13  
Enter value: 5  
The factorial of 5 is: 120  
$
```

使用 `factorial` 函数很容易。创建了这样的函数后，你可能希望将其用于其他脚本。接下来，看看如何高效地做到这一点。

## 创建库

显而易见，函数可以帮助在单个脚本中节省打字工作，但如果你在多个脚本之间恰好使用了相同的单个代码块怎么办？如果你必须在每个脚本中定义相同的函数，而在每个脚本中只使用一次，那就显然是具有挑战性的。

这个问题有一个解决方案！Bash shell 允许你为你的函数创建一个*库文件*，然后在需要的任意数量的脚本中引用这个单一的库文件。

该过程的第一步是创建一个公共库文件，其中包含脚本中需要的函数。这里是一个名为 `myfuncs` 的简单库文件，定义了三个简单函数：

```bash
$ cat myfuncs
# my script functions

function addem {
    echo $[ $1 + $2 ]
}

function multem {
    echo $[ $1 \* $2 ]
}

function divem {
    if [ $2 -ne 0 ]
    then
        echo $[ $1 / $2 ]
    else
        echo -1
    fi
}
$  
```

下一步是将 `myfuncs` 库文件包含在希望使用其中任何函数的脚本文件中。这是棘手的地方。

问题在于 shell 函数的作用域。与环境变量一样，shell 函数仅在你定义它们的 shell 会话中有效。如果你从 shell 命令行接口提示符运行 `myfuncs` shell 脚本，shell 会创建一个新的 shell 并在该新 shell 中运行脚本。这为那个 shell 定义了三个函数，但当你尝试运行另一个使用这些函数的脚本时，它们不可用。

这也适用于脚本。如果你只是尝试将库文件作为普通脚本文件运行，函数不会出现在你的脚本中：

```bash
$ cat badtest4
#!/bin/bash
# using a library file the wrong way
./myfuncs

result=$(addem 10 15)
echo "The result is $result"
$ ./badtest4
./badtest4: addem: command not found
The result is
$  
```

