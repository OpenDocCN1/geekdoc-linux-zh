
`/etc/rc.d/rc0.d` 运行级别 0 目录。
`/etc/rc.d/rc1.d` 运行级别 1 目录。
`/etc/rc.d/rc2.d` 运行级别 2 目录。
`/etc/rc.d/rc3.d` 运行级别 3 目录。
`/etc/rc.d/rc4.d` 运行级别 4 目录。
`/etc/rc.d/rc5.d` 运行级别 5 目录。

通过这种方式，`/etc/rc.d/rc0.d/K60atd`、`/etc/rc.d/rc1.d/K60atd`、`/etc/rc.d/rc2.d/K60atd`、`/etc/rc.d/rc3.d/S40atd`、`/etc/rc.d/rc4.d/S40atd`、`/etc/rc.d/rc5.d/S40atd` 以及 `/etc/rc.d/rc6.d/K60atd` 都是指向 `/etc/rc.d/init/atd` 的符号链接。使用这种简单一致的机制，你可以自定义启动时启动的程序。

## 理解启动脚本的作用

一个启动/关机 shell 脚本示例是 `/etc/rc.d/init.d/atd`。它控制 `atd` 守护进程的启动和停止，重现如下：

```bash
#!/bin/bash
# /etc/rc.d/init.d/atd
# 启动守护进程
# config: 45 60
# description: 在运行 at 命令指定的时间运行 atd 调度的任务，
# 并在负载足够低时运行 batch 任务。
# processname: atd

# 源函数库。
. /etc/rc.d/init.d/functions

test -x /usr/sbin/atd || exit 0
# 查看是如何调用的。
case "$1" in
start)
  # 检查 atd 是否已经在运行
  if [ ! -f /var/lock/subsystems/atd ]; then
    echo -n 'Starting daemon: '
    daemon /usr/sbin/atd
    echo
    touch /var/lock/subsystems/atd
  fi
  ;;
stop)
  echo -n 'Stopping daemon: '
  killproc /usr/sbin/atd
  echo
  rm -f /var/lock/subsystems/atd
  ;;
reload|restart)
  $0 stop
  $0 start
  ;;
status)
  status /usr/sbin/atd
  ;;
*)
  echo "Usage: /etc/rc.d/init.d/atd (start|stop|restart|status)"
  ;;
esac
```

与刚才分析的 `/etc/rc.d/init.d` 脚本一样，该脚本在子 shell 中运行。`config`、`description` 和 `processname` 行供 `chkconfig` 程序使用。这些行描述了守护进程的作用，并告知 `chkconfig` 在运行级别 3、4 和 5（优先级 40）启动，在其他运行级别（优先级 60）杀死。

再次，读取 `/etc/rc.d/functions` 以提供几个标准过程，如 `daemon`、`status` 和 `killproc`。下一行检查可执行程序是否存在且是否可执行，如果不存在或不可执行则退出。`case` 块包含了程序的核心逻辑：

- 如果使用 `start` 参数调用脚本，它会检查 `/var/lock/subsystems/atd` 文件是否存在。如果，说明另一个 `at` 实例正在运行。否则，脚本创建并启动 `atd` 守护进程。
- 使用 `stop` 参数运行时，如果 `at` 正在运行则将其杀死并移除 `/var/lock/subsystems/atd` 文件。
- 如果调用 `reload` 或 `restart`，脚本通过连续调用 `stop` 和 `start` 参数来重启守护进程。
- `status` 选项报告 `at` 进程是否运行，如果活动则列出 `at` 进程的 PID。
- 任何其他参数都会导致脚本打印用法信息，指示哪些命令行有效。

最后一行向启动它的进程返回成功的退出值。脚本在此处结束处理，但守护进程继续运行（取决于你运行的是 `start` 还是 `stop`）。

## 修改启动行为

