
``` 
double elapsed;               /* 进程中所有 lwp 的经过时间 *
double total_user;              /* 当前秒总计 */
double total_system;
double total_child;             /* 已退出的子进程 *
double user_time;               /* 此间隔内的用户时间 \
double system_time;             /* 此间隔内的系统调用时间 \
double trap_time;               /* 此间隔内的系统陷阱时间 \
double child_time;              /* 此间隔内的子进程 CPU \
double text_pf_time;            /* 此间隔内的文本页异常等待 \
double data_pf_time;            /* 此间隔内的数据页异常等待 \
double kernel_pf_time;          /* 此间隔内的内核页异常等待 *

double user_lock_time;         /* 此间隔内的用户锁等待 *
double sleep_time;              /* 所有其他睡眠时间 *
double cpu_wait_time;           /* 在运行队列上等待 CPU 的时间 *
double stopstime;               /* 从 ^Z 停止的时间 *
ulong scyllangs;               /* 此进程的系统调用/次数 *
ulong inblocks;                /* 间隔输入块 - 仅元数据
only - 无意义 *        /* 间隔输出块 - 仅元数据
ulong outblocks;
only - 无意义 *        /* 以 KB 为单位的尺寸 *
ulong vmem_size;               /* 以 KB 为单位的 RSS *
ulong rmem_size;               /* majf/间隔 *
ulong maj_faults;
ulong min_faults;             /* 最小/间隔 - 始终为 0 - 漏洞？
total_swaps;            /* 交换计数 *
long priority;                  /* 当前优先级 *
long niceness;                 /* 当前 nice 值 *
char class[PRSZ];               /* 类名 *
double messages;               /* 间隔消息 *
ulong signals;                 /* 间隔信号 *
ulong vcontexts;              /* 自愿上下文切换/间隔 *
ulong contexts;             /* 非自愿上下文切换/间隔
ulong charios;               /* 字符进出 *
ulong lwp_count;              /* 曾经的 lwp 数量 *
int uid;                        /* 当前 uid *
long ppid;                     /* 父进程 pid *
char fname[PRFS];               /* 执行路径的最后部分 *
char args[PRARGS];             /* 参数的初始部分
```（等待，根据上下文修正最后一行：

`char fname[PRFS];           /* 执行路径的最后部分 *

char args[PRARGS];           /* 参数的初始部分 *`)

### 图 5-6 SE Toolkit Process Class 的组合进程信息（续）

第 5 章 工作负载测量 99

5-6 中的大部分数据都是自而易懂的。所有时间以秒为精度。最小页异常计数器似乎坏了，因为它总是报告 0。输入块和输出块计数器没有意义，因为它们只引用文件缓存的元数据。`charles` 计数包含了所有文件描述符的读写数据，因此你可以看到文件 IO 速率。`lwp_count` 不是当前的 `lwp` 数量。它是进程曾经拥有的 `lwp` 数量。如果计数大于1，则进程是多线程的。可以访问每个 `lwp` 并读取其 `psinfo` 和使用数据。进程数据是这些数据的和。

子数据在进程退出时积累。子进程使用的 CPU 被累加到父进程。这可以用于发现产生短寿命命令的进程。

## 统计

谁运行了、何时以及多少资源？

许多进程的生命周期很短。你无法通过 `ps` 查看此类进程，但它们可能非常频繁，从而主导系统的负载。捕捉它们的唯一方法是让系统记录每个运行过的进程、谁运行的、是什么、何时开始和结束以及使用了多少资源。答案来自系统统计子系统。虽然你可能对统计“老大哥盯着你”的含义或额外开销的成本有所担心，但这些信息非常有价值。收集统计数据的开销总是存在的，但微不足道。

统计数据在长时间的测量中最为有用。这种时间信息在工作站网络以及单个时分服务器上都有用。从这些信息中，你可以识别程序运行的频率、每个程序使用的 CPU 时间、I/O 和内存，以及在周期间的模式。要立即启用统计，请输入以下三个命令。

```
# ln /etc/init.d/acct /etc/rc0.d/K22acct
# ln /etc/init.d/acct /etc/rc2.d/S22acct
# /etc/init.d/acct start
启动进程统计
```

请参考《Solaris System Administration Answerbook》中的会计章节并查看 `acctcmd`。添加一些条目来汇总和检查点会计日志。收集和检查点会计数据对系统产生的负载微乎其微，但每天或每周运行一次的汇总图表具有显著的效果，请将其安排在非业务时间运行。

管理员用户的 `crontab` 文件应包含以下内容：

```
# crontab -1 adm
| #ident | "@(#) adm | 1.5 | 92/07/14 SMI* | /* Svr4.0 1.2 | / | |
| #min | day | month | weekday |
| 0 | * | * | * | /usr/lib/acct/ckpact |
| 30 | 2 | * | * | /usr/lib/acct/runacct 2 > /var/adm/
| acct/nite/fd2log | 9 | * | 5 | /usr/lib/acct/runacct |
```

你可以获得每日会计摘要，但最好跟踪存储在 `/var/adct/acfil` 中的每月摘要。以下是来自 `fiscript07` 的示例，它是该桌面环境 7 月份的报告。

1990年7月26日

| FIS 07 命令总计 第 1 页 |

| 命令数量 | 总计 | 总 | 总 | 平均 | HOG | 字符 块 |

| 名称 | CMDS | KOREMIN | REAL-MIN | SIZE-K | CPU-MIN | FACTOR |

| 总计 | 26488 | 1606200.75 | 3960.11 | 49462.41 | 4055.95 | 0.15 | 0.01 | 1724829964 | 1653 |

| mae | 36 | 714287.25 | 1501.73 | 2128.50 | 4756.45 | 0.41 | 0.71 | 205981444 | 3434 |

| sundango | 16 | 3668845.19 | 964.83 | 1074.34 | 3802.36 | 0.60 | 0.90 | 139538911 | 1295 |

| Xsun | 29 | 1342098.55 | 501.52 | 991.62 | 5640.18 | 0.67 | 0.03 | 274879402 | 1151 |

| xlock | 32 | 1027093.16 | 726.87 | 425.43 | 4863.71 | 0.19 | 0.47 | 40099888 | 37838 |

| fountain | 20 | 808205.26 | 141.55 | 333.65 | 6762.19 | 0.11 | 0.56 | 517976 | 15 |

| cityscape | 22 | 489512.97 | 72.39 | 367.61 | 7936.27 | 0.32 | 0.88 | 80257392 | 3064 |

| marker4X | 14 | 426182.31 | 43.77 | 5004.30 | 9736.27 | 0.4 | 0.85 | 355813610 | 587 |
