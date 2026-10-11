
Another new feature is that you can run the option letter and the parameter value together without a space:

```bash
$ ./test19 -abtest1

Found the -a option

Found the -b option, with value test1

$
```

The `getopts` command correctly parsed `test1` value from the `-b` option. Yet another feature of the `getopts` command is that it bundles any undefined option that it finds in the command line into a single output, the question mark:

```bash
$ ./test19 -d

Unknown option: ?

$ ./test19 -acde

Found the -a option

Found the -c option

Unknown option: ?

Unknown option: ?

$
```

Any option letter not defined in the `optstring` value is sent to your code as a question mark.

The `getopts` command knows when to stop processing options, and leave the parameters for you to process. As `getopts` processes each option, it increments the `OPTIND` environment variable by one. When you've reached the end of the `getopts` processing, you can just use the `OPTIND` with the `shift` command to move to the parameters:

```bash
$ cat test20

#!/bin/bash

# simple demonstration of the getopts command

while getopts :abc opt; do

  case "$opt" in

    a) echo "Found the -a option"

    b) echo "Found the -b option, with value $OPTARG"

    c) echo "Found the -c option"

    *) echo "Unknown option: $opt"

  esac

done

shift

for param in "$@"

do

  echo "Parameter #$count: $param"

  count=$[ count + 1 ]

done

$ ./test19 -ab test1 -c

Found the -a option

Found the -b option, with value test1

Found the -c option

Parameter #1: 'test2'

Parameter #2: 'test3'

Parameter #3: 'test4'

$
```

Now things are looking pretty fancy. However, there's still one small bug that lurks in the `getopt` command. Check out output:

```bash
./test18 -a -b test1 -cd "test2 test3" test4

Found the -a option

Found the -b option, with parameter value 'test1'

Found the -c option

Parameter #1: 'test2'

Parameter #2: 'test3'

Parameter #3: 'test4'

$
```

The `getopt` command isn't good at dealing with parameter values with spaces. It interpreted the space as the parameter separator, instead of following the double quotation and combining the two values into one parameter. Fortunately for us, there's yet another solution that solves this problem.

## 处理用户输入

```bash
shift

done

count=1

for param in "$@"

do

  echo "Parameter #$count: $param"

  count=$[ count + 1 ]

done

$
```

你会注意到这个脚本基本上和 `test17` 中的脚本相同。唯一的变化是添加了 `getopt` 命令，以帮助格式化我们的命令行参数。

现在，当你带有复杂的选项运行脚本时，运行情况会好得多：

```bash
./test18 -ac

Found the -a option

Found the -c option

$
```

当然，所有原始功能也都能正常工作：

```bash
./test18 -a -b test1 -cd test2 test3 test4

Found the -a option

Found the -b option, with parameter value 'test1'

Found the -c option

Parameter #1: 'test2'

Parameter #2: 'test3'

Parameter #3: 'test4'

$
```

现在看起来相当高级了。然而，`getopt` 命令中仍然潜伏着一个小的 Bug。查看输出：

```bash
./test18 -a -b test1 -cd "test2 test3" test4

Found the -a option

Found the -b option, with parameter value 'test1'

Found the -c option

Parameter #1: 'test2'

Parameter #2: 'test3'

Parameter #3: 'test4'

$
```

`getopt` 命令并不擅长处理带有空格的参数值。它将空格解释为参数分隔符，而不是遵循双引号并将两个值合并为一个参数。幸运的是，我们还有另一种可以解决这个问题的方案。

## 301

## 第二部分 Shell 脚本基础

### 更高级的 getopts

`getopts` 命令（注意它是复数形式）是 `bash` shell 内置的。它看起来和它的表兄弟相似，但具有一些扩展功能。

与 `getopt` 不同（后者为命令行中找到的所有已过的选项和参数产生一个输出），`getopts` 命令是按顺序对现有的 shell 参数变量进行操作。

它在每次被调用时逐个处理在命令行中检测到的参数。当用完参数后，它会以大于零的退出状态退出。这使其非常适合在循环中使用，以解析命令行上的所有参数。

`getopts` 命令的格式为：

```bash
getopts string variable
```

`optstring` 的值与 `getopt` 命令中使用的类似。`optstring` 中有效的选项列表，如果该选项需要参数值，则加上一个冒号。要抑制错误消息，请以冒号开头 `optstring`。`getopts` 命令将当前参数存放在命令行中定义的变量中。

`getopts` 命令使用了两个环境变量。`OPTARG` 环境变量包含如果选项需要参数值时将使用的值。`OPTIND` 环境变量包含 `getopts` 停止处理时在参数列表中的当前位置值。这使你能够在处理完选项后继续处理其他命令行参数。

让我们来看一个使用 `getopts` 命令的简单示例：

```bash
$ cat test19

#!/bin/bash

# simple demonstration of the getopts command

while getopts :abc opt; do

  case "$opt" in

    a) echo "Found the -a option"

    b) echo "Found the -b option, with value $OPTARG"
