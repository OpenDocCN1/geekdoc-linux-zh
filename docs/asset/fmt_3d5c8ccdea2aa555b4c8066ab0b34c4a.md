
> **注意** 许多系统服务已迁移到 systemd。但是，如果你想双重检查，可以在此处查看特定服务的迁移状态：http://fedoraproject.org/wiki/User:Johann/QA/%Systemd/compatibility

要查看特定服务是否正在运行，请使用以下命令：

```bash
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: enabled (/lib/systemd/system/cups.service; enabled)
Active: active (running) Mon 30 Apr 2015 12:36:31 -0400; 13h ago
Main PID: 1315 (cupsd)
Group: name=systemd/cups.service
└ 1315 /usr/sbin/cupsd -f
```

`systemctl` 命令可用于显示单个服务的状态。在前面的示例中，选择了打印服务。注意服务的名称为 `cups.service`。这里提供了许多关于服务的有用信息，例如它是已启用并激活的、它的启动时间以及进程 ID (PID)。

现在你已经审计服务并获取有关它们的一些信息，你需要了解如何在 Linux 服务器上完成启动、停止和重载服务。

## 停止和启动服务

启动、停止和重启服务的任务通常指的是即时需求——换句话说，是在不重启服务器的情况下管理服务。例如，如果你想临时停止服务，那么你找对地方了。但是，如果你想停止一个服务并防止它在服务器重启时重新启动，那么你实际上需要禁用该服务，这在本章后面的“配置持久化服务”节中介绍。

## 停止和启动经典的 SysVinit 守护进程

停止和启动 SysV 服务的主要命令是 `service` 命令。使用 `service` 命令时，你想要控制的服务名称位于命令行的第二个。最后一个选项是你想对服务执行的操作：停止（`stop`）、启动（`start`）、重启（`restart`）等。以下示例显示了如何停止 cups 守护进程。注意显示了 OK，这让你知道 cups 已停止。

```
# service cups status
cupsd (pid 5857) is running...
#
# service cups stop
Stopping cups:      [ OK ]
#
# service cups status
cupsd is stopped
```

要启动服务，只需在 `service` 命令末尾添加 `start` 选项而不是 `stop` 选项。

```
# service cups start
Starting cups:      [ OK ]
#
# service cups status
cupsd (pid 6860) is running...
```

要重启 SysVinit 服务，只需在 `service` 命令末尾添加 `restart` 选项。

```
# service cups restart
Stopping cups:      [ OK ]
Starting cups:      [ OK ]
#
# service cups status
cupsd (pid 6860) is running...
```

# 第四部分：成为 Linux 服务器管理员

```
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service; enabled)
Active: inactive (dead) since Tue, 01 May 2015 04:43:0...
Process: 1315 ExecStart=/usr/sbin/cupsd -f
(code=exited, status=0/SUCCESS)
CGroup: name=system/cups.service
```

注意在查看服务状态时，停止 cups 守护进程后，该服务处于非活动（死亡）状态，但仍被视为已启用（`enabled`）。这意味着 cups 守护将在服务器启动时启动。

## 使用 systemd 启动服务

启动 cups 守护进程与停止它一样简单。下面的示例演示了这种便利性。

```
# systemctl start cups.service
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service; enabled)
Active: (running) since Tue, 01 May 2015 04:43:0...
Main PID: 17003 (cupsd)
CGroup: name=system/cups.service
└ 17003 /usr/sbin/cupsd -f
```

启动 cups 守护进程后，使用 `systemctl` 的 `status` 选项显示该服务处于活动（运行）状态。此外还会显示其 ID（PID）数字 17003。

## 使用 systemd 重启服务

重启服务意味着停止服务然后重新启动。如果服务当前未运行，重启将直接启动服务。

```
# systemctl restart cups.service
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service; enabled)
Active: active (running) since Tue, 01 May 2015 04:45:2...
Main PID: 17015 (cupsd)
CGroup: name=system/cups.service
└ 17015 /usr/sbin/cupsd -f
```

你也可以使用 `systemctl` 对服务进行条件重启。条件重启仅在服务当前运行时才会进行重启。任何处于非活动状态的服务都不会被启动。

## 第15 章：启动和停止服务

```
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service, enabled)
Active: inactive (dead) since Tue, 01 May 2015 06:03:22...
Process: 17108 ExecStart=/usr/bin/cupsd -f
(code=exited, status=0/SUCCESS)
Group: name=systemd:cups.service
```

```
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service, enabled)
Active: inactive (dead) since Tue, 01 May 2015 06:03:22...
Process: 17108 ExecStart=/usr/bin/cupsd -f
(code=exited, status=0/SUCCESS)
Group: name=systemd:cups.service
```

注意示例中，cups 守护进程处于非活动状态。当执行条件重启时，没有生成任何错误信息！cups 守护进程没有启动，因为条件重启只会影响活动状态的服务。因此，在启动、停止、条件重启等之后，检查服务的状态始终是一个良好的习惯。

## 使用 systemd 重新加载服务

重新加载服务与重启服务不同。当你重新加载服务时，服务本身不会停止。只有配置会被重新加载。

```
# systemctl reload cups.service
Failed to issue method: Job reload is not applicable for unit cups.service.
```

```
# systemctl reload sshd.service
```
