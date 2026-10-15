

每个进程以及线程运行的 CPU（在 PSR 下显示），在本例中为 CPU 0。请注意，sched 只有一个线程，而处理所有 ZFS 请求的 zpool-rp 进程在我们的系统上运行着 141 个内核可见线程，如 `ps -eL | grep "zpool" | wc -l` 命令的输出所示。`ps -eL | wc -l` 命令的输出显示系统当前运行着 416 个 LWPs。会话中的最后一个命令展示了如何使用 -o 选项显示系统上运行的所有进程的各种属性。

```
$ ps -t pts/2
  PID TTY      TIME CMD
  9624 pts/2    0:00 bash
```

```
$ ps -eL
  PID   LWP PSR TTY          LTIME CMD
    0     1   0 ?           0:01 sched
    5     1   0 ?           0:00 zpool-rp
    5     2   0 ?           0:00 zpool-rp
    5     3   0 ?           0:00 zpool-rp
    5     4   0 ?           0:00 zpool-rp
    5     5   0 ?           0:00 zpool-rp
  ...
 14079   1   0 ?           0:00 sshd
 14069   1   0 pts/3       0:00 man
 14076   1   0 pts/3       0:00 less
 14105   1   0 pts/5       0:00 ps
```

```
$ ps -eL | grep "zpool" | wc -l
  141
```

```
$ ps -eL | wc -l
  416
```

```
$ ps -e -o user,uid,pid,ppid,pri,nice,vsz,rss,nlwp,args
  USER     UID   PID  PPID PRI NI   VSZ   RSS NLWP COMMAND
  root       0     0     0  96  SY     0     0    1 sched
  root       0     5     0  99  SD     0     0  141 zpool-rpool
  root       0     6     0  99  SD     0     0    1 kmem_task
  root       0     1     0  59 20  3084 1964    1 /usr/sbin/init
  root       0     2     0  98  SY     0     0    2 pageout
  root       0     3     0  60  SY     0     0    1 fsflush
  root       0     7     0  60  SY     0     0    1 intrd
  root       0     8     0  60  SY     0     0    5 vmtasks
  root       0     9     0  99  SD     0     0    1 postwaitq
  ...
  sarwar  1007  9624  9621  49 20 10188 2300    1 -bash
  root       0  9620   516  59 20 16660 3892    1 /usr/lib/ssh/sshd
  sarwar  1007  9523  9522  59 20 19548 5420    1 /usr/lib/ssh/sshd
  sarwar  1007  9838  9624  59 20  9460 1556    1 ps -e -o
$
```

在第 10.2 节中我们简要讨论了 UNIX SV 中调度的工作方式。这里，我们讨论 PC-BSD 和 Solaris 中调度的工作方式。在 PC-BSD（即 FreeBSD）中，线程的优先级值范围在 0 到 255 之间。阈值优先级设置为 120。系统中用户进程的优先级每四个时钟滴答（通常为 40 毫秒）使用以下公式计算一次：

priority value = threshold priority + nice value + ( recent CPU usage/2 ).

优先级值小于阈值优先级时设为 120。此计算导致进程的优先级基于最近的 CPU 使用率线性下降。每秒对每个进程的最近 CPU 使用率应用一次数字衰减滤波器（即衰减函数）。

与旧版本的 ps 和 top 命令在报告优先级时先减去 84 不同，新版本的这些命令报告线程的优先级值，就像它们存储在与之关联的内核数据结构中一样。表 10.5 显示了分配给不同类别进程/线程的优先级类。优先级值越高表示优先级越低。ITHD 类用于处理中断的线程。

下半部分内核线程和实时用户线程的优先级是固定的，不会改变。内核线程的优先级分配方式旨在造成最小延迟并防止无限阻塞。此外，下半部分（中断）线程可能不会被中断（抢占）。因此，在这些优先级类下执行的线程的执行可能不会被交错。然而，根据其最近的 CPU 使用率，用户线程的优先级可能会随时间变化（增加或减少），方式与第 10.2 节中所述类似。这意味着用户级线程可能会在与不同优先级相关联的队列之间上下移动。因此，我们说 UNIX 使用多级反馈队列调度。最高优先级队列中的多个线程按 FCFS 基础调度。

Solaris 中的 CPU 调度工作方式相当不同，并且有多个调度器同时运行。全局而言，有 170 个优先级值；0 为最低，169 为最高。优先级值越高表示优先级越高。与 FreeBSD 和大多数其他 UNIX 系统不同，每个线程，包括内核线程，都可以被抢占，并且更高优先级的线程可以抢占更低优先级的线程。这允许高优先级实时线程

## 表 10.5 FreeBSD 中各种类别进程/线程的优先级范围和优先级类分配

| Process/Thread Category | Priority Range | Priority Class |
|---|---|---|
| Lower-half kernel (interrupt) | 0–47 | ITHD |
| Real-time user | 48–79 | REALTIME |
| Top-half kernel | 80–119 | KERN |
| Time-sharing user | 120–223 | TIMESHARE |
| Idle user | 224–255 | IDLE |

