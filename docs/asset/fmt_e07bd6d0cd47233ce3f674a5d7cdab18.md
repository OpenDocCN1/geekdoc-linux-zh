
```bash
#!/bin/bash

# case-menu: a menu driven system information program

clear
echo "
Please Select:

A. Display System Information
B. Display Disk Space
C. Display Home Space Utilization
Q. Quit
"
read -p "Enter selection [A, B, C or Q] > "

case $REPLY in
    q|Q)    echo "Program terminated."
            exit
            ;;
    a|A)    echo "Hostname: $HOSTNAME"
            uptime
            ;;
    b|B)    df -h
            ;;
    c|C)    if [[ $(id -u) -eq 0 ]]; then
                echo "Home Space Utilization (All Users)"
                du -sh /home/*
            else
                echo "Home Space Utilization ($USER)"
                du -sh $HOME
            fi
```

```
    ;;
    *) echo "Invalid entry" >&2
    exit 1
    ;;
esac
```

在这里，我们修改 `case-menu` 程序以使用字母而不是数字进行菜单选择。注意新的模式如何允许输入大写和小写字母。

#### 总结

`case` 命令是我们编程技巧包中的一个方便的补充。正如我们在下一章中将看到的那样，它是处理某些类型问题的完美工具。

#### 进一步阅读

- *Bash Reference Manual* 中关于 Conditional Constructs 的部分详细描述了 `case` 命令：

- http://tiswww.case.edu/php/chet/bash/bashref.html#SEC21

- *Advanced Bash-Scripting Guide* 提供了 `case` 应用的更多示例：

- http://tldp.org/LDP/abs/html/testbranch.html

### 33 – 位置参数

我们程序中缺少的一个功能是接受和处理命令行选项和参数的能力。在本章中，我们将研究 shell 功能，使我们的程序能够访问命令行内容。

#### 访问命令行

shell 提供了一组称为位置参数的变量，其中包含命令行上的各个单词。变量命名为 0 到 9。它们可以这样演示：

```bash
#!/bin/bash

# posit-param: script to view command line parameters
echo "
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"
```

一个非常简单的脚本，显示变量 `$0-$9` 的值。执行时不带命令行参数：

```
[me@linuxbox ~]$ posit-param

$0 = /home/me/bin/posit-param
```

```
$1 =
$2 =
$3 =
$4 =
$5 =
$6 =
$7 =
$8 =
$9 =
```

即使没有提供参数，`$0` 也始终包含出现在命令行上的第一项，即正在执行的程序的路径名。当提供参数时，我们看到的结果：

```
[me@linuxbox ~]$ posit-param a b c d

$0 = /home/me/bin/posit-param
$1 = a
$2 = b
$3 = c
$4 = d
$5 =
$6 =
$7 =
$8 =
$9 =
```

> **注意：** 你实际上可以使用参数扩展访问超过九个参数。要指定大于九的数字，请用大括号括住该数字。例如 `${10}`、` ${55}`、` ${211}` 等。

#### 确定参数数量

Shell 还提供了一个变量 `$#`，它会给出命令行上的参数数量：

```bash
#!/bin/bash

# posit-param: script to view command line parameters
echo "
Number of arguments: $#
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"
```

结果：

```
[me@linuxbox ~]$ posit-param a b c d

Number of arguments: 4
$0 = /home/me/bin/posit-param
$1 = a
$2 = b
$3 = c
$4 = d
$5 =
$6 =
$7 =
$8 =
$9 =
```

#### shift – 获取对多个参数的访问

但当我们给程序提供大量参数时，例如这样会怎样：

```
[me@linuxbox ~]$ posit-param *

Number of arguments: 82
$0 = /home/me/bin/posit-param
$1 = addresses.ldif
$2 = bin
$3 = bookmarks.html
$4 = debian-500-i386-netinst.iso
$5 = debian-500-i386-netinst.jigdo
$6 = debian-500-i386-netinst.template
$7 = debian-cd_info.tar.gz
$8 = Desktop
$9 = dirlist-bin.txt
```

在这个示例系统中，通配符 `*` 扩展为八十二个参数。我们如何处理这么多参数？Shell 提供了一种方法，尽管笨拙，可以做到这一点。`shift` 命令每次执行时都会使所有参数“向下移动一位”。事实上，通过使用 `shift`，只需一个参数（除了永远不变的 `$0`）即可：

```bash
#!/bin/bash

# posit-param2: script to display all arguments

count=1

while [[ $# -gt 0 ]]; do
    echo "Argument $count = $1"
    count=$(($count + 1))
    shift
done
```

每次执行 `shift` 时，`$2` 的值会移动到 `$1`，`$3` 的值会移动到 `$2`，依此类推。`$#` 的值也会减少一。

在 `posit-param2` 程序中，我们创建一个循环来评估剩余的参数数量，只要至少有一个参数就继续。我们显示当前参数，每次循环迭代时递增变量 `count` 以提供已处理参数的运行计数，最后执行 `shift` 以将下一个参数加载到 `$1` 中。以下是程序运行的情况：

```
[me@linuxbox ~]$ posit-param2 a b c d
Argument 1 = a
Argument 2 = b
Argument 3 = c
Argument 4 = d
```

#### 简单应用

即使没有 `shift`，也可以使用位置参数编写有用的应用程序。举例来说，这里有一个简单的文件信息程序：

```bash
#!/bin/bash

# file_info: simple file information program

PROGNAME=$(basename $0)

if [[ -e $1 ]]; then
    echo -e "\nFile Type:"
    file $1
    echo -e "\nFile Status:"
    stat $1
else
    echo "$PROGNAME: usage: $PROGNAME file" >&2
    exit 1
fi
```

该程序显示指定文件的类型（由 `file` 命令确定）和文件状态（来自 `stat` 命令）。该程序的一个有趣特性是 `PROGNAME` 变量。它被赋予 `basename $0` 命令的结果值。`basename` 命令删除路径名的前导部分，只留下文件的基名。在我们的示例中，`basename` 删除了 `$0` 参数中包含的路径名的前导部分，即我们示例程序的完整路径名。此值在构造诸如程序末尾的使用消息等消息时很有用。通过这种方式编码，脚本可以重命名，消息会自动调整为包含程序的名称。

#### 使用 Shell 函数的位置参数

正如位置参数用于向 shell 脚本传递参数一样，它们也可以用于向 shell 函数传递参数。为了演示，我们将 `file_info` 脚本转换为 shell 函数：
