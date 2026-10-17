
```
nslookup -type=SOA apple.com
Address: 162.33.160.100
non-authoritative answer:
www.apple.com canonical name = akens.net
nameserver = a1-ns1
addr = hostmaster@apple.com
serial = 21
refresh = 50 (50)
retry = 50 (50)
minimum ttl = 50 (50)

non-authoritative answer:
priority = 30, mail exchanger = mail-in.apple.com
```

```Authoritative answers can be found from:
apple.com nameserver = a1-ns1
apple.com nameserver = a2-ns2
apple.com nameserver = a3-ns3
apple.com nameserver = a4-ns4
apple.com nameserver = a5-ns5
```

- 3 输入 `nslookup` 并按回车键。
- 4 输入 `querytype=SOA` 并按回车键。
- 5 输入域名并按回车键。
- 6 输入 `querytype=MX` 并按回车键。
- 7 输入域名并按回车键。

屏幕显示指定域名的 MX 记录。

屏幕显示指定域名的 SOA 记录。

## 检查你的网络连接

查看网络连接信息在你排查故障时特别有用。例如，你可以使用 `ifconfig` 命令检查你的网络连接是否运行或确定你的网络状态。你可以检查你的网络连接，查看接口视图，并对你的网络连接有一个直观的。两种网络连接都有重要功能，你可以使用 `ifconfig` 命令检查两者。`ifconfig` 接口配置命令提供了有关你系统中建立的网络接口的信息。这些信息显示分配给每个网络接口的地址是否正常。`ifconfig` 命令还显示与你的网络连接相关的子网掩码。这对于本地网络的正常运行和提高通信能力至关重要。普通连接与网络适配器关联，另一个可能是环回，提供了系统在自通信时使用网络协议的方法。环回地址在 Unix 上关联相同的 IP 地址（`127.0.0.1`）。普通或网络 IP 地址在每个系统中都是不同的，如果系统连接到接口也可能不同。用于检查你网络连接的接口命令是 `netstat`。该命令提供了路由表列表，以及你的系统正在处理的流量类型的细节。

## 检查你的网络连接

```
$ ifconfig

lo:BROADCAST,LOOPBACK,RUNNING,mtu 16384
       inet6 ::1
      inet 127.0.0.1 netmask 255.0.0

eth0:BROADCAST,MULTICAST,RUNNING,UP,mtu 1500
       inet 192.168.1.10 netmask 255.255.255.0
       ether 00:00:5e:00:01

eth1:BROADCAST,MULTICAST,RUNNING,UP,mtu 1500
       inet 192.168.1.11 netmask 255.255.255.0
       ether 00:00:5e:00:02

eth2:BROADCAST,MULTICAST,RUNNING,UP,mtu 1500
       inet 192.168.1.12 netmask 255.255.255.0
       ether 00:00:5e:00:03

eth3:BROADCAST,MULTICAST,RUNNING,UP,mtu 1500
       inet 192.168.1.13 netmask 255.255.255.0
       ether 00:00:5e:00:04
```

```
$ netstat -rn

Destination     Gateway         Flags    Us  Iflg  Ref    Interface
default         192.168.1.1      UG        0    0     0  eth0
127.0.0.1       0            H         0    0     0  lo
192.168.1.0      192.168.1.1      UG        0    0     0  eth0
192.168.1.0             0            U         0    0     0  eth1
```

```
Destination     Gateway         Flags    Interface
                                                              link4
                                                              lo
fe8::/64                                                              Uc
                                                              lo
                                                              link1
```

## 使用网络命令

Unix 系统（特别是作为服务器的系统）在任何时间通常都有已建立的连接。在连接的末端，系统通过端口进行通信。端口与客户端端的服务请求者和服务器端的服务请求者相关的地址。使用带有 Microsoft Internet Explorer 的软件可以与 Apache 等服务进行通信。

网络连接基于 TCP。TCP 是组成 TCP/IP 的主要协议之一，也是大多数网络工具使用的协议。网络连接通过一系列状态运行，从初始连接请求开始到关闭结束。端口监听请求。当客户端请求到达时，客户端和服务器交换信息并建立连接。

`netstat` 命令允许你查看哪些系统正在通信，以及它们在过程中使用了哪些端口。

`netstat -a` 命令提供的信息包括每个连接的末端服务器的名称或地址，以及正在使用的端口或服务地址。查看 `netstat` 输出可以帮助你确定你的系统支持多少个连接，以及它在负载下的性能如何。

输入以下内容：

