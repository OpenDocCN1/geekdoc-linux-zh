
`linuxconf stream tcp wait /bin/linuxconf --http`

第一行取消注释显示 `ppd` 进程受 `inetd` 控制。要找到它在哪个端口等待输入，请查看 `/etc/services` 文件。该文件每个服务至少有一行，列出了其名称、端口以及它使用的任何别名。

`FTP` 服务具有以下 `/etc/services` 条目：

`ftp 21/tcp`

这告诉我们 `FTP` 服务运行在端口 21。许多服务有两个条目分别对应 `TCP` 和 `UDP` 协议。下面的行表示 `http` 进程通过端口 80。

| www | 80/tcp | Wide HTTP |
|---|---|---|
| www | 80/udp | HyperText Protocol |

关闭任何你不打算使用的服务是一个好主意；在 `/etc/inetd.conf` 中对应该服务的每行开头添加井号（`#`）。`chkconfig`

通过 `inetd` 控制的服务外，许多服务器直接使用超级服务器运行端口。你可以像第 5 章描述的那样通过启动脚本来关闭它们。

# TCP Wrappers

`TCP Wrappers` 是一种基于主机的安全层，适用于守护进程。你可能在上面的 `/etc/hosts.conf` 中注意到 `tcpd` 可执行文件是一个检查指定服务是否应该运行的封装程序。当 `xinetd` 启动 `tcpd` 时，它读取 `/etc/hosts.allow`，然后是 `/etc/hosts.deny`。`xinetd` 是 `inetd` 和 `TCP Wrappers` 的替代品。`Red Hat Linux 7.0` 和 `Mandrake Linux 7.2` 已切换到 `xinetd`。`xinetd` 将在第 15 章讨论。

# 防御网络入侵

`/etc/hosts.allow` 是 `tcpd` 程序的配置文件。该文件包含允许哪些主机访问本地服务的规则。格式如下：

```
service_list: host_list: [optional_command]
```

服务列表是应用于此规则的服务名称逗号分隔列表。也可以使用关键字 `ALL` 或 `EXCEPT`。例如，以下条目允许所有用户使用所有本地服务，`FTP` 除外：

```
ALL EXCEPT in.ftpd: ALL
```

主机列表是逗号分隔的主机名列表。主机名可以表示为 `IP` 地址、特定主机名或带有通配符的主机以便匹配。如果主机名以点开头，所有共享该字符的主机都匹配此规则。例如，下面的行将匹配来自 `somedomain.com` 网络计算机的 `Telnet` 尝试。

```
in.telnetd:.somedom.com
```

如果使用数字，可能是特定机器的完整 `IP` 地址，也可能由前三个分隔数字组成，导致匹配任何以这三个数字开头的 `IP`。主机列表可能包含这些关键字：`ALL`、`LOCAL`、`PARANOID` 和 `EXCEPT`。`ALL` 关键字将导致所有主机匹配。`LOCAL` 关键字允许任何本地登录匹配。`PARANOID` 关键字意味着任何被伪造的主机都会匹配。`EXCEPT` 关键字通常与 `ALL` 结合使用，如例所示：

```
ALL EXCEPT hostname
```

这将匹配除列出主机外的每一个主机。该主题的另一种变体允许规则包含如下形式的表达式：

```
12.34.56.0/255.255.254
```

这将被解释为网络/掩码对，如果网络部分等于地址和掩码部分的位与与的结果，则将匹配。因此，它允许任何从 `12.34.56.0` 到 `12.34.57.255` 之间的地址访问系统。可选参数标识要运行的命令。

该命令将返回一个明确允许或拒绝的访问列表，包括访问相关的守护进程（`daemon`）、访问相关的客户端（`client`）以及实际的访问判定。这是一个示例：

```
>>> Rule /etc/hosts.allow line 18:

daemons:  in.telnetd

clients: .ntrnet.net

access:  granted
```

另一个工具是 `tcpmatch` 实用程序，允许你对特定的守护进程和客户端进行测试。命令如下：

```
# tcpmatch in in.telnetd www.macrosoft.com
```

如果允许访问，命令将返回以下内容：

```
client:  hostname www.macroshaft.com

client:  address  117.4.137.45

server:  process   in.telnetd

access:  granted
```

如果主机被拒绝访问，响应将如下：

```
client:  hostname www.macroshaft.com

client:  address  117.4.137.45

server:  process   in.telnetd

matched: /etc/hosts.deny line 10

access:  denied
```

一旦用户获得了访问，`TCP Wrappers` 软件包为你的系统提供了相当的保护。然而，仅靠拒绝服务是不够的。

## xinetd

从 `Red Hat 7.0` 开始，`inetd` 不再默认安装。相反，它使用了更安全的扩展互联网服务守护进程（`xinetd`）。其他发行版也在切换到 `xinetd`。`xinetd` 和 `inetd` 可以在系统中并发运行。事实上，`xinetd` 代码的作者建议运行 `RPC` 服务的管理员通过 `inetd` 运行。你可以使用你的 `inetd.conf` 为非 `RPC` 服务创建一个 `xinetd.conf`。

![image](img/4fb617eb648f87def380ef5d92052d01_260_0.png)

## 第 7 章 安全

在 `Red Hat 7.0` 系统上，`/usr/sbin/inetdconvert` 是一个 `Python` 脚本，它能将你的 `inetd.conf` 文件转换为新 `/etc/inetd.d` 目录下的多个文件。使用此工具转换所有尚未转换服务的命令是：

```
# inetdconvert --convertremaining
```

一个用于将 `inetd.conf` 脚本转换为 `xinetd.conf` 文件的 `Perl` 脚本包含在 `xinetd` 软件包的其他版本中，位于与二进制文件相同的目录下。如果该脚本存在于你的系统中，它将位于 `/usr/sbin`，你可能需要使用以下命令运行它（假设可执行文件位于 `/usr/sbin`）：

```
# /usr/sbin/xconv.pl < /etc/xinetd.conf > /tmp/xinetd.conf
```

转换在 `/etc/xinetd.d` 目录下创建了几个文件。这些文件包含了由 `xinetd` 管理的服务的配置选项，因此你需要编辑这些文件来配置 `xinetd` 以按照你想要的方式处理这些服务。例如，列表 7.9 显示了 `/etc/xinetd.d/telnet` 文件，它配置了 `Telnet` 服务。

### 列表 7.9 `/etc/xinetd.d/telnet` 文件配置了 `Telnet` 服务，是单个服务 `xinetd` 文件的典型示例。

```
# default: on

# description: The telnet server serves telnet sessions, it uses \

# encrypted username/password pairs for authentication.

service telnet {

    flags = REUSE NAMEINARGS

    socket_type = stream

    wait = no

    user = root

    server = /usr/sbin/in.telnetd

    log_on_failure += USERID

}
```

来自 `inetd.conf` 的条目处理 `Telnet` 服务实际上包含了大部分相同的信息：

```
telnet stream nowait root /usr/sbin/tcpd.telnetd
```
