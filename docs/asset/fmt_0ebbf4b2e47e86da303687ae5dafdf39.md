
# 高级 Bash 脚本指南

## 示例 15-14. 强制注销

```bash
#!/bin/bash

# 杀死 ppp 以强制注销。
# 当然，对于拨号连接。
# 脚本应作为 root 用户运行。

SERPORT=tty3

# 取决硬件甚至内核版本，
# 你的机器上的调制调器端口可能不同
# /dev/ttyS1 /dev/ttyS2。

killpp="kill -9 \$ps aux | awk '/ppp/ { print \$1 }'"

# ------ ppp 的进程 ID
```

```bash
$killpp      # 此变量现在是一个命令。
```

以下操作必须作为 `root` 用户执行。

```bash
chmod 666 /dev/$SERPORT # 恢复读写权限，否则呢？
# 因为对 ppp 进行操作会更改串口的权限，
# 我们将权限恢复到之前的状态。

rm /var/lock/LOCK.$SERPORT # 串口锁文件。为什么？
exit $?
```

## 示例 15. 内部命令与内置命令

### 示例 15-15. `rot13` 的版本

```bash
#!/bin/bash

# 使用 'eval' 的 "rot13" 版本。
# 与 "rot13.sh" 示例对比。

setvar_rot_13() {      # "rot13" 乱码
{
  local varname=$1 value=$2
  eval $varname='$(echo \$value | tr a-z n-a-m)'
}

setvar_rot_13 "foobar"      # 通过 rot13 运行 "foobar"。
echo $var

setvar_rot_13 var "$var"    # 通过 rot13 运行 "sbbone"。
# 回到原始变量。
echo $var
}
```

# 此示例由 Stephane Chelas 提供。由文档作者修改。

```bash
exit 0
```

这里是另一个使用 `eval` 评估复杂表达式的示例，这个来自 `Yong` 的俄罗斯方块游戏的早期版本。

```bash
eval ${1+="\x${y}}"}
```

### 示例 15-16. 使用 `set` 配合位置参数

```bash
#!/bin/bash

## set-test.sh
# 使用三个命令行参数调用此脚本，例如 "set.sh one three"。

echo "set 之前的位置参数:"
echo -a
echo "命令行参数 #1 = $1"
echo "命令行参数 #2 = $2"
```

在上下文中，未声明的变量和未设置的变量是等价的。然而，`S[parameter:-default]` 参数替换结构可以区分这两者。

`export [file]` 命令使变量对正在运行的脚本或 `shell` 的所有子进程均可用。`export` 命令的一个重要用途是在启动文件中，用于初始化并使随后的用户进程能够访问环境变量。

遗憾的是，没有办法可以将变量导出到父进程（即调用或启动该 `shell` 的进程）。

### 示例 15-20. 使用 `export` 将变量传递给嵌入的 `awk` 脚本

```bash
#!/bin/bash

# "列总和器" (column totaler) 脚本 (col-totaler.sh) 的另一个版本
#++ 在目标文件中添加指定的列（数字列）。
# 此处使用环境变量将脚本变量传递给 'awk' . . .
# 并将 awk 脚本存放在一个变量中。

ARGS=2
E_WRONGANGS=85

if [ $# -ne "$ARGS" ] # 检查命令行参数是否正确。
then
    echo "Usage: basename $0 column-number"
    exit $E_WRONGANGS
fi

filename=$1
column_number=$2

n###### 与原始脚本相同，到此为止 -----

export column_number

# 将列数导出到环境变量，以便检索。
#

awkscript='total += $ENVIRON["column_number"]'
END { print "total" }

# 是的，变量可以包含一个 awk 脚本。
#

# 现在运行 awk 脚本。
awk "$awkscript" "$filename"

# 感谢 Stephane Chazelas。
```

可以在操作中初始化并导出变量，例如 `export var1=xxx`。

然而，正如 `Greg Keraunen` 指出的，在某些情况下，这种做法与先设置变量再导出的效果可能不同。

