
列表 8.9 中最重要的注意点是前台主脚本与后台协进程函数 `proc_watch` 之间使用的通信链接，以及使用 `getopts` 解析命令行参数。其他值得关注的是使用 `string_test` 函数进行整数测试，以及通过时间戳通知用户新进程启动或停止的方式。更新后的进程计数、所有 PID 的列表以及函数内部如何将文本发送到 tty 显示。一如既常，我们在控制结构中使用双括号测试方法（注意这里没有使用 `$` 来定义用户自定义变量！）。该脚本还包含了许多使用不同结构的良好实践，以及逻辑与/或（`&&` 和 `||`）的使用，这减少了对 `if.then.else`、`,` 和 `case` 的需求。

8.9 的后续部分定义了脚本中使用的所有函数。我们有一个用于显示用法错误的 `usage` 函数。这里有 `trap_exit` 函数。该陷阱退出函数会在代码 1、2、3 和 15 时执行，这些代码会出现在脚本的“主体开始”处。接下来是 `pre_event_script`、`startup_event_script` 和 `post_event_script` 函数。你可能会问为什么函数类型指示它是脚本。这样做是为了鼓励使用外部脚本，或者任何启动或后事件，而不是编辑此脚本并调试内部函数。

然后是执行所有工作的主函数 `proc_watch`。该函数也是我们一直在讨论的协进程函数。`proc_watch` 函数是一个包含内部循环的无限循环，其中一个内部循环在任何时候执行。在两个循环中，我们都会检查变量 `BREAK` 是否为 `Y`。`Y` 值表示函数应立即退出。当 `BREAK` 变量被更新、更改，或者主脚本通过脚本中的命令“引用”此后台协进程时，就会发生这种情况。该函数在每次循环迭代时使用标准 `read` 命令重新读取它。这正是能够从后台函数循环退出的关键。如果主脚本被中断，最内层的循环在函数和脚本结束后仍将继续执行。它会在循环结束时自行退出。

参数满足了，但如果它们从未被满足，我们最终将导致失效的进程。为了解决这个问题，我们使用函数符号的后缀 `&` 将 `proc_watch` 函数作为后台协进程启动——例如，`proc_watch &`。协进程可以简单地理解为一条通往后台的管道，通过这个管道我们建立了一个通信链接。

对于 shell 脚本的主部分，在 `MAIN` 开始处，我们首先设置了一个陷获（`trap`）。在 `trap` 命令中，我们将 `BREAK` 变量设置为 `'Y'`，表示 `proc_watch` 协进程应该退出，并通过 `print -p $BREAK 2>/dev/null` 将 `BREAK` 的值让协进程感知。此命令将错误通知发送到标准错误（文件 2），但我们希望抑制所有的错误通知，否则错误信息会在脚本执行期间显示在屏幕上，这是非常不可取的。

接下来是初始化几个变量并检查参数数量的细节。运行此脚本有两种方式：(1) 仅指定总秒数要监控的进程 (2) 使用命令行开关来指定分钟、小时、天和要监控的进程。后者方法将使用 `getopts` 命令来解析参数，但对于第一种方法我们需要 `getopts`。我们首先检查是否仅有秒数进程。第二个参数可以是任何不是 `'-'` 开头的字符串或空字符串的任何内容。否则我们将使用 `getopts` 命令解析命令。

当我们需要处理命令行参数时，使用 `getopts` 会让生活变得更容易；然而，`getopts` 有其局限性。该命令负责解析命令行参数，但它不在乎参数是什么。因此，我们需要对每一个参数进行合理检查，以确保它符合预期标准。如果参数失败，我们就运行用法函数并带返回代码 1 退出。对每个参数会进行两次测试：我们测试所使用的变量以确保它不为空，并检查所有的数值值。整数测试是为了确保 `SECONDS`、`MINUTES`、`HOURS` 和 `DAYS` 中至少有一个大于 0 的整数值。如果我们进入这一阶段，我们就认为有了可靠的数据来开始监控。

监控从初始化进程状态开始（当前运行或未运行）。根据此信息我们初始化 `RUN` 变量，它被作为脚本其余部分的控制机制。初始化文本会记录日志并显示在屏幕上，通过 `proc_watch &` 将 `proc_watch` 函数作为后台协进程启动。主脚本只是倒计时到 0 然后退出。为了让 `proc_watch` 函数干净退出，我们将 `'Y'` 赋值给 `BREAK` 变量，并通过 `print -p $BREAK` 命令让协进程感知新值。然后杀死保存在 `WATCH_PID` 变量中的后台 PID，最后带返回代码 0 退出脚本。如果脚本被中断，陷获将处理停止协进程并退出。参见列表 8.10。

# 进程监控

```
[root:yogi]@/scripts/WILEY/PROC_MON# ./proc_watch_timed.ksh -m 5 -p xcalc

Currently running xcalc processes running

The xcalc process is not currently running...monitoring...
MON_STARTED: Monitoring for xcalc began => 09/27/01@21:15:02
ACTIVE PIDS
START PROCESS: xcalc start time => 09/27/01@21:15:19
ACTIVE PIDS: 26190
STARTUP EVENT: Executing Startup Event Script...
SUCCESS: Startup Event Script Completed Rc - 0
PROCESS COUNT: 2 xcalc Processes Running => 09/27/01@21:15:46
ACTIVE PIDS: 13060 26190
PROCESS COUNT: 3 xcalc Processes Running => 09/27/01@21:16:04
ACTIVE PIDS: 13060 18462 26190
PROCESS COUNT: 4 xcalc Processes Running => 09/27/01@21:16:27
ACTIVE PIDS: 18462 22996 26190
PROCESS COUNT: 5 xcalc Processes Running => 09/27/01@21:16:39
ACTIVE PIDS: 18462 22996 24134
PROCESS COUNT: 6 xcalc Processes Running => 09/27/01@21:16:56
ACTIVE PIDS: 18462 22996 24134 26190
PROCESS COUNT: 7 xcalc Processes Running => 09/27/01@21:17:31
ACTIVE PIDS: 22996 24134 26190
PROCESS COUNT: 8 xcalc Processes Running => 09/27/01@21:17:41
ACTIVE PIDS: 22996 24134 21622
PROCESS COUNT: 9 xcalc Processes Running => 09/27/01@21:18:39
ACTIVE PIDS: 21622 22996 24134
PROCESS COUNT: 10 xcalc Processes Running => 09/27/01@21:18:58
ACTIVE PIDS: 21622 22996 24134
PROCESS COUNT: 11 xcalc Processes Running => 09/27/01@21:19:04
ACTIVE PIDS: 18180 21622 22996
PROCESS COUNT: 12 xcalc Processes Running => 09/27/01@21:19:10
ACTIVE PIDS: 18180 22758 22996
PROCESS COUNT: 13 xcalc Processes Running => 09/27/01@21:19:17
ACTIVE PIDS: 18180 22758 23164
PROCESS COUNT: 14 xcalc Processes Running => 09/27/01@21:19:37
ACTIVE PIDS: 18180 22758 23164
PROCESS COUNT: 15 xcalc Processes Running => 09/27/01@21:19:47
ACTIVE PIDS: 18180 22996 23164
PROCESS COUNT: 16 xcalc Processes Running => 09/27/01@21:19:53
ACTIVE PIDS: 18180 22996 26244
```

列表 8.10 `proc_watch_times.ksh` 脚本执行中。（继续）
