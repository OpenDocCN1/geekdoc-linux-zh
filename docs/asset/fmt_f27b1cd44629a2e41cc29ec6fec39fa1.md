
4.3 版本通过提供 `wait/nowait` 简化了这一点。`inetd` 意通过 `wait` 字段接管与服务相关的监听套接字。配置为 `wait` 的 UDP 服务具有独立的监听和接受套接字，且几乎总是被配置为 `nowait`。TCP 服务可以用这两种方式处理，取决于编写守护进程的人，但 `nowait` 是最常见的。

IPv6 与 `/etc/inetd.conf` 的交互取决于供应商，为了实现你的目标需要特别注意细节。某些使用 `tcp6` 或 `udp6` 协议表示为该服务创建一个 IPv6 套接字。某些 `tcp46` 或 `udp46` 协议值表示允许 IPv6 和 IPv4 连接的守护套接字。这些特殊的协议名称通常不在 `/etc/protocols` 文件中。

## 图 13.6 inetd 文件的字段。

| 字段 | 描述 |
|---|---|
| service-name | 必须存在 `/etc/services` 中 |
| socket-type | `stream` (TCP) 或 `dgram` (UDP) |
| protocol | 必须存在 `/etc/protocols` 中：或是 `tcp` 或 `udp` |
| wait-flag | TCP 通常为 `nowait`，UDP 为 `wait` |
| login-name | 来自 `/etc/passwd`：通常为 `root` |
| server-program | 要执行的完整路径 |
| server-program-arguments | `exec` 的参数 |

一些示例行：

```
ftp stream tcp nowait root /usr/bin/ftppd -1
telnet stream tcp nowait root /usr/bin/telnetd
login stream tcp nowait root /usr/bin/rlogind rlogind -s
tftp dgram udp wait nobody /usr/bin/tftpd tftpd -s
```

图 13.7 展示了 `inetd` 守护进程所的操作。

## 图 13.7. inetd 执行的步骤。

![](img/ab2a67f72092d143e16c9adbe684e62b_465_0.png)

1. 在启动时，它会读取 `/etc/inetd.conf` 文件，并为文件中指定的所有服务创建适当类型（流或数据报）的套接字。`inetd` 能够处理的最大服务器数量取决于 `inetd` 能创建的最大描述符数量。每个新套接字都是描述符集合，将在 `select` 调用中使用。
2. 对套接字调用 `bind`，指定服务器的端口和通配符 IP 地址。此 TCP 或 UDP 端口号通过 `getservbyname` 获取，其参数为配置文件中的服务名和协议/字段。
3. 对于 TCP 套接字，调用 `listen` 以接收传入的连接请求。数据报（datagram）套接字执行此步骤。
4. 在创建所有套接字后，调用 `select` 等待任何套接字变为可读。回想第 6.3 节，当新连接准备好被接受时，监听的 TCP 套接字变为可读；当数据报到达时，UDP 套接字变为可读。`inetd` 大部分时间花在名为 `select` 的块中，等待套接字变为可读。
5. 当 `select` 返回套接字可读时，如果该套接字是 TCP 套接字且就绪，则调用 `accept` 接受新连接。
6. `inetd` 守护进程进行 `fork`，子进程处理服务请求。这类似于标准的并发服务器（第 4.8 节）。

子进程关闭除正在处理的套接字以外的所有描述符：TCP 服务器由 `accept` 返回的新套接字，或原始的 UDP 套接字。子进程执行三次 `dup`，将套接字复制到描述符 0、1 和 2（标准输入、输出和标准错误）。通过这样做，子进程中打开的描述符只有 0、1 和 2。如果子进程从输入读取，它将从套接字读取；写入输出或标准错误的内容将将写入套接字中。子进程使用 `getpwn` 为配置文件中指定的登录名命名密码文件条目。如果该字段不是 `root`，则子进程使用 `setgid` 和 `setuid` 函数变为指定的用户（由于 `inetd` 进程以用户 ID 0 运行，子进程在 `fork` 之后继承此用户 ID，并能够使用它选择的任何用户）。

