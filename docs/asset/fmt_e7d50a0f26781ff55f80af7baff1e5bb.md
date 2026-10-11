
| 6 | 重启 (Reboot) | 用于重启系统的特殊运行级别 |

> 由于 `init` 守护进程负责启动和停止守护进程，因此，更改运行级别的操作通常被称为 `initstates`。

# 第 8 章 系统初始化、X Windows 与本地化

要查看系统当前的运行级别和之前的运行级别（如果自系统设置以来运行级别发生了变化），你可以使用 `runlevel` 命令，如下所示的输出：

```
[root@server1 ~]# runlevel
N 5
[root@server1 ~]#
```

之前的 `runlevel` 命令表示系统处于运行级别 5，而在进入此运行级别之前的最近一个运行级别不存在（N）。

要更改运行中系统的运行级别，你只需要指定 `init` 命令后跟新的运行级别；若要从运行级别 5 更改到运行级别 1，你可以使用以下命令：

```
[root@server1 ~]# runlevel
N 5
[root@server1 ~]# init 1
```

*系统在进入单用户模式时 `init` 守护进程正在停止的守护进程列表。*

告诉 `INIT` 进入单用户模式。

```
[root@server1 /]#
[root@server1 /]# runlevel
5 1
[root@server1 /]#
```

> 注意
>
> 在更改运行级别时，可以使用 `telinit` 命令代替 `init` 命令。因此，可以使用 `init 1` 切换到单用户模式。

还可以从引导加载程序向 Linux 内核传递选项，以强制系统引导到特定级别。如果你在 GRUB Legacy 或 GRUB2 配置屏幕的内核行中附加关键字 `single`，你将引导到单用户模式。

## /etc/inittab 文件

除非另有指定，否则 `init` 守护进程会进入 `/etc/inittab` 中指定的默认运行级别。在过去，`/etc/inittab` 包含了整个配置。然而，在使用 SysV 的系统上，`/etc/inittab` 被设置为。

## 28 第 8 章 系统初始化、X Windows 与本地化

> 注意
>
> `/etc/inittab` 包含了默认运行级别。

```
[root@server1 ~]# cat /etc/inittab
5:default
[root@server1 ~]# 
```

## 运行时脚本

在启动过程中，`init` 守护进程必须执行多个脚本来启动守护进程并最终将系统带入状态。这些脚本被称为运行时（rc）脚本。

在使用传统 SysV 的 Linux 系统上，`init` 守护进程识别 `/etc/inittab`。为了确保目录中的文件按特定顺序执行，在 S 或 K 开头处添加了序列号。`rc5` 的内容如下：

```
[root@server1 ~]# ls /etc/
```

## 452 第 8 章 系统初始化、X Windows 与本地化

> 注意
>
> `/etc/inittab` 中的 `5:default` 显示运行级别 5 是默认值。Ubuntu 14.04 没有。

## 运行时配置

`/etc/rc[runlevel].d` 目录中的每个文件都是 `/etc/init.d` 目录中可执行 rc 脚本的符号链接，用于启动或停止某个守护进程。从前面的输出可以看出，进入此运行级别时 `init` 守护进程将启动 `postfix`。字母顺序：

```
[root@server1 ~]# ls /etc/rc5
S11apache
S15bind
S19postgresql
S20fs-mount
S20fs-share
S20postfix
S20rsync
```

## 453 第 8 章 系统初始化、X Windows 与本地化

回想级别 1（单用户模式）仅包含足够让用户登录并执行系统任务的守护进程。如果用户使用 `init` 命令命令 `init` 守护进程更改此运行级别，它将执行 `/etc.d` 中所有以 S 或 K 开头的文件。由于单用户模式下启动的守护进程很少，此目录中的大多数文件以 K 开头，如下所示：

```
[root@server1 ~]# ls /etc/rc
K08tomcat7
K09apache2
K20screen-cleanup
K20fs-mount
K20fs-share
K20postfix
K20rsync
K21postgresql
K30killprocs
[root@server1 ~]#
```

