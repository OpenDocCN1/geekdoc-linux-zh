
如果你没有重定向标准输出和标准错误，`nohup`命令将自动创建一个 `nohup.out` 的文件来保存它们。

# 杀死后台作业

如果你记录了启动后台作业时显示的 PID，那么使用以下步骤可以轻松终止该作业。你也可以使用 `ps` 命令和 `who -u` 命令来确定要终止的任务或用户会话的 PID 号。

## 如何通过 PID 终止作业

- 1. 在 shell 提示符下，输入 `kill PID`，其中 `PID` 是你想终止的进程的 PID 号。双击检查输入的数字是否正确。然后按回车键。此 `kill` 命令会给作业一个正常终止的机会，关闭应用程序并移除锁文件和临时文件。不会显示任何消息。
- 2. 现在输入命令 `kill -9 PID`，其中 `PID` 是步骤 1 中使用的数字。双击检查你输入的数字是否正确。然后按回车。此 `kill` 命令会结束无响应的命令。虽然你可以在步骤 1 之后立即执行步骤 2，但你可能想等待几秒钟让作业完成。
- 3. 如果步骤 2 给出错误 `No such PID`，请忽略该错误。这意味着步骤 1 已经足够结束该任务，步骤 2 是没必要的但没有危害。

如果你不记得你的 PID 号，可以使用 `ps` 命令查找：

> 注意
> 请参附录 B，“术语表”，以获取 PID 值的定义。

## 使用 ps 查找 PID 号

- 1. 在 shell 提示符下，输入以下两个命令：
`ps -ef`
`ps aux`
某些系统同时支持这两个命令，但有时只有其中一个会有结果。
- 2. 使用在你系统上有效的命令，查看初始标题以找到 PID 列、用户 `UID` 列和命令 `CMD` 列。
- 3. 如果必要，重新运行命令并将其通过（pipe）到 `pg`、`more`，或者以逐页查看的方式查看。

或者，你可以将 `ps` 命令的输出通过到 `grep` 以过滤掉你不关心的行。注意，这也会移除表头。
- 4. 找到你想终止的命令。检查 `UID` 列以确保该命令是由你启动的。
- 5. 找到该命令的 PID。然后你就可以按照 PID 终止作业的示例进行操作。

这是一个用于查找后台作业的命令示例。然而，输出在中间被截断了。因为 `ps` 可以显示很多进程，该命令使用 `c`（在 Solaris 上）被中止：

```
# UID PID PPID C STIME TTY TIME CMD

root 0 0 Feb 20 ? 0:02 sched

root 1 0 Feb 20 ? 0:15 /etc/init -

root 2 0 Feb 20 ? 0:00 pageant

root 3 0 Feb 20 ? 1:02 fsflush

root 289 1 0 Feb 20 ? 0:00 /usr/lib/saf/sac -t 300
```

假设你正在运行之前的命令来查找一个早些启动的 `find` 命令。你可以使用 `grep` 过滤掉你不需要的行，如下所示：

```
# ps -ef|grep find

root 27961 27955 5 13:53:33 pts/1 0:03 find -name acme -print

root 27967 27955 0 13:54:19 pts/1 0:00 grep find

#
```

从 `CMD` 字段（最后一个字段），你可以看到找到了两个 `find` 进程。查看第 2 字段，你会发现 `PID` 27961 是你想终止的进程。注意 `PID` 27967 是正在查找的 `grep` 进程；换句话说，`grep` 在查找时看到了它自己。

这是一个使用额外的 `grep -v` 移除额外 grep 进程的类似示例：

```
# ps -ef | grep find

root 27961 27955 5 13:53:33 pts/1 0:03 find -nameme -print

#
```

# 在 Korn Shell 中使用作业控制

当你知道要终止的 PID 时，可以输入以下行来杀死进程：

```
kill 27961

kill -9 27961
```

另另
关于 `grep` 的更多信息，请参见第 494 页。

## 在 Korn Shell 中使用作业控制

上一节涵盖了适用于所有 shell（包括 Bourne shell）的后台作业用法。新的 shell 通过引入名为“作业控制”的功能，处理后台作业变得简单得多。例如，某些系统为 Bourne shell 添加了作业控制，可以作为 `jsh` 调用。本节描述了其他作业控制命令，它们与 `jsh` 类似：分别是 C shell 的 `csh` 和 Korn shell 的 `ksh`。

# 列出后台作业

要列出支持作业控制的 shell 中的所有后台作业，进入 shell 提示符并输入 `jobs`。

你会看到如下输出：

```
$ jobs

[4] + Running find / -name acme -print > /tmp/acacfind

[3] Stopped (SIGTSTP) man find

[2] Stopped (SIGTSTP) man

[1] Stopped (SIGTSTP) bc
```
