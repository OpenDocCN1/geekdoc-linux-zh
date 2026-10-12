
| process | 要执行的进程。 |

##### 表 8-9

| 动作 | 功能 |

| :--- | :--- |

| `respawn` | 每当进程终止时，该进程将被重新启动。你会看到这在 `getty` 登录进程中被使用，它们需要每次重新生成。 |

| `wait` | 进程启动一次，然后 `init` 等待其终止。 |

| `once` | 当进入运行级别时，该进程仅执行一次。 |

| `boot` | 进程将在启动时执行，任何运行级别字段条目将被忽略。 |

| `bootwait` | 进程在启动时开始，`init` 将等待其完成后再继续。 |

| `initdefault` | 指定系统启动时进入的运行级别。 |

| `sysinit` | 此条目将在启动时执行，在任何其他 `boot` 或 `bootwait` 条目之前。运行级别字段被忽略。 |

| `powerwait` | 当系统断电（由 UPS 报告）时，此条目将被处理。`init` 将等待其完成后再继续。 |

| `powerfail` | 与 `powerwait` 相同，但 `init` 不等待此进程完成。 |

| `powerokwait` | 当电源恢复到系统时，此进程将被执行。`init` 将等待其完成。 |

| `powerfailnow` | 当 UPS 向系统发出电池几乎耗尽的信号时，此进程将被执行。 |

| `ctrlaltdel` | 当用户按下 Ctrl-Alt-Delete 键组合时，此条目将被处理。 |

| `kbrequest` | 当按下定义的特殊键盘组合时，执行指定的进程。 |

以下是 `/etc/inittab` 文件的示例，并附有说明。

```
#
id:3:
```

告知系统默认启动进入的运行级别。由此可见，该系统可能是红帽系统，启动进入多用户文本模式。

> **考试提示** `initdefault` 条目定义了系统将启动进入的运行级别。

```
# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit
```

这些行在系统初始化期间运行 `/etc/rc.d/rc.sysinit` 脚本。此脚本在任何其他脚本之前执行，且 `init` 将等待其完成后再继续。

```
l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6
```

这些行告诉 `init` 每个运行级别应运行哪个命令。例如，当系统更改为运行级别 5 时，命令 `/etc/rc.d/rc 5` 被执行。`/etc/rc.d/rc` 脚本启动系统，通过传递参数 5，它在运行级别 5 启动。`init` 也将等待指定脚本完成后再继续。

```
# Things to run in every runlevel.
::once:/sbin/update
```

此行导致在系统启动时，对于所有运行级别，`/sbin/update` 命令执行一次。

```
# Trap CTRL-ALT-DELETE
ca:ctrlaltdel:/sbin/shutdown -t3 -r now
```

此行导致每当输入 Ctrl-Alt-Delete 键组合时，系统执行 `/sbin/shutdown -t3 -r now` 命令。这对于捕获信号并优雅地重启系统很有用。

```
pf:powerfail:/sbin/shutdown -f -h +2 "Power Failure: System Shuttin Down"
```

此行导致如果不间断电源（UPS）发出失去电源的信号，系统将优雅地关机。

```
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
```

如果 UPS 检测到电源已恢复，此行将取消重启。

```
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

`/sbin/mingetty` 进程在运行级别 2 到 5 中启动。这些提供标准的登录控制台，并在每次终止时重新生成。

```
x:5:respawn:/etc/X11/prefdm -nodaeamon
```

此行在运行级别 5 启动图形登录进程。

#### 定制启动过程

`init` 在启动系统时遵循的过程在 `/etc/inittab` 文件中确切地列出。但此文件并没有说明全部情况；它只是启动处理大多数任务的其他脚本。大多数 Linux 发行版使用许多不同的脚本文件来启动系统中的服务和进程。目前使用两种不同类型的启动程序：BSD 和 Sys V。

##### BSD 启动

一些 Linux 发行版使用较旧的 BSD 风格初始化，其中最流行的是 Slackware。在 BSD 初始化中，系统使用几个长的 `rc`（run control）脚本文件来设置和配置系统。这些通常命名为类似 `/etc/rc` 和 `/etc/rc.local`。这种设置的优点是你知道在哪里查找大多数内容，并且所有信息都存储在同一位置。BSD 风格初始化的问题是更难快速定制。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_343_0.png)

> 顾名思义，FreeBSD 和 OpenBSD 等 BSD 变体使用这种类型的启动。

##### Sys V 启动

Red Hat、其变体以及 Debian 都使用 System V 初始化，称为 Sys V init。这种启动风格使用许多小脚本文件，位于按运行级别分隔的层次目录结构中。在 Red Hat 中，此目录树的根是 `/etc/rc.d`，而在 Debian 中，根仅在 `/etc` 中。

在树的根目录下有一个名为 `init.d` 的目录。在此目录内有多个不同的脚本文件。这些脚本中的每一个都服务于特定目的，无论是启动服务器、启用网络子系统还是检查文件。这些脚本可用于管理系统上的服务。要查看可以传递给脚本的命令，只需不带参数执行该脚本。例如：

```
[root@redhat init.d]# ./lpd
Usage: lpd {start|stop|restart|reload|status}
```

启动脚本在第 11 章中更详细地介绍。

所有脚本至少接受 `start`、`stop` 和 `restart` 命令。这些用于优雅地管理服务，并应代替手动运行服务可执行文件。许多服务提供 `status` 命令，它可以显示有用的信息，例如以下：

```
[root@redhat init.d]# ./network status
Configured devices:
lo eth0
Devices that are down:

Devices with modified configuration:
```

在 `/etc/rc.d` 下，有名为 `rc0.d` 到 `rc6.d` 的每个运行级别的目录。在运行级别目录内，是指向 `init.d` 目录中脚本的链接文件。运行级别目录中链接文件的名称与它们链接到的脚本名称不同。第一个字母是 `S` 或 `K`。当系统执行运行级别目录中的脚本时，它向以 `S` 开头的脚本传递 `start` 命令，向以 `K` 开头的脚本传递 `stop` 命令。这样你可以限制在更改运行级别时哪些进程保持运行。在第一个字母之后是一个数字，指定脚本启动的顺序。这样你可以说 `S35syslog` 在 `S50inet` 之前启动。在优先级数字之后是脚本的名称，这只是描述性信息。

由于运行级别目录仅包含指向 `init.d` 中脚本的链接，因此很容易更改在新运行级别进入时发生的服务和功能。如果你想删除一个服务，只需删除链接文件。如果你想向一个运行级别添加新服务，只需创建一个指向 `init.d` 中脚本文件的符号链接，以 `S` 作为第一个字母并加上优先级数字。此外，由于所有运行级别都指向相同的脚本，你只需修改一个文件即可做出更改。

##### Red Hat 启动

当 Red Hat 启动时，`init` 运行的第一个脚本是 `/etc/rc.d/rc.sysinit`。它由 `/etc/inittab` 文件中的以下行运行。

```
si::sysinit:/etc/rc.d/rc.sysinit
```

##### 系统配置脚本

此脚本配置最基础的系统设置，包括主机名、时间和文件系统，并加载所需的内核模块。以下是此脚本执行的任务完整列表。

- 1. 设置默认系统 `PATH` 变量。