```bash
netstat -a | grep ESTABLISHED
```

- * 屏幕显示已建立连接的列表。

```
Terminal File Edit Scrollback Font Window Help
user:~netstat -s | grep more
tcp:
5595 received
5283 data (87348 bytes)
0 packet (0 bytes) retransmitted
0 rounds initiated by MTU discovery
350 ack-ack packets (173 delayed)
0 only packets
window probe packets
window update packets
125 connection resets
5563 sent
5263 data (87352 bytes)
44 duplicate packets
0 asks for absent data
5092 packets (847806 bytes) received in-sequence
0 completely duplicate packets
0 old duplicate packets
0 packets with some dup. data (0 bytes)
0 out of order packets (0 bytes)
0 packets (0 bytes) of data after timeout
window probes
```

- 3 输入 `netstat -s` 后跟一个空格。
- * 屏幕显示你当前连接的列表。
- 5 输入 `| more` 并按回车。
- * 屏幕显示你的网络统计列表。
- 4 输入 `| more` 并按回车。
- 6 输入 `| more` 并按回车。

## 检查另一台计算机可访问

你可以使用 `ping` 命令检查远程系统是否可用，并使用 `traceroute` 跟踪路由。每当你遇到连接系统出现困难时，可以使用 `ping` 测试连接——这是一个简单的命令，它以数据包的形式向远程系统发送请求并要求回复；就像声纳在定位地址时发出的声音一样。

如果你的系统每个请求都收到回复，你可能拥有良好的连接。

测试网络连接的另一个有用命令是 `traceroute`。`traceroute` 命令尝试测量你的系统到目标主机路径上每个连续路由器之间的连接时间。结果是每个跳点的列表，以及到达每个跳点所需时间的报告。这些计时信息可以帮助解释连接质量。

如果远程系统正在运行并能够回复，它将用回显（echo）响应请求。`ping` 会一直请求，直到你按下 `Ctrl+C`。它会显示响应摘要，包括每次往返的时间。响应摘要告诉了你是否能够到达远程系统，并指示了连接的质量。

`ping` 和 `traceroute` 均依赖于一种名为互联网控制消息协议（ICMP）的协议，该协议有时会在路由器上被拦截。如果你在系统上运行 `ping` 或 `traceroute`，结果可能显示系统不可访问，但你可能可以通过 `telnet` 或 `ssh` 访问它。

```bash
$ user ping www.apple.com
ping www.apple.com [6 packets transmitted, 54 data bytes]
bytes from 17.253.12.32: icmp_seq=1 ttl=58 time=185.32 ms
bytes from 17.253.12.32: icmp_seq=2 ttl=58 time=184.25 ms
bytes from 17.253.12.32: icmp_seq=3 ttl=58 time=185.51 ms
bytes from 17.253.12.32: icmp_seq=4 ttl=58 time=187.85 ms
bytes from 17.253.12.32: icmp_seq=5 ttl=58 time=178.28 ms
bytes from 17.253.12.32: icmp_seq=6 ttl=58 time=179.47 ms

--- ping statistics ---
5 packets transmitted, 5 received, 0% packet loss
round-trip min/avg/max = 178.288/181.096/187.852 ms
user ~
```

```bash
$ user ping www.microsoft.com
ping www.microsoft.com [8 packets transmitted, 64 data bytes]

--- ping statistics ---
8 packets transmitted, 8 received, 0% packet loss
user ~
```

注意：执行此任务你必须已连接互联网。

- 1 输入 `ping` 后跟一个空格。
- 2 输入远程系统的域名并按回车。
- 3 `ping` 命令会显示响应的摘要。
- 4 没有数据包丢失或未收到答。
- 4 输入 `ping` 后跟一个空格。
- 5 输入 `www.microsoft.com` 并按回车。
- 6 按下 `Ctrl + C` 等待10 秒或更多。
- 7 `ping` 命令显示响应的摘要。
- 7 如果没有收到回复，ICMP 协议可能被拦截。

## 使用网络命令

你可以简化命令的复杂性。许多命令依赖 DNS 解析域名。如果你在网络连接遇到问题，在使用 `ping` 和 `traceroute` 时使用 IP 地址而不是域名。当然，这样更快。你可以通过添加 `-n` 参数来关闭 DNS 解析。

```bash
ping 192.142.137.55
```

PING 192.142.137.55 (192.142.137.55): 56 data bytes

bytes from 192.142.137.55: icmp_seq=0 ttl=58 time=157.03 ms

