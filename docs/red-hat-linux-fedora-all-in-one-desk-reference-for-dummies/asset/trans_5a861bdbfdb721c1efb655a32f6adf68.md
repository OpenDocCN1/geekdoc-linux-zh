

| Configuration File | Description |
|---|---|
| /etc/inittab | init 进程使用的配置文件，用于启动所有其他进程 |
| /etc/issue | 文件包含在显示文本模式登录提示之前打印的消息（通常是 Red Hat Linux 版本号） |
| /etc/lilo.conf | Linux Loader（LILO）的配置——可从磁盘加载操作系统的引导加载程序之一 |
| /etc/login.defs | 创建用户账户的默认信息，由 useradd 命令使用 |
| /etc/modules.conf | 包含加载内核模块指令的配置文件（例如以太网和声音驱动程序） |
| /etc/mtab | 关于当前已挂载文件系统的信息 |
| /etc/passwd | 关于所有用户账户的信息（实际密码存储在 /etc/shadow 中） |
| /etc/profile | BASH shell 的系统范围环境和启动文件 |
| /etc/rc.d | 存放 Red Hat Linux 系统启动和关闭脚本的目录 |
| /etc/rc.d/rc.sysinit | Red Hat Linux 初始化脚本 |
| /etc/shadow | 包含所有用户账户加密密码的安全文件 [只能由 root 读取] |
| /etc/shells | 系统上用户可用的所有 shell 的列表 |
| /etc/skel | 存放诸如 .bash_profile 等文件初始版本的目录，这些文件会被复制到新用户的主目录 |
| /etc/sysconfig | Red Hat Linux 配置文件 |
| /etc/termcap | 终端功能和选项数据库 |
| /etc/xinetd.conf | 按需启动多个 Internet 服务的 xinetd 守护进程的配置 |
| /var/log/cron | 运行计划任务的 cron 进程的消息日志文件 |
| /var/log/httpd/access_log | Web 服务器访问日志 |
| /var/log/httpd/error_log | Web 服务器错误日志 |
| /var/log/messages | 系统日志 |

## Monitoring System Performance

监控系统性能

When you're the system administrator, you must keep an eye on how well your Red Hat Linux system is performing. You can monitor the overall performance of your system by looking at information such as

作为系统管理员，您必须密切关注 Red Hat Linux 系统的运行状况。您可以通过查看以下信息来监控系统的整体性能，例如

- Central Processing Unit (CPU) usage
- Physical memory usage
- Virtual memory (swap space) usage
- Hard-drive usage

- 中央处理器（CPU）使用情况
- 物理内存使用情况
- 虚拟内存（交换空间）使用情况
- 硬盘使用情况

Red Hat Linux comes with a number of utilities you can use to monitor one or more of these performance parameters. Here I introduce a few of these utilities and show you how to understand the information presented by these utilities.

Red Hat Linux 附带了许多可用于监控一个或多个这些性能参数的实用程序。在这里我介绍其中几个实用程序，并向您展示如何理解这些实用程序提供的信息。

### Using the top utility

使用 top 实用程序

To view the top CPU processes — the ones that are using most of the CPU time — you can use the text mode top utility. To start that utility, type top in a terminal window (or text console). The top utility then displays a text screen listing the current processes, arranged in the order of CPU usage, along with various other information, such as memory and swap space usage. Figure 1-2 shows a typical output from the top utility.

要查看占用 CPU 时间最多的 top CPU 进程，您可以使用文本模式 top 实用程序。要启动该实用程序，在终端窗口（或文本控制台）中输入 top。top 实用程序随后会显示一个文本屏幕，列出当前进程，按 CPU 使用情况排序，并附带其他各种信息，例如内存和交换空间使用情况。图 1-2 显示了 top 实用程序的典型输出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_439_0.png)

The top utility updates the display every 5 seconds. If you keep top running in a window, you can continually monitor the status of your Red Hat Linux system. To quit top, press Ctrl+C or close the terminal window.

top 实用程序每 5 秒更新一次显示。如果您在窗口中保持 top 运行，可以持续监控 Red Hat Linux 系统的状态。要退出 top，请按 Ctrl+C 或关闭终端窗口。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_439_1.png)

Figure 1-2
You can see the top CPU processes by using the top utility.

图 1-2
您可以使用 top 实用程序查看 top CPU 进程。

The first six lines of the output screen (refer to Figure 1-2) provide summary information about the system. Here is what these six lines show:

输出屏幕的前六行（参见图 1-2）提供了有关系统的摘要信息。以下是这六行显示的内容：

- The first line shows the current time, how long the system has been up, how many users are logged in, and three load averages — the average number of processes ready to run during the last 1, 5, and 15 minutes.
- 第一行显示当前时间、系统已运行的时间、已登录的用户数以及三个负载平均值——过去 1、5 和 15 分钟内准备运行的进程的平均数量。
- The second line lists the total number of processes and the status of these processes.
- 第二行列出进程总数以及这些进程的状态。
- The third line shows CPU usage — what percentage of CPU time is used by user processes, what percentage by system (kernel) processes, and during what percentage of time the CPU is idle.
- 第三行显示 CPU 使用情况——用户进程使用多少百分比的 CPU 时间，系统（内核）进程使用多少百分比，以及 CPU 空闲的百分比。
- The fourth and fifth lines show how the physical memory is being used — the total amount, how much is used, how much is free, how much is shared, and how much is allocated to buffers (for reading from disk, for example).
- 第四行和第五行显示物理内存的使用情况——总量、使用量、空闲量、共享量以及分配给缓冲区（例如从磁盘读取）的量。
- The sixth line shows how the virtual memory (or swap space) is being used — the total amount of swap space, how much is used, how much is free, and how much is being cached.
- 第六行显示虚拟内存（或交换空间）的使用情况——交换空间总量、使用量、空闲量以及被缓存的量。

