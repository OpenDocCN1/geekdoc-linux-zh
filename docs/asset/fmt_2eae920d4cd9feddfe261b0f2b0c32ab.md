
| user11 11561 1159 0 17:49:40 pts/0 | | 0:00 in.telnet |
| root 13362 240 0 Apr 17? | | 0:00 ps |
| root 11/75 11691 1 17:51:28 ? | | 0:00 popper -d -s -T 300 |
| user11 110444 240 0 17:44:16 ? | | 0:32 /usr/lib/sendmail -bd -ql |
| root 28470 4229 0 15:46:58 ? | | 0:00 in.telnet |
| root 6094 240 0 Apr 17? | | 0:00 csh |
| user12 13545 240 0 17:49:31 ? | | 0:00 popper -d -s -T 300 |
| user1 13684 13362 0 Apr 17 pts/2 | | 0:00 csh |
| root 8375 1 0 17:18:07 ? | | 0:00 /usr/lib/sendmail -bd -ql |
| root 9780 1 0 17:31:06 ? | | 0:00 /usr/lib/sendmail -bd -ql |
| root 25171 1 13 Apr 18? | | 624:07 rpc.nisd |
| root 11/71 1 1 17:51:27 ? | | 0:00 /usr/lib/sendmail -bd -ql |
| user13 11722 240 1 17:51:05 ? | | 0:00 popper -d -s -T 300 |

# 第1章 Unix 系统设计

为了支持这些长事务，你首先需要一个强大的 CPU。长事务意味着进程倾向于在系统中堆积，特别是在峰值期间。你的主机必须能够继续服务当前的事务，并为新到达的事务留出空间。这意味着你应该尝试获取一台具有冗余功率的机器。

你还需要大量的磁盘空间，特别是大量的交换空间（见后关于虚拟内存的章节）。

另一个示例，列表 15 提供了运行 Oracle 数据库管理系统（DBMS）的数据库服务器的真实使用状况。

## 列表 1-5：数据库服务器上 `ps-ef` 命令的输出

| UID | PID | PPID | STIME | TTY | CMD |
| :--- | :--- | :--- | :--- | :--- | :--- |
| root | 0 | 0 | Apr 14 | ? | 0:05 sched |
| root | 1 | 0 | Apr 14 | ? | 0:00 /etc/init - |
| root | 2 | 0 | Apr 14 | ? | 0:00 paupeut |
| root | 3 | 0 | Apr 14 | ? | 29:22 fsflush |
| root | 161 | 1 | 0 | Apr 14 | ? | 0:00 /usr/lib/libpsced |
| root | 226 | 1 | 0 | Apr 14 | ? | 0:00 /usr/lib/saf/sac -t 300 |
| root | 107 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/rppcbind |
| root | 107 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/rppcbind |
| root | 115 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/kerbd |
| root | 124 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/inetd -s |
| root | 109 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/keyserv |
| root | 168 | 161 | 0 | Apr 14 | ? | 0:00 ipNet |
| root | 135 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/syslogd |
| root | 151 | 1 | 0 | Apr 14 | ? | 0:06 /usr/sbin/nscd |
| root | 160 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/cron |
| root | 175 | 1 | 0 | Apr 14 | ? | 0:00 /usr/sbin/vold |
| root | 184 | 1 | 0 | Apr 14 | ? | 0:22 /opt/oracle/orahome/bin/orrasv |
| root | 182 | 1 | 0 | Apr 14 | ? | 0:00 /usr/lib/utmpd |
| root | 233 | 226 | 0 | Apr 14 | ? | 0:00 /usr/lib/saf/ttmon |
| oracle | 249 | 1 | 0 | Apr 14 | ? | 0:53 ora_1gwr_sid |
| oracle | 247 | 1 | 0 | Apr 14 | ? | 0:00 ora_pmon_SID |
| oracle | 248 | 1 | 0 | Apr 14 | ? | 17:35 ora_dbwer_SID |
| oracle | 250 | 1 | 0 | Apr 14 | ? | 0:02 ora_smon_SID |
| oracle | 251 | 1 | 0 | Apr 14 | ? | 0:00 ora_reco_SID |
| oracle | 252 | 1 | 0 | Apr 14 | ? | 0:00 ora_s000_SID |
| oracle | 253 | 1 | 0 | Apr 14 | ? | 0:00 ora_d000_SID |
| oracle | 4684 | 175 | 0 | Apr 14 | ? | 72:34 oracleSID:1,2048,6 |
| root | 6900 | 124 | 0 | Apr 14 | ? | 17:44:18 0:00inetd |
| yves | 6902 | 1 | 17:44:18 0:00 -csh |
| root | 6906 | 1 | 17:44:28 0:00 -ef |
|  |  |  |  |  |  |

在列表 1-5 中，特别注意 `ps` 输出的 `TIME` 列。它列出了进程所使用的累计 CPU 时间。每当你看到 `flush` 词时，表示数据库服务器以及其他程序从内存中释放了大量的系统资源。

## 虚拟内存

偶尔，Unix 所需的内存将超过物理安装的内存。这种情况发生时，Unix 通过将进程映像保存到磁盘上称为交换设备的特殊区域来释放内存。这种技术允许系统以某种下降的方式运行。配置系统的交换空间是一个重要的考虑因素。你可能会在按需分页的情况下，地址空间的部分根据需要读入主内存。交换程序决定哪些进程可以换入或换出，并执行所有必要的操作。然而，分页允许进程不再完全位于内存中。

## 信号

Unix 信号是内核或其他进程通知事件已发生并指示其采取某些行动的一种。导致进程接收信号的典型事件包括硬件中断（如键盘输入或串口）；错误条件；超时；硬件故障以及子进程退出等。某些信号类型会被执行进程捕获，调用定义的信号处理器而不是执行默认操作。其他信号无法被忽略或捕获，由默认程序处理——这通常会导致进程中止。根据 Unix 的实现，存在 30 到 40 个不同的信号。表 1-1 描述了其中大多数信号。

## 表 1-1 Unix 信号

| 信号名称 | 信号编号 | 默认操作 | 描述 |
| :--- | :--- | :--- | :--- |
| SIGHUP | 1 | 退出 | 挂断信号 |
| SIGINT | 2 | 退出 | 中断信号（也称为 rubout） |
| SIGQUIT | 3 | 核心储 | 退出信号 |
| SIGILL | 4 | 核心储 | 非法指令 |
| SIGTRAP | 5 | 核心储 | 跟踪/断点陷阱 |
| SIGABRT | 6 | 核心储 | 中止 |
| SIGFPE | 8 | 核心储 | 浮点异常 |
| SIGKILL | 9 | 退出 | 杀死（无法捕获或忽略） |
| SIGBUS | 10 | 核心储 | 总错误 |
| SIGSEGV | 11 | 核心储 | 段错误 |
| SIGSYS | 12 | 核心储 | 系统调用参数错误 |
| SIGPIPE | 13 | 退出 | 管道破 |
| SIGALRM | 14 | 退出 | 闹钟 |
| SIGTERM | 15 | 退出 | 软件终止 |
| SIGUSR1 | 16 | 退出 | 用户信号 1 |
| SIGUSR2 | 17 | 退出 | 用户信号 2 |
| SIGCHLD | 18 | 忽略 | 子进程状态改变 |
| SIGPWR | 19 | 忽略 | 断电/重启 |
