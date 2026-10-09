

## bash 与 -bash

**提示** 在某些系统上，`echo $0` 显示为 `-bash`，而在其他系统上则显示为 `bash`。前者表示登录 shell（第 330 页）；后者表示非登录 shell。在图形用户界面环境中，某些终端模拟器启动的是登录 shell，而另一些则不是。

## $1 – $n：位置参数

Shell 将 `$1` 展开为命令行上的第一个参数，将 `$2` 展开为第二个参数，依此类推直到 `$n`。这些参数是 `${1}, ${2}, ${3},` 等的简写形式。当 *n* 的值小于或等于 9 时，花括号是可选的。当 *n* 的值大于 9 时，数字必须包含在花括号内。例如，第十二个位置参数表示为 `${12}`。以下脚本显示持有命令行参数的位置参数：

```text
$ cat display_5args
echo First 5 arguments are $1 $2 $3 $4 $5

$ ./display_5args zach max helen
First 5 arguments are zach max helen
```

`display_5args` 脚本显示前五个命令行参数。Shell 将代表命令行上不存在的每个参数展开为空字符串。因此，在此示例中 `$4` 和 `$5` 参数的值为空。

## 始终为位置参数加引号

> **注意** 如果你不为位置参数加引号，你可能会“丢失”位置参数。请参阅下文中的示例。

在双引号内包含对位置参数的引用。当你将位置参数用作命令的参数时，引号尤为重要。如果没有双引号，未设置或具有空值的位置参数将消失：

```text
$ cat showargs
echo "$0 was called with $# arguments, the first is :$1:"

$ ./showargs a b c
./showargs was called with 3 arguments, the first is :a:

$ echo $xx

$ ./showargs $xx a b c
./showargs was called with 3 arguments, the first is :a:

$ ./showargs "$xx" a b c
./showargs was called with 4 arguments, the first is :::
```

`showargs` 脚本显示其被调用时接收到的参数数量（`$#`），后跟第一个参数值（用冒号包围）。在上面的示例中，`showargs` 最初被调用时带有三个参数。接下来，`echo` 命令显示 $xx 变量（未设置）具有空值。$xx 变量是第二个和第三个 `showargs` 命令的第一个参数；它在第二个命令中未加引号，而在第三个命令中使用双引号引用。在第二个 `showargs` 命令中，Shell 将参数展开为 a b c 并传递三个参数给 `showargs`。在第三个 `showargs` 命令中，Shell 将参数展开为 " a b c，这导致以四个参数调用 `showargs`。这两次对 `showargs` 的调用的差异说明了使用可能未设置或可能具有空值的位置参数时的一个细微潜在问题。

## LP1 set：初始化位置参数

当你使用一个或多个参数调用 `set` 内建命令时，它将参数的值分配给位置参数，从 $1 开始。以下脚本使用 `set` 将值分配给位置参数 $1、$2 和 $3：

```text
$ cat set_it
set this is it
echo $3 $2 $1
$ ./set_it
it is this
```

`set` 命令行上的单个连字符（-）标记选项的结束和 Shell 分配给位置参数的值的开始。`--` 还会关闭 `xtrace` (-x) 和 `verbose` (-v) 选项（第 401 页的表 9-13）。以下 `set` 命令打开 `posix` 模式，并设置前两个位置参数，如 `echo` 命令所示：

```text
$ set -o posix - first.param second.param
$ echo $*
first.param second.param
```

`set` 命令行上的双连字符（--）如果没有后续参数，则取消设置位置参数；如果跟随参数，则设置位置参数，包括那些以连字符（-）开头的参数。

```text
$ set --
$ echo $*
$
```

