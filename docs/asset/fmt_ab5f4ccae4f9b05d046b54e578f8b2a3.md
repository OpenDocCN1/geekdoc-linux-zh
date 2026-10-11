
`[root@fedora-serverA A1]# service xinetd restart`

注意，对于其他没有提供 `service` 命令的发行版，我们可以改为向 `xinetd` 发送 HUP 信号。首先，使用 `ps` 命令找到 `xinetd` 的进程 ID (`PID`)。然后使用 `kill` 命令向 `xinetd` 进程 ID 发送 HUP 信号。我们可以通过 `tail` 命令查看 `/var/log/messages` 文件的最后消息来验证重启是否成功。查找 `xinetd` 的 PID、杀死 `xinetd` 以及查看日志文件的命令为：

```bash
[root@serverA]# ps -C CMD

PID TTY CMD xinetd

14024 ? 00:00:00

[root@serverA]# kill -a 14024

[root@serverA]# tail /var/log/messages

Dec 9 12:47:45 serverA xinetd Version 2.3.14 started with libwrap

Dec 9 12:47:45 serverA xinetd[14024]: Starting configuration

Dec 9 12:47:45 serverA xinetd[14024]: Swapping defaults

Dec 9 12:47:45 serverA xinetd[14024]: readjusting service echo-stream

Dec 9 12:47:45 fedora-serverA xinetd[14024]: Reconfigured: new=0 old-1 dropped=0(services)
```

- 4. Telnet 到 echo 服务的端口（端口 7），查看服务是否正在运行。输入

```bash
[root@fedora-serverA]# telnet localhost 7

Trying 127.0.0.1...

Connected to localhost.

Escape character is ' '
```
