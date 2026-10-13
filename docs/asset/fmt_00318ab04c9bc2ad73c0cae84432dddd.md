
```
fuser /var/admin/messages
```

其输出看起来像这样

```
/var/admin/messages: 434
```

> 在过去，`fuser` 用于查看系统管理员想要卸载的文件系统上有哪些进程打开了文件。要列出在 `/usr` 上打开文件的进程，请使用命令 `fuser -m /usr`

你可以使用我们新的 `pp` 脚本以此识别该进程：

```
pp 434
```

典型输出将是：

```
F UID PID PPID PRI NI SIZE RSS WCHAN STAT TTY TIME COMMAND
040 0 434 0 0 0 0 0
```

在这种情况下，忽略你不在乎的 `demuxprotrej` 警告。可以使用额外的 `grep` 命令来搜索或忽略额外项目。请记住，破解者可以像你一样使用 `crontabs`。虽然我没听说过有人这样做，但破解者可以使用 `crontab` 条目定期调用木马程序。除非研究 `crontab` 条目，否则大多数时间很难检测到有恶意进程在运行。即使为了此目的调用一个标准程序，搜索木马程序也将一无所获。当然，这是 Tripwire 的工作。

## 16.1 监控活动（继续）

可以通过调用 `telnet` 并传入第二个参数（即数字端口号或其在 `/etc/services` 中的符号名称）来轻松测试 TCP 服务。这些 DTC 服务中的将会超时。超时值是可配置的，但通常为 30 秒。要查看端口 365 上的 `dtk` 服务的功能，请查看此命令：

```
telnet yours.pentacorp.com dtk
```

如果你在运行 `Configure /log` 时选择普通日志，它将包含所有客户端输入的命令，就像它们的初始连接一样。此外，在 `/IP/` 下将为每个尝试访问服务的客户端系统唯一 IP 生成一个日志文件。这些日志文件的名称是点四分位表示法中的数字 IP 地址，例如：

```
/dtk/log/192.168.43.184
```

`/dtk/README` 文件解释了 `/default` 下状态描述文件的格式和用法。它阐述了如何配置状态机，使得某些地址获得真实服务，而其他地址获得欺骗服务。此外，它还解释了如何运行另一个进程，例如使用 `blockip` 通过 Adaptive-TCP Wrappers 锁定系统。后者在第 559 页的《自适应防火墙：使用破解陷阱增强防御》中进行了详细讨论。

## killall -HUP inetd

可以通过调用 `telnet` 并传入第二个参数（即数字端口号或其在 `/etc/services` 中的符号名称）来轻松测试 TCP 服务。这些 DTC 服务中的将会超时。超时值是可配置的，但通常为 30 秒。要查看端口 365 上的 `dtk` 服务的功能，请查看此命令：

```
telnet yours.pentacorp.com dtk
```

如果你在运行 `Configure /log` 时选择普通日志，它将包含所有客户端输入的命令，就像它们的初始连接一样。此外，在 `/IP/` 下将为每个尝试访问服务的客户端系统唯一 IP 生成一个日志文件。这些日志文件的名称是点四分位表示法中的数字 IP 地址，例如：

```
/dtk/log/192.168.43.184
```

`/dtk/README` 文件解释了 `/default` 下状态描述文件的格式和用法。

## 16.15 监控进程

几乎每个人都知道使用 `ps` 列出进程状态以查看系统上运行着哪些程序。典型的调用方式是

```
ps -axlw | more
```

花时间仔细阅读其运行的手页绝对值得的。`SIZE` 字段列出以 KB 为单位的大小。某些内存页可能会被交换到“交换空间”。`RSS` 是驻留集大小（Resident Set Size），这表示程序留在内存中的部分，以 KB 为单位。

了解这些值对于你的系统守护进程和 Netscape 等常用程序的典型取值是有帮助的。你甚至可以每天存储一次 `ps` 用的输出。这可能让你识别出破解者是否因为大小错误而安装了这些程序之一的木马版本。

通常，通过 `grep` 过滤 `ps` 的输出来寻找匹配特定 UID、程序名或 tty 设备进程是有帮助的。以下脚本多年一直是我喜欢的工具，可以轻松地实现这一点；感谢 David Barker 的创建。它被称为 `pp`。

```
/bin/echo \
" F UID PID PPID PRI NI SIZE RSS WCHAN STAT TTY TIME COMMAND": \
/bin/ps -axlw|/bin/grep -i $1|/bin/grep -v -w 'grep' \
|/bin/grep -v -w 'pp') | /bin/more
```

要为指定的 PID（例如 1701）获取 `pp` 输出，可以执行命令：

```
pp 1701
```

除了 `ps` 之外，`top` 程序非常有有用。它提供了最活跃进程的动态更新视图，通常对于发现异常操作非常有帮助。通过输入 "u" 命令然后输入账户名，可以将显示限制为单个账户的进程。

`fuser` 程序将列出使用指定文件、文件系统或网络端口的进程。它可以用于确定哪些进程正在对可疑文件进行 I/O。之前讨论的 `pp` 脚本随后可以找到这些极可疑进程的父进程。以下命令将列出任何当前打开了 `/var/admin/messages` 的进程 PID：

```
fuser /var/admin/messages
```

其输出看起来像这样

```
/var/admin/messages: 434
```

> 在过去，`fuser` 用于查看系统管理员想要卸载的文件系统上有哪些进程打开了文件。要列出在 `/usr` 上打开文件的进程，请使用命令 `fuser -m /usr`

你可以使用我们新的 `pp` 脚本以此识别该进程：

```
pp 434
```

典型输出将是：

```
F UID PID PPID PRI NI SIZE RSS WCHAN STAT TTY TIME COMMAND
040 0 434 0 0 0 0 0
```

## 16.16 Cron: 监控破解者

`cron` 功能对于定期执行系统管理员检测系统问题所需的各种分析非常有帮助。对日志文件进行定期分析是一个极佳的主意。`root` `crontab` 条目是说明性的（要使用此项，你需要删除换行符）。

```
0 9 * * /bin/grep -v demuxprotrej:/var/adm/secure \ | tail -500 | mailix -s '\research.pentacorp security report' bob@pentacorp.com
```
