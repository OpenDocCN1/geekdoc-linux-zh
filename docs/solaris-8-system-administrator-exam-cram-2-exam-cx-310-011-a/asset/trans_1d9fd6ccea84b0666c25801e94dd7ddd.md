

答案 a 和 d 是正确的。root 用户可以使用 **admintool** 和 **passwd** 命令来更改密码。**passmgmt** 和 **usermod** 命令不提供任何指定密码的功能。因此，答案 b 和 c 是错误的。

## 问题 12

哪个命令会显示当前登录到系统的所有用户？（请选择所有适用的选项。）

- [ ] a. **who**
- [ ] b. **last**
- [ ] c. **whodo**
- [ ] d. **id**

答案 a、b 和 c 是正确的。**who**、**last** 和 **whodo** 命令会显示当前登录到系统的所有用户。**id** 命令显示指定用户账户的真实和有效 UID、GID 及所属组。因此，答案 d 是错误的。

## 需要了解更多信息？

- Mulligan, John P. 著，*Solaris 与必备参考*（New Riders，印第安纳波利斯，印第安纳州：2001），ISBN 0-7357-1007-4。
- Sobell, Mark G. 著，*Solaris 实用指南*（Addison-Wesley，雷丁，马萨诸塞州：1999），ISBN 0-201-89548-X。
- Sun Microsystems 公司，*系统管理指南，第 1 卷*。提供印刷版本（部件号 805-7228-10），也可在 **http://docs.sun.com** 网站上获取，还可从 Solaris 8 操作系统附带的在线文档 AnswerBook2 中获取。
- Sun Microsystems 公司，*系统管理指南，第 2 卷*。提供印刷版本（部件号 805-7229-10），也可在 **http://docs.sun.com** 网站上获取，还可从 Solaris 8 操作系统附带的在线文档 AnswerBook2 中获取。
- Sun Microsystems 公司，*系统参考手册，第 1 部分——用户命令*。提供印刷版本（部件号 806-0624-10），也可在 **http://docs.sun.com** 网站上获取，还可从 Solaris 8 操作系统附带的在线文档 AnswerBook2 中获取。
- Sun Microsystems 公司，*系统参考手册，第 1M 部分——系统管理命令*。提供印刷版本（部件号 806-0625-10），也可在 **http://docs.sun.com** 网站上获取，还可从 Solaris 8 操作系统附带的在线文档 AnswerBook2 中获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_179_0.png)

## 控制进程

**你需要理解的术语：**

- ✓ 进程属性
- ✓ **ps**、**prstat** 和 **pgrep** 命令
- ✓ 信号
- ✓ **kill** 和 **pkill** 命令
- ✓ **cron** 和 **crontab** 命令
- ✓ Crontab 文件

**你需要掌握的技巧：**

- ✓ 使用 **ps**、**prstat** 和 **pgrep** 命令查看进程属性
- ✓ 使用 **kill** 和 **pkill** 命令终止进程
- ✓ 使用 **cron** 和 **at** 命令调度进程
- ✓ 控制 **cron** 和 **at** 命令的使用

本章介绍如何控制系统上运行的程序或进程。这种控制包括查看进程状态、按需终止进程，以及调度进程的自动启动。本章涵盖*进程控制*的考试目标。

### 查看和终止进程

**ps(1)**、**prstat(1M)** 和 **pgrep(1)** 命令用于查看进程属性，而 **kill(1)** 和 **pkill(1)** 命令用于终止进程。

#### ps 命令

**ps** 命令用于显示活动进程的信息。不带任何命令行参数时，**ps** 命令显示与执行该命令的用户账户具有相同有效用户 ID（UID）的进程。表 7.1 列出了 **ps** 命令支持的命令行参数。

通过 **ps** 命令及其多种显示格式，可以获取大量关于进程的信息。

![](img/b957f979417d9f16274c2eb52c8f2c9f_180_0.png)

进程默认显示的信息包括进程 ID（PID）、关联的终端设备（TTY）、累计执行时间（TIME）以及程序或命令名称（CMD）。除非特别省略，否则这些信息会包含在所有显示格式中。

