
## 示例 14.67（续）

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

## 解释

- 1 第一个 trap 命令捕获 INT 信号，即 Ctrl-C。如果在程序运行期间按下 Ctrl-C，将执行引号内的命令。程序不会中止，而是打印“Ctrl-C will not terminate trapping”并继续提示用户输入。
- 2 第二个 trap 命令将在用户按下 Ctrl-\（即 QUIT 信号）时执行。程序会显示“Ctrl-\ will not terminate trapping”并继续运行。默认情况下，该信号（SIGQUIT）会终止进程并生成核心转储文件。
- 3 第三个 trap 命令将在用户按下 Ctrl-Z（即 TSTP 信号）时执行。程序会显示“Ctrl-Z will not terminate trapping”并继续运行。如果启用了作业控制，该信号通常会导致程序在后台挂起。
- 4 提示用户输入。
- 5 进入 while 循环。
- 6 打印字符串“Go ahead...”，然后程序等待输入（参见下一行的 read）。
- 7 read 命令将用户输入赋值给内置变量 REPLY。

## 解释（续）

8 如果 REPLY 的值与“Stop”或“stop”匹配，break 命令将使循环退出，程序终止。除非用 kill 命令杀死，否则输入“Stop”或“stop”是退出此程序的唯一方式。

9 break 命令使循环体退出。

10 done 关键字标记循环的结束。

## 14.8.4 trap 与函数

如果在函数中使用 trap 来处理信号，那么一旦函数被调用，它就会影响整个脚本。trap 对脚本来说是全局的。在下面的示例中，trap 被设置为忽略中断键 ^C。这个脚本必须用 kill 命令杀死才能停止循环。这演示了在函数中使用 trap 时可能产生的不良副作用。

## 示例 14.68

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

## 示例 14.68（续）

```
In the main script
In trapper
Still in main
The pid is 4267
Caught in a trap!      # User just pressed Ctrl-C
In the main script
```

## 解释

- 1. 定义了 `trapper` 函数。函数中设置的所有变量和 trap 都是脚本全局的。
- 2. `trap` 命令将忽略 INT 信号（信号 2，即中断键 ^C）。如果按下 ^C，将打印消息“Caught in a trap!”，脚本将永远继续执行。可以使用 `kill` 命令或 Ctrl-\ 杀死该脚本。
- 3. 主脚本开始一个无限循环。
- 4. 调用 `trapper` 函数。
- 5. 当函数返回时，执行从这里开始。
- 6. 将显示 PID。之后，你可以在另一个终端中使用该编号来杀死进程。例如，如果 PID 是 4267，执行 `kill 4267` 将终止该进程。
- 7. 程序暂停（休眠）5 秒。

## 14.9 调试

通过使用 `bash` 命令的 `-n` 选项，你可以在不实际执行任何命令的情况下检查脚本的语法。如果脚本中存在语法错误，shell 将报告错误。如果没有错误，则不会显示任何内容。

最常用的脚本调试方法是使用带 `-x` 选项的 `set` 命令，或者使用 `-x` 选项及脚本名调用 `bash`。调试选项列表参见表 14.7。这些选项允许对脚本进行执行跟踪。脚本中的每个命令都会在执行替换后显示出来，然后执行该命令。当脚本中的某一行被显示时，其前面会带有一个加号（+）标志。

打开 verbose 选项，或使用 `-v` 选项调用 shell（`bash -v 脚本名`）时，脚本中的每一行都会按照脚本中键入的原样显示，然后执行。（详见第 967 页第 15 章“调试 Shell 脚本”。）

