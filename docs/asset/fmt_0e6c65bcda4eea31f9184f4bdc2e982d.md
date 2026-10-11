
$ ./extractwithgets.sh -ade

Found the -a option

Unknown option: ?

Unknown option: ?

$
```
任何在 `optstring` 中定义的选项字母都会以问号的形式发送给你的代码。
```
`getopts` 命令知道何时停止处理选项并将参数留给你处理。当 `getopts` 处理每个选项时，它会将 `OPTIND` 变量加 1。当你完成 `getopts` 处理后，你可以使用 `OPTIND` 值配合 `shift` 命令移动到参数：
```
$ extractwithoptparamswithgetopts.sh
!/bin/bash
# 使用 getopts 提取命令行选项和参数
#
echo
```
（续）

# 第二部分：Shell 脚本基础

（续）
```
while getopts :ab:cd opt
do
  case "$opt" in
    a) echo "Found the -a option";
    b) echo "Found the -b option with parameter value $OPTARG";
    c) echo "Found the -c option";
    d) echo "Found the -d option";
    *) echo "Unknown option: $opt"
esac
```
done
#
shift [$OPTIND - 1 ]
#
echo
count=1
for param in "@"
do
  echo "Parameter count: $param"
  count=$[$count + 1]
done
exit
$
./extractoptparamswithgetopts.sh -db BValue test1 test2
```
Found the -d option
Found the -b option with parameter value BValue

- Parameter 1: test1
- Parameter 2: test2
$ 

现在，你拥有了一个功能齐全的命令行选项和参数处理工具，你可以在你所有的脚本中使用！

# 标准化选项

当你创建脚本时，显然你控制着发生的情况。选择使用哪些选项以及如何选择使用它们完全取决于你。

然而，一些选项在 Linux 世界中已经获得了一种某种标准的含义。如果你在 Shell 脚本中保留这些选项，你的脚本将变得更符合用户习惯。

表格 14-1 显示了 Linux 中使用的命令行选项的一些常见含义。

你可能在通过整本书与各种 bash 命令交互的过程中已经识别了大部分这些选项的含义。为你的选项使用相同的含义有助于用户与你的脚本交互，而无需担心何时该使用哪些选项。

# 第 14 章：处理用户输入

# 表格 14-1 常见的 Linux 命令行选项

| 选项 | 说明 |
|---|---|
| -a | 显示所有对象。 |
| -c | 输出。 |
| -d | 指定目录。 |
| -e | 扩展文本。 |
| -f | 指定文件。 |
| -h | 显示帮助信息。 |
| -i | 忽略大小写。 |
| -l | 详细输出。 |
| -n | 抑制换行符。 |
| -o | 指定输出。 |
| -q | 静默模式运行。 |
| -r | 递归处理。 |
| -s | 静音模式运行。 |
| -v | 详细输出。 |
| -x | 排除对象。 |
| -y | 回答 yes。 |

# 获取输入

虽然提供命令行选项是获取数据的很好的方法，但有时你需要交互式。`read` 命令可以从键盘或文件接受输入。

# 读取基础

`read` 命令允许你等待输入。在接收输入后，`read` 命令将其放入变量中。这里是最简单的示例：
```
$ cat extractname.sh
!/bin/bash
# 使用 read 命令
#
echo
read -p "Enter name: " name
echo "Hello $name, welcome to script."
exit
```
```
$ ./extractname.sh
Enter name: Richard
Hello Richard, welcome to script.
$
```
你会注意到这个示例中 `case` 语句有些不同之处。当 `getopts` 命令解析命令行选项时，它会剥离开头的横杠，因此你不需要在 `case` 定义中定义横杠。

`getopts` 命令提供了几个很棒的功能。首先，你可以在参数值中包含空格：
```
$ ./extractwithgets.sh -b "B1 BValue2" -a
```
Found the -b option with parameter value B1 BValue2
Found the -a option
$
另一个很棒的功能是你可以同时运行选项和参数值而不需要空格：
```
$ ./extractwithgets.sh -abBValue
```
Found the -a option
Found the -b option with parameter value BValue
$
`getopts` 命令正确解析了来自 `-b` 选项的 `BValue`。此外，`getopts` 命令会将命令行中发现的未定义选项合并成单个输出，即问号：
```
$ ./extractwithgets.sh -d
```
Unknown option: ?
$ ./extractwithgets.sh -ade
Found the -a option
Unknown option: ?
Unknown option: ?
$
```
任何在 `optstring` 中定义的选项字母都会以问号的形式发送给你的代码。
```
`getopts` 命令知道何时停止处理选项并将参数留给你处理。当 `getopts` 处理每个选项时，它会将 `OPTIND` 变量加 1。当你完成 `getopts` 处理后，你可以使用 `OPTIND` 值配合 `shift` 命令移动到参数：
```
$ extractwithoptparamswithgetopts.sh
!/bin/bash
# 使用 getopts 提取命令行选项和参数
#
echo
```
（续）
```
while getopts :ab:cd opt
do
  case "$opt" in
    a) echo "Found the -a option";
    b) echo "Found the -b option with parameter value $OPTARG";
    c) echo "Found the -c option";
    d) echo "Found the -d option";
    *) echo "Unknown option: $opt"
esac
```
done
#
shift [$OPTIND - 1 ]
#
echo
count=1
for param in "@"
do
  echo "Parameter count: $param"
  count=$[$count + 1]
done
exit
$
./extractoptparamswithgetopts.sh -db BValue test1 test2
```
Found the -d option
Found the -b option with parameter value BValue
- Parameter 1: test1
- Parameter 2: test2
$ 

现在，你拥有了一个功能齐全的命令行选项和参数处理工具，你可以在你所有的脚本中使用！

`read` 命令中的 `-n` 选项会抑制字符串末尾的换行符，允许提示。

# 标准化选项

当你创建脚本时，显然你控制着发生的情况。选择使用哪些选项以及如何选择使用它们完全取决于你。

然而，一些选项在 Linux 世界中已经获得了一种某种标准的含义。如果你在 Shell 脚本中保留这些选项，你的脚本将变得更符合用户习惯。

表格 14-1 显示了 Linux 中使用的命令行选项的一些常见含义。你可能在通过整本书与各种 bash 命令交互的过程中已经识别了大部分这些选项的含义。为你的选项使用相同的含义有助于用户与你的脚本交互，而无需担心何时该使用哪些选项。

`REPLY` 环境变量包含了输入中的所有数据，它可以像其他变量一样在 Shell 脚本中使用。

你也可以在 `read` 命令行时不指定变量。如果你这样做，`read` 命令会将收到的任何数据放入特殊的环境变量 `REPLY` 中：
