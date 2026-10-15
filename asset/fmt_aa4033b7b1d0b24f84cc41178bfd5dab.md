
```
top -14:00:36 up 15 days, 2:31 1 user, load average: 1.16, 1.15
Tasks: 95 total, 89 sleeping, 0 stopped, 0 zombie
Cpu(s): 97.0 us, 2.66 sy, 0.0 ni, 0.0 wa, 0.34 hi
Mem: 51472k total, 43456k used, 80192k free, 118432 buff
Swap: 102820k total, 8k used, 102112k free, 8298k cache

PID | VIRT | RES | SHR | S | %CPU | %MEM | TIME | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 7182 | 0 | 2676 | 15144 | F | 0.0 | 0.0 | 00:00:19 | user |
| 16379 | 0 | 8572 | 16M | S | 1.3 | 3.5 | 00:45:69 | ksyuga |
| 16378 | 0 | 8572 | 16M | S | 0.0 | 0.0 | 00:00:24 | ksyuga |
| 13675 | 0 | 2760 | 15M | S | 0.0 | 0.0 | 00:11:70 | ksyuga |
| 16511 | 0 | 2615 | 16M | S | 0.0 | 0.0 | 00:12:22 | kelnit |
| 14127 | 0 | 3320 | 21M | 26S | 0.3 | 0.4 | 00:15:30 | kelnit |
| 17114 | 0 | 1792 | 920 | 1536 | R | 0.3 | 0.2 | 00:00:45 | top |
| 1 | 0 | 0 | 0 | RS | 0.0 | 0.0 | 00:00:04 | trait |
| 2 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:06 | ksfit |
| 3 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:15 | events/ |
| 4 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:00 | kapsid |
| 5 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:00 | blocked |
| 6 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:00 | blocked |
| 7 | 0 | -10 | 0 | S | 0.0 | 0.0 | 00:00:07 | khelper |
| 8 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:23:73 | pdflush |
| 9 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:74 | pdflush |
| 10 | 0 | -10 | 0 | S | 0.0 | 0.0 | 00:00:00 | aio-0/ |
| 1 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:05:16 | kswdd |
| 163 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00:00 | kserod |
```

图 1-4

下半部分显示服务器上运行的进程按 CPU 使用率排序。屏幕每秒更新一次。

你可以按内存（类型 `m`）或用户（类型 `u`）对进程排序，并向进程发送信号（例如挂起或杀死进程）。完成后，按 `q` 退出。![](img/667acce1695f6403deb2b60e994760c8_57_0.png)

尽管 `top` 命令为你提供了系统头部的信息，你可能还想使用 `uptime` 命令显示系统运行时间、用户数以及平均负载。

`ps` 实用工具显示系统上运行的进程按进程 ID 排序。例如，使用 `ps aux` 查看详细信息：

| USER | PID | %CPU | %MEM | VSZ | RSS | TTY | STAT | TIME | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| root | 1 | 0.0 | 0.0 | 588 | 244 | ? | S | Aug20 00:00 | [5] |
| root | 2 | 0.0 | 0.0 | 0 | 0 | ? | SN | Aug20 00:00 | ksoftqd/0] |
| root | 3 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | events/0] |
| root | 4 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | kpcpid] |
| root | 5 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | khelper] |
| root | 6 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | klockd/0] |
| root | 7 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | pdflush] |
| root | 8 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:12 | pdflush] |
| root | 9 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | xseriod] |
| root | 10 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | aio/0] |
| root | 169 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:05 | kswappd/0] |
| root | 530 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | reiserlf/0] |
| root | 707 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | kccpyd/0] |
| root | 769 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | kjournal] |
| root | 1426 | 0.0 | 0.0 | 0 | 0 | ? | S | Aug20 00:00 | khubud] |
| root | 1843 | 0.0 | 0.1 | 1584 | 720 | ? | Ss | Aug20 00:27 | [/sbin/resmgrd] |
| bin | 1846 | 0.0 | 0.1 | 1432 | 624 | ? | Ss | Aug20 00:37 | [portmap] |

`netstat` 命令可以发现哪些端口提供服务以及哪些连接是已建立的，如下所示：

```
geeko@DA50~$ netstat -patune
```

### uname

你可以使用 `uname` 命令来查询当前的内核版本，如下所示：

```
geeko@DA50:~ uname -a
Linux DA50 2.6.5-7.97-default #1 Mon Jul 2 14:21:59 UTC 2007 i686 i686
i386 GNU/Linux
geeko@DA50:~
```

### GUI 桌面实用

以下是你可以从桌面查看硬件信息和 Linux 系统信息的工具：

- KDE System Guard
- Xosview
- SuSEPlugger

#### KDE System Guard

KDE System Guard 是 KDE 桌面任务管理器和性能监控器。通过 KDE System Guard，你可以监控系统负载性能（CPU 负载、平均负载、物理内存、交换内存）或进程。

要访问 KDE System Guard，请从系统菜单选择系统 > 监控器 > KDE System Guard（见图 1-5）。

![](img/667acce1695f6403deb2b60e994760c8_60_0.png)

图 1-5

图 1-7

每个参数的状态都以水平条的形式显示，并分为颜色编码区域。每个区域代表正用于特定用途的资源百分比。当你完成信息查看后，可以通过关闭窗口或输入 `q` 来退出。

#### SuSEPlugger

你可以使用 SuSEPlugger 工具查看 Linux 系统上特定硬件的详细信息，并启动相应的 YaST 模块来配置硬件。要启动 SuSEPlugger，请执行以下操作之一：

- 从你的桌面面板（屏幕底部）选择 **SuSEPlugger** 图标。
- 从终端窗口输入 `suseplugger`。

启动后，SuSEPlugger 工具会打开，如图 1–8 所示。