```bash
bash$ export var=(a b); echo ${var[0]}
(a b)
```

需要导出的变量可能需要特殊处理。参见示例 M-2。

### `declare`, `typeset`

`declare` 和 `typeset` 命令指定并限制变量的属性。

`readonly`

等同于 `declare -r`，将变量设置为只读，或者实际上将其视为常量。尝试更改时会带上错误信息。这相当于 C 语言中的 `const` 类型限定符。

`getopts` 这个强大的工具用于解析给脚本的命令行参数。它是 `Bash` 中对应 `getopt` 外部命令以及 C 程序员熟悉的 `getopt` 库函数的等价物。它会将多个选项 [62] 以及关联参数打印并合并到脚本中（例如 `scriptname -abc -usr/local`）。

`getopt` 构建了两个隐式变量。`$OPTIND` 是参数指针 (`OPTIndex`)，`$OPTARG` (`OPTArgument`) 是附加在选项上的（可选）标签。声明标签后的冒号表示该选项具有关联参数。

一个 `getopt` 结构通常封装在一个 `while` 循环中，该循环逐个处理选项和参数，然后增加 `$OPTIND` 变量以指向下一个。

1. 命令行参数必须以横杠 (`-`) 开头。这种前缀让 `getopt` 将命令行参数识别为选项。事实上，`gets` 不处理没有 `--` 前缀的参数，并在遇到第一个缺少该前缀的参数时终止选项处理。
2. `gets` 模板与标准的 `while` 循环略有不同，因为它缺少条件括号。
3. `gets` 结构是传统 `getopt` 外部命令的高功能替代品。

```bash
while getopt ":abc:fg" Option
# 初始声明。
# 期望的选项（标志）是 a, b, c, d, e, f 和 g。

# 选项 'e' 后的冒号显示它将有一个传递的参数。
do
case $OPTIND in
  a) # 执行某些操作
  b) # 执行某些操作。
  e) # 执行某些操作。
  g) # 执行某些操作。
esac
done

shift $((OPTIND - 1))

# 移动指针以指向下一个。
```

### 示例 15-24. `exec` 的影响

```bash
#!/bin/bash
echo echo "Exiting \$0" at line $LINENO."  # 在此处退出脚本。
# $LINENO 是一个表示其所在行号的内部变量。

# 以下行永远不会执行。
echo "这条 echo 无法回显。"
exit 99      # 此脚本不会退出。
# 在脚本终止后用 'echo' 检查退出值。
# 它将“不会”这样。
```

**示例 15-25. 一个执行自身的脚本**

```bash
#!/bin/bash
## self-exec.sh

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

`exec` 还用于分配文件描述符。例如，`exec <zzz-file` 将 `stdin` 替换为文件 `zzz-file`。`find` 与动态更改 `shell` 选项的内置命令不同（参见示例 25-1）。它经常出现在 `Bash` 启动文件中，但也使用版本 2 或更高版本通过 `'cd'` 查找缺失的目录名称。

```bash
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

`true`
一个返回成功（零）退出状态但什么都不做的命令。

```bash
bash$ true
bash$ echo $?
0
```

# 无限循环

```bash
while true
do
  operation-1
  operation-2
  operation-n
  # 需要一种跳出循环的方法，否则将挂挂。
done
```

`false`

一个返回非零退出状态但什么都不做的命令。

```bash
bash$ false
bash$ echo $?
1
```

# 测试 "false"

```bash
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
```

`type [cmd]`

与外部命令 `which` 类似，`type cmd` 识别 "cmd"。与 `which` 不同，`type` 是一个 `Bash` 内置命令。`-a` 选项显示标识关键字和内置命令，并定位具有相同名的系统命令。

```bash
bash$ type 'f'
# 是一个 shell 内置命令
bash$ type -a 'f'
# 是一个 shell 内置命令
# 是 /usr/bin/
bash$ type type
type 是一个 shell 内置命令
```

`type` 命令对于测试某个命令是否存在非常有用。

`hash [cmds]`
