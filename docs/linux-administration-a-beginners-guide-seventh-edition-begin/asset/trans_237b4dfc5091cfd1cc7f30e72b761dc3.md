

## 第15 章 网络安全 411

- 如果我们需要某项服务，默认设置是安全的吗？这个问题也可以帮助消除某些服务——如果它们不安全且无法使其变得安全，那么它们很有可能应该被移除。例如，如果启用了远程登录 Telnet 服务来提供该功能，则应该使用如 SSH 这样的替代方案，因为 Telnet 无法在网络上对登录信息进行加密。（默认情况下，大多数 Linux 发行版出厂时禁用了 Telnet 并启用了 SSH）。

- 提供服务的软件需要更新吗？所有软件都需要不时更新，例如 Web 服务器和 FTP 服务器。这在一定是因为随着新功能的添加，新的安全/漏洞问题也会随之而来。务必记住跟踪服务器的开发，并在必要时获取更新。

## 关闭 xinetd 和 inetd 服务

要关闭通过 xinetd 程序启动的服务，只需编辑位于 `/etc/xinetd/` 目录下的 `servicess` 文件，并将 `disable` 的值设置为 `Yes`。

对于传统的基于 System V 的服务，你也可以使用 `chkconfig` 命令来禁用由 xinetd 管理的服务。例如，要禁用 echo 服务，你需要运行：

```
root@server ~]# chkconfig echo off
```

在运行 system 的 Linux 发行版上（如 Fedora/CentOS/RHEL），你也可以选择性使用 `systemctl` 禁用服务。例如，要禁用 xinetd 服务，请使用以下命令：

```
root@fedora-server ~]# systemctl disable xinetd
```

在基于 Debian 的系统（如 Ubuntu）上，你可以使用 `sysv-rc-conf` 命令（如果没有安装，请使用 `apt-get` 命令安装）来实现相同的效果。例如，在 Ubuntu 中禁用 echo 服务，你可以运行：

```
master@ubuntu-server:-$ sysv-rc-conf echo off
```

> 提示：在仍然使用 `inetd` 超级守护进程的其他 Linux 发行版上，你应该编辑 `/etc/inetd.conf` 文件并注释掉你不再需要的服务。要禁用服务，在行开头加井号 (`#`)。（有关 `xinetd` 和 `inetd` 的更多信息请参见第 8 章）。在对 `/etc/inetd.conf` 文件进行任何更改后，记得向 `inetd` 发送 HUP 信号，并发送 SIGUSR2 信号以重启 `xinetd`。如果你正在使用 Fedora（或类似的）发行版，还可以使用以下命令重新加载 `xinetd`：

```
root@server ~]# /etc/rc.d/init.d/xinetd reload
```

![](img/9f6657924397c33f088db5321b751a83_430_0.png)

## 关闭非 xinetd 服务

如果服务未由 xinetd 管理，那么有一个在引导启动时启动的独立进程或脚本正在运行。如果该服务是由你的发行版安装的，且你的发行版提供了一个禁用服务的易用工具，你可能会发现这是最简单的方法。

例如，某些 Linux 发行版支持 `chkconfig` 程序，它提供了一种启用和禁用单个服务的简单方法。例如，在这些系统上，要禁用 `rpcbind` 服务在运行级别 3 和 5 启动，请使用以下命令：

```
[root@server ~]# chkconfig --level 35 rpcbind off
```

参数 `--level` 指受此更改影响的运行级别。由于运行级别 3 和 5 代表两个多用户模式，我们选择了了这些级别。`rpcbind` 参数是 `/etc/init.d/` 目录中涉及的服务名称。最后，最后一个参数可以设置为 `on`、`off` 或 `reset`。`on` 和 `off` 选项是言而易明的。`reset` 选项是指将服务重置为其原始状态。

如果你想再次开启 `rpcbind` 服务，只需运行：

```
[root@server ~]# chkconfig --level 35 rpcbind on
```

注意，`chkconfig` 实际上不会真正开启或关闭已经运行的服务；相反，它定义了下一次启动时会发生什么。要停止进程，请使用 `/etc/init.d/` 目录中的控制脚本。在 `rpcbind` 的情况下，你通过以下命令停止它：

```
[root@server ~]# /etc/init.d/rpcbind stop
```

在运行 `systemd` 的 Linux 发行版（如 Fedora）上，你也可以使用 `systemctl` 命令停止服务。例如，要停止 `rpcbind` 服务，输入：

```
[root@fedora-server ~]# systemctl stop rpcbind.service
```

同样，要永久禁用 `rpcbind` 单元从下次系统启动时启动，使用 `systemctl` 工具，输入：

```
[root@fedora-server ~]# systemctl disable rpcbind.service
```

## 监控你的系统

执行监控的免费开源商业级应用程序非常值得尝试。在这里，我们将查看各种有助于系统监控的优秀工具。其中某些工具已安装在你的 Linux 发行版中；另一些没有。它们都是免费且易于获取的。

## 充分利用 syslog

在第 8 章中，我们探索了系统日志记录 `rsyslogd` 以及 `systemd-journal` (journal)，它们都有助于管理和收集来自各种程序的日志消息。现在，你可能已经见过通过 `rsyslog` 获取的日志消息类型，并且玩过 `journalctl` 工具。这些包括与安全相关的消息。

