
该系统的负载平均似乎正在下降。

在四个 CPU 上，负载平均为 2.92，意味着所有 CPU 在约 73% 的时间内在使用状态。

在过去的 5 分钟内，系统超载了 12%。

在过去的 15 分钟内，系统超载了 30%。

空闲的 CPU 队列负载数值为 0。每个等待 CPU 的进程都会为负载数值加 1。如果有一个进程在 CPU 上运行，则该资源（CPU）正在使用中，但没有等待的请求。如果一个进程运行了一整一分钟，它对分钟负载平均的贡献将是 1。然而，不可中断地提供关键磁盘或网络资源的进程也包含在计数中并会增加平均值。虽然这并不是 CPU 利用率的指标，但这些进程被添加到队列中，因为它们在获得资源之前无法运行。这是由于资源限制导致的系统负载。在资源饱和接近 100% 之前，负载平均保持在 1 以下，每个额外的请求开始经历等待。

## 真实进程监控

`top` 程序是系统进程的动态视图，显示一个摘要头，随后是一个类似于 `ps` 信息的进程或线程列表。与静态 `ps` 输出不同，`top` 会以可配置的间隔持续刷新，并提供重新排序、排序和高亮功能。用户配置可以保存并持久化。默认输出列可以从其他工具识别出来：

- 进程 (`PID`)。
- 用户名 (`VIRT`)。
- 驻内存 (`RES`) 是物理内存。
- 共享内存 (`SHR`) 是共享内存。
- 虚拟内存 (`VSZ`) 是进程使用的虚拟内存。
- 状态（`S`）是进程状态。
- CPU 时间（`TIME`）是进程自启动的累积时间。
- 命令（`COMMAND`）是进程名。
- 状态（`S`）：
  - `D` = 不中断睡眠
  - `R` = 运行
  - `S` = 睡眠
  - `T` = 停止
  - `Z` = 僵尸

### top 快捷键

| KEY | 目的 |
|---|---|
| `?` | 显示交互式快捷键帮助。 |
| `L` | 修改刷新率（例如 0.5, 1）。 |
| `s` | 显示单个 CPU 的负载。 |
| `B` | 切换反色显示。 |
| `C` | 切换高亮显示。 |
| `U` | 按用户进行过滤。 |
| `M` | 按内存使用排序。 |
| `P` | 按 CPU 使用排序。 |
| `T` | 按时间排序。 |
| `W` | 保存当前显示配置。 |
| `K` | 杀死进程。 |
| `Q` | 退出 `top`。 |
| 注意: | 在安全模式下启动 `top` 时不可用。见 `top(1)`。 |

## 参考文献

`ps(1)`, `top(1)`, `uptime(1)` 和 `w(1)` 手页面

## 引导性练习

### 监控进程活动

在此练习中，你将使用 `top` 命令动态检查并控制进程。

#### 结果

你应该能够实时管理进程。

#### 开始之前

使用 `student` 作为密码登录工作站。

在工作站上，运行 `lab-monitor start` 命令。该命令运行一个定义主机（服务器）在网络上是否可用的脚本。

```
[student@workstation ~]$ lab-monitor start
```

1. 在工作站上打开两个终端。这些终端被称为左和右。在每个终端中，使用 `ssh` 命令以 `student` 用户身份登录服务器。

```
[student@workstation ~]$ ssh student@servera
激活 Web 控制台：systemctl enable --now cockpit.socket
```

```
最后登录：2019年2月8日 周五 12:04:52 来自 172.250.254
$student@servera ~$
```

2. 在左终端中，创建一个新目录 `/home/student/bin`。在新目录创建一个名为 `monitor` 的 shell 脚本。确保脚本具有可执行权限。

2.1. 使用 `mkdir` 命令创建新目录 `/home/student/bin`。

```
[student@servera ~]$ mkdir /home/student/bin
```

2.2. 使用 `vim` 命令在 `/home/student/bin` 目录创建 `monitor` 脚本。按下 `I` 键进入 Vim 交互模式。使用 `:wq` 命令保存文件。

```
[student@servera ~]$ vim /home/student/bin/monitor
!/bin/bash

while true; do

var=1

while [[ var -lt 50000 ]]; do

var=$((var+1))

done

done
```

```
# 第 8 章 | 监控和管理 Linux 进程

sleep 1
done
```

> 注意
监控脚本将一直运行直到终止。它通过执行五十个加法题产生人工 CPU 负载。然后它休睡眠一秒，重置变量并重复。

2.3. 使用 `chmod` 命令配合 `+x` 选项使监控变为可执行。

```
[student@servera~$] chmod +x /home/student/bin/monitor
```

3. 在右侧终端中，运行 `top` 实用。将窗口调整得尽可能高。

```
[student@servera~$] top
top -12:13:03 up 11 days, 58 min, 3 users          load average: 0.00, 0.00, 0.00
tasks: 113 total, 2 running, 111 sleeping, 0 stopped, 0 zombie
CPU(s): 0.2 us, 0.0 sy, 0.0 ni, 99.8 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
Mib Mem: 1829.4 total, 1377.3 free, 193.9 used, 258.2 buff/cache
Mib Swap: 1024.0 total, 1024.0 free, 1476.6 avail Mem
PID PR NI VIRT RES SHR S %CPU %MEM TIME+  COMMAND
5861 root 20 0 0 0 I 0.3 0.0 00:00:01 worker/1-3events
6068 student 20 0 273546 4380 3688 R 0.3 0.2 00:00:01 systemd
1 root 20 0 178680 13424 0 S 0.0 0.7 00:04:03
2 root 20 0 0 0 0 S 0.0 0.0 00:00:03 kthread
3 root 20 0 0 0 0 I 0.0 0.0 00:00:00 rcu_gp
...output已省略...
```

4. 在左侧终端中，观察 `lscpu` 命令以确定此虚拟机上的逻辑 CPU 数量。

```
[student@servera~$] lscpu
Architecture: x86_64
CPU op-mode(s): 32-bit, 64-bit
Byte Order: Little Endian
CPU(s): 2
...output已省略...
```

5. 在左侧终端中，运行一个监控执行文件的单实例。使用安培符号 `&` 在后台运行该进程。

```
[student@servera~$] monitor &
[1] 6071
```

6. 在右侧终端中，观察 `top` 显示。通过按键 `L`、`T` 和 `M` 切换负载、线程和内存表头行。观察此行为后，确保所有表头均已出来。

RH124-RHEL8.0-en-1-20190507

7. 注意 `monitor` 的进程 ID (`PID`)。查看该进程的 CPU 百比，预计该百分比将在 15% 到 20% 之间波动。

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
0671 student 20 0 222448 2964 2716 S 18.7 0.2 00:27:35 monitor
...output已省略...
```

查看负载平均值。当前一分钟负载平均小于 1.0。观察到的值可能受到来自另一个虚拟机或虚拟主机资源竞争的影响。

```
top - 12:23:45 up 11 days, 1:09, 3 users, load average: 0.21, 0.14, 0.05
```

8. 在左侧终端 shell 中，运行第二个 `monitor` 实例。使用安培符号 `&` 在后台运行该进程。

```
$student@servera ~]$ monitor &
[2] 6498
```

9. 在右侧终端 shell 中，注意第二个 `monitor` 进程的进程 ID (`PID`)。查看该进程的 CPU 百比，预计同样将在 15% 到 20% 之间波动。

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
```
