
```sh
who | grep "^$name " > /dev/null && echo "$name's not logged on" \
        || echo "$name is logged on"
```

（回想一下，当 `\` 用在行末时，它向 shell 表示行继续。）

如果 `grep` 成功，执行第一个 `echo`；如果失败，则执行第二个。

这些结构也经常用在 `if` 命令中，正如这个来自系统 shell 程序的片段所展示的那样（如果你不理解其中调用的每个命令，也不用担心）：

```sh
if validsys "$sys" && timeok
then
        sendmail "$user@$sys" < $message
fi
```

如果 `validsys` 返回的退出状态为零，`timeok` 会被执行，然后其退出状态被 `if` 测试。如果该状态为零，则执行 `sendmail`。然而，如果 `validsys` 返回非零退出状态，`timeok` 不会被执行，`if` 会测试这个失败的退出状态，最终 `sendmail` 不会被执行。

在前面的情况中，使用 `&&` 运算符是一种逻辑与（logical AND）；两个程序都必须返回退出状态零，`sendmail` 程序才会被执行。实际上，你也可以把上面的 `if` 条件写成

```sh
validsys "$sys" && timeok && sendmail "$user@$sys" < $message
```

相比之下，当 `||` 用在 `if` 中时，效果类似于逻辑或（logical OR）：

```sh
if endofmonth || specialrequest
then
        sendreports
fi
```

如果 `endofmonth` 返回零退出状态，`sendreports` 会被执行；否则 `specialrequest` 被执行，如果其退出状态为零，`sendreports` 会被执行。最终效果是，只要 `endofmonth` 或 `specialrequest` 中任何一个返回零退出状态，`sendreports` 就会被执行。

在第 8 章中，你将学习如何在程序中编写复杂的流程控制循环。但在此之前，请用本章讲解的 `if`、`case`、`&&` 和 `||` 记法尝试后面的练习。

# 转不停的小马

在本章中，您将学习如何设置程序循环。这些循环使您能够执行一组命令，既可以是指定次数，也可以是直到满足特定的结束条件。

Shell 编程中三个内置的循环命令是：

- `for`
- `while`
- `until`

在本章的各节中，您将逐一了解这些循环。

## `for` 命令

`for` 命令用于将一条或多条命令执行指定次数。其基本格式如下所示：

```sh
for var in word₁ word₂ ... wordₙ
do
        command
        command
        ...
done
```

包含在 `do` 和 `done` 之间的命令称为循环体，它们会针对 `in` 之后列出的每一项各执行一次。当循环执行时，第一个词 `word₁` 被赋给变量 `var`，然后循环体被执行。接着，列表中的第二个词 `word₂` 被赋给 `var`，循环体再次执行。

这个过程持续进行，列表中的词依次被赋给 `var`，循环体中的命令依次执行，直到列表中的最后一个词 `wordₙ` 被赋给 `var` 并执行循环体。此时，列表中不再有剩余的词，`for` 命令的执行也随之完成。接着，执行过程继续沿 `done` 之后的命令进行。

如果 `in` 之后列出了 *n* 个词，则循环结束时，循环体总共执行了 *n* 次。

下面是一个将被执行三次的循环：

```sh
for i in 1 2 3
do

        echo $i

done
```

要试用它，请在终端中直接输入，就像输入任何其他 shell 命令一样：

```sh
$ for i in 1 2 3
> do
>
>        echo $i
>
> done
1
2
3
$
```

当 shell 等待输入 `done` 以完成 `for` 命令时，它会持续显示次级命令提示符。当用户输入 `done` 后，shell 接着继续执行循环。由于 `in` 之后列出了三个项（1、2 和 3），循环体——在本例中是一条 `echo` 命令——将总共执行三次。

第一次进入循环时，列表中的第一个值 1 被赋给变量 `i`，然后循环体被执行，在终端显示出 `i` 的值。接着列表中的下一个词 2 被赋给 `i`，`echo` 命令再次执行，导致在终端显示 2。第三次进入循环时，列表中的第三个词 3 被赋给 `i` 并执行 `echo` 命令，结果是在终端显示 3。此时，列表中不再有剩余的词，因此 `for` 命令执行完毕，shell 显示命令提示符让您知道它已完成。

现在回到第 6 章，回顾一下能让您通过 `tbl`、`nroff` 和 `lp` 运行文件的 `run` 程序：

```sh
$ cat run
tbl $1 | nroff -mm -Tlp | lp
$
```

如果您想运行 `memo1` 到 `memo4` 这些文件，可以在终端输入以下命令：

```sh
$ for file in memo1 memo2 memo3 memo4
> do
>        run $file
> done
request id is laser1-33 (standard input)
request id is laser1-34 (standard input)
request id is laser1-35 (standard input)
request id is laser1-36 (standard input)
$
```

`memo1`、`memo2`、`memo3` 和 `memo4` 这四个值将依次赋给变量 `file`，并以该值作为参数执行 `run` 程序。执行过程就像您输入了四条命令一样：

```sh
$ run memo1
request id is laser1-33 (standard input)
$ run memo2
request id is laser1-34 (standard input)
$ run memo3
request id is laser1-35 (standard input)
$ run memo4
request id is laser1-36 (standard input)
$
```

shell 允许在 `for` 语句的词列表中进行文件名替换，因此前面的循环也可以这样编写：

```sh
for file in memo[1-4]
do
        run $file
done
```

如果您想使用 `run` 程序打印当前目录中的所有文件，可以输入

```sh
for file in *
do
        run $file
done
```

要做一些更复杂的操作，假设 `filelist` 包含一个文件列表，表示您想通过 `run` 运行的文件。您可以输入

```sh
files=$(cat filelist)

for file in $files
do
        run $file
done
```

来运行每个文件，或者更简洁地：

```sh
for file in $(cat filelist)
do
        run $file
done
```

不过，更好的做法实际上是改进 `run` 脚本本身，而事实证明 `for` 语句非常适合这项工作：

```sh
$ cat run
#
# process files through nroff -- version 2
#
for file in $*
do
        tbl $file | nroff -mm -Tlp | lp
done
$
```

回想一下，特殊的 shell 变量 `$*` 代表命令行上输入的所有参数。如果您输入以下命令来执行新版的 `run`：

```sh
run memo1 memo2 memo3 memo4
```

`for` 列表中的 `$*` 将被替换为四个参数 `memo1`、`memo2`、`memo3` 和 `memo4`。当然，您也可以输入

```sh
run memo[1-4]
```

来获得相同的结果。

### `$@` 变量

既然我们正在使用 `$*`，不妨更仔细地看看它及其兄弟 `$@` 是如何工作的。为此，让我们编写一个名为 `args` 的程序，它将显示命令行上输入的所有参数，每行一个。

```sh
$ cat args
echo Number of arguments passed is $#

for arg in $*
do
        echo $arg

done
$
```

现在来试一下：

```sh
$ args a b c
Number of arguments passed is 3
a
b
c
$ args 'a b' c
Number of arguments passed is 2
a
b
c
$
```
