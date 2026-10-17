
## 创建组

该组将被创建，并根据 Red Hat Linux 7.1 `groupadd` 手页中的以下规则分配一个新的用户数字：“默认使用大于 500 且大于其他所有组的最小 ID 值。” 若干 Linux 发行版默认会将新用户添加到 `users` 组 (`100`)。

如果你想指定组号，只需使用 `-g` 标志来指示该数字：

```bash
# groupadd -g 503 groupname
```

这会在 `/etc/group` 中产生一个类似于下面的条目：

```
groupname::503:
```

该条目显示了一个具有指定名称和组 ID 的空组。

> **提示**：如果你不记得想要哪个组，现有的组 ID 存储在 `/etc/group` 文件中。

## 将用户添加到组

遗憾的是，没有标准的程序可以方便地将用户添加到组。要实现这一点，最简单的方法是直接编辑 `/etc/group` 文件。该文件的每一行代表一个组的定义，格式如下：

```
groupname::password:groupid:userlist
```

该行的组成部分如下：

- 组条目是组名。
- 密码条目代表组的密码；通常密码不应用于组，因此此条目通常为空。
- `groupid` 是该组的数字 ID，对于该组来说应该是唯一的。
- `userlist` 条目是属于该组的用户逗号分隔列表。例如，如果 `user1`、`user2` 和 `user3` 都属于组 ID 为 `505` 的 `group1` 组，则该组的条目看起来像是：

```
group1::505:user1,user2,user3
```

如果你想将用户添加到现有组，只需使用你喜欢的文本编辑器编辑 `/etc/group` 文件并添加用户名即可。

## 删除组

通过 `groupdel` 命令实现删除。该命令非常简单；没有可用的标志或选项。只需将组名作为参数提供即可：

```bash
# /usr/sbin/groupdel groupname
```

尽管它非常简单，但有一些注意事项：

- 组必须是空的才能删除。
- 如果该组是用户的主组（在密码文件中指定），则无法删除。

这留下了另一个问题：如果该用户在系统的其他地方拥有需要删除的文件怎么办？这可以通过在删除用户后使用 `find` 命令来实现。为了执行此操作，请在删除用户之前从 `/etc/passwd` 文件中记录用户的 ID，然后使用 `find` 命令：

```bash
# find / -type f -uid 503 -print -exec rm {} \;
```

此命令将找到属于该用户的文件并使用 `rm` 命令删除它们（注：原文此处描述有误，`find` 命令本身不改变所有权，`chgrp` 用于改变组所有权，但配合 `-delete` 或 `-exec rm` 用于删除文件。根据上下文“删除文件”，保留命令意图，修正末尾缺失的分号 `\;`）。

## 系统启动

对于许多用户（而非管理员）来说，一个神秘领域是屏幕上闪烁的启动序列。启动消息保存在系统日志 `/var/log/dmesg` 中。日志文件将在后文中讨论。

## 启动期间发生了什么？

启动周期比启动信息显示的要简单得多。简单来说，启动过程有两个阶段：

- **引导内核**：在此阶段，内核加载到内存并在初始化每个设备驱动时打印消息。
- **执行 `init` 程序**：在内核加载和初始化完成后，`init` 程序运行。它处理所有程序的启动，包括基本系统守护进程和其他指定加载的软件。

## `init` 程序

本节将详细查看 `init` 程序，因为在这里你可以轻松地自定义启动周期期间加载的程序。`init` 的工作是启动新进程并在它们退出时重启它们。一个完美的例子是提供虚拟登录控制台的进程集。在 Linux 系统上，初始加载六个此类进程。当你退出控制台窗口时，该进程结束，`init` 会启动一个新的，以保持六个控制台始终可用。

控制 `init` 程序运行的规则存储在 `/etc/inittab` 文件中。Red Hat Linux 7.1 的默认 `/etc/inittab` 文件如下：

