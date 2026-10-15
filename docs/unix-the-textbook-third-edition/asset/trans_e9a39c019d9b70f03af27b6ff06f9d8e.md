

## 表 20.24 /etc/inetd.conf 中行的字段及其用途

| Field | Purpose |
| --- | --- |
| Service name | A port number in decimal or name corresponding to the service as listed in the /etc/services file |
| Socket type | The type of socket that the service is offered for, usually, stream for TCP style communication or dgram for UDP style communication. It could also be raw, rdm, or seqpacket |
| Protocol | For TCP, this field is tcp or tcp6 for IPv4 and IPv6, respectively. For UDP, this field is udp or udp6 for IPv4 and IPv6, respectively. For protocols based on remote procedure call (RPC), this field may be rpc/tcp or rpc/udp |
| Wait/nowait | This field specifies if inetd should wait until the service program terminates (wait) or continue (nowait). For stream type sockets, this field is normally nowait |
| User:group | The user name and optional group name that the respective service process runs as. Most of the services run under root ownership |
| Server-program | Absolute pathname of the program that is executed for the offered service |
| Arguments | This field contains the name of the program and the arguments with which it runs |

以下是我们 BSD 系统上 /etc/inetd.conf 文件的内容。

```
% cat /etc/inetd.conf
# $FreeBSD$
#
# Internet server configuration database
#
# Define *both* IPv4 and IPv6 entries for dual-stack support.
# To disable a service, comment it out by prefixing the line
# with '#'.
# To enable a service, remove the '#' at the beginning of the
# line.
#
ftp    stream  tcp    nowait root /usr/libexec/ftpd      ftpd -l
ftp    stream  tcp6   nowait root /usr/libexec/ftpd      ftpd -l
ssh    stream  tcp    nowait root /usr/sbin/sshd       sshd -i -4
ssh    stream  tcp6   nowait root /usr/sbin/sshd       sshd -i -6
telnet stream  tcp    nowait root /usr/libexec/telnetd telnetd
telnet stream  tcp6   nowait root /usr/libexec/telnetd telnetd
... [output truncated]
%
```

请注意，第一字段中的服务名称与最后一字段中给出的程序名称不同，后者是程序（守护进程）的名称以及命令行参数，当 inetd 收到对此服务的客户端请求时该程序会被执行。任何用户都可以显示此文件的内容。

inetd 提供的一些服务被标记为“internal”。以下会话显示了我们在 BSD 系统上的此类服务。

```
% grep "internal"$ /etc/inetd.conf
daytime stream tcp nowait root internal
daytime stream tcp6 nowait root internal
daytime dgram udp wait root internal
daytime dgram udp6 wait root internal
time stream tcp nowait root internal
time stream tcp6 nowait root internal
time dgram udp wait root internal
time dgram udp6 wait root internal
echo stream tcp nowait root internal
echo stream tcp6 nowait root internal
echo dgram udp wait root internal
echo dgram udp6 wait root internal
... [output truncated]
%
```

这些服务非常简单，由 inetd 直接处理而不运行任何外部程序（守护进程）。它们可用于测试目的，但容易受到“拒绝服务”（DoS）攻击。因此，您应该通过将其注释掉来禁用它们。您可以使用 grep -v "#" /etc/inetd.conf 命令列出已启用的服务。

## 20.10.1.2 在 PC-BSD 和 Solaris 上定位 inetd 服务

/etc/services 文件是包含服务名称、服务的端口号以及其用于通信的传输层协议（通常为 tcp 或 udp）的数据库。inetd 提供的任何服务都必须在 /etc/services 文件中有一个条目。它每行一个服务，格式如下：

```
service-name port-number/protocol-name [aliases]
```

这里，service-name 是服务的名称，例如 smtp，port-number 是 IANA 分配的端口号，例如 smtp 为 25，protocol-name 是传输层协议，例如 tcp、udp 等。以下是 /etc/services 文件中的一个示例行：

```
pop3 110/tcp    #Post Office Protocol - Version 3
```

该行显示 pop3 是一个 TCP（即面向连接的）服务，在端口 110 提供。以下会话显示，我们的 PC-BSD 系统上 /etc/services 文件中 SSH 服务有三个条目。这意味着 SSH 服务在 tcp、udp 和 sctp 协议下在端口 22 上提供。流控制传输协议（SCTP）旨在在两个已连接套接字之间传输多个数据流。它也被称为“下一代 TCP”或“TCPng”。端口 614 上的 SSHELL 服务用于安全套接字层 shell（SSLshell）。

