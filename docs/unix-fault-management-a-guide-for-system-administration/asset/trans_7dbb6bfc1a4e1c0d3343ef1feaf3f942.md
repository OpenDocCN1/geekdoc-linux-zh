

应用运行的时长，以及当前用户数。还可以获取一些资源与性能信息。

## DMI

通过使用 DMI（桌面管理接口）也可以获取系统资源信息，DMI 是另一种用于存储和访问管理信息的标准。管理信息以 MIF（管理信息框架）中的文本文件形式表示。它被划分为若干组件，每个组件都有一个服务提供商（SP），负责向请求 DMI 信息的管理应用提供这些信息。

包括 HP-UX 在内的多个系统平台都为系统 MIF 和软件 MIF 提供了度量机制。附录 A 包含了这些 MIF 的完整列表。

与 MIB-II 类似，系统 MIF 可用于获取通用的系统信息（例如已运行了多长时间）和系统联系人信息。它包含系统名称、启动时间、联系信息、正常运行时间、用户数，以及一些关于文件系统和磁盘的信息。

软件 MIF 提供有关系统中安装的软件产品和产品捆绑包的信息，在发现应用存在问题后，它可以作为一个有用的工具。通过使用 MIF 浏览器，你可以检查软件 MIF，以查看问题是否可能由坏的补丁或修改过的文件引起。MIF 包含每个产品的版本信息，包括创建时间和修改时间。可以检查版本信息以确定是否存在兼容性问题。最后，提供产品供应商信息，以便你联系产品的支持人员。

惠普（Hewlett-Packard）等厂商正在努力提供企业范围内的软件配置信息库。需要工具来比较不同系统上的应用版本，并将系统更新到相同的修订级别。

## pstat

有时，你可能会希望编写自己的应用程序来获取关于特定进程的信息。该接口被称为 *pstat*。你的程序可以仅为感兴趣的进程生成输出，这比在 *top* 或 *ps* 的输出中翻找重要信息要容易得多。

*列表 7-2* 和 *列表 7-3* 分别展示了一个获取 *pstat* 统计信息的程序以及运行该程序的输出。该程序显示匹配你输入名称的进程的信息。*pstat* 接口还可以显示整体系统信息，如 *列表 7-2* 中所示。

对于 *列表 7-3* 中的示例，关注点是一个名为 *memhog* 的应用使用过多的内存，因此程序被用于在不同时间点检查 *memhog* 的内存使用情况，并跟踪整体系统负载。这比运行 *top* 或 *GlancePlus* 等其他工具并筛选输出更方便。

### 列表 7-2 使用 pstat 的程序代码。

```c
/* pstat example */
#include <stdio.h>
#include <stdlib.h>
#include <sys/time.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <sys/errno.h>
#include <sys/pstat.h>

convert_status (status,stat)
char *status;
long stat;
{
    switch (stat) {
        case 1: strcpy (status,"sleeping");
                break;
        case 2: strcpy (status,"running");
                break;
        case 3: strcpy (status,"stopped");
                break;
        case 4: strcpy (status,"dead (zombie)");
                break;
        case 5: strcpy (status,"other");
                break;
        case 6: strcpy (status,"idle");
                break;
    }
}

main()
{
    struct pst_status pst;
    struct pst_dynamic dyn;
    struct pst_static mystatic;
    struct timeval temp;
    struct timezone dummy;
    char target[80];
    char status[14];
    int index = 0;
    int duration;
    long prm_id;
    unsigned long now;
    gettimeofday(&temp,&dummy);
    printf ("Enter process name:");
    scanf ("%s",target);
    now = temp.tv_sec;
    while ( pstat_getproc(pst,sizeof (struct pst_status),
	1,index) > 0) {
	if (strcmp(target,pst.pst_ucomm)==0) {
	duration = now - pst.pst_start;
	convert_status(status,pst.pst_stat);
	printf ("PID %8d Status: %s\n",pst.pst_pid,status);
	printf ("Started %d seconds ago\n",duration);

	printf ("Real pages(DATA %d TEXT %d STACK %d)\n",
		pst.pst_dsize,pst.pst_tsize,pst.pst_ssize);
	printf ("RSS %d MAX RSS(hwm) %d\n",
		pst.pst_rssize,pst.pst_maxrss);
	printf ("Number of swaps: %d\n",pst.pst_nswap);
	}
	index = pst.pst_idx+1;
} /* end while loop */

printf ("Overall System Info:\n");
pstat_getstatic(mystatic,sizeof(struct pst_static),
	0,0);
pstat_getdynamic(dyn,sizeof(struct pst_dynamic),
	0,index);
printf ("Run queue len(1- %1f,",
	dyn.psd_avg_1_min);
printf ("5- %1f,",
	dyn.psd_avg_5_min);
printf ("15- %1f)\n",
	dyn.psd_avg_15_min);
printf ("Physical Memory: %d\n",mystatic.physical_memory);
printf ("Active Real Memory: %d Free pages: %d bytes\n",
	dyn.psd_arm,dyn.psd_free*mystatic.page_size);
}
```