修改任何脚本的启动行为涉及用文本编辑器打开文件。例如，`atd` 守护进程（由上述脚本控制）会对通过 `at` 和 `batch` 命令提交的任务进行队列。系统负载低于特定值（可以通过 `at` 的命令行选项设置）时，才会通过 `batch` 提交的任务。默认值 0.8 是基于以下假设：单处理器机器 CPU 利用率低于 80% 可以处理 batch 任务的额外负载。然而，如果你为机器添加了另一个 CPU，默认阈值将太低，batch 任务将无法充分限制。

你可以将系统负载阈值从 0.8 改为 1.6 以适应增加容量。为此，只需修改 `/etc/rc.d/init.d/atd` 脚本中的以下行（start 部分）：

```
daemon /usr/sbin/atd
```

用此行替换它，使用 `-l` 参数指定新的最小负载值：

```
daemon /usr/sbin/atd -l 1.6
```

保存文件并退出编辑器后，你可以重启机器或仅运行以下三个命令之一开始使用新的 batch 阈值：

```
/etc/rc.d/init.d/atd reload
/etc/rc.d/init.d/atd restart
/etc/rc.d/init.d/atd stop ; /etc/rc.d/init.d/atd stop
```

## 移除守护进程

处理从系统启动目录移除程序的方法有两种。第一种方法是手动删除符号链接。如果你想让 `sendmail` 守护进程不在级别 2 启动（仅在运行级别 3、4 和 5 活动），你可以删除 `/etc/rc.d/rc2/S80sendmail` 链接。然而，将链接重命名为不以 S 开头的名称（例如 `/etc/rc.d/rc2_S80sendmail`）可能更方便，以防以后想要启用。

> 你永远不要删除实际文件（在此例中为 `/etc/rc.d/init.d/sendmail`）。此外 `/etc/rc.d/init.d` 中的脚本从不直接访问，只有来自 `/etc/rc.d/rc.X` 目录的链接会被访问。

第二方法更为简单。`chkconfig` 程序使用 `config`、`description` 和 `processname` 标签（嵌入 `/etc/rc.d/init.d` 文件中）来管理 `/etc/rc.d/rc.X` 目录中的链接。

目录。为了实现在运行级别 2 中消除 sendmail 的目标，请编辑 `/etc/rc.d/init.d/sendmail` 文件并修改以下行：

```
# chkconfig: 2345 80 30
```

将其修改为：

```
# chkconfig: 345 80 30
```

然后执行以下两个命令中的任意一个（它们是等等的）：

```
chkconfig sendmail reset
chkconfig sendmail --level 2 reset
```

## 添加守护进程

对于两种方法，为新守护进程添加适当的文件非常相似。在安装了虚拟 `my_daemon` 程序的二进制文件后，需要将其配置为在运行级别 3、4 和 5 中启动，并在所有运行级别下终止。要实现这一点，只需在 `/etc/rc.d/init.d` 中放置一个名为 `my_daemon`（或其他其他直观的名称）的脚本。该脚本至少应支持 `start` 和 `stop` 命令行选项。对于手动方法，只需创建以下符号链接：

```
cd /etc/rc.d/rc0.d : ln -s ../init.d/my_daemon K28my_daemon
cd /etc/rc.d/rc1.d : ln -s ../init.d/my_daemon K28my_daemon
cd /etc/rc.d/rc2.d : ln -s ../init.d/my_daemon K28my_daemon
cd /etc/rc.d/rc3.d : ln -s ../init.d/my_daemon S82my_daemon
cd /etc/rc.d/rc4.d : ln -s ../init.d/my_daemon S82my_daemon
cd /etc/rc.d/rc5.d : ln -s ../init.d/my_daemon S82my_daemon
cd /etc/rc.d/rc6.d : ln -s ../init.d/my_daemon K28my_daemon
```

或者，使用 `chkconfig`，确保 `/etc/rc.d/init.d/my_daemon` 脚本中包含以下行：

```
# chkconfig: 345 82 28
# description: Does something pretty cool - you really \
# have to see it to believe it!
# processname: my_daemon
```