`/etc/rc[runlevel].d` 目录中的每个文件都是 `/etc/init.d` 目录中可执行 rc 脚本的符号链接。图 8

图 8-5 展示了引导到运行级别 5 的传统 UNIX SysV 系统初始化过程。

![](img/255973d661f18692a98dbc628624ab00_453_0.png)

**图 8-5 传统的 UNIX SysV 系统初始化过程**

> 注意
>
> 在执行 `/etc/rc[runlevel].d` 目录下的运行时配置脚本后，`init` 守护进程会执行 `/etc/rc.local` 脚本（如果存在）。因此，Linux 管理员经常会在 `/etc/rc.local` 中添加在初始化结束时运行的命令。

> 某些 Linux 发行版使用 `/etc/rc[runlevel].d` 目录代替 `/etc/rc[runlevel].d`，并使用 `/etc/rc.init.d` 目录代替 `/etc/init.d`。

## 第 8 章 系统初始化、X Windows 和本地化

在使用 upstart 系统的 Linux 系统上，不使用 `/etc/rc[runlevel].d` 目录。相反，守护进程会从 `/etc/initab` 中识别默认运行级别，并直接执行 `/etc/init.d` 目录中的 rc 脚本，根据 `/etc/init/` 目录下配置文件中指定的信息来启动或停止守护进程。每个守护进程在 `/etc/init/` 目录下都有一个独立的配置文件，该文件使用标准通配符符号来识别其应该启动或停止的运行级别。例如，接下来的 `/etc/init/cron.conf` 文件表示 `cron` 守护进程应该在运行级别 2, 3, 4 和 5 中启动（`[2345]`），并且不在运行级别 2, 3, 4 和 5 中停止。

```
[root@server1 ~]# cat /etc/init/cron.conf
# cron 定期后台程序处理守护进程
#
# cron 是一个标准的 UNIX 程序，在周期性调度时间运行
# 用户指定的程序
```

"定期后台程序处理守护进程"

在运行级别 `[2345]` 停止

在运行级别 `[!2345]` 停止

expect fork

respawn

```
exec cron
[root@server1 ~]#
```

图 8-6 展示了启动到运行级别 5 的系统的 upstart 系统初始化过程。

![](img/255973d661f18692a98dbc628624ab00_454_0.png)

图 8-6 upstart 系统初始化过程

> 注意
>
> 某些守护进程与 upstart 系统不兼容。因此，使用 upstart 系统的 Linux 发行版通常包含通过 `/etc/rc[runlevel]/d` 目录条目启动的传统 UNIX SysV 守护进程。

## 手动启动和停止守护进程

回上一节，`init` 守护进程在系统初始化时启动守护进程，并在运行级别改变后通过执行 `/etc/init.d` 目录内的 rc 脚本来启动和停止守护进程。要在系统启动后操作守护进程，你可以直接从 `/etc/init.d` 目录带适当的参数（`start`, `stop` 或 `restart`）执行它们。例如，要重启 `cron` 守护进程，你可以运行以下命令：

```
[root@server1 ~]# /etc/init.d/cron restart
cron stop/waiting
cron start/running, process 3371
[root@server1 ~]#
```

你也可以使用 `service` 命令启动、停止或重启 `/etc/init.d` 目录中列出的任何守护进程。例如，你可以使用以下命令重启 `cron` 守护进程：

```
[root@server1 ~]# service cron restart
cron stop/waiting
cron start/running, process 3352
[root@server1 ~]#
```

如果你修改了守护进程的配置文件，必须重启守护进程以确保守护进程重新加载配置文件。然而，某些守护进程允许你仅无需重启守护进程即可重新加载配置文件；例如，要强制 `cron` 守护进程重新加载其配置文件，你可以运行 `/etc/init.d/cron reload` 或 `service cron reload` 命令。你也可以随时通过 `status` 命令或 `/etc/init.d/cron` 内部的守护进程脚本或 `service` 来查看守护进程的状态；要查看 `cron` 守护进程的状态，你可以运行 `/etc/init.d/cron status`
