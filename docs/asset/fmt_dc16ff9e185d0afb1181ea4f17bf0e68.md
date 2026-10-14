
```
# cd /proc/11934
# ls -l
total 3497
-rw------- 1 users 1769472 Mar 30 09:20 as
-r------- 1 users 152 Mar 30 09:20 auxv
-r------- 1 users 32 Mar 30 09:20 cred
-r------- 1 users 0 Mar 30 09:20 ctl
-r-x------ 1 users 0 Mar 30 09:20 cwd ->
dr-xr-x 2 users 1184 Mar 30 09:20 fd
-r-r-- 1 users 1200  30 09:20psinfo
-r------- 1 users 9122 30 09:20 latus
atus
-r-r  1 users 236 Mar 30 09:20 usage
dr-xr-x 3 users 48 Mar 30 09:20 lwp
-r------- 1 users 2016 Mar 30 09:20 map
dr-x------ 2 users 544 Mar 30 09:20 pagedata
-r-r-- 1 users 2552 Mar 30 09:20 pagevent
-r------- 1 users 336 Mar 30 09:20 psinfo
-r-x------ 1 users 2016 Mar 30 09:20 rmap
-r------- 1 users 0 Mar 30 09:20 root ->
-r------- 1 users 1440 Mar 30 09:20 sigfault
-r------- 1 users 12322 Mar 30 09:20 status
-r-r-- 1 users 256 Mar 30 09:20 usage
-r-r-- 1 users 0 Mar 30 09:20 watch
-r------- 1 users 3192 Mar 30 09:20 xmap
```

每个与 `PID` 同名的目录都包含额外的子目录，这些目录包含状态信息和相关的控制函数。例如，`status` 文件包含定义状态元素的结构，包括以下内容：

* 进程标志
* 进程 ID
* 父进程 ID
* 进程组 ID
* 会话 ID
* 线程 ID
* 进程挂起信号集
* 进程堆虚拟地址
* 进程栈大小
* 用户和系统 CPU 时间
* 总子进程用户和系统 CPU 时间
* 故障轨迹

# 第 22 章：伪文件系统与交换空间

结构中的进程标志定义了特定的进程状态特征，包括以下内容：

- `PR_ISSYS` 系统进程标志
- `PR_VFORKP` vfork 子进程/父进程标志
- `PR_FORK` fork 继承（Inher-on-fork）标志
- `PR_RLC` 最后关闭运行（Run-on-last-close）标志
- `PR_KLC` 最后关闭杀死（Kill-on-last-close）标志
- `PR_ASYNC` 异步停止（Asynchronous-stop）标志
- `PR_MSACCT` 微状态计数开启标志
- `PR_MSFORK` fork 后微状态计数继承标志
- `PR_BPTADJ` 断点开启标志
- `PR_PTRACE` ptrace 性开启标志

> 考试提示 访问 `docs.sun.com` 上的材料以获取关于 `proc` 文件系统的更多信息。

此外，还提供了一个路径设施，负责控制内存访问。一系列 `proc` 工具可以解释 `/proc` 子目录中包含的信息，这些信息显示了每个进程的特征。这些工具设计用于操作 `/proc` 文件系统中的数据。每个实用程序使用 `PID` 作为参数，并执行与 `PID` 相关的操作。例如，`pflags` 命令打印该 `PID` 问题的标志和数据模型细节。对于 Korn shell，我们可以轻松地打印出此状态：

```
# /usr/proc/bin/pflags 29081
29081: /bin/ksh data model = IL3P2 flags = PR_ORPHAN/ flags = PR_PCNVAL_PR_ASLEEP [ waitid(0x7,0x0,080414c,0x7) ]
```

我们可以使用 `pcred` 命令打印此进程的凭据信息，包括进程所有者的有效真实 `UID` 和 `GID`：

```
# /usr/proc/bin/pcred 29081
29081: e/r/uid=100 e/r/gid=10
```

在这里，有效和真实的 `UID` 均为 100（用户 pretty），有效和真实的 `GID` 为 10（组 staff）。要检查目标进程的地址空间以及它执行时使用的库，我们使用 `pmap` 命令：

```
# /usr/proc/bin/pmap 29081
29081: 08046000 8K read/write/exec [ stack ]
08048000 16K read/exec /usr/bin/ksh
08070000 8K read/write/exec /usr/bin/ksh
```

```
08072000      28K read/write/exec      [ heap ]
DFAB4000      16K read/write/exec      /usr/lib/locale/en_AU/en_AU.so.2
DFAB8000       8K read/write/exec      /usr/lib/locale/en_AU/en_AU.so.2
DFABB0000      4K read/write/exec      [ anon ]
DFABD0000      12K read/write/exec      /usr/lib/libmp.so.2
DFCA0000      4K read/write/exec      /usr/lib/libc.so.1
DFB42000      52K read/write/exec      /usr/lib/libc.so.1
DFB54000       8K read/write/exec      [ anon ]
DFB57000     444K read/write/exec      /usr/lib/libnsl.so.1
DFBC6000      328K read/write/exec      /usr/lib/libnsl.so.1
DFBD0000      32K read/write/exec      [ anon ]
DFBD4000       8K read/write/exec      /usr/lib/socket.so.1
DFBC0000       4K read/write/exec      /usr/lib/socket.so.1
DFBD0000       4K read/write/exec      /usr/lib/libldl.so.1
DFBE3000     100K read/write/exec      [ anon ]
DFBE6000      14K read/write/exec      /usr/lib/ld.so.1
DFFC0000     148KB                               /usr/lib/ld.so.1
```

看到应用程序执行时加载了这么多库真是令人惊讶，特别是对于像 shell 这样复杂的程序——在本例中，导致了总计 148KB 的内存使用。你可以使用 `plld` 命令获取链接到每个进程的动态库列表：

```
# /usr/proc/bin/plld 29081
29081: /bin/ksh
/usr/lib/libnsl.so.1
/usr/lib/libc.so.1
/usr/lib/libldl.so.1
/usr/lib/lib.so.2
/usr/lib/locale/en_AU/en_AU.so.2
```

信号是进程之间通信的方式，也可以从 shell 与派生的进程进行通信（通常用于挂起或杀死它们）。我们在第 8 章检查信号。然而，通过使用 `psig` 命令，可以列出与每个进程相关的信号：
