
`wpa_supplicant` 0:off 1:off 2:off 3:off 4:off 5:off 6:off

`xfs` 0:off 1:off 2:on 3:on 4:on 5:on 6:off

`ypbind` 0:off 1:off 2:off 3:off 4:off 5:off 6:off

`yum-updatesd` 0:off 1:off 2:off 3:on 4:on 5:on 6:off

示例中的某些服务永远不会启动。其他服务（如 `vncserver` 和 `cups` 守护进程）在运行级别 2 到 5 上启动。

使用 `chconfig` 命令，你无法判断某个服务当前是否运行。要做到这一点，你需要使用 `service` 命令。为了只隔离出当前正在运行的服务，将 `service` 命令通过给 `grep` 命令并进行排序，如下：

```
# service --all | grep running... | sort

anachron (pid 2162) is running...

atd (pid 2172) is running...

audit (pid 1653) is running...

automount (pid 1952) is running...

console-kit-daemon (pid 2046) is running...

crond (pid 2118) is running...

cupsd (pid 1988) is running...
```

# 第 15 章：启动和停止服务

```
sshd (pid 2002) is running...

syslogd (pid 1681) is running...

xfs (pid 2151) is running...

yum-updated (pid 2205) is running...
```

你可以同时使用 `chkconfig` 和 `service` 命令来查看单个服务的设置。在下方的示例中使用了这两个命令，你可以查看 `cups` 的设置。

```
# chkconfig --list cups

cups 0:off 1:off 2:on 3:on 4:on 5:on 6:off

# service status cups

cupsd (pid 1988) is running...
```

你可以看到 `cups` 守护进程被设置为在每个运行级别 0、1 和 6 上启动，通过 `service` 命令，你可以看到它当前正在运行。此外，还给出了守护进程的进程 ID (PID)。

## 检查启动系统的服务

要查看使用 Startup 初始化的 Linux 服务器上运行的所有服务，请使用以下命令：

```
# initctl list | grep start/running

tty (/dev/tty3) start/running, process 1163

system-setup-keyboard start/running, process 656

prefdm start/running, process 1154
```

请记住，可能仍有尚未迁移到 init 守护进程的服务。你还需要使用经典的 SysV 命令 `service` 来检查任何遗留的 SysV 服务。注意，在某些发行版中，你可能会在 `init` 和 `service` 命令的输出中同时看到某些服务。

```
# service --status-all | grep running

abrtd (pid 1118) is running...

acpid (pid 996) is running...

atd (pid 1146) is running...

...

syslogd (pid 752) is running...

sendmail (pid 109) is running...
```

> 提示
> 只要 `service` 状态为 `stopped`，并不意味着它不可用。可能仍有尚未迁移到 init 守护进程的服务。你还需要使用经典的 SysV 命令 `service` 来检查任何遗留的 SysV 服务。注意，在某些发行版中，你可能会在 `init` 和 `service` 命令的输出中同时看到某些服务。

要查看单个服务的状态，请使用 `initctl`。为了查看无论状态如何的所有服务，使用 `initctl` 如下。

```
# initctl status vpc-cleanup

vpc-cleanup stopped

# service status

sshd (pid 190) is running...
```

在示例中，`sshd` 已经迁移。

## 检查 systemd 系统的服务

要查看使用 systemd 的 Linux 服务器提供的所有服务，请使用以下命令：

```
# systemctl list-unit-files --type=service | grep -v disabled

UNIT FILE | STATE |

| :--- | :--- |

| abrtc-cc.service | enabled |

| abrtc-oops.service | enabled |

| abrtc-vmcore.service | enabled |

| abrtd.service | enabled |

| salsa-restore.service | static |

| salsa-store.service | static |

| anaconda-shell.service | static |

| arp-eth0.service | enabled |

| atd.service | enabled |

| audit.service | enabled |

| avaahi-daemon.service | enabled |

| bluetooth.service | enabled |

| console-log-restart.service | static |

| console-log-start.service | static |

| console-log-stop.service | static |

| crond.service | enabled |

| cups.service | enabled |

| ... | | |

| sshd-keygen.service | enabled |

| sshd.service | enabled |

| systemd-setup-keyboard.service | enabled |

| ... | | |
```

列出了 134 个单元文件。

记住 systemd 服务的三个状态可能性：启用（enabled）、禁用（disabled）或静态（static）。为了查看哪些服务设置为激活，不需要包含禁用，这在前面的示例中通过对 `grep` 命令使用 `-v` 选项有效地实现的。静态状态本质上是启用的，因此应该包含。

要查看特定服务是否正在运行，请使用以下命令：

```
# systemctl status cups.service

cups.service - CUPS Printing Service

Loaded: loaded (/lib/systemd/system/cups.service; enabled)

Active: active (running) since Mon, 30 Apr 12:26:31 -0400; 13h ago

Main PID: 1315 (cups)

CGroup: system=systemd/cups.service

 L 1315 /usr/bin/cups -f
```

`systemctl` 命令可以显示单个服务的状态。在前面的示例中，选择了该服务。注意服务的名称是 cups。这里提供了关于该服务的许多有用信息，例如它是处于启用和激活状态、启动时间以及其进程 ID (PID)。

# 第四部分：成为 Linux 服务器管理员

要启动服务，你只需在服务命令的末尾使用 `start` 选项而不是 `stop` 选项，如下：

```
# service cups start

Starting cups: [ OK ]

# service cups status

cups (pid 6860) is running...
```

对于 SysInit 服务，使用 `restart` 选项。该选项会停止服务并立即重新启动。

```
# service cups restart

Stopping cups: [ OK ]

Starting cups: [ OK ]

# service cups status

cupsd (pid 7955) is running...
```

当服务已经停止时，执行 `restart` 会在尝试停止它时产生 `FAILED` 状态。然而，如所示，当尝试重启时，服务会成功重新启动。
