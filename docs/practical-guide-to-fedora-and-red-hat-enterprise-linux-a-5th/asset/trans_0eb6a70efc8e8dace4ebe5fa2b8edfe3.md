
将输入赋值给 **key_3** 变量。一旦用户输入了与原始键之一（**key_2**）匹配的字符串，**until** 循环终止，并且键盘回显再次开启。

## break 和 continue

你可以使用 **break** 或 **continue** 语句来中断 **for**、**while** 或 **until** 循环。 **break** 语句将控制权转移到 **done** 语句之后的语句，从而终止循环的执行。 **continue** 命令将控制权转移到 **done** 语句，从而继续循环的执行。

以下脚本演示了这两个语句的用法。 **for** **in** 结构循环遍历 1–10 的值。第一个 **if** 语句在索引值小于或等于 3（**$index -le 3**）时执行其命令。第二个 **if** 语句在索引值大于或等于 8（**$index -ge 8**）时执行其命令。在这两个 **if** 之间，**echo** 显示索引的值。对于所有包括 3 在内的较小值，第一个 **if** 语句显示 **continue** 并执行 **continue** 语句，该语句跳过 **echo $index** 和第二个 **if** 语句，并继续下一个 **for** 语句。对于值 8，第二个 **if** 语句显示 **break** 并执行 **break** 语句，从而退出 for 循环：

```bash
$ cat brk
for index in 1 2 3 4 5 6 7 8 9 10
do
if [ $index -le 3 ] ; then
echo "continue"
continue
fi
#
echo $index
#
if [ $index -ge 8 ] ; then
echo "break"
break
fi
done

$ brk
continue
continue
continue
4
5
6
7
8
break
```

## case

case 结构（图 27-7，第 912 页）是一种多分支决策机制。通过该结构的路径取决于 *test-string* 与其中一个 *patterns* 之间是否匹配。case 控制结构具有如下语法：

```bash
case test-string in
	pattern-1)
		commands-1
	;;
	pattern-2)
		commands-2
	;;
	pattern-3)
		commands-3
	;;
... 
	esac
```

以下 case 结构检查用户输入作为 *test-string* 的字符。该值存储在变量 *letter* 中。如果 *test-string* 的值为 A，该结构执行跟随 *pattern* A 之后的命令。右括号是 case 控制结构的一部分，而不是 *pattern* 的一部分。如果 *test-string* 的值为 B 或 C，该结构执行跟随匹配 *pattern* 之后的命令。星号 (*) 表示*任意字符串*，并作为未匹配时的兜底选项。如果没有 *pattern* 与 *test-string* 匹配，且没有通配 (*) *pattern*，控制权将传递给 esac 语句之后的命令，而 case 结构不采取任何操作。

```bash
$ cat case1
  echo -n "Enter A, B, or C: "
  read letter
  case "$letter" in
    A)   echo "You entered A"
    ;;
    B)   echo "You entered B"
    ;;
    C)   echo "You entered C"
    ;;
    *)   echo "You did not enter A, B, or C"
    ;;
  esac

$ case1
Enter A, B, or C: B
You entered B
```

![](img/f28adb66a7398a382f0505e0ba74a872_952_0.png)

图 27-7 Case 流程图

case1 的下一次执行显示用户输入了小写 b。因为 test-string b 与大写 B 模式（或 case 语句中的任何其他模式）不匹配，程序执行跟随通配模式后的命令并显示消息：

```bash
$ case1
Enter A, B, or C: b
You did not enter A, B, or C
```

case 结构中的模式类似于模糊的文件引用。它可以包含表 27-2 中显示的任何特殊字符和字符串。

以下脚本同时接受大写字母和小写字母：

```bash
$ cat case2
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

$ case2
Enter A, B, or C: b
You entered B
```

### 表 27-2 模式

| 模式 | 功能 |
| :--- | :--- |
| \* | 匹配任意字符串。用于默认情况。 |
| ? | 匹配任何单个字符。 |
| [...] | 定义字符类。括号内包含的任何字符都会逐一尝试，以匹配单个字符。两个字符之间的连字符指定一个字符范围。 |
| \| | 分隔满足 case 结构中特定分支的替代选择。 |

**可选** 以下示例展示了如何使用 **case** 结构创建简单的菜单。 **command\_menu** 脚本使用 **echo** 呈现菜单项并提示用户进行选择。（**select** 控制结构 [第 917 页] 使菜单编码变得更加容易。）然后，**case** 结构根据用户的选择执行相应的实用程序。

