
## 需要多长时间？

  你可以使用 **time** 命令来查看你的 shell 程序运行所耗用 **时间** 的报告。**time** 的输出在许多 UNIX 变体中有所不同。你可能需要查看 **time** 的手册页，以了解你可以预期的输出。**csh** 中 **time** 的典型输出如图 11-5 所示。

![](img/75f39fc91296b889c0653851accdfd46_775_0.png)

  由于你编写的一些脚本可能会消耗大量的系统资源，你可能需要考虑研究 C shell 的一些作业控制功能。你可以使用的最简单的作业控制是在后台运行脚本，从而使脚本的优先级较低。通过输入脚本名称后跟 **&**，你将在后台运行该脚本。如果你在后台运行多个脚本，你可以通过发出 **jobs** 命令来获取这些脚本的状态。这是一个更高级的 C shell 主题，但根据你编写的脚本的复杂度，你可能需要研究作业控制。

## 第 11 章中使用的一些命令的手册页

  本章不包含任何手册页。本章中使用的命令的手册页出现在许多其他章节中，包括：

- csh - 第 7 章
- ksh - 第 6 章
- **grep**、**awk**、**sed** 和其他工具 - 第 10 章

# 第 12 章

# 系统管理简介

## 系统管理

  在这本书中，我们一直围绕着系统管理展开讨论。我们已经涉及了许多系统管理内容，例如在 shell 编程章节中列出和终止进程，查看可用磁盘空间等。在本章中，我们将查看许多无侵入性的系统管理命令。所谓无侵入性，我的意思是那些不改变你系统设置且用户通常可以运行的命令。

  你的系统管理员负责系统的设置和操作；然而，系统设置的许多方面是用户可能感兴趣的。我们将介绍许多与系统设置和系统运行方式相关的常用命令。作为用户，你可能对系统的操作方式和与系统管理相关的命令感兴趣。此外，还有一些与你的工作直接相关的命令，例如列出你正在运行的进程以及如何终止它们，这些命令可以作为用户运行。

  在章末，我也提供了本章使用的许多命令的手册页。系统管理中发生的许多事情在用户手册中只能作简要介绍，而手册页提供了更多细节，但依然不会让你成为系统管理专家。

  本章中的示例是在 Solaris、HP-UX、AIX 和 Linux 系统上执行的；不过，这些命令和文件在不同系统之间是相似的，因此你应该能够将本章中的信息与你的 UNIX 变体联系起来。

  大多数 UNIX 变体都附带一个系统管理工具。该工具提供了一种基于菜单的方式来执行常见的系统管理任务，例如管理以下内容：用户和组；磁盘和文件系统；网络；打印机；等等。没有广泛使用的此类管理工具标准，因此每个 UNIX 变体都不同。这些工具通常需要超级用户权限才能运行，因为用户控制了系统最重要和最关键的方面。其中一些工具允许非超级用户执行由超级用户定义的任务子集。我不覆盖系统管理工具，因为它们因运行它们的 UNIX 变体而异，并且主要由系统管理员使用。我将覆盖系统管理员使用的许多文件以及一些更常用的无侵入性命令。以下的一些章节也出现在其他章节中。

### 使用 ps 检查进程

![](img/75f39fc91296b889c0653851accdfd46_779_0.png)

  要回答“我的系统在做什么？”这个问题，请使用 **ps -ef**。该命令提供有关系统上每个运行进程的信息。例如，如果你想知道 NFS 是否正在运行，只需输入 **ps -ef** 并查找 NFS 守护进程。虽然 **ps** 告诉你系统上正在运行的每个进程，但它并不能提供系统资源消耗水平的好摘要。我猜想 **ps** 是最常发出的系统管理命令。你可以使用许多选项与 **ps** 配合使用。我通常使用 **e** 和 **f**，它们提供关于每个（"e"）运行进程的信息，并以完整列表（"f"）形式列出这些信息。**ps** 的输出在系统之间几乎相同。以下三个例子分别来自 Solaris、AIX 和 HP-UX 系统：

Solaris 示例：