设置好这些行后，只需运行以下命令：

```
chkconfig --add my_daemon
```

相应的链接将自动创建。可以使用以下命令进行验证：

```
chkconfig --list my_daemon
```

输出结果应该如下：

`my_daemon 0:off 1:off 2:off 3:on 4:on 5:on 6:off`

## 操作运行级别

除了启动时选择的运行级别外，你还可以在登录状态下随时更改运行级别。`telinit` 命令（实际上只是指向 `init` 的符号链接）允许你指定所需的运行级别，从而导致终止所有不应在该运行级别下存在的系统进程，并启动所有应该运行的进程。

> 注意：`telinit` 命令还用于指示 `init` 重新加载其配置文件 `/etc/inittab`。这可以通过 `telinit q` 或 `telinit Q` 命令完成。

例如，如果你在启动时遇到硬盘问题，可能会被置于单用户模式（运行级别 1）以进行系统维护。一旦机器稳定，你只需执行以下命令：

```
telinit 5
```

`init` 命令将处理终止和启动所有进程，为你呈现一个图形化登录窗口。

## 确定当前运行级别

你可以使用命名准确的 `runlevel` 命令来确定机器当前的运行级别。使用上一个启动到单用户模式并手动更改运行级别的例子，`runlevel` 命令的输出将：

```
# runlevel
s 5
```

这意味着上一个运行级别是 S（代表单用户模式），当前运行级别是 5。如果机器启动正常，上一个运行级别将列为 N，表示实际上没有上一个运行级别。

## 切换到关机运行级别

关机仅仅是运行级别的改变。考虑到这一点，其他更改运行级别的方法包括 `reboot`、`halt`、`poweroff` 和 `shutdown` 命令。`reboot` 命令是指向 `halt` 命令的符号链接，它执行 `shutdown -r now`，终止所有进程并重启机器。`halt` 命令执行 `shutdown -h now`，终止所有进程并让机器处于空闲状态（但仍通电）。同样，`poweroff` 命令也是 `halt` 命令的链接，它执行到运行级别 0 的更改，但如果机器的 BIOS 支持高级电源管理 (APM)，它将关闭机器电源。

`shutdown` 命令必须指定时间，如果指定 `+m`（代表启动关机前的延迟分钟数）或 `hh:mm`（绝对时间值，其中 hh 是你希望开始关机的小时，mm 是分钟）。或者，`now` 常用于立即启动关机。

## 调度系统任务

经常会有在无人值守或非工作时间运行进程的需求。`at` 设施用于在特定时间运行此类作业。提交的作业在 `/var/spool/at` 目录中排队，等待 `at` 守护进程执行。作业使用提交作业时活动的当前环境执行。任何输出或错误信息都将发送到用户处。`at` 设施的设计用于在特定时间运行此类作业。提交的作业在 `/var/spool/at` 目录中排队，等待 `at` 守护进程执行。作业使用提交作业时活动的当前环境执行。任何输出或错误信息都将发送到用户处。`at` 设施的设计用于在特定时间运行此类作业。提交的作业在 `/var/spool/at` 目录中排队，等待 `at` 守护进程执行。作业使用提交作业时活动的当前环境执行。任何输出或错误信息都将发送到用户处。

## 使用 at.allow 和 at.deny

`at` 提供了两个访问控制文件来限制谁可以使用 `at`。`/etc/at.allow` 文件包含允许 `at` 的用户列表，`/etc/at.deny` 文件包含不允许 `at` 的用户。如果这两个文件都不存在，所有用户都可以使用 `at`。

## 指定时间

有很多方法可以指定 `at` 运行的时间。以下是示例：

