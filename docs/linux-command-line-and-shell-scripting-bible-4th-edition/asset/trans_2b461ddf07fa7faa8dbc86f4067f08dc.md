

## Shell 脚本编程：参数与特殊变量

在前面的示例中，使用的命令行参数都是数值。你也可以使用文本字符串作为参数：

```bash
$ cat stringparam.sh
#!/bin/bash
# 使用一个命令行字符串参数
#
echo 你好 $1，很高兴见到你。
exit
$
$ ./stringparam.sh world
你好 world，很高兴见到你。
$
```

Shell 会将命令行中输入的字符串值传递给脚本。但是，如果你尝试对包含空格的文本字符串执行此操作，就会遇到问题：

```bash
$ ./stringparam.sh big world
你好 big，很高兴见到你。
$
```

请记住，参数之间是以空格分隔的，因此 Shell 将空格解释为仅用于分隔两个值。要将空格作为参数值的一部分，你必须使用引号（单引号或双引号均可）：

```bash
$ ./stringparam.sh 'big world'
你好 big world，很高兴见到你。
$
$ ./stringparam.sh "big world"
你好 big world，很高兴见到你。
$
```

> **注意**
> 
> **在将文本字符串作为参数传递时使用的引号不属于数据的一部分。它们仅用于界定数据的开始和结束。**

如果你的脚本需要超过九个命令行参数，你可以继续添加，但变量名的写法会略有不同。在第九个变量之后，你必须在大括号中包裹变量编号，例如 `${10}`。以下是这样做的示例：

```bash
$ cat positional10.sh
#!/bin/bash
# 处理大量的命令行参数
#
product=$((${10} * ${11}))
echo 第十个参数是 ${10}。
echo 第十一个参数是 ${11}。
echo 乘积值是 $product。
exit
$
$ ./positional10.sh 1 2 3 4 5 6 7 8 9 10 11 12
第十个参数是 10。
第十一个参数是 11。
乘积值是 110。
```

这种技术允许你向脚本添加尽可能多的命令行参数，以满足你的需求。

### 读取脚本名称

你可以使用 `$0` 参数来确定 Shell 从命令行启动的脚本名称。如果你在编写具有多个功能或产生日志消息的工具时，这会非常有用。

```bash
$ cat positional0.sh
#!/bin/bash
# 处理 $0 命令行参数
#
echo 此脚本名称是 $0。
exit
$ bash positional0.sh
此脚本名称是 positional0.sh。
$
```

然而，这里存在一个潜在问题。当使用不同的命令运行 Shell 脚本时，该命令会与 `$0` 参数中的脚本名称混淆在一起：

```bash
$ ./positional0.sh
此脚本名称是 ./positional0.sh。
$
```

另一种情况是，当实际传递的字符串是完整的脚本路径，而不仅仅是脚本名称时。在这种情况下，`$0` 变量会被设置为完整的脚本路径和名称：

```bash
$ /home/christine/scripts/positional0.sh
此脚本名称是 /home/christine/scripts/positional0.sh。
$
```

如果你希望编写一个仅使用脚本名称的脚本，你需要做一些工作来去除用于运行脚本的路径或任何混入的命令。幸运的是，有一个方便的命令可以做到这一点。`basename` 命令返回不含路径的脚本名称：

```bash
$ cat posbasename.sh
#!/bin/bash
# 在 $0 命令行参数中使用 basename
# 
name=$(basename $0)
# 
echo 此脚本名称是 $name。
exit
$ ./posbasename.sh
此脚本名称是 posbasename.sh。
$
```

这样好多了。你可以使用这种技术来编写一个脚本，生成标识其运行时间的日志消息：

```bash
$ cat checksystem.sh
#!/bin/bash
# 在消息中使用 $0 命令行参数
scriptname=$(basename $0)
#
echo $scriptname 在 $(date) 运行 >> $HOME/scripttrack.log
exit
$
$ ./checksystem.sh
$ cat $HOME/scripttrack.log
checksystem.sh 在 Thu 04 Jun 2020 10:01:53 AM EDT 运行
$
```

拥有一个能自我识别的脚本对于追踪脚本问题、审计系统以及生成日志消息非常有用。

### 测试参数

在 Shell 脚本中使用命令行参数时要小心。如果脚本在没有所需参数的情况下运行，可能会发生不良后果：