| 参数 | 说明 |
|---|---|
| `-a` | 显示所有进程，但进程组组长和与终端无关联的进程除外 |
| `-A` | 显示所有进程（等同于 `-e`） |
| `-c` | 显示备用列 |
| `-d` | 显示所有进程，但进程会话首脑除外 |
| `-e` | 显示所有进程 |
| `-f` | 使用完整列表显示格式 |
| `-g` *进程组 ID* | 显示具有指定进程组 ID 的进程 |
| `-G` *组 ID* | 显示具有指定进程组 ID（GID）的进程 |
| `-j` | 显示会话 ID 和进程组 ID |
| `-l` | 使用长列表显示格式 |
| `-L` | 显示每个轻量进程（LWP）的信息 |
| `-n` *名称* | 使用备用的名称列表文件（已忽略） |
| `-o` *格式* | 使用备用显示格式 |
| `-p` *进程 ID* | 显示具有指定进程 ID（PID）的进程 |
| `-P` | 显示执行该进程的处理器编号（仅在多处理器系统上有意义） |
| `-s` *进程会话 ID* | 显示具有指定进程会话 ID 的进程 |
| `-t` *终端设备路径* | 显示与指定终端设备路径关联的进程 |
| `-u` *有效用户 ID* | 显示具有指定有效用户 ID 的进程 |
| `-U` *真实用户 ID* | 显示具有指定真实用户 ID 的进程 |
| `-Y` | 在长列表中显示备用列 |

所有用于指定 ID 的命令行参数——例如进程组 ID、真实组 ID、PID、进程会话 ID、有效 UID 和真实 UID——都接受多个 ID（用逗号分隔）。对于真实和有效用户 ID 以及真实组 ID，可以指定数字 ID 或账户名称。

以下输出示例使用了带有几个不同命令行参数的 **ps** 命令：

```text
$ ps -udla
   PID TTY      TIME CMD
   781 pts/5    0:19 xterm
   782 pts/5    0:00 sh
   910 pts/5    0:10 telnet
   913 pts/6    0:01 sh
$ ps -t pts/6
   PID TTY      TIME CMD
   782 pts/5    0:00 sh
   910 pts/5    0:10 telnet
$ ps -f -udla
   UID  PID PPID  C  STIME TTY      TIME CMD
   dla  781    0  0  Aug 28 ?        0:19 xterm -display
   dla  782  781  0  Aug 28 pts/5    0:00 sh
   dla  910  782  0  Aug 28 pts/5    0:10 telnet solaris
   dla  913  911  0  Aug 28 pts/6    0:01 -sh
$
```

PPID 列列出进程的父 PID，C 列列出处理器利用率（已过时），STIME 显示开始日期。

#### prstat 命令

prstat(1M) 命令生成活动进程的统计报告。如果使用时不带任何命令行参数，则会显示所有活动进程的信息，并按 CPU 使用率排序。报告大约每三秒更新一次，直到被终止。以下输出示例展示了 prstat 命令的用法：

```text
$ prstat
 PID USER  SIZE  RSS STATE   PRI NICE      TIME  CPU PROCESS/NLWP
7793 dla   1032K 844K cpu0     58    0  0:00:00 0.1% prstat/1
 789 dla   2960K 2132K sleep    58    0  0:00:00 0.1% xterm/1
 217 root  1908K 1100K sleep    53    0  0:00:00 0.1% mscd/7
 312 root  1936K  660K sleep    48    0  0:00:00 0.1% nfsiod/12
 397 root   64M   47M sleep     59    0  0:00:07 0.0% perimeter/1
 790 dla    808K  628K sleep    41    0  0:00:00 0.0% sh/1
 177 root  1576K  0K   sleep    30    0  0:00:00 0.0% lockd/1
 229 root  2692K  0K   sleep    48    0  0:00:00 0.0% lpsched/1
 165 root  1940K  696K sleep    58    0  0:00:00 0.0% in.named/1
 250 root   804K  480K sleep    58    0  0:00:00 0.0% utmpd/1
 188 root  2720K  664K sleep    58    0  0:00:00 0.0% automount/5
 143 root  2144K  672K sleep    58    0  0:00:00 0.0% rpcbind/1
 129 root  1552K  300K sleep    59    0  0:00:00 0.0% in.ndpd/1
 122 root  1304K  220K sleep    58    0  0:00:00 0.0% routed/1
Total: 64 processes, 146 lwps, load averages: 0.11, 0.04, 0.05
$
```

**prstat** 的命令行参数允许你根据 PID、所有者的 UID、所使用的 CPU 等来选择要监控的进程。表 7.2 列出了 **prstat** 的命令行参数。

| 参数 | 说明 |
|---|---|
| `-a` | 分别显示进程和用户的报告。 |
| `-c` | 打印新的报告，而不是覆盖初始报告。 |
| `-C` *集合* | 仅报告绑定到指定处理器集的进程。 |
| `-L` | 报告每个 LWP。 |
| `-m` | 报告微状态信息。 |
| `-n` *数量* | 将报告限制为窗口或终端中的 **数量** 行。默认使用整个显示区域。 |
| `-p` *PID 列表* | 仅报告其 PID 由 **PID 列表** 列出的进程。 |
| `-P` *CPU 列表* | 仅报告在 **CPU 列表** 所列 CPU 上执行的进程。 |
| `-R` | 在实时模式下执行 **prstat**。 |

