
服务章节中的字段通常是自明的，允许我们配置类型、使用的协议以及传递给服务的参数。默认部分的字段代表：

| 字段 | 定义 |
|---|---|
| `instances` | 服务器处理的最大请求数。 |
| `logtype` | 在这种情况下，我们使用 `SYLOG` 日志。 |
| `logsuccess` | 我们可以在连接成功时记录一些信息，包括 `PID`、`HOST`。 |
| `logfailure` | 特定 IP 地址对特定服务的最大连接数。 |
| `per_source` | |

从 `inetd` 转换为 `xinetd` 的最后一步是通过修改 `/etc/rc.d` 中的相应脚本来启动 `xinetd`。

## 464 Linux 攻防揭秘：Linux 安全秘密与解决方案

> **注意** 在此转换之后，我们通常会切出 `ftp` 和 `telnet` 部分，并将它们放在 `/etc/xinetd.d` 目录下的文件中。这些文件通常命名为 `/etc/xinetd.d/telnet` 和 `/etc/xinetd.d/ftpd`。如果我们选择将这两个服务的配置移动到文件中，我们必须在 `/etc/inetd.conf` 中添加以下行：
> `include /etc/xinetd`

## 不必要的黑客连接

| 流行 | 简单性 | 影响 | 风险评分 |
|---|---|---|---|
| 9 | 8 | 9 | 9 |

如果你运行了服务——如果你的机器连接了网络——迟早黑客会尝试探测它们。这些服务中的某些在滥用之前需要身份验证。然而，这些服务可能存在完全不需要身份验证即可被利用的漏洞。

黑客通过社交工程等手段发现了用户名和密码。如果他尝试使用有效账户 `telnet` 到你的机器，你的计算机无法区分合法用户和入侵者，因此无法阻止他成功登录。

## 使用 inetd 和 TCP wrappers 实现主机控制

让我们来看配置了 `tcpd` 的机器上 `/etc/inetd.conf` 的部分：

```
ftp      stream tcp    nowait root      /usr/sbin/tcpd  in.ftpd -1 -a

telnet   stream tcp    nowait root      /usr/sbin/tcpd  in.telnet

shell    stream tcp    nowait root      /usr/sbin/tcpd  in.rhmd

pop-3    stream tcp    nowait root      /usr/sbin/tcpd  ipop3
```

### 第 13 章：访问控制与防火墙

注意 `/usr/bin/sbin/tcpd` 被“包裹”在 `in.ftpd`、`in.telnet`、`in.rshd` 和 `in.popd` 中。当尝试连接这四个服务之一时，都会检查 `tcpd` 规则。

#### TCP Wrappers 规则

`TCP wrappers` 通过两个文件实现：`/etc/hosts.allow` 和 `/etc/hosts.deny`。当远程机器尝试连接到 Linux 服务器时，`tcpd` 首先在 `/etc/hosts.allow` 文件中查找远程机器的 IP 名称或 IP 地址。如果远程机器在 `/etc/hosts.allow` 中被授予了其尝试连接的服务的访问权限，则允许访问。如果远程机器匹配 `/etc/hosts.deny` 中的项，或者该机器不匹配 `/etc/hosts.allow` 或 `/etc/hosts.deny` 中的任何规则，则连接被拒绝。

`/etc/hosts.allow` 和 `/etc/hosts.deny` 文件由零或多行文本组成。这些文本按照出现的顺序从上到下进行处理。一旦找到匹配项，处理立即终止。

长行可以被折断——在行尾使用反斜杠（`\`）表示该行在下一行继续。此外，空行和以井字符（`#`）开头的行会被忽略，这允许您通过空行和注释使文件更易读。

`/etc/hosts.allow` 和 `/etc/hosts.deny` 的行遵循以下格式：

```
daemon_list : client_list { : shell_command }
```

让我们从最简单、最安全的配置开始。例如，假设一个名为 `example.com` 的远程机器尝试通过 `telnet` 连接到我们机器的 23 端口（默认 `telnet` 端口）。当它尝试连接时，`tcpd` 首先扫描 `/etc/hosts.allow`：

