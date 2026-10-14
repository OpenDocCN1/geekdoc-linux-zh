

与之前的密码类似，是字典词，或太容易猜到。

```
[me@linuxbox ~]$ passwd
(current) UNIX password:
New UNIX password:
BAD PASSWORD: is too similar to the old one
New UNIX password:
BAD PASSWORD: it is WAY too short
New UNIX password:
BAD PASSWORD: it is based on a dictionary word
```

如果您拥有超级用户权限，可以将用户名作为参数指定给 passwd 命令，以为其他用户设置密码。超级用户还有其他选项可用于允许锁定账户、密码过期等。有关详细信息，请参阅 passwd 手册页。

## 总结

在本章中，我们看到了类 Unix 系统（如 Linux）如何管理用户权限以允许对文件和目录进行读取、写入和执行访问。该权限系统的基本思想可以追溯到 Unix 的早期时代，并且经受住了时间的考验。但是类 Unix 系统中的原生权限机制缺乏更现代系统的精细粒度。

## 10
进程

![](img/314a0280bc10c5c0d45be132de172677_159_0.png)

现代操作系统通常是*多任务*的，这意味着它们通过快速在各个正在执行的程序之间切换来制造同时做多件事情的假象。内核通过使用*进程*来管理这一点。进程是 Linux 组织等待 CPU 轮到的不同程序的方式。

有时计算机会变得迟缓或应用程序停止响应。在本章中，我们将查看命令行上可用的一些工具，让我们检查程序正在做什么以及如何终止行为不正常的进程。

本章将介绍以下命令：

- **ps** 报告当前进程的快照
- **top** 显示任务
- **jobs** 列出活动作业
- **bg** 将作业置于后台
- **fg** 将作业置于前台
- **kill** 向进程发送信号
- **killall** 按名称终止进程
- **shutdown** 关闭或重新启动系统

## 进程如何工作

系统启动时，内核以进程的形式启动其自身的几个活动并启动一个名为 init 的程序。init 又运行一系列位于 /etc 的 shell 脚本（称为 init 脚本），这些脚本启动所有系统服务。其中许多服务以守护进程程序的形式实现，守护进程程序只是坐在后台做它们的事情而没有任何用户界面。因此，即使我们没有登录，系统也在至少进行一些例行工作。

程序可以启动其他程序这一事实在进程方案中表现为父进程产生子进程。

内核维护有关每个进程的信息以帮助保持组织有序。例如，每个进程都被分配一个称为进程 ID（PID）的编号。PID 按升序分配，其中 init 始终获得 PID 1。内核还跟踪分配给每个进程的内存，以及进程恢复执行的就绪情况。与文件一样，进程也有所有者、用户 ID、有效用户 ID 等。

## 查看进程

查看进程的最常用命令（有几个）是 ps。ps 程序有很多选项，但在最简单的形式下使用如下：

```
[me@linuxbox ~]$ ps
PID TTY          TIME CMD
5198 pts/1    00:00:00 bash
10129 pts/1    00:00:00 ps
```

此示例中的结果列出了两个进程，进程 5198 和进程 10129，分别是 bash 和 ps。正如我们所见，默认情况下，ps 并没有向我们显示太多内容，只是与当前终端会话关联的进程。要查看更多内容，我们需要添加一些选项；不过，在这样做之前，让我们先看看 ps 生成的其他字段。TTY 是“电传打字机”的缩写，指进程的控制终端。这里 Unix 显示出它的年代。TIME 字段是进程消耗的 CPU 时间。正如我们所见，没有一个进程让计算机工作得很辛苦。

如果我们添加一个选项，我们就可以更全面地了解系统正在做什么。

```
[me@linuxbox ~]$ ps x
PID TTY      STAT   TIME COMMAND
2799 ?        Ss l    0:00 /usr/libexec/bonobo-activation-server -ac
2820 ?        Sl     0:01 /usr/libexec/evolution-data-server-1.10 --
15647 ?       Ss     0:00 /bin/sh /usr/bin/startkde
15751 ?       Ss     0:00 /usr/bin/ssh-agent /usr/bin/dbus-launch --
15754 ?       S      0:00 /usr/bin/dbus-launch --exit-with-session
15755 ?       Ss     0:01 /bin/dbus-daemon --fork --print-pid 4 -pr
15774 ?       Ss     0:02 /usr/bin/gpg-agent -s -daemon
15793 ?       S      0:00 start_kdeinit --new-startup +kcminit_start
15794 ?       Ss     0:00 kdeinit Running...
15797 ?       S      0:00 dcopserver --nosid
-- snip --
```

添加 x 选项（注意前面没有破折号）告诉 ps 显示我们所有的进程，而不管它们是否受某个终端控制。TTY 列中出现 ? 表示没有控制终端。使用此选项，我们可以看到我们拥有的每个进程。

由于系统运行了大量进程，ps 会产生很长的列表。将 ps 的输出通过管道传输到 less 中以便更轻松地查看通常很有帮助。一些选项组合也会产生很长的输出行，因此最大化终端模拟器窗口可能也是个好主意。

输出中新增了一列名为 STAT。STAT 是状态的缩写，显示进程的当前状态，如表 10-1 所示。

### 表 10-1：进程状态

| 状态 | 含义 |
|-------|---------|
| R | 运行中。这意味着进程正在运行或准备运行。 |
| S | 睡眠中。进程未运行；相反，它正在等待事件，例如按键或网络数据包。 |

