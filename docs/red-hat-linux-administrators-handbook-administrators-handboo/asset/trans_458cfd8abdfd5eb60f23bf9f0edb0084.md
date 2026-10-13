
## Listing 15-2 续

```
linuxconf stream tcp wait root /bin/linuxconf linuxconf -
-http
#
# End of inetd.conf
```

正如许多其他 UNIX 配置文件一样，以 # 字符开头的行被视为注释，并连同空行一起被忽略。

每一行配置的格式如下：

```
service_name sock_type proto flags user server_path args
```

service_name 字段与 /etc/services 文件中指定的服务名称相匹配。以下是一个示例：

```
finger stream tcp nowait root /usr/sbin/tcpd in.fingerd
```

/etc/services 文件将 finger 服务映射到 TCP 端口 79。当 inetd 在 TCP 端口 79 上收到连接请求时，它会使用 in.fingerd 参数启动 /usr/sbin/tcpd 服务。tcpd 程序被称为 TCP wrapper，它启动 in.fingerd finger 服务器。finger 服务器按其认为合适的方式响应请求。

## 从 /etc/inetd.conf 中移除不必要的服务

默认的 /etc/inetd.conf 可能并不适合你的需求。浏览此文件，删除或注释掉任何你不想向任何人提供的服务。例如，前面默认安装的 /etc/inetd.conf 文件启用了 FTP、Telnet、Gopher、远程 shell（rsh）、远程登录（rlogin）、远程执行（rexec）、talk、ntalk、POP2、POP3、IMAP、finger、time（tcp）、time（udp）、auth（ident）以及 linuxconf 的 Web 服务。这几乎相当于让系统完全暴露在攻击之下。通过 inetd 可用的任何服务都是潜在攻击的开放入口。在我的 Web 服务器系统上，我只保留 FTP、Telnet 和 POP3 服务，因为这些是用户使用的。因此，我的 Red Hat Linux 服务器上的 /etc/inetd.conf 看起来像这样：

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
-l -a
```

```
telnet stream tcp nowait root /usr/sbin/tcpd
in.telnetd
```

```
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
```

弄清楚你必须保留哪些服务，哪些可以不用。修改 /etc/inetd.conf 后不要忘记重启 inetd 服务。你可以使用 killall -HUP inetd 命令来重启它。

## 使用 TCP wrapper 保护 inetd 运行的服务

/etc/inetd.conf 中的配置行表明每一行的 server_path 部分始终为 /usr/sbin/tcpd，而实际的服务器程序是 tcpd 程序的参数。例如，

```
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
```

在功能上等同于以下行：

```
pop-3 stream tcp nowait root /usr/sbin/ipop3d
```

当 inetd 收到 POP3 请求时，两种情况下都会启动 ipop3d 服务器，但第一个更安全，因为 tcpd 程序是 TCP wrapper 程序，通过提供以下服务来增强安全性：

- Logging service. Logs information about a request by using the syslog facility.
- Host-based access control. Provides host-based access control by using pattern matching.
- Host name and address verification service. Detects spoofing of host names or addresses when a host is pretending to be some other host.

TCP wrapper 足够重要，以至于它作为默认 Red Hat Linux 安装的一部分提供。没有任何理由不将你的每个 inetd 服务用 TCP wrapper 包裹起来。

![](img/c2419364ebb911c809b6a79991707c27_470_0.png)

## 注意

默认情况下，Red Hat Linux 不使用 tcpd 包裹 linuxconf 的 Web 服务，因为它似乎在用 tcpd 包裹时无法工作。这是一个非常好的理由不要运行 linuxconf Web 服务。

## 通过 TCP wrapper 限制主机访问

如前所述，TCP wrapper 在控制 Internet 主机（或 IP 地址）级别的访问方面提供了很大的灵活性。这种灵活性在配置紧密的服务器系统时非常有用。本节讨论一个紧密控制的系统的示例，该系统基于我每天使用的系统。

首先，确定示例控制配置的目标。假设你想要创建一个 Internet Web 服务器系统，只允许 Telnet、FTP、POP3 和 HTTP 服务。由于 Web 服务（HTTP）通常是高需求服务，它不通过 inetd 运行。假设 Web 服务器是 Apache 并且作为独立服务运行。因此，inetd 将管理其余服务。此外，假设你只想将 Telnet、FTP 和 POP3 访问限制为网络地址为 206.171.50.0 的单个网络。

Listing 15-3 显示了此示例所需的 /etc/inetd.conf 文件。

## Listing 15-3 /etc/inetd.conf 文件

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
-l -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
in.telnetd
pop-3 stream tcp nowait root /usr/sbin/tcpd in.pop3d
```

