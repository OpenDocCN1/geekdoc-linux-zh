

# inet 服务 543

```
finger stream tcp wait root /usr/sbin/tcp
➤in.fingerd
#cfinger stream tcp wait root /usr/sbin/tcp
➤in.cfingerd
#systat tcp wait guest /usr/sbin/tcp
➤/bin/ps -auwwxx
#netstat stream tcp wait guest
/usr/sbin/tcpd /bin/netstat -f inet
```

# 认证

```
auth stream tcp wait nobody /usr/sbin/
➤in.identd in.identd -l -o
```

注意以井号（#）开头的行。这些是注释，会被 inet 服务器忽略。其余行的通用格式为：

```
service socket_type protocol wait_option userid
➤program_path arguments
```

其中：

- service 是 /etc/services 中列出的服务
- socket_type 对于 TCP 服务取值为 `page stream`，对于 UDP 服务值为 `dgram`（其他有时使用的值请参阅 `inetd.conf` 手册页）
- protocol 为 `tcp` 或 `udp`
- wait_option 等待 UDP 服务，否则为 `nowait`（其他使用的值请参阅 `inetd.conf` 手册页）
- userid 指定运行服务的用户 ID（该用户 ID 通常为 root）
- program_path 指定可执行文件的路径。（当使用 TCP wrappers 时，program_path 指定的是 `tcpd` 程序的路径，见下一节说明。）注意许多 TCP 服务的程序名以 `in.` 开头
- arguments 供程序使用

Copyright©2000 SYBEX, Inc., Alameda, CA www.syex.com

示例文件仅启用了以下服务：

- telnet
- ftp
- talk
- ntalk
- shell
- login
- finger
- auth

除 auth 之外，所有这些服务都使用 TCP wrappers 运行，它们将在下一节中进行解释。

当你修改 `inetd.conf` 文件时，必须提示 inetd 重新读取该文件。为此，请执行命令：

```
killall -HUP inetd
```

关于 inetd 的更多信息，请参阅 Terry Dawson 和 Alessandro Rubini 编写的 NET-3-HOWTO，路径为 /usr/doc/HOWTO/NET-3-HOWTO。
要直观地查看 inetd 如何工作，请完成练习 22.1。

练习 22.1

# 配置 inetd

inetdset被许多——也许是大多数——提供网络服务的 Linux 系统使用。因此，熟悉 inetd 对你来说很重要。观察 inetd 配置更改的效果，请执行以下步骤：

1. 注释掉 `inetd.conf` 中引用 telnet 的那行。
2. 提示 inetd 重新加载其配置。
3. 尝试 telnet 到本地主机。客户端请求将不会被接受。

# 练习 22.1（继续）

4. 识别 `inetd.conf` 中启用的每个服务。禁用任何实际上不需要的服务。

现在，你可以回顾该章节和其他来源来帮助你执行这些操作。但在参加 RHCE 考试之前，请确保你可以在不参考考试期间无法使用的材料的情况下操作 inetd。

# TCP Wrappers

`tcpd` 程序可以控制对在 inetd 下运行的服务的访问。要使用 `tcpd` 控制特定服务的访问，请在接收到该服务的客户端请求时，指定 `tcpd` 为应运行的程序。提供服务的程序名称（以及你想传递给程序的运行时参数）被作为 `tcpd` 命令的 `arguments` 指定。以这种方式运行的服务被称为 TCP 的。在之前给出的 `inetd.conf` 示例中，telnet 和其他服务是通过 TCP wrapper 运行的。

`tcpd` 程序使用两个配置文件：/etc/hosts.allow 和 /etc/hosts.deny。`/etc/hosts.allow` 文件包含指定服务和允许使用这些服务的主机的指令；`/etc/hosts.deny` 文件包含类似的指令，指定被禁止使用这些服务的宿机。当主机尝试访问带有 TCP wrapper 的服务时，授权过程如下：

1. 如果 `/etc/hosts.allow` 文件包含某行指定该主机允许访问该服务，则 `tcpd` 授权访问。

2. 如果 `/etc/hosts.deny` 文件包含某行指定该主机被禁止访问该服务，则 `tcpd` 拒绝访问。

3. 在所有其他情况下，`tcpd` 授权访问。

# /etc/hosts.allow 文件

如前所述，如果 `/etc/hosts.allow` 文件包含某行指定该主机允许访问某服务，则 `tcpd` 授权访问。文件中的行通用格式为：

```
service: host_list
```

其中 *service* 标识一个与 `/etc/inetd.conf` 和 `/etc/services` 文件相同名称的服务，而 *host_list* 指定一个或多个允许访问该服务的主机。每个主机之间用逗号隔开。
主机可以通过以下任一方式进行指定：

- 通过 IP 地址，例如 192.168.1.1
- 作为网络地址/子网掩码对，例如 192.168.1.0/255.255.255.0

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_558_0.png)

你也可以通过指定一个不完整的 IP 地址后跟一个点来指定地址范围。例如，`192.168.1.` 指的是与 `192.168.1.0/255.255.255.0` 相同的 IP 地址范围。

- 通过主机名，例如 www.example.com
- 通过域名或子域名，例如 .example.com（注意开头的点）
- 通过关键字 `LOCAL`，表示本地主机

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_558_1.png) 由于实现上的特性，关键字 `LOCAL` 匹配任何不带点的主机名。例如，`LOCAL` 将匹配 `/etc/hosts` 中输入的不带点的主机名。如果你使用关键字 `LOCAL`，请确保不会无意中给非本地主机特权。

