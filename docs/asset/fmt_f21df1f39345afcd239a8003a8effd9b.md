
## 用法
`paxtcl <options> <files>`

### 选项
- `-p`：禁用 `PAGEEXEC`；`-P`：启用 `PAGEEXEC`
- `-e`：禁用 `EMUTRMAP`；`-E`：启用 `EMUTRMAP`
- `-m`：禁用 `MPROTECT`；`-M`：启用 `MPROTECT`
- `-r`：禁用 `RANDMAP`；`-R`：启用 `RANDMAP`
- `-x`：禁用 `RANDEXEC`；`-X`：启用 `RANDEXEC`
- `-s`：禁用 `SEGMEXEC`；`-S`：启用 `SEGMEXEC`
- `-v`：查看标记；`-z`：恢复默认标记
- `-q`：静制错误消息；`-Q`：简报标记

### 标记格式
例如：
```
# paxtcl -v /usr/bin/
PaX control v0.2
Copyright 2004 PaX Team <pageexec@freemail.hu>
```

- PaX 标记：`--M--ER- [/usr/X11R6/bin/XFree86]`

`MPROTECT` 已启用

`EMUTRAMP` 已启用

`RANDMAP` 已启用

为了实验目的，你可能想以软模式运行系统一短时间，仅在少数测试服务上启用 `PaX`。当你对其完全满意后，以正常模式启动，使所有可执行文件默认启用 `PaX`。如果应用程序在 `PaX` 下运行异常（可能是由于跳板，或预期 `malloc()` 分配的内存是可执行的），你随后可以禁用它们的部分或全部保护（唯一与 `PaX` 不兼容的应用程序是 `XFree86`）。请记住，由于 `PaX` 控制标记存储在可执行文件的头中，它们在重启后将仍然存在，但重新安装应用程序会导致任何分配给该可执行文件的 `Pax` 标记丢失。你可能想创建一个在启动时执行并包含 `paxtcl` 命令的 shell 脚本。

# 缓冲区溢出检测
`PaX` 的 `ASLR` 特性非常有用，但因为其依赖随机性，理论上只要有足够的时间是可以被破解的。由于错误的猜测将不可避免地导致应用程序崩溃，因此，一个不断崩溃的服务（大多数服务被配置为崩溃后自动重启）可能是攻击者正尝试缓冲区溢出攻击的迹。为了防止攻击者在 `ASLR` 保护的进程中猜测正确内存布局的可能性（远程），你需要限制守护进程在给定时间内允许重启的次数。

设置此限制的工具之一是 `Segvguard`，可从 `ftp://fp.pl.open.com/misc/segvguard/` 获取。`Segvguard` 由两部分组成：一个内核模块和一个用户态守护进程（`segvdaemon`）。该模块拦截 `SIGGV`、`SIGKILL`、`SIGBUS` 和 `SIGILL` 信号，并将进程临时暂停在 `TASK_UNINTERRUPTIBLE` 状态。它通知被拦截的信号，并等待 `segvdaemon` 提供进一步指令。

什么构成潜在攻击由用户态守护进程 `segvdaemon` 决定。目前，`Segvguard` 将具有以下属性的崩溃视为潜在攻击：

- 进程正在以 `SUID` 运行。
- 导致崩溃的用户 `UID` 与执行该进程的 `UID` 不符。
- 进程 `UID` 为 `0`（以 `root` 身份运行）。

# 系统加固 323
## 8.5 使用 STRACE 策略系统调用
“系统调用”一词被管理员频繁使用，但他们往往没有完全理解其含义。简单来说，系统调用是用户空间应用程序向内核请求资源或操作的手段；其形式可能表现为（例如）创建目录（`sys_mkdir`）、设置系统时钟（`sys_stime`）或挂载文件系统（`sys_mount`）。`Linux` 定义了超过 200 多个系统调用，涵盖了从文件处理到内存管理的广泛功能。你可以在 `http://linuxassembly.org/syscall.html` 查看完整列表。

在本章早前的“`Strace`”部分中，我们曾将 `strace` 视为查看进程所发系统调用的手段；你可能想要回顾一下这个系统调用，因为该命令对 `Linux` 的内部工作机制提供了有趣的见解。你可能会惊讶于执行像 `pwd` 或 `uname` 这样的典型程序时，竟然使用了如此多的系统调用。

