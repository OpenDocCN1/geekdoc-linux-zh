
你也可以使用 rpcinfo 来注销 RPC 程序。 使用 -d 选项时，可以删除服务的注册。 例如，sprayd 在本地系统上运行。 我可以按如下方式注销它：

```
rpcinfo -d sprayd 1
```

sprayd 服务将被停止。 在第 9 章“进程控制”中，我描述了如何向进程发送信号。 我可以通过向 inetd 守护进程发送 HUP（挂断）信号来重新启动 sprayd，如下所示：

```
pkill -HUP inetd
```

## 名称服务

当用户输入 ping xena 之类的命令时，必须发生的第一件事之一是将主机名 xena 翻译为 IP 地址。 这可以通过两种方式之一实现。

IP 地址可以从 /etc/hosts 文件中确定，也可以通过域名服务解析。 对于小型网络，仅使用 /etc/hosts 不是问题。 对于大型网络，尝试在所有主机上保持 /etc/hosts 文件同步可能会导致大量工作，因为这些文件在每个主机上必须完全相同。 如果同一地址被用于两个不同的系统，网络可能会失败。

DNS 依赖于 named（读作 name d）服务器提供主机名到 IP 地址的转换。 named 服务器是永久存储特定域的主机名和 IP 地址信息的主机。 域名是主机名的网络等价物。 主机名指的是网络上的特定系统，而域名指的是特定网络。 站点和机构会被分配一个用于其网络的域名。 反过来，他们为域内的系统分配主机名。 Internet 域名系统提供了一种方案，使世界上的每个站点都有一个唯一名称。

名称服务和 DNS 在第 18 章中会再次更详细地讨论。

## TCP/IP 命令

TCP/IP 提供了多个命令和功能，这些命令和功能在 Solaris 操作环境中得到支持。 这些命令是 TCP/IP 网络包的一部分，可在所有实现 TCP/IP 的 UNIX 系统上使用，除非管理员专门禁用。

### telnet

telnet 用于登录网络上的另一系统。 以下是一个示例会话：

```
# telnet pyramid1
Trying 192.9.200.4...
Connected to pyramid1.
Escape character is '^]'.

SunOS 5.8
login: bill
Password:
Last login: Mon Jul 30 15:12:59 from 192.9.200.1
Sun Microsystems Inc.  SunOS 5.8  Generic February 2000
pyramid1%
```

### rlogin

rlogin 也是用于登录网络上另一系统的命令。 与 telnet 不同，rlogin 具有一种机制，如果 ~/.rhosts 和 /etc/hosts.equiv 文件已就位，则无需输入登录名和密码。 这些文件在第 9 章中讨论。

### ftp

文件传输协议（FTP）用于在网络上的两个系统之间传输一个或多个文件。 以下是一个示例 ftp 会话：

```
pyramid1% ftp pyramid1
Connected to pyramid1.
220 pyramid1 FTP server (SunOS 5.8) ready.
Name (pyramid1:bill): <cr>
331 Password required for bill.
Password: <enter password>
230 User bill logged in.
ftp> pwd
257 "/users/bill" is current directory.
ftp> ls
200 PORT command successful.
150 ASCII data connection for /bin/ls (192.9.200.4,47131) \
(0 bytes).
admin
file1
data
226 ASCII Transfer complete.
19 bytes received in 0.049 seconds (0.38 Kbytes/s)
ftp> get file1 /tmp/file1
200 PORT command successful.
150 ASCII data connection for file1 (192.9.200.4,47132) \
(31311 bytes).
226 ASCII Transfer complete.
local: /tmp/file1 remote: file1
31441 bytes received in 0.12 seconds (266.82 Kbytes/s)
ftp> bye
221 Goodbye.
pyramid1%
```

### rcp

你也可以使用 rcp（远程复制）命令在网络上的两个主机之间传输一个或多个文件。 另一系统必须信任你在当前主机上的 ID。 这种信任关系在第 8 章中讨论过。

rcp 命令比 ftp 更方便。 首先，如果系统之间存在适当的信任关系，rcp 不需要登录或密码，这使其适合脚本使用。 其次，rcp 允许将完整的目录树从一个系统复制到另一个系统。 然而，ftp 具有更多选项，被认为更安全。 以下是 rcp 的示例用法：