```
martyp $ ps -ef
      UID   PID  PPID  C     STIME TTY          TIME CMD
      root     0     0   0     Feb 18 ?           0:00 sched
      root     1     0   0     Feb 18 ?           1:30 /etc/init -
      root     2     0   0     Feb 18 ?           0:02 pageout
      root     3     0   1     Feb 18 ?           61:34 fssflush
      root  3065 3059  0 Feb 22 ?           5:10 /usr/dt/bin/sdtperformer -f -H -r
      root    88     1   0     Feb 18 ?           0:01 /usr/sbin/in.routed -q
      root   478     1   0     Feb 18 ?           0:00 /usr/lib/saf/sac -t 300
      root    94     1   0     Feb 18 ?           2:50 /usr/sbin/rcpid
      root   150     1   0     Feb 18 ?           6:03 /usr/sbin/syslogd
      root    96     1   0     Feb 18 ?           0:00 /usr/sbin/keyserv
      root   144     1   0     Feb 18 ?          50:37 /usr/lib/autofs/automountd
      root  1010    10   0     Apr 12 ?           0:00 /opt/bin/bin/ama daemon
      root   106     1   0     Feb 18 ?           0:02 /usr/lib/netsvc/yp/ypbind -broad
      root   156     1   0     Feb 18 ?           0:03 /usr/sbin/cron
      root   176     1   0     Feb 18 ?           0:00 /usr/lib/lpsched
      root   129     1   0     Feb 18 ?           0:00 /usr/lib/nfs/lockd
daemon   130     1   0     Feb 18 ?           0:01 /usr/sbin/nfs/lockd
      root 14798     1   0    Mar 09 ?          31:10 /usr/sbin/nscd
      root   133     1   0     Feb 18 ?           0:10 /usr/sbin/inetd -s
      root   197     1   0     Feb 18 ?           0:00 /usr/sbin/power/powerd
      root   196     1   0     Feb 18 ?           0:35 /etc/opt/ licenses/Imgrd.ste -c /d
      root   213     1   0     Feb 18 ?         4903:09 /usr/sbin/vold
      root   199   196   0     Feb 18 ?           0:03 suntecdh -T 4 -c /etc/opt/d
      root   219     1   0     Feb 18 ?           0:08 /usr/lib/sendmail -bd -q15m
      root   209     1   0     Feb 18 ?           0:05 /usr/lib/lp/ldap
      root   293   266   0     Feb 22 ?          48:08 /usr/openwin/bin/Xsun :0 -nobanner
      root 16795 16763  1   07:51:34 pts/4      0:00 ps -ef
      root  2963  2954  0     Feb 22 ?           0:17 /usr/openwin/bin/fbconsole
      root    79     1   0     Feb 18 ?           0:00 /usr/lib/saf/lttymon -g -h -p sunc
      root 10976     1   0    Jun 01 ?           0:00 /opt/perf/bin/ttd
      root  1468     1   0     Feb 24 ?           0:13 /opt/perf/bin/pvalarmd
      root   266     1   0     Feb 18 ?           0:01 /usr/dt/bin/dtlogin -daemon
martyp  1673 16761  1   07:46:46 pts/4      0:01 -ksh
      root 10995     1   0    Jun 01 ?           0:01 /opt/perf/bin/perflbd
      root   484   478   0     Feb 18 ?           0:00 /usr/bin/saf/ttymon
      root   458     1   0     Feb 18 ?          20:06 /usr/ib/snm/snmqxd -y -c /etc/f
      root  4791 3059  0   07:50:37 ?           0:00 /usr/dt/bin/dtscreen -mode blank
      root   471     1   0     Feb 18 ?           0:07 /usr/dt/dmi/dmispd
      root   474     1   0     Feb 18 ?           0:00 /usr/dt/dmi/snmpXdmid -s
      root   485   458   0     Feb 18 ?         739:44 mibiisa -r -P 32874
      root  2954  2936  0     Feb 22 ?           0:01 /bin/ksh /usr/dt/bin/Xsession
      root   236   266   0     Feb 22 ?           0:00 /usr/dt/bin/dtlogin -Xdaemon
      root  3061  3059  0     Feb 22 ?           1:32 dtwm
      root  3058     1   0  Feb 22 pts/2       0:01 /usr/dt/bin/dt/tsssession
      root   712   133   0     Feb 18 ?           0:01 rpc.ttdbserverd
      root 11001 11000  0     Feb 22 ?           0:01 <defunct>
      root  2938     1   0     Feb 22 ?           0:00 /usr/openwin/bin/fbconsole -d :0
      root  2999  2954  0     Feb 22 pts/2      0:16 /usr/dt/bin/sdt_shell -c
      root  3059 3002  0     Feb 22 pts/2       283:35 /usr/dt/bin/dt.dsession
      root  3063 3059  0     Feb 22 ?           0:03 /usr/dt/bin/dthelpview -help/olur
      root  3099  3062  0     Feb 22 ?           0:13 /usr/dt/bin/dtfile -geometry +700
      root 11000 10995  0    Jun 01 ?           0:02 /opt/perf/bin/agdbserver -t alar
      root  3002  2999  0     Feb 22 pts/2      0:01 -ksh -c                 unset DT;
      root   730   133   0     Feb 18 ?           1:37 rpc.statd
      root  3062  3059  0     Feb 22 ?           2:17 /usr/dt/bin/dtfile -geometry +700
      root  3067     1   0     Feb 22 ?           0:00 /usr/dt/usr/dt/bin/sdtvolcheckm
```

