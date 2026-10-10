

```bash
for param in "$@"
do
    echo "Parameter #$count: $param"
    count=$[ $count + 1 ]
done
exit
$
```

你会发现，这基本上与 `extractoptionsopt.sh` 中的脚本相同。唯一的区别是添加了 `getopt` 命令，以帮助格式化命令行参数。

现在，当你使用复杂选项运行脚本时，效果会好得多：

```bash
$ ./extractwithgetopt.sh -ac

Found the -a option
Found the -c option
$
```

当然，所有原始功能也都运行正常：

```bash
$ ./extractwithgetopt.sh -c -d -b BValue -a test1 test2

Found the -c option
-d is not an option
Found the -b option with parameter value 'BValue'
Found the -a option

Parameter #1: 'test1'
Parameter #2: 'test2'
$
```

现在情况看起来相当出色。然而，`getopt` 命令中仍潜伏着一个小小的 bug。看看这个示例：

```bash
$ ./extractwithgetopt.sh -c -d -b BValue -a "test1 test2" test3

Found the -c option
-d is not an option
Found the -b option with parameter value 'BValue'
Found the -a option

Parameter #1: 'test1
Parameter #2: test2'
Parameter #3: 'test3'
$
```

`getopt` 命令在处理包含空格和引号的参数值方面表现不佳。它将该空格解释为参数分隔符，而不是遵循双引号将两个值合并为一个参数。幸运的是，这个问题有另一种解决方案。

### 进阶使用 getopts

`getopts` 命令（注意它是复数形式）内置于 Bash shell 中。它看起来很像它的 `getopt` 亲戚，但具有一些扩展功能。

与 `getopt` 不同，`getopt` 会针对在命令行中发现的所有已处理选项和参数产生一个输出，而 `getopts` 命令则按顺序处理现有的 shell 参数变量。

它每次被调用时，逐条处理其在命令行中检测到的参数。当它用完所有参数时，会以大于 0 的退出状态退出。这使得它非常适合在循环中使用，以解析命令行上的所有参数。

以下是 `getopts` 命令的格式：

```bash
getopts optstring variable
```

`optstring` 值类似于在 `getopt` 命令中使用的那个。有效的选项字母列在 `optstring` 中，如果选项字母需要参数值，则附带一个冒号。要抑制错误消息，请在 `optstring` 开头添加一个冒号。`getopts` 命令将当前参数放置在命令行中定义的 `variable` 中。

`getopts` 命令使用两个环境变量。如果选项需要参数值，`OPTARG` 环境变量将包含该值。`OPTIND` 环境变量包含 `getopts` 在参数列表中停止的位置的当前值。这允许你在完成选项处理后继续处理其他命令行参数。

让我们来看一个使用 `getopts` 命令的简单示例：

```bash
$ cat extractwithgetopts.sh
#!/bin/bash
# Extract command-line options and values with getopts
#
echo
while getopts :ab:c opt
do
  case "$opt" in
    a) echo "Found the -a option" ;;
    b) echo "Found the -b option with parameter value $OPTARG";;
    c) echo "Found the -c option" ;;
    *) echo "Unknown option: $opt" ;;
  esac
done
exit
$
```

```bash
$ ./extractwithgetopts.sh -ab BValue -c

Found the -a option
Found the -b option with parameter value BValue
Found the -c option
$
```

### 第二部分：Shell 脚本基础

`while` 语句定义了 `getopts` 命令，指定了要查找哪些命令行选项，以及用于在每次迭代中存储它们的变量名（`opt`）。

你会发现这个示例中的 `case` 语句有所不同。当 `getopts` 命令解析命令行选项时，它会去掉前导的破折号，因此在 `case` 定义中你不需要前导破折号。

`getopts` 命令提供了几个不错的功能。首先，你可以在参数值中包含空格：

```bash
$ ./extractwithgetopts.sh -b "BValue1 BValue2" -a

Found the -b option with parameter value BValue1 BValue2
Found the -a option
$
```

