
## 控制结构 965

第一个 `test-command` 用于判断用户是否在命令行中指定了单个参数。如果 `test-command` 返回 `0`（`true`），则变量 `directory` 被赋值为当前工作目录（`.`）。如果 `test-command` 返回 `false`，则 `elif` 语句测试第二个参数是否是一个目录。如果它是目录，变量 `directory` 将被设置为第二个命令行参数，即 `$2`。如果 `$2` 不是目录，`lnks` 会向标准错误发送一条用法信息并返回状态为 1 退出。

`lnks` 中的下一个 if 语句测试 `$file` 是否存在。该测试可防止 `lnks` 浪费时间去为一个不存在的文件查找链接。当 `test` 内置命令使用 `!`、`-f` 和 `$file` 这三个参数调用时，如果文件 `$file` 不存在，其结果为 `true`：

```bash
[ ! -f "$file" ]
```

位于 `test` 的 `-f` 参数之前的 `!` 运算符会对结果取反，因此如果文件 `$file` 确实存在且为普通文件，结果将为 `false`。

接下来，`lnks` 使用 `set` 和 `ls` 来检查 `$file` 有多少个链接：

```bash
# 检查文件的链接数
set -- $(ls -l "$file")
linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
    echo "lnks: no other hard links to $file" 1>&2
    exit 0
fi
```

`set` 内置命令使用命令替换（见第 362 页）将位置参数设置为 `ls -l` 的输出。此输出中的第二个字段是链接数，因此用户创建的变量 `linkcnt` 被赋值为 `$2`。与 `set` 一起使用的 `--` 防止 `set` 将 `ls -l` 产生的第一个参数解释为选项（第一个参数是文件的访问权限，通常以 `-` 开头）。if 语句检查 `$linkcnt` 是否等于 1；如果相等，`lnks` 显示一条消息并退出。虽然这条消息严格来说不是错误信息，但它被重定向到了标准错误。按照 `lnks` 的编写方式，所有信息性消息都发送到标准错误。只有 `lnks` 的最终产物——指向指定文件的链接路径名——才发送到标准输出，因此你可以随意重定向输出。

如果链接数大于 1，`lnks` 继续查找 `$file` 的 `inode`（见第 1153 页）。如第 229 页所述，比较与文件名关联的 inode 是判断这些文件名是否链接到同一文件的好方法。`lnks` 脚本使用 `set` 将位置参数设置为 `ls -l` 的输出。`set` 的第一个参数是文件的 inode 号，因此名为 `inode` 的用户创建变量被赋值为 `$1`：

```bash
# 获取给定文件的 inode
set $(ls -i "$file")
inode=$1
```

最后，`lnks` 使用 `find` 实用程序搜索具有与 `$inode` 匹配的 inode 号的文件：

```bash
# 查找并打印具有该 inode 号的文件
echo "lnks: using find to search for links..." >&2
find "$directory" -xdev -inum $inode -print
```

`find` 实用程序在以由第一个参数（`$directory`）指定的目录为根的目录层级中，搜索满足剩余参数指定标准的文件。在此示例中，剩余参数将 inode 号与 `$inode` 匹配的文件名发送到标准输出。由于不同文件系统上的文件可能拥有相同的 inode 号但实际上并未相互链接，因此 `find` 必须只搜索与 `$directory` 位于同一文件系统上的目录。`-xdev`（跨设备）参数可防止 `find` 搜索其他文件系统上的目录。有关文件系统和链接的更多信息，请参阅第 226 页。

`lnks` 中位于 `find` 命令之前的 `echo` 命令，用于告知用户 `find` 正在运行。之所以包含它，是因为 `find` 的运行时间可能很长。由于 `lnks` 不包含最终的 exit 语句，因此 `lnks` 的退出状态就是其最后一个执行的命令 `find` 的退出状态。

## 调试 shell 脚本

在编写类似 `lnks` 这样的脚本时，很容易出错。你可以使用 shell 的 `-x` 选项来辅助调试脚本。此选项会使 shell 在执行命令之前显示每条命令。以此方式跟踪脚本的执行过程可以为你提供有关问题所在的信息。

你可以像前面的示例那样运行 `lnks`，并使 shell 在执行前显示每条命令。你可以为当前 shell 设置 `-x` 选项（`set -x`），这样所有脚本在执行时都会显示命令；或者使用 `-x` 选项仅影响由命令行调用的正在运行该脚本的 shell。

