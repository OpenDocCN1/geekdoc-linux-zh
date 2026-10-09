
# 结构 985

```bash
$ ./fruit2
1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon

Choose your favorite fruit from these possibilities: 3
You choose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities: 99
Invalid entry.

Choose your favorite fruit from these possibilities: 7
Thanks for playing!
```

在设置 `PS3` 提示符并使用 `select` 语句建立菜单后，`fruit2` 执行 `do` 和 `done` 之间的命令。如果用户提交了无效输入，shell 将 `varname`（`$FRUIT`）设为空值。如果 `FRUIT` 为空，`echo` 会显示错误；`continue` 让 shell 重新绘制（显示） `PS3` 提示符。如果输入是有效的，脚本将测试用户是否想要停止。如果是，`echo` 显示消息，`break` 退出 `select` 结构（并退出脚本）。如果用户显示了响应的名称和数字且不想停止，脚本将显示名称。（有关 `echo` 的 `-option` 选项的信息请参见第 98 页）。

# Here document（在此文档）

Here document 允许从 shell 内部将内容重定向到 shell 脚本。它之所以被称为 Here document，是因为它“在这里”（在 shell 脚本中可立即访问），而不是在“那里”（可能在另一个文件中）。

以下名为 `birthday` 的脚本包含一个 Here document。第一行的两个小于符号（`<<`）表示一个 Here document。界定 Here document 的一个或多个字符紧跟在小于符号之后——示例使用了加号 `+`。起始界定符必须与小于符号相邻，结束界定符必须单独一行。shell 将两个界定符之间的所有内容作为输入发送给进程。示例所示展示了你如何重定向标准输入从文件获取内容，只不过文件是嵌入在 shell 脚本中的：

```bash
$ cat birthday

grep - "1" <<

Max June 22

Barbara February 3

Darlene May 8

Helen March 13

Zach January 23

Nancy June 26

```

```bash
+ $ ./birthday Zach

Zach January 23

$ ./birthday june

Max June 22

Nancy June 26
```

# 986 第 27 章 编写 Bourne Again Shell

当你运行 `birthday` 时，它列出所有包含你调用参数的 Here 行。在这种情况下，第一次运行 `birthday` 时，它显示 `Zach` 的生日，因为它是带参数 `Zach` 被调用的。第二次运行显示 6 月的所有生日，`-i` 参数导致 `grep` 的搜索不区分大小写。

下一个名为 `bundle` 的脚本包含了对 Here document 的巧妙使用。`bundle` 脚本是一个创建 shell 归档（`tar`）文件的优雅脚本示例。该脚本创建了一个本身是 shell 脚本的文件，其中包含了其他文件以及重新创建原始文件的代码：

```bash
$ cat bundle

#!/bin/bash

# bundle: group files into distribution package

echo "To unbundle, this file"

for i in
  echo "echo i 1>&"
  echo "cat $i<<End of $i"
  cat $i
  echo "End of"
done
```

正如 shell 不会将 shell 脚本标准输入中出现的特殊字符视为特殊字符一样，shell 也不会将 Here document 中界定符之间出现的特殊字符视为特殊字符。

如下例所示，`bundle` 的输出是一个 shell 脚本，被重定向到名为 `bothfiles` 的文件。它包含了每个文件的内容。

# 文件描述符 989

```bash
*)
echo "Usage: mycp [source] [dest"
return 1
ac
```

# 调用 `cat` 命令，输入来自文件描述符 3
# 输出重定向到文件描述符 4
`cat <3 >&4`

# 关闭文件描述符 3 和 4
`exec 3<&- 4<&-`

该函数的实际工作是在以 `cat` 开头的那行完成的。脚本的其他部分负责让文件描述符 3 和 4（即 `cat` 命令的输入和输出）与适当的文件关联。

下一个程序获取命令行上的两个文件名，对它们进行排序，并将输出到临时文件。该程序将排序后的文件合并到标准输出，并在每行前加上一个数字预测它来自哪个文件。

```bash
$ cat sortmerge

#!/bin/bash

usage ()
{
if [ $#-ne 2 ]; then
echo "Usage: $0 file1 file2" 2>&1
exit 1
fi

# 默认临时目录
:TMPDIR=/tmp

# 检查参数计数
usage "$@"

# 为排序设置临时文件
file1=$TMPDIR/$file1
file2=$TMPDIR/$file2

# 排序
sort $1 > $file1
sort $2 > $file2

# 打开 $file1 和 $file2 读取。使用文件描述符 3 和 4。
exec 3<$file1
exec 4<$file2

# 读取每个文件的第一行以确定如何开始。
read Line1 <&3
status1=$?
read Line2 <&4
status2=$?

# 990 第 27 章 编写 BOURNE AGAIN SHELL

# 策略：当两个文件中都有输入时：

# 输出应该先出现的行。

# 从该行所在的文件读取新的一行。

while [ $status1 -eq 0 -a $status2 -eq 0 ]; do
    if [ "$Line2" > "$Line1" ]; then
        echo "1.\t$Line1"
        read -u3 Line1
        status1=$?
    else
        echo "2.\t$Line2"
        read -u4 Line2
        status2=$?
    fi
done

# 现在其中一个文件已到达末尾。

# 从每个文件读取到结束。

# 第一个文件1:

while [ $status1 -eq 0 ]; do
    echo "1.\t$Line1"
    read Line1 <&3
    status1=$?
done

# 下一个文件2:

while [[ $status2 -eq 0 ]]; do
    echo "2.\t$Line2"
    read Line2 <&4
    status2=$?
done

# 关闭并删除两个输入文件

exec 3<&- 4<&-

rm -f $file1 $file2

exit 0
```

