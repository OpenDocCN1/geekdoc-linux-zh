
然后，`arraydblr` 函数使用 `echo` 语句输出数组变量值的各个值。脚本使用 `arraydblr` 函数的输出来将值重新组合成一个新的数组变量。

### 考虑函数递归

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

### 创建库

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

## 第三部分：高级 Shell 脚本编程

使用函数库的关键在于 `source` 命令。`source` 命令在当前 shell 上下文中执行命令，而不是创建一个新的 shell 来执行它们。你使用 `source` 命令在你的 shell 脚本内部运行库文件脚本。这样做使这些函数对脚本可用。

`source` 命令有一个快捷别名，称为点运算符。要在 shell 脚本中引入 `myfuncs` 库文件，你只需添加以下行：

```
. ./myfuncs
```

你可能很难看清，但在 `./myfuncs` 命令之前有一个点号（即句点）。此示例假设 `myfuncs` 库文件位于与 shell 脚本相同的目录中。如果不是，你需要使用适当的路径来访问该文件。下面是一个创建使用 `myfuncs` 库文件的脚本的示例：

```
$ cat test14
#!/bin/bash
# 使用在库文件中定义的函数
. ./myfuncs

value1=10
value2=5
result1=$(addem $value1 $value2)
result2=$(multem $value1 $value2)
result3=$(ditem $value1 $value2)
echo "The result of adding them is: $result1"
echo "The result of multiplying them is: $result2"
echo "The result of dividing them is: $result3"
$
$ ./test14
The result of adding them is: 15
The result of multiplying them is: 50
The result of dividing them is: 2
$
```

该脚本成功使用了在 `myfuncs` 库文件中定义的函数。

### 在命令行上使用函数

你可以使用脚本函数来创建一些相当复杂的操作。有时，能够直接在命令行界面中使用这些功能会非常方便。

就像你可以在 shell 脚本中将脚本函数用作命令一样，你也可以在命令行界面中将脚本函数用作命令。这是一个很好的特性，因为你在 shell 中定义函数后，可以从系统中的任何目录使用它；你不必担心脚本是否在 `PATH` 环境变量中。诀窍是让 shell 识别该函数。你可以通过几种方式来实现这一点。

#### 在命令行上创建函数

由于 shell 在你输入时解释命令，因此你可以直接在命令行上定义函数。你可以以两种方式完成此操作。

第一种方法将函数定义在一行上：

```
$ function divem { echo -n $1 / $2 ; }
$ divem 100 5
20
$
```

当你在命令行上定义函数时，务必记住在每个命令末尾包含一个分号，以便 shell 知道在哪里分隔命令：

```
$ function doubleit { read -p "Enter value: " value; echo -n
$ $value * 2 ; }
$
$ doubleit
Enter value: 20
40
$
```

另一种方法是使用多行来定义函数。这样做时，Bash shell 会使用次要提示符请求更多命令。使用此方法，你不需要在每个命令末尾放置分号；只需按 Enter 键即可。

```
$ function multem {
> echo $[ $1 * $2 ]
>}
$ multem 2 5
10
$
```

当你在函数末尾使用大括号时，shell 知道你已完成函数定义。

> **警告**
>
> 在命令行上创建函数时要格外小心。如果你使用的函数与内置命令或其他命令同名，该函数将覆盖原始命令。

#### 在 .bashrc 文件中定义函数

直接在命令行上定义 shell 函数的明显缺点是，当你退出 shell 时，你的函数就会消失。对于复杂的功能，这可能会成为一个问题。一种更简单的方法是在一个每次启动新 shell 时都会被 shell 重新加载的地方定义函数。
