
## 第 9 章：系统日志、监控与自动化

### 步骤 1. 编辑 `/etc/sysconfig/syslog` 文件以包含 `-r` 选项：

```bash
# nano /etc/sysconfig/syslog
# 禁用 syslog 的选项
# -m 禁用'MARK'消息
# -r 启用远程日志
# 详情见 syslog(8)
```

### 步骤 2. 保存文件并重启 syslog 服务：

```bash
# service syslog restart
Shutting down system logger:      [ OK ]
Starting system logger:             [ OK ]
```

## 系统性能

每当运行一个程序或命令时，都会为其创建一个进程。这些进程都是唯一的，并通过分配给它的进程标识（`PID`）进行标识。系统进程对于保持系统运行或为客户端提供服务至关重要。进程管理有助于保持系统稳定，或在系统不稳定时提供帮助。以下是你可以使用的一些进程命令：

- `ps` 显示运行中进程的信息
- `kill` 终止进程
- `pgrep` 根据 PID 查找进程
- `pidof` 显示与某个服务或命令相关的所有进程
- `top` 监控系统资源（类似于 Windows 中的任务管理器）
- `renice` 调整特定进程的优先级

让我们首先通过 `ps` 命令查看当前 root 用户当前拥有的进程：

```bash
# ps
PID TTY TIME CMD
4474 pts/3 00:00:00 bash
4506 pts/3 00:00:00 ps
```

`ps` 命令包含许多选项，用于生成不同类型的输出，包括查看当前系统上运行的进程。

要查看带有更详细信息的进程，可以使用以下命令：

```bash
# ps aux
USER PID %CPU MEM VSZ RSS TTY STAT TIME COMMAND
root 2387 0.0 0.1 1660 424 tty Ss+ 07:30 0:00 /bin/mintty tty1
root 2388 0.0 0.1 1660 420 tty Ss+ 07:30 0:00 /bin/mintty tty2
root 2389 0.0 0.1 1660 428 tty Ss+ 07:30 0:00 /bin/mintty tty3
root 2398 0.0 0.1 1660 428 tty Ss+ 07:30 0:00 /bin/mintty tty4
root 2391 0.0 0.1 1660 448 tty S+ 07:30 0:00 /bin/mintty tty5
root 2392 0.0 0.1 1660 420 tty Ss+ 07:30 0:00 /bin/mintty tty6
```

在这里，我们不仅使用了 `PID`，还使用了 CPU 和内存利用率。我在使用 `ps` 命令时，常用的一组组合是结合 `grep` 命令使用，以过滤掉我不感兴趣的内容。这样，我就可以获取特定进程的详细信息。假设你想查看与 SSH 服务相关的任何进程可用信息：

```bash
# ps aux
root 4286 0.0 0.1 62616 1216 ? Ss Sep23 0:00 /usr/sbin/sshd
root 15872 0.0 0.3 90116 3248 ? S 10:06 0:00 sshd: user0 [priv]
user0 15874 0.0 0.0 90116 1740 ? S 10:06 0:00 sshd: user0@pts/0
user0 15921 0.0 0.0 61176 728 pts/0 R+ 10:14 0:00 grep ssh
```

然而，使用此命令，你将收到 59 行输出，你必须从中筛选才能找到实际需要的 4 行。你可以看到缩小输出范围是很有帮助的。

让我们也看看 `ps` 命令提供的其他选项：

```bash
$ ps --help
********** 简单选择 ********* 按列表选择 ******
-A 所有进程
-C 按命令名选择
-N 取反选择
-a w/ tty 排除会话首进程
-d 除会话首进程以外的所有进程
-e 所有进程
-T 此终端上的所有进程
-a w/ tty，包括其他用户
-g 已用 - 不要使用
-r 仅限运行中的进程
-x 进程/o 控制 tty
*** 输出格式 **********
-o, 用户定义 -f 完整格式
-j, 作业控制 s 信号
-o, 预加载 -o 虚拟内存
-l, 详细 u 用户导向
-f 额外数据 x 寄存器
*** 错误选项 **********
-G 按实际组 ID 选择（支持名称）
-U 按实际用户选择（支持名称）
-g 按会话或有效组名选择
-p 按进程 ID 选择
-s 指定会话中的进程
-t 按 tty 选择
-u 按有效用户选择（支持名称）
-U 指定用户的进程
-t 按 tty 选择
长选项 **********
--Group --User --cols --ppid
--group --user --sid --rows --info
--cumulative --format --deselect
--tty --forest --version
--heading --no-heading --context
-V,V 显示版本 L 列表代码 f ASCII 艺术树 forest
-m,L,-T,H 线程 S 子进程在 yum -y 更改格式
-M,Z 安全数据 c true 命令名 -c 调度类
-w,w 宽输出 n 数字 WCHAN,UID -H 进程层次结构
```

你可以看到有许多输出格式和排序功能。了解如何操作 `ps` 命令的输出以及你正在寻找的内容，对于在考试中故障排除非常有帮助，在现实世界中的故障排除中也起着巨大作用。

如果你系统上的某个进程失控了会怎样？在这种情况下，你可以使用 `kill` 命令来终止进程，即使它没有响应（也称为失控进程）。然而，要使用 `kill` 命令，你需要知道要杀死的进程的 `PID`。语法：`kill PID`

如果你想在 SSH 服务无响应时停止它，你只需要查找与 daemon 关联的 `PID`。如果你查看输出，可以看到这个 `PID` 4286。要强制杀死该进程，请执行：

```bash
# kill 4286
```

有时 `kill` 命令没有按预期工作，请带有 `-9` 选项来赋予其优先级：

```bash
# kill -9 4286
```

如果你不知道要终止的进程的 `PID` 怎么办？你如何从 `ps` 命令的输出中查找？实际上有两个命令可以确定服务的 `PID`：`pid` 和 `pgrep`。首先，使用 `pid` 找到属于 SSH 的 `PID`：

```bash
# pid ssh
4286
15872
5874
```

为了获得相同但更易读的格式，你可以使用 `pgrep`：

```bash
# pgrep ssh
4286
15872
5874
```

知道运行了多少进程是好事，但如果你需要知道特定进程占用了多少资源呢？让我们看看 `top`。此命令提供了系统进程的概述、内存使用情况和 CPU 利用率。要检查系统整体情况，执行以下命令获得与图 9-1 类似的结果：