```bash
$ bash -x lnks letter /home
+ '[' 2 -eq 0 -o 2 -gt 2 ']'
+ '[' -d letter ']'
+ file=letter
+ '[' 2 -eq 1 ']'
+ '[' -d /home ']'
+ directory=/home
+ '[' ']' -f letter ']'
...
```

**PS4** 脚本执行的每条命令前都会显示 `PS4` 变量的值——默认是一个加号 (+)，因此你可以区分调试输出和脚本产生的输出。如果在调用脚本的 shell 中设置了 `PS4`，必须将其导出。下一条命令将 `PS4` 设置为 `>>>>` 后跟一个空格并将其导出：

```bash
$ export PS4='>>>> '
```

你还可以通过在脚本开头附近放入以下 `set` 命令，来设置正在运行脚本的 shell 的 `-x` 选项：

`set -x`

将 `set -x` 放在脚本中任何你想要开启调试的位置。使用加号关闭调试选项：

`set +x`

`set -o xtrace` 和 `set +o xtrace` 命令分别与 `set -x` 和 `set +x` 执行相同的功能。

## for...in

`for...in` 控制结构具有以下语法：

```bash
for loop-index in argument-list
    do
        commands
    done
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_1017_0.png)

图 27-4 for...in 流程图

for...in 结构（图 27-4，上一页）将参数列表（argument-list）中第一个参数的值分配给循环索引（loop-index），并执行 do 和 done 语句之间的命令。do 和 done 语句标记 for 循环的开始和结束。

当控制权传递给 done 语句后，该结构将参数列表（argument-list）中第二个参数的值分配给循环索引（loop-index）并重复执行命令。然后，它对参数列表（argument-list）中的每个参数各重复一次 do 和 done 语句之间的命令。当结构遍历完参数列表（argument-list）后，它将控制权传递给 done 之后的语句。

以下的 for...in 结构将 apples 赋值给用户创建的变量 fruit，然后显示 fruit 的值，即 apples。接下来，该结构将 oranges 赋值给 fruit 并重复该过程。当遍历完参数列表后，该结构将控制权转移到 done 之后的语句，该语句显示一条消息。

```bash
$ cat fruit
for fruit in apples oranges pears bananas
do
echo "$fruit"
done
echo "Task complete."

$ ./fruit
apples
oranges
pears
bananas
Task complete.
```

下一个脚本通过循环遍历工作目录中的文件并使用 test 确定哪些是目录文件，从而列出工作目录中目录文件的名称：

```bash
$ cat dirfiles
for i in *
do
if [ -d "$i" ]
then
echo "$i"
fi
done
```

模糊的文件引用字符 * 匹配工作目录中所有文件（除隐藏文件外）的名称。在执行 for 循环之前，shell 展开 * 并使用生成的列表依次将值分配给索引变量 i。

## for

for 控制结构具有以下语法：

```bash
for loop-index
commands
done
```

在 for 结构中，循环索引（loop-index）依次获取每个命令行参数的值。除了获取循环索引（loop-index）值的方式不同外，for 结构与 for...in 结构（图 27-4，第 967 页）相同。for 结构执行一系列命令，通常依次处理每个参数。

以下的 shell 脚本展示了一个 for 结构，它显示每个命令行参数。脚本的第一行 `for arg` 隐含了 `for arg in "$@"`，其中 shell 将 "$@" 展开为带引号的命令行参数列表 "$1" "$2" "$3" 等。脚本的其余部分对应于 for...in 结构。

```bash
$ cat for_test
for arg
do
echo "$arg"
done
$ for_test candy gum chocolate
candy
gum
chocolate
```

## whos 脚本

以下名为 whos 的脚本演示了在 for 结构中使用隐含的 "$@" 的实用性。你给 whos 提供一个或多个用户的完整姓名或用户名作为参数，whos 会显示关于这些用户的信息。whos 脚本从其显示的信息中获取数据，这些数据来自 /etc/passwd 文件的第一个和第五个字段。第一个字段包含用户名，第五个字段通常包含用户的完整姓名。你可以提供一个用户名作为 whos 的参数来识别用户的姓名，或者提供一个姓名作为参数来识别用户名。whos 脚本类似于 finger 实用程序，尽管 whos 提供的信息较少。

```bash
$ cat whos
#!/bin/bash

if [ $# -eq 0 ]
then
echo "Usage: whos id..." 1>&2
exit 1
fi
for id
do
mawk -F: '{print $1, $5}' /etc/passwd | grep -i "$id"
done
```

在下一个示例中，whos 识别用户名为 chas 的用户以及姓名为 Maridou Smith 的用户：

```bash
$ ./whos chas "Maridou Smith"
chas Charles Casey
msmith Maridou Smith
```