从安全的角度来看，系统调用特别有趣，因为如果我们能控制对它们的访问，就可以紧密且细粒度地控制用户或进程在系统上的权限。在 `OpenBSD` 世界中，用于此目的的流行程序是 `Strace` (`http://www.strace.org`)，并且提供了 `Linux` 端口。

对于它所保护的每个应用程序，`Strace` 维护一个策略文件，规定允许哪些系统调用。未在该文件中列出的调用将被拒绝，并向 `syslog` 发送错误消息。然而，与仅仅复制实际系统调用的类似项目不同，`Strace` 还会监控给它的参数。这使得例如，可以允许网络守护进程使用 `sys_bind()` 调用，但仅绑定到特定端口；或者允许守护进程读取其配置文件，但不允许读取 `/etc` 中的其他文件。预判应用程序可能进行的每一个系统调用是棘困难的，因此 `Strace` 还提供了一种交互式学习模式，在此模式下它将监控应用程序并尝试构建一个合适的策略文件。这消除了大部分繁性工作。

### 安装
`Strace` 以内核补丁、用户空间管理工具以及（可选的）`GTK`（`GIMP Toolkit`）前端的形式提供；所有这三者都可以从 `http://www.citi.umich.edu/u/pro/strace/` 获取。用户空间应用程序的源代码不特定于平台，但在下载内核补丁时，请确保选择 `Linux` 端口。

补丁和编译内核是我们迄今已多次涵盖的话题，因此我们在此不再详述。在将 `Strace` 补丁应用到内核源码后，`Linux` 安全选项菜单中会创建一个 `Strace` 支持（`CONFIG_SYSTRACE`）选项（假设你正在使用 `2.6.x` 内核）。启用此选项。

现在你已经重新编译了内核，可以安装用户空间工具了。`Strace` 需要 `libevent`（可从 `http://monkey.org/~provos/libevent/` 获取），因此你需要先安装它。在配置 `Strace` 时，你可能还需要指定 `libevent` 的安装路径：
```
$ ./configure --with-libevent=/usr/local
```

然后你可以像往常一样构建应用程序：
```bash
# make
# make install
```

如果编译失败并提示错误未找到 `linux/strace.h`，这表明补丁未正确应用。通过将内核补丁中的 `strace.h` 复制到 `/usr/include/linux` 可以轻松解决此问题：
```bash
# cp /usr/src/linux-2.6.1/include/linux/strace.h \
/usr/include/linux/strace.h
```

然后尝试再次 `make`。

# 策略文件的组件
如前所述，策略文件构成了 `Strace` 的核心，精确定义了允许应用程序进行的系统调用（及其参数）。策略可能存储在 `/etc/strace` 目录下——这是 `Strace` 查找的第一个位置。如果没有找到策略文件，`Strace` 会 `~/.strace` 中查找。策略的文件名基于相关应用程序的名称（包括路径），并将正斜杠替换为下划线，例如 `usr_bin_ls`。

# 通用语法
典型策略文件的摘可能如下：
```
Policy: /bin/login, Emulation: linux
linux-newname: permit
linux-brk: permit
linux-old_mmap: permit
linux-fsread: filename eq "/etc/ld.so.preload" then permit
linux-fsread: filename eq "/etc/ld.so.cache" then permit
```

第一行定义了策略所应用的文件（在本例中为 `/bin/login`）以及使用的仿真模式。目前支持 `native`（针对 `OpenBSD`）和 `linux`；自然地我们需要后者。策略文件的其余行是单独的规则，其形式为：
```
<emulation type>-<system call>: <action> [log]
```

为了更具灵活性，还可以进行比较：
```
<emulation type>-<system call>: <term 1> ! <comparison operator> <term 2> then <action> [log]
```

其中 `action` 为 `permit`、`ask` 或 `deny`。因为未显式允许的操作将被自动拒绝，因此 `deny` 动作的价值有限。

# 比较
比较运算符允许你匹配传递给系统调用的参数。考虑规则：
```
linux-bind: permit
```

这允许进程绑定到 `TCP/IP` 端口。更好的做法是仅允许绑定到特定地址。以下是改进版本：
```
linux-bind: sockaddr eq "*inet-[0.0.0.0]:22" then permit
```

对于系统调用匹配的属性列表，请参阅手册页（例如 `man bind`）。可以使用以下比较运算符：

- `match`: 允许基本通配符，例如 `"/bin*"`
- `eq`: 两个项相等，例如 `filename "/bin/sh"`
- `ne`: 两个项不等。
