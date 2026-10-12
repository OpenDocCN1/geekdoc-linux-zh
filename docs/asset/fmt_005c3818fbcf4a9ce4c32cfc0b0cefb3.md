
不带选项时，`history` 显示带有行号的命令历史列表。以 `*` 开头的行表示已修改。用作参数的数字将列出行数。如果提供了非选项参数，它将作为历史文件的名称；否则，将使用 `HISTFILE` 的值。`history` 的选项如下：

| 选项 | 说明 |
| :--- | :--- |
| `-a` | 将自当前 `BASH` 会话开始以来输入的历史事件添加到历史文件中。 |
| `-n` | 将尚未从历史文件中读取的历史事件读取到当前历史列表中。 |
| `-r` | 读取历史文件的事件并将其用作当前历史。 |
| `-w` | 用当前历史列表替换历史文件。 |

除非遇到非法选项或在读写历史文件时发生错误，否则 `history` 返回 0。

## if-then

```
if Linux command
then
    commands
else
    commands
fi
fi
```

`if` 结构为命令设置了一个条件。该条件是特定 Linux 命令的退出状态。如果命令成功（返回退出状态为 0），则执行 `if` 结构中的命令。如果退出状态为 0 以外的任何值，则表示命令失败，并执行 `if` 结构中的命令。

`if` 命令以关键字 `if` 开始，后跟一个 Linux 命令，将评估该命令的退出条件。该命令始终会被执行。在命令之后，关键字单独占一行。其后可以跟任何一组命令。关键字 `fi` 结束命令。通常，你需要根据 Linux 命令是否成功在两种替代方案之间进行选择。`else` 关键字允许 `if` 结构在两种替代方案之间进行选择。如果 Linux 命令成功，则执行 `then` 关键字之后的命令；否则，执行 `else` 关键字之后的命令。

下一个示例中的脚本 `elsels` 执行 `ls` 命令，通过两种不同的可能选项列出文件：按大小排序或显示所有文件信息。如果用户输入 `s`，则按大小列出文件；否则，则列出所有文件信息。

### elsels

```
echo Enter s to list file sizes,
echo otherwise all file information is listed,
echo -n "Please enter option: "
```

```bash
read choice
if [ "$choice" = s ]
then
    ls -s
else
    ls -l
fi
echo Good-bye
```

```
$ elsels

Enter s to list file sizes,

otherwise all file information is listed.

Please enter option: s

total 2

1 monday 2 today

Good-bye

$
```

`if` 结构通常用于检查用户是否为 shell 脚本输入了正确数量的参数。特殊 shell 变量 `#` 包含用户输入的参数数量。在测试操作中使用 `$#` 允许你检查用户是否输入了正确数量的参数。

如果参数数量不对，你可能需要结束 shell 脚本。在下一个示例中，如果用户输入了多个参数，则测试将为真，并打印错误消息。

```bash
if [ $# -ne 1 ]
then
    echo Invalid number of arguments
    exit 1
fi
echo $#
```

```
$ arg

Invalid number of arguments
```

## jobs

```
jobs [-lnp] [jobspec]
jobs -x [arguments ...]
```

### BASH 命令 43

`jobs` 命令列出活动作业。`-l` 选项仅显示进程 ID，而 `-p` 选项仅列出作业组的进程 ID。`-n` 选项显示自上次通知以来变化的作业。如果提供特定作业编号作为参数（`jobspec`），则只显示该作业的信息。除非遇到非法选项或列出非法作业指定，否则 `jobs` 返回 0。使用 `-x` 选项，`jobs` 用于引用当前作业中的进程。命令或参数中找到任何作业指定都将被相应的进程 ID 替换，然后执行带有参数的命令。

结果列表中的每个条目将由括号内的作业号、是停止（stopped）还是运行（running）状态以及作业名称组成。加号 `+` 表示当前正在处理的作业，连字符 `-` 表示下一个要执行的作业。在下一个示例中，两个命令被放置在后台。`jobs` 命令随后会列出这些作业，并显示哪一个正在执行。

