
![](img/8fe037bf1ed016dccb79dbd1a27184f2_666_0.png)

- 6. 使用光标滚动邮件列表直到到达顶部，按回车读取第一条消息的内容。完成后按 `i` 退出。
- 7. 按 `d` 删除第一条消息。现在高亮的是哪个消息？你能再次使用光标高亮第一条消息吗？
- 8. 按 `q` 退出邮件代理。当提示清理已删除的消息时，输入 `y`。

# 第 15 章

## 配置网络服务与安全

完成本章后，你将能够：

* 识别并配置常见的网络服务
* 配置路由和防火墙
* 描述 Linux 安全的不同方面
* 提高 Linux 计算机的安全性
* 概述可用于检测 Linux 安全违规的措施

在上一章中，你检查了网络接口的配置以及如何使用网络实用工具与网络上的网络服务进行交互。在本章中，你将检查常见网络服务、路由和防火墙的配置。随后，你将检查本地和网络安全概念、良好的安全实践，以及你可以用于加固 Linux 计算机和检测入侵者的实用工具。

## 网络服务

回想第 1 章“Linux 简介”，Linux 为网络上的用户提供了多种可用服务。在能够根据你的组织需求以满足组织需求而组织合适的网络服务之前，你必须首先识别网络服务的类型和特征。随后，你可以根据需要配置这些网络服务，并配置额外的网络相关服务，例如路由和防火墙。

### 识别网络服务

网络服务是运行在你计算机上的进程，它们为网络上的客户端提供某种类型的价值服务。它们通常由一系列监听网络上特定请求的守护进程（daemon processes）表示。守护进程通过你响应哪些数据包来识别，仅监听具有特定数字的数据包。这个数字被称为端口（port），用于唯一标识某个特定的服务。端口号就像邮件投的公寓号。IP 地址的网络 ID 确保数据包递送到正确的街道（网络）；主机 ID 确保数据包被递到正确的建筑（主机）；而传输层协议和端口号则确保数据包被递到正确的公寓（服务）。

端口及其关联协议定义在 `/etc/services` 文件中。查看 telnet 守护进程监听哪个端口，可以使用以下命令：

```
[root@server1 root]# grep telnet /etc/services
telnet 23/tcp
telnet 23/udp
telnet 107/tcp
net 107/udp
telns 992/tcp
telns 992/udp
[root@server1 root]#
```

上述输出表示 telnet 守护进程同时使用 TCP/IP 和 UDP/IP 监听端口 23。

> 用户数据报协议/网协议 (UDP/IP) 是一个比 TCP/IP 更快但因此可靠性较低的版本。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_671_0.png)

端口数字范围从 0 到 65534。端口 0–1023 称为“良好端口”，因为它们代表了常用的服务。表 15-1 提供了常见良好端口的列表。

### 表 15-1 常见良好端口

| 服务 | 端口 |
| :--- | :--- |
| FTP | TCP 20, 21 |
| Telnet | TCP 23 |
| SMTP | TCP 25 |
| HTTP | TCP 80 |
| DNS | TCP 53, UDP 53 |
| 简单 FTP (TFTP) | UDP 69 |
| POP3 | TCP 110 |
| NNTP | TCP 119 |
| IMAP | TCP 143 |
| 安全 HTTP | TCP 443 |

此外，网络实用工具（如上一章所示）可以直接连接到提供网络服务的守护进程，也可以通过互联网超级守护进程 (`xinetd`) 连接到网络守护进程，如图 15-1 所示。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_672_0.png)

图 15-1 与网络服务的交互

互联网超级守护进程通常用于启动和管理较小网络守护进程的连接，例如 telnet、login 和 FTP 守护进程。它在启动时自动启动并使用配置文件 `/etc/xinetd.conf`。通常，该文件包含了 `/etc/xinetd.d` 目录下的所有文件。大多数由互联网超级守护管理的守护进程是通过 `/etc/xinetd.d` 目录中命名的文件进行配置的。例如，telnet 守护进程是由互联网超级守护进程通过 `/etc/xinetd.d` 文件配置的，输出所示：

```
[@server1 root]# cat /etc/xinetd.d/telnet
# default: on
# description: The telnet server serves telnet sessions; it uses \
 unencrypted username/password pairs for authentication.
service telnet
{
    flags = REUSE
    socket_type = stream
    wait = no
}
user = root
server = /usr/sbin/in.telnetd
log_on_failure += USERID
disable = yes
```

```
[root@server1 root]#
```