```
# inittab
此文件描述了 INIT 进程如何在特定的运行级别设置系统。
# 由 Marc Ewing 和 Donnie Barnes 修改自 RHS Linux

默认运行级别。RHS 使用的运行级别：
# 0 - 停止（不要将默认级别设置为此）
# 1 - 单用户模式
# 2 - 多用户、无 NFS（如果没有网络，与 3 相同）
# 3 - 全多用户模式
# 4 - 未使用
# 5 - X11
# 6 - 重启（不要将默认级别设置为此）

id:3:initdefault:

# 系统初始化
si::sysinit:/etc/rc.d/rc.sysinit

1:0:wait:/etc/rc.d/rc 0
1:1:wait:/etc/rc.d/rc 1
1:2:wait:/etc/rc.d/rc 2
1:3:wait:/etc/rc.d/rc 3
1:4:wait:/etc/rc.d/rc 4
1:5:wait:/etc/rc.d/rc 5
1:6:wait:/etc/rc.d/rc 6

# 在每个运行级别下运行的任务
once::/sbin/update

# 捕获 CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# 当我们的 UPS 告诉我们电源故障时，假设我们还有剩余电。
# 安排在 2 分钟后关机。
# 当然，这假设你已经安装了电源并且你的
# UPS 连接并正常工作。
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure, System Shutting Down"

# 如果电源在关机生效之前恢复，则取消它。
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# 在标准运行级别运行 getty
1:2345:respawn:/sbin/getty 38400 tty1
2:2345:respawn:/sbin/getty 38400 tty2
3:2345:respawn:/sbin/getty 38400 tty3
4:2345:respawn:/sbin/getty 38400 tty4
5:2345:respawn:/sbin/getty 38400 tty5
6:2345:respawn:/sbin/getty 38400 tty6

# 在运行级别 5 下运行 xdm
# xdm 现在是一个独立的服务
x:5:respawn:/usr/bin/X11/xdm-nodaemon
```

虽然学习如何编写自己的 `initab` 文件并不重要，但理解这个文件在告诉我们什么是有用的：

Linux 有一套运行级别（run levels）系统。运行级别是一个数字，标识系统的当前状态以及 `init` 应该在该系统中运行并保持运行的进程。在 `initab` 文件中，第一条目 `id:3:initdefault` 指定了启动时加载的默认运行级别。在之前的示例中，它是多用户控制台模式，运行级别为 `3`。然后 `initab` 文件中的每个条目都指定了它适用于哪个运行级别（位于条目的第二个字段，每个字段由列分隔）。因此，对于运行级别 `3`，以下行是相关的：

```
1:3:wait:/etc/rc.d/rc 3
1:2345:respawn:/sbin/getty 38400 tty1
2:2345:respawn:/sbin/getty 38400 tty2
3:2345:respawn:/sbin/getty 38400 tty3
4:2345:respawn:/sbin/getty 38400 tty4
5:2345:respawn:/sbin/getty 38400 tty5
6:2345:respawn:/sbin/getty 38400 tty6
```

第一行运行启动脚本 `/etc/rc.d/rc 3`。这将运行目录 `/etc/rc.d/rc3.d` 中包含的所有脚本。这些脚本代表系统初始化时需要启动的程序，例如 `sendmail`、`PCMCIA` 服务、打印机守护进程和 `cron`。通常情况下，你不想编辑或更改这些脚本；它们是系统的默认值。最后六行设置了 Linux 提供的六个终端。

### 注意

需要注意的是，`rc3.d` 目录中最后执行的脚本将是 `S99local` 脚本。该脚本实际上是文件 `/etc/rc.d/rc.local` 的链接；你可以在这里放置你想在启动时运行的自定义启动程序。

在其他 Linux 系统上，`/etc/inittab` 的结构可能会不同，`/etc/rc.d` 目录的组织也是如此。但在所有系统中，`/etc/rc.d/rc.local` 文件代表了可以在其中添加自定义启动命令的文件。

## 使用 `rc.local` 文件

默认的 Red Hat Linux 7.1 `rc.local` 文件只设置了登录提示，没有其他内容：

```bash
#!/bin/sh
# 此脚本将在所有其他 init 脚本之后执行。
# 如果你不想执行完整的 Sys V 风格初始化操作，
# 你可以把初始化内容放在这里。
```
