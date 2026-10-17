
```bash
local result=$(factorial $temp)

echo $( $result * $1 ))
```

```
fi

}
```

`read -p "Enter value: " value`

`result=$(factorial $value)`

`echo "The factorial of $value is: $result"`

```
$
./test13

Enter value: 5
```

5 的阶乘是：120
$

使用 `factorial` 函数非常简单。创建了这样一个函数后，你可能想在其他脚本中使用它。接下来，我们来看看如何高效地实现。

## 创建库

很容易看出函数如何在单个脚本中节省打字量，但如果你恰好在不同的脚本之间使用同一个代码块怎么办？如果你必须在每个脚本中定义相同的函数，却每个脚本中只使用一次，这显然是具有挑战性的。

这个问题有解决方案！bash shell 允许你为函数创建一个库文件，然后在任意需要的脚本中引用该单一库文件。

该过程的第一步是创建一个包含你在脚本中所需的函数的通用库文件。这里有一个名为 `myfuncs` 的简单库文件，它定义了三个简单函数：

```bash
$ cat myfuncs

# my script functions

function add {

  echo $[ $1 + $2 ]

}

function mult {

  echo $[ $1 * $2 ]

}

function div {

  if [ $2 -ne 0 ];

  then

    echo $[ $1 / $2 ]

  else

    echo -1

  fi

}
```

下一步是在想要使用任何一个函数的脚本文件中包含 `myfuncs` 库。这就是事情变得棘手的地方。

问题在于 shell 函数的作用域。作为环境变量，shell 函数仅在定义它们的 shell 会话中有效。如果你从命令行界面提示符运行 `myfuncs` shell 脚本，shell 会创建一个新的 shell 并在该新 shell 中运行脚本。这为该 shell 定义了函数，但当你尝试运行另一个使用这些函数的脚本时，它们是不可用的。

这同样适用于脚本。如果你尝试将库文件作为普通的脚本文件运行，函数将不会在你的脚本中：

```bash
$ cat badtest4

#!/bin/bash

# using a library file the wrong way

./myfuncs

result=$(add 10 15)

echo "The result is $result"

$
./badtest4: add: command not found

The result is
$
```

使用函数库的关键是 `source` 命令。`source` 命令在当前 shell 上下文中执行它们，而不是创建一个新的 shell 来执行它们。你使用 `source` 命令在你的 shell 脚本运行库文件。这使得函数对脚本可用。

`source` 命令有一个快捷别名，称为点操作符 `.`。要在 shell 脚本中 source `myfuncs` 库文件，你只需要添加以下行：

```bash
. ./myfuncs
```

此示例假设 `myfuncs` 库文件在同一目录下。

## 在命令行使用函数

本地函数变量提供的一个特性是自包含性。一个自包含的函数不使用函数之外的任何资源，除了脚本通过命令行传递给它的变量。

使得函数可以被递归调用，这意味着函数通过调用自己来获得答案。通常，递归函数有一个最终会迭代到的基准值。许多高级数学算法使用递归来反复将复杂的方程降低一个级别，直到达到基准值定义的级别。

递归算法的经典示例是计算阶乘。一个数的阶乘是该数与其之前数字的积。因此，要找到 5 的阶乘，你需要执行以下方程：

```
5! = 1 * 2 * 3 * 4 * 5 = 120
```

使用递归，方程被简化为以下格式：

```
x! = x * (x-1)!
```

或者用英语描述，x 的阶乘等于 x 乘以 x-1 的阶乘。这可以通过简单的递归脚本来实现：

```bash
function factorial {

  if [ $1 -eq 1 ]

  then

    echo 1

  else

    local temp=$(($1 - 1))

    local result=$(factorial $temp)

    echo $( $result * $1 ))

  fi

}
```

`factorial` 函数使用自己来计算阶乘的值：

```bash
$ cat test13

#!/bin/bash

# using recursion

function factorial {

  if [ $1 -eq 1 ]

  then

    echo 1

  else

    local temp=$(($1 - 1))

    local result=$(factorial $temp)

    echo $( $result * $1 ))

  fi

}

read -p "Enter value: " value

result=$(factorial $value)

echo "The factorial of $value is: $result"

$
./test13

Enter value: 5
```

5 的阶乘是：120
$

使用 `factorial` 函数非常简单。创建了这样一个函数后，你可能想在其他脚本中使用它。接下来，我们来看看如何高效地实现。

请确保包含正确的库路径，以便 bash shell 能够找到该库文件。下一次启动 shell 时，库中的所有函数都可以在命令行界面中可用：

```
$ addem 10 5
15
$ autem 10 5
50
$ divem 10 5
2
$
```

更好的是，shell 还会将任何定义的函数传递给子 shell 进程，因此你从当前 shell 会话运行的任何 shell 脚本都可以自动使用这些函数。你可以通过编写一个无需定义或加载（source）就使用这些函数的脚本来测试这一点：

```
$ cat test15
!/bin/bash

# 使用在 .bashrc 文件中定义的函数

value1=10
value2=5
result1=$(addem $value1 $value2)
result2=$(multem $value1 $value2)
result3=$(divem $value1 $value2)

echo "The result of adding them is: $result1"
echo "The result of multiplying them is: $result2"
echo "The result of dividing them is: $result3"

$
$ ./test15

The result of adding them is: 15
The result of multiplying them is: 50
The result of dividing them is: 2
$
```

即使没有加载库文件，这些函数在 shell 脚本中也能完美运行。

# 实例示例

使用函数的意义不仅仅是让你的函数运行起来。在开源世界，代码共享是关键，shell 函数也是如此。有许多不同的脚本函数可供你下载并并在你自己的应用程序中使用。

本节将介绍如何下载、安装和使用 GNU shtool shell 函数库。shtool 库提供了一些简单的脚本函数，用于执行日常 shell 操作，例如处理临时文件和文件夹或格式化输出显示。

## 下载与安装

该过程的第一是下载并安装 GNU shtool 库到你的系统中，以便你可以在自己的脚本中使用库函数。要实现这一点，你需要使用 FTP 客户端程序或图形化桌面中的浏览器。以下是下载 shtool 包的 URL：

```
ftp://getfp.gnu/gnu/shtool-2.0.8.tar
```

这会将 `shtool-2.0.8.tar.gz` 文件下载到文件夹中。从那里开始，你可以使用 Linux 发行版中的 `cp` 命令行工具或图形化文件管理器（如 Ubuntu 中的 Nautilus）将文件复制到你的家目录。

将文件复制到家目录后，你可以使用 `tar` 命令对其进行解压：
`tar -zxvf shtool-2.0.8.tar.gz`

这会将包文件解压到名为 `shtool-2.0.8` 的文件夹中。现在你准备好构建 shell 脚本库文件了。

## 构建库

shtool 分发包必须针对你特定的 Linux 环境进行配置。要做到这一点，你需要使用编程环境中常用的 `configure` 和 `make` 命令。要构建库文件，只需要运行两个命令：

```
$ ./configure
make
```
