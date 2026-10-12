
图 6.6：`uptime` 的输出示例

`/proc/loadavg` 文件包含了之前三列描述的系统信息，用斜杠（`/`）分隔，显示有多少进程正在访问 `CPU`，最后一列表示进程 `id`。

```
[root@server ~]# cat /proc/loadavg
0.04 0.09 0.05 2/640 21736
```

`top` 命令提供关于系统的实时信息。在第 5 章《文件、目录和进程》中引入了该命令以列出系统中运行的进程。如图 6.8 所示：

```
top - 13:33:43 up 74 days, 6:49, 2 users, load average: 0.08, 0.05, 0.05
Tasks: 466, 2 running, 463 sleeping, 1 stopped, 0 zombie
%CPU: 0,0 us,  0,3 sy,  0,0 ni,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
Mem: 257658.4, 23417.0 free, 184388.5 used, 49763.3 buff/cache
Swap: 0.0 total, 0.0 free, 0.0 used, 67273.6 avail
```

图 6.8：`top` 命令头部示例

`top` 命令的前三行信息如下：

- `Uptime`、登录用户数以及系统平均负载。与 `uptime` 命令输出相同。
- 运行进程列表，指示有多少进程正在使用 `CPU`，多少处于睡眠、停止或僵尸状态（意味着不接受中断，通常需要重启系统来恢复）。
- 系统所有 `CPU` 的使用百分比，具体如下：
  - `us` (`user`)：无 `nice` 值的进程运行时间。
  - `sy` (`system`)：内核进程运行时间。
  - `ni` (`nice`)：带 `nice` 值的进程运行时间。
  - `id` (`idle`)：空闲时间。
  - `wa` (`input/output`)：等待输入输出完成的时间。

`top` 有不同的可视化选项（按 `h` 键获取选项）；按 `i` 键显示每个 `CPU` 的信息，按 `l` 键显示每个 `CPU` 插槽（`NUMA` 节点）。图 6.9 和 6.10 显示了示例：

显示键 1（截断输出）：

```
top - 13:45:20 74 days, 7:00, 2 users, load average: 0.00, 0.03, 0.04
Tasks: 467 total,    1 running, 465 sleeping,    1 stopped, 0 zombie
%Cpu0:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu1:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu2:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu3:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu4:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu5:  0,3 us,  0,3 sy,  0,0 ni,99,3 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu6:  0,3 us,  0,0 sy,  0,0 ni,99,7 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu7:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu8:  0,0 us,  0,0 sy,  0,0 ni,100,0 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Cpu9:  0,0 us,  0,0 sy,  0,0 ni,99,7 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
```

图 6.9：`top` 命令头部示例

显示键 2：

```
top - 13:45:45 74 days, 7:01, 2 users, load average: 0,00, 0,02, 0,04
Tasks: 467 total,    1 running, 465 sleeping,    1 stopped, 0 zombie
%Cpu(s): 0,0 us,  0,2 sy,  0,0 ni,99,8 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Node0:  0,0 us,  0,0 sy,  0,0 ni,99,9 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
%Node1:  0,0 us,  0,5 sy,  0,0 ni,99,5 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
```

图 6.10：`top` 命令头部示例

## 命令 `atop` `htop`

这些命令是传统 `top` 的现代替代方案。图 6.11 显示了 `atop` 应用的界面，它包含了更多与系统的信息：

```
ATOP  server             2022/08/13 13:55:33               10s elapsed
PRC sys   user  1.10s #proc 473  #zombie 0  no procacat
CPU sys   7%      1    iq       0  idle 319% wait       0%
CPL avl   0.06    0%    avgl     0.00  cvw 9950 slab 7.86 nummode 2
MEM in 251.36    22.26M swac 1.00  umM vlim 125.86
SWP top   0.00    free 0.0M swac 0.0M  umcm 306.13 womkill 0
PAG numamig 0  migrate 543  swin       0  swout 0
DSK sda      tci 5    read 0  defi 0  write 7 avio 0.14 ms
NET transport  ipl 29  ipo       ipfrw 0  udpgo 0 deliv 6
NET network   0%    pki 72  pcko 0  si 4 Kbps so 1 Kbps
NET eth2       0%    pki 68  pcko 0  si 3 Kbps so 0 Kbps
PID SYSCU USCPU R0.06s VGROW RGROW RDOSK WROSK CMD 1/4
247 0.99s 0.00s R0.06s 0B 0B 0B 0B 0B 10% ksmd
83078 0.02s 0.10s 0.00s 0B 0B 0B 0B 0B 1% qemu-kvm
2120339 0.00s 0.01s 0.00s 0B 0B 0B 0B 0B 0% atop
36944 0.00s 0.00s 0.00s 0B 0B 0B 0B 0B 0% vbmcd
1531 0.00s 0.00s 0.00s 0B 0B 0B 0B 0B 0% NetworkManager
248 0.01s 0.00s 0.00s 0B 0B 0B 0B 0B 0% Khugepage
83098 0.01s 0.00s 0.00s 0B 0B 0B 0B 0B 0% vnhst-83078
91418 0.01s 0.00s 0.00s 0B 0B 0B 0B 0B 0% kvm-pit/91396
281928 0.01s 0.00s 0.00s 0B 0B 0B 0B 0B 0% kvm-pit/218867
2115603 0.01s 0.00s 0.00s 0B 0B 0B 0B 0B 0% kworker/0:2-ev
```

> 图 6.11：`atop` 命令示例界面

图 6.12 显示了 `htop` 应用的界面，它提供了 `CPU` 使用率的概览：

### `mpstat`

该命令是 `sysstat` 软件包的一部分，需要安装后才能使用。该应用报告与处理器相关的统计数据。图中显示了不带任何选项或参数的示例输出：
