
## 参考资料

- gnuplot：http://www.gnuplot.org/。
- gprof：http://sources.redhat.com/binutils/docs-2.12/gprof.info/index.html。
- Hinton, Glenn, 等人。 “Pentium 4 处理器的微体系结构”， http://www.intel.com/technology/iti/q12001/pdf/art_2.pdf。
- Luo, Yue, 等人。 “在超级可扩展机器上对互联网服务器进行基准测试”，《计算机》， 2003 年 2 月，第 34-40 页。
- Kernprof： http://oss.sgi.com/projects/kernprof。
- netstat： http://www.ussg.iu.edu/usail/man/linux/netstat.8.html。
- nfsstat： http://www.die.net/doc/linux/man/man8/nfsstat.8.html。
- oprofile： http://oprofile.sourceforge.net/doc。
- Performance Inspector： http://www-124.ibm.com/developerworks/opensource/pii/。
- Readprofile： http://nodevice.com/sections/ManIndex/man1303.html。
- sysstat： http://perso.wanadoo.fr/sebastien/godard/。
- strace： http://sourceforge.net/projects/strace。
- Stallings, William.《计算机组织与架构：为性能而设计》，第六版。 Prentice Hall， 2003。
- tcpdump： http://www.die.net/doc/linux/man/man8/tcpdump.8.html。
- top： http://nodevice.com/sections/ManIndex/man1818.html。
- Intel VTune： http://www.intel.com/software/products/vtune/。
- vmstat： http://nakula.rvs.uni-bielefeld.de/cgi-bin/man.sh?man=8+vmstat。
- 网络资源： http://www.ping127001.com/pingpage.htm。
- 网络资源： http://www.ethereal.com/docs/man-pages/tcpdump.8.html。
- 网络资源： http://csrc.nist.gov/tools/tools.htm。
- 网络资源： http://www.ripe.net/ripepcc/pub-services/db/irrtoolset/。
- 网络资源： http://www.insecure.org/tools.html。
- Tanenbaum, Andrew.《计算机网络》，第三版。 Prentice Hall， 1996。

## 第五章. 系统跟踪工具

作者： Ron Cadima, Gerrit Huizenga, Duc J. Vianney 和 Peter Wai Yee Wong

### 简介

当发生性能瓶颈或问题时，系统跟踪工具可以帮助您确定问题的根源。在跟踪系统时，您不仅需要知道使用哪些工具，还需要知道何时何地以及如何使用它们。

通常，系统跟踪涉及多个步骤：在每一步中，您都会更深入地探究问题，最终创建一个解决方案或优化系统或相应应用程序。首先从系统全局角度审视问题，然后专注于特定应用程序或一系列事件，您可以更可靠地确定性能问题的根本原因。例如，仅仅因为系统在启动某个特定应用程序后变慢，并不一定意味着该应用程序是变慢的原因。该应用程序可能只是一个催化剂，暴露了系统中另一个应用程序内部的问题。

开源社区中有许多可用的 Linux 跟踪工具。本章讨论其中一些最常用工具：

- `top`，用于提供正在使用系统及其正在使用的系统资源的过程的整体视图
- `strace`，用于跟踪来自应用程序的所有系统调用
- `Oprofile`，基于系统定时器或性能计数器支持，提供正在运行的系统的性能分析信息，包括系统在应用程序中花费的时间
- `Performance Inspector`，一套用于识别性能问题和特征的工具

本章还讨论了在开始跟踪系统之前需要满足的要求。

请注意，鉴于 Linux 的动态特性，可能会开发新的系统跟踪工具，并且现有工具（包括本章中讨论的工具）将继续更新。

### 系统跟踪的要求

为了获取有用的信息以排查性能问题，在开始跟踪系统之前请遵循以下准则：

- 在分析的相应步骤中使用正确的工具。如果您使用的工具的数据不可靠，因为它是错误的工具，那么您分析错误数据或应用程序的时间就会被浪费。
- 确保正在跟踪的系统有足够的内存和存储空间。例如，如果内存不足，就会发生交换，这可能会扭曲结果。
- 了解您使用的工具的开销。如果工具对系统的侵入性很强，性能分析可能不准确。
- 使用定义好的测试场景进行测量。必须使用一致的一系列步骤进行测量，并且结果必须是可重复的。在分析的每个步骤中，按相同的顺序测量相同的函数。
- 使用受控环境。除非它们是测量场景的一部分，否则不要在测量和跟踪期间允许其他进程或函数运行。在应用了基于测量和跟踪结果的修复措施后，您可以开始新一轮测试，将新的应用程序添加到其中。最好的经验法则是保持场景简单，并知道何时在运行什么。