另一个不错的功能是你可以将选项字母和参数值连在一起运行，中间不需要空格：

```bash
$ ./extractwithgetopts.sh -abBValue

Found the -a option
Found the -b option with parameter value BValue
$
```

`getopts` 命令正确解析了 `-b` 选项中的 `BValue` 值。此外，`getopts` 命令将它在命令行中发现的任何未定义选项打包成一个输出，即问号：

```bash
$ ./extractwithgetopts.sh -d

Unknown option: ?
$
```

```bash
$ ./extractwithgetopts.sh -ade

Found the -a option
Unknown option: ?
Unknown option: ?
$
```

任何未在 `optstring` 值中定义的选项字母都会以问号的形式发送到你的代码中。

`getopts` 命令知道何时停止处理选项并将参数留给你处理。当 `getopts` 处理每个选项时，它将 `OPTIND` 环境变量的值加 1。当你到达 `getopts` 处理的末尾时，你可以使用 `OPTIND` 值配合 `shift` 命令移动到参数部分：

```bash
$ cat extractoptsparamswithgetopts.sh
#!/bin/bash
# Extract command-line options and parameters with getopts
#
```

### 第 14 章：处理用户输入

```bash
echo
while getopts :ab:cd opt
do
case "$opt" in
a) echo "Found the -a option" ;;
b) echo "Found the -b option with parameter value $OPTARG";;
c) echo "Found the -c option" ;;
d) echo "Found the -d option" ;;
*) echo "Unknown option: $opt" ;;
esac
done
# shift ${ OPTIND - 1 }
# echo
count=1
for param in "$@"
do
echo "Parameter $count: $param"
count=$[ $count + 1 ]
done
exit
```

```bash
$ ./extractoptsparamswithgetopts.sh -db Bvalue test1 test2
Found the -d option
Found the -b option with parameter value Bvalue
Parameter 1: test1
Parameter 2: test2
$
```

现在，你拥有了一个功能齐全的命令行选项和参数处理工具，可以在所有 shell 脚本中使用！

### 标准化选项

当你创建 shell 脚本时，显然你掌控着发生的事情。选择使用哪些字母选项以及如何选用，完全取决于你。

然而，在 Linux 领域，几个字母选项已经获得了一定的标准含义。如果你在 shell 脚本中利用这些选项，你的脚本将更具用户友好性。

表 14.1 展示了一些在 Linux 中用于命令行选项的常见含义。

你很可能仅凭阅读本书中各种 bash 命令的经验就能认出大多数这些选项的含义。为你的选项使用相同的含义，可以帮助用户在无需费心确定何时使用哪个选项的情况下与你的脚本进行交互。

#### 表 14.1 常见的 Linux 命令行选项

| 选项 | 描述 |
| :--- | :--- |
| a | 显示所有对象 |
| c | 生成计数 |
| d | 指定目录 |
| e | 展开对象 |
| f | 指定读取数据的文件 |
| h | 显示命令的帮助消息 |
| i | 忽略文本大小写 |
| l | 生成输出的长格式版本 |
| n | 使用非交互（批处理）模式 |
| o | 指定重定向所有输出的文件 |
| q | 运行在静默模式 |
| r | 递归处理目录和文件 |
| s | 运行在无声模式 |
| v | 生成详细输出 |
| x | 排除对象 |
| y | 对所有问题回答是 |

### 获取用户输入

虽然提供命令行选项和参数是从脚本用户处获取数据的好方法，但有时你的脚本需要更具交互性。你可能需要在脚本运行时提出问题，并等待运行你的脚本的人回应。Bash shell 为此目的提供了 `read` 命令。

### 读取基础

`read` 命令接受来自标准输入（例如键盘）或另一个文件描述符的输入。在接收到输入后，`read` 命令将数据放入变量中。以下是 `read` 命令最简洁的形式：

```bash
$ cat askname.sh
#!/bin/bash
# Using the read command
#
echo -n "Enter your name: "
read name
echo "Hello $name, welcome to my script."
exit
$
```

