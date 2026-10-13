
以下示例显示了用于红帽 Linux 的 `xinetd.conf` 文件：

``` 
# xinetd 的简单配置文件

# 一些默认设置，包含 /etc/xinetd.d/
```

## 第 20 章：服务器管理 375

``` 
defaults {

  instances      = 60

  log_type       = SYSLOG authpriv

  log_on_success = HOST PID

  log_on_failure = HOST

  cps            = 25 30

}
```

``` 
included /etc/xinetd.d
```

作为示例显示了 `xinetd.d` 目录中的 `swat` 文件。请注意，它默认是禁用的：

``` 
# default: off
# description: SWAT 是 Samba Web 管理工具。
# 使用 swat 配置你的 Samba 服务器。
# 要使用 SWAT，请用你喜欢的 Web 浏览器连接到端口 901。

service swat {
  port           = 901
  socket_type    = stream
  wait           = no
  only_from      = localhost
  user           = root
  server         = /usr/sbin/swat
  log_on_failure +== USERID
  disabled       = yes
}
```

### TCP Wrappers

TCP wrappers 为由 `xinetd` 管理的服务器增加了另一层安全。实际上，服务器被了一层中间安全层保护，用于监控连接并控制访问。通过 `xinetd` 建立的服务器连接会受到监控，验证远程用户的身份并确保它们是有效请求。连接将由 `syslog` 守护进程记录（在第 27 章之后），并可以在 `/var/log/secure` 这样的 `syslog` 文件中找到。通过 TCP wrappers，你还可以限制远程主机对你系统的访问。主机列表保留在 `.allow` 和 `.deny` 文件中。这些文件格式为 `服务主机名:域名`。域名是可选的。对于服务，你可以指定特定服务（如 FTP），或输入 `ALL` 使用通配符来匹配多个服务。对于主机名，你可以指定特定主机或多个主机。例如，`ALL` 将匹配所有主机。表 20-7 列出了可用的通配符。在下文中，第一个条目允许所有主机访问 Web 服务 `http`。第二个条目允许 `pangol.train.com` 主机访问所有服务。第三和第四个条目允许 `rabbit.trek.com` 和 `sparrow.com` 的 FTP 访问：

```
http:ALL
pangol.train.com
ftp:rabbit.trek.com
ftp:sparrow.com
```

| 通配符 | 描述 |
| --- | --- |
| ALL | 匹配所有主机或服务。 |
| LOCAL | 匹配仅指定主机名而不带域名的主机。用于匹配本地域内的主机。 |
| UNKNOWN | 匹配名称或地址未知的用户或主机。 |
| KNOWN | 匹配名称或地址已知的用户或主机。 |
| PARANOID | 匹配主机名与其 IP 地址不匹配的主机。 |
| EXCEPT | 运算符允许你提供匹配的例外。其形式为 `list1`，其中 `list1` 中匹配的主机在 `list2` 中匹配并被排除。 |

`hosts.allow` 文件持有你允许访问的主机。如果你想允许除少数特定主机以外的所有主机访问，可以在 `hosts.allow` 文件中指定 `ALL`，但在 `hosts.deny` 文件中列出它们。使用 IP 地址代替主机名更安全，因为主机名可能会被 DNS 欺骗。当 `xinetd` 接收到请求时，TCP wrapper 会监控连接并启动 FTP 服务器。要允许该服务的请求，可以在 `/etc/hosts.allow` 中输入：

```
ftp:ALL
```
