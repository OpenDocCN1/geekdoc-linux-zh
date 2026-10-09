
下面的脚本`whos`演示了`for`结构中隐含的`"$@"`的用处。你向`whos`提供一个或多个用户登录名作为参数，`whos`会显示关于这些用户的信息。`whos`脚本从`/etc/passwd`文件的第一字段和第五字段获取其显示的信息。第一个字段始终包含用户名，第五字段通常包含用户的全名。你可以提供登录名或名称作为参数来识别用户。`whos`脚本类似于`finger`工具，尽管`whos`提供的信息较少。

```
$cat whos
#!/bin/bash
# adapted from finger.sh by Lee Sailer
# UNIX/WORLD, III:11, p. 67, Fig. 2

if [ $@ -eq 0 ]
	then
	echo "Usage: whos id.." 1>&2
	exit 1
fi

for id
do
	gawk -F '{print $1, $5}' /etc/passwd |
	grep -i "$id"
done
```

下方的`whos`识别出用户名为`chas`的以及名字为`Marilou Smith`的用户：

```
$whos chas "Marilou Smith"
chas Charles Casey
msmith Marilou Smith
```

## "$@"

`whos`脚本使用`for`语句来遍历命令行参数。在这个脚本中，`for`循环中隐含的`"$@"`使用特别有益，因为它导致`for`循环将包含空格（`SPACE`）的参数视为单个参数。此示例为`Marilou Smith`加了引号，导致`shell`将其作为单个参数传递给脚本。然后语句中隐含的`"$@"`使`shell`重新生成带引号的参数`Marilou Smith`，使其被视为单个参数。

```
awk
```

对于每个命令行，`whos`都会搜索`/etc/passwd`文件。在`for`循环内部，`awk`工具（第 12 章）从`/etc/passwd`的行中提取第一个（`$1`）和第五（`$5`）字段。`-F`选项允许`grep`在读取`/etc/passwd`时使用冒号（`:`）作为分隔符。`grep`命令设置并使用了`$1`和`$5`参数；它们包含在单引号内并由`shell`解析。不要将这些参数与对应于命令行参数的位置参数混淆。第一个和第五个字段被通过管道发送给`grep`（第 683 页）。`grep`工具搜索`Sid`（即该名字）。

## while

`while`结构（`tcsh`中不可用）具有如下语法：

```
while condition
do
    commands
done
```

`while`结构在条件为真时会执行命令块。条件在每次循环迭代的开始时进行评估。如果条件为假，循环终止。

接下来的脚本展示了一个从零数到四的`while`循环：

```bash
number=0
while [ $number -lt 5 ]
do
    echo $number
    ((number++))
done
```

### 图 11-5. A while 流程图

![](img/bf98da8888128a6a4235ca4c80ee1f24_591_0.png)

## test

接下来的脚本首先将`number`初始化为零。然后`test`判断`number`是否小于 10。只要`test`返回真，该结构就会执行命令。对于数值比较，使用`-ne`（不等于）、`-eq`（等于）、`-gt`（大于）、`-ge`（大于等于）、`-lt`（小于）或`-le`（小于或等于）。对于字符串比较，使用`=`（等于）或`!=`（不等于）。

```bash
#!/bin/bash
number=0
while [ $number -lt 10 ]
do
    echo -n "$number"
    ((number++))
done
```

`echo`命令的`-n`参数防止`echo`发出换行符，以便使下一个提示符出现在最左侧列。

```bash
echo "Usage: spell_check file file2" 1>&&2
echo "file1: list of correct spellings" 1>&&2
echo "file2: file to be checked" 1>&&2
exit 1
fi

if [ ! -r "$1" ]
then
    echo "spell_check: $1 is not readable" 1>&&2
    exit 1
fi

if [ ! -r "$2" ]
then
    echo "spell_check: $2 is not readable" 1>&&2
    exit 1
fi

aspell -l < "$2" |
while read line
do
    if ! grep "^$line$" "$1" > /dev/null
    then
        echo $line
    fi
done
```

`spell_check`脚本将`aspell`的输出（使用`-l`选项，会生成一个拼写错误的单词列表）通过管道传递到`while`结构的标准输入，该结构从标准输入每次读取一行（每行有一个单词）。只要能接收到一行内容，测试命令（即`read line`）就会返回一个真的退出状态。

在`while`循环内部，一个`if`语句监控`grep`的返回值，用以判断该行是否在用户的正确拼写单词列表中。`grep`搜索的模式（`line`的值）前后都有特殊字符，分别指定行的开始和结束（分别为`^`和`$`）。这些特殊字符确保了只有当`line`变量匹配正确拼写文件中的某行时，`grep`才会找到匹配。（否则，如果正确拼写文件中包含`paulson`一词，`grep`会在`aspell`的输出中匹配`paul`等字符串）。这些特殊字符与`line`变量的值共同构成了一个正则表达式（附录 A）。

