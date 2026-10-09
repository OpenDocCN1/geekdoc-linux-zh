
在未指定命令行的情况下调用 `env` 时，它会显示环境变量列表（其行为类似于 `printenv`（第 1034 页））：

```
$ env
 ...
SHELL=/bin/bash
TERM=xterm
USER=sam
PWD=/home/sam
y=10
 ...
```

## set：用于处理 shell 特性、位置参数和变量

`set` 内建命令可以执行以下任务：

- 设置或取消 shell 特性（也称为属性；第 400 页）。
- 为位置参数赋值（第 1024 页）。
- 显示当前 shell 可用的变量。这些变量包括 shell 变量（不在环境变量中的变量）和环境变量。`set` 内建命令会以一种格式显示变量，你可以将该格式用于 shell 脚本，或作为输入传递给 `set` 以声明和初始化变量。输出基于当前区域设置进行排序（第 368 页）。你无法重置只读变量。

```
$ set
 ... 
BASH=/bin/bash
COLUMNS=70
PWD=/home/sam
SHELL=/bin/bash
x=5
y=10
 ...
```

## 扩展空变量和未设置变量

表达式 `${name}`（如果没有歧义，也可以仅写为 `$name`）将扩展为**name** 变量的值。如果**name** 为空或未设置，`bash` 会将 `${name}` 扩展为空字符串。Bourne Again Shell 提供了以下几种替代方法，以避免接受空字符串作为变量的值：

- 使用变量的默认值。
- 使用默认值并将该值赋给变量。
- 显示错误。

你可以使用修饰符配合变量名来选择其中一种替代方法。此外，你可以使用 `set -o nounset`（第 402 页）使得当脚本引用未设置变量时，`bash` 显示错误消息并退出脚本。

### ：- 使用默认值

`:-` 修饰符使用默认值来替代空或未设置的变量，同时允许非空变量表示自身：

`$name:-default`

Shell 将 `:-` 解释为：“如果 *name* 为空或未设置，则扩展 *default* 并使用扩展后的值替代 *name*；否则使用 *name*。”

以下命令列出由 LIT 变量指定的目录的内容。如果 LIT 为空或未设置，它将列出 /home/max/literature 的内容：

```
$ ls ${LIT:-/home/max/literature}
```

Shell 会扩展 *default* 中的变量：

```
$ ls ${LIT:-$HOME/literature}
```

### := 分配默认值

`:=` 修饰符本身不会改变变量的值。然而，通过使用 `:=` 修饰符，你可以将一个空或未设置变量的值更改为 *default* 的扩展值：

`$name:=default`

Shell 扩展表达式 `$name:=default` 的方式与扩展 `$name:-default` 相同，但还会将 *name* 的值设置为 *default* 的扩展值。

如果脚本包含如下一行，且在执行该行时 LIT 未设置或为空，则 Shell 会将 LIT 的值设置为 /home/max/literature：

```
$ ls ${LIT:=/home/max/literature}
```

### : (null) 内建命令

某些 shell 脚本包含以 `:`（null）内建命令开头的行，并在同一行后跟 `:=` 扩展修饰符。这种语法用于设置那些为空或未设置的变量。`:` 内建命令评估命令行剩余部分的每个标记，但不执行任何命令。

使用以下语法在 shell 脚本中为为空或未设置的变量设置默认值（第一个冒号后面跟随一个 *空格*）。如果没有开头的冒号（:），Shell 将评估并尝试执行由评估结果生成的“命令”。

```
: $name:=default
```

当脚本需要一个目录用于临时文件，并使用 *TEMPDIR* 的值作为该目录的名称时，如果 *TEMPDIR* 为空，以下行将 /tmp 分配给 *TEMPDIR*：

```
: ${TEMPDIR:=/tmp}
```

### :? 向标准错误发送错误消息

有时脚本需要某个变量的值，但在编写脚本时无法提供合理的默认值。在这种情况下，你希望如果变量未设置，脚本应退出。如果变量为空或未设置，`:?` 修饰符会导致脚本向标准错误发送错误消息，并以退出状态 1 终止。交互式 Shell 在使用 `:?` 时不会退出。

`${name:?message}`

如果省略 *message*，Shell 将显示**参数为空或未设置**。在以下命令中，`TESTDIR` 未设置，因此 Shell 将 `:?` 之后字符串的扩展值发送到标准错误。在这种情况下，该字符串包含使用 %T 语法的 `date` 命令替换，随后是字符串 *error, variable not set*。

```
$ cd ${TESTDIR:?"$(date +%T) error, variable not set."}
bash: TESTDIR: 16:16:14 error, variable not set.
```

## 数组变量

