
出现在命令行上。因此，在此示例中，$4 和 $5 参数的值为空。

## shift：提升命令行参数

shift 内建命令会提升每个命令行参数。第一个参数（即原 $1）被丢弃。第二个参数（即原 $2）变为第一个参数（现为 $1），第三个参数变为第二个，依此类推。由于不存在“unshift”命令，因此无法恢复已被丢弃的参数。shift 命令的一个可选参数指定要移动的位数（即要丢弃的参数数量）；默认值为 1。

以下 demo_shift 脚本以三个参数调用。围绕 echo 命令参数的双引号保留了输出的间距。该程序显示参数，并反复进行移位操作，直到没有更多参数可移为止：

```
$ cat demo_shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
$ ./demo_shift alice helen zach
arg1= alice\targ2= helen\targ3= zach
arg1= helen\targ2= zach\targ3=
arg1= zach\targ2=\targ3=
arg1=\targ2=\targ3=
```

反复使用 shift 是循环遍历 shell 脚本中所有命令行参数的便捷方式，适用于期望任意数量参数的脚本。有关使用 shift 的 shell 脚本，请参阅第 959 页。

## set：初始化命令行参数

当你调用带有 1 个或多个参数的 set 内建命令时，它会将这些参数的值分配给位置参数，从 $1 开始。以下脚本使用 set 为位置参数 $1、$2 和 $3 赋值：

```
$ cat set_it
set this is it
echo $3 $2 $1
$ ./set_it
it is this
```

将命令替换（第 362 页）与 set 内建命令结合使用，是一种获取命令标准输出的便捷方式，这种形式易于在 shell 脚本中操作。以下脚本展示了如何使用 date 和 set 以有用的格式提供日期。第一条命令显示 date 的输出。然后 cat 显示 dataset 脚本的内容。此脚本中的第一条命令使用命令替换将位置参数设置为 date 实用程序的输出。下一条命令，**echo $***，显示上一条 set 命令生成的所有位置参数。后续命令显示参数 $1、$2、$3 和 $6 的值。最后一项命令以可用于信函或报告中的格式显示日期：

```
$ date
Wed Aug 14 17:35:29 PDT 2010
$ cat dataset
set $(date)
echo $*
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 6: $6"
echo "Aug $2, $6"
$ ./dataset
Wed Aug 14 17:35:34 PDT 2010

Argument 1: Wed
Argument 2: Aug
Argument 3: 14
Argument 6: 2010

Aug 14, 2010
```

你还可以使用 date 命令的 **+format** 参数来修改其输出格式。在不带任何参数调用的情况下，set 会显示已设置的 shell 变量列表，包括用户创建的变量和关键字变量。在 bash 中，此列表与不带任何参数调用的 declare 和 type set 所显示的列表相同。

set 内建命令还接受选项，允许你自定义 shell 的行为。更多信息请参阅第 353 页的“set +o：开启和关闭 shell 功能”。

## $* 和 $@：表示所有命令行参数

$* 参数表示所有命令行参数，如下面的 display_all 程序所示：

```
$ cat display_all
echo 'All arguments are $*'

$ ./display_all a b c d e f g h i j k l m n o p
All arguments are a b c d e f g h i j k l m n o p
```

将位置参数的引用包裹在双引号中是个好习惯。当将位置参数用作命令的参数时，双引号尤为重要。如果没有双引号，未设置或值为空的位置参数将会消失：

```
$ cat showargs
echo "$0 was called with $# arguments, the first is :$1:"

$ ./showargs a b c
./showargs was called with 3 arguments, the first is :a:.
$ echo $xx

$ ./showargs $xx a b c
./showargs was called with 3 arguments, the first is :a:.
$ "./showargs "$xx" a b c
./showargs was called with 4 arguments, the first is : :.
```

**showargs** 脚本显示参数数量（**$#**），随后显示第一个参数的值，该值被冒号包围。在上一个示例中，**showargs** 最初以三个简单参数调用。接下来，`echo` 命令演示了未设置的 `$xx` 变量具有空值。在针对 **showargs** 的最后两次调用中，第一个参数是 `$xx`。在第一种情况下，命令行变为 `showargs a b c`；shell 将**三个**参数传递给 **showargs**。在第二种情况下，命令行变为 `showargs "" a b c`，这导致以四个参数调用 **showargs**。这两次调用 **showargs** 之间的差异说明了使用可能未设置或具有空值的位置参数时应牢记的一个潜在细微问题。

### "“*” 与 "$@"

**$*** 和 **$@** 参数的工作方式相同，除非它们被双引号包围。使用 "$*" 会产生单个参数（位置参数之间带有**空格**或 `IFS` 的第一个字符的值 [第 323 页]），而使用 "$@" 则生成一个列表，其中每个位置参数都是独立的参数。这种区别通常使得在 shell 脚本中 "$@" 比 "$*" 更有用。

