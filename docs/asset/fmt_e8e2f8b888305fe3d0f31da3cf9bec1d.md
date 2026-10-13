
```sh
if command₁
then
        command
        command
        ...
else
    if command₂
    then
        command
        command
        ...
    else
        ...
        if commandₙ
        then
            command
            command
            ...
        else
            command
            command
            ...
        fi
        ...
    fi
fi
```

当你需要做出不仅仅是二选一的决定时，这种命令序列会很有用。在这种情况下，会进行多路决策；如果前面的条件都不满足，则执行最后一个 `else` 子句。

作为一个相对简单的例子，让我们编写一个名为 `greetings` 的程序，它会根据一天中的时间打印友好的 Good morning、Good afternoon 或 Good evening。为了举例方便，我们假定从午夜到正午为上午，正午到下午 6 点为下午，下午 6 点到午夜为晚上。

要编写这个程序，你必须先获取当前时间。`date` 命令完全可以满足这一目的。再看一下这个命令的输出：

```text
$ date
Wed Aug 29 10:42:01 EDT 2002
$
```

`date` 命令的输出格式是固定的，你可以利用这一点，因为时间总会出现在字符位置 12 到 19 上。实际上，你只需要位置 12 和 13 上的小时值：

```text
$ date | cut -c12-13
10
$
```

现在编写 `greetings` 程序的任务就很简单了：

```text
$ cat greetings
#
# Program to print a greeting
#

hour=$(date | cut -c12-13)

if [ "$hour" -ge 0 -a "$hour" -le 11 ]
then
        echo "Good morning"
else
        if [ "$hour" -ge 12 -a "$hour" -le 17 ]
        then
                echo "Good afternoon"
        else
                echo "Good evening"
        fi
fi
$
```

如果小时大于或等于 0（午夜）且小于或等于 11（直到 11:59:59），则显示 Good morning。如果小时大于或等于 12（正午）且小于或等于 17（直到下午 5:59:59），则显示 Good afternoon。如果前面的条件都不满足，则显示 Good evening。

```text
$ greetings
Good morning
$
```

然而，再看一下这个程序，你会意识到 `greetings` 中使用的嵌套 `if` 命令序列相当笨拙。为了精简这类 *if-then-else* 序列，shell 还支持一种特殊的 `elif` 元素，它的行为有点像 *else if 条件*，但不会增加你的嵌套层级。一般格式为

```sh
if command₁
then
        command
        command
        ...
elif command₂
then
        command
        command
        ...
else
        command
        command
        ...
fi
```

`command₁`、`command₂`、……、`commandₙ` 依次执行并测试它们的退出状态。一旦其中一个返回 TRUE（零）的退出状态，就会执行紧随其后的 `then` 之后列出的命令，直到遇到另一个 `elif`、`else` 或 `fi`。如果所有条件表达式都不为真，则执行可选的 `else` 之后列出的命令。

现在你可以使用这种新格式重写 `greetings` 程序，如下所示：

```text
$ cat greetings
#
# Program to print a greeting -- version 2
#

hour=$(date | cut -c12-13)

if [ "$hour" -ge 0 -a "$hour" -le 11 ]
then
        echo "Good morning"
elif [ "$hour" -ge 12 -a "$hour" -le 17 ]
then
        echo "Good afternoon"
else
        echo "Good evening"
fi
$
```

这确实是一个改进。程序更易读了，而且不会因为缩进不断加深而向右边缘偏移。

顺便说一句，很少会看到 `date | cut` 这样的管道，因为 `date` 命令本身有一套丰富而复杂的输出格式，你可以利用它们只获取所需的信息或值。例如，要以 0–23 的格式仅输出当前小时，可以使用 `%H`，并加上必要的 `+` 前缀以表明这是一个格式字符串：

```text
$ date +%H
10
$
```

作为练习，你应该修改 `greetings` 程序，使用这种更简洁的方式来获取当前小时。

## `rem` 的另一个版本

让我们回到电话号码删除程序 `rem`。之前我们提到过它很危险，因为如果不检查其操作的正确性，它可能会盲目删除超出用户预期数量的条目。

解决这个问题的一种方法是：在删除之前检查与用户指定模式匹配的条目*数量*。如果匹配项不止一个，则发出相应的消息并终止程序的执行。但是，如何确定匹配条目的数量呢？

一种简单的方法是对 `phonebook` 文件执行 `grep`，然后用 `wc` 统计匹配结果的数量。如果匹配数量大于 1，就可以发出相应的提示信息。该逻辑可以编写如下：

```sh
$ cat rem
#
# Remove someone from the phone book -- version 3
#

if [ "$#" -ne 1 ]
then
        echo "Incorrect number of arguments."
        echo "Usage: rem name"
        exit 1

fi

name=$1

#
# Find number of matching entries
#

matches=$(grep "$name" phonebook | wc -l)

#
# If more than one match, issue message, else remove it
#

if [ "$matches" -gt 1 ]
then
        echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
        grep -v "$name" phonebook > /tmp/phonebook
        mv /tmp/phonebook phonebook

else
        echo "I couldn't find $name in the phone book"
fi
$ 
```

为了提高可读性，在检查参数数量之后，将位置参数 `$1` 赋值给变量 `name`。

将命令序列的输出赋值给变量在 shell 程序中非常常见，如下面这行所示：

```sh
matches=$(grep "$name" phonebook | wc -l)
```

计算出匹配数量后，就可以很容易地沿 `if...elif...else` 命令序列逐步执行，它会首先测试匹配数量是否大于 1。如果是，则打印“more than one match”（匹配多于一个）的消息。如果不是，则测试匹配数量是否等于 1。如果是，则从电话簿中删除该条目。如果既不是 1 也不是大于 1，那么匹配数量必定为零，此时会显示一条消息提醒用户这一情况。

请注意，`grep` 命令在此程序中使用了两次：第一次用于确定匹配数量，第二次使用 `-v` 选项，在确保只有一行匹配后删除匹配的条目。

以下是 `rem` 这个版本的一些示例运行：

```text
$ rem
Incorrect number of arguments.
Usage: rem name
$ rem Susan
More than one match; please qualify further
$ rem 'Susan Topple'
$ rem 'Susan Topple'
I couldn't find Susan Topple in the phone book    She's history
$
```