Bourne Again Shell 支持一维数组变量。下标是整数，采用零基索引（即，数组的第一个元素的下标为 0）。以下语法用于声明数组并为其赋值：

`name=(element1 element2 ...)`

以下示例为数组 `NAMES` 分配四个值：

```
$ NAMES=(max helen sam zach)
```

按如下方式引用数组的单个元素；花括号不可省略：

```
$ echo ${NAMES[2]}
sam
```

下标 `[*]` 和 `[@]` 都提取整个数组，但在双引号内使用时表现不同。`@` 产生原始数组的副本；而 `*` 产生数组（或普通变量）的一个元素，该元素包含由 `IFS`（通常是 SPACE，第 363 页）中的第一个字符分隔的所有数组元素。在以下示例中，使用 `*` 将 `NAMES` 变量的元素填充到数组 `A` 中，并使用 `@` 填充 `B`。带有 `-a` 选项的 `declare` 内建命令（第 357 页）显示数组的值（并提醒你对数组使用零基索引）：

```
$ A=("${NAMES[*]}")
$ B=("${NAMES[@]}")

$ declare -a
declare -a A=([0]="max helen sam zach")
declare -a B=([0]="max" [1]="helen" [2]="sam" [3]="zach")
...
declare -a NAMES=([0]="max" [1]="helen" [2]="sam" [3]="zach")
```

`declare` 的输出表明 NAMES 和 B 具有多个元素。相比之下，A（其值在双引号内通过 `*` 赋值）只有一个元素：A 的所有元素都包含在一对双引号之间。

在下一个示例中，`echo` 尝试显示数组 A 的元素 1。由于 A 只有一个元素且该元素索引为 0，因此未显示任何内容。数组 A 的元素 0 包含所有四个名字。数组 B 的元素 1 包含数组中的第二个项，元素 0 包含第一个项。

```
$ echo ${A[1]}

$ echo ${A[0]}
max helen sam zach
$ echo ${B[1]}
helen
$ echo ${B[0]}
max
```

`${#name[*]}` 运算符返回数组中的元素数量：

```
$ echo ${#NAMES[*]}
4
```

当使用数组元素索引代替 `*` 时，同一个运算符返回该元素的长度：

```
$ echo ${#NAMES[1]}
5
```

可以在赋值语句的左侧使用下标来替换数组中指定的元素：

```
$ NAMES[1]=max
$ echo ${NAMES[*]}
max max sam zach
```

## 函数中的变量

由于函数在与调用它的 shell 相同的环境中运行，变量由 shell 及其调用的函数隐式共享。

```
$ nam () {
> echo $myname
> myname=zach
> }

$ myname=sam
$ nam
sam
$ echo $myname
zach
```

在前面的示例中，交互式 shell 中将 `myname` 变量设置为 `sam`。然后 `nam` 函数显示 `myname` 的值（`sam`）并将 `myname` 设置为 `zach`。最后的 `echo` 表明，在交互式 shell 中，`myname` 的值已更改为 `zach`。

局部变量对于编写通用函数的 shell 很有帮助。由于函数可能被许多由不同程序员编写的脚本调用，你需要确保函数内部使用的变量名称不会与（即重复）调用该函数的程序中的变量名称冲突。局部变量消除了这个问题。在函数内使用时，`local` 内建命令将变量声明为局部于定义它的函数。

下一个示例展示了函数中局部变量的使用。它包含两个名为 `count` 的变量。第一个在交互式 shell 中声明并初始化为 10。运行 `count_down` 后，`echo` 验证其值从未改变。另一个 `count` 使用 `local` 声明为 `count_down` 函数的局部变量。它的值在函数外部未知，范围从 4 到 1，正如函数内的 `echo` 命令所证实的那样。

以下示例显示函数是从键盘输入的；它不是一个 shell 脚本。请参见第 1017 页的技巧“函数不是 shell 脚本”。

```
$ count_down () {
> local count
> count=$1
> while [ $count -gt 0 ]
> do
>     echo "$count..."
>     ((count=count-1))
>     sleep 1
> done
> echo "Blast Off."
> }

$ count=10
$ count_down 4
4...
3...
2...
1...
Blast Off.
$ echo $count
10
```

`count=count-1` 赋值语句被包裹在双括号中，这促使 shell 执行算术评估（第 1056 页）。在双括号内，你可以引用 shell 变量而无需前导美元符号 ($)。关于函数局部变量的另一个示例，请参见第 397 页。

## 内建命令

内建命令在第 5 章中介绍过，执行它们时不会分叉新进程。本节讨论 `type`、`read`、`exec`、`trap`、`kill` 和 `getopts` 内建命令。第 1055 页的表 2-6 列出了许多 `bash` 内建命令。