The table that appears below the summary information (refer to Figure 1-2) lists information about the current processes, arranged in decreasing order by amount of CPU time used. Table 1-4 summarizes the meanings of the column headings in the table that top displays.

出现在摘要信息下方（参见图 1-2）的表格列出了有关当前进程的信息，按使用的 CPU 时间量递减顺序排列。表 1-4 总结了 top 显示的表格中列标题的含义。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_440_0.png)

If the RSS field is drastically smaller than the SIZE field for a process, the process is using too little physical memory compared to what it needs. The result is a lot of swapping as the process runs. You can use the vmstat utility (which I discuss later in this section) to find out how much your system is swapping.

如果进程的 RSS 字段远小于 SIZE 字段，则该进程使用的物理内存相对于其需求来说太少。其结果是进程运行时会进行大量交换。您可以使用 vmstat 实用程序（我在本节后面讨论）来了解系统的交换量。

Table 1-4 Meanings of Column Headings in top Utility's Output

表 1-4 top 实用程序输出中列标题的含义

| Heading | Meaning |
|---|---|
| PID | 进程的进程 ID |
| USER | 进程正在运行的用户名 |
| PRI | 进程的优先级 |
| NI | 进程的 Nice 值——值范围从 -20（最高优先级）到 19（最低优先级），默认值为 0 |
| SIZE | 进程的总大小，以千字节为单位 |
| RSS | 任务使用的总物理内存（通常以千字节显示，但 M 后缀表示兆字节） |

Table 1-4 (continued)

表 1-4（续）

| Heading | Meaning |
|---|---|
| SHARE | 进程使用的共享内存量 |
| STAT | 进程的状态（S 表示睡眠，D 表示不可中断睡眠，R 表示运行，Z 表示僵尸——本应死亡但仍在运行的进程——或 T 表示停止；尾随的 < 表示进程具有负 Nice 值） |
| %CPU | 自上次屏幕更新以来使用的 CPU 时间百分比 |
| %MEM | 进程使用的物理内存百分比 |
| TIME | 进程启动以来使用的总 CPU 时间 |
| CPU | 进程正在运行的处理器（如果系统只有一个处理器，则该字段始终为零） |
| COMMAND | 启动进程的命令的简短形式 |

### Using the GNOME system monitor

使用 GNOME 系统监视器

Like the text mode top utility, the GNOME System Monitor tool also enables you to view the system load in terms of the number of processes that are currently running, their memory usage, and the free disk space on your system. To run the tool, select Main Menu→System Tools→System Monitor. The tool starts and displays its output in a window, as shown in Figure 1-3.

与文本模式 top 实用程序类似，GNOME 系统监视器工具也允许您以当前正在运行的进程数量、其内存使用情况以及系统上的可用磁盘空间来查看系统负载。要运行该工具，请选择 主菜单→系统工具→系统监视器。工具启动并在窗口中显示其输出，如图 1-3 所示。

The output is similar to the output you see when you type top in a text-mode console or a terminal window, except that with the System Monitor, you can decide which columns you want to see. Figure 1-3 shows the default view (the Process Listing tab) with the process name, user who is running the process, memory used, percentage of CPU time, and the process ID. The GNOME System Monitor keeps updating the display to reflect the current state of the system.

输出与在文本模式控制台或终端窗口中输入 top 时看到的输出类似，只是使用系统监视器时，您可以决定要查看哪些列。图 1-3 显示了默认视图（进程列表选项卡），其中包含进程名称、运行进程的用户、使用的内存、CPU 时间百分比和进程 ID。GNOME 系统监视器会不断更新显示以反映系统的当前状态。

The GNOME System Monitor window has another tab labeled System Monitor. Click that tab to view a summary of CPU, memory, and disk usage. Figure 1-4 shows a typical view of the System Monitor tab.

GNOME 系统监视器窗口还有另一个标签页，标记为系统监视器。单击该标签页可查看 CPU、内存和磁盘使用情况的摘要。图 1-4 显示了系统监视器标签页的典型视图。

The upper plot in Figure 1-4 shows the percentage of CPU usage with time. The next plot shows the history of memory use and swap space use. Disk space use is summarized in a table at the bottom.

图 1-4 中的上部图表显示了随时间变化的 CPU 使用百分比。下一个图表显示了内存使用和交换空间使用的历史记录。磁盘空间使用情况在底部的表格中进行了汇总。

### Using the uptime command

使用 uptime 命令

You can use the uptime command to get a summary of the system's state. Just type the command like this:

您可以使用 uptime 命令获取系统状态的摘要。只需像这样输入命令：

```
uptime
```

It displays output similar to the following:

它会显示类似以下内容的输出：

```
15:03:21 up 32 days, 57 min, 3 users, load average: 0.13, 0.23, 0.27
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_442_0.png)

Figure 1-3: Use the GNOME System Monitor to view information about the current processes.

图 1-3：使用 GNOME 系统监视器查看有关当前进程的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_442_1.png)

Figure 1-4: GNOME System Monitor displays summary CPU, memory, and disk usage information.

图 1-4：GNOME 系统监视器显示摘要 CPU、内存和磁盘使用信息。