`grep`的输出被重定向到`/dev/null`（第 122 页），因为不需要输出；只有退出码是重要的。如果语句检查`grep`的取反退出状态（开头的感叹号会取反或改变退出状态的含义——真变为假，反之亦然），那么在找到匹配行时，其状态为 0 或假（取反后为假）。如果退出状态不是假（取反后为真），则说明该单词不在正确拼写文件中。`echo`内置命令将不在正确拼写文件的单词列表发送到标准输出。

一旦检测到`EOF`（文件末尾），`read`将返回一个假的退出状态。随后，控制权退出`while`结构，脚本终止。

在使用`spell_check`之前，请创建一个包含正确拼写的文件，其中你经常使用但不在标准字典中的单词。例如，如果你在名为`Blinkship`和`Klimowski`的律师事务所工作，你会将`Blinkship`和`Klimowski`放入文件中。以下示例显示了`spell_check`检查名为`memo`的文件的拼写，并从错误拼写单词的输出列表中移除`Blinkship`和`Klimowski`：

```
$aspell -1 < memo
Blinkship
Klimowski
targat
hte
$cat word_list
Blinkship
Klimowski
$spell_check word_list memo
targat
hte
```

关于`aspell`的更多信息，请参考第 589 页。

[1] 该`if`语句也可以写成：

```bash
if ! grep -qw "line" "$1"
```

`-q`选项会抑制`grep`的输出，只返回退出码。`-w`选项导致`grep`仅匹配整个单词。

## until

`until`（在`tcsh`中不可用）和`while`（在`tcsh`中可用，语法略有不同）结构非常相似，区别在于循环顶部执行的测试的含义。图 11-6 显示，`until`会持续循环，直到测试命令返回一个真的退出状态。`while`结构在测试命令继续返回真或非错误条件时循环。

## case

`case`结构（图 11-7，第 461 页）是一种多分支决策机制。通过该结构的路径取决于测试字符串（`test-string`）与其中一个模式（`patterns`）之间的匹配或不匹配。`tcsh`中的`case`控制结构使用`switch`，其语法如下：

```
case test-string in
  pattern-1)
    commands-1
    ;
  pattern-2)
    commands-2
    ;
  pattern-3)
    commands-3
    ;
  ...
esac
```

### 图 11-7. case 流程图

![](img/bf98da8888128a6a4235ca4c80ee1f24_601_0.png)

下面的`case`结构检查用户作为测试字符串输入的字符。该值被存储在变量`letter`中。如果测试字符串的值为`A`，该结构将执行`A`之后的命令。右括号是`case`控制结构的一部分，而不是模式的一部分。如果测试字符串的值为`B`或`C`，该结构将执行匹配的模式之后的命令。星号（`*`）表示*任何字符字符串*，并作为没有匹配项时的兜底方案。如果没有模式匹配测试字符串，且没有兜底项（`*pattern`），则控制权将传递到`esac`语句之后的命令，而`case`结构不执行任何操作。

```bash
$case1
echo -n "Enter A, B, or C: " 
read letter
case "$letter" in
  A)
    echo "You entered A"
  ;
  B)
    echo "You entered B"
    ;;
  C)
    echo "You entered C"
    ;;
  *)
    echo "You did not enter A, B, or C"
    ;;
esac

$case1 A, B, or C: B
You entered B
```

下一次执行`case1`显示用户输入了小写`b`。由于测试字符串`b`不匹配大写`B`模式（或`case`语句中的任何其他模式），程序将执行兜底模式之后的命令并显示消息：

```bash
$case1
Enter A, B, or C: b
You did not enter A, B, or C
```

`case`结构中的模式类似于歧义的文件引用。它可以包含表 11-2 所示的任何特殊字符和字符串。

### 表 11-2. 模式

| 模式 (Pattern) | 功能 |
| :--- | :--- |
| `*` | 匹配任何字符字符串。用于默认情况。 |
| `?` | 匹配任何单个字符。 |
| `[...]` | 定义字符类。括号内的任何字符都会被逐一尝试，以尝试匹配单个字符。两个字符之间的连字符指定字符范围。 |
| `\|` | 分隔满足`case`结构特定分支的备选方案。 |

接下来的脚本同时接受大写和小写字母：

```bash
$cat case2
echo -n "Enter A, B, or C: " 
read letter
case "$letter" in
    a|A)
        echo "You entered A"
        ;;
    b|B)
        echo "You entered B"
        ;;
    c|C)
        echo "You entered C"
        ;;
*)
        echo "You did not enter A, B, or C"
        ;;
esac

$case2
Enter A, B, or C: b
You entered B
```

## optional

下面的示例展示了如何使用`case`结构创建一个简单的菜单。`command_menu`脚本使用`echo`显示项目并提示用户进行选择。（`select`控制结构 [第 466 页] 使得创建菜单变得简单得多。）`case`结构根据用户的选择执行相应的程序。