| 命令 | 运行说明 |
| :--- | :--- |
| `at now` | 立即运行 |
| `at now + 2 minutes` | 任务在2分钟后运行 |
| `at now + 1 hour` | 任务在1小时后运行 |
| `at now + 5 days` | 任务在5天后运行 |
| `at now + 4 weeks` | 任务在4周后运行 |
| `at now next minute` | 任务在下一分钟运行 |
| `at now next day` | 任务在明天运行 |
| `at now next month` | 任务在下个月运行 |
| `at now next year` | 任务在明年运行 |
| `at now next fri` | 任务在下周五运行 |
| `at 16:00 today` | 任务在今天16:00运行 |
| `at 16:00 tomorrow` | 任务在明天16:00运行 |
| `at 2:45pm 14` | 任务在14日的下午:45运行 |
| `at 5:00 Sep 14` | 任务在9月14日的5:00运行 |

## 提交作业

`at` 设施在提交作业方面提供了很大的活性。有三种方法可以提交作业：

- 从标准输入管道。例如，以下命令将在明天早晨尝试构建 Perl-5.056：`echo "cd /tmp/perl5.056; make; ls -al" | at 2am tomorrow`。此过程的一个辅助好处是编译过程的完整日志将发送给提交的用户。
- 作为标准输入读取。如果没有指定命令，`at` 将提示你输入命令 `at>`，如下例所示。你必须按 Ctrl+D 来指示命令的结束（<EOT>）。

```
at 23:40
at> cd /tmp/perl500_56
at> make
at> ls -al
at> <EOT>
```

- 从文件读取。当 `-f` 命令行选项后跟着有效文件名时，该文件的内容将作为执行的命令，例如：`at -f /root/runme now + 5 hours` 这将在5小时后运行在 /root/runme 中的命令。文件可以是简单的命令列表，也可以是在独立的 shell 中运行的脚本（即文件以 #bin/bash 或其他 shell 开头）。

## 查看作业

你可以使用 `atq` 命令等同于 `at -l`）查看队列中待处理作业的列表，显示作业的序列号、计划运行的日期和时间以及作业所在的队列。

两个最常见的队列名称是“a”，代表队列，“b”代表批队列。所有其他字母（大写或小写）都可以用于指定优先级更低的队列。如果 `atq` 命令列出的队列名称为 =，表示该作业正在运行。以下是 `atq` 命令的输出示例：

```
# atq
2 1999-07-02 00:51 a
3 1999-07-02 00:52 a
4 1999-07-05 23:52 a
```

## 删除计划执行的任务

如果你决定取消某个特定的任务，可以使用 `atrm` 命令（等同于 -d），并结合 `atq` 命令报告的任务编号（或多个编号）来操作。例如，使用 `atq` 的以下输出：

```bash
# atq
18 1999-06-01 03:00 a
19 1999-06-29 05:27 a
20 1999-06-30 05:27 a
21 1999-07-14 00:01 a
22 1999-09-01 03:00 a
```

你可以使用 `atrm 19 20` 命令从队列中删除计划在 6 月 29 日和 6 月 30 日 5:27 运行的任务。

## 使用 batch 命令

如果你的机器上系统资源非常紧张，或者你提交的任务可以以低于正常的优先级运行，那么 `batch` 命令（等同于 -q b）可能会很有用。它由同一个 at 守护进程控制，并允许以与提交相同的格式提交任务（尽管时间指定是可选的）。

然而，为了防止你的任务占用稀缺的处理器时间，任务只有在系统负载平均值低于特定值时才会运行。默认值为 0.8，但可以通过指定命令行选项添加 cron 来修改此值。这在后面描述启动和关机的章节中曾用作示例。这里是 `batch` 命令的一个示例。

```bash
batch
at> -h /home > /tmp/duhome
at> <Ctrl-d>
```

在这个示例中，在我输入 `batch` 命令后，将调用该功能以允许我输入想要运行的命令（或）。输入 `du -h /home > /tmp/duhome` 命令行会将 /home 目录下所有内容的磁盘使用情况输出到 /tmp/duhome 文件中。在下一行，按下 Ctrl-d 结束批任务。只要负载平均值足够低，命令就会执行。

## 使用 cron 设施
