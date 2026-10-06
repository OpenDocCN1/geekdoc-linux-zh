
进入`/path/to/xxx`目录，找到`xxx.json`。

你可以为未设置的变量提供默认值，但通过省略冒号，让设置为为空的变量展开为空：

```bash
ls ${LIT-HOME/literature}
```

# 分配默认值

`:-`修饰符不会改变变量的值。在脚本中你可能想将空或未设置变量的值更改为默认值。你可以使用`:=`修饰符来实现此。

```bash
${name:=default}
```

Bourne Shell 展开表达式`${name:=default}`的方式与`${name:-default}`相同，但其副作用是会将`name`的值设置为`default`展开后的值。

## 可选项（续）

当你省略`:=`中的`:`时，bash会为未设置的变量赋值，但不会为空的变量赋值。如果你的脚本包含如下行，且在执行此行时`LIT`是未设置的，则它将赋值为`/home/alex/literature`：

```bash
ls ${LIT:=/home/alex/literature}
```

bash脚本的一个常见特性是在脚本开头使用带有`:`（冒号）的内置展开修饰符来设置任何可能为空或未设置的变量。内置命令评估剩余行中的每个标记（token），但不会执行命令。如果没有开头的`:`，shell将评估并尝试执行评估结果产生的“命令”。评估顺序是：如果一个变量是一个命令且你这样命名了它，它将被执行。如果它不是有效命令，你将得到错误。

使用以下语法为空或未设置的变量设置默认值：

```bash
: ${name}:=default
```

如果你的脚本需要一个创建临时文件的目录，并使用`TEMPDIR`的值作为该目录的名称，以下行将`TEMPDIR`默认`/tmp`：

```bash
: ${TEMPDIR}:=/tmp
```

# 显示信息

有时脚本需要变量的值，而你在编写脚本时无法提供合理的默认值。在这种情况下，如果变量为空或未设置，你可以强制脚本显示错误消息并以退出状态1终止。此目的的修饰符是`:?`。

```bash
cd ${TESTDIR?=msg}
```

如果`TESTDIR`为空或未设置，bash将`msg`的展开值显示在标准错误上并终止。如果消息包含空格，脚本必须使用引号括起消息。如果你省略了`:`，则显示默认错误消息（参数未设置）。如果你省略了`:`，则只有在变量未设置时才会发生错误；空变量将展开为空字符串。

# 内置命令

许多bash脚本使用在开头带有`:`（冒号）的展开修饰符来设置任何可能为空或未设置的变量。内置命令评估剩余行中的每个标记，但不会执行命令。如果没有开头的`:`，shell将评估并尝试执行评估结果产生的“命令”。如果一个变量是一个命令且你这样命名了它，它将被执行。如果它不是有效命令，你将得到错误。

使用以下语法为空或未设置的变量设置默认值：

```bash
: ${name}:=default
```

如果你的脚本需要一个创建临时文件的目录，并使用`TEMPDIR`的值作为该目录的名称，以下行将`TEMPDIR`默认`/tmp`：

```bash
: ${TEMPDIR}:=/tmp
```

# 显示错误信息

有时脚本需要变量的值，而你在编写脚本时无法提供合理的默认值。在这种情况下，如果变量为空或未设置，你可以强制脚本显示错误消息并以退出状态1终止。此目的的修饰符是`:?`。

```bash
cd ${TESTDIR?=msg}
```

如果`TESTDIR`为空或未设置，bash将`msg`的展开值显示在标准错误上并终止。如果消息包含空格，脚本必须使用引号括起消息。如果你省略了`:`，则显示默认错误消息（参数未设置）。如果你省略了`:`，则只有在变量未设置时才会发生错误；空变量将展开为空字符串。

*(注：由于提供的英文文本后部分存在重复且逻辑断层，译文已根据上下文意图进行了对齐并保留了 Markdown 格式)*

# 400 第11 章：Shell 编程

| 信号 | 编号 | 产生条件 |
| --- | --- | --- |
| 非真实信号 | 0 | 因执行`exit`命令或到达程序末尾而退出（不是实际信号，但在`*trap*`中有用） |
| 挂断 (Hang up) | 1 | 断开电话线 |
| 终端中断 | 2 | 按中断键（通常为 CONTROL-C） |
| 退出 (Quit) | 3 | 按退出键（通常为 CONTROL-SHIFT-I 或 CONTROL-SHIFT-\） |
| 杀死 (Kill) | 9 | 使用 -9 选项的`*kill*`命令（无法被捕获） |
| 软件终止 | 15 | `kill`命令的默认值 |
| 停止 (Stop) | 20 | 按作业控制停止键（通常为 CONTROL-Z） |

