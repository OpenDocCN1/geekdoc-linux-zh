
| 编号 | 时间 | 源地址 | 目标地址 | 协议 | 长度信息 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 3 | 8.125497384 | 19.11.0.126 | 19.11.1.145 | TCP | 31 80BPS TCP-1 |
| 4 | 8.187829833 | 19.11.1.115 | 19.11.6.126 | ICMP | 71 目标不可达 (端口未... |
| 5 | 1.802881589 | 19.11.0.126 | 19.11.1.115 | UDP | 43 51082 - 161 Len=5 |
| 6 | 2.003950947 | 19.11.0.125 | 19.11.1.115 | UDP | 43 51082 - 161 Len=5 |
| 7 | 2.403284646 | 19.11.0.126 | 19.11.1.115 | UDP | 43 43218 - 160 Len=1 |
| 8 | 2.231871853 | 19.11.1.115 | 19.11.8.126 | ICMP | 71 目标不可达 (端口未... |

![](img/ec25e59d75726b7041242a56d3376832_182_0.png)

如图43所示，一个空的UDP数据包被发送到特定端口（数据包3、5、6和7）。如果目标UDP端口是开放的，数据包将被传递到应用层，接收到的响应取决于应用程序如何处理空数据包。在此示例中，应用程序未发送任何响应。然而，如果目标UDP端口是关闭的，目标主机应响应ICMP端口不可达消息（如数据包4和8所示），该消息由目标主机的UDP/IP协议栈发送。

大多数UDP扫描器倾向于使用标准的“ICMP端口不可达”消息来推断目标端口的状态。然而，当目标端口被防火墙过滤时，这种方法可能完全不可靠。实际上，在这些情况下，由于缺少ICMP消息，扫描器会将目标端口报告为开放。

### 7.2.1.3 常见的端口扫描陷阱

UDP扫描可能因多种原因而存在问题。首先，UDP扫描往往不可靠，因为防火墙和路由器可能会丢弃ICMP数据包。这会导致误报，使得实际关闭的端口显示为开放。其次，许多端口扫描器不会扫描所有可用端口，通常使用预定义的“感兴趣端口”列表进行扫描。这意味着开放的UDP端口可能会被忽略。使用特定于协议的UDP端口扫描器有助于获得更准确的结果。最后，渗透测试人员经常忘记扫描开放的UDP端口，而是专注于“更令人兴奋的”TCP端口。尽管UDP扫描可能不可靠，但开放的UDP端口背后隐藏着大量的攻击向量。

## 7.2.2 使用Nmap进行端口扫描

Nmap[^196]（由Gordon Lyon，aka Fyodor编写）是目前可用的最流行、多用途且健壮的端口扫描器之一。它已活跃开发了十多年，除了端口扫描外还具有众多功能。

> *本模块中介绍的一些Nmap示例扫描是使用sudo运行的*  
> *这是因为许多Nmap扫描选项需要访问原始套接字，* [^197]*而原始套接字又需要root权限。原始套接字允许对TCP和UDP数据包进行精细操作。如果没有对原始套接字的访问权限，*

[^196]: (Nmap, 2019), http://nmap.org/  
[^197]: (Man7, 2017), http://man7.org/linux/man-pages/man7/raw.7.html

![](img/ec25e59d75726b7041242a56d3376832_183_0.png)

> *Nmap会受到限制，因为它回退到使用标准Berkeley套接字API来构造数据包。* [^198]

[^198]: 文本中未明确引用，但暗示为脚注198。

让我们探索一些端口扫描示例，以便更好地熟悉Nmap及其选项。

### 7.2.2.1 对流量负责

默认的Nmap TCP扫描将扫描给定机器上1000个最流行的端口。在我们盲目开始运行扫描之前，让我们检查一下这种类型的扫描发送的流量大小。我们将扫描实验室机器之一，同时使用**iptables**监控发送到目标主机的流量量[^199]。

[^199]: 文本中未明确引用，但暗示为脚注199。

我们将使用几个**iptables**选项。首先，我们将使用`-I`选项将新规则插入到给定的链中，在这种情况下，包括**INPUT**（入站）和**OUTPUT**（出站）链，后跟规则编号。我们将使用`-s`指定源IP地址，使用`-d`指定目标IP地址，并使用`-j`来**ACCEPT**（接受）流量。最后，我们将使用`-Z`选项将所有链中的数据包和字节计数器清零。

现在让我们运行这些命令：

```
kali@kali:~$ sudo iptables -I INPUT 1 -s 10.11.1.220 -j ACCEPT
kali@kali:~$ sudo iptables -I OUTPUT 1 -d 10.11.1.220 -j ACCEPT
kali@kali:~$ sudo iptables -Z
```
列表 229 - 配置用于扫描的iptables规则

现在让我们使用**nmap**生成一些流量。

```
kali@kali:~$ nmap 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:20 EST
Nmap scan report for 10.11.1.220
Host is up (0.29s latency).
Not shown: 989 closed ports
PORT STATE SERVICE
21/tcp open ftp
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open msrpc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswd5
593/tcp open http-rpc-epmap
636/tcp open ldapssl
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPSsl
3389/tcp open ms-wbt-server
Nmap done: 1 IP address (1 host up) scanned in 46.29 seconds
```
列表 230 - 扫描IP的前1000个最流行TCP端口

扫描完成，发现了一些开放端口。

现在让我们查看一些**iptables**统计信息，以了解扫描产生了多少流量。我们将使用**-v**选项为输出添加一些详细信息，使用**-n**启用数字输出，使用**-L**列出所有链中存在的规则：

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 1528 packets, 226K bytes)
 pkts bytes target prot opt in out source destination
1263 51264 ACCEPT all -- * * 10.11.1.220 0.0.0.0/0

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target prot opt in out source destination

Chain OUTPUT (policy ACCEPT 1323 packets, 191K bytes)
 pkts bytes target prot opt in out source destination
1314 78300 ACCEPT all -- * * 0.0.0.0/0 10.11.1.220
```
列表 231 - 使用iptables监控前1000端口扫描的nmap流量

根据此输出，这个默认的1000端口扫描产生了大约78 KB的流量。

让我们再次使用**iptables -Z**将所有链中的数据包和字节计数器清零，并使用**-p**指定所有TCP端口运行另一个**nmap**扫描：

```
kali@kali:~$ sudo iptables -Z
kali@kali:~$ nmap -p 1-65535 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:27 EST
Nmap scan report for 10.11.1.220
Host is up (0.00067s latency).
Not shown: 65507 closed ports
PORT STATE SERVICE
21/tcp open ftp
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open msrpc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswd5
593/tcp open http-rpc-epmap
636/tcp open ldapsssl
1291/tcp filtered seagullms
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPssl
3389/tcp open ms-wbt-server
5722/tcp open msdfs
9389/tcp open adws
12777/tcp filtered unknown
46056/tcp filtered unknown
47001/tcp  open    winrm
...
Nmap done: 1 IP address (1 host up) scanned in 80.42 seconds
```

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 219K packets, 252M bytes)
 pkt  bytes  target     prot opt  in      out     source        destination
66243  2659K  ACCEPT    all  --  *      *      10.11.1.220   0.0.0.0/0

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkt  bytes  target     prot opt  in      out     source        destination

Chain OUTPUT (policy ACCEPT 85792 packets, 11M bytes)
 pkt  bytes  target     prot opt  in      out     source        destination
66768  4006K  ACCEPT    all  --  *      *      0.0.0.0/0    10.11.1.220
```
*列表 232 - 使用iptables监控所有TCP端口扫描的nmap流量*

类似的本地端口扫描明确探测所有65535个端口，产生了大约4 MB的流量，数量显著更高。然而，这个全端口扫描发现了默认TCP扫描未发现的新端口。

上述结果表明，对C类网络（254台主机）进行完整的Nmap扫描将导致向网络发送超过1000 MB的流量。在理想情况下，对每台目标机器进行完整的TCP和UDP端口扫描将提供关于暴露的网络服务的最准确信息。然而，上面的例子揭示了需要使用更全面的扫描来平衡流量限制（如慢速上行链路）与发现额外开放端口和服务的需求。对于更大的网络，如A类或B类网络评估，这一点尤为正确。

在下一节中，我们将探索Nmap的各种扫描技术。

### 7.2.2.2 隐蔽 / SYN 扫描

Nmap首选的扫描技术是SYN扫描，也称为“隐蔽”扫描[^200]。使用SYN扫描有许多好处，因此，当**nmap**命令中未指定扫描技术且用户具有所需的原始套接字权限时，它是默认的扫描技术。

[^200]: (Nmap, 2019). https://nmap.org/book/synscan.html

SYN扫描是一种TCP端口扫描方法，涉及向目标机器的各个端口发送SYN数据包，而不完成TCP握手。如果TCP端口是开放的，目标机器应返回SYN-ACK，告知我们该端口是开放的。此时，端口扫描器不会发送最终的ACK来完成三次握手。

```
kali@kali:~$ sudo nmap -sS 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:27 EST
Nmap scan report for 10.11.1.220
Host is up (1.3s latency).
Not shown: 980 closed ports
PORT     STATE  SERVICE
21/tcp   open     ftp
53/tcp   open     domain
```

