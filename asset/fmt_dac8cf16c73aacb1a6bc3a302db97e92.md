
在 Listing 8.3 中，我们首先定义了两个函数，它们都用于异常操作。我们始终需要一个 `usage` 函数，在这个 shell 脚本中我们添加了一个 `trap_exit` 函数，它只在捕获到陷获的信号时执行。`trap` 定义了退出信号 1、2、3 和 15。当然，你无法捕获退出信号 9。此 `trap_exit` 函数将显示“EXITING on a trapped signal...”。然后 `trap` 将执行第二个命令 `exit 3`。在下一步中，我们检查命令行参数的数量是否正确（一个或两个），并使用嵌入的 `case` 语句将目标进程赋值给变量 `PROCESS`。如果两个命令行参数的第一个参数 `$1` 中指定了 `-v`，则使用详细模式。详细模式将显示 `grep` 命令进行模式匹配的 `ps -ef` 输出。否则，该信息处于活跃状态。这是我们第一次查看目标进程是否活跃。如果目标进程没有执行，则通知用户并以返回码 2 退出。接下来是在命令行上指定了 `-v` 开关时使用详细模式。注意我们在通过 `ps -ef | head -1` 显示进程之前，是如何提取 `ps` 输出的列信息的。这有助于用户确认这与列标题匹配正确。现在我们知道进程正在运行，所以我们开始了一个循环。该循环将持续到进程结束或程序被中断——例如，按了 CTRL-C。

`proc_mon.ksh` 脚本完成了工作，但我们没有日志，且监控会在进程停止时停止。如果能跟踪进程的启动和停止就太好了。如果我们能监控这种转换，就可以保留日志文件进行审查，并查看是否能发现趋势。

```bash
[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is NOT an active process...EXITING...
[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is currently RUNNING...`date`
[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is currently RUNNING...`date`

[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is currently RUNNING...`date`
[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is currently RUNNING...`date`
[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is currently RUNNING...`date`
[root:yogi]@@scripts/WILEY/PROC_MON# ./proc_mon.ksh xcalc

xcalc is currently RUNNING...`date`
```

```bash
echo "START PROCESS: $PROCESS began => $TIMESTAMP > $TTY
)

################################################################
################ 主程序开始 ####################
################################################################

 设置陷阱 (TRAP) ###

trap 'trap_exit; exit 0' 1 2 3 15

# 检查正确的命令行参数 - 仅限1个

if (( $# != 1 ))
then
    usage
    exit 1
```

## 获取初始状态并设置 RUN 标志

```bash
ps -ef | grep -v "$PROCESS" | grep -v $SCRIPT_NAME \
grep $PROCESS >/dev/null
```

## PROC_RC? 检查返回值！！

# 在启动循环之前提供一些初始反馈

```bash
if (( $PROC_RC == 0 ))
then
    echo "$PROCESS 当前正在运行...监控中..."
    RUN_FLAG="Y"
    # 将 RUN 标志设为 YES
else
    echo "$PROCESS 当前未运行...监控中..."
    RUN_FLAG="N"
    # 将 RUN 标志设为 NO
fi
```

`TIMESTAMP=$(date +%T)` 获取日志所需的时间戳

# 使用 "tee -a $LOGFILE" 同时输出到标准输出

# 和 $LOGFILE 所引的文件

```bash
echo "MON_START: Monitoring for $PROCESS began => $TIMESTAMP" \
| tee -a $LOGFILE
```

## 无限循环！！

```bash
while :
```

**列表 8.5** `proc_watch.ksh` shell 脚本列出。（继续）

```bash
case $RUN in
'Y') # 循环直到进程结束
RUN=$$(mon_proc_end)
  ;
'N') # 循环直到进程开始
RUN=$$(mon_proc_start)
  ;
esac;

done
```

列表 8.5 `proc_watch.ksh` shell 脚本列出。（继续）

列表 8.5 中的该 shell 脚本是一个非常良好的模块化脚本。实际的监控循环是最后的 `while` 循环。该循环非常非常短且紧凑，所有工作都在两个进程 `proc_mon_start` 和 `proc_mon_end` 中完成。注意，在这两种情况下，我们都一直保持在循环中，直到发生从“运行”到“未运行”再到“进程启动”的转换。在每次转换中，我们使用 `print` 命令将更新的状态信息返回给调用脚本，而不是使用 `return`。为了实现屏幕并发显示和文件日志，我们在脚本体内部使用 `tee -a $LOGFILE`，而在函数内部，我们将输出重定向到分配给 `$TTY` 设备的 tty 设备，以确保屏幕输出到我们正在查看的终端或伪终端。否则，我们无法确保标准输出指向函数内部。注意，我们没有在双括号方法中使用 `$` 类型的数字测试。对于 `while` 循环，我们是每秒都循环一次。`while :` 允许这种操作运行（使用 `true` 也可以）。`proc_watch.ksh` shell 脚本将持续运行，直到被中断——例如通过 CTRL-C。

我们改进了脚本，但它并不知道有多少个活动进程。接下来我们将扩展脚本以以不同的方式执行一些操作。首先，我们希望能够对特定时间段进行计时。我们想让用户知道有多少活动进程以及每个进程的 PID。此外，我们想为每个进程的启动和结束标记时间戳。为了给每个进程标记时间戳，我们可以在每次循环迭代中计算运行的进程数量，如果计数发生变化，我们将获取新的时间戳并更新当前运行进程的 PID 列表。我们还将提供在进程启动前、启动时或结束后运行某些预、启动和和或后事件的选项。

```bash
[root:yogi]@/scripts/WILEY/PROC_MON# ../proc_watch.ksh xcalc

xcalc进程当前正在运行..监控中...
MON_START: Monitoring for xcalc begin => 09/27/01@21:09:41
END PROCESS: xcalc ended => 09/27/01@21:09:56
START PROCESS: xcalc begin => 09/27/01@21:10:06
END PROCESS: xcalc ended => 09/27/01@21:10:25
MON_STOP: Monitoring for xcalc ended ==> 09/27/01@21:10:33
```

列表 8.6 `proc_watch.ksh` shell 脚本运行实例。

## 进程监控的定时执行、显示 PID 和时间戳，具备事件和计时能力

听起来很多吗？在我们过完这一节后，每一步都会变得直观易懂。在之前的三个脚本中，我们无法监控每个匹配通用模式的进程，也无法针对特定时间执行监控。因为我们使用了 `grep` 命令，我们可能会获得模式的匹配项。在有多个匹配的情况下，我们需要知道 (1) 我们有多少个匹配以及 (2) 我们必须管理的每个进程。如果你正在监控用户的活动，或者我们对运行的进程 ID 感感兴趣，这些信息将非常有帮助。

我们希望有一个良好的机制，能够方便、灵活地对监控活动的持续时间进行计时。我们不知道具体需求是什么，所以我们希望尽可能提供灵活性。让我们进入最后，并允许从开始计时。

## 进程监控

在本节中，我们将做两件事：使用 *getopts* 解析命令行并在后台执行一个函数。*getopts* 功能是解析命令行的一种简单方法。