```bash
$ lpr intro &
[1] 547
$ cat *.c > myprogs &
[2] 548
$ jobs
[1] + Running lpr intro
[2] - Running cat *.c > myprogs
$
```

如果你愿意，可以通过输入与符号 `&` 一次性在命令行中将多个命令放置在后台。在这种情况下，`&` 既分隔了命令行上的命令，又在后台执行了它们。在下一个示例中，第一个排序并重定向所有 `.l` 文件的命令被放置在后台。在同一行命令行上，第二个命令（打印所有 `.c` 文件的命令）也被放置在后台。注意两个命令都以 `&` 结束。`jobs` 命令会将 `sort` 和 `lpr` 命令作为独立操作列出。

```bash
$ sort *.l > l1docs & lpr *.c &
[1] 534
[2] 567
$ jobs
```

### BASH 命令

```
+   [1] + Running sort *.1 > ldocs

[2] - Running lpr

$
```

## kill

```
kill [-s sigspec | -sigspec] [pid | jobspec] ...

kill -l [signum]
```

`kill` 用于终止进程或作业。通过 `-s` 选项，你可以指定要发送的信号 (`sigspec`)。默认情况下，信号是终止进程。通过 `-l` 选项，命令列出信号名称。对于信号数字 (`signum`)，会列出对应信号的名称。参数 `--` 会禁用后续参数的选项检查。如果成功发送了一个信号，`kill` 返回 `true`；如果发生错误或遇到非法选项，则返回 `false`。

`kill` 命令接受的参数可以是用户作业号 (`jobspec`) 或是系统进程号 (`pid`)。用户作业号前必须有一个百分号 `%`。你可以通过 `jobs` 命令查看作业号。在下一个示例中，`jobs` 命令列出了后台作业；然后取消了 2 号作业。

```
$ jobs

[1] + Running lpr intro

[2] - Running cat *.c > myprogs

$ kill %2
$
```

## let

```
let valuel operator value2
```

`let` 命令是 `BASH` shell 中执行算术值操作的 shell 命令。通过 `let`，你可以比较两个值或对它们执行算术操作，例如加法或乘法。此类操作经常用于 shell 程序中，以管理控制结构或执行必要的计算。`let` 命令可以使用关键字 `let` 指明，也可以使用一组双括号。其语法由关键字 `let` 后面跟两个由算术运算符或关系运算符分隔的数值值组成。

你可以使用本章之前“算术运算符”部分中列出的任何运算符作为你的运算符。`let` 命令会自动假设运算符是算术或关系性的。你不需要对 shell 运算符加引号。`let` 还会自动求值变量并将它们的值转换为算术值。这意味着你可以将你的算术操作写成简单的算术表达式。在下面的示例中，`let` 命令将值 2 和 7 相乘。结果输出到标准输出并显示。

```
$ let 2*7
14
```

如果你想在算术表达式的运算数之间留有空格，你必须对该表达式加引号。`let` 命令期望一个字符串。

```
$ let "2 * 7"
```

你还可以在 `let` 表达式中包含赋值操作。在下面的示例中，乘法的结果被赋值给 `res`。

```
$ let "res=2 * 7"
$ echo $res
14
$
```

你也可以使用任何关系运算符对数值值进行比较，例如检查一个值是否小于另一个值。关系操作经常用于管理控制结构，如循环和条件。在下面的示例中，`helloprg` 显示三次单词 "hello"。它利用小于等于的操作来管理循环，`let "again <= 3"`，并递增 `again` 变量，`let "again = again + 1"`。注意，当 `again` 增加时，它不需要被求值。不需要前面的 `$` 符号。`let` 会求值表达式中的变量。

### helloprg

```
again=1
while let "again <= 3"
do
  echo $again Hello
```

```
let "again=again + 1"
done
```

```
$ helloprg
1 Hello
2 Hello
3 Hello
```

## local

```
local [variable-name[value] ...]
```
