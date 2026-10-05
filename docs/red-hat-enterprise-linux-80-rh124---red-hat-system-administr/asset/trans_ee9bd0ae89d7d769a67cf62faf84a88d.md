

# 第 8 章 | 监控和管理 Linux 进程

sleep 1
done

> 注意
监控脚本将一直运行直到终止。它通过执行五十个加法题产生人工 CPU 负载。然后它休睡眠一秒，重置变量并重复。

2.3. 使用 `chmod` 命令配合 `+x` 选项使监控变为可执行。

```
[student@servera~$] chmod +x /home/student/bin/monitor
```

- 3. 在右侧终端中，运行 `top` 实用。将窗口调整得尽可能高。

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

- 4. 在左侧终端中，观察 `lscpu` 命令以确定此虚拟机上的逻辑 CPU 数量。

```
[student@servera~$] lscpu
Architecture: x86_64
CPU op-mode(s): 32-bit, 64-bit
Byte Order: Little Endian
CPU(s): 2
...output已省略...
```

- 5. 在左侧终端中，运行一个监控执行文件的单实例。使用安培符号 `&` 在后台运行该进程。

```
[student@servera~$] monitor &
[1] 6071
```

- 6. 在右侧终端中，观察 `top` 显示。通过按键 `L`、`T` 和 `M` 切换负载、线程和内存表头行。观察此行为后，确保所有表头均已出来。

RH124-RHEL8.0-en-1-20190507

- 7. 注意 `monitor` 的进程 ID (PID)。查看该进程的 CPU 百比，预计该百分比将在 15% 到 20% 之间波动。

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
0671 student 20 0 222448 2964 2716 S 18.7 0.2 00:27:35 monitor
...output已省略...
```

查看负载平均值。当前一分钟负载平均小于 1.0。观察到的值可能受到来自另一个虚拟机或虚拟主机资源竞争的影响。

top - 12:23:45 up 11 days, 1:09, 3 users, load average: 0.21, 0.14, 0.05

- 8. 在左侧终端 shell 中，运行第二个 `monitor` 实例。使用安培符号 `&` 在后台运行该进程。

```
$student@servera ~]$ monitor &
[2] 6498
```

- 9. 在右侧终端 shell 中，注意第二个 `monitor` 进程的进程 ID (PID)。查看该进程的 CPU 百比，预计同样将在 15% 到 20% 之间波动。

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
0671 student 20 0 222448 2964 2716 S 19.0 0.2 01:36:53 monitor
6498 student 20 0 222448 2996 2748 R 15.7 0.2 01:16:34 monitor
...output已省略...
```

查看一分钟负载平均值，它仍然小于 1.0。等待至少一分钟让计算能够适应新的工作负载是重要的。

top - 12:27:45 up 11 days, 1:09, 3 users, load average: 0.21, 0.14, 0.05

- 10. 在左侧终端 shell 中，运行第三个 `monitor` 实例。使用安培符号 `&` 在后台运行该进程。

```
$student@servera ~]$ monitor &
[3] 7112
```

- 11. 在右侧终端 shell，注意第三个 `monitor` 进程的进程 ID (PID)。查看该进程的 CPU 百比，预计同样将在 15% 到 20% 之间波动。