```bash
#!/bin/bash

# 简单命令的界面

echo -e "\n   COMMAND MENU\n"
echo " a.    Current date and time"
echo " b.    Users logged in"
echo " c.    Name of the working directory"
echo -e "\n d.    Contents of the working directory\n"
echo -n "Enter a, b, c, or d: "
read answer
case "$answer" in
  a)
    date
    ;;
  b)
    who
    ;;
  c)
    pwd
    ;;
  d)
    ls
    ;;
  *)
    echo "There is no selection: $answer"
    ;;
esac

$command_menu

+   COMMAND MENU
a. Current date and time
b. Users logged in
c. Name of the working directory
d. Contents of the working directory

Enter a, b, c, or d: a

Wed Jan 5 12:31:12 PST 2005
```

在设置脚本变量后，它将替换用法和错误消息中的脚本文件名。通过使用从调用脚本的命令派生的变量，而不是硬编码在脚本中的文件名，你可以为脚本创建链接或对其进行重命名，而用法和错误消息仍将提供准确的信息。

## 命名临时文件

`safedit`的一个重要特性与在临时文件命名中使用`$$`变量有关。`esac`语句后面的语句创建并为`tempfile`变量赋值了一个值。该变量包含存储在`/tmp`目录下的临时文件名称，因为许多临时文件以`shell`的`PID`号开头，并以脚本名称结尾。使用`PID`号可以确保文件名是唯一的，`safedit`不会尝试覆盖已存在的文件，即使有两个人同时使用`safedit`也是如此。末尾会附加脚本名称，这样如果文件由于原因留在了`/tmp`中，你也可以查出它源自哪里。

`PID`号被置于脚本文件名之前而不是，是因为旧版本的`UNIX`对文件名有 14 个字符的限制。`Linux`系统没有这个限制。`PID`号确保了文件名的唯一性，它被放置在开头是为了确保它不会被截断。（如果脚本部分被截断，文件名仍然是唯一的。）因此，当几行后的`if`控制结构内部创建备份文件时，文件名由字符串`bak`组成，随后是正在编辑的文件名。在旧系统上，如果将`bak`作为后缀而不是前缀且原始文件名长度为 14 个字符，`bak`可能会丢失导致原始文件被覆盖。`basename`工具在为`Seditfile`加上`bak`前缀之前提取其简单文件名。

第四，`safedit`在`if`结构中使用了一个不常见的测试命令：`vim Seditfile`。该测试命令调用`vim`来编辑`Seditfile`。当你完成文件编辑并退出`vim`时，`vim`返回一个退出码。如果控制结构使用该退出码来决定执行哪个分支，如果编辑会话成功完成，`vim`返回 0，然后执行后续语句。如果`vim`未正常终止（如果用户杀杀了`vim`进程，就会发生这种情况），`vim`返回一个非零退出状态，脚本将执行`else`之后的语句。

## select

`select`控制结构（`tcsh`不可用）基于`Korn Shell`中的相同结构。它显示一个菜单，根据用户对项目的选择为变量分配值，并执行一系列命令。`select`控制结构具有以下语法：

```
select varname [in arg ..]
do
    commands
done
```

`select`结构显示一个`arg`项目的菜单。如果你省略了关键字`"in"`和参数列表，`select`将使用位置参数代替`arg`项目。菜单在每个项目前都有数字格式化。例如，一个起始于内容的`select`结构

```
select fruit in apple blueberry kiwi orange watermelon STOP
```

显示如下菜单：

- 1) `apple`
- 3) `blueberry`
- 5) `orange`
- 7) `STOP`
- 2) `banana`
- 4) `kiwi`
- 6) `watermelon`

`select`结构使用`LINES`和`COLUMNS`变量的值来确定显示区域。（`LINES`的默认值为 24；`COLUMNS`的默认值为 80。）当`COLUMNS`设置为 20 时，菜单如下：

- 1) `apple`
- 2) `banana`
- 3) `blueberry`
- 4) `kiwi`
- 5) `orange`
- 6) `watermelon`
- 7) `STOP`

## PS3

在显示菜单后，`select`会显示`PS3`的值，即特殊的`select`提示符。`PS3`的默认值是`# `，通常你会将`PS3`设置为一个一个更有具意义的值。当你输入一个有效数字（菜单范围内的数字）来响应`PS3`提示符时，`select varname`将赋值为与输入数字对应的参数。如果你输入无效内容，`varname`将置为空。`select`会将你的响应存储在关键字变量`REPLY`中，然后执行`do`和`done`之间的命令。如果你在没有输入参数的情况下按回车，`shell`将重新显示循环和`PS3`提示符。

`select`结构会继续发布`PS3`提示符并执行命令，直到某些情况导致它通常遇到`break`或`exit`语句。`break`语句退出循环，`exit`语句退出脚本。

以下脚本说明了`select`的用法：
