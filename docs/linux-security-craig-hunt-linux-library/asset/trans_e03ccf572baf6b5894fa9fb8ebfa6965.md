

## 表 4.3 TCP Wrappers 配置：Shell 命令展开（续）

| 模式 | 含义 |
| :------- | :------- |
| %h | 服务器主机名 |
| %p | 守护进程 ID |
| %d | 守护进程名称 (argv[0]) |

### TCP Wrapper 配置示例

以下命令展示了 TCP Wrappers 的一些访问控制配置。这是一个有限的配置设置，其中您拒绝所有访问，除了对 `finger` 守护进程（完全开放）的访问以及对 `telnet` 守护进程（仅限本地主机、`.sybex.com` 域内的主机以及 `192.168.0.0/16` 网段内的主机）的访问。

```text
[ramon]$ more /etc/hosts.allow
in.fingerd:ALL
in.telnetd:LOCAL, .sybex.com, 192.68.
[ramon]$ more /etc/hosts.deny
ALL: ALL
```

下一个示例与前面的示例类似；它采取全部拒绝的立场，但允许除主机 `badguy.example.com` 以外的任何地方进行 `ftp` 连接。

```text
[ramon]$ more /etc/hosts.allow
in.ftpd:ALL EXCEPT badguy.example.com
[ramon]$ more /etc/hosts.deny
ALL: ALL
```

以下示例是一个带有“陷阱”的简单配置。您允许来自内部主机的所有流量访问所有服务器。您禁止任何外部流量，并且每次连接失败的通知都会通过电子邮件发送到 root 账户。请注意，您实际上是将 `safe_finger` 命令的结果应用于违规主机并发送邮件。该命令随 TCP Wrappers 提供，它充当一个简化的 `finger` 客户端，比标准的 Linux `finger` 客户端更加精简（且更安全）。

```text
[ramon]$ more /etc/hosts.allow
ALL:LOCAL
[ramon]$ more /etc/hosts.deny
ALL: ALL (/usr/sbin/safe_finger -l @%h | /bin/mail -s %d-%h root) &
```

### 测试您的 TCP Wrappers 配置

除了手册页和文档之外，TCP Wrappers RPM 文件安装 TCP Wrappers 包的一部分，包括四个可执行文件。您已经看到了其中两个：

/usr/sbin/tcpd tcpd 文件是主要的守护进程可执行文件，它由 inetd 守护进程在调度适当的网络服务器应用程序之前调用。

/usr/sbin/safe-finger safe-finger 文件是 finger 应用程序，通常用于从试图建立入站连接的客户端通过网络获取信息。

另外两个工具对于测试您的 TCP Wrappers 配置非常重要。它们是 tcpdchk 和 tcpdmatch，并在以下两个部分中描述。

#### 使用 tcpdchk

可执行文件 /usr/sbin/tcpdchk 是 TCP Wrappers 配置“检查器”。tcpdchk 脚本检查配置文件并报告其中可能存在的任何潜在问题。它报告以下类型的问题：

- /etc/inetd.conf 中不存在的路径名
- 由 tcpd 配置但不在 /etc/inetd.conf 中的服务
- 无法用 TCP Wrappers 保护的服务
- /etc/inetd.conf 和/或 tcpd 配置文件中的语法错误

可以使用 -v 选项调用 tcpdchk 命令，以获取详细的表格输出。我强烈建议您在 TCP Wrappers 设置上线之前运行此命令，并且不要在生产服务器上运行它。

清单 4.8 包含了 tcpdchk 命令的示例输出。

**清单 4.8 运行 tcpdchk 实用程序**

```text
[ramon]$ tcpdchk -v
   Using network configuration file: /etc/inetd.conf

>>> Rule /etc/hosts.allow line 1:
    daemons:	ALL
    clients:	LOCAL 208.203.255.	153.39.	63.64.73.	204.177.181.9
	204.254.33.
    access:	granted

>>> Rule /etc/hosts.allow line 2:
    daemons:	finger
    warning: /etc/hosts.allow, line 2: finger: no such process name
	in /etc/inetd.conf

clients: LOCAL
access: granted

>>> Rule /etc/hosts.allow line 3:
daemons: pop-3
warning: /etc/hosts.allow, line 3: pop-3: no such process name in
/etc/inetd.conf
clients: LOCAL 208.255.255.256
warning: /etc/hosts.allow, line 3: 208.255.255.256: not an internet
address
access: granted
>>> Rule /etc/hosts.deny line 1:
daemons: ALL
clients: ALL
access: denied
```

在清单 4.8 的示例中，tcpdchk 脚本在某个 tcpd 配置文件中发现了两条规则，它们引用了 ftp 和 pop-3 服务，而这两个服务均未在 /etc/inetd.conf 文件中找到。此外，tcpdchk 脚本在我们的 tcp 配置中发现了一个语法错误（主机 208.255.255.256）；IP 地址八位位组不能高于 255。

