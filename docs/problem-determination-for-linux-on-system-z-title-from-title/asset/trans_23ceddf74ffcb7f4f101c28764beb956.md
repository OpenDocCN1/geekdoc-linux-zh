
也可以使用 `-e trace=open` 选项仅获取 `open()` 系统调用的跟踪信息。

为了演示 strace 的功能，我们编写了一个简单程序，该程序试图打开一个完全未初始化的文件描述符。尽管程序本身没有报错，但使用 strace 我们仍能进行调试并发现程序存在某些缺陷。在示例 3-40 中，strace 指出该程序试图打开一个不可用的文件。

## 示例 3-40 使用 strace 调试无效文件描述符问题

```bash
lnx02:~ # strace -o report.txt ./unmemory
Could not open the file
lnx02:~# cat report.txt
execve("./unmemory", ["./unmemory"], [/* 53 vars */]) = 0
uname({sys="Linux", node="lnx02", ...}) = 0
brk(0)                                 = 0x80002000
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x2000001a000
open("/etc/ld.so.preload", O_RDONLY)   = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY)     = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=90768, ...}) = 0
mmap(NULL, 90768, PROT_READ, MAP_PRIVATE, 3, 0) = 0x2000001b000
close(3)                               = 0
open("/lib64/tls/libc.so.6", O_RDONLY) = 3
read(3, "\177ELF\2\1\0\0\0\0\0\0\0\0\0\3\0\26\0\0\0\1\0\0\0"..., 640) = 640
lseek(3, 624, SEEK_SET)                = 624
read(3, "\0\0\0\4\0\0\0\0\20\0\0\0\1GNU\0\0\0\0\0\0\0\2\0\0\0\6"..., 32) = 32
fstat(3, {st_mode=S_IFREG|0755, st_size=1542487, ...}) = 0
mmap(NULL, 1331616, PROT_READ|PROT_EXEC, MAP_PRIVATE, 3, 0) = 0x20000032000
madvise(0x20000032000, 1331616, MADV_SEQUENTIAL|0x1) = 0
mmap(0x20000157000, 118784, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED, 3, 0x124000) = 0x20000157000
mmap(0x20000174000, 12704, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x20000174000
close(3)                               = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x20000178000
munmap(0x2000001b000, 90768)           = 0
brk(0)                                 = 0x80002000
brk(0x80023000)                        = 0x80023000
brk(0)                                 = 0x80023000
open("file.txt", O_RDONLY)             = -1 ENOENT (No such file or directory)
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 1), ...}) = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x2000001b000
write(1, "Could not open the file \n", 25) = 25
munmap(0x2000001b000, 4096)           = 0
exit_group(0)                         = ?
```

### 3.3.3 ltrace

`ltrace` 实用工具可以拦截并记录由执行进程发出的动态库调用以及该进程接收到的信号。它还可以拦截并打印程序执行的所有系统调用。

与 `strace` 类似，`ltrace` 也非常擅长获取跟踪信息。`ltrace` 实用工具可以通过以下两种方法进行调试：

- 使用 `ltrace` 实用工具启动用户程序或应用程序（示例 3-41）。

#### 示例 3-41 获取 ls 命令的 ltrace 示例

```bash
lnx02:~ # ltrace -o out_file -tt -f echo .hello.
.hello.
lnx02:~ # cat out_file
9901 21:02:44.476858 __libc_start_main(0x800014b0, 2, 0x3ffffa0f348, 0x80003344, 0x80003340 <unfinished ...>
9901 21:02:44.477045 getenv("")
= "LC_ALL"
9901 21:02:44.477126 setlocale(6, "")
= "C"
9901 21:02:44.477687 bindtextdomain("/usr/share/locale", "/usr/share/locale") = "/usr/share/locale"
9901 21:02:44.477791 textdomain("/usr/share/locale")
= "coreutils"
9901 21:02:44.477877 __cxa_atexit(0x80001a84, 0, 0, 0x20000065610, 0x80003828) = 0
9901 21:02:44.477957 getopt_long(2, 0x3ffffa0f348, "", 0x80005028, NULL) = -1
9901 21:02:44.478044 fputs_unlocked(0x3ffffa0f638, 0x2000018ba80, 0x8000162c, 1, 1) = 1
9901 21:02:44.478152 __overflow(0x2000018ba80, 10, 0x8000157c, 0x20000027007, 0) = 10
9901 21:02:44.478335 exit(0 <unfinished ...>
9901 21:02:44.478378 __fpending(0x2000018ba80, 0, 0x80001a84, 0x2000018a8a8, 0)
= 0
9901 21:02:44.478631 ++ exited (status 0) +++
```

- 使用 `ltrace` 实用工具挂接到正在运行的进程的 PID（示例 3-42）。

#### 示例 3-42 PID 1834 的 ltrace

```bash
ltrace -o out_file -tt -f -p 1834
```

注意：`ltrace` 无法跟踪线程进程。如果某个进程生成了一个共享同一地址空间的线程（即使用参数 `CLONE_VM` 和 `CLONE_THREAD` 调用 `clone` 系统调用），被跟踪的进程将因收到 `SIGILL` 信号而终止。

这里展示的另一个简单示例是使用 `ltrace` 获取系统调用统计信息，如调用次数、时间和调用列表。在示例 3-43 中，我们将 `ls` 命令作为被跟踪的可执行文件传入。从示例 3-43 中，我们可以看到哪个函数被调用得最多并消耗大量 CPU 周期。通过这种方式，开发人员可以优化其代码以提高运行效率。

#### 示例 3-43 使用 ltrace 进行调用跟踪

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