bytes from 192.142.137.55: icmp_seq=1 ttl=58 time=167.24 ms

bytes from 192.142.137.55: icmp_seq=2 ttl=58 time=169.94 ms

--- 192.142.137.55 statistics:

3 packets transmitted, 3 received, 0% packet loss

round-trip min/avg/max = 157.03/164.73/169.94 ms

输入以下内容：

```bash
netstat -an | grep ESTABLISHED
```

```
netstat -an | grep ESTABLISHED
tcp        0      0 192.168.1.10:443      172.217.16.14:5432  ESTABLISHED
```

```bash
$ user traceroute -n 33.163.77
traceroute to 33.163.77 (33.163.77), 30 hops,40 bytes per sec
1  192.168.1.1 (1.287 ms, 3.714 ms, 6.78 ms)
2  10.0.0.1 (15.781 ms, 17.581 ms, 18.74 ms)
3  172.217.16.1 (98.842 ms, 102.115 ms, 106.62 ms)
4  33.163.77 (108.414 ms, 106.687 ms, 108.63 ms)
5  33.163.77 (100.196 ms, 107.94 ms)
6  12.15.70.122.119.197 (101.374 ms, 107.583 ms, 108.41 ms)
7  122.124.196.1 (119.916 ms, 108.459 ms, 109.28 ms)
8  122.122.194.1 (108.253 ms, 108.754 ms, 109.99 ms)
9  122.122.192.1 (172.125 ms, 118.393 ms, 124.247 ms)
10 122.122.192.1 (162.623 ms, 161.463 ms, 166.72 ms)
11 122.122.192.1 (169.162 ms, 162.169 ms, 163.11 ms)
12 122.123.157.1 (164.613 ms, 157.239 ms, 159.378 ms)
```

- 7 输入 `traceroute` 后跟一个空格。
- 8 输入你的计算机的域名，或默认网关的 IP 地址。
- 9 `traceroute` 后面会跟一个头行和单条路由行。
- 10 输入远程系统的域名并按回车。
- * 列表中的星号意味着数据没有及时返回。

## 登录另一台计算机

你可以利用其他系统的账户和应用程序。你可以使用 `telnet` 或 `login` 登录远程系统。Unix 系统（如 Mac OS X）提供了多种登录其他系统的方法。你最常用的是 `telnet`，它比互联网还要悠久。telnet 为另一个系统建立终端连接。连接后，它会请求用户名和密码并登录。

另一个登录远程系统的工具是 `login`。这个工具与 `telnet` 相似，但并不常见。你可能只在 Unix 系统上找到它，即使如此也可能被禁用了。`login` 命令要求使用相同的用户名登录，除非你在命令末尾添加 `-l` 参数。你可以通过注销结束终端会话。对于大多数系统，你可以按下 `Control + D` 或输入命令 `logoff` 退出。

## 使用 telnet

- 1 在终端窗口中输入 `telnet` 后跟一个空格。
- 2 输入你有 shell 账户的系统的域名。

注意：如果没有远程系统账户，请输入 `telnet localhost`。

- 3 在提示处输入你的用户名和密码。
- 4 如果远程系统是 Unix 主机，输入 `who am i` 并按回车。
- * 屏幕显示登录用户列表中的你的登录。

## 使用网络命令操作

应用实例

你可以在命令行中输入系统名的同时提供端口号，从而使用 `telnet` 测试与其它系统的连接。如果你想检查支持 POP3 的系统中收件箱中有多少条消息，可以连接到为 POP3 服务器提供服务的端口，并使用 `telnet` 请求此类信息。你还可以使用 `telnet` 来判断邮件服务器是否有响应。POP3 是一种用于从邮件服务器下载电子邮件的简单协议。

# 输入以下内容：

```
[ferro:-] telnet <servername> 110
```

使用你通过 POP3 接收电子邮件的服务器名称。在输入以下行之后，请将括号中的文本替换为你的账户信息：

```
user <your username>
pass <your password>
stat
quit
```

## 结果：

在执行 `stat` 命令后，系统会显示一个数字，告诉你在你的收件箱中有多少条消息。

```
[ferro:-] user login achilles tcsnet.net
- 
last login Thu Jan Z 11:22:27 from achilles
bash-2.03 $
```

# 使用登录

- 1 在终端窗口中，输入 `login` 后跟一个空格。
- 2 输入远程系统的名称或 IP 地址并按回车键。
- 3 输入你的密码进行登录。

# 注销

- 1 输入 `logout` 并按回车键。