```
rcp /etc/hosts systemB:/etc/hosts
```

此示例使用 rcp 将文件 /etc/hosts 从本地系统复制到 systemB。

### rsh

你使用 rsh（远程 shell）命令在网络上的另一系统上执行 shell。 另一系统必须信任你在当前系统上的 ID。 以下示例使用 rsh 获取 systemB 上目录 /etc 的长列表：

```
rsh systemB ls -la /etc
```

### rexec

rexec 命令也用于在远程系统上执行 shell。 该命令与 rsh 的不同之处在于你必须输入密码。 在许多站点，出于安全原因 rsh 被禁用，而 rexec 被用作替代。

### rwho

rwho 命令产生的输出类似于 who 命令（在第 9 章中描述），但适用于网络上的所有系统。

### finger

finger 命令显示登录到本地系统或其他系统的用户的信息。 如果不带参数使用 finger，它会提供当前登录用户的相关信息。 如果 finger 带参数使用（例如用户名 glenda），它会显示与参数匹配的所有用户的信息。 你也可以通过将用户指定为 username@host 来使用 finger 命令查找远程系统上的用户。 为了保护用户隐私，许多远程系统不允许远程 finger 其系统。

### rup

rup 命令显示远程系统的主机状态，类似于 uptime 命令。 例如，要获取名为 sparc14 的远程主机的正常运行时间信息，请输入以下内容：

```
rup sparc14
```

系统会以下列方式响应：

```
sparc14  up  2 days, 41 mins,  load average: 0.00, 0.00, 0.01
```

### ping

使用 ping 命令测试到特定主机的网络连通性。 ping 命令的语法如下：

/usr/sbin/ping <options> <host> [timeout]

<host> 是相关机器的主机名，而 [timeout] 是可选参数，用于指定 ping 尝试访问机器的时间（以秒为单位）。 默认值为 20 秒。

ping 命令的一些更常见选项在表 13.6 中描述。

表 13.6
ping 选项

| 选项 | 描述 |
|---|---|
| -v | 详细输出。列出收到的除 ECHO_RESPONSE 之外的任何 ICMP 数据包。 |
| -I <interval> | 指定连续传输之间的间隔。默认值为 1 秒。 |
| -s | 指定 -s 标志时，ping 每秒发送一个数据报（可使用 -I 调整），并为收到的每个 ECHO_RESPONSE 打印一行输出。 |

当你运行 ping 时，ICMP 协议会向你指定的主机发送一个数据报，请求响应。 ICMP 是负责 TCP/IP 网络上错误处理的协议。

要测试 ultra5 和 sparc14 之间的网络连通性，请输入以下内容：

```
ping sparc14
```

如果主机 sparc14 处于运行状态，将显示以下消息：

```
sparc14 is alive
```

该消息表明 sparc14 对 ICMP 请求做出了响应。 然而，如果 sparc14 已关闭或无法接收 ICMP 数据包，你会收到以下响应：

```
no answer from sparc14
```

如果你怀疑某台机器即使处于运行状态也可能丢失数据包，可以使用 ping 的 -s 选项尝试检测问题。 例如，请输入以下内容：

```
ping -s sparc14
```

ping 会持续向 sparc14 发送数据包，直到你发送中断字符或发生超时。 你屏幕上的响应将类似于以下内容：

```
PING sparc14: 56 data bytes
64 bytes from sparc14 (192.9.200.14): icmp_seq=0. time=1. ms
64 bytes from sparc14 (192.9.200.14): icmp_seq=1. time=0. ms
64 bytes from sparc14 (192.9.200.14): icmp_seq=2. time=0. ms
64 bytes from sparc14 (192.9.200.14): icmp_seq=3. time=0. ms
64 bytes from sparc14 (192.9.200.14): icmp_seq=4. time=0. ms
...
...
---sparc14 PING Statistics---
8 packets transmitted, 8 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 0/0/1
```

输出末尾的数据包丢失统计信息指示主机是否丢弃了数据包，这可能表明存在网络问题。

### spray

spray 命令测试网络的可靠性。 它可以告诉你数据包是否被延迟或丢弃。 spray 使用远程过程调用（RPC）向主机发送单向数据包流。 它报告接收到的数量以及传输速率。

语法如下：

```
spray [ -c <count> -d <interval> -l <packet_size>] <hostname>
```
