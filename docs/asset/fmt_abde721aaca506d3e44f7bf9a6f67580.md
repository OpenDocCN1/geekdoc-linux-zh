
如果脚本在运行期间收到中断，`trap` 命令允许你以多种方式处理中断信号。你可以让信号正常（默认）表现，忽略该信号，或创建一个在信号到达时调用的处理函数。

诸如 `HUP` 和 `INT` 之类的信号名称通常以 `SIG` 作为前缀，例如 `SIGHUP`、`SIGINT` 等。`bash` shell 允许你使用信号的符号名称，即不带 `SIG` 前缀的信号名称，或者使用信号的数值。参见表 14.6。伪信号名称 `EXIT` 或数字 `0` 将在 shell 退出时导致 `trap` 被执行。

## 14.8.1 重置信号

要将信号重置为其默认行为，请在 `trap` 命令后跟信号名称或编号。在函数中设置的 `trap` 一旦函数被调用，就会被调用该函数的 shell 识别。在函数外部设置的任何 `trap` 也会在函数中被识别。

### 示例 14.62

```
trap INT
```

**说明：**

将信号 2（`SIGINT`）的默认操作重置。默认操作是在按下中断键（Ctrl-C）时杀死进程。

### 示例 14.63

```
trap 2
```

**说明：**

将信号 2（`SIGINT`）的默认操作重置，该信号用于杀死进程（即 Ctrl-C）。

### 示例 14.64

```
trap 'trap 2' 2
```

**说明：**

将信号 2（`SIGINT`）的默认操作设置为在信号到达时执行引号内的命令字符串。用户必须按两次 Ctrl-C 才能终止程序。第一个 `trap` 捕获信号，第二个 `trap` 将 `trap` 重置为其默认操作，即杀死进程。

## 14.8.2 忽略信号

如果 `trap` 命令后面跟一对空引号，则列出的信号将被进程忽略。

### 示例 14.65

```
trap "" 1 2 or trap "" HUP INT
```

**说明：**

信号 1（`SIGHUP`）和 2（`SIGINT`）将被 shell 进程忽略。

## 14.8.3 列出 `trap`

要列出所有 `trap` 及其分配的命令，请键入 `trap`。

### 示例 14.66

```
(At the command line)
1  $ trap 'echo "Caught ya!; exit"' 2
2  $ trap
trap -- 'echo "Caught ya!; exit 1"' SIGINT
3  $ trap -
```

**说明：**

+   1 `trap` 命令被设置为在信号 2（Ctrl-C）时退出。

+   2 不带参数的 `trap` 命令列出所有已设置的 `trap`。

+   3 如果参数是短横线（-），所有信号都将重置为原始值，即 shell 启动时的值。

### 示例 14.67

```
(The Script)
#!/bin/bash
# Scriptname: trapping
# Script to illustrate the trap command and signals
# Can use the signal numbers or bash abbreviations seen
# below. Cannot use SIGINT, SIGQUIT, etc.
1  trap 'echo "Ctrl-C will not terminate $0."' INT
2  trap 'echo "Ctrl-\ will not terminate $0."' QUIT
3  trap 'echo "Ctrl-Z will not terminate $0."' TSTP
echo "Enter any string after the prompt."
When you are ready to exit, type \"stop\"."
```

### 示例 14.67（续）

```
5 while true
6 do
7 echo -n "Go ahead..."
8 read
9 if [[ $REPLY == [Ss]top ]]
10 then
    break
fi
done
```

（输出）

```
4 Enter any string after the prompt.
When you are ready to exit, type "stop".
6 Go ahead... this is it^C
1 Ctrl-C will not terminate trapping.
6 Go ahead... this is it again^Z
3 Ctrl-Z will not terminate trapping.
6 Go ahead... this is never it^\ 
2 Ctrl-\ will not terminate trapping.
6 Go ahead... stop
$
```

**解释：**

- 1 第一个 `trap` 命令捕获 `INT` 信号，即 Ctrl-C。如果在程序运行期间按下 Ctrl-C，将执行引号内的命令。程序不会中止，而是打印“Ctrl-C will not terminate trapping”并继续提示用户输入。

- 2 第二个 `trap` 命令将在用户按下 Ctrl-\（即 `QUIT` 信号）时执行。程序会显示“Ctrl-\ will not terminate trapping”并继续运行。默认情况下，该信号（`SIGQUIT`）会终止进程并生成核心转储文件。

- 3 第三个 `trap` 命令将在用户按下 Ctrl-Z（即 `TSTP` 信号）时执行。程序会显示“Ctrl-Z will not terminate trapping”并继续运行。如果启用了作业控制，该信号通常会导致程序在后台挂起。

- 4 提示用户输入。

- 5 进入 `while` 循环。

- 6 打印字符串“Go ahead...”，然后程序等待输入（参见下一行的 `read`）。

- 7 `read` 命令将用户输入赋值给内置变量 `REPLY`。

**解释（续）：**

8 如果 `REPLY` 的值与“Stop”或“stop”匹配，`break` 命令将使循环退出，程序终止。除非用 `kill` 命令杀死，否则输入“Stop”或“stop”是退出此程序的唯一方式。

9 `break` 命令使循环体退出。

10 `done` 关键字标记循环的结束。

## 14.8.4 `trap` 与函数

如果在函数中使用 `trap` 来处理信号，那么一旦函数被调用，它就会影响整个脚本。`trap` 对脚本来说是全局的。在下面的示例中，`trap` 被设置为忽略中断键 ^C。这个脚本必须用 `kill` 命令杀死才能停止循环。这演示了在函数中使用 `trap` 时可能产生的不良副作用。

### 示例 14.68

```
(The Script)
#!/bin/bash
1 function trapper () {
    echo "In trapper"
2   trap "echo 'Caught in a trap!'" INT
    # Once set, this trap affects the entire script. Anytime
    # ^C is entered, the script will ignore it.
3 }
    while :
    do
        echo "In the main script"
4       trapper
5       echo "Still in main"
6       echo "The pid is $$"
        sleep 5
7   done
```

```
(The Output)
In the main script
In trapper
Still in main
The pid is 4267
Caught in a trap!      # User presses ^C
```

### 示例 14.68（续）

```
In the main script
In trapper
Still in main
The pid is 4267
Caught in a trap!      # User just pressed Ctrl-C
In the main script
```

**解释：**

- 1. 定义了 `trapper` 函数。函数中设置的所有变量和 `trap` 都是脚本全局的。

- 2. `trap` 命令将忽略 `INT` 信号（信号 2，即中断键 ^C）。如果按下 ^C，将打印消息“Caught in a trap!”，脚本将永远继续执行。可以使用 `kill` 命令或 Ctrl-\ 杀死该脚本。

- 3. 主脚本开始一个无限循环。

- 4. 调用 `trapper` 函数。

- 5. 当函数返回时，执行从这里开始。

- 6. 将显示 PID。之后，你可以在另一个终端中使用该编号来杀死进程。例如，如果 PID 是 4267，执行 `kill 4267` 将终止该进程。

- 7. 程序暂停（休眠）5 秒。

## 14.9 调试

通过使用 `bash` 命令的 `-n` 选项，你可以在不实际执行任何命令的情况下检查脚本的语法。如果脚本中存在语法错误，shell 将报告错误。如果没有错误，则不会显示任何内容。
