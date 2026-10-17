
```
  user = root

  server = /usr/sbin/in.ftpd

  server_args = -1 -a

}
service telnet
{
  flags = REUSE NAMEINARGS
  socket_type = stream
  protocol = tcp
  wait = no
  user = root
  server = /usr/sbin/in.telnetd
  server_args = 
}
```

`defaults` 部分的字段代表以下含义：

| 字段 | 定义 |
| --- | --- |
| instances |此值是服务器可以同时处理的请求最大数。 |
| log_type | 在这种情况下，我们将日志记录到文件中，xinetd 同时也允许使用 SYSLOG。 |
| log_on_success / log_on_failure | 我们可以选择连接成功或失败时记录几条信息，包括 PID、HOST 和 USERID。 |
| per_source |此值是来自特定 IP 地址到某个服务的最大连接数。 |

`service` 部分的字段通常是自显其懂的，允许我们配置套接字类型、使用的协议、执行服务的用户以及传递给服务的参数。

在完成此转换后，我们通常会切出 ftp 和 telnet 部分，并将它们放在 `/etc/xinetd.d` 目录下的独立文件中。这些文件通常命名为 `/etc/xinetd.d/telnet` 和 `/etc/xinetd.d/wu-ftpd`。如果我们选择将这两个服务的配置移动到该目录下的文件中，我们必须在 `/etc/xinetd.conf` 中添加以下行：
`includedir /etc/xinetd.d`

从 inetd 到 xinetd 转换的最后一步是通过修改 `/etc/rc.d` 中的相应脚本来执行重启。

# 不需要的黑客连接

| 流行度: | 9 |
| --- | --- |
| 简单性: | 8 |
| 影响力: | 9 |
| 风险等级 | 9 |

如果你有正在运行的服务——如果你的机器连接了网络，你很可能是这样——那么早晚，黑客都会尝试探测这些服务。其中某些服务在被滥用之前需要身份验证。然而，这些服务可能存在无需任何身份验证即可被利用的漏洞。

也许黑客已经通过其他其他手段（如社会工程学）发现了有效的用户名和密码。如果她尝试用有效账户 telnet 到你的机器，你的计算机无法区分合法用户和入侵者，因此无法阻止她成功登录。

# 使用 inetd 和 TCP Wrappers 实现访问控制

TCP wrappers 是由 Wietse Venena 编写的，其意义在于，由于 TCP wrapper 守护进程 `tcpd` 正如 `/etc/inetd.conf` 所示，它被“包裹”在服务周围。`tcpd` 会干预连接，并验证尝试连接的主机是否允许连接到该主机上的服务。`tcpd` 通过将请求与主机上定义的规则（定义在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中，在本章稍后会详细讨论）对比来验证这一点，如果请求通过了规则，则允许连接。如果请求未通过规则，则拒绝连接。

让我们看看安装了 `tcpd` 的机器上的 `/etc/inetd.conf` 部分内容：

```
ftp      stream tcp    nowait root    /usr/sbin/tcpd in.ftpd -1 -a
telnet   stream tcp    nowait root    /usr/sbin/tcpd in.telnetd
shell    stream tcp    nowait root    /usr/sbin/tcpd in.rshd
pop-3    stream tcp    nowait root    /usr/sbin/tcpd ipop3d
```

# 第 13 章：访问控制与防火墙

注意 `/usr/sbin/tcpd` 被“包裹”在 `in.ftpd`、`in.telnet`、`in.rsh` 中，当尝试连接这四个服务之一时，将会检查 `tcpd` 规则。

# TCP Wrappers 规则

TCP wrappers 使用两个文件实现：`etc/hosts.allow` 和 `/etc/hosts.deny`。当远程机器尝试连接到 Linux 服务器时，`tcpd` 首先在 `/etc/hosts.allow` 文件中查找机器的 IP 名称或 IP 地址。如果远程机器在 `/etc/hosts.allow` 中被授予访问其尝试连接的服务，则授予访问。如果远程机器匹配 `/etc/hosts.deny` 中的条目，则被拒绝访问。如果机器不匹配 `/etc/hosts.allow` 或 `/etc/hosts.deny` 中的任何规则，则允许连接。

`/etc/hosts.allow` 和 `/etc/hosts.deny` 文件由零行或多行文本组成。这些文本行按照出现的顺序从上到下进行处理。一旦找到匹配项，处理就会终止。

长行可以折断——以反斜杠 (`\`) 结尾表示它在下一行继续。此外，空行和以井号 (`#`) 开头的行会被忽略，这允许你通过空行和注释使文件更易读。

`/etc/hosts.allow` 和 `/etc/hosts.deny` 的行遵循以下格式：

```
daemon_list : client_list [ shell_command ]
```

`ALL` 是一个通配符。TCP wrappers 支持以下通配符：

- `ALL` 匹配所有客户端。
- `LOCAL` 匹配任何不包含点号 (`.`) 的客户端。
- `UNKNOWN` 匹配任何名称或地址未知的客户端（谨慎使用！）。
- `KNOWN` 匹配任何名称和地址已知的客户端（谨慎使用：由于主机问题可能暂时不可用）。
- `PARANOID` 匹配任何名称与其地址不匹配的客户端。

因此，为了防止 telnet 攻击，在 `/etc/hosts.deny` 中设置 `ALL: ALL` 将拒绝黑客的 telnet 连接。如果有允许使用 telnet 连接，我们可以在 `/etc/hosts.allow` 文件中添加此内容：

```
telnet: server1.example.com
```

# 使用 xinetd 进行主机访问控制

xinetd 的最重要的改进之一是它不再需要使用 TCP wrappers，因为访问控制已内置在 xinetd 中。可以对服务进行以下访问控制：

- 与 TCP wrappers 类似的控制：
基于 IP 地址的控制
基于 IP 名称的控制
基于域名的控制

访问时间控制（例如，你可以将 ftp 访问限制在早上 8 点到下午 5 点）。

在前面的使用 `inetd` 控制主机的示例中，`/etc/hosts.deny` 的内容拒绝所有客户端的所有服务：

`ALL: ALL`

而 `/etc/hosts.allow` 允许所有这些服务：

```
ALL: 127.0.0.1 trusted.machine,example.com .example.com
ipop3d: ALL
telnetd: server1.example.com
```
