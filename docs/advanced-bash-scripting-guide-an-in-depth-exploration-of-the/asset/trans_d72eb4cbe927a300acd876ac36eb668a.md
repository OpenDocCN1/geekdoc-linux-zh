

# 高级 Bash 脚本指南

## 因为 $pass_count 尚未初始化。

let $pass_count += "
## 假设未初始化的变量 $pass_count
## 在第一次循环时可以进行递增。
## 这在 Bash 和 pdksh 中有效，
## 但它依赖于不可移植（且可能危险的）的行为。
## 更好的做法是在递增之前将 $pass_count 初始化为 0。

```
while [ "$pass_count" -le $MAXPASSCOUNT ]
do
  . # 脚本“源化”它自己，而不是调用自己。
  # . /$0（这将导致真正的递归）在这里不起作用。为什么？
done
```

## 发生的情况并不是真正的递归，
## 因为脚本实际上“展开”了它自己，即：
## 每通过一次 'while' 循环，
## 就会生成一段新的代码，
## 每通过一次第 20 行的 'source'。
## 当然，脚本将每个新被“源化”的 "!" 行
## 视为注释，而不是新脚本的开始。

```
echo

exit 0
  # 最终效果是从 1 数到 100。
  # 令人印象深刻。
```

练习：
# 写一个使用此技巧来执行实际操作的脚本。

exit
无条件终止脚本。[63] exit 命令可以接受一个整数参数，该参数将作为退出状态返回给 shell。良好的习惯是所有简单的脚本都以 exit 0 结束，表示运行成功。

- 如果脚本以带有参数的 exit 退出，则脚本的退出状态是脚本中执行的最后一个命令的退出状态，不计入 exit。这等同于 exit $?.
- exit 命令可用于终止子壳（subshell）。

exec
此 shell 使用指定的命令重建当前进程。通常，当 shell 遇到命令时，它会派生（fork）一个子进程来实际执行它。使用 exec 内置命令，shell 不会派生，被 exec 的命令将替换 shell。在脚本中使用时，它会在被 exec 的命令终止时强制退出脚本。[64]

# 15-24. exec 的影响

```bash
#!/bin/bash
echo echo "Exiting \$0" at line $LINENO."  # 在此处退出脚本。
# $LINENO 是一个表示其所在行号的内部变量。
```

15. 内置命令和内置函数

```bash
# 以下行永远不会执行。
echo "这条 echo 无法回显。"
exit 99      # 此脚本不会退出。
# 在脚本终止后用 'echo' 检查退出值。
# 它将“不会”这样。
```

**示例 15-25. 一个执行自身的脚本**

```bash
#!/bin/bash
# self-exec.sh

# 注意：将此脚本的权限设置为 755 或 555，
# 然后用 ./self-exec.sh 调用它。
echo
echo "这一行在脚本中只出现了一次，但它一直在不断 echo。"
echo "此脚本实例的 PID 仍然是 $$"
# 证明子壳没有被派生。
exec $0      # 产生此脚本的另一个实例
# 并替换上一个。
echo "这一行永远不会 echo!"  # 为什么不？
exit 99      # 在此处不会退出！
```

exec 还用于分配文件描述符。例如，`exec <zzz-file` 将 stdin 替换为文件 `zzz-file`。find 与动态更改 shell 选项的内置命令不同（参见示例 25-1）。它经常出现在 Bash 启动文件中，但也使用版本 2 或更高版本通过 'cd' 查找缺失的目录名称。