### top 实用程序

`top` 实用程序随大多数平台和大多数 Linux 发行版一起提供。`top` 实时报告处理器活动，对于获取正在使用系统及它们正在使用的资源的过程的整体视图最为有用。`top` 允许您指定测量之间的延迟和要进行的测量次数。`top` 还允许一种批处理操作模式，将数据写入常规文本格式。`top` 的另一个选项允许您指定仅显示实际正在运行的进程。

`top` 报告进程使用的大致内存量。您可以配置 `top` 以显示进程层次结构。

将 `top` 用作分析的第一步，查看系统中正在运行哪些进程以及它们消耗了多少系统时间。通过在一段时间内运行 `top` 并将输出定向到文件，您可以查看哪些进程在何时运行。您还可以近似地查看进程何时停止、何时消耗大量内存，以及何时有一两个进程开始消耗大量处理器时间。例如，如果 `top` 输出表明某个特定进程消耗了大部分处理时间，您可以使用其他工具来识别应用程序中时间被消耗的位置。内存使用量也是如此。如果突然消耗大量内存或内存消耗逐渐增加，请使用低级跟踪工具来确定内存使用量增加发生的位置。

以下是 `top` 报告的示例。默认情况下，显示每 5 秒更新一次。

```
# top

8:24 am  up 4 days, 19:31,  1 user,  load average: 0.16, 0.06, 0.09
 57 processes:  55 sleeping, 2 running,  0 zombie, 0 stopped
CPU states:  2.1% user,  0.6% system,  4.0% nice,  4.3% idle
  Mem:  252976k av, 21516k used, 41460k free,      0k shrd,  29820k buff
 Swap:  522072k av,  27060k used, 495012k free          76836k cached

  PID USER     PRI   NI SIZE  RSS SHARE STAT %MEM %CPU   TIME COMMAND
 20269 root      16  224  224  188  188  R  98.4  0.0  0:09 pi_watch
 20270 root     10    0 1040 1040  828  R   1.9   0.4  0:00 top
   1 root      9    0  464  428  412  S   0.0   0.1  0:00 init
   2 root      9    0    0    0    0  SW  0.0   0.0  0:00 keventd
   3 root     19   19   0    0    0  SWN 0.0   0.0  0:00 ksoftirqd_CPU0
   4 root      9    0    0    0    0  SW  0.0   0.0  0:09 kswapd
   5 root      9    0    0    0    0  SW  0.0   0.0  0:00 bdflush
   6 root      9    0    0    0    0  SW  0.0   0.0  0:02 updated
   8 root      9    0    0    0    0  SW  0.0   0.0  0:00 khubd
  10 root     -1  -20   0    0    0  SW  0.0   0.0  0:00 mdrecoveryd
  14 root      9    0    0    0    0  SW  0.0   0.0  0:14 kjournald
 127 root      9    0    0    0    0  SW  0.0   0.0  0:00 kjournald
 128 root      9    0    0    0    0  SW  0.0   0.0  0:00 kjournald
 129 root      9    0    0    0    0  SW  0.0   0.0  0:00 kjournald
 428 root      9    0  536  528  456  S   0.0   0.2  0:00 syslogd
 432 root      9    0  428  412  376  S   0.0   0.1  0:00 klogd
 449 rpc      9    0  560  556  484  S   0.0   0.2  0:00 portmap
 468 rpcuser   9    0  660  576  576  S   0.0   0.2  0:00 rpc.statd
 581 root      9    0  972  732  732  S   0.0   0.2  0:00 sshd
 594 root      9    0  716  588  588  S   0.0   0.2  0:00 xinetd
 615 root      9    0 1644 1260 1068  S   0.0   0.4  0:14 sendmail
 624 smmsp     8    0 1176  772  688  S   0.0   0.3  0:00 sendmail
 634 root      9    0  400  368  352  S   0.0   0.1  0:14 gpm
 643 root      9    0  604  564  528  S   0.0   0.2  0:00 crond
 674 xfs      9    0  6136  4  552 1032  S  0.0  1.7  0:06 xfs
```

