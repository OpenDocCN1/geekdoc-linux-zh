
`root 745 0.0 1 3510 2804 ?? SS 3:30PM 02:01.04 mailsend.`

```
$ ps 显示 tty 进程

PID STAT COMMAND

1133 S 00:00:38 -sh (sh)

2595 R 00:00:00 -t tty0

$ ps -p 1129 -o pid,tty,time,args 显示 PID 1129 的信息

PID TTY TIME COMMAND

1129 chris 07:00:08 chris:chriv (sshd)

$ ps -U chris,francis -o pid,tty,stat,args 查看两个用户的信息

PID USER TTY STAT COMMAND

1132 chris ? S sshd: chris:ttyp0 (sshd)

2480 chris ?? S sshd: chris:ttyp1 (sshd)
```

## 使用 top 监控进程

如果你想持续查看运行中的进程，可以使用 `top` 命令。`top` 命令运行一个面向屏幕的运行进程视图并持续更新。如果你在不带任何选项的情况下使用 `top` 命令，它将显示系统的运行时间、任务、`CPU` 使用率和内存使用情况，随后是按使用率排序的运行进程列表。这是一个示例：

```
$ top

last pid: 2697; load averages: 0.04, 0.03, 0.00  up 00:48:44

00:14:17

58 processes: 1 running, 57 sleeping

cpu states: 0.0% user, 0.0% nice, 0.8% system, 0.0% interrupt, 99.2% idle

Mem: 58M Active, 97M M, 73M Wired, 12M Cache, 34M Buf, 1508 Free

Swap: 484M Total, 484M Free

PID USER THR NI SIZE RES STAT TIME WCPU COMMAND

2696 chris 1 96 02532K 15520K select 0:03 2.05% gtiali

2618 chris 1 96 08392K 14300K select 0:03 0.00% Xorg

2652 chris 3 20 034244K 31506K kresel 0:07 0.00% nautilus

2650 chris 1 96 026564K 16688K select 0:04 0.00% gnome-panel
```

# 第 9 章：检查和管理运行中的进程

以下是你可以使用的其他选项，用于启动 `top` 以持续显示运行中的进程：

- `$ top -s 5` 将更新延迟更改为 5 秒（从 3 秒改为）
- `$ top -u francois` 仅显示有效用户名为 `francois` 的进程
- `$ top -s` 显示系统进程以及其他进程
- `$ top -d 10` 在退出前刷新屏幕 10 次
- `$ top -b` 以非交互式、非屏幕导向的批模式运行

此 `top -b` 示例将 `top` 的输出格式化为适合输出到文件的形式，而不是在屏幕上重绘相同的屏幕以进行交互式查看。这可以用于创建进程日志，例如，在半夜寻找耗尽你所有资源的进程时。以下是运行 `top` 并记录 10 分钟输出的方法：

- `$ top -b -d 12000 > myprocesslog`

当 `top` 运行时，你可以通过不同的方式更新和排序进程列表。要立即更新进程列表，按 `Space` 按 `CPU` 和加权 `CPU` 时间进行排序。按 `I` 隐藏空闲进程或显示它们。或者，按 `m` 在 `CPU` 和 `IO` 模式之间切换。在 `IO` 模式下，按 `o` 选择数据排序的顺序。

有几种方法可以在 `top` 运行时更改其行为。按 `s` 并输入代表秒的类型来更改刷新的延迟。按 `u` 输入用户名以仅显示所选用户的进程。按 `Ctrl-L` 重新绘制屏幕。

你可以以不同的方式对任何运行中的进程进行操作。要向运行中的进程发送信号（杀死进程），输入 `k` 然后输入你想要发送信号的进程的 `PID`。这将发送默认的 `15 (TERM)`，允许进程以有序的方式关闭。要给予更高的或更低的运行优先级，输入 `r` 然后添加一个负数（增加优先级）或正数（降低优先级），最后加上你想更改的进程 ID。

如果你想找到更多关于如何使用 `top` 的信息，可以在 `top` 会话期间输入 `?`。主页有很多关于如何使用 `top` 的信息：

```
$ man top 查看 top 的 man 页面
```

当你使用 `top` 时，输入 `q` 退出。

## 查找和控制进程

更改进程首先意味着找到你想更改的进程，然后修改其处理优先级或发送信号来改变其行为。如果你在寻找某个特定的进程，你可能会在 `ps` 或 `top` 输出的大型进程列表中找到并定位它。`pgrep` 命令提供了在活动进程中搜索你正在寻找的进程的方法。`renice` 命令允许你更改运行中进程的处理优先级。`kill`、`pkill` 和 `killall` 命令允许你向运行中的进程发送信号（包括结束这些进程的信号）。

