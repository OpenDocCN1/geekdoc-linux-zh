
使用函数库的关键是 `source` 命令。`source` 命令在当前 shell 上文中执行命令，而不是创建一个新的 shell 来执行它们。你使用 `source` 命令在 shell 脚本内部运行库文件。这使得函数对脚本可用。

`source` 命令有一个快捷别名，称为点操作符（dot operator）。要在 shell 脚本中源化 `myfuncs` 库文件，你只需要添加以下行：

```bash
. ./myfuncs
```

此示例假设 `myfuncs` 库文件与 shell 脚本位于同一目录下。如果你需要使用适当的路径来访问该文件。这里创建一个使用 `myfuncs` 库文件的脚本示例：

```bash
$ cat test14

#!/bin/bash

# 使用库文件中定义的函数

. ./myfuncs
```

```bash
value1=10

value2=5

result=`addem $value1 $value2`

result2=`multem $value1 $value2`

result3=`dive $value1 $value2`

echo "The result of adding them is: $result"

echo "The result of multiplying them is: $result2"

echo "The result of dividing them is: $result3"

$ ./test14

The result of adding them is: 15

The result of multiplying them is: 50

The result of dividing them is: 2

$
```

该脚本成功地使用了 `myfuncs` 库中定义的函数。

# 在命令行上使用函数

你可以使用脚本函数来创建相当复杂的操作。有时，如果能够直接在命令行界面上使用这些函数会很好。

就像你可以在 shell 脚本中使用脚本函数作为命令一样，你也可以在命令行界面将脚本函数作为命令。这是一个非常棒的功能，因为一旦你在 shell 中定义了函数，就可以在系统的任意目录下使用它；你不需要担心脚本是否在你的 `PATH` 环境变量中。技巧在于让 shell 识别该函数。有几种方法可以实现这一点。

## 在命令行上创建函数

由于 shell 在你输入命令时对其进行解释，因此你可以直接在命令行上定义函数。有两种方法可以做到。

第一方法在一行内定义所有函数：

```bash
$ function dime { echo [$1 / $2]; }
$ dime 100 5
20
$
```

当你在命令行上定义函数时，必须记住在每个命令的末尾包含一个分号，shell 知道在哪里处分隔命令：

```bash
$ function doublet { read -p "Enter value: " value; echo [$value * 2]; }
$ doublet
Enter value: 20
40
$
```

另一种方法是使用多行来定义函数。当你这样做时，bash shell 使用次级提示符提示你输入更多命令。使用这种方法，你不需要在每个命令的末尾放置分号；只需按回车键即可：

```bash
$ function multem {
> echo [$1 * $2]
 }
```

# 第三部分：高级 shell 脚本编写

```bash
$ multem 2 5
10
$
```

当你在函数末尾使用大括号 `}` 时，shell 就知道你已经完成了。

**注意**：在命令行上创建函数时要格外小心。如果你使用的函数名称与内置命令或其他命令同名，该函数将覆盖原始命令。

# 在 .bashrc 中定义函数

直接在命令行上定义 shell 函数显而易见的缺点是当你退出 shell 时，你的函数就会消失。对于复杂的函数，这可能会变成一个问题。一种简单得多的方法定义函数，让 shell 在每次启动新 shell 时重新加载它。这样做最好的地方是 `.bashrc` 文件。

## 定义函数

你可以直接在主目录下的 `.bashrc` 文件中定义函数。大多数 Linux 发行版已经定义了一些内容，所以注意不要删除它们。只需将你的函数添加到文件的末尾即可。这是一个这样做的示例：

```bash
$ cat .bashrc
# Source global definitions
if [ ... ]; then
```
（注：此处根据原文逻辑应在 `.bashrc` 底部添加函数）

当你开始一个新的 shell 时，shell 会自动重新加载这些函数。使用 `source` 命令（或其别名点操作符）来源化库文件。这被称为源化库文件。

