
`kill [-s signal] pid[...]`

你可以通过信号名称或数字传递信号；例如，`kill -s 6940` 和 `kill -SIGKILL 6940` 是等效的。你也可以省略 `-s` 并在信号名称或数字前加上连字符，如 `kill -SIGKILL 6940`。当你传递信号名称时，是否包含 `SIG` 部分是可选的；例如，`KILL` 和 `SIGKILL` 是等效的。在实践中，你有时需要发送 `SIG` 部分。如果你不传递任何信号，`kill` 将使用 `SIGTERM`——并非所有进程都会响应所有信号。如果进程未能响应信号，它将直接终止，就像通过了 `SIGTERM` 信号一样。

如果一个进程失去了控制（例如，它没有响应且消耗了过多的 CPU 时间），你正在杀死它。通常最好的做法是先尝试 `SIGTERM`（这是默认信号），但 `kill pid` 是通常的第一步。失控的程序通常会响应这个礼貌的关闭请求，但你可能需要采取更强硬的手段。你可以通过发送 `SIGKILL` 来实现这一点，进程无法忽略该信号。只有 `root` 用户或进程所有者可以终止它。

`kill` 的一个问题是你需要一个 PID。你可以通过 `ps` 或类似的工具找到进程的 PID。如果你知道某个进程已经失控，例如，你可以使用命令 `ps -C crunch` 来定位 `crunch` 的 PID。某些守护进程还将它们的 PID 存储在文件中，通常是为了 SysV 启动脚本的需要。这些文件通常位于 `/var/run`，并以它们所指的进程命名，文件名以 `.pid` 结尾。例如，`/var/run/crond.pid` 持有 `cron` 的 PID。遗憾的是，有时同一个计算机上运行着多个相同的程序实例，因此隔离你想要杀死的进程可能很困难。你可能可以使用许多 `ps` 选项所报告的用户 ID 来缩小范围。如果程序正在消耗大量的 CPU 时间，它可能会出现在显示列表的顶端。

### 杀死不需要的进程 299

如果你确定某个程序只运行了一个实例，并且知道进程名称，你可以使用 `killall` 代替 `kill`。该程序的工作原理与 `kill` 相同，但你传递给它的是程序名称而不是 PID，且 `killall` 会杀死指定程序的所有运行实例。例如，`killall crunch` 会杀死所有 `crunch` 进程。警告：`killall` 会杀死所有运行的 `crunch` 进程。由于 Linux 是类 Unix 系统，可以使用 `killall` 代替 `kill`。

### 额外的进程工具

在 Linux 中可以使用以下工具来管理进程：

- [top](https://man.linux.org/man-pages/fed8/man1/top.1.html) 实时查看系统资源消耗
- [ps](https://man.linux.org/man-pages/fed8/man1/ps.1.html) 报告当前进程快照
- [htop](https://man.linux.org/man-pages/fed8/man1/htop.1.html) 更加直观的交互式进程管理器
- [vmstat](https://man.linux.org/man-pages/fed8/man1/vmstat.1.html) 报告内核、内存和进程统计
- [strace](https://man.linux.org/man-pages/fed8/man1/strace.1.html) 跟踪进程的系统调用
- [lsof](https://man.linux.org/man-pages/fed8/man1/lsof.1.html) 列出进程打开的所有文件
- [fstat](https://man.linux.org/man-pages/fed8/man1/fstat.1.html) 获取文件系统状态信息
- [iotop](https://man.linux.org/man-pages/fed8/man1/iotop.1.html) 监控进程的 I/O 使用率
- [killall](https://man.linux.org/man-pages/fed8/man1/killall.1.html) 根据名称杀死所有匹配的进程

### 总结

- `kill` 命令用于向进程发送信号。
- `SIGTERM` 是默认信号，用于礼貌地终止进程。
- `SIGKILL` 强制终止进程，进程无法忽略。
- 你可以通过 PID 或信号名称来操作进程。
- `killall` 允许根据进程名称杀死所有实例。
- 使用 `ps` 工具可以查找 PID。
- 某些守护进程会在 `/var/run` 下存储 PID 文件。

# 第 15 章

## 创建自定义内核

内核是 Linux 系统的核心。内核是一个程序，但它是一个特殊的程序。它作为程序与硬件之间的接口，分配 CPU 时间、划分内存、管理文件系统并在其他方面控制计算机。这些任务非常基础且至关重要，因此正确配置内核至关重要。

注意：严格来说，Linux 指的是内核。Linux 系统中的其他部分——如 Shell、服务器、窗口系统、打印软件等——在 FreeBSD 甚至 Windows 上可用。因此，有些人反对使用 Linux 来指的是整个操作系统。有些人将整个操作系统称为 GNU/Linux。

由于 Linux 是开源操作系统，系统管理员可以自定义内核。你可以包含或省略特定的驱动、更改内核组件的编译选项，甚至针对特定的 CPU 进行优化。了解这些操作将使你能够提高系统性能。本章涵盖了相关主题，从如何获取内核开始，接着介绍了用于修改内核配置的工具。接下来是对可用内核选项的概述，然后是对某些特定内核性能优化选项的深入探讨。最后，本章介绍了在配置后如何编译和安装内核。

## 获取内核

所有 Linux 发行版都带有一个二进制内核（或多个内核），并经过不同的优化。在大多数情况下，你可以使用发行版提供的内核代码，这样做有某些优点。发行版提供有时会应用内核补丁——这些代码不是原始程序的一部分，但改进或扩展了它。你的系统可能依赖此类补丁来运行或提供某些功能，例如某些特殊硬件的驱动程序。另一方面，发行版提供的源代码可能会由于某些原因产生问题。补丁可能包含官方内核源码中不存在的 Bug，如果你向他人寻求帮助，而问题与补丁有关，可能会引起困惑。

我倾向于使用未经修改的 Linux 内核源码。你可以从 `http://www.kernel.org` 或其镜像获取这些代码；点击链接进入存档区域并下载包。你应该下载一个文件名名为 `linux-a.b.c.tar.bz2` 或 `linux-a.b.c.tar.gz` 的文件。根据扩展名，该文件包含了使用 bzip2 或 gzip 压缩的 a.b.c 版本内核源码。侧边栏的“内核版本编号”描述了 Linux 内核是如何命名的。

鉴于内核的重要性，你可能想使用 `gpg` 工具验证其完整性。要做到这一点，你必须随内核一起下载一个签名文件。该文件与内核文件名相同，但扩展名为 `.sign`。当你下载了内核及其签名文件后，尝试执行以下命令：

```bash
$ gpg --keyserver wwwkeys.org --recv-keys 0x517DF0FE

gpg keyring:/home/rodmith/.gnupg/securing.gpg created

gpg :/home/rodmith/.gnupg/trustdb created
```