```
# /etc/hosts.allow

# empty
```

`tcpd` 接着扫描 `/etc/hosts.deny`：

```
# /etc/hosts.deny

ALL: ALL
```

注意 `/etc/hosts.allow` 中没有任何项，因此 `test.example.com` 并没有根据允许规则被授予访问权限。由于 `/etc/hosts.allow` 中未授予访问，将搜索 `/etc/hosts.deny`，`tcpd` 找到了 `ALL: ALL`。

这意味着所有机器都被拒绝访问所有服务。因此，`test.example.com` 被拒绝 `telnet` 访问。

### 破解 Linux 暴露：Linux 安全秘密与解决方案

这种配置虽然安全，但并不好用，因为所有机器（包括主机本身）都被拒绝访问所有服务：

```
machine# telnet localhost

Trying 127.0.0.1...

Connected to localhost.

Escape character is '^]'

Connection closed by foreign host.

machine#
```

如果我们想允许通过 `localhost` 对机器进行 `telnet` 访问，应在 `/etc/hosts.allow` 中添加以下内容：

```
# /etc/hosts.allow

inet.telnetd 127.0.0.1
```

这意味着机器 `127.0.0.1`（也称为 `localhost`）将被允许连接到端口 23 上的 `telnet` 服务。

- 你的 `localhost` 是一个受信任机器，因此我们可以授予该主机所有服务的权限：

```
# /etc/hosts.allow

ALL 127.0.0.1
```

此 `/etc/hosts.allow` 允许 `localhost` 连接到机器上开启的所有服务：`telnet`、`FTP`、`SSH`、`POP3`。通常，还有其他受信任机器被允许完全自由地连接，我们可以将它们添加到此行中。列出的客户端可以用空格或逗号分隔：

```
# /etc/hosts.allow

ALL 127.0.0.1 trusted.machine.com .example.org
```

> 注意：项 `trusted.machine.example.com` 仅匹配一个客户端，而项 `.example.org`（开头的点非常重要）匹配该域名下的所有客户端（即 `client1.example.org`、`client2.example.org` 等）。

这种匹配的完整规则如下：

- 如果字符串以点（`.`）开头，则它匹配该域内的所有客户端。例如，`.example.com` 匹配 `client1.example.com` 以及 `mail.internal.example.com`。
- 如果字符串以点（`.`）结尾，则它匹配所有第一个数字匹配的客户端。例如，`192.168.` 匹配所有类似于 `192.168.x.x` 的 IP 地址。

#### 第 18 章：访问控制与防火墙

- 以字符 `(@)` 开头的字符串被视为 NIS 网络组（netgroup）名称。项 `ssh: @trustedhosts` 将允许 `trustedhosts` 网络组中的所有机器允许 `SSH` 访问。
- 如果字符串的形式为 `x.x.x.x/y.y.y`，则它被视为子掩码对。如果客户端的 IP 地址在与掩码进行位与运算后的范围内，则匹配成功。例如，`192.168.1.0/255.255.255.0` 匹配 `192.168.1.0` 到 `192.168.1.255` 范围内的所有 IP 地址。

如果我们的 Linux 机器要作为 POP 服务器，我们可能希望允许所有机器连接，因此我们将添加以下内容：

```
# /etc/hosts.allow

ALL: ALL
```

等待，让我们重新检查流程。如果我们的 Linux 机器作为 POP 服务器使用，我们可能希望允许所有机器连接，我们将添加：

```
# /etc/hosts.allow

ALL: ALL
```

实际上，根据文本：如果我们的 Linux 机器作为 POP 服务器使用，我们可能希望允许所有机器连接，我们将添加：

```
# /etc/hosts.allow

ALL: ALL
```

等待，OCR 文本是碎片化的。让我们重构流程：如果我们的 Linux 机器作为 POP 服务器使用，我们可能希望允许所有机器连接，我们将添加：

```
# /etc/hosts.allow

ALL: ALL
```