### 使用 tcpdmatch

/usr/sbin/tcpdmatch 脚本预测来自特定客户端针对给定服务的请求是被允许还是被拒绝。tcpdmatch 脚本的命令语法为

```text
tcpdmatch service client
```

其中 service 是服务器名称，而 client 是请求该服务的主机的 IP 地址或主机名。例如，请考虑清单 4.9 中显示的三次 tcpdmatch 脚本调用。

**清单 4.9 运行 tcpdmatch 实用程序**

```text
[ramon]$ tcpdmatch in.ftpd local.example.com
client: hostname local.example.com
client: address 10.0.0.2
server: process in.ftpd
matched: /etc/hosts.allow line 1
access: granted

[ramon]$ tcpdmatch in.ftpd 143.45.22.3
client: address 143.45.22.3
server: process in.ftpd
matched: /etc/hosts.deny line 1
access: denied

[ramon]$ tcpdmatch in.telnetd remote.example.com
client:      hostname remote.example.com
client:      address 207.55.44.67
server:      process in.telnetd
matched:     /etc/hosts.deny line 1
access:      denied
```

在清单 4.9 的前两个命令中，您正在测试对 ftp 服务器的访问，首先使用本地主机作为目标，然后使用外部地址作为目标。根据 tcpd 配置，第一个请求将被允许，而第二个请求将被拒绝。清单 4.9 中的第三个命令示例探测从远程地址对 telnet 守护进程的访问，这当然是被拒绝的。

### TCP Wrappers 事件日志记录

TCP Wrappers 最有用的功能之一，仅次于基于地址的过滤（基于请求客户端的 IP 地址进行过滤），是记录每个传入的网络请求及其结果（允许/拒绝）的能力。与大多数 Linux 应用程序一样，TCP Wrappers 使用 syslog 设施来记录感兴趣的事件。检查您的 /etc/syslog.conf 设置，并在 authpriv.* 设施指向的文件中查找 TCP Wrappers 日志事件（通常是 /var/log/secure）：

```text
[ramon]$ sudo tail -f secure
Oct 24 08:05:47 buggs in.telnetd[24257]: connect from elmer
Oct 24 08:06:07 buggs in.ftpd[24259]: connect from elmer
Oct 24 08:07:10 buggs in.rlogind[24261]: connect from elmer
Oct 24 21:04:42 buggs in.ftpd[25220]: connect from localhost
Oct 24 21:05:34 buggs in.telnetd[25228]: connect from goodguy
Oct 24 21:06:03 buggs in.fingerd[25232]: refused connect from badguy
```

请注意，此 sudo 命令输出的每个条目包含

- 时间戳
- 主机名称（buggs）
- 网络服务器名称
- 操作，无论是接受（elmer、localhost、goodguy）还是拒绝（badguy）

通常，配置 swatch 和/或 logcheck 以查找关键字 refused 并提醒工作人员注意重复的未成功连接请求是一个好主意，这是暴力攻击的明确迹象。

## /etc/services 文件

/etc/services 文件存在于每个 Linux 安装中，它提供数字传输层端口号（TCP/UDP）与用于引用该服务的字符串之间的映射。例如，/etc/services 文件是系统实用程序查找 ftp 使用 21/TCP 端口而 snmp 使用 161/UDP 端口的地方。该文件的一般语法为

```text
service-name port/protocol #comment
```

这些字段的含义如下：

- service-name 是要查找的字符串（ftp、snmp、telnet 等）
- port 是数字端口号（21、161 等）。
- protocol 是 TCP 或 UDP。
- #comment 也可以是给定 service-name 的别名列表。

清单 4.10 列出了在 Linux 系统上典型的 /etc/services 文件的顶部。

**清单 4.10 Linux /etc/services 文件的部分细节**

```text
[ramon]$ more /etc/services
# /etc/services:
# $Id: services,v 1.4 1997/05/20 19:41:21 tobias Exp $
#
# Network services, Internet style
#
# Note that it is presently the policy of IANA to assign a
# single well-known port number for both TCP and UDP; hence,
# most entries here have two entries even if the protocol
# doesn't support UDP operations. Updated from RFC 1700,
# ``Assigned Numbers`` (October 1994). Not all ports
# are included, only the more common ones.

tcpmux	1/tcp		# TCP port service multiplexer
	echo	7/tcp
	echo	7/udp

discard	9/tcp		sink null
	discard	9/udp		sink null
	systat	11/tcp		users
	daytime	13/tcp
	daytime	13/udp
	netstat	15/tcp
	qotd	17/tcp		quote
```

