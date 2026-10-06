
## Handling User Input

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

You'll notice this is basically the same script as in test17. The only thing that changed is the addition of the getopt command to help format our command line parameters.

Now when you run the script with complex options, things work much better:

```bash
./test18 -ac
Found the -a option
Found the -c option
$
```

And of course, all of the original features work just fine as well:

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

Now things are looking pretty fancy. However, there's still one small bug that lurks in the getopt command. Check out output:

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

The getopt command isn't good at dealing with parameter values with spaces. It interpreted the space as the parameter separator, instead of following the double quotation and combining the two values into one parameter. Fortunately for us, there's yet another solution that solves this problem.

## 301

## Part II Shell Scripting Basics

## The more advanced getopts

The getopts command (notice that it's plural) is built into the bash shell. It looks a lot like its cousin, but has some expanded features.

Unlike getopt, which produces one output for all of the processed options and parameters found in the command line, the getopts command works on the existing shell parameter variables sequentially.

It processes the parameters it detects in the command line one at a time it is called. When it runs out of parameters, it exits with an exit status greater than zero. This makes it great for using in loops to parse all of the parameters on the command line.

The format of the getopts command is:

```bash
getopts string variable
```

The optstring value is similar to the one used in the getopt command. Valid list options in the optstring, along with a colon if the option requires a parameter value. To suppress error messages, start the optstring with a colon. The getopt command places the current parameter in the variable defined in the command line.

There are two environment variables that the getopts command uses. The OPTARG environment variable contains the value to be used if an option requires a parameter value. The OPTIND environment variable contains the value of the current location within the parameter list where getopts left off. This allows you to continue processing other command line parameters after finishing the options.

Let's take a look at a simple example that uses the getopts command:

```bash
$ cat test19
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
$ ./test19 -ab test1 -c
Found the -a option
Found the -b option, with value test1
Found the -c option
$
```

 while statement defines the getopts command, specifying what command line options to look for, along with the variable name to store them in for each iteration.

You'll notice something different about the case statement in this example. When the getopts parses the command line options, it strips off the leading dash, so you don't need them in the case definitions.

There are several new features in the getopts command. For starters, you can now include spaces in your parameter values:

```bash
$ ./test19 -b "test1 test2" -a
Found the -b option, with value test1 test2
Found the -a option
$
```

Another new feature is that you can run the option letter and the parameter value together without a space:

```bash
$ ./test19 -abtest1
Found the -a option
Found the -b option, with value test1
$
```

The getopts command correctly parsed test1 value from the -b option. Yet another feature of the getopts command is that it bundles any undefined option that it finds in the command line into a single output, the question mark:

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

Any option letter not defined in the optstring value is sent to your code as a question mark.

The getopts command knows when to stop processing options, and leave the parameters for you to process. As getopts processes each option, it increments the OPTIND environment variable by one. When you've reached the end of the getopts processing, you can just use the OPTIND with the shift command to move to the parameters:

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

Now things are looking pretty fancy. However, there's still one small bug that lurks in the getopt command. Check out output:

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

The getopt command isn't good at dealing with parameter values with spaces. It interpreted the space as the parameter separator, instead of following the double quotation and combining the two values into one parameter. Fortunately for us, there's yet another solution that solves this problem.
[/content]

译文：

[content]
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

你会注意到这个脚本基本上和 test17 中的脚本相同。唯一的变化是添加了 `getopt` 命令，以帮助格式化我们的命令行参数。

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

## 更高级的 getopts

`getopts` 命令（注意它是复数形式）是 bash shell 内置的。它看起来和它的表兄弟相似，但具有一些扩展功能。

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
    c) echo "Found the -c option"
    *) echo "Unknown option: $opt"
  esac
done
$ ./test19 -ab test1 -c
Found the -a option
Found the -b option, with value test1
Found the -c option
$
```

`while` 语句定义了 `getopts` 命令，指定了要查找的命令行选项，以及每次迭代中用于存储它们的变量名。

你会注意到这个示例中 `case` 语句的某些不同之处。当 `getopts` 解析命令行选项时，它会剥离开头的横杠，因此你不需要在 `case` 定义中包含它们。

`getopts` 命令有几个新功能。首先，你现在可以在参数值中包含空格了：

```bash
$ ./test19 -b "test1 test2" -a
Found the -b option, with value test1 test2
Found the -a option
$
```

另一个新功能是你可以一起运行选项字母和参数值而无需留空格：

```bash
$ ./test19 -abtest1
Found the -a option
Found the -b option, with value test1
$
```

`getopts` 命令正确解析了 `-b` 选项的 `test1` 值。`getopts` 命令的另一个功能是它会将命令行中找到任何未定义选项合并到一个输出中，即问号：

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

任何在 `optstring` 值未定义的选项字母都会以问号的形式发送给你的代码。

`getopts` 命令知道何时停止处理选项，并将参数留给你进行处理。当 `getopts` 处理每个选项时，它会将 `OPTIND` 环境变量加 1。当你完成 `getopts` 处理后，你可以直接使用 `OPTIND` 配合 `shift` 命令移动到参数：

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