# 参数与变量

Shell 参数和变量在第 312 页介绍。本节对之前的内容进行了补充，讨论了数组变量、全局与局部变量、特殊和位置参数，以及空和未设置变量的扩展。

## 数组变量

Bourne Again Shell 支持一维数组变量。下标是基于 0 索引的整数（即数组的第一个元素下标为 0）。以下格式声明并为数组赋值：

```bash
# name=(element1 element2 ...)
```

以下示例为 `NAMES` 数组分配了四个值：

```bash
$ NAMES=(max helen sam zach)
```

通过如下方式引用数组的单个元素：

```bash
$ echo ${NAMES[2]}
sam
```

下标 `[*]` 和 `[@]` 都可以提取整个数组，但在配合双引号时工作方式不同。`*` 会产生一个与原始数组相同的数组；`@` 会产生一个数组元素（或普通变量），该元素包含了用 `IFS` 中的第一个字符（通常是空格）分隔的数组所有元素。在这个示例中，数组 `A` 使用 `*` 填充 `NAMES` 变量的元素填充，而 `B` 使用 `@` 填充。带有 `-a` 选项的内置命令 `declare` 用于显示数组的值（并提醒你 `bash` 对数组使用基于 0 的索引）：

```bash
$ A=("NAMES[*]}")
$ B=("NAMES[@]}")

declare -a A='[0]="max helen sam zach"'

declare -a B='[0]="max" [1]="helen" [2]="sam" [3]="zach"'

declare -a NAMES='[0]="max" [1]="helen" [2]="sam" [3]="zach"'
```

从 `declare` 的输出中，可以看到 `NAMES` 和 `B` 有多个元素。相比之下，在双引号内使用 `*` 赋值赋值的 `A` 只有一个元素：`A` 的所有元素都被包含在双引号之间。

在下一个示例中，`echo` 尝试显示数组 `A` 的元素 1。什么都没有被显示，因为 `A` 只有一个元素，且该元素的索引为 0。`A` 的元素 0 拥有所有四个名字。`B` 的元素 1 拥有数组中的第二个元素，元素 0 拥有第一个项。

```bash
$ echo ${A[1]}
$ echo ${A[0]}
max helen sam zach

$ echo ${B[1]}
helen

$ echo ${B[0]}
max
```

你可以对数组变量应用 `${#name[*]}` 运算符，它返回数组中的元素数量：

```bash
$ echo ${#NAMES[*]}
4
```

`subtest` 脚本从未接收到来自 `extent1` 的 `cheese` 的值，而 `extent1` 也永远不会丢失该值。在 `bash` 中——与现实世界不同——子进程无法影响其父进程的属性。当进程尝试显示一个未声明的变量的值时（如 `subtest` 所示），该进程什么都不显示；未声明变量的值为空字符串。

下面的 `test2` 脚本与 `test1` 相同，但它使用 `export` 让 `subtest` 脚本可以使用 `cheese` ：

```bash
$ catstest2

export cheese=american

echo "extest2 1: $cheese"

subtest

echo "extest2 2: $cheese"

./extest2

extest2 1: american

subtest 1: american

subtest 2: swiss

extest2 2: american
```

在这里，子进程继承了 `cheese` 为 `american` 的值，并在显示此值后，将其副本更改为 `swiss`。当控制权返回给父进程时，父进程的副本保持不变。

`export` 内置命令可以可选包含一个赋值：

```bash
export cheese=american
```

上述语句等同于以下两条命令：

```bash
cheese=american

export
```

## 函数

由于函数在调用它们的 Shell 相同的环境中运行，变量是隐式共享的。

```bash
$ name () {
    echo $myname
    myname=zach
}
```

```bash
$ myname=sam
$ name
sam

$ echo myname
zach
```

在上一个示例中，`myname` 变量被设置为 `sam`。`name` 函数随后显示该值并将 `myname` 设置为 `zach`。最后的 `echo` 显示在交互式 Shell 中，`myname` 的值已经被更改。

由于函数可能被不同程序员编写的许多脚本调用，你需要确保函数内部使用的变量名称不会与调用它的程序中的名称冲突（即重复）。局部变量消除了这个问题。在函数内部使用 `typeset` 内置命令可以将变量声明为局部。

