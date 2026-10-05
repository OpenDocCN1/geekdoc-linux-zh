

## 第 3 章 运行 Sendmail

从 linuxconf 窗口左侧的菜单中，选择 Control ➤ Panel ➤ Service Activity。窗口右侧会出现一个服务列表；这与 ntsys 显示的服务列表相同。同样，使用 ntsys 时，你不需要担心运行级别（runlevels）。只需通过选择 sendmail 条目旁相应的按钮来启用或禁用 sendmail 脚本即可。

## 使用 chkconfig 启用 Sendmail

另一个可用于控制启动时运行脚本的工具是 chkconfig。这是一个基于 Silicon Graphics IRI 版本 Unix 中的 chkconfig 程序的命令行工具。Linux 版本对其进行了一些增强，例如能够控制脚本运行的运行级别。`chkconfig` 命令的 `--list` 选项可以显示当前设置：

```
[chkconfig] --list sendmail
sendmail 0:off 1:off 2:on 3:on 4:on 5:off 6:off
```

要为特定的运行级别启用或禁用脚本，请使用 `--level` 选项指定运行级别，随后输入想要控制的脚本名称以及你想要执行的操作（使用 `on` 启用脚本或使用 `off` 禁用）。例如，要禁用运行级别 2 的 sendmail，请输入列表 3.3 所示的命令。

## 3.3 使用 chkconfig 控制 Sendmail

```
[root]#chkconfig --level 2 sendmail off
[root]#chkconfig --list sendmail
sendmail 0:off 1:off 2:off 3:on 4:on 5:off 6:off
```

## 手动运行启动脚本

之前的章节讨论了实现本质相同操作的不同方法——在启动时启用或禁用 Sendmail。所有这些方法都是有效的。请选择与你正在运行的 Linux 版本兼容且符合你喜好的方法。记住，大多数情况下，你会在初始系统配置期间安装并启用 Sendmail，并且永远不需要调整启动文件。

你更有可能需要停止或重启已经在系统中运行的 Sendmail 进程。在许多系统中，这可以通过手动调用启动脚本来实现。Red Hat 系统上的 sendmail 启动脚本接受五个参数：

- stop 终止当前的 Sendmail 守护进程。
- start 如果当前没有正在运行，则启动一个新的 Sendmail 守护进程。
- restart 终止当前的 Sendmail 守护进程并启动一个新的。该命令的替代名称是 reload。
- condrestart 先检查 Sendmail 是否正在运行。如果正在运行，则终止当前的 Sendmail 守护进程并启动一个新的。如果 Sendmail 当前未运行，则启动 Sendmail。
- status 显示当前 Sendmail 守护进程的进程 ID（PID）。

列表 3.4 是在 Red Hat 系统上重启 Sendmail 守护进程的示例。

## 列表 3.4 使用通用启动脚本重启 Sendmail

```
[root]# /etc/rc/init.d/sendmail restart
Shutting down sendmail: [ OK ]
Starting sendmail: [ OK ]
```

> 注意：如果你运行的是 Red Hat 6.0 或更高版本，指定 sendmail 启动脚本全路径的替代方案是输入 `service sendmail restart`。在其他版本的 Red Hat 上，请使用路径名。

启动脚本的主要局限性是 Sendmail 守护进程仅带有 `-bd` 和 `-q` 选项运行。这在 99% 的情况下都是正确的。在某些情况下需要额外的命令行参数。如果是为了测试，从命令行重启 Sendmail 就足够简单了。如果你在每次启动都需要额外的命令行参数，唯一的选择是编辑启动脚本或创建自己的启动脚本以包含你需要的参数。请参阅附录 B“Sendmail 命令”，获取可用 sendmail 命令的许多命令行参数的完整列表和说明。

## 使用信号控制 Sendmail

并不是每个 Linux 都有一个可用于停止、启动和重启 Sendmail 的系统。但在所有系统中，都可以通过信号控制 Sendmail。Sendmail 进程处理三种信号。嗯，如果你算上 SIGTERM 终止 Sendmail 就像终止其他进程一样的话——但有三个信号具有特定含义。这三个是：

- SIGHUP SIGHUP 信号调用 Sendmail 守护进程重启并重新读取其配置文件。SIGHUP 最常见的用途是在配置文件更新后强制 Sendmail 重新加载配置。SIGHUP 甚至可以用于在 Sendmail 程序更新后终止当前的副本 副本并运行新副本，因为 SIGHUP 会导致真正的重启，而不仅仅是重新读取配置文件。
- SIGINT SIGINT 信号导致 Sendmail 优雅关闭。当 Sendmail 接收到 SIGINT 时，如果它正在处理队列，它将移除锁文件，切换到启动时使用的用户 ID 以创建一个干净的日志条目，然后无错误退出。和大多数进程一样，Sendmail 可以被 kill 信号 SIGTERM 终止。然而，SIGINT 是关闭 Sendmail 更干净的方法，与 SIGTERM 不同，SIGINT 不会留下未解决的日志条目或使用的锁文件。
- SIGUSR1 使用 SIGUSR1 信号让 Sendmail 通过 syslog 输出其当前状态。Sendmail 日志的细节在第12章“测试安全性”中介绍。目前，理解这些就足够。

## 列表 3.5 使用通用启动脚本重启 Sendmail

```
[root]# ps -ax | grep sendmail
sendmail 0:off 1:off 2:on 3:on 4:on 5:off 6:off
```

