
```
12061 ? 00:00:00 inetd
12063 ? 00:00:00 rpc.portmap
12086 ? 00:00:00 amd
12092 ? 00:00:00 rpcidd
12093 ? 00:00:00 lockd
12103 ? 00:00:00 cron
12109 ? 00:00:00 atd
12115 ? 00:00:00 sendmail
12129 ? 00:00:00 rpc.statd
12158 ? 00:00:00 httpd.apache
12164 ? 00:00:00 httpd.apache
12165 ? 00:00:00 httpd.apache
12228 tty1 00:00:00 getty
12229 tty2 00:00:00 getty
12230 tty3 00:00:00 getty
12231 tty4 00:00:00 getty
12232 tty5 00:00:00 getty
12233 tty6 00:00:00 getty
12234 ? 00:00:00 sh
12235 ? 00:00:00 rc.gui
12237 ? 00:00:00 kdm
12239 ? 00:07:26 X
14269 ? 00:00:02 kwmsound
29595 ? 00:00:00 kdm
29608 ? 00:00:18 kwm
29629 ? 00:00:01 kbg
29658 ? 00:00:26 kfm
29659 ? 00:00:00 audioserver <defunct>
29660 ? 00:00:00 kwmsound <defunct>
29661 ? 00:00:02 krootwm
29662 ? 00:00:14 panel
29665 ? 00:00:02 kdizard
19603 ? 00:01:02 kvt
19605 pts/0 00:00:34 bash
30089 pts/0 00:00:00 vi
30425 pts/0 00:00:00 paste
32040 pts/0 00:00:00 cat
1183 pts/0 00:00:00 awk
30704 pts/0 00:00:00 ps
$
```

注意显示中的以下项目：

- 系统启动时启动的最小数字 `PID`（注意项目 1 到 5）。通常情况下，这些是关键进程；如果它们没有出现，部分或全部系统将无法工作。

- 并非所有进程都绑定到了终端。问号 (`?`) 表示该进程在系统中运行，没有终端交互或没有默认输出终端。

- 每个终端都运行一个 `getty`。虽然没有用户在使用 `tty1` 到 `tty6`，但很容易看出这些代表了用户可以与系统交互的六个终端。

你可以使用的其他确定显示信息的选项包括：

- `-l`: 显示详细列表（参考 `-l`）。

- `-u`: 显示用户名和相关统计。

- `-f`: 显示完整列表（所有内容）。

最后一个选项经常被使用，并受到管理员的青睐，因为它为显示增加了额外的列：

```
$ ps -f
UID PID PPID C STIME TTY CMD
root 19605 19603 0 Aug pts/0 00:00:34 bash
root 30089 19605 0 Aug pts/0 00:00:00 vi fileone
root 30425 19605 0 Aug pts/0 00:00:00 paste_d filesize
root 32040 19605 0 Aug 22 pts/0 00:00:00 cat
root 1183 19605 0 Aug 23 pts/0 00:00:00 awk -F: questions
root 30778 19605 0 14:25 pts/0 00:00:00 ps -f
$
```

现在存在四个之前没有的列。第一列识别与进程关联的用户 ID。第三列识别该进程报告给哪个进程（第五项结果的图形表示请参见图 6.3）。第四列指示是否涉及调度，第五列是进程启动的时间。

> 请注意，使用 `f` 时，`CMD` 列出的是整个命令，而像其他显示那样只列出部分。

![](img/f9e5762d07ca45a6f38ffcb92cd56e5e_147_0.png)

你可以组合这些选项；最常见的组合是 `ef`，它以完整格式显示所有进程：

## 进程操作

![](img/f9e5762d07ca45a6f38ffcb92cd56e5e_148_0.png)

图 6.3 `ps -f` 暗示的父子关系图形表示。

```
$ ps -ef
root PID PPID C STIME TTY CMD
root 1 0 Jul 6 00:00:05 init [5]
root 2 1 Jul 6 00:00:39 kflushd]
root 3 1 Jul 6 00:00:00 kpiod]
root 4 1 Jul 6 00:00:15 kswapd]
root 5 1 Jul 6 00:00:00 mdrecovery]
root 11635 ? 00:00:11 update]
root 12046 ? 00:00:00 syslog]
root 12049 ? 00:00:00 klogd]
root 12061 ? 00:00:00 inetd]
root 12063 ? 00:00:00 rpc.portmap]
root 12086 ? 00:00:00 amd]
root 12092 ? 00:00:00 rpcidd]
root 12093 ? 00:00:00 lockd]
root 12103 ? 00:00:00 cron]
root 12109 ? 00:00:00 atd]
root 12115 ? 00:00:00 sendmail]
root 12129 ? 00:00:00 rpc.statd]
root 12158 ? 00:00:00 httpd.apache]
root 12164 ? 00:00:00 httpd.apache]
root 12165 ? 00:00:00 httpd.apache]
root 12228 tty1 00:00:00 getty]
root 12229 tty2 00:00:00 getty]
root 12230 tty3 00:00:00 getty]
root 12231 tty4 00:00:00 getty]
root 12232 tty5 00:00:00 getty]
root 12233 tty6 00:00:00 getty]
root 12234 ? 00:00:00 sh]
root 12235 ? 00:00:00 rc.gui]
root 12237 ? 00:00:00 kdm]
root 12239 ? 00:07:26 X]
root 14269 ? 00:00:02 kwmsound]
root 29595 ? 00:00:00 kdm]
root 29608 ? 00:00:18 kwm]
root 29629 ? 00:00:01 kbg]
root 29658 ? 00:00:26 kfm]
root 29659 ? 00:00:00 audioserver <defunct>]
root 29660 ? 00:00:00 kwmsound <defunct>]
root 29661 ? 00:00:02 krootwm]
root 29662 ? 00:00:15 kanel]
root 29665 ? 00:00:02 kdewizard]
root 19603 29658 08 Aug 10? 00:01:03 vt -T ption -icon kvt.
root 19605 pts/0 00:00:34 bash
root 30089 pts/0 00:00:00 vi fileone
root 30425 pts/0 00:00:00 paste_d filesize
root 32040 pts/0 00:00:00 cat
root 1183 pts/0 00:00:00 awk -F: questions
root 30778 19605 0 14:25 pts/0 00:00:00 ps -f
$
```

```
tty3 12231 1 00 Jul 6 tty4 00:00:00 /sbin/getty

root 12237 1 00 Jul 6 tty5 00:00:00 /sbin/getty

tty4 linux 12232 1 00 Jul 6 tty6 00:00:00 /sbin/getty

tty5 linux 12233 1 00 Jul 6 tty7 00:00:00 /sbin/getty

tty6 linux 12234 1 00 Jul 6 tty8 00:00:00 /sbin/getty

root 12235 12234 0 Jul 6 00:00:00 /bin/sh -c /etc/rc.d/rc.gui

root 12237 12235 0 Jul 6 00:00:00 /opt/kde/bin/knd -daemon
```
