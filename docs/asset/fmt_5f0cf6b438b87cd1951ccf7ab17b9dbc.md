
| T | 501 | 2456 | 2431 | 80 | 80 | 0 | | | | | | |

| R | 501 | 2431 | 2430 | 80 | 80 | 0 | | | pts/0 | 00:00:00 | bash |

实际上，根据提供的提供的 OCR 文本：

| F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| S | 501 | 2431 | 2430 | 80 | 80 | 0 | 27118 | wait | pts/0 | 00:00:00 | bash |

| T | 501 | 2456 | 2431 | 80 | 80 | 0 | | | | | | |

| R | 501 | 2431 | 2430 | 80 | 80 | 0 | | | pts/0 | 00:00:00 | bash |

（注：表格行的 OCR 文本已损坏/交叉；我已根据标准的 `ps` 输出模式和提供的片段进行了重构。）

正如你可能注意到的，shell 将这些信号传递给你的 shell 脚本进行处理。然而，`bash` 脚本的默认行为并不控制这些信号，这会对脚本的运行产生不利影响。为了避免这种情况，你可以编写脚本来识别信号并执行命令，为信号带来的后果做好准备。

# 生成信号

`bash` shell 允许你通过键盘上的组合键生成两种基础的 Linux 信号。当你需要停止或暂停一个失控的进程时，这个功能非常有用。

### 中断进程

`Ctrl+C` 组合会生成 `SIGINT` 信号并将其发送到当前 shell 中运行的所有进程。你可以通过运行一个通常需要长时间完成的命令，然后按下 `Ctrl+C` 组合键来测试：

```bash
$ sleep 100
^C
```

`Ctrl+C` 组合键发送 `SIGINT` 信号，它仅仅是停止 shell 中运行的当前进程。`sleep` 命令会暂停 shell 的操作指定的秒数并返回 shell 提示符。通过在时间到达前按下 `Ctrl+C` 组合键，`sleep` 命令提前终止。

# 暂停进程

与其终止进程，不如你可以在它执行任何操作的中间将其暂停。有时，这可能是危险的（例如，如果脚本对关键系统文件打开了文件锁），但通常它允许你在不实际终止进程的情况下查看脚本正在执行的内容。

`Ctrl+Z` 组合会生成 `SIGSTOP` 信号，停止 shell 中运行的任何进程。停止进程与终止进程是不同的。停止进程会让程序留在内存中，并能够从停止的地方继续运行。在本章稍后的“控制作业”部分中，你将学习如何重启一个已停止的进程。

当你使用 `Ctrl+Z` 组合键时，shell 会通知你进程已停止：

```bash
$ sleep 100
[1]+ Stopped sleep 100
$
```

方括号中的数字是 shell 分配的任务号。shell 将 shell 中运行的每个进程称为一个“作业”`job`，并在当前 shell 中为每个作业分配一个唯一的作业号。它将第一个启动的进程分配作业号 1，第二个分配作业号 2，依此类推。

如果你的 shell 会话中有一个已停止的作业，当你尝试退出 shell 时，`bash` 会警告你：

```bash
$ sleep 100
[1]+ Stopped sleep 100
$ exit
exit: There are stopped jobs.
$
```

你可以使用 `ps` 命令查看已停止的作业：

```bash
$ sleep 100
[1]+ Stopped sleep 100
$ ps -l
```

# 第二部分：Shell 脚本基础

（由于原文存在大量重复OCR错误，此处保留核心逻辑翻译）

| F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| S | 501 | 2431 | 2430 | 80 | 80 | 0 | 27118 | wait | pts/0 | 00:00:00 | bash |

| T | 501 | 2456 | 2431 | 80 | 80 | 0 | | | | | | |

| R | 501 | 2431 | 2430 | 80 | 80 | 0 | | | pts/0 | 00:00:00 | bash |

（注：原文中包含大量重复的错误和杂乱的文本，已根据要求提取核心内容并完成翻译。）

# 第 16 章：脚本控制

```bash
#
count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 1
    count=$[$count + 1 ]
done
#
trap 'echo I modified the trap!' SIGINT
#
count=1
while [ $count -le 5 ]
do
    echo "Second Loop #$count"
    sleep 1
    count=$[$count + 1 ]
done
#
$
```

在信号捕获 `trap` 被修改后，脚本将以不同的方式管理信号。如果在修改 `trap` 之前接收信号，脚本将按照原始的 `trap` 命令处理它：

```bash
$ ./test3.sh
Loop #1
Loop #2
Loop #3
^C Sorry... Ctrl-C is trapped.
Loop #4
Loop #5
Second Loop #1
Second Loop #2
^C I modified the trap!
Second Loop #3
Second Loop #4
Second Loop #5
$
```

你也可以移除一组设置的 `trap`。只需在 `trap` 命令后添加两个横杠，以及你想要恢复默认行为的信号列表：

```bash
$ cat test3b.sh
#!/bin/bash
# Removing a set trap
#
trap 'echo Sorry... Ctrl-C is trapped.' SIGINT
#
```

## 第二部分：Shell 脚本基础

```bash
count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 1
    count=$[$count + 1 ]
done
#
# Remove the trap
trap SIGINT
echo "Just removed the trap"
#
count=1
while [ $count -le 5 ]
do
    echo "Second Loop #$count"
    sleep 1
    count=$[$count + 1 ]
done
#
./test3b.sh
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
I just removed the trap
Second Loop #1
Second Loop #2
Second Loop #3
^C
$
```

> **提示**

你可以在 `trap` 后使用单个破折号代替双破折号将信号恢复到它们的默认行为。单、双破折号都可以正常工作。

在移除信号 `trap` 后，脚本将以默认方式处理 `SIGINT` 信号。然而，如果在移除 `trap` 之前接收信号，脚本将按照原始的 `trap` 命令处理：

```bash
./test3b.sh
Loop #1
Loop #2
Loop #3
^C Sorry... Ctrl-C is trapped.
Loop #4
Loop #5
I just removed the trap
Second Loop #1
Second Loop #2
$
```

在这个示例中，第一个 `Ctrl+C` 组合键用于尝试正常终止脚本。由于在移除 `trap` 之前接收到了信号，脚本执行了 `trap` 中指定的命令。在脚本执行移除 `trap` 后，`Ctrl+C` 就可以提前终止脚本。

## 在后台模式下运行脚本

有时，直接从命令行界面运行 shell 脚本是不方便的。某些脚本可能需要长时间才能处理，而你可能不想为了等待占用命令行。在脚本运行期间，你无法在终端会话中执行其他事情。幸运的是，这个问题有一个简单的解决方案。

当你使用 `ps` 命令时，你会看到看到 Linux 系统上运行的一组进程。显然，并不是所有的进程都运行在你的终端显示器上。这被称为在后台运行进程。在后台模式下，进程的运行不与终端会话的 `STDIN`、`STDOUT` 和 `STDERR` 关联（见第 15 章）。

你也可以在 shell 脚本利用这一特性，允许它们在后台运行而不锁定你的终端会话。接下来的章节介绍了如何在 Linux 系统上以后模式运行你的脚本。

## 在后台运行
