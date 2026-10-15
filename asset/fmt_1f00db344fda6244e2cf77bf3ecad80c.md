
[root@server1 root]## `grep telnet /etc/services`

`telnet 23/tcp`

`telnet 23/udp`

`telnet 107/tcp` # Remote Telnet

`telnet 107/udp`

`telnet 992/tcp`

`telnet 992/udp`

[root@server1 root]#

前面的输出表明 `telnet` 守护进程使用 TCP/IP 和 UDP/IP 监听端口 23。

> 用户数据报协议/IP协议 (UDP/IP) 是比 TCP/IP 更快但因此可靠性较低的版本。

端口数量范围从 0 到 65534。端口 0–1023 被称为已知端口（well-known ports），因为它们代表了常用的服务。表 15–1 提供了常用已知端口的列表。

### 表 15-1 常用已知端口

| 服务 | 端口 |
| :--- | :--- |
| FTP | TCP 20, 21 |
| Telnet | TCP 23 |
| SMTP | TCP 25 |
| HTTP | TCP 80 |
| DNS | TCP 53, UDP 53 |
| Trivial FTP (TFTP) | UDP 69 |
| POP3 | TCP 110 |
| NNTP | TCP 119 |
| IMAP | TCP 143 |
| Secure HTTP | TCP 443 |

此外，网络实用程序（如上一章所示）可以直接连接到提供网络服务的守护进程，也可以通过互联网超级守护（`xinetd`）连接到网络守护进程，如图 15-1 所示。

图 15-1 与网络服务的交互

互联网超级守护通常用于启动并为较小的网络守护进程建立连接，如 `telnet`、`login` 和 `FTP` 守护进程。它在启动时自动启动并使用配置文件 `/etc/xinetd.conf`。通常情况下，大多数守护进程也由 `/etc/xinetd.d` 目录下的所有文件管理。互联网超级守护通过 `/etc/xinetd.d` 目录下以守护进程命名的文件进行配置。例如，`telnet` 守护进程是由互联网超级守护通过 `/etc/xinetd.d/telnet` 文件配置的，如下所示：

```bash
@server1 # @etc/xinetd.d/telnet

# default: on

# description: telnet 服务器提供 telnet 会话；它使用未加密的用户名/密码对进行身份验证。

# service telnet

{
    flags = REUSE
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable = yes
}
```

```bash
[root@server1]#
```
