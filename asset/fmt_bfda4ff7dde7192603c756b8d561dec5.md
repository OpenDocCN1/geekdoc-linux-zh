
在清单 4.9 的前两个命令中，您正在测试对`ftp`服务器的访问，首先使用本地主机作为目标，然后使用外部地址作为目标。根据`tcpd`配置，第一个请求将被允许，而第二个请求将被拒绝。清单 4.9 中的第三个命令示例探测从远程地址对`telnet`守护进程的访问，这当然是被拒绝的。

### TCP Wrappers 事件日志记录

`TCP Wrappers`最有用的功能之一，仅次于基于地址的过滤（基于请求客户端的 IP 地址进行过滤），是记录每个传入的网络请求及其结果（允许/拒绝）的能力。与大多数 Linux 应用程序一样，`TCP Wrappers`使用`syslog`设施来记录感兴趣的事件。检查您的`/etc/syslog.conf`设置，并在`authpriv.*`设施指向的文件中查找 `TCP Wrappers`日志事件（通常是`/var/log/secure`）：

```text
[ramon]$ sudo tail -f secure
Oct 24 08:05:47 buggs in.telnetd[24257]: connect from elmer
Oct 24 08:06:07 buggs in.ftpd[24259]: connect from elmer
Oct 24 08:07:10 buggs in.rlogind[24261]: connect from elmer
Oct 24 21:04:42 buggs in.ftpd[25220]: connect from localhost
Oct 24 21:05:34 buggs in.telnetd[25228]: connect from goodguy
Oct 24 21:06:03 buggs in.fingerd[25232]: refused connect from badguy
```

请注意，此`sudo`命令输出的每个条目包含

- 时间戳
- 主机名称（`buggs`）
- 网络服务器名称
- 操作，无论是接受（`elmer`、`localhost`、`goodguy`）还是拒绝（`badguy`）

通常，配置`swatch`和/或`logcheck`以查找关键字`refused`并提醒工作人员注意重复的未成功连接请求是一个好主意，这是暴力攻击的明确迹象。

### `/etc/services` 文件

`/etc/services`文件存在于每个 Linux 安装中，它提供数字传输层端口号（TCP/UDP）与用于引用该服务的字符串之间的映射。例如，`/etc/services`文件是系统实用程序查找`ftp`使用 `21/TCP` 端口而`snmp`使用 `161/UDP` 端口的地方。该文件的一般语法为

```text
service-name port/protocol #comment
```

这些字段的含义如下：

- `service-name`是要查找的字符串（`ftp`、`snmp`、`telnet` 等）
- `port`是数字端口号（`21`、`161` 等）。
- `protocol`是 `TCP` 或 `UDP`。
- `#comment`也可以是给定 `service-name` 的别名列表。

清单 4.10 列出了在 Linux 系统上典型的 `/etc/services` 文件的顶部。

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

## 网络服务与网络安全章节

```text
msp 18/tcp # message send protocol
msp 18/udp # message send protocol
chargen 19/tcp ttytst source
chargen 19/udp ttytst source
ftp-data 20/tcp
ftp 21/tcp
fSP 21/udp fspd
ssh 22/tcp # SSH Remote Login Protocol
ssh 22/udp # SSH Remote Login Protocol
telnet 23/tcp
```

虽然使用服务名称并非强制要求，但在 `/etc/inetd.conf` 中应避免使用服务编号，因为它们的可读性较差，且比字符字符串更容易出错。相反，`netstat` 命令（将在下一节中描述）如果你为所有正在使用的服务编号创建服务名称，其可读性会大大提高。

### netstat 命令

`netstat` 命令是你为寻求安全的网络配置而可用的最强大实用工具之一。虽然进程表显示哪些守护进程是从命令行启动的，`/etc/inetd.conf` 文件显示哪些是由 `inetd` 控制的，但 `netstat` 命令是诊断你的 Linux 服务器正在监听哪些端口的最终权威。

`netstat` 命令功能非常广泛，但 `--inet` 和 `-a` 选项向你展示了当前网络配置的状态。考虑 Listing 4.11 中的示例输出。

#### Listing 4.11 netstat --inet -a 命令的输出

```text
[ramon]$ netstat --inet -a
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 bugs::ssh elmer:1186 ESTABLISHED
tcp 0 0 \*:telnet \*: \* LISTEN
tcp 0 0 \*:ftp \*: \* LISTEN
tcp 1 0 bugs:2148 226.146.218.1:www CLOSE_WAIT
tcp 1 0 bugs:2146 226.148.218.1:www CLOSE_WAIT
tcp 0 0 \*:www \*: \* LISTEN
tcp 0 0 bugs:1335 elmer:6000 ESTABLISHED
tcp 0 0 bugs::ssh elmer:39470 ESTABLISHED
tcp 0 0 \*:smtp \*: \* LISTEN
```

`tcp 0 0 \*:ssh \*:\* LISTEN`

`tcp 0 0 \*:socks \*:\* LISTEN`

`raw 0 0 \*:icmp \*:\* 7`

`raw 0 0 \*:tcp \*:\* 7`

Listing 4.11 中的 `netstat --inet -a` 命令显示了当前活动的连接（`ESTABLISHED`）或正在拆除的连接（`CLOSE_WAIT`），以及那些正在等待新连接的服务（`LISTEN`）。你需要关注后一类，查找那些在 `Local Address` 列下主机名（和点号）之后出现的服务。事实上，我经常创建一个脚本，定期通过电子邮件向我发送以下 `netstat` 命令的输出：

```text
[ramon]$ netstat --inet -a | grep LISTEN
tcp 0 0 \*:telnet \*:\* LISTEN
tcp 0 0 \*:ftp \*:\* LISTEN
tcp 0 0 \*:www \*:\* LISTEN
tcp 0 0 \*:smtp \*:\* LISTEN
tcp 0 0 \*:ssh \*:\* LISTEN
tcp 0 0 \*:socks \*:\* LISTEN
```

之前 `netstat` 命令的输出是你 Linux 服务器在潜在入侵者眼中最准确的形象。总共有六个服务处于活动状态，并且它们都有服务名称。（我不得不手动将服务名称 `socks` 添加到 `/etc/services` 中；否则我将只会看到端口 `1080`。）
