

如果这看起来真的很让人困惑，别太焦虑。事实上，这一切确实非常复杂，所以我们来看一个例子，让你明白 getopts 是如何工作的。假设你正在为一个脚本编写代码，想要使用 getopts 来识别选项 -a、-i 和 -r。你的 getopts 调用可能如下所示：

```sh
getopts "air" option
```

在这里，第一个参数——air——指定了三个可接受的命令标志（-a、-i 和 -r），而 option 是 getopts 将用来存储遇到的每个匹配值的变量名。

getopts 命令还允许选项在命令行中组合或合并在一起。做法是在一个减号后面紧跟多个连续选项。例如，我们的 foo 命令可以这样执行：

```sh
foo -a -r -i
```

或者这样：

```sh
foo -ari
```

利用这个简单的分组功能。

但是等等，getopts 远比我们目前所解释的要强大得多！例如，它还能处理选项需要额外参数的情况。例如，将要添加到 waitfor 命令中的新 -t 选项也需要一个参数。

为了正确解析用户指定选项之后的参数，getopts 要求命令行中选项与参数之间至少用一个空格分隔。在这种情况下，选项不能组合在一起。

要向 getopts 指示某个选项带有必需参数，需要在 getopts 命令行中的选项字母后添加一个冒号字符。因此，waitfor 程序允许 -m 和 -t 两个选项，其中后者带有必需的附加参数，它应该像这样调用 getopts：

```sh
getopts mt: option
```

如果 getopts 在需要参数的选项后面没有找到参数，它会在变量中存储一个问号，并向标准错误输出一条错误消息。否则，它会把该字符存储在变量中，把用户指定的参数存储在一个名为 OPTARG 的特殊变量中。

关于 getopts 的最后一点说明：另一个名为 OPTIND 的特殊变量会被初始设置为 1，并且每次 getopts 返回时都会更新，以反映下一个待处理命令行参数的编号。

为了更清楚地说明这一点，下面是 waitfor 的第三个版本，它使用 getopts 命令来处理命令行参数。该版本还包含了前面提到的修改，即向运行程序的用户发送邮件。

```sh
$ cat waitfor
#
# Wait until a specified user logs on -- version 3
#
# Set up default values

mailopt=FALSE
interval=60

# process command options

while getopts mt: option
do
        case "$option"
        in
                m) mailopt=TRUE;;
                t) interval=$OPTARG;;
                \?) echo "Usage: waitfor [-m] [-t n] user"
                    echo "    -m means to be informed by mail"
                    echo "    -t means check every n secs."
                    exit 1;;
        esac
done

# Make sure a user name was specified

if [ "$OPTIND" -gt "$#" ]
then
        echo "Missing user name!"
        exit 2
fi

shiftcount=$((OPTIND - 1))
shift $shiftcount
user=$1

#
# Check for user logging on
#

until who | grep "^$user " > /dev/null
do
        sleep $interval
done

#
# When we reach this point, the user has logged on
#
if [ "$mailopt" = FALSE ]
then
        echo "$user has logged on"
else
        runner=$(who am i | cut -c1-8)
        echo "$user has logged on" | mail $runner
fi
```

```sh
$ waitfor -m
Missing user name!
$ waitfor -x fred                    Illegal option
waitfor: Illegal option -- x
Usage: waitfor [-m] [-t n] user
    -m means to be informed by mail
    -t means check every n secs.
$ waitfor -m -t 600 ann &
[1] 5792
$
```

每 10 分钟检查一次 ann。

让我们更仔细地看看最后一行。当执行

```sh
waitfor -m -t 600 ann &
```

时，while 循环内会发生以下过程：getopts 被调用，将字符 m 存储在变量 option 中，将 OPTIND 设置为 2，并返回一个零退出状态。

然后，case 命令会判断 option 中存储的内容。与字符 m 匹配表示选择了“发送邮件”选项，因此 mailopt 被设置为 TRUE。（注意，case 中的 ? 是被引号括起来的。这是为了消除它在 shell 中作为模式匹配字符的特殊含义。）

第二次执行 getopts 时，getopts 将字符 t 存储在 option 中，将下一个命令行参数 (600) 存储在 OPTARG 中，将 OPTIND 设置为 3，并返回一个零退出状态。然后，case 命令会匹配存储在 option 中的字符 t。随后，与该 case 关联的代码会将存储在 OPTARG 中的值 600 复制到变量 interval 中。

第三次执行 getopts 时，getopts 返回一个非零退出状态，表示已到达用户指定命令选项的末尾。

然后，程序会将 OPTIND 的值与 $# 进行比较，以确保命令行中键入了用户名。如果 OPTIND 大于 $#，则说明不再有其他参数，用户忘了输入用户名参数。否则，使用 shift 命令将用户名参数移动到 $1 中。实际需要移动的位置数比 OPTIND 的值少 1。

waitfor 程序的其余部分保持不变；唯一的更改是使用 `interval` 变量来指定睡眠的秒数。

如果你对 `getopts` 及其用法感到有点晕头转向，别担心，它会在后续的 shell 程序中不断出现，多接触一些你就能掌握它。它也很值得为高级 shell 编程而研究，因为否则的话，手动解析任何不止一个命令标志的内容都会极其低效。

## 读取和打印数据

在本章中，你将学习如何使用 read 命令从终端或文件读取数据，以及如何使用 printf 命令将格式化数据写入标准输出。

### `read` 命令

read 命令的一般格式是

```sh
read variables
```

当此命令执行时，shell 会从标准输入读取一行，并将第一个单词赋给 `variables` 中列出的第一个变量，将第二个单词赋给第二个变量，依此类推。如果行中的单词数多于列出的变量数，多余的单词会赋给最后一个变量。例如，命令

```sh
read x y
```

会从标准输入读取一行，将第一个单词存储到变量 x 中，将行的其余部分存储到变量 y 中。由此可知，命令

```sh
read text
```

会读取一整行并存储到 shell 变量 text 中。

### 一个复制文件的程序

让我们编写一个简化版的 cp 命令，让 read 命令派上用场。我们把它命名为 mycp，并让它接受两个参数：源文件和目标文件。如果目标文件已经存在，程序会警告用户，并询问他们是否要继续复制。如果回答是“是”，我们就继续；否则程序将退出。

```sh
$ cat mycp
#
# Copy a file
#
if [ "$#" -ne 2 ] ; then
    echo "Usage: mycp from to"
    exit 1
fi

from="$1"
to="$2"

#
# See if the destination file already exists
#

if [ -e "$to" ] ; then
    echo "$to already exists; overwrite (yes/no)?"
    read answer

    if [ "$answer" != yes ] ; then
        echo "Copy not performed"
        exit 0
    fi
fi

#
# Either destination doesn't exist or "yes" was typed
#

cp $from $to      # proceed with the copy
$
```

现在让我们快速测试一下这个程序：

```sh
$ ls -C                         What files? -C forces multicolumn output too
Addresses       intro       lotsaspaces      mycp
names           nu          numbers          phonebook
stat
$ mycp                          No arguments
Usage: mycp from to
$ mycp names names2              Make a copy of names
$ ls -l names*                   Did it work?
-rw-r--r--  1 steve  steve      43 Jul 20 11:12 names
-rw-r--r--  1 steve  steve      43 Jul 21 14:14 names2
$ mycp names numbers             Try to overwrite an existing file
numbers already exists; overwrite (yes/no)?
no
Copy not performed
$
```

