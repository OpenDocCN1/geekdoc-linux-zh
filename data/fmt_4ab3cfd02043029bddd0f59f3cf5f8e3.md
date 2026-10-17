
```bash
lnx02:~ # ltrace -c ls
autoinst.xml  forker      netperf     out_file    segfault    tcp_crr     tcp_stream
threader      vpd.properties
bin          kerntest    netserver   rmfms       segfault.c  tcp_rr      test.c
threader.c
% time     seconds    usecs/call     calls      function
--------------- --------------- ----------- --------- --------------------
34.01      0.004400    4400           1          qsort
15.20      0.001966    19             101        __errno_location
15.13      0.001958    19             102        __ctype_get_mb_cur_max
7.98       0.001033    22             47         __overflow
7.10       0.000919    19             47         strcoll
5.19       0.000671    20             32         readdir
4.13       0.000534    534            1          setlocale
3.49       0.000452    19             23         malloc
2.69       0.000348    20             17         fwrite_unlocked
1.34       0.000173    21             8          getenv
0.58       0.000075    75             1          opendir
0.44       0.000057    19             3          free
0.42       0.000054    54             1          fclose
0.30       0.000039    39             1          isatty
0.26       0.000033    33             1          closedir
0.25       0.000032    32             1          getopt_long
0.24       0.000031    31             1          ioctl
0.24       0.000031    31             1          bindtextdomain
0.19       0.000025    25             1          _setjmp
0.19       0.000024    24             1          _init
0.17       0.000022    22             1          realloc
0.16       0.000021    21             1          __fpending
0.15       0.000020    20             1          textdomain
0.15       0.000019    19             1          __cxa_atexit
------------------------------- ------------------------------- -------------------------------
100.00     0.012937              393 total
```

### 3.3.4 SysRq

SysRq 是一种键盘组合键，无论内核正在执行什么其他操作，只要它没有完全死锁，都会响应该按键。除了内核 oops 或 panic 之外，任何内核问题都不会自动触发内核核心转储。如果系统在某种程度上仍能响应键盘输入，则可以通过魔法 SysRq 键盘组合键手动触发内核核心转储。为此，运行在系统上的内核必须启用 `CONFIG_MAGIC_SYSRQ` 进行编译。这些魔法按键可分别提供当前运行进程和所有进程的堆栈跟踪。系统会生成一个 `/var/log/messages` 文件用于回溯分析。

要为正在运行的内核启用此功能，请执行以下命令。在图 3-12 中，我们列出了 `/proc/sys/kernel/sysrq` 中可能的值。

```text
0 - 完全禁用 sysrq
1 - 启用 sysrq 的所有功能
>1 - 允许使用的 sysrq 功能的位掩码（有关详细功能说明，请参阅下文）：
  2 - 启用控制台日志级别控制
  4 - 启用键盘控制（SAK, unraw）
  8 - 启用进程等调试转储
 16 - 启用 sync 命令
 32 - 启用以只读方式重新挂载
 64 - 启用向进程发送信号（term, kill, oom-kill）
128 - 允许重启/关机
256 - 允许对所有 RT 任务进行 nice 值调整
```

**图 3-12 可为 SysRq 设置的值**

#### 示例 3-44 启用 sysrq

```bash
echo 1 > /proc/sys/kernel/sysrq
```

若要永久启用魔法 SysRq 功能，请在 `/etc/sysconfig/sysctl` 文件中更新 `ENABLE_SYSRQ="yes"`。若要获取有关使用 SysRq 的信息，可以执行 `"echo t > /proc/sysrq-trigger"`。内核跟踪信息将被写入 `"/var/log/messages"`。请参阅示例 3-45。

#### 示例 3-45 来自 /var/log/messages 的 SysRq 报告

```bash
lnx02:/ # echo 1 > /proc/sys/kernel/sysrq
lnx02:/ # echo t > /proc/sysrq-trigger
lnx02:/ # tail /var/log/messages
Mar 25 13:54:34 lnx02 kernel: 00000000efc7bb40 00000000ffe8aa00
00000000f0d92370 00000000fd092050
Mar 25 13:54:34 lnx02 kernel: 0000000000000000 00000000fd092050
00000000846d37b8 00000000efc7ba60
Mar 25 13:54:34 lnx02 kernel: 00000000ff401000 000000000035b1b8
0000000012a652 00000000efc7ba60
Mar 25 13:54:34 lnx02 kernel: 0000000001950d00 00000000fc6e1d00
07000000efc7bb78 07000000efc7bb78
Mar 25 13:54:34 lnx02 kernel: Call Trace:
```

```
Mar 25 13:54:34 lnx02 kernel: [<000000000013db4a>] schedule_timeout+0x9e/0x150
Mar 25 13:54:34 lnx02 kernel: [<00000000001b2080>] do_select+0x4a0/0x5e8
Mar 25 13:54:34 lnx02 kernel: [<00000000001b2514>] sys_select+0x34c/0x588
Mar 25 13:54:34 lnx02 kernel: [<00000000001f2ac>] sysc_noemu+0x10/0x16
```

#### 表 3-4 SysRq 按键分配

| 按键 | 操作 |
|---|---|
| 'r' | 关闭键盘原始模式并将其设置为 XLATE。 |
| 'k' | 安全访问密钥 (SAK) 终止当前虚拟控制台上的所有程序。 |
| 'b' | 立即重启系统，不同步也不卸载磁盘。 |
| 'o' | 关闭系统电源。 |
| 's' | 尝试同步所有已挂载的文件系统。 |
| 'u' | 尝试将所有已挂载的文件系统重新挂载为只读。 |
| 'p' | 将当前寄存器和标志转储到控制台。 |
| 't' | 将当前任务列表及其信息转储到控制台。 |
