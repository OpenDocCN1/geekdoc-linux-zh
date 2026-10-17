
# 第四部分：红帽 Linux 系统维护

设置 `IFS` 允许脚本正确地解析 `/etc/passwd` 条目。`while read` 语句读取输入的每一行，将每个字段的值分配给相应的变量，然后执行操作。

## 第 19 章：使用脚本自动化任务 539

```bash
# 是否被正确调用？

getopts ":u" OPT || usage syntax

[ "$OPT" = ":" ] && usage arg
```

```bash
# 用户是否存在？

UNAME=$OPTARG

grep $UNAME /etc/passwd > /dev/null || usage user
```

```bash
# 杀死用户的进程

for SIG in TERM INT HUP QUIT KILL
do
  echo "Trying $SIG$SIG"
  kill -$SIG -u $UNAME > /dev/null
  sleep 1
  pgrep -u $UNAME > /dev/null || exit 0
done
```

```bash
# 显示简短的用法信息

function usage
{
ERR=$1
case $ERR in
  "root") echo "只有 root 可以运行此脚本" ;;
  "syntax" ) echo "USAGE: kujob.sh -u UNAME" ;;
  "arg") echo "-u 需要用户名" ;;
  "user") echo "无此类用户" ;;
esac
exit 1
}
```

`usage` 是一个函数，但作为一个方便的错误处理器。它总会在显示与传递的参数相关的错误消息后终止脚本。它的方便之处在于集中了脚本所有的错误处理；它的粗糙之处在于没有尝试从错误中恢复。

第一块代码使用 Bash 的内置变量 `UID` 来检查调用脚本的是否为 root（即用户 ID `UID` 为 0）。如果测试返回为假，意味着运行脚本的用户不是 root，则 `kujob.sh` 将带 `root` 参数调用 `usage`。否则，继续执行。

第二块代码使用 `getopts` 处理其命令行参数。正如我们在选项字符串所示，唯一的有效选项是 `u`。前面的 `:`（在 `u` 之前）关闭 Bash 的默认错误信息，允许脚本提供自己的错误信息。末尾的 `:` 表示 `-u` 需要一个参数。如果使用了无效选项，`kujob.sh` 将带 `syntax` 参数调用 `usage`。下一行代码确保如果漏掉了必需参数，`OPT` 变量中会出现 `a`，因此如果测试为真，它将带该参数调用 `usage`。

## 第四部分：Red Hat Linux 系统维护

一旦 `kujob.sh` 确定其被正确调用，下一块代码将执行完整性检查：确保指定的用户确实存在。脚本的其余部分依赖于此信息。通过将传递给变量 `UNAME` 的用户名，`grep` 命令在 `/etc/passwd` 文件中进行搜索。如果存在，`grep` 返回 0（真）并继续执行语句。如果名称不存在，`grep` 返回 1（假），`kujob.sh` 将带 `user` 参数调用 `usage`。注意 `grep` 命令的 `stderr` 和 `stdout` 都重定向到了 `/dev/null`，这使得脚本的运行时外观更加简洁。

最后，`kujob.sh` 尝试杀死用户的所有进程。它使用的信号按严重程度和优先的增加顺序列出（更多信息请参见 `signal(7)`）。如果某个信号未能杀死进程，将尝试下一个更强的信号，直到所有与用户相关的进程都被杀死。`sleep` 语句让内核在脚本继续之前完成与进程终止相关的清理工作。在所有用户进程都终止后，脚本退出（如果没有进程匹配指定标准，`grep` 返回 1，即假）。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_571_0.png)

除了杀死用户的进程外，`kujob.sh` 还会杀死用户的 shell。使用此脚本时要小心。

`kill` 和 `pgrep` 命令是 `procps` 软件包的一部分，这是一套进程管理和监控工具。特别是 `kill` 和 `pgrep`，为 `ps` 命令及其杂杂命令行选项提供了一个更简单的接口。事实上，`kill` 语句通过 `-u` 结构将 `SIG` 指定的信号发送给 `UNAME` 中指定用户所拥有的所有进程。`pgrep` 使用相同的 `u` 选项，列出所有匹配进程的进程 ID `PID`（尽管你看不到它们，但 `pgrep` 的 `stdout` 和 `stderr` 已重定向到 `/dev/null`）。更多信息请参阅 `kill` 和 `pgrep` 的帮助页。

列表 19-16 中的脚本 `dskug.sh` 打印每个挂载文件系统的磁盘使用报告，按目录大小从大到小排序输出。

### 列表 19-16：按顶级目录大小显示磁盘使用情况

```bash
#!/bin/sh

# dskug.sh - 打印每个文件系统的磁盘使用情况
# 顶级目录按降序排列

[ $UID -eq 0 ] || usage

for FS in $(grep ^/ /etc/mtab | cut -f2 -d " ")
do
    echo "$FS"
```

## 第 19 章：使用脚本自动化任务

```bash
du -x --max-depth=1 --exclude=/dev* $FS | sort -rg
echo
done

function usage
{
    echo "你必须是 root 才能获得准确报告"
    exit 1
}
```

第一条语句确保如果执行脚本的用户不是 root 或等等权限的用户，则打印错误消息并退出。普通用户没有权限访问 Red Hat Linux 系统上的许多目录树（例如 `/root` 和 `/var/log`），因此该语句确保了报告的准确性，并在此过程中消除了重定向 `stderr` 到 `/dev/null` 的必要性）。脚本选择 `/etc/mtab` 中列出的挂载文件系统。它使用 `/etc/mtab` 而不是 `/proc/mtab` 的输出，因为它更容易解析。对于每个文件系统，脚本打印名称，然后按磁盘使用量降序打印顶级目录，这是使用 `--max-depth=1` 实现的。这了脚本分析 `/proc`。例如，`--exclude=/dev*` 将 `/dev` 文件排除在外。通过将输出传递给 `sort`，脚本可以使用 `-g` 根据数值排序并使用 `-r` 反转顺序。此脚本的输出可能类似于：

```
./dskug.sh
172552 /bin
106636 /var
39720 /lib
10892 /etc
5376 /root
268 /tmp
48 /tftp
16 /lost+found
12 /mnt
4 /automount
```

## 第四部分：Red Hat Linux 系统维护

```
/boot
3485 /boot/lost+found
```

```
/home
297920 /home
270828 /home
270428 /home
24 /home
lost+found
```

```
/usr
2113504 /usr
```

```
853948 /usr/share
746872 /usr/lib
167220 /usr/X11
102200 /usr/src
59948 /usr/include
30428 /sbin
12236 /i386-glibc
6228 /libexec
5512 /kerberos
2612 /games
120 /html
80 /local
16 /lost+found
4 /etc
dict
```

列表 19-17 运行 `vmstat` 命令，将其输出重定向到文件，以便稍后使用电子表格或其他工具进行分析。`vmstat.sh` 旨在作为 cron 任务运行。本章稍后的“自动化脚本”部分讨论了 `cron` 和用于自动运行脚本的 `at`set。

### 列表 19-17：为离线分析收集 vmstat 统计数据

```bash
#!/bin/sh
# vmstat.sh - 收集 vmstat 报告供以后分析
LOG=/var/log/vmstat.log
[ $UID -eq 0 ] || LOG=$HOME/vmstat.log
```

## 第 19 章：使用脚本自动化任务

```bash
DELAY=${1:-60}
vmstat -n $DELAY >> $LOG
```
