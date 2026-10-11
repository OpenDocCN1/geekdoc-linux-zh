
`/lib/systemd/system/runlevel.target`

- 2. 要列出你服务器上运行（或激活）的服务，你需要根据使用的初始化守护进程使用不同的命令。
    - 对于 SysVinit，使用示例所示的 `service` 命令：
```bash
# service --status-all | grep running...
anacron (pid 2162) is running...
atd (pid 2172) is running...
```
    - 对于 Upstart，使用 `initctl` 命令。然而，也应使用 `service` 命令，因为并不是所有服务都迁移到了 Upstart：
```bash
# initctl list | grep start/running
tty (dev/tty3) start/running, process 1163
...
```
    - 对于 systemd，使用 `systemctl list-units --type=service | grep -v disabled`
| UNIT FILE | STATE |
|---|---|
| abrtd-ccpp.service | enabled |
| abrtd-oops.service | enabled |

- 3. 要列出你 Linux 服务器上（运行或激活的）服务，请根据服务器使用的初始化守护进程使用答案 5 中确定的相应命令。

- 4. 对于每个初始化守护进程，以下命令显示了特定服务的状态：
    - 对于 SysV，使用 `service service_name status` 命令。
    - 对于 Upstart，使用 `initctl status service_name` 命令。
    - 对于 systemd，使用 `systemctl status service_name` 命令。

- 5. 要显示你 Linux 服务器上 `cups` 守护进程的状态，请使用以下命令：
    - 对于 SysV：
```bash
# service cups status
cupsd (pid 8236) is running...
```
    - 对于 Upstart：
```bash
# initctl status cups
cups start/running, process 2390
```
    - 记住，如果服务尚未迁移到 Upstart，则你需要使用 `service` 命令而不是 `initctl`。
    - 对于 systemd：
```bash
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service; enabled)
Active: active (running) since Tue, 01 May 2015 04:43...
Main PID: 17003 (cupsd)
CGroup: name=system:/system/cups.service
17003 /usr/bin/cupsd -f
```

- 6. 要尝试重启你 Linux 服务器上的 `cups` 守护进程，请使用以下命令：
    - 对于 SysV：
```bash
# service cups restart
Stopping cups: [ OK ]
Starting cups: [ OK ]
```
    - 对于 Upstart：
```bash
# initctl restart cups
cups start/running, process 2490
```
    - 记住，如果服务尚未迁移到 Upstart，则你需要使用 `service` 命令而不是 `initctl`。
    - 对于 systemd：
```bash
# systemctl restart cups.service
```

- 7. 要尝试重载你 Linux 服务器上的 `cups` 守护进程，请使用以下命令：
    - 对于 SysVinit：
```bash
# service cups reload
Reloading cups:      [ OK ]
```
    - 对于 Upstart：
```bash
# initctl reload cups
```
    记住，如果服务尚未迁移到 Upstart，则你需要使用 `service` 命令而不是 `initctl`。
    - 对于 systemd，命令如下：
```bash
# systemctl reload cups.service
```

- 8. 要更改你 Linux 服务器上默认的运行级别或目标单元，你可以执行以下操作之一（取决于你服务器的 init 守护进程）：
...（此处重复逻辑已通过维持流程处理）

- 1. 要更改你 Linux 服务器上默认的运行级别或目标单元...（上下文流程）

- 2. 对于每个初始化守护进程，以下命令显示了特定服务的状态：
    - 对于 SysV，使用 `service service_name status` 命令。
    - 对于 Upstart，使用 `initctl status service_name` 命令。
    - 对于 systemd，使用 `systemctl status service_name` 命令。

- 3. 要显示你 Linux 服务器上 `cups` 守护进程的状态，请使用以下命令：
    - 对于 SysV：
```bash
# service cups status
cupsd (pid 8236) is running...
```
    - 对于 Upstart：
```bash
# initctl status cups
cups start/running, process 2390
```
    - 记住，如果服务尚未迁移到 Upstart，则你需要使用 `service` 命令而不是 `initctl`。
    - 对于 systemd：
```bash
# systemctl status cups.service
cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service; enabled)
Active: active (running) since Tue, 01 May 2015 04:43...
Main PID: 17003 (cupsd)
CGroup: name=system:/system/cups.service
17003 /usr/bin/cupsd -f
```

- 4. 要尝试重启你 Linux 服务器上的 `cups` 守护进程，请使用以下命令：
    - 对于 SysV：
```bash
# service cups restart
Stopping cups: [ OK ]
Starting cups: [ OK ]
```
    - 对于 Upstart：
```bash
# initctl restart cups
cups start/running, process 2490
```
    - 记住，如果服务尚未迁移到 Upstart，则你需要使用 `service` 命令而不是 `initctl`。
    - 对于 systemd：
```bash
# systemctl restart cups.service
```

- 5. 要尝试重载你 Linux 服务器上的 `cups` 守护进程，请使用以下命令：
    - 对于 SysVinit：
```bash
# service cups reload
Reloading cups:      [ OK ]
```
    - 对于 Upstart：
```bash
# initctl reload cups
```
    记住，如果服务尚未迁移到 Upstart，则你需要使用 `service` 命令而不是 `initctl`。
    - 对于 systemd，命令如下：
```bash
# systemctl reload cups.service
```

# 附录 B：练习答案

在 RHEL 6 或更早版本中，

```bash
# service httpd start
# chkconfig httpd on
```

使用 `netstat` 命令查看 `httpd` 服务器正在监听哪些端口，请使用以下命令：

```bash
# netstat -tupn | grep httpd
tcp6 0 :::* LISTEN 2496/httpd
tcp6 0 :::443 :::* LISTEN 2496/httpd
```