以下脚本有助于解释这两个特殊参数之间的区别。在这两个脚本的第二行中，单引号阻止 shell 解析其中的特殊字符，因此这些字符被传递给 `echo` 并原样显示。`bb1` 脚本表明 set "$*" 将多个参数分配给第一个命令行参数：

```
$ cat bb1
set "$*"
echo $# parameters with '"$*"'
echo 1: $1
echo 2: $2
echo 3: $3
$ ./bb1 a b c
1 parameters with "$*"
1: a b c
2:
3:
```

**bb2** 脚本表明 set "$@" 将每个参数分配到不同的命令行参数：

```
$ cat bb2
set "$@"
echo $# parameters with "$@" 
echo 1: $1
echo 2: $2
echo 3: $3

$ ./bb2 a b c
3 parameters with "$@" 
1: a
2: b
3: c
```

## 扩展空变量和未设置变量

表达式 \$[name]（如果不存在歧义，也可以只写 \$name）扩展为 *name* 变量的值。如果 *name* 为空或未设置，*bash* 将 \$[name] 扩展为空字符串。*Bourne Again Shell* 提供了以下替代方案，以接受扩展后的空字符串作为变量的值：

- 使用变量的默认值。
- 使用默认值，并将该值分配给变量。
- 显示错误。

你可以通过在变量名称中使用修饰符来选择这些替代方案之一。此外，你可以使用 `set -o nounset`（第 355 页），使得每当引用未设置的变量时，*bash* 显示错误并退出脚本。

### :− 使用默认值

`:-` 修饰符使用默认值替代空或未设置的变量，同时允许非空变量代表其自身：

```
$[name:-default]
```

shell 将 `:-` 解释为“如果 *name* 为空或未设置，则扩展 *default* 并在使用 *name* 的位置使用扩展后的值；否则使用 *name*”。以下命令列出由 `LIT` 变量指定的目录的内容。如果 `LIT` 为空或未设置，则列出 /home/max/literature 的内容：

```
$ ls ${LIT:-/home/max/literature}
```

默认值本身可以包含会被扩展的变量引用：

```
$ ls ${LIT:-$HOME/literature}
```

### := 分配默认值

`:=` 修饰符不会改变变量的值。然而，你可以使用 `:=` 修饰符在脚本中将空或未设置变量的值更改为其默认值：

```
$[name:=default]
```

shell 以与扩展 `$(name:-default)` 相同的方式扩展表达式 `$(name:=default)`，但还将 `name` 的值设置为 `default` 的扩展值。如果脚本包含如下所示的行，且在执行该行时 `LIT` 未设置或为空，则 `LIT` 被赋值为 `/home/max/literature`：

```
$ ls ${LIT:=/home/max/literature}
```

### :（null）内建命令

Shell 脚本通常以 `:`（null）内建命令开头，并在同一行后跟 `:=` 扩展修饰符，以设置可能为空或未设置的变量。`:` 内建命令评估命令其余部分的每个标记，但不执行任何命令。如果没有开头的冒号（`:`），shell 将评估并尝试执行由评估产生的“命令”。

在 shell 脚本中为空或未设置变量设置默认值时，使用以下语法（第一个冒号后跟一个 `SPACE`）：

```
: ${name:=default}
```

当脚本需要目录用于临时文件，并使用 `TMPDIR` 的值作为该目录的名称时，如果 `TMPDIR` 为空，则以下行将 `TMPDIR` 赋值为 `/tmp`：

```
: ${TMPDIR:=/tmp}
```

### :? 显示错误消息

有时脚本需要某个变量的值，但你在编写脚本时无法提供合理的默认值。如果该变量为空或未设置，`:?` 修饰符会导致脚本显示错误消息并以 `1` 的退出状态终止：

```
${name:?message}
```

如果省略 `message`，shell 将显示默认错误消息（**parameter null or not set**）。在使用 `:?` 时，交互式 shell 不会退出。在以下命令中，`TESTDIR` 未设置，因此 shell 在标准错误输出中显示 `:?` 后字符串的扩展值。在这种情况下，该字符串包括带有 `%T` 格式的 date 命令替换，后跟字符串 **error, variable not set.**。

```
cd ${TESTDIR:?$(date +%T) error, variable not set.}  
bash: TESTDIR: 16:16:14 error, variable not set.
```

## 内建命令

在 `Chapter 7` 中介绍的内建命令，在执行时不会创建新进程。本节讨论 `type`、`read`、`exec`、`trap`、`kill` 和 `getopts` 内建命令。第 1015 页的表 27-6 列出了许多 bash 内建命令。