```bash
$ ./positional1.sh
./positional1.sh: line 5: ((: number <= : 语法错误：
期望操作数（错误标记为 "<= "）
 的阶乘是 1
$
```

当脚本假设参数变量中有数据，但实际上没有数据时，你很可能会收到脚本发出的错误消息。这是一种糟糕的脚本编写方式。在使用参数之前，务必始终检查它们，以确保数据存在：

```bash
$ cat checkpositional1.sh
#!/bin/bash
# 使用一个命令行参数
#
if [ -n "$1" ]
then
    factorial=1
    for (( number = 1; number <= $1; number++ ))
    do
        factorial=$(($factorial * $number))
    done
    echo $1 的阶乘是 $factorial
else
        echo "你没有提供参数。"
fi
exit
$ ./checkpositional1.sh
你没有提供参数。
$ ./checkpositional1.sh 3
3 的阶乘是 6
$
```

在这个示例中，使用 `-n` 测试评估来检查 `$1` 命令行参数中是否有数据。在下一节中，你将学习另一种检查命令行参数的方法。

### 使用特殊参数变量

有几个特殊的 Bash Shell 变量用于跟踪命令行参数。本节将描述它们是什么以及如何使用它们。

#### 统计参数数量

正如你在上一节所见，在脚本中使用命令行参数之前，你应该验证这些参数。对于使用多个命令行参数的脚本，这种检查可能会变得繁琐。

与其测试每个参数，你可以统计在命令行中输入了多少个参数。Bash Shell 为此提供了一个特殊变量。

`$#` 变量包含运行脚本时包含的命令行参数数量。你可以像普通变量一样在脚本的任何地方使用这个特殊变量：

```bash
$ cat countparameters.sh
#!/bin/bash
# 统计命令行参数
#
if [ $# -eq 1 ]
then
    fragment="个参数被"
else
    fragment="个参数被"
fi
echo $# $fragment 提供。
exit
$ ./countparameters.sh
0 个参数被提供。
$ ./countparameters.sh Hello
1 个参数被提供。
$ ./countparameters.sh Hello World
2 个参数被提供。
$ ./countparameters.sh "Hello World"
1 个参数被提供。
$
```

现在你具备了在尝试使用参数之前测试存在参数数量的能力：

```bash
$ cat addem.sh
#!/bin/bash
# 添加命令行参数
#
if [ $# -ne 2 ]
then
    echo 用法: $(basename $0) 参数1 参数2
else
    total=$[ $1 + $2 ]
    echo $1 + $2 是 $total
fi
exit
$
$ ./addem.sh
用法: addem.sh 参数1 参数2
$ ./addem.sh 17
用法: addem.sh 参数1 参数2
$ ./addem.sh 17 25
17 + 25 是 42
$
```

`if-then` 语句使用 `-ne` 评估对提供的命令行参数进行数值测试。如果没有正确数量的参数，将显示一条错误消息，展示脚本的正确用法。

该变量还提供了一种很酷的方式来获取命令行中的最后一个参数，而无需知道使用了多少个参数。但是，你需要使用一个小技巧来达到目的。

仔细想想，你可能会认为，由于 `$#` 变量包含参数数量的值，因此使用变量 `${$#}` 将代表最后一个命令行参数变量。尝试一下看看会发生什么：

```bash
$ cat badlastparamtest.sh
#!/bin/bash
# 测试获取最后一个参数
#
echo 参数数量是 $#
echo 最后一个参数是 ${$#}
exit
$ ./badlastparamtest.sh one two three four
参数数量是 4
最后一个参数是 2648
$
```

显然，出问题了。事实证明，你不能在大括号内使用美元符号。相反，你必须用感叹号替换美元符号。这有点奇怪，但它是有效的：

```bash
$ cat goodlastparamtest.sh
#!/bin/bash
# 测试获取最后一个参数
#
echo 参数数量是 $#
echo 最后一个参数是 ${!#}
exit
$ ./goodlastparamtest.sh one two three four
参数数量是 4
最后一个参数是 four
$ ./goodlastparamtest.sh
参数数量是 0
最后一个参数是 ./goodlastparamtest.sh
$
```

完美。需要注意的是，当命令行中没有参数时，`$#` 的值为 0，但 `${!#}` 的值是用于运行脚本的命令。