下一个示例展示了在函数中使用局部变量。它包含两个名为 `count` 的变量。第一个在活动 Shell 中声明并赋值为 10。在运行 `count_down` 后，`echo` 验证了它的值从未改变。另一个 `count` 使用 `typeset` 声明为局部。它的值在函数外部不可知的，范围从 4 到 1。

该示例显示了从键盘输入的函数；它不是一个脚本。见提示页 988。

```bash
$ count_down () {
  typeset count
  count=$1
  while [ $count -gt 0 ]
  do
    echo "$count..."
    $((count=count-1))
    sleep 1
  done
  echo "Blast Off."
}

$ count=10
$ count_down 4

4...

3...

2...

1...

Blast Off.

$ echo count
10
```

`((count=count-1))` 赋值被包含在双括号之间，这会导致 Shell 执行算术评估（第 1016 页）。在双括号内，你可以引用 Shell 变量无需加前面的美元符号 (`$`)。

# 参数与变量 995

## PID 号

`shell` 使用 `$$` 参数存储正在执行的进程的 PID 号。在接下来的交互中，`echo` 显示此变量的值，`ps` 工具则确认了该值。两个命令都显示 shell 的 PID 号为 5209：

```bash
$ echo $$
5209

$ ps
PID TTY      TIME CMD
5209 pts/1   00:00:00 bash
6015 pts/1   00:00:00 ps
```

由于 `echo` 是 shell 的内置命令，当你提供 `echo` 命令时，shell 不会创建另一个进程。然而，无论 `echo` 是否为内置，结果都是相同的，因为 shell 在派生进程运行命令之前会替换 `$$` 的值。使用由另一个进程运行的 `echo` (`/bin/echo`) 会发生什么呢？在下面的示例中，shell 替换了 `$$` 的值，并将该值作为文件名前缀传递给 `cp`：

```bash
$ echo $$
8232

$ cp memo $$$.memo

$ ls
8232.memo memo
```

在文件名中包含 PID 号对于在名称含义不明时创建唯一文件名非常有用；这种技术经常用于 shell 脚本中创建临时文件的名称。当两个人在运行同一个 shell 脚本时，拥有唯一的文件名可以防止用户无意中共享同一个临时文件。

下面的示例演示了 shell 在运行脚本时会创建一个新进程。`id2` 显示了正在运行的进程的 PID 号（而不是它所调用的进程——`$$` 的替换是由派生来运行 `id2` 的 shell 完成的）：

```bash
$ cat id2
echo "$0 PID= $$"

$ echo $$
8232

$ id2
./id2 PID= 8366

$ echo $$
8232
```

第一个 `echo` 显示交互式 shell 的 PID 号。然后 `id2` 显示了它的名称 (`$0`) 以及它正在运行的子 shell 的 PID 号。最后一个 `echo` 显示交互式 shell 的 PID 号没有变化。

# 996 第 27 章 编写 Bourne Again Shell

`shell` 使用 `$!` 存储最后一个在后台运行的进程的 PID 号。下面的示例将 `sleep` 执行为后台任务，并使用 `echo` 显示 `$!` 的值：

```bash
$ sleep 60 &
[1] 8376

$ echo $!
8376
```

## $?: 退出状态

当进程因任何原因停止执行时，它会向父进程返回一个退出状态。退出状态也被称为状态码或返回码。`$?` 变量存储上一个命令的退出状态。

按照惯例，非零退出状态表示假值，意味着命令执行失败。在下面的示例中，第一个命令成功，第二个命令失败，如退出状态所示：

```bash
$ ls es
es

$ echo $?
0

$ ls xxx
ls: xxx: No file or directory

$ echo $?
1
```

你可以通过使用 `exit` 内置命令后跟一个数字来指定 shell 脚本返回的退出状态并终止脚本。如果你不使用带数字的 `exit` 来终止脚本，脚本的退出状态就是脚本运行的最后一个命令的退出状态。

```bash
$ cat es
echo This program returns an exit status of 7.

exit 7

$ es
This program returns an exit status of 7.

$ echo $?
7

$ echo $?
0
```

`shell` 脚本显示一条消息并使用 `exit` 命令终止执行，该命令返回退出状态 7，这是脚本中用户定义的退出状态。第一个 `echo` 显示了 `es` 的退出状态值。第二个显示第一个 `echo` 的退出状态值。该值是 0，表示第一个 `echo` 执行成功。

## 位置参数

位置参数包括命令名和命令行参数。这些参数被称为位置参数，是因为在 shell 脚本中，你通过它们在命令行上的位置来引用它们。只有 `set` 内置命令（见第 998 页）允许你更改位置参数的值。然而，你无法从脚本内部更改命令名的值。

## $#: 命令行参数个数

`$#` 参数持有命令行上参数（位置参数）的数量，不包括命令本身：

```bash
$ cat num_args
```
