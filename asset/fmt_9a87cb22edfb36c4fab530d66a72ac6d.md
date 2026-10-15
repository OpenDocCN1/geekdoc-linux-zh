
```
exec outfile > 2errfile
```

当你以这种方式使用 `exec` 时，当前进程不会被新进程替换，`exec` 后面可以跟随脚本中的命令。

当你将脚本的输出重定向到文件时，必须确保用户能看到脚本显示的提示。`/dev/tty` 是用户屏幕的别名，无需知道是哪个设备正在使用；你可以使用此设备来指代用户的屏幕。通过将输出重定向到 `/dev/tty`，你可以确保提示消息发送给已登录的用户。如果脚本的标准输出和标准错误被重定向，发送到 `/dev/tty` 的消息将不会被偏离。

`./screen1` 将输出发送到三个地方：标准输出、标准错误和用户屏幕。当带有重定向的标准输出和标准错误运行时，`./screen1` 仍然会将消息显示在用户屏幕的 `/dev/tty` 上。`err` 文件持有发送到标准输出和标准错误的输出。

```
$ cat to-screen1
echo "message to standard output"
echo "message to standard error" 1&2
echo "message to the user" > /dev/tty
```

```
$ ./screen1 > 2err
message to the user
$ cat out
message to standard output
$ cat err
message to standard error
```

以下命令将脚本的输出重定向到用户屏幕：

```
exec > /dev/tty
```

将此内容放在之前脚本的开头，`exec` 将标准输出重定向到用户屏幕，因此 `> /dev/tty` 是多余的。在 `exec` 命令之后，所有到标准输出的输出都会去 `/dev/tty`（终端）。到标准错误的输出不受影响。

```
$ cat to-screen2
exec > /dev/tty
echo "message to standard output"
echo "message to standard error" 1&2
echo "message to the user" > /dev/tty
```

```
$ ./screen2 > 2err
message to standard output
message to the user
```

使用 `exec` 将输出重定向到 `/dev/tty` 的缺点是，除非你在脚本中再次使用 `exec`，否则所有后续内容都将被重定向。

你也可以重定向输入以读取（标准输入），使其来自 `/dev/tty`（键盘）：

```
read name < /dev/tty
```

或者

```
exec < /dev/tty
```

# trap：捕获信号

信号是向进程报告某种条件的机制。Linux 使用信号来报告用户生成的中断（例如，按下中断键）以及糟糕的系统调用、断管道、非法指令和其他状况。`trap` 捕获（traps）一个或多个信号，允许你指定脚本在接收到特定信号时采取的行动。

本文讨论涵盖了处理 shell 脚本时重要的六种信号。表 27-5 列出了这些信号、通常附带它们的信号数字以及产生它们的条件。

表 27-5 信号

| 类型 | 名称 | 编号 | 产生条件 |
| :--- | :--- | :--- | :--- |
| 非真实信号 | EXIT | 0 | 退出或到达程序结束 |
| 挂断 | SIGHUP | 1 | 断开连接 |
| 终端中断 | SIGINT | 2 | 按下中断键 (CTRL-C) |
| 退出 | SIGQUIT | 3 | 按下退出键 (CTRL-Q) |
| 杀死 | SIGKILL | 9 | 无法捕获 |
| 软件终止 | SIGTERM | 15 | 默认命令 |
| 停止 | SIGTSTP | 20 | 按下暂停键 (CTRL-Z) |
| 调试 | DEBUG | | 每个命令执行后 |
| 错误 | ERR | | 在每个命令返回非零状态后 |

当 `trap` 捕获信号时，脚本会捕获你指定的任何操作：它可以根据需要删除文件或完成处理、显示消息、终止执行或忽略信号。如果你不在脚本中使用 `trap`，表 27-5 中列出的任何活动状态信号（EXIT 和 DEBUG 除外）都将终止脚本。由于进程无法捕获 KILL 信号，你可以使用 `kill -9` 作为最后手段来终止脚本或进程。

