
类似地，以下命令将标准输出和标准错误分别重定向到 outfile 和 errfile：

```
exec > outfile 2> errfile
```

当你以这种方式使用 **exec** 时，当前进程不会被新进程替换，并且 **exec** 之后可以跟随脚本中的其他命令。

## /dev/tty

当你将脚本的输出重定向到文件时，必须确保用户能看到脚本显示的任何提示。/dev/tty 设备是用户当前工作屏幕的别名；你可以使用此设备来引用用户的屏幕，而无需知道具体是哪个设备。（`tty` 实用程序会显示你正在使用的设备名称。）通过将脚本的输出重定向到 /dev/tty，你可以确保无论用户登录在哪个终端上，提示信息和消息都会发送到用户的终端。即使脚本的标准输出和标准错误被重定向，发送到 /dev/tty 的消息也不会被分流。

`to_screen1` 脚本将输出发送到三个地方：标准输出、标准错误以及用户的屏幕。当标准输出和标准错误被重定向时运行 `to_screen1`，发送给 /dev/tty 的消息仍会在用户的屏幕上显示。`out` 和 `err` 文件分别保存发送到标准输出和标准错误的输出。

```
$ cat to_screen1
echo "message to standard output"
echo "message to standard error" 1>&2
echo "message to the user" > /dev/tty
```

```
$ ./to_screen1 > out 2> err
message to the user
$ cat out
message to standard output
$ cat err
message to standard error
```

以下命令将脚本的输出重定向到用户的屏幕：

```
exec > /dev/tty
```

将此命令放在上一个脚本的开头，会改变输出的去向。在 `to_screen2` 中，`exec` 将标准输出重定向到用户的屏幕，因此 > /dev/tty 是多余的。在执行了 `exec` 命令后，所有发送到标准输出的输出都会进入 /dev/tty（屏幕）。发送到标准错误的输出不受影响。

```
$ cat to_screen2
exec > /dev/tty
echo "message to standard output"
echo "message to standard error" 1>&2
echo "message to the user" > /dev/tty
```

```
$ ./to_screen2 > out 2> err
message to standard output
message to the user
```

使用 `exec` 将输出重定向到 /dev/tty 的一个缺点在于，除非你在脚本中再次使用 `exec`，否则后续的所有输出都会被重定向。

你还可以将输入重定向到 **read**（标准输入），使其来自 **/dev/tty**（键盘）：

```
read name < /dev/tty
```

*或者*

```
exec < /dev/tty
```

## trap：捕获信号

*信号* 是关于某种状态发送给进程的报告。Linux 使用信号来报告用户生成的中断（例如，按下中断键），以及糟糕的系统调用、管道破裂、非法指令和其他状态。**trap** 内置命令捕获（trap）一个或多个信号，允许你指定脚本在接收到特定信号时执行的操作。

本讨论涵盖了在处理 shell 脚本时重要的六个信号。表 27-5 列出了这些信号、系统通常分配给它们的信号号，以及通常生成每个信号的状态。输入命令 **kill -l**（小写“ell”）、**trap -l**（小写“ell”）或 **man 7 signal** 以显示所有信号名称的列表。

### 表 27-5 \ 信号

| 类型 | 名称 | 编号 | 生成条件 |
|---|---|---|---|
| 非真实信号 | EXIT | 0 | 因 exit 命令或程序结束而退出（不是实际的信号，但在 trap 中很有用） |
| 挂起 | SIGHUP 或 HUP | 1 | 断开线路 |
| 终端中断 | SIGINT 或 INT | 2 | 按下中断键（通常是 CONTROL-C） |
| 退出 | SIGQUIT 或 QUIT | 3 | 按下退出键（通常是 CONTROL-\）或 CONTROL-] |
| 杀死 | SIGKILL 或 KILL | 9 | 带有 -9 选项的 kill 内置命令（无法被捕获；仅作为最后手段使用） |
| 软件终止 | SIGTERM 或 TERM | 15 | kill 命令的默认值 |
| 停止 | SIGTSTP 或 TSTP | 20 | 按下暂停键（通常是 CONTROL-Z） |
| 调试 | DEBUG | | 在每个命令后执行 **trap** 语句中指定的 **commands**（不是实际的信号，但在 trap 中很有用） |
| 错误 | ERR | | 在每个返回非零退出状态的命令后执行 **trap** 语句中指定的 **commands**（不是实际的信号，但在 trap 中很有用） |