shopt -s cd -u sets.
cd /home  # 哎！错写了 '/home'。
pwd       # shell 修正了拼写错误。
```

在函数内部放置命令会输出关于调用者的信息。

```bash
#!/bin/bash
function () {
  # 如果没有指定数字，fg 或 bg 命令将作用于当前运行的作业。
  # 调用脚本的名称。
  # 函数被调用的行号。
  # 没有效果，因为它不在函数内部。
```

命令还可以从另一个脚本中返回调用者信息。类似于函数，这是一种“子程序调用”。你可能会在调试时发现这个命令很有用。

true
一个返回成功（零）退出状态但什么都不做的命令。

```bash
bash$ true
bash$ echo?
0
```

# 无限循环
while true
do
  operation-1
  operation-2
  operation-n
  # 需要一种跳出循环的方法，否则将挂挂。
done
```

false
一个返回退出状态但什么都不做的命令。

```bash
bash$ false
bash$ echo?
1
```

# 测试 "false"
if false
then
  echo "false 值为 \"true\""
else
  echo "false 值为 \"false\""
fi
# false 值为 "false"

# 在 "false" 时循环（空循环）
while false
do
  # 以下代码将不会执行。
operation-1
operation-2
...
operation-n
# 什么都没有发生！
done

# type [cmd]
与外部命令 which 类似，**type cmd** 识别 "cmd。"与 which 不同，**type** 是一个 Bash 内置命令。-a 选项显示标识关键字和内置命令，并定位具有相同名的系统命令。

```bash
bash$ type 'f'
# 是一个 shell 内置命令
bash$ type -a 'f'
# 是一个 shell 内置命令
# 是 /usr/bin/
bash$ type type
type 是一个 shell 内置命令
```

**type** 命令对于测试某个命令是否存在非常有用。

hash [cmds]
记录指定命令的路径名称——shell 哈希表——这样 shell 或脚本在后续调用这些命令时就不需要搜索 PATH。当调用 hash且不带参数时，它只需列出已哈希的命令.-r 选项重置哈希表。

bind
bind 内置命令显示或重新定义绑定。

help
获取 shell 内置命令的用法摘要。这是 whatis 的对应项，但是针对内置命令。帮助信息的显示在 Bash 版本 4 发布中得到了急需的更新。

```
bash$ help exit
exit: exit [n]
以状态 N 退出 shell。如果省略 N，则退出状态为上一个执行命令的退出状态。
```

# 15.1. 作业控制命令
以下某些作业控制命令接受作业标识作为参数。参见章节末尾的表格。

jobs
列出后台运行的作业，提供作业号。不像 ps 有用。很容易混淆作业和进程。某些内置命令（如 kill、disown 和 wait）接受作业号或进程号。fg、bg 和 jobs 仅接受作业号。

```
bash$ sleep 100 &
[1] 1384
```

```
bash $ jobs
[1]+ Running sleep 100 &
```

"1" 是作业号（作业由当前 shell 管理）。"1384" 是 PID 进程 ID（进程由系统维护）。要杀死此作业/进程，可以使用 kill %1 或 kill 1384。disown
从 shell 的活动作业表中移除作业。

fg, bg
fg 命令将后台作业切换到前台。bg 命令重新启动挂起的作业并在后台运行。如果没有指定作业号，fg 或 bg 命令作用于当前运行的作业。

wait
暂停脚本执行，直到所有后台作业终止，或指定的选项作业或进程 ID 终止。返回等待命令的退出状态。你可以使用 wait 命令防止脚本在后台作业执行之前退出（除非你创建了孤儿进程）。

# 示例 1-26. 在继续之前等待进程

```bash
#!/bin/bash
ROOT_UID=0 # 只有 UID 为 0 的用户才有 root 权限。
E_NOTROOT=65
E_NOPARAMS=66

if [ "$UID" -ne "$ROOT_UID" ];
then
    echo "必须以 root 身份运行此脚本。"
    # "去吧孩子，该睡觉时间了。"
    exit $E_NOTROOT
fi

if [ -z "$1" ];
then
    echo "用法: basename $0 字符串"
    exit $E_NOPARAMS
fi

echo "更新 'locate' 数据库..."
echo "这可能需要一段时间。"
updatedb /usr & # 必须以 root 身份运行。
```

```
wait
# 在 updatedb 完成之前不要运行脚本的其余部分。
# 你希望在查找文件名之前更新数据库。
```

```
locate $1
```
