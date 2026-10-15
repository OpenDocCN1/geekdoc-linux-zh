

```
% grep ^ssh /etc/services
ssh 22/tcp #Secure Shell Login
ssh 22/tcp #Secure Shell Login
ssh 22/udp #Secure Shell Login
sshell 614/tcp #SSLshell
sshell 614/udp
%
```

## 20.10.1.3 在 PC-BSD 和 Solaris 上定位 inetd 协议

inetd 运行时的另一个读取文件是 /etc/services。该文件是协议名称的数据库，包含协议的名称、IANA 分配给该协议的编号以及协议的别名。inetd 用于任何服务的协议必须在 /etc/protocols 文件中有一个条目。它以以下格式每行一个协议：

```
protocol-name number [aliases]
```

这里，protocol-name 是协议名称，例如 tcp，number 是 IANA 分配给该协议的编号，例如 tcp 为 6，aliases 是协议的替代名称，例如 tcp 的 TCP。以下是 /etc/protocols 文件中 tcp 协议的行：

```
% grep ^tcp /etc/protocols
tcp 6 TCP # transmission control protocol
%
```

## 20.10.1.4 在 PC-BSD 上添加或删除 inetd 服务

作为管理员，你可以通过简单地从 /etc/inetd.conf 文件中删除相关服务的行来删除 inetd 提供的服务。同样，你可以通过在 /etc/inetd.conf 文件中添加对应服务的一行来在 inetd 中添加新服务。

在 /etc/inetd.conf 文件中做出必要的更改后，你可以动态地重新配置 inetd，使其提供更新的服务集，而无需终止并重新启动它。你可以通过使用 kill 或 killall 命令向 inetd 发送 SIGHUP（无挂断信号）来实现。表 20.25 显示了执行此任务的四种方法。请注意，killall 命令使用进程名，而 kill 使用进程 ID（PID）。请注意反引号（`）用于 cat /var/run/inetd.pid 命令的替换，并执行该命令。

### EXERCISE 20.27

显示系统中 /etc/inetd.conf 文件中列出的所有“internal”服务的行。

TABLE 20.25 Ways of Restarting inetd

|  |  |
|---|---|
| 1 | killall -HUP inetd |
| 2 | killall -1 inetd |
| 3 | kill -HUP `cat /var/run/inetd.pid` |
| 4 | kill -1 `cat /var/run/inetd.pid` |

## EXERCISE 20.28

显示 /etc/protocols 文件中 UDP 协议的行。UDP 协议关联的数值是多少？该文件中定义了多少个协议？

## 20.11 并发客户端

似乎很明显地认为需要并发服务器以高效地同时为多个客户端服务，从而减少客户端经历的平均响应时间。然而，并发客户端的需求并不那么明显。由于应用协议的需要，存在几个现实生活中的并发客户端示例。许多知名服务需要并发客户端，包括 SSH、TELNET、FTP 和 HTTP。这些服务的每个客户端都必须处理两个描述符：一个标准输入描述符（键盘）用于读取用户输入，以及一个由客户端用于与服务器进程通信的套接字描述符。任一描述符都可能异步准备好进行 I/O；用户可能随时使用键盘为客户端输入下一个命令，并且服务器对先前客户端请求的响应可能在任何时刻到达客户端套接字，具体取决于服务器进程的负载和网络流量。

我们通过面向连接的（TCP）SSH 客户端的示例来解释并发客户端的需求。SSH 的 TCP 客户端期望从两个描述符接收输入，一个用于键盘，另一个用于连接到 SSH 服务器端套接字的套接字。客户端需要接收通过键盘输入的用户输入（即要在远程主机上执行的下一个 shell 命令）和通过已连接套接字接收的服务器响应，如图 20.32 所示。由于两个描述符异步就绪，你可以通过使用 select() 系统调用来实现此类并发客户端。

另一个需要并发客户端的场景出现是因为 BSD UNIX 不允许独立进程共享主内存。X Window 系统允许多个客户端绘制（即重绘）位图显示，以便在需要时更新各自客户端的窗口。由于 X 显示是

![](img/02e070097d401d3bf7de4bf1c470b267_990_0.png)

