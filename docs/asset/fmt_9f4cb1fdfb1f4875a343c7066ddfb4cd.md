
```
$ grep LatencyTOP /boot/config-$(uname -r)

CONFIG_HAVE_LATENCY_SUPPORT=y
```

`LatencyTOP` 通过 `proc` 文件系统与用户空间通信。访问这些信息需要 root 权限。通过向 `/proc/sys/kernel/latency` 写入“1”或“0”来启用或禁用数据采集。一旦启用，可以通过 `/proc/latency_stats` 获取整个系统的延迟统计。此外，可以通过进程目录下的 latency 文件访问，例如 `/proc/2145/latency`。

每个文件的第一行是头部，标识 `LatencyTOP` 版本。头部之后是零或多个数据条目。每个条目的格式为三个整数后跟着字符串。该字符串包含函数栈，从右侧开始，每个函数调用用空格分隔。此调用只跟踪内核函数，因此右侧的函数总是系统调用。第一个整数表示该函数调用的次数。第二个整数表示该调用栈引起的总微秒延迟。第三个整数表示该调用栈单次调用的最大延迟（van de, 2008）。

例如：

```bash
$ cat /proc/630/latency
Latency Top version : v0.1

1 881 poll_schedule_timeout do_sys_poll Sys_poll system_call_ fastpath

1 9 futex_wait_queue_me futex_wait_futex Sys_futex system_call_ fastpath
```