信号发生时触发，而不是在 shell 评估`*trap*`的参数时触发。即使你没有在`*commands*`中使用任何变量，也需要将任何带有参数的命令用单引号或双引号括起来，以便 shell 将整个命令作为单个参数传递给`*trap*`。

`*信号数字*`是`*trap*`捕获的信号数量。`*commands*`部分是可选的。如果没有该部分，`*trap*`会将陷阱重置为初始状态，这允许你退出脚本。如果存在`*commands*`部分，shell 在捕获到其中一个信号时会执行`*commands*`。在执行完`*commands*`之后，shell 将从之前停止的地方继续执行脚本。如果你想让`*trap*`在接收信号时防止脚本意外退出，但不显式地运行任何命令，你可以使用`*trap*`配合一个`*null*`（空）内置命令，如`*locktty*`脚本（第 386 页）所示。以下命令捕获编号为 15 的信号，脚本继续运行：

```bash
trap '' 15
```

如果你在不带任何参数的情况下调用`*trap*`，该命令会列出你捕获的每个信号以及信号发生时你执行的命令。如果你带参数 -l 调用`*trap*`，该命令会列出所有信号的名称及其对应的数字。

以下脚本演示了如何使用内置命令`*trap*`捕获编号为 2 的信号。它返回退出状态 1。

```bash
bash$ cat inter
#!/bin/bash
trap 'echo PROGRAM INTERRUPTED; exit 1' 2
while true
do
    echo "Program running."
done
```

`*inter*`的第二行为编号为 2 的信号设置了陷阱。当信号被捕获时，shell 会执行`*trap*`命令中单引号之间的两个命令。内置命令`*echo*`会显示消息 PROGRAM INTERRUPTED。然后`*exit*`终止该 shell，父 shell 显示提示符。如果没有`*exit*`，shell 在显示消息后将把控制权还给`*while*`循环。

# 内置命令 Builtins 401

`*while*`循环持续重复，直到脚本接收到信号，因为`*true*`命令始终返回真状态。你可以用写为冒号（:）的空内置命令来代替`*true*`，它始终返回 0 或真状态。那么`*while*`语句应该是`while :`而不是`while true`。

当脚本提前终止时，`*trap*`经常会移除临时文件，这样文件就不会被留在那里占用文件系统。

以下 shell 脚本 `addbanner` 使用两个`*trap*`，在脚本正常终止或因挂断、软件中断或软件终止信号时移除临时文件。

```bash
bash$ cat addbanner
#!/bin/bash
script=$(basename $0)
if [ ! -r "$HOME/banner" ]
then
    echo "$script: need readable $HOME/banner "
    "$file" 1>&2
    exit 1
fi
trap 'exit 1 2 3 15'
trap 'rm /tmp/$.$.script 2>/dev/null'
for file
do
    if [ -r "$file" -a w "$file" ]
    then
        cat $HOME/banner $file > /tmp/$.$.script
        cp /tmp/$.$.script $file
        echo "$script: banner added to $file" 1>&2
    else
        echo "$script: need read and write "
        "permission for $file" 1>&2
    fi
done
```

当带一个或多个文件名参数调用时，`addbanner`会遍历这些文件，并在每个文件的顶部添加头部。当你对备录使用标准格式，或想为 shell 脚本添加标准头部时，此脚本非常有用。头部存储在用户主目录下一个名为 `banner` 的文件中。`HOME`变量包含用户主目录的路径，因此 `addbanner` 可以在不修改的情况下被多个用户使用。如果 Alex 在编写脚本时使用的是 `/home/alex` 而不是 `$HOME`，并将脚本生成给 Jenny，那么要么 Jenny 必须修改它，要么在 Jenny 运行时，`addbanner` 会使用 Alex 的 `banner` 文件。

`addbanner` 中的第一个`*trap*`导致它在接收到挂断中断（终端中断或退出信号）或软件终止信号时以状态 1 退出。第二个`*trap*`在信号编号中使用 0，这导致每当脚本因 `exit` 命令或到达末尾而退出时，`*trap*`都会执行其命令参数。这两个陷阱共同在脚本正常或提前终止时移除临时文件。第二个`*trap*`的标准错误被重定向到 `/dev/null`，以防止`*trap*`尝试移除不存在的临时文件。在这些情况下，`rm`会向标准错误发送错误消息。

# 402 第11 章：Shell 编程

内置命令部分列表

下面是某些内置命令的列表。