子进程执行 `exec` 来运行服务器程序以处理请求，并传递配置文件中指定的参数。

7. 如果套接字是流套接字，父进程关闭已连接的套接字（类似于我们的标准并发服务器）。父进程再次调用 `select`，等待下一个套接字变为可读。

如果我们更详细地查看正在发生的描述符处理，图 13.8 显示了当来自 FTP 客户端的连接请求到达时，`inetd` 中的描述符。

## 图 13.8. 当 TCP 端口 21 有连接请求时 inetd 的描述符。

![](img/ab2a67f72092d143e16c9adbe684e62b_466_0.png)

连接请求指向 TCP 端口 21，但由 `accept` 创建了一个新的连接套接字。

图 13.9 显示了调用 `fork` 之后、子进程关闭除已连接套接字以外的所有描述符后的描述符。

## 图 13.9. 子进程中的 inetd 描述符。

# inetd (子进程)

![](img/ab2a67f72092d143e16c9adbe684e62b_467_0.png)

下一步是子进程将连接套接字复制到描述符 0、1 和 2，然后关闭连接套接字。这让我们得到了图 13.10 所示的描述符。

## 图 13.10. dup2 之后的 inetd 描述符。

![](img/ab2a67f72092d143e16c9adbe684e62b_467_1.png)

子进程随后调用 `exec`。回想第 4.7 节，所有描述符在 `exec` 之后通常保持打开，因此真正的服务器可以使用任何描述符 0、1 或 2 与客户端通信。

```c
getpeername(0, cliaddr, &len);
err_msg("connection from %s", sock_ntop(cliaddr, len));
```

```c
ticks = time(NULL);
printf(buff, sizeof(buff), "%.24s\r\n", ctime(&ticks));
write(0, strlen(buff));
```

```c
close(0);                /* 关闭 TCP 连接 */
exit(0);
```

这个程序有两个主要变化。首先，所有的套接字创建代码都是：对 `tcp_listen` 和 `accept` 的调用。这些步骤由 `inetd` 完成，我们使用描述符 0（标准输入）来引用 TCP 连接。其次，无限循环消失了，因为我们每个连接都会被调用一次。处理完该客户端后，我们就会终止。

### getpeername

II-14 由于我们没有调用 `tcp_listen`，因此不知道它返回的套接字结构的大小；由于没有调用 `accept`，我们不知道客户端的协议地址。因此，我们使用 `sizeof(struct sockaddr_storage)` 为套接字结构分配一个缓冲区，并调用 `getpeername`，将描述符 0 作为第一个参数。

要在 Solaris 系统上运行此示例，我们首先为该服务分配名称和端口，在 `/etc/services` 中添加以下行：

```
mydaytime9999/tcp
```

然后，我们在 `/etc/inetd.conf` 中添加以下行：

```
mydaytime stream tcp nowait andy
/home/andy/daytimecpsrv3 daytimecpsrv3
```

（我们对长行进行了折行。）我们将可执行文件放在指定位置，并向 `inetd` 发送 `SIGHUP`，告诉它重新读取配置文件。下一步是执行 `netstat` 以验证 TCP 端口 9999 上是否创建了一个监听套接字。

```bash
solaris % netstat -na | grep 9999
*.9999 .* 0 0 49152 0 LISTEN
```

然后，我们从另一台主机调用服务器。

```bash
linux % telnet solaris 9999
Trying 192.168.1.20...
Connected to solaris.
Escape character is '^]'
Tue Jun 10 11:04:02 2003
Connection closed by foreign host.
```

`/var/adm/messages` 文件（我们在 `/etc/syslog.conf` 中将 `LOG_USER` 设施的消息重定向此处）包含以下条目：

Jun 10 11:04:02 solaris daytimecpsrv3[28724]: connection from 192.168.1.10.58145

## 13.7 总结