### 列表 7-3 显示 pstat 信息的程序输出。

```
# ./pstate
Enter process name:memhog
PID	24549 Status: running
Started 247 seconds ago
Real pages(DATA 1955 TEXT 3 STACK 3)
RSS 1979 MAX RSS(hwm) 1979
Number of swaps: 0
Overall System Info:
Run queue len(1- 0.000000,5- 0.000000,15- 0.000000)
Physical Memory: 393216
Active Real Memory: 0 Free pages: 0 bytes
#
```

*列表 7-3* 中的示例仅显示了内存信息，但还可以获取多种其他度量指标。以下是每个进程可用信息的摘要：

- 用户 ID、PID、有效用户 ID、真实和有效组 ID，以及父进程 PID
- 用于数据、文本或堆栈的实际页面数
- 用于共享内存、内存映射文件等的实际页面数
- 用于数据、文本、堆栈、共享内存等的虚拟页面数
- 优先级和 nice 值
- 终端设备 ID
- 进程组号和 PRM 组 ID
- 进程中内存的地址
- 执行过程花费的用户时间和系统时间
- 进程启动时间
- 进程状态和状态标志
- 最后使用进程的处理器的标识
- 进程的命令行和执行文件基本名称
- 使用的 CPU 时间
- 驻留集大小的当前值和高水位标记
- 换页次数、页面错误和页面回收次数
- 接收的信号或套接字消息数量
- 发送的套接字消息数量
- 进程调度策略
- 会话 ID
- 进程根目录、当前目录和执行文件的文件 ID
- 当前打开的最高文件描述符
- 读取和写入的字符数

有关此接口可用的进程和系统度量指标的更多信息，可以在系统包含文件 /usr/include/sys/psstat.h 中找到。

## 故障检测工具

本节描述可用于检测应用故障的产品。本章后面还将讨论用于监控应用性能的其他工具。

## IT/Operations

IT/Operations（IT/O）是一款面向系统操作员的高级管理产品。企业中的系统可以显示在屏幕地图上，颜色代表其当前状态。其中包括应用程序库，可用于启动默认或自定义工具。可以从整个企业的系统中发送事件，并配置相应的恢复操作。

IT/O 还可以用于监控受管系统上的指定组件。提供了一些预定义的监控器，其中一个能够监控特定进程。如果进程失败，事件将被发送到 IT/O 控制台。可以配置恢复操作以重启应用程序。

虽然 IT/O 可以检测应用程序故障并重启应用程序，但它不具备足够的高可用性功能，无法将应用迁移到其他系统或确保只有一个副本在运行。更广泛的高可用性功能由 MC/ServiceGuard 提供，接下来将对其进行讨论。

## MC/ServiceGuard

MC/ServiceGuard 是惠普（Hewlett-Packard）的一款高可用性产品，用于保护您的关键应用程序和服务器。MC/ServiceGuard 最常用于多系统（集群）环境中。每个系统上的 MC/ServiceGuard 软件监控集群中的其他系统。MC/ServiceGuard 可以检测系统、网络和应用故障。例如，MC/ServiceGuard 可以透明地从 LAN 故障中恢复。

在确定需要保护哪些应用程序后，使用 MC/ServiceGuard 命令或可从 SAM 访问的图形界面将它们配置为包。需要定义应用程序的众多属性，例如：

- 应用程序名称
- 用于启动和停止应用程序的脚本
- 组成应用程序的进程或服务
- 应用程序使用的子网
- 应用程序可运行的备用系统
- 额外的资源依赖关系

然后，MC/ServiceGuard 监控这些服务和依赖关系。如果发生故障，该包将在本地重启，或迁移到另一个系统并重启。同样，当发生系统故障时，MC/ServiceGuard 软件可以检测问题并自动在备用节点上重启关键应用程序。

MC/ServiceGuard 软件检测各种错误条件，但没有复杂的机制来通知你发生了什么。错误通常写入系统日志文件，这有助于追溯发生了什么。

由于 MC/ServiceGuard 可以自动将应用程序迁移到其他系统，因此你可能很难了解应用程序的当前状态。MC/ServiceGuard 命令（如 cmviewcl）可以告知集群及其包的当前状态。HP MC/ServiceGuard MIB 也包含此信息。但是，包可能因多种原因被迁移，而 MC/ServiceGuard 不会告知原因。你可能需要检查每个集群系统上的系统日志文件（/var/adm/syslog/syslog.log）以查看其特定的 MC/ServiceGuard 活动。下面是包故障转移期间记录到系统日志文件中的事件示例