```bash
$ cat command_menu
#!/bin/bash
# menu interface to simple commands

echo -e "\n\t\tCOMMAND MENU\n"
echo "	a. Current date and time"
echo "	b. Users currently logged in"
echo "	c. Name of the working directory"
echo -e "	d. Contents of the working directory\n"
echo -n "Enter a, b, c, or d: "
read answer
echo

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

$ command_menu
    COMMAND MENU
    a. Current date and time
    b. Users currently logged in
    c. Name of the working directory
    d. Contents of the working directory
    Enter a, b, c, or d: a
    Wed Jan 9 12:31:12 PST 2008
```

**echo -e** -e 选项使 echo 将 \n 解释为换行符。如果不包含此选项，echo 不会输出使菜单易于阅读的额外空行，而是输出（字面）的两个字符序列 \n。 -e 选项使 echo 解释其他几个反斜杠引用的字符（表 27-3）。请记住，要用引号（即，用双引号包围字符串）引住反斜杠引用的字符，以便 shell 不解释它，而是将反斜杠和字符传递给 echo。参见 xpg_echo（第 341 页）了解避免使用 -e 选项的方法。

### 表 27-3 echo 中的特殊字符（必须使用 -e）

| 引用字符 | echo 显示 |
| :--- | :--- |
| \a | 警报（铃） |
| \b | 退格 |
| \c | 抑制尾随换行 |
| \f | 换页 |
| \n | 换行 |
| \r | 回车 |
| \t | 水平制表符 |
| \v | 垂直制表符 |
| \\ | 反斜杠 |
| \nnn | ASCII 八进制代码为 nnn 的字符；如果 nnn 无效，echo 原样显示该字符串 |

你还可以使用 case 控制结构在脚本中采取各种操作，具体取决于调用脚本时使用的参数数量。以下名为 safedit 的脚本使用基于命令行参数数量（$#）进行分支的 case 结构。它保存你用 vim 编辑的文件的备份副本。

```bash
$ cat safedit
#!/bin/bash
# UNIX/WORLD, IV:11
PATH=/bin:/usr/bin
script=$(basename $0)
case $# in
    0)
        vim
        exit 0
        ;;
    1)
        if [ ! -f "$1" ]
        then
            vim "$1"
            exit 0
        fi
        if [ ! -r "$1" -o ! -w "$1" ]
        then
            echo "$script: check permissions on $1" 1>&2
            exit 1
        else
            editfile=$1
        fi
        if [ ! -w "." ]
        then
            echo "$script: backup cannot be created in the working directory" 1>&2
            exit 1
        fi
        ;;
    *)
        echo "Usage: $script [file-to-edit]" 1>&2
        exit 1
        ;;
esac

tmpfile=/tmp/$$.$script
cp $editfile $tmpfile
if vim $editfile
then
   mv $tmpfile bak.$(basename $editfile)
   echo "$script: backup file created"
else
   mv $tmpfile editerr
   echo "$script: edit error--copy of original file is in editerr" 1>&2
fi
```

如果你不带任何参数调用 `safedit`，`case` 结构执行其第一个分支，并在没有文件名参数的情况下调用 `vim`。由于没有编辑现有文件，`safedit` 不会创建备份文件。如果你带有一个参数调用 `safedit`，它运行 `case` 结构第二个分支中的命令，并验证 `$1` 指定的文件尚不存在，或者是用户具有读和写权限的文件名称。`safedit` 脚本还验证用户对当前工作目录是否具有写权限。如果用户带有一个以上的参数调用 `safedit`，`case` 结构的第三个分支将显示用法信息并以状态 `1` 退出。

## 设置 PATH

除了使用 `case` 结构根据命令行参数数量进行分支外，`safedit` 脚本还引入了其他几个特性。首先，在脚本开头，将 `PATH` 变量设置为搜索 `/bin` 和 `/usr/bin`。以这种方式设置 `PATH` 可确保脚本执行的命令是标准实用程序，这些实用程序保存在这些目录中。通过在脚本内部设置 `PATH`，你可以避免以下问题：用户将 `PATH` 设置为优先搜索他们自己的目录，并且拥有与脚本调用的实用程序同名的脚本或程序。你也可以在脚本中包含绝对路径名以实现此目的，但这种做法可能会降低脚本的可移植性。

## 程序名称

在第二个 `safedit` 特性中，以下行创建一个名为 `script` 的变量，并将脚本的简单文件名赋值给它：

```bash
script=$(basename $0)
```

`basename` 实用程序将其参数的简单文件名片段发送到标准输出，该输出通过命令替换被赋值给 `script` 变量。`$0` 保存调用脚本时使用的命令（第 931 页）。无论用户使用以下哪个命令调用脚本，`basename` 的输出都是简单文件名 `safedit`：

```bash
$ /home/alex/bin/safedit memo
$ ./safedit memo
$ safedit memo
```

设置 `script` 变量后，它会替换用法和错误消息中的脚本文件名。通过使用从调用脚本的命令中推导出的变量，而不是硬编码到脚本中的文件名，你可以创建

