
| 0x00000000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | <unknown> [App] |
| `/home/orc/ALCD2/lib/app1.so` | 0x00400000 | | | PRIVATE_MEM_COMMIT | PAGE_EXECUTE | Image [App] |
| `/home/orc/ALCD2/lib/app1.so` | 0x00418000 | | | PRIVATE_MEM_COMMIT | PAGE_READONLY | Image [App] |
| `/home/orc/ALCD2/lib/app1.so` | 0x00000000 | | | PRIVATE_MEM_COMMIT | PAGE_READWRITE | Image [App] |
| 0x00360000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00400000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00400000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00410000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00418000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420000 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420020 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420038 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420048 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420058 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420068 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |
| 0x00420078 | 0x00000000 | | | PRIVATE_MEM_COMMIT | | |

19. 我们在退出 WinDbg 会话前选择了日志：

```
0:000> logclose
Opening log file 'C:\ALCD2\A64\App1-WinDbg.log'
```

我们建议在每次练习后退出 WinDbg。

## 练习 A2D

- **目标**: 学习如何识别异常、查找问题线程和 CPU 指令。
- **模式**: 崩溃签名；空指针（数据指针）；活跃线程 (x64, GDB)

`\ALCDA-Dumps\Exercise-A2D-x64-GDB.pdf`
`\ALCDA-Dumps\Exercise-A2D-A64-GDB.pdf`
`\ALCDA-Dumps\Exercise-A2D-A64-WinDbg.pdf`
`\ALCDA-Dumps\Exercise-A2D-x64-WinDbg.pdf`

## 练习 A2D (x64, GDB)

目标：学习如何识别异常、找到问题线程和 CPU 指令。

模式：崩溃签名；空指针（数据指针）；活跃线程。

1. 从 `x64/App2D` 目录加载 `core.App2D` 文件和 App2D 可执行文件：

```
~/ALCD2/x64/App2D$ gdb -c core.App2D -se App2D
GNU gdb (Debian 8.2.1-2+b3) 8.2.1
Copyright (2018) Free Software Foundation, Inc.
License GNU: GPL version 3 or later <http://www.gnu.org/licenses/gpl.html>
这是一个自由软件：可以更改和重新发布。
在法律允许的范围内不提供任何保证。
输入 "show copying" 和 "show warranty" 查看详情。
此 GDB 配置为 "x86_64-linux-gnu"。使用 "show configuration" 查看配置详情。
有关错误报告的说明，请参阅：
http://www.gnu.org/gdb/bugs/.
在网上查找 GDB 手册和其他在线文档资源：
http://www.gnu.org/software/gdb/documentation/
```

需要帮助时请输入 "help"。

输入 "apropos word" 搜索与 "word..." 相关的命令。

正在从 App2D 读取符号..

```
[New LWP 3577]
[New LWP 3575]
[New LWP 3576]
[New LWP 3579]
[New LWP 3578]
[Thread debugging using libthread_db enabled]
使用主机 libthread_db库 "lib/x86_64-linux-gnu/libthread_db.so"。
core 由 ../App2D 生成。
程序因信号 SIGSEGV 终止，段错误 (Segmentation fault)。
#0 0x0000000000401bbd in procA (a)
[Current thread 1 (0x7faf716597000 (LWP 3577))]
```

2. 将日志重定向到文件，以防命令输出过长：

```
(gdb) set logging on App2D.log
正在将输出拷贝到 App2D.log。
```

3. 列出所有线程：

| Id | info threads | Frame |
|---|---|---|
| *1 | Thread 0x7faf71659700 (LWP 3577) | 0x0000000000401bbd in procA (a) |
| 2 | Thread 0x7faf98780 (LWP 3575) | 0x000000000442a21 in clone () |
| 3 | Thread 0x7faf71e5a700 (LWP 3576) | 0x000000000041a50 in nanosleep () |
| 4 | Thread 0x7faf706f5700 (LWP 3579) | 0x000000000442a21 in clone () |
| 5 | Thread 0x7faf70e58700 (LWP 3578) | 0x000000000441a50 in nanosleep () |

4. 问题线程似乎是当前线程：

```
(gdb) thread 1
[Switching to thread 1 (Thread 0x7faf71659700 (LWP 3577))]
#0 0x0000000000401bbd in procA (a)
```

```
(gdb) bt
# 0 0x000000000401bbd in procA ()
# 1 0x0000000004010c3b in bar_two ()
# 2 0x0000000004010c4c in foo_two ()
# 3 0x0000000004010c65 in thread_two ()
# 4 0x0000000004013113 in start_thread (arg=<optimized out>) at pthread_create.c:486
# 5 0x0000000004042a2f in clone ()
```

5. 反汇编问题指令并检查 CPU 寄存器详情（NULL 数据指针）：

```
(gdb) x/1 0x000000000401bbd
=> 0x401bbd <procA+16>: mov $0x1,%rax
```

`gdb` 命令 `info $rax`

```
(gdb) x $rax
0x0: Cannot access memory at 0x0
```

6. 列出所有线程堆栈并识别非等待活跃线程：