# 使用 pgrep 查找进程

在最基本的形式中，你使用 `pgrep` 搜索命令（或命令的一部分），并产生包含该名称的任何进程的进程 ID。例如：

```
$ pgrep init

显示包含 'init' 字符串的任何进程的 PID

2617

1
```

由于我们知道只有一个 `init` 进程在运行，我们使用 `-l` 选项来查看每个进程的命令名称（以了解哪些进程出现了）：

```
$ pgrep -l init

显示包含 'init' 的任何进程的 PID 和名称

2617

1 init
```

你也可以搜索与特定用户相关的进程：

```
$ pgrep -lu chris

列出所有用户 chris 拥有的进程

2803 vim

2552 bash

2551 sshd
```

使用 `pgrep` 最有用方法可能是找到运行中进程的进程 ID，并将这些 `PID` 管道到另一个命令以产生输出。以下是示例（寻找其他如 `metacity` 或 `firefox` 未运行的命令）：

```
$ ps -p 'pgrep metacity'

搜索 metacity 并运行 ps (短格式)

PID TID STAT COMMAND

2617 ? S 00:07:02 /usr/local/bin/metacity --sm-client-id=default0

$ ps -f 'pgrep init'

搜索 init 并运行 ps (全格式)

PID TID STAT COMMAND

2617 v2 I+ 00:01 /usr/X16/bin/home/.initrc

$ renice -5 'pgrep firefox'

搜索 firefox，提高其优先级

2052:旧优先级 0, 新优先级 -5

2057:旧优先级 0, 新优先级 -5
```

任何可以接受进程 ID 作为输入的命令都可以以这些方式与 `pgrep` 结合。正如前面的 `pgrep` 示例所示，你可以使用 `renice` 等命令来更改进程在运行时的行为。

# 使用 fuser 查找进程

定位特定进程另一种方法是根据进程正在访问的内容。`fuser` 命令（作为 `root`，输入 `pkg_add -r fuser`）可用于查找当前哪些进程打开了文件或套接字。找到进程后，可以使用 `fuser` 向这些进程发送信号。`fuser` 命令最有用用于查找哪些文件被挂载文件系统（如硬盘或 `Samba` 共享）上的进程打开。找到这些进程允许你正确地关闭它们（如果必须，则直接杀死它们），以便卸载文件系统。以下是 `fuser` 命令的某些示例，用于列出在选系统中打开了文件的进程：

```
# fuser -cu /home 输出打开 /home 的进程（带用户名）

...（此处省略具体输出，原文逻辑保持一致）
```

# 第 9 章：检查和管理运行进程

在下面的命令序列中，我们从终端窗口启动了 `GIMP` 图像程序。随后有一系列控制键和命令用于停止、启动进程，以及将其在前台和后台之间移动：

```
$ gimp                在前台运行 gimp

<Ctrl+Z>            停止进程并将其放入后台

[1]+ Stopped        gimp

$ bg 1             在后台重新启动运行进程 (bash)

$ bg %1             在后台重新启动运行进程 (sh)

$ fg 1              在前台继续运行进程 (bash)

$ fg %1             在前台继续运行进程 (sh)

gimp

<Ctrl+C>            杀死进程
```

请注意，放置在后台的进程带有一个作业 ID（`job ID`）符号及其对应的数字（例如 `%1`），你可以通过 `bg` 和 `fg` 命令或通过 `shell` 来识别特定的进程；在命令中输入该数字（如 `fg 1`）。当当前 `shell` 运行一个或多个后台作业时，你可以使用该命令来管理正在运行的作业：

```
$ jobs             显示当前 shell 的后台作业

[1] Running         gimp &

[2] Running         xmms &

[3]- Running         gedit &

[4]+ Stopped         gtali

$ jobs -1 %2       显示每个作业信息并包含 PID

[1] 31676 Running      gimp &

[2] 31677 Running      xmms &

[3]- 31683 Running     gedit &

[4]+ 31688 Stopped     gtali

                      仅显示作业 %2 的信息

                      xmms &
```

在 `jobs` 中运行的进程可能是你在登录（`ssh`）远程系统时完成的，但你想在本地桌面上运行 `GUI` 应用。通过在后台运行这些进程，你可以同时运行多个应用程序，同时保持它们与当前 `shell` 关联。

> 注意：使用 `fg` 或 `bg` 时，如果没有指定要操作哪个进程，将使用当前作业。当前作业旁边有一个加号 (`+`)。