即使不源化库文件，函数在脚本中也能正常工作。

### 总结

shell 函数允许将脚本中重复的代码放在一个地方。

（此处省略后续总结内容）

下一章将讨论在脚本中使用文本图形的主题。

# 第 15 章

## 为脚本添加色彩

多年来，Shell 脚本一直以单调无聊而闻名。然而，如果你计划在图形化环境中运行脚本，就不不必如此。除了使用 `read` 和 `echo` 语句外，还有许多方法可以与脚本用户交互。本章将深入探讨几种不同的方法，让你能够为交互式脚本注入活力，让它们看起来不再过时。

- 本章内容
- 创建文本菜单
- 让脚本变得彩色
- 文本窗口小部件
- 使用 X Windows 图形

## 创建文本菜单

创建交互式 Shell 脚本最常见的方法是利用菜单。为客户提供各种选项的选择可以帮助他们准确了解脚本可以和不能[做]什么。

菜单脚本通常会清空显示区域，然后显示可用选项列表。客户可以通过按下为每个选项分配的相应字母或数字来选择选项。图 15-1 显示了示例菜单的布局。

脚本菜单的核心是 `case` 命令（见第 9 章）。`case` 命令根据客户从菜单中选择的字符执行执行特定的命令。

接下来的章节将引导你完成创建基于菜单的 Shell 脚本的步骤。

### 图 15-1
从 Shell 脚本显示菜单

![](img/adcbcf1053b52dbf22f3aa187738232f_417_0.png)

### 创建菜单布局

创建菜单的第一步显然是确定你想在菜单中显示的元素，并按照你想要的方式进行布局。

在创建菜单之前，通常清空显示器屏幕是一个好主意。这可以让你在一个干净的环境中显示菜单，而不会被其他文本干扰。

`clear` 命令使用终端会话的 `terminfo` 数据（见第 2 章）来清空显示器上显示的任何文本。执行 `clear` 命令后，你可以使用 `echo` 命令显示你的菜单元素。

默认情况下，`echo` 命令只能显示可打印的文本字符。在创建菜单项时，使用不可打印项（如制表符和换行符）通常很有帮助。要在 `echo` 命令中包含这些字符，你必须使用 `-e` 选项。因此，命令：

```
echo -e "1\tDisplay disk space"
```

结果输出为：

1. Display disk space

这非常有助于菜单项布局的格式化。只需几个 `echo` 命令，你就可以创建一个看起来合理的菜单：

```
clear
echo -e "\t\t\tSys Admin Menu\n"
echo -e "\t1. Display disk space"
echo -e "\t2. Display logged on users"
echo -e "\t3. Display memory usage"
echo -e "\t0. Exit menu\n"
echo -e "\t\tEnter option: "
```

最后一行的 `-n` 选项在显示菜单时末尾不带换行符。这使得菜单看起来更专业，因为光标将停留在行尾等待客户的输入。

创建菜单的最后一部分是从客户那里获取输入。这是通过使用 `read` 命令完成的（见第 11 章）。由于我们只期望单个字符输入，很方便的做法是在 `read` 命令中使用 `-n` 选项来只获取一个字符。这允许客户输入数字而无需按回车键：

```
read -n 1 option
```

接下来，你需要创建你的菜单函数

### 创建菜单函数

将 Shell 脚本选项作为一组独立的函数来创建更为简单。这允许你创建一个简单、简洁且易于遵循的 `case` 命令。

要做到这一点，你需要为每个菜单选项创建独立的 Shell 函数。创建菜单 Shell 脚本的第一步是定义你想让脚本执行的函数。

（注：原文后续部分存在大量重复，此处已根据核心逻辑整合并翻译）

```bash
function memusage (
  clear
  cat /proc/meminfo
)
```

```bash
PS3="Enter option: "
select option in "Display disk space" "Display logged on users" "Display memory usage" "Exit program"
do
```