如你所见，所有三个服务都用 tcpd wrapper 包裹。现在，你需要通过 /etc/hosts.allow 和 /etc/hosts.deny 文件来限制对这些服务的访问。/etc/hosts.allow 文件用于指定哪些主机允许访问 inetd 服务，而 /etc/hosts.deny 文件用于指定哪些主机不允许访问 inetd 服务。这两个文件使用相同的配置格式，如下所示：

```
daemon list : client list [ : shell command ]
```

daemon list 是一个或多个服务进程名称的列表。例如，in.ftpd、in.telnetd 和 in.pop3d 是此示例的守护进程名称。client list 由一个或多个主机名或 IP 地址组成。你可以在 daemon 和 client 列表中同时使用表 15-6 中显示的通配符。

## 表 15-6 /etc/hosts.allow | deny 文件中守护进程和客户端列表的通配符

| Wildcard | Meaning |
|---|---|
| ALL | Always matches. |
| LOCAL | Matches a local host name such as wormhole, but not wormhole.nitec.com |
| UNKNOWN | Matches when the host name or IP address is unknown due to a problem. |
| KNOWN | Matches when a host or IP address is known. |
| PARANOID | Matches a host that does not match its IP address. This works only if the tcpd wrapper program is not built with the -DPARANOID option at compilation. |

你也可以使用以下模式：

- ‘.nitec.com’ matches a host name such as wormhole.nitec.com or picaso.nitec.com. In other words, when a leading dot is used in a pattern, it can be matched from the right side of the host name.
- ‘206.171.50.’ matches any hosts with addresses in the range of 206.171.50.0 to 206.171.50.255. In other words, when a trailing dot is used in a pattern, the matching is done from the left.
- ‘206.171.50.0/255.255.255.0’ matches any hosts with addresses in the range of 206.171.50.0 to 206.171.50.255. The pattern is treated as a network/netmask definition.

此外，如果你计划使用 shell 命令执行某些操作，请利用表 15-7 中显示的字符扩展。

## 表 15-7 Shell 命令的字符扩展

| Character | Expanded Meaning |
|---|---|
| %a | The IP address of the client trying to access a service |
| %A | The IP address of the server |
| %c | Client information such as host name or IP address, or user@host or user@ip_address, etc. |
| %d | The name of the daemon or service |
| %h | The host name of the client trying to access a service |
| %H | The host name of the server |
| %p | The process ID (PID) of the daemon or service |
| %s | Server information such as host name or IP address, or user@host or user@ip_address, etc. |
| %u | The client username, if known; otherwise, set to unknown |
| %% | The % character |

由于此示例的目标是禁止除属于 206.171.50.0 网络的主机之外的所有主机，你可以创建如 Listing 15-4 所示的 /etc/hosts.deny 文件。

## Listing 15-4 /etc/hosts.deny 文件

```
#
# hosts.deny  This file describes the names of the
# hosts that are not allowed to use the local INET
# services, as decided by the /usr/sbin/tcpd program.
#
# Deny all daemon access to all hosts.
#
ALL : ALL
```

/etc/hosts.deny 文件设置为拒绝所有主机。单行配置 ALL : ALL 告诉 TCP wrapper（tcpd）拒绝 ALL 守护进程对 ALL 主机的访问。如果保持原样并且系统中不存在 /etc/hosts.allow 文件，则没有任何主机能够访问三个 inetd 运行的服务（Telnet、FTP 和 POP3）。因此，你必须在 /etc/hosts.allow 文件中允许特定主机，特别是 206.171.50.0 网络，访问这些服务。这在 Listing 15-5 中完成。

## Listing 15-5 /etc/hosts.allow 文件

```
#
# hosts.allow  This file describes the names of the
# hosts that are allowed to use the local INET
```
