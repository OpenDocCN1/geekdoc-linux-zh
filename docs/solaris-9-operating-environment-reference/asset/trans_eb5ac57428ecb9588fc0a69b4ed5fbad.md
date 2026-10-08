

## proc tools

1119

# proc tools — 进程工具

# 概要

```
/usr/proc/bin/pflags [-r] pid | core...
/usr/proc/bin/pcred pid | core...
/usr/proc/bin/imap [-srx1F] pid | core...
/usr/proc/bin/plld [-F] pid | core...
/usr/proc/bin/psig [-n] pid...
/usr/proc/bin/pstack [-F] pid | core...
/usr/proc/bin/ptiles [-F] pid...
/usr/proc/bin/pwdx [-F] pid...
/usr/proc/bin/pstop pid...
/usr/proc/bin/prum pid...
/usr/proc/bin/pwait [-v] pid...
/usr/proc/bin/ptree -a [pid | user...]...
/usr/proc/bin/ptime command [arg...]
/usr/bin/pargs [-aeFx] [core]
```

注意 — 从 Solaris 8 版本开始，所有的 proc tools 都已从 /usr/proc/bin 移动到 /usr/bin。/usr/proc/bin 中的工具是 /usr/bin 目录下对应工具的新软链接。

# 描述

proc tools 是使用 /proc 功能（参见 proc(4)）的命令。它们大多数接受进程 ID (pid) 列表。处理进程 ID 的工具也接受 /proc/nid 作为进程 ID，因此你可以使用扩展路径 /proc/* 来指定系统中的所有进程。

从 Solaris 8 版本开始，你还可以将某些 proc tools 应用于核心文件（参见 core(4)）。那些可以应用于核心文件的命令接受进程 ID 列表或核心文件名称，或两者兼有。

- pargs: 打印命令参数 (argv[])环境变量和辅助向量 (auxiliary vector)。Solaris 9 版本。
- pflags: 打印每个进程每个轻量级进程 (lwp) 的 /proc 跟踪标志、挂起和持有信号以及 /proc 状态信息。
- pcred: 打印每个进程的凭据（有效、真实保存的 UID 和 GID）。
- pfiles: 报告每个进程中所有打开文件的 stat(2) 和 fcntl(2) 信息。
- plld: 列出链接到每个进程的动态库，包括通过 dlopen(3DL) 显式附加的共享对象。参见 ldd(1)。
- pmap: 打印每个进程的地址空间映射。
- prun: 设置每个进程运行（pstop 的反操作）。
- psig: 列出每个进程的信号动作。参见 signal(3)。
- pstack: 为每个进程中的每个 lwp 打印十六进制+符号栈回溯。
- pstop: 停止每个进程（PR_REQUESTED 停止）。
- ptime: 对命令进行计时，类似于 time(1) 命令，但使用微秒计数以实现可重现的精度。
- ptree: 打印包含指定 pid 或用户的进程树，子进程相对于其父进程会缩进。如果参数为全数字，则视为进程 ID；否则假设为用户登录名。默认为所有进程。
- pwait: 等待所有指定的进程终止。
- pwdx: 打印每个进程当前工作目录。

pfiles、pldd、pmap 和 pwdx 命令在检查目标进程并报告结果时会停止这些进程。在进程停止期间，它无法执行任何操作。

# 选项

- -a (ptree 专用): 包含进程 0 的子进程。
- -a (pargs 专用): 打印 argv[] 的进程参数。Solaris 9 版本新增。
- -e (pargs 专用): 打印进程环境变量及其值。Solaris 9 版本新增。
- -F: 强制获取目标进程，即使另一个进程正在控制它。
- -l (pmap 专用): 打印未解析的动态链接器映射。
- -n (psig 专用): 显示信号处理地址而非名称。Solaris 9 版本新增。
- -r (flags 专用): 如果进程已停止，显示其机器寄存器。
- -r (pmap 专用): 打印进程的保留地址。
- -s (pmap 专用): 打印使用的硬件翻译的页大小。Solaris 9 版本新增。
- -v (pwait 专用): 将每个终止报告到标准输出。
- -x (pmap 专用): 打印进程驻留/共享/映射详情。
- -x (pargs 专用): 打印进程辅助向量。Solaris 9 版本新增。

# 使用

pfiles、pldd、pmap 和 stack 等 proc 工具在检查进程并报告结果时会停止这些进程。进程在停止时无法执行任何操作。例如，如果 X 服务器由一个在 X 服务器控制的窗口下运行的 proc 进程检查，整个系统可能会死锁，因为该 proc 工具将尝试将其结果打印到无法记录的窗口中。在这种情况下，从另一个系统使用 rkill(1) 杀死违问题的 proc 工具即可消除死锁。

使用 -F 选项时要小心。对一个受害者进程施加两个进程可能会导致混乱。只有当主控制进程（通常是调试器）已停止受害者进程，且主控制进程在应用相关 proc 工具的时刻没有执行任何操作时，才能确保安全。

从 Solaris 8 版本开始，某些 proc tools 也可以应用于核心文件。核心文件是进程状态的快照，由内核在通过信号或使用 gcore(1) 命令终止进程产生。某些 proc tools 可能需要获取生成 core 的进程执行文件名称或与进程相关的共享库名称。这些文件对于 pstack(1) 提供符号信息是所需要的。如果相关的 proc 工具无法找到所需的执行文件或共享库，则某些符号信息不可用。同样，如果在不同的操作系统上检查核心文件，运行时调试接口 (librt1d_db) 可能无法初始化。在这种情况下，共享库的符号信息不可用。

# 退出状态

- 0：成功
- 非零：发生了错误。

# 文件

- /proc/*: 进程文件。
- /usr/proc/lib/* 支持 proc 工具的文件。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 | 可性 |
| :--- | :--- | :--- |
| 32-bit | SUNW | |
| 64-bit | SUNW | |

# 参见

core(4), dlopen(3DL), exit(3), fcntl(2), gcore(1), gprof(1), kill(1), ldd(1), librt1d_db, pstack(1), signal(3), proc(4), attributes(5), rkill(1), ptrace(2), stat(2), time(1), wait(2)