| 内置命令 | 功能 |
| --- | --- |
| `.` | 执行程序或 shell 脚本 |
| `alias` | 给命令起名 |
| `bg` | 将作业放入后台 |
| `break` | 退出 for, while, until 循环 |
| `cd` | 目录 |
| `continue` | 继续 for, while, until 循环 |
| `declare` | 为变量声明属性 |
| `dirs` | 列出目录栈；参见 `pushd` 和 `popd` |
| `echo` | 显示参数 |
| `eval` | 扫描并执行行 |
| `exec` | 替换当前 |
| `exit` | 退出 shell（通常通过 CONTROL-D） |
| `export` | 将变量值放入环境变量 |
| `fc` | 查看、编辑并执行历史命令 |
| `fg` | 将作业调前台 |
| `getopts` | 解析参数 |
| `hash` | 记住路径中命令的位置 |
| `help` | 显示内置命令的帮助信息 |
| `history` | 显示历史命令 |
| `jobs` | 显示前台和后台作业 |
| `kill` | 向进程发送信号 |
| `let` | 计算数值表达式 |

# 函数 403

| 内置命令 | 功能 |
| --- | --- |
| `pop` | 弹出目录栈顶端目录并切换 |
| `pushd` | 将参数推入目录栈顶端并切换 |
| `pwd` | 打印工作目录名称 |
| `read` | 从标准输入读取行 |
| `readonly` | 将变量声明为只读 |
| `return` | 退出函数 |
| `set` | 设置 标志或命令行变量；不带参数时显示所有变量 |
| `shift` | 移动每个命令行参数 |
| `test` | 比较参数 |
| `time` | 显示当前 shell 子进程的时间 |
| `trap` | 捕获信号 |
| `type` | 显示每个参数将如何解释为命令 |
| `typeset` | 为变量声明属性（同 `declare`） |
| `umask` | 文件创建掩码 |
| `alias` | 移除别名 |
| `unset` | 移除变量或函数 |
| `wait` | 等待后台进程终止 |

# 404 第 11 章：Shell 编程

用于声明 Shell 函数的语法如下

```bash
function-name ()
{
  commands
}
```

`function-name`是你要调用函数时使用的名称。`commands`包含了在调用函数时执行的命令列表。这些命令可以包含任何你可以放入 Shell 脚本中的的内容，包括对函数的调用。

下一个示例展示了如何创建一个简单的函数，用于显示日期、标题以及正在使用系统的用户列表。该函数运行的与第 303 页描述的 `whoson` 脚本相同的命令。

```bash
bash$ whoson ()
  date
  echo "Users Currently Logged In"
  who
bash$ whoson
Thu Jun 12 09:51:09 PDT 1997
Users Currently Logged In
hls     console Jun 16 08:59
alex     tty20    Jun 16 09:33
jenny   tty24   Jun 16 09:23
```

如果你希望 `whoson` 函数始终可用，而无需每次登录时都输入它，请将其定义放在你的 `.bash_profile` 文件中。在 `.bash_profile` 中添加 `whoson` 后，使用 `.`（点）命令运行 `.bash_profile` 以立即使生效。关于 `.bash_profile` 的更多信息，请参阅第 72 页。

```bash
bash$ cat .bash_profile
TERM=vt100
export TERM
stty kill '^Au'
whoson ()
{
  date
  echo "Users Currently Logged In"
  }
bash$ .bash_profile
```

在调用函数时可以指定参数。在函数内部，这些参数以位置参数的形式存在。下一个函数允许你使用 `grep` 在历史列表中搜索特定事件。然后你可以可以确保给了正确的命令、重新执行该事件，或修改并重新执行该事件（第 359 页）。以下示例使用 `.` 命令实现了该函数，并展示了如何在历史列表中搜索所有的 `chmod` 命令。即使你没有在提示符中包含它们，也可以看到并使用事件编号。

```bash
bash$ A hg
hg() {
  history | grep -i "$1"
  .
  hg
}
14 chmod 644 README
56 chmod 755 program1
98 man chmod
```

接下来的函数允许你使用 System UNIX 下的 C shell 提供的 Linux 下的 tcsh 语法来导出变量。`printenv` 实用程序列出所有环境变量及其值，并验证 `setenv` 是否正常工作。

```bash
bash$ cat .bash_profile
# setenv keep csh and tcsh users
setenv()
if [ $# -eq 2 ]
then
  eval $1=$2
  export $1
else
  echo "Usage: setenv NAME VALUE" 1>&2
fi
bash$ .bash_profile
bash$ setenv TCL_LIBRARY /usr/local/lib/tcl
bash$ printenv | grep TCL_LIBRARY
TCL_LIBRARY=/usr/local/lib/tcl
```
