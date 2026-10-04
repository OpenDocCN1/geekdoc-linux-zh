
```
trap "commands" signal_list
```

在这种形式下，trap 会在脚本接收到 signal_list 中数字所对应的任意信号时执行引号中的命令。

若要将信号恢复为其默认动作，请使用以下形式的 trap 命令：

```
trap signal_list
```

不指定任何命令。

允许忽略信号的第三种形式，格式为：

```
trap "" signal_list
```

仅指定了一个空命令字符串。

trap 的典型用途是在程序异常终止时清理临时文件，否则这些文件可能会占用你的文件空间。下面的代码片段假设在脚本内部使用一个名为 /tmp/tmp$$ 的唯一临时文件，并且如果脚本在接收到中断或退出信号时异常终止，则需要在脚本终止前删除该临时文件作为清理操作：

```
trap "rm -f /tmp/tmp$$; exit 0" 2 3
touch /tmp/tmp$$
#
# Rest of shell script here
#
trap 2 3
```

该脚本首先设置自身以捕获信号 2 和 3（来自键盘的 Ctrl-c 和 Ctrl-\）。如果这两个信号中的任一个发生，通常是因为用户试图中断脚本并中止其运行。trap 执行后，信号 2 和 3 将导致执行以下命令：

```
rm -f /tmp/tmp$$; exit 0
```

rm 命令会删除临时文件，然后 exit 命令终止脚本。请注意，如果用分号分隔，可以在同一行输入多个命令。

trap 命令执行后，shell 脚本的其余部分将正常执行，从 touch 命令创建临时文件开始。该代码片段的最后一行将信号 2 和 3 的操作恢复为默认状态，presumably 在临时文件不再需要并且已经删除之后。

## Exercises

编写 shell 脚本以执行以下各项操作：

- 1. 将两个目录的名称作为参数。复制第一个目录中的所有文件到第二个目录，并在复制过程中将文件中所有出现的字符串 SP 翻译为 SU。
- 2. 检查你的 PATH 变量是否包含 /usr/local/bin 作为搜索目录之一，并显示合适的消息。
- 3. 从标准输入设备读取文本行并复制到标准输出。以与 cat -n 类似的方式为每一行输出加上行号（不使用 cat 命令）。
- 4. 接受一个介于 2 到 15 之间的参数，并在标准输出上使用加号 (+)、减号 (-) 和竖线 (|) 符号绘制该大小的正方形，例如：
- 5. 接受两个命令行参数，第一个是目录的名称，第二个是文件大小（字节）。该命令应列出你有读权限且小于给定大小的目录中的所有普通文件。你应检查是否只传递了两个参数，并且第一个参数确实是一个目录。

```
$ drawsquare 4
+--+
|  |
|  |
+--+
```

如果给命令的参数数量错误或参数不是正确范围内的数字，应显示合适的错误消息并返回退出状态 1。

## Answers

1. 一种可能的解决方案是依次取每个源路径名，从该路径中取出基本名，然后使用 sed 将源文件复制到目标目录，使用相同的基名，并在复制过程中执行所需的转换：

```
for i in $1/*
do
x=`basename $i`
sed s/SP/SU/ $i >$2/$x
done
exit 0
```

2. 使用 grep 检查 PATH 是否包含目录 /usr/local/bin 的名称并显示适当的消息是很简单的：

```
if echo $PATH | grep "/usr/local/bin" &>/dev/null
then
    echo PATH contains /usr/local/bin
else
    echo PATH does not contain /usr/local/bin
fi
exit 0
```

请注意，grep 命令的输出和错误输出都被丢弃了，因为只有 grep 的退出状态才重要。

3. 最简单的方法是使用 shell 的数值表达式求值功能来维护一个行计数，可以在每一行输出的开头将其回显到标准输出，然后递增以备下一行使用：

```
linecount=1
while read line
do
    echo $linecount $line
    linecount=$( $[ $linecount+1 ] )
done
exit 0
```

4. 该问题的解决方案首先检查命令行参数是否存在错误。然后代码从左到右、从上到下遍历输出正方形的字符位置，通过一些简单的逻辑确定在每个位置显示哪一个字符：

```
if test $# -ne "1"
then
    echo `usage: drawsquare <n>`
    exit 1
fi
if test $1 -lt "2" -o $1 -gt "15"
then
    echo `usage: drawsquare <n>`
    echo `      (where 2<=n<=15)`
    exit 1
fi
xcount=$1
ycount=$1
while test $ycount -gt "0"
do
```

```
while test $xcount -gt "0"
do
    if test $xcount -eq "1" -o $xcount -eq $1
    then
        if test $ycount -eq "1" -o $ycount -eq $1
        then
            echo -n "+"
        else
            echo -n "|"
        fi
    else
        if test $ycount -eq "1" -o $ycount -eq $1
        then
            echo -n "-"
        else
            echo -n " "
        fi
    fi
    xcount=$[$xcount-1]
done
xcount=$1
ycount=$[$ycount-1]
echo
done
exit 0
```

5. 对于指定目录中的每个文件，都进行测试以查看它是否可读且为普通文件。如果该测试为真，则检查文件大小，并显示小于第二个参数的文件名及其大小：

```
if test $# -ne 2
then
    echo `usage: listfiles <dirpath> <size>`
    exit 1
fi
if ! test -d $1
then
    echo `usage: listfiles <dirpath> <size>`
    exit 1
fi
for i in $1/*
do
    if test -r $i -a -f $i
    then
```

```
size=`wc -c <$i`
if test $size -lt $2
then
    echo `basename $i` has size $size bytes
fi
fi
done
```

## Part II

## ADMINISTRATION

## Getting Up and Running

理想情况下，你将慢慢进入 Linux 系统管理，并在作为普通用户探索和使用系统有足够机会之后。当你开始管理之旅时，希望你身边会有一些人已经在你前方道路的各个阶段，他们能够指导你的早期步骤。或者至少你将是其中一群希望一起踏上这段旅程的计算爱好者之一。

虽然这种场景适用于你们中的许多人，但仍会有更多人缺乏必要的经验或帮助。如果你确实发现自己起初是独自一人，并且对 Linux 只有有限的经验，那么这将是一项缓慢且容易出错的工作。在这种情况下，当事情第一次没有按预期工作时，或者尽管你已经阅读了手册页十几次以从中榨取最后一点意义，但仍然看不到如何做某件事时，重要的是不要过于沮丧或灰心——只要深呼吸…。

关于 Linux，首先要记住的是，尤其是如果你在 PC 上运行它并且有 DOS 背景，尽管表面看起来如此，Linux 是一种大型机器操作系统，即使你是在小型机器上运行它。如果你想避免许多等待着捕获粗心的陷阱，你必须培养大型机器操作系统的习惯和心态。底线是，即使不是你，也需要有人为你的系统担任系统管理员——虽然管理工作的量可以很小，但不能为零。

即使有了所有这些警告，最坏的情况是你做了某些事情破坏了你的安装。在这种情况下，即使是从非常慢的发行介质（约 70 张软盘）安装一个非常完整的 Linux 系统（约 150 Mb），也最多只需约两个小时即可让你恢复正常工作。