```
(gdb) apply all bt
Thread 5 (Thread 0x7faf70e58700 (LWP 3578)):
# 0 0x000000000441a50 in nanosleep ()
# 1 0x00000000041a9da in sleep ()
# 2 0x000000000441c7a in bar_two () at pthread_create.c:688
# 3 0x000000000441c6b in foo_two ()
# 4 0x000000000441cd4 in thread_three () at pthread_create.c:688
# 5 0x000000000031113 in start_thread (arg=<optimized out>) at pthread_create.c:486
# 6 0x000000000442a2f in clone ()
Thread 4 (Thread 0x7faf7065770 (LWP 3579)):
# 0 0x000000000442a21 in clone ()
# 1 0x00000000003028 in ?? () at pthread_create.c:362
# 2 0x0000000007faf0657700 in ?? ()
# 3 0x0000000000000000 in ?? ()
Thread 3 (Thread 0x7faf71e5a700 (LWP 3576)):
# 0 0x000000000441a50 in nanosleep ()
# 1 0x00000000041a9da in sleep ()
# 2 0x000000000441bfc in bar_one () at pthread_create.c:688
# 3 0x000000000441c0d in foo_one () at pthread_create.c:688
# 4 0x000000000441d26 in thread_one () at pthread_create.c:688
# 5 0x000000000031113 in start_thread (arg=<optimized out>) at pthread_create.c:486
# 6 0x000000000442a2f in clone ()
Thread 2 (Thread 0x7faf097880 (LWP 3575)):
# 0 0x000000000442a21 in clone ()
# 1 0x000000000414f4 in create_thread (pd@entry=0x7faf065770, attr@entry=0x7ff7cddbc0, started_stack@start_entry=0x7ff7cddcee, stackaddr@entry=0x7ff7cddcef, thread_run@start_entry=0x7ff7cdd6ce@/sys/kernel/clone.c:101)
# 2 0x00000000043986 in pthread_create (newthread=<optimized out>, attr=<optimized out>, start_routine=<optimized out>, arg=<optimized out>) at pthread_create.c:826
# 3 0x000000000401dac in main () at pthread_create.c:688
Thread 1 (0x7faf1659700) [LWP 3577]:
#0 0x0000000000000bd in procA () at pthread_create.c:688
#1 0x000000000000401c in bar_two () at pthread_create.c:688
#2 0x00000000000041c4 in foo_two () at pthread_create.c:688
#3 0x00000000000041c5 in thread_two () at pthread_create.c:688
#4 0x0000000000003113 in start_thread (arg=<optimized out>) at pthread_create.c:486
#5 0x000000000000442af in clone ()
```

7. 检查 #4 的 CPU 指令和栈指针，查看是否有任何栈溢出的迹象（跨越当前栈指针的不可访问块）：

```
(gdb) thread 4
Switching to thread 4 (Thread 0x7faf7065770 (LWP 3579])
#0 0x000000000000421 in clone ()

(gdb) bt
#0 0x000000000000421 in clone ()
# 1 0x000000000003028 in ?? () at pthread_create.c:362
# 2 0x0000000007faf0657700 in ?? ()
# 3 0x0000000000000000 in ?? ()
```

`gdb` 命令 `x/1 0x0000000000402a1`

```
=> 0x402a1 <clone+49> test %rax,%rax
```

`gdb` 命令 `x $rsp`

```
(gdb) x $rsp
0x7faf7065770: 0x40320
```

`gdb` 命令 `x $rsp-10`

```
0x7faf706e6f0: 0x000000
```

8. 切换到线程 #2 并验证 main 函数在线程 #4 中执行：

```
(gdb) thread 2

Switching to thread 2 (Thread 0x7faf097880 [LWP 3575])

#0 0x00000000000042a1 in clone ()

```
`gdb` 命令 `bt`

```
(gdb) bt
#0 0x00000000000042a1 in clone ()
# 1 0x00000000041f74 in create_thread (pd@entry=0x7faf065770, attr@entry=0x7ff7cddbc0, started_stack@start_entry=0x7ff7cddcee, stackaddr@entry=0x7ff7cddcef, thread_run@start_entry=0x7ff7cdd6ce@/sys/kernel/clone.c:101)
# 2 0x00000000043986 in pthread_create (newthread=<optimized out>, attr=<optimized out>, start_routine=<optimized out>, arg=<optimized out>) at pthread_create.c:826
# 3 0x000000000401dac in main () at pthread_create.c:688
```

`gdb` 命令 `disassemble main`

```
0x00000000040001d9 <+0>:  push   %rbp
0x00000000040001d2 <+1>:  mov    %rsp,%rbp
0x00000000040001d4 <+2>:  sub    $0x40,%rsp
0x00000000040001d8 <+8>:  mov    %edi,-34(%rbp)
0x00000000040001d4 <+11>: mov    %rsi,-44(%rbp)
0x00000000040001d8 <+15>: lea    -8(%rbp),%rax
0x00000000040d041c <+19>: mov     $0x,%ec
0x00000000040d04d1 <+24>: lea     -138(%rip),%rdx    # 0x401c10 thread_one_
0x00000000040d04d8 <+31>: mov     $0x,%esi
0x00000000040d04d4 <+36>: mov     %rax,%rdi
0x00000000040d04d9 <+39>: callq  0x40b340 <pthread_create_2>
0x00000000040d04d5 <+44>: mov     -10(%rbp),%rax
0x00000000040d045e <+49>: mov     $0x,%esi
0x00000000040d0453 <+54>: lea     -116(%rip),%rdx    # 0x401c84 thread_two_
0x00000000040d0456 <+59>: mov     $0x,%esi
0x00000000040d046a <+64>: mov     %rax,%rdi
0x00000000040d0468 <+69>: callq  0x40b340 <pthread_create_2>
0x00000000040d073 <+73>: lea     -137(%rip),%rdx
0x00000000040d077 <+77>: mov     -04(%rip),%rdx
0x00000000040d082 <+82>: mov     $0x,%esi
0x00000000040d087 <+87>: mov     %rax,%rdi
0x00000000040d08c <+92>: callq  0x40b340 <pthread_create_2>
```