将命令替换（第 410 页）与 `set` 内建命令结合使用，是一种方便的方式来改变命令的标准输出，使其能够以易于在 Shell 脚本中操作的形式呈现。以下脚本展示了如何使用 `date` 和 `set` 提供有用格式的日期。第一个命令显示 `date` 的输出。然后 `cat` 显示 `dateset` 脚本的内容。该脚本中的第一个命令使用命令替换将位置参数设置为 `date` 实用程序的输出。下一个命令 `echo $*` 显示由前一个 `set` 产生的所有位置参数。后续命令显示 $1、$2、$3 和 $6 的值。最后一个命令以你可以用于信件或报告的格式显示日期。

```sh
$ date
Wed Aug 15 17:35:29 PDT 2012
$ cat dateset
set $(date)
echo $*
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 6: $6"
echo
echo "$2 $3, $6"

$ ./dateset
Wed Aug 15 17:35:34 PDT 2012

Argument 1: Wed
Argument 2: Aug
Argument 3: 15
Argument 6: 2012

Aug 15, 2012
```

你还可以使用 date 的 +format 参数来指定其输出的内容和格式。

在没有参数时调用，set 显示已设置的 Shell 变量列表，包括用户创建的变量和关键字变量。在 bash 下，此列表与不带任何参数调用 declare（第 357 页）时显示的列表相同。

```bash
$ set
BASH_VERSION='4.2.24(1)-release'
COLORS=/etc/DIR_COLORS
COLUMNS=89
LESSOPEN=" | /usr/bin/lesspipe.sh %s"
LINES=53
LOGNAME=sam
MAIL=/var/spool/mail/sam
MAILCHECK=60
...
```

set 内建命令还可以执行其他任务。欲了解更多信息，请参阅第 1036 页的“set：与 Shell 功能、位置参数和变量协同工作”。

## shift：提升位置参数

shift 内建命令提升每个位置参数。第一个参数（原来由 $1 表示）被丢弃。第二个参数（原来由 $2 表示）变成第一个参数（现在是 $1），第三个参数变成第二个，依此类推。由于不存在“unshift”命令，你无法找回已丢弃的参数。shift 的一个可选参数指定要移动的位置数（以及要丢弃的参数数）；默认值为 1。

以下 demo_shift 脚本被调用时带有三个参数。echo 参数周围的双引号保留了输出的空格，但允许 Shell 展开变量。该程序显示参数并反复移动它们，直到没有参数可移动为止。

```text
$ cat demo_shift
echo "$arg1= $1    arg2= $2    arg3= $3"
shift
echo "$arg1= $1    arg2= $2    arg3= $3"
shift
echo "$arg1= $1    arg2= $2    arg3= $3"
shift
echo "$arg1= $1    arg2= $2    arg3= $3"
shift
```

```text
$ ./demo_shift alice helen zach
arg1= alice    arg2= helen    arg3= zach
arg1= helen    arg2= zach     arg3=
arg1= zach     arg2=          arg3=
arg1=          arg2=          arg3=
```

反复使用 shift 是一种在 Shell 脚本中对所有命令行参数进行循环的便捷方法，适用于预期具有任意数量参数的 Shell 脚本。请参阅第 989 页中一个使用 shift 的 Shell 脚本。

## $* AND $@：展开为所有位置参数

Shell 将 $* 参数展开为所有位置参数，如 display_all 程序所示：

```text
$ cat display_all
echo "All arguments are $*"
```

```text
$ ./display_all a b c d e f g h i j k l m n o p
All arguments are a b c d e f g h i j k l m n o p
```

## "$*" 与 "$@"

$* 和 $@ 参数的工作方式相同，除非它们被包含在双引号内。使用 "$*" 会产生一个单一参数，其中 IFS 的第一个字符（第 363 页；通常是空格）位于位置参数之间。使用 "$@" 会生成一个列表，其中每个位置参数都是一个独立的参数。这种差异通常使得在 Shell 脚本中 "$@" 比 "$*" 更有用。

以下脚本有助于解释这两个参数之间的区别。在两个脚本的第二行中，单引号阻止 Shell 解释封闭的特殊字符，允许 Shell 将它们传递给 echo，以便 echo 可以显示它们。bbl 脚本表明 set "$*" 将多个参数分配给第一个命令行参数。

