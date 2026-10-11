
你可能需要将此脚本的输出重定向到 `more` 命令以便停止它。一切看起来运行正常，直到满足了 `if-then` 条件，shell 执行了 `continue` 命令。当 shell 执行 `continue` 命令时，它会跳过循环中的剩余命令。

你可以在 shell 脚本中组合循环，产生多层循环。`bash` shell 提供了 `continue` 和 `break` 命令，这些命令允许我们根据循环内部不同的值来改变正常循环过程的流程。

`bash` shell 还允许我们使用标准命令重定向和管道来改变循环的输出。你可以使用重定向将循环的输出重定向到文件，或者使用管道将循环的输出重定向到另一个命令。这提供了丰富的功能，让你通过这些功能控制你的 shell 脚本的执行。

下一章将讨论如何与 shell 脚本的用户进行交互。通常，shell 脚本并不是完全自包含的。它们通常需要某种类型的外部数据，这些数据必须在运行时提供。下一章将展示不同的方法，通过这些方法向你的 shell 脚本提供实时数据进行处理。

## 第 11 章

## 处理用户输入

到为止，你已经了解了如何编写与 Linux 系统上的数据、变量和文件交互的脚本。有时，你需要一个必须与运行脚本的人交互的脚本。`bash` shell 提供了几种不同的方法从人类获取数据，包括命令行参数（在命令后添加的数据值）、命令行选项（修改命令行为的单字母值）以及直接从键盘读取输入。本章将讨论如何将这些不同的方法整合到你的 `bash` shell 脚本中，从运行脚本的用户获取数据。

- 本章内容
- 使用命令行参数
- 确定你的选项
- 从用户获取输入

### 命令行参数

将数据传递给 shell 脚本的最基本方法是使用命令行参数。命令行参数允许你在执行脚本时向命令行添加数据值：

```bash
$ ./addem 10 30
```

这个示例向脚本 `addem` 传递了两个命令行参数（10 和 30）。脚本使用特殊变量处理这些命令行参数。接下来的部分描述了如何在 `bash` shell 脚本中使用命令行参数。

### 读取参数

`bash` shell 为命令行中输入的所有参数分配了名为“位置参数”（positional parameters）的特殊变量。这甚至包括 shell 执行的程序名称。位置参数变量是标准数字，其中 `$0` 是程序名称， `$1` 是第一个参数， `$2` 是第二个参数，以此此类推，直到 `$9` 是第九个参数。

这是一个在 shell 脚本中使用一个命令行参数的简单示例：

```bash
$ cat test1

#!/bin/bash

# 使用一个命令行参数

factorial=1

for (( number = 1; number <= $1; number++ ))
do
    factorial=$[$factorial * $number ]
done

echo The factorial of $1 is $factorial

$../test1

The factorial of 5 is 120

$
```

你可以像使用 shell 脚本中的任何其他变量一样使用 `$1` 变量。shell 脚本会自动将命令行参数的值赋值给变量，你不需要对它进行任何操作。

如果你需要输入更多的命令行参数，每个参数在命令行上必须用空格隔开：

```bash
$ cat test2

#!/bin/bash

# 测试两个命令行参数

total=$[1 * $2]

echo The first parameter is $1.
echo The second parameter is $2.
echo The total value is $total.

$../test2 2 5

The first parameter is 2.
The second parameter is 5.
The total value is 10.

$
```

shell 将每个参数分配给相应的变量。

在这个示例中，使用的命令行参数都是数值值。你也可以在命令行中使用字符串字符串：

```bash
$ cat test3

#!/bin/bash

# 测试字符串参数

echo Hello $1, glad to meet you.

$ ./test3 Rich

Hello Rich, glad to meet you.

$
```

shell 将输入到命令行的字符串值传递给脚本。然而，如果你尝试对包含空格的文本字符串执行此操作，你将会遇到问题：

```bash
$ ./test3 Rich Blum

Hello Rich, glad to meet you.

$
```

记住，每个参数都是由空格隔开的，因此 shell 将空格解释为仅是两个值的分隔符。要将包含空格的内容作为参数值，你必须使用引号（单引号或双引号均可）：

```bash
$ ./test3 'Rich Blum'

Hello Rich Blum, glad to meet you.

$ ./test3 "Rich Blum"

Hello Rich Blum, glad to meet you.
```

注意引号不是数据的一部分，它们界定了数据的开始和结束。

如果你的脚本需要超过九个命令行参数，你可以继续使用，但变量名会略有不同。在第九个变量之后，你必须在变量数字周围使用括号，例如 `$[10]`。这里有一个示例：

```bash
$ cat test4

#!/bin/bash

# 处理大量参数

total=$[10] * $[11]

echo the tenth parameter is $[10]
echo the eleventh parameter is $[11]
echo The total is $3total

$ ./test3 1 2 3 4 5 6 7 8 9 10 11 12

The tenth parameter is 10
The eleventh parameter is 11
The total is 110

$
```

这种技术允许你向脚本添加任何你可能需要的命令行参数。

### 读取程序名称

你可以使用 `$0` 参数来确定 shell 从命令行启动的程序名称。这可以很有用，特别是当你编写需要根据程序名执行函数的脚本时。然而，如果你直接这样做，可能会遇到问题。看看这个简单的示例：

```bash
$ cat test5

#!/bin/bash

# 使用 basename 获取程序名

echo The program is $0

$ ./test5

The program is ./test5

$ /home/rich/test5

The program is /home/rich/test5
```

`$0` 获取的是整个路径，而不是只有程序名。如果你只需要程序名，则需要使用 `basename` 命令来剥离路径：

```bash
$ cat test5

#!/bin/bash

# 使用 basename 获取程序名

name=`basename $0`

echo The program is $name

$ ./test5

The program is test5

$ /home/rich/test5

The program is test5
```

## 第二部分 Shell 脚本基础

```bash
$ ./test7 Rich

Hello Rich, glad to meet you.

$ ./test7

Sorry, you didn't identify yourself.

$
```

在例例中，我在 `test` 命令中使用了 `-n` 参数来检查命令行参数中是否存在数据。在下一节中，你将看到另一种检查命令行参数的方法。

## 特殊参数变量

`bash` shell 中提供了几个特殊的变量，用于跟踪命令行参数。本节将介绍它们这些什么，以及如何使用它们。

## 统计参数数量

正如你在上一节中看到的，在脚本中使用命令行参数之前对其进行验证通常是一个好主意。对于使用多个命令行参数的脚本，这可能会非常繁琐。

与其测试每个参数，你只需要统计在命令行上输入了多少个参数。`bash` shell 提供了一个特殊的变量专门为此目的。

特殊变量 `$#` 包含了脚本运行时所包含的命令行参数数量。你可以在脚本任何地方使用这个特殊变量，就像使用普通变量一样：

```bash
$ cat test8

#!/bin/bash

# 获取参数数量

echo There were $# parameters supplied.

./test8 0 parameters supplied.

./test8 1 2 3 4 5

There were 5 parameters supplied.

./test8 1 2 3 4 5 6 7 8 9 10

There were 10 parameters supplied.

./test8 "Rich Blum"

There were 1 parameters supplied.

$
```
