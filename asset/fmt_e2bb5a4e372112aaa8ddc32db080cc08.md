
现在你就有了在尝试使用参数之前测试其存在参数数量的能力：

```
$ cat test9

#!//bin/bash

# 测试参数

if [ $# -ne 2 ]

then

    echo Usage: test9 a b

else

    total=$(( $1 + $2 ))

    echo The total is $total

fi

$ test9

Usage: test9 a b

$ ./test9 10

Usage: test9 a b

$ ./test9 10 15

The total is 25.

$ ./test9 10 20

Usage: test9 a b

$
```

`if-then` 语句使用 `test` 命令对命令行上提供的参数数量进行数值测试。如果提供的参数数量不正确，你可以打印一条错误信息，显示脚本的正确用法。

该变量还提供了一种酷炫的方法来获取命令行上的最后一个参数，而无需知道使用了多少个参数。然而，你需要使用一个小技巧才能达到目的。

如果你仔细思考一下这个问题，你可能会认为既然 `$#` 变量包含了参数数量的值，那么使用变量 `$($#)` 就会代表最后一个命令行变量。尝试一下看看会发生什么：

```
$ cat badtest1

!/bin/bash

# 测试获取最后一个参数

echo The last parameter was ${#)

$ ./badtest1 10

The last parameter was 15354

$
```

## 第二部分 Shell 脚本基础

哇，这里发生了什么？显然发生了某些错误。事实证明，你不能在大括号中使用美元符号。相反，你必须将美元符号替换为感叹号。或者，这样做行得通：

```
$ test10

#!/bin/bash

# 获取最后一个参数

params=$#

echo The last parameter is $params

echo The last parameter is ${!#}

./test10 1 2 3 4 5

The last parameter is 5

The last parameter is 5

./test10

The last parameter is 0

The last parameter is ./test10

$
```

完美。这个测试还将 `$#` 的值赋值给变量 `params`，然后又在特殊的命令行变量格式中使用了该变量。两个版本都有效。同样重要的是注意到，当命令行上没有任何参数时，`$#` 的值为零，这显示在 `params` 变量中，但 `${!#}` 返回的是用于命令的脚本名称。

### 获取所有数据

在某些情况下，你想要获取命令行上提供的所有参数并对它们都进行迭代。与其费力使用 `$#` 变量来确定命令行上有多少个参数并遍历它们，你可以使用两个特殊变量。

`"*"` 和 `"$@"` 变量为你所有的参数提供了一个一站式的解决方案。这两个都将所有的命令行参数包含在一个单一变量中。

`"*"` 变量将命令行上提供的所有参数视为单个单词。该单词包含了命令行上出现的每个值。基本上，`"*"` 不再将参数视为多个对象，而是将它们全部视为一个参数。

另一方面，`"$@"` 变量将命令行上提供的所有参数视为同一字符串中的独立单词。它允许你遍历这些值，分离出提供的每个参数。这通过使用 `for` 命令最容易实现。

关于这两个变量如何运作，很容易产生困惑。如果你从字面上看它们，你甚至看不出区别：

```
$ cat test11

#!/bin/bash

# 测试 "*" 和 "$@"

echo "Using the \* method: $*"

echo "Using the \"@\" method: $@"

$ ./test11 rich barbara katie jessica

Using the "*" method: rich barbara katie jessica

Using the "$@" method: rich barbara katie jessica

$
```

注意，在表面上，这两个变量产生了相同的输出，一次性显示所有的命令行参数。现在这里有另一个例子展示了差异所在：

```
$ cat test12

#!/bin/bash

# 测试 "*" 和 "$@"

count=1

for param in "$*"

do

  echo "* Parameter #$count = $param"

  count=$((count + 1))

done

count=1

for param in "$@"

do

  echo "@" Parameter #$count = $param"

  count=$((count + 1))

done

$ ./test11 rich barbara katie jessica

"* Parameter #1 = rich barbara katie jessica

"$@" Parameter #1 = rich

"$@" Parameter #2 = barbara

"$@" Parameter #3 = katie

$
```

现在我们有了进展。通过使用 `for` 命令遍历特殊变量，我们可以看到它们的不同。`"*"` 将所有参数视为字符串，而 `"$@"` 则逐个处理。

### 使用 shift

`shift` 命令是 bash shell 中一个强大的工具。它将位置参数左移，允许你一个一个处理它们。

当你使用 `shift` 时，第一个参数会被移除，第二个变成第一个，以此此类推。这对于处理脚本中的选项和参数特别有用。

在之前的 `test13` 脚本中，你看到了如何使用 `shift` 命令遍历命令行参数。你可以使用相同的技术来处理命令行选项。

当你提取每个独立参数时，使用 `case` 语句来判断参数是否为选项格式：

```
$ cat test13

#!/bin/bash

# 展示 shift

count=1

while [ -n "$1" ]

do

  echo "Parameter #$count = $1"

  count=$((count + 1))

  shift

done

$ ./test13 rich barbara katie jica

Parameter #1 = rich

Parameter #2 = barbara

Parameter #3 = katie

Parameter #4 = jica
```

通过在 `shift` 命令中使用值，你可以轻松跳过不需要的参数。

### 处理选项

如果你一直在跟着这本书学习，你会看到提供了参数和选项的 bash 命令。选项是以横杠开头的单个字母，用于改变命令的行为。本节展示了在脚本处理选项的三种不同方法。

#### 寻找你的选项

表面上看，命令行选项并没有什么特别。它们紧随脚本名称之后，与命令行参数相同。实际上，如果你愿意，你可以以处理命令行参数的方式来处理命令行选项。

#### 处理简单选项

在之前的 `test13` 脚本中，你看到了如何使用 `shift` 命令遍历脚本提供的命令行参数。你可以使用相同的技术来处理命令行选项。

```
$ cat test15

#!//bin/bash

# 将命令行选项作为参数提取

while [ -n "$1" ]

do

  case "$1" in

    -a) echo "Found the -a option" ::;

    -b) echo "Found the -b option" ::;

    -c) echo "Found the -c option" ::;

    *) echo "$1 is not an option"

  esac

  shift

done

$ ./test15 -a -b -c -d

Found the -a option

Found the -b option

Found the -c option

-d is not an option
```

`case` 语句检查每个参数的有效选项。当找到匹配项时，会在 `case` 语句中执行相应的命令。

无论选项在命令行中的出现顺序如何，这种方法都有效：

```
$ ./test15 -d c -a

-d is not an option

Found the -c option

Found the -a option
$
