
```bash
#!/bin/bash

# killall--Sends the specified signal to all processes that match a
# specific process name

# By default it kills only processes owned by the same user, unless you're
# root. Use -s SIGNAL to specify a signal to send to the process, -u USER
# to specify the user, -t TTY to specify a tty, and -n to only report what
# should be done, rather than doing it.

signal="-INT"    # Default signal is an interrupt.
user="" tty="" donothing=0

while getopts "s:u:t:n" opt; do
    case "$opt" in
        # Note the trick below: the actual kill command wants -SIGNAL
        # but we want SIGNAL, so we'll just prepend the "-" below.
        s ) signal="-$OPTARG" ;;
        u ) if [ -z "$tty" ] ; then
            # Logic error: you can't specify a user and a TTY device
            echo "$0: error: -u and -t are mutually exclusive." >&2
            exit 1
        fi
user=$OPTARG;
;;
t ) if [ ! -z "$user" ] ; then
echo "$0: error: -u and -t are mutually exclusive." >&2
exit 1
fi
tty=$2;
;;
n ) donothing=1;
;;
? ) echo "Usage: $0 [-s signal] [-u user|-t tty] [-n] pattern" >&2
exit 1
esac
done

# Done with processing all the starting flags with getopts...
shift $(($OPTIND - 1))

# If the user doesn't specify any starting arguments (earlier test is for -?)
if [ $# -eq 0 ] ; then
echo "Usage: $0 [-s signal] [-u user|-t tty] [-n] pattern" >&2
exit 1
fi

# Now we need to generate a list of matching process IDs, either based on
# the specified TTY device, the specified user, or the current user.

if [ ! -z "$tty" ] ; then
pids=$(ps cu -t $tty | awk "/ $1/ { print $2 }")
elif [ ! -z "$user" ] ; then
pids=$(ps cu -U $user | awk "/ $1/ { print $2 }")
else
pids=$(ps cu -U $(USER:-LOGNAME) | awk "/ $1/ { print $2 }")
fi

# No matches? That was easy!
if [ -z "$pids" ] ; then
echo "$0: no processes match pattern $1" >&2
exit 1
fi

for pid in $pids
do
# Sending signal $signal to process id $pid: kill might still complain
# if the process has finished, the user doesn't have permission to kill
# the specific process, etc., but that's okay. Our job, at least, is done.
if [ $donothing -eq 1 ] ; then
echo "kill $signal $pid"  # The -n flag: "show me, but don't do it"
else
kill $signal $pid
fi
done

exit 0
```

## 工作原理

由于此脚本非常激进且可能危险，我们已投入额外精力来最大限度地减少错误的模式匹配，以便像 `sh` 这样的模式不会匹配 `ps` 输出中包含 `bash` 或 `vi crashtest.c` 或其他嵌入该模式的值的情况。这是通过 `awk` 命令上的模式匹配前缀完成的（1，2，3）。

在指定的模式 `$1` 前加上一个前导空格，并在模式后加上一个尾随 `$`，会导致脚本在 `ps` 输出中搜索指定的模式 `'sh'` 时搜索 `' sh$'`。

## 运行脚本

此脚本具有多种起始标志，可让你修改其行为。`-s SIGNAL` 标志允许你指定除默认中断信号 `SIGINT` 之外的信号发送给匹配的进程或进程。`-u USER` 和 `-t TTY` 标志主要对 `root` 用户有用，可分别杀死与指定用户或 `TTY` 设备关联的所有进程。`-n` 标志可让你选择让脚本报告它将要执行的操作，而不实际发送任何信号。最后，必须指定一个进程名称模式。

## 结果

要杀死 OS X 上的所有 `csmount` 进程，现在可以使用 `killall` 脚本，如清单 6-7 所示。

```
$ ./killall -n csmount
kill -INT 1292
kill -INT 1296
kill -INT 1306
kill -INT 1310
kill -INT 1318
```

清单 6-7：在任何 `csmount` 进程上运行 `killall` 脚本

## 修改脚本

在运行此脚本时可能会出现一个不太可能但并非不可能的错误。为了仅匹配指定的模式，`awk` 调用会输出匹配该模式的进程的进程 ID，外加输入行末尾出现的前导空格。但理论上可能同时运行两个进程——例如，一个名为 `bash`，另一个名为 `emulate bash`。如果使用 `bash` 作为模式调用 `killall`，这两个进程都将被匹配，尽管只有前者是真正的匹配。要解决此问题以获得一致的跨平台结果将非常棘手。

比杀死更重要。调用 `renice` 让你可以更改程序的相对优先级，例如，你可以降低长时间文件传输的优先级，同时提高老板正在运行的视频编辑器的优先级。

## 48 验证用户 crontab 条目

Linux 世界中最有用的设施之一是 `cron`，它能够在未来的任意时间安排作业，或使其每分钟、每隔几小时、每月甚至每年自动运行。每个优秀的系统管理员都有一个由 `crontab` 文件运行的瑞士军刀脚本集。

然而，输入 `cron` 规范的格式有点棘手。

例如，如果你用错别字指定星期几，`crontab` 会报告类似如下的错误：

```
"/tmp/crontab.DjT4v6wGR':9: bad day-of-week
crontab: errors in crontab file, can't install"
```

事实上，示例输入文件第 12 行还有第二个错误，但由于其糟糕的错误检查代码，`crontab` 会迫使我们通过迂回的方式在脚本中查找它。

与其按照 `crontab` 的方式进行错误检查，一个有点冗长的 shell 脚本（参见清单 6-8）可以逐步检查合理的文件，检查语法并确保值在合理范围内。能够在 shell 脚本中进行此验证的一个原因是可以将集合和范围视为单独的值。因此，要测试 `3-11` 或 `4、6 和 9` 是否是字段的可接受值，只需在前一种情况下测试 `3` 和 `11`，在后一种情况下测试 `4、6 和 9` 即可。

### 代码