`fg` 和 `bg` 命令通过将进程移动到前台或后台来手动操作运行中的进程。另一种操作运行命令的方法是直接向这些进程发送信号。向运行进程发送信号的一种常用方法是使用 `kill` 和 `killall` 命令。

## 杀死和信号进程

你可以通过向进程发送信号来停止或更改运行中的进程。`kill` 和 `killall` 命令可以向运行的进程发送你选择的信号，正如其名称所示，这通常是杀死进程的信号。

信号由数字（`9`、`15` 等）和字符串（`SIGKILL`、`SIGTERM` 等）表示。表 9-2 显示了你可以向 `BSD` 系统中的进程发送的标准信号。

### 表 9-2：发送给进程的标准信号

| 信号数字 | 信号名称 | 描述 |
|---|---|---|
| 1 | `SIGHUP` | 终端挂断或控制进程死亡 |
| 2 | `SIGINT` | 中断程序 |
| 3 | `SIGQUIT` | 退出程序 |
| 4 | `SIGILL` | 非法指令 |
| 5 | `SIGTRAP` | 跟踪陷阱 |
| 6 | `SIGABRT` | 从 `abort` 函数发送的终止 |
| 7 | `SIGEMT` | 执行了模拟指令 |
| 8 | `SIGFPE` | 浮点数异常 |
| 9 | `SIGKILL` | 杀死信号 |
| 10 | `SIGBUS` | 总线错误 |
| 11 | `SIGSEGV` | 段违规 |
| 12 | `SIGSYS` | 调用了不存在的系统调用 |
| 13 | `SIGPIPE` | 管道破（无可读或写） |
| 14 | `SIGALRM` | 来自闹系统调用的信号 |
| 15 | `SIGTERM` | 终止信号 |
| 16 | `SIGURG` | 丢弃信号 |
| 17 | `SIGSTOP` | 停止进程 |
| 18 | `SIGTSTP` | 在终端输入的停止 |
| 19 | `SIGCONT` | 如果进程已停止则继续 |
| 20 | `SIGCHLD` | 子进程状态改变 |
| 21 | `SIGTTIN` | 终端尝试读取后台进程 |
| 22 | `SIGTTO` | 终端尝试向后台进程写入 |

`kill` 命令可以通过 ID 或作业号向进程发送信号，而 `killall` 命令可以根据命令名称向进程发送。以下是一些示例：

```
$ kill 28665

$ kill - 4895

$ kill -SIGCONT 5254

$ kill %3

$ killall spamd

$ killall -SIGHUP sendmail
```

向 `PID` 为 `28665` 的进程发送 `SIGTERM`
向 `PID` 为 `4895` 的进程发送 `SIGKILL`
继续已停止的进程 (`pid` `5254`)
杀死作业 `#3` 代表的进程
杀死当前运行的所有守护进程
让 `sendmail` 进程重新读取配置文件

`SIGKILL` (`9`) 信号通常被热衷于触发信号的管理员使用，应保留作为最后的手段。它不允许进程整洁地退出。这可能会导致该进程处理的数据丢失或损坏。`SIGKILL` 原本用于 `UNIX` 系统，表示终端与主机断开（例如拨号调制调器挂起）。然而，`sendmail` 和 `httpd` 等守护进程被实现为捕获 `SIGKILL`。

## 离开当前 shell 运行进程

如果你希望进程即使在断开连接后也运行，有几种方法可以。`at` 和 `batch` 命令用于队列命令。在这里：

```
$ at now             启动一个命令

mycript. &
```

`at` 和 `batch` 命令使用次级 `at` 提示符。在该提示符处输入你想运行的命令。之后你可以输入命令。完成后，单独占一行按 `Ctrl+D` 来队列命令。

```
$ at now +5             在 5 天后启动命令
```

`at` 和 `batch` 命令用于一次性任务。这些命令被编写进 `cron` 作业，并在 `crontab` 文件中进行调度。有一个系统级 `crontab` 文件 (`/etc/crontab`)。此外，每个用户都可以按照自己选择的时间创建个人 `crontab`。要创建个人 `crontab`，输入以下内容：

```
$ crontab -e             创建个人 crontab 文件
```

`crontab -e` 命令使用 `vi` 编辑器打开你的 `crontab` 文件（或创建一个新的）。以下是可以添加到 `crontab` 的几个条目示例：

```
15 8 * * Mon,Tue,Wed,Thu,Fri mail < /var/project/stats.txt

* * 1,4,7,10 * find / | grep .doc $ > /var/sales/documents.txt
```