`trap` 命令具有以下语法：

```
trap ['commands'] [signal]
```

可选的 `commands` 指定了脚本在捕获到由 `signal` 指定信号之一时执行的命令。`signal` 可以是信号名称或数字——例如 INT 或 2。如果不存在 `commands`，则 `trap` 将重置为其初始状态，通常是退出脚本。

引号 `trap` 内置命令不需要像上述语法那样对命令加引号，但使用引号是一种良好的习惯，这样变量是在信号发生时展开，而不是在 shell 评估 `trap` 命令时展开。即使你没有使用任何 shell 变量，可能也需要对任何带参数的命令使用单双引号。引号命令会导致 shell 将整个命令作为一个单独参数传递。

执行命令后，shell 将从中断的地方继续执行脚本。如果你想让 `trap` 在接收到信号时阻止脚本退出但不显式运行任何命令，可以指定一个空（null）命令字符串，如 `locktrap` 脚本（第 975 页）所示。以下命令捕获信号数字 15 后脚本继续：

```
trap '' 15
```

以下脚本演示了 `trap` 内置命令如何捕获中断信号（2）。你可以使用 SIGINT、INT 或 2 来指定此信号。脚本返回退出状态为 1：

```
$ cat int
#!/bin/bash
trap 'echo PROGRAM INTERRUPTED; exit 1' INT
while true
do
    echo "Program running.
    sleep 1
done
$ ./int
Program running.
Program running.
Program running.
CONTROL-C
PROGRAM INTERRUPTED
$
```

# 内置命令 1011

`(null)` builtin `trap` 迭代器的第二行使用 `INT` 为终端中断信号设置陷阱（trap）。当 `trap` 捕获到信号时，shell 会执行 `trap` 命令中单引号之间的两个命令。`echo` 内置命令显示消息 "PROGRAM INTERRUPTED"，`exit` 终止脚本，而父 shell 则显示提示符。如果没有 `exit`，shell 在显示消息后会将控制权交回 `while` 循环，直到脚本接收到信号，因为 `true` 实用程序始终返回真状态。你可以使用内置命令 `:` 来替代 `true`，它被写为一个冒号，并且始终返回 0（真）。

`trap` 内置命令在脚本提前终止时经常会删除临时文件，从而确保这些文件不会留在文件系统中造成杂乱。以下 shell 脚本 `addbanner` 使用了两个 `trap`，以便在脚本正常终止或由于挂断、软件中断、退出或软件信号而终止时删除临时文件。

- *addbanner*

```bash
#!/bin/bash
script=$(basename $0)

if [ -r "$HOME/banner" ]
then
    echo "$script: need readable HOME/banner" 1>&2
    exit 1
fi
trap 'exit 1' 1 2 3 5
trap 'rm /tmp/$script 2> /dev/null' 0
for file in "$@"; do
    if [ -r "$file" -w "$file" ]
    then
        cat "$HOME/banner" "$file" > /tmp/$script
        cp /tmp/$script $file
        echo "$script: banner added to $file" 1>&2
    else
        echo "$script: need read and write permission for $file" 1>&2
    fi
done
```

当用一个或多个文件名调用时，`addbanner` 会遍历这些文件，并在每个文件的顶部添加页头。当你对文档使用标准格式（例如备忘录的标准布局），或者当你想为 shell 脚本添加标准页头时，该脚本非常有用。页头保留在一个名为 `/banner` 的文件中。由于 `addbanner` 使用了 `HOME` 变量（该变量包含用户主目录的路径），因此该脚本可以在无需修改的情况下被多个用户使用。如果 Max 在编写脚本时用 `/HOME/max` 代替 `HOME`，然后将脚本交给 Zach，那么每个 Zach 都必须修改它，否则 Zach 在运行 `addbanner` 时将使用 Max 的页头文件（假设 Zach 对该文件有读取权限）。

# 1012 第 27 章 编程 Bourne Again Shell
