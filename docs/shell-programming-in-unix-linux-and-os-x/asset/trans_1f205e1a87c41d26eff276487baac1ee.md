

# 命令摘要

do

```
nroff -Tlp $file | lp
done
```

## getopts 命令

通用格式：getopts options var

此命令处理命令行参数。options 是一个有效单字母选项列表。如果 options 中的任何字母后面跟着一个冒号 `:`，则该选项在命令行上需要一个额外的参数，该参数与选项之间至少要有一个空格分隔。

每次调用 getopts 时，它都会处理下一个命令行参数。如果找到有效选项，getopts 会将匹配的选项存储在指定的变量 var 中，并返回零退出状态。

如果选项是无效的（未列在 options 列表中），getopts 将一个 `?` 存储在 var 中，并返回零退出状态。它会向标准错误输出一条错误信息。

如果某个选项需要参数，getopts 将匹配的选项存储在 var 中，并将命令行参数存储在指定的变量 OPTARG 中。如果命令行上没有剩余参数，getopts 将 var 设为 `?` 并向标准错误输出一条错误信息。

如果命令行上没有更多剩余的参数（如果下一个命令行参数不以 `-` 开头），getopts 返回非零退出状态。

特殊变量 OPTIND 也被 getopts 使用。它最初被设置为 1，并在每次 getopts 返回时都会进行调整，以指示下一个要处理的命令行参数编号。

参数 `--` 可以放在命令行上，以指定命令行参数的结束。

getopts 支持堆叠参数，例如：

```
repx - iau
```

这等同于：

```
repx -i -a -u
```

具有强制参数的选项不能堆叠。

如果使用了格式：

```
getopts options args var
```

getopts 解析由 args 指定的参数而不是命令行参数。

示例

```
usage="Usage: foo [-r] [-0 outfile] infile"
```

```
while getopts ro: opt
```

## 录录 Shell 摘要

```
do
  case "$opt"
    in
      r) rflag=1;
      O) oflag=1
        file=$OPTARG;
      \?) echo "$usage"
    esac
    exit 1;
```

```
if [ $OPTIND -gt $# ]
then
  echo "Needs input file!"
  echo "$usage"
  exit 2
fi
```

```
shift $((OPTIND - 1))
if=$1
```

## hash 命令

**通用格式：** hash `commands`

此命令告诉 shell 查找指定的命令，并记住它们所在的目录。如果未指定 `commands`，则显示哈希命令列表。

如果使用了格式：

```
hash -r
```

shell 会从其哈希列表中移除所有命令。下次执行任何命令时，shell 将使用其标准的搜索方法来查找命令。

*示例*

```
hash rolo whoq
hash
hash -r
```

- 将 rolo 和 whoq 添加到哈希列表
- 打印哈希列表
- 移除哈希列表

## if if 命令

**通用格式：**

```
if command;
then
```

## 命令摘要 345

```
command
command
...
fi
```

command，被执行并测试其退出状态。如果状态为零，则执行后续直到 `fi` 之前的命令。否则，跳过后续直到 `fi` 之前的命令。

## 示例

```
if grep $sys sysnames > /dev/null
then
  echo "$sys is a valid system name"
fi
```

如果 grep 返回退出状态为零（如果在 sysnames 文件中找到了 $sys，则如此），则执行 echo 命令；否则跳过它。

内置命令 test 经常被用作 if 后的命令，可以通过显式调用 test 或使用其助记简写来实现，后者需要匹配的 `[ ]`。

## 示例

```
if [ $ -eq 0 ]; then
  echo "Usage: $0 [-1] file ..."
  exit 1
```

可以可以为 if 添加一个 `else` 子句，当命令返回非零退出状态时执行该子句。在这种情况下，if 的通用格式变为：

```
if command;
then
  command
  command
  ...
else
  command
  command
  ...
fi
```

如果 command，返回退出状态为零，则执行后续直到 `else` 之前的命令，并跳过 `else` 和 `fi` 之间的命令。否则，command，返回非零退出状态，跳过 `then` 和 `else` 之间的命令，并执行 `else` 和 `fi` 之间的命令。

```
if [ -z "$line" ]
then
  echo "I couldn't find $name"
```

else

```
echo "$line"
```

```
fi
```

在前面的示例中，如果 line 的长度为零，则执行显示消息 "I couldn't find $name" 的 echo 命令；否则，执行显示 line 值的 echo 命令。

当需要做出两个方向以上的决策时，if 命令的最终格式非常有用。它的通用格式是：

```
if command,
```

```
then
```

```
command
  command
  ...
```

```
elif command_j
```

```
then
```

```
command
  command
  ...
```

```
elif command_n
```

```
then
```

```
command
  command
  ...
```

```
else
```

```
command
  command
  ...
```

```
fi
```

如果 command，返回退出状态为零，则执行后续直到 `else` 之前的命令，并跳过 `else` 和 `fi` 之间的命令。否则，command，返回非零退出状态，跳过 `then` 和 `else` 之间的命令，并执行 `else` 和 `fi` 之间的命令。

## 命令摘要 346

## jobs 命令

通用格式：jobs

打印活动作业列表。如果指定了 -l 选项，则也会列出详细信息。如果指定了 -p 选项，仅列出进程 ID。

如果 jobs 命令提供了可选的 job_id，则列出该作业的信息。

示例

```
$ sleep 100 &
[1] Running      sleep 100
```

## kill 命令

通用格式：kill -signal job

kill 命令向指定的进程发送信号，job 是进程 ID 或作业 ID，signal 是数字或信号名称。-l 选项列出相应的信号名称。

当提供信号名称时也可以使用 -s 选项，在这种情况下前面不使用横杠（见下例）。

如果没有指定 signal，则使用 SIGTERM (TERM)。

示例

```
$ kill -9 1234
$ kill -HUP $2
kill -s TERM $2
kill $1
```

## newgrp 命令

通用格式：newgrp group

此命令将你的实际组 ID (GID) 更改为 group。如果没有参数，它将切换回默认组。

## Shell 摘要

示例

```
newgrp shbook    切换到组 shbook
newgrp             切换回默认
```

如果新组关联了密码，且你不是该组的成员，将被提示输入密码。

```
newgrp -l 切回你的登录组。
```

## pwd 命令

通用格式：pwd

此命令告诉 shell 打印你的工作目录，写入标准输出。

示例

```
$ pwd
/users/steve/documents/memos
$ cd
$ pwd
/users/steve
$
```

## read 命令

通用格式：read vars

此命令导致 shell 从标准输入读取一行，并将连续空白分隔的单词赋值给变量 vars。如果列出的变量少于行的单词，额外的单词将存储在最后一个变量中。

指定一个变量的效果是将整行读取并赋值给该变量。除非遇到文件结束（EOF）条件，否则 read 的退出状态为零。

示例

```
$ read hours mins
10 19
$ echo "$hours:$mins"
10:19
$ read num rest
39 East 12th Street, New York City 10003
$ echo "$num\n$rest"
39
East 12th Street, New York City 10003
```