- 通过关键字 `ALL`，表示所有主机

你可以使用关键字 `EXCEPT` 指定通用规则的例外。例如，指令 `inftpd: ALL EXCEPT 192.168.1.0/192.168.1.255` 指定 192.168.1.0 到 192.168.1.255 范围内的所有主机之外均访问 FTP 服务。你可以使用 `ALL` 和 `EXCEPT` 关键字指定服务以及主机。例如，指令 `ALL EXCEPT in telnetd: www.example.com` 指定主机 www.example.com 可以访问除 telnet 外的所有服务。

# /etc/hosts.deny

portmap 服务配置为使用 TCP wrappers，尽管它在 `inetd.conf` 文件中被提到。然而，你不能使用主机或域名来指定对 portmap 服务的访问；仅使用 IP 地址或关键字 `ALL AND EXCEPT`。
如前所述，如果 `/etc/hosts.allow` 文件包含某行指定主机允许访问某服务，则 `tcpd` 授权访问。文件中的行通用格式为：

```
service: host_list
```

其中 *service* 标识与 `/etc/inetd.conf` 和 `/etc/services` 文件相同名称的服务，*host_list* 指定一个或多个允许访问服务的主机。每个主机之间用逗号隔开。
主机可以通过以下任一方式指定：

- 通过 IP 地址，例如 192.168.1.1
- 作为网络地址/子网掩码对，例如 192.168.1.0/255.255.255.0

你也可以通过指定一个不完整的 IP 地址后跟一个点来指定地址范围。例如，`192.168.1.` 指的是与 `192.168.1.0/255.255.255.0` 相同的 IP 地址范围。

- 通过主机名，例如 www.example.com
- 通过域名或子域名，例如 .example.com（注意开头的点）
- 通过关键字 `LOCAL`，表示本地主机

由于实现上的特性，关键字 `LOCAL` 匹配任何不带点的主机名。例如，`LOCAL` 将匹配 `/etc/hosts` 中不带点的主机名。如果你使用关键字 `LOCAL`，请确保不会无意中给非本地主机特权。

- 通过关键字 `ALL`，表示所有主机

你可以使用关键字 `EXCEPT` 指定通用规则的例外。例如，指令 `inftpd: ALL EXCEPT 192.168.1.0/192.168.1.255` 指定 192.168.1.0 到 192.168.1.255 范围内的所有主机之外均访问 FTP 服务。你可以使用 `ALL` 和 `EXCEPT` 关键字指定服务以及主机。例如，指令 `ALL EXCEPT in telnetd: www.example.com` 指定主机 www.example.com 可以访问除 telnet 外的所有服务。

# /etc/hosts.deny（重复部分说明）

尽管在 `inetd.conf` 文件中提到了，但 portmap 服务被配置为使用 TCP wrappers。然而，你不能使用主机或域名来指定对 portmap 服务的访问；仅使用 IP 地址或关键字 `ALL AND EXCEPT`。
如前所述，如果 `/etc/hosts.allow` 文件包含某行指定主机允许访问某服务，则 `tcpd` 授权访问。文件中的行通用格式为：

```
service: host_list
```

其中 *service* 标识与 `/etc/inetd.conf` 和 `/etc/services` 文件相同名称的服务，*host_list* 指定一个或多个允许访问服务的主机。每个主机之间用逗号隔开。
主机可以通过以下任一方式指定：

- 通过 IP 地址，例如 192.168.1.1
- 作为网络地址/子网掩码对，例如 192.168.1.0/255.255.255.0

# 检查 TCP Wrappers

TCP wrappers 背后的正向/负向逻辑很容易让人困惑。`tcpcdchk` 命令可以帮助你确定配置正确的 TCP wrappers。执行命令：

```
tcpcdchk -v
```

命令将通过列出你指定的规则来响应，如下：

Using network configuration file: /inetd.conf

```
>>> Rule /etc/hosts.allow line 6:
daemons:     ALL
clients:    .apu.edu 216.126.187.224 127.0.0.
access:     granted
```

你可以检查输出以确定 tcpd 是否以你相同的方式理解你的。另一个有命令是 `tcpdmatch`。执行格式为 `tcpdmatch service host`，其中 `service` 指定配置为使用 TCP wrappers 的服务，`host` 指定真实的或假设的主机。该命令确定你的配置是否允许主机访问指定的服务并报告结果。以下是此类结果的示例：

```
tcpdmatch in.ftpd www.example.net
client: address 192.168.1.1
server: process in.ftpd
access: granted
```

# 使用 twist 替换服务

`twist` 指令用于替换请求服务的替代服务。例如，`/etc/hosts.allow` 中的行：

```
in.telneted: .example.net : twist /usr/local/sbin/telneted
```

为 example.net 域名内的主机用 `/usr/local/sbin/telneted` 程序替换通常的 telnet 服务。
你也可以在 `/etc/hosts.deny` 文件中使用 `twist` 指令。例如，指令：

```
in.telneted: .example.net : twist /bin/echo Hosts from
example.net not welcome
```

为 example.net 域名内的主机显示自定义的拒绝欢迎消息。