当脚本捕获信号时，它会执行你指定的任何操作：它可以根据需要删除文件或完成其他处理、显示消息、立即终止执行或忽略信号。如果你不在脚本中使用 trap，表 27-5 中列出的六个实际信号中的任何一个（不包括 EXIT、DEBUG 或 ERR）都将终止脚本。因为进程无法捕获 KILL 信号，你可以将 kill -KILL（或 kill -9）作为终止脚本或其他进程的最后手段。（有关 kill 的更多信息，请参见第 1012 页。）

trap 命令具有以下语法：

```
trap ['commands'] [signal]
```

可选的 commands 指定了当 shell 捕获由 signal 指定的信号之一时执行的命令。signal 可以是信号名称或编号——例如，INT 或 2。如果不存在 commands，trap 会将陷阱重置为其初始状态，这通常是从脚本退出。

### 引号

前面的语法表明，trap 内置命令不要求使用单引号括起 commands，但使用单引号是一种良好的实践。单引号使得 commands 中的 shell 变量在信号发生时进行扩展，而不是在 shell 评估 trap 的参数时进行扩展。即使你在 commands 中没有使用任何 shell 变量，也需要将任何接受参数的命令包裹在单引号或双引号内。对 commands 加引号会使 shell 将整个命令作为单个参数传递给 trap。

执行完 commands 后，shell 从暂停处继续执行脚本。如果你希望 trap 在接收到信号时防止脚本退出，但不想显式运行任何命令，你可以指定一个空（null）的 commands 字符串，如 locktty 脚本（第 975 页）所示。以下命令捕获编号为 15 的信号，之后脚本继续执行：

```
trap '' 15
```

以下脚本演示了 trap 内置命令如何捕获终端中断信号（2）。你可以使用 SIGINT、INT 或 2 来指定此信号。该脚本返回退出状态 1：

```
$ cat inter
#!/bin/bash
trap 'echo PROGRAM INTERRUPTED; exit 1' INT
while true
do
    echo "Program running."
    sleep 1
done
$ ./inter
Program running.
Program running.
Program running.
CONTROL-C
PROGRAM INTERRUPTED
$
```

### :（null）内置命令

`inter` 的第二行使用 `INT` 设置了针对终端中断信号的陷阱。当 `trap` 捕获该信号时，shell 执行 `trap` 命令中单引号内的两条命令。`echo` 内置命令显示消息 **PROGRAM INTERRUPTED**，`exit` 终止运行脚本的 shell，父 shell 显示提示符。如果没有 `exit`，shell 在显示消息后会将控制权返回给 `while` 循环。`while` 循环会持续重复，直到脚本接收到信号，因为 `true` 实用程序总是返回 `true` 退出状态。你可以用 `: (null)` 内置命令代替 `true`，它写作冒号，并且总是返回 `0 (true)` 状态。

`trap` 内置命令经常在脚本过早终止时删除临时文件，从而确保文件不会残留并弄乱文件系统。以下 shell 脚本名为 `addbanner`，使用两个陷阱在脚本正常终止或因挂起、软件中断、退出或软件终止信号而终止时删除临时文件：

```bash
$ cat addbanner
#!/bin/bash
script=$(basename $0)

if [ ! -r "$HOME/banner" ]
then
	echo "$script: need readable $HOME/banner file" 1>&2
	exit 1
fi

trap 'exit 1' 1 2 3 15
trap 'rm /tmp/$$.$script 2> /dev/null' 0

for file
do
	if [ -r "$file" -a -w "$file" ]
	then
		cat $HOME/banner $file > /tmp/$$.$script
		cp /tmp/$$.$script $file
		echo "$script: banner added to $file" 1>&2
	else
		echo "$script: need read and write permission for $file" 1>&2
	fi
done
```

当调用 `addbanner` 并带有一个或多个文件名参数时，`addbanner` 会遍历这些文件，在每个文件的顶部添加页眉。当你使用标准格式作为文档顶部时，例如备忘录的标准布局，或者当你想为 shell 脚本添加标准页眉时，此脚本非常有用。页眉保存在名为 `~/.banner` 的文件中。由于 `addbanner` 使用了包含用户主目录路径名的 `HOME` 变量，因此该脚本可以供多个用户使用而无需修改。如果 Max 使用 `/home/max` 代替 `HOME` 编写了脚本，然后将脚本交给 Zach，那么要么 Zach 必须修改它，要么当 Zach 运行 `addbanner` 时会使用 Max 的 `banner` 文件（假设 Zach 对该文件有读取权限）。

