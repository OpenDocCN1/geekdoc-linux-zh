
> 234 - 使用 `nmap` 执行 TCP connect 扫描

## 7.2.4 UDP 扫描

在执行 UDP 扫描时，`Nmap` 使用两种不同方法的结合来判断端口是开放还是关闭。对于大多数端口，它将使用标准的“ICMP 端口不可达”方法，即通过向给定端口发送空数据包来实现。然而，对于常用端口（例如用于 `SNMP` 的 `161` 端口），它将使用协议-`SNMP` 数据包来获取该端口的响应。要执行 UDP 扫描，需要使用 `-U` 选项，并且需要 `sudo` 权限访问原始套接字（raw sockets）：

```
kal@kali:$ sudo nmap -sU -U 10.11.1.115
Starting Nmap 7.80 (https://nmap.org) at 2019-03-04 12:46 EST
Nmap report for 10.11.1.115
Host is up (0.079 latency).
Not shown: 997 open/filtered ports
PORT STATE SERVICE
111/udp open rpcbind
137/udp open netbios-ssn
161/udp open snmp
```

`Nmap` 扫描：1 个 IP 地址 (1 个主机)，耗时 22.49 秒

`UDP` 扫描 (`-U`) 也可以与 `TCP` 扫描 (`-sS`) 选项结合使用，以构建更完整的目标画像：

```
kal@kali:$ sudo nmap -sS -U 10.11.1.115
Starting Nmap 7.80 (https://nmap.org) at 2019-03-04 12:46 EST
Nmap report for 10.11.1.115
Host is up (0.15 latency).
Not shown: 997 open/filtered ports, 989 closed ports
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
25/tcp open smtp
80/tcp open http
111/tcp open rpcbind
139/tcp open netbios-ssn
143/tcp open imap
199/tcp open smux
443/tcp open https
3389/tcp open mysql
32768/tcp open filet-nms
111/udp open rpcbind
137/udp open netbios-ssn
161/udp open snmp
```

`Nmap` 扫描：1 个 IP 地址 (1 个在线主机)，耗时 64.74 秒

在下一节中，我们将探索处理大型网络或受流量限制网络的技巧。

> 202 (`Nmap`, 2019), https://nmap.org/book/scan-methods-udp-scan.html

## 7.2.5 网络扫描

为了处理大量的主机，或者为了节省网络流量，我们可以尝试使用网络扫描（Network Sweeping）技术来探测目标。我们先从宽范围扫描开始，然后对感兴趣的主机进行更特定的扫描。

当使用 `Nmap` 的 `-sn` 选项进行扫描时，主机发现过程不仅包含 `ICMP` 回显。`ICMP` 请求中还添加了其他几种探测。`Nmap` 会向 `443` 端口发送 `TCP SYN` 包，向 `80` 端口发送 `TCP ACK` 包，并发送 `ICMP` 时间戳来验证主机是否可用。

```
kali@kali:~ nmap -sn 10.11.1.1-254
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 12:17 EST
Nmap scan report for 10.11.1.5
Host is up (0.026s latency).
MAC Address: 00:50:56:89:70:15
Nmap scan report for 10.11.1.7
Host is up (0.026s latency).
MAC Address: 00:50:56:36:32 (VMware)
Nmap: 254 IP addresses (44 hosts up) scanned in 6.4 seconds
```

在标准的 `Nmap` 输出上使用 `grep` 命令查找在线机器可能非常麻烦。相反，使用 `Nmap` 的“greppable”输出参数 `-oG` 将结果保存为易于解析的格式。

```
kali@kali:~ nmap -v -sn 10.11.1.1-254 -oG ping-sweep.txt
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:34 EST
Initiating ARP Scan at 11
Scanning 254 hosts [port]
Completed ARP Scan at 11:35, 4.7 elapsed (254 total hosts)
Initiating DNS resolution of 254 hosts, at 11:35
Nmap scan report for 10.11.1.1 [host down]
Nmap scan report for 10.11.1.2 [host down]
Nmap scan report for 10.11.1.3 [host down]
Nmap scan report for 10.11.1.4 [host down]
Nmap scan report for 10.11.1.5 [host down]
Host is up (0.026s latency).
MAC Address: 00:50:56:89:70:15 (VMware)
...
```
```
kali@kali:~ grep up ping-sweep.txt | cut -d " " -f2
10.11.1.5
10.11.1.7
10.11.1.8
```

我们还可以跨网络扫描特定的 `TCP` 或 `UDP` 端口，以定位有用或存在漏洞的端口。这比 `ping` 扫描更准确。

```
kali@kali:~ nmap -p 80 10.11.1.254 -oG web-sweep.txt
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:38 EST
Nmap scan report for 10.11.1.5
Host is up (0.036s latency).
PORT STATE SERVICE
80/tcp closed
MAC Address: 00:50:56:89:70:15 (VMware)
Nmap scan report for 10.11.1.7
Host is up (0.029s latency).
PORT STATE SERVICE
80/tcp filtered
MAC Address: 00:50:56:36:32 (VMware)
Nmap scan report for 10.11.1.8
Host is up (0.034s latency).
PORT STATE SERVICE
80/tcp open
MAC Address: 00:50:56:89:24 (VMware)
...
```
```
kali@kali:~ grep open web-sweep.txt | cut -d "" -f2
10.11.1.8
10.11.1.10
10.11.1.13
...
```

为了节省时间并网络资源，我们也可以扫描多个 `IP` 并探测短端口列表。例如，让我们使用 `--top-ports=20` 对 20 个端口进行 `TCP` 扫描、操作系统检测、脚本扫描和 `traceroute`：

```
kali@kali:~ nmap -sT -A --top-ports=20 10.11.1.254 -oG port-sweep.txt
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:40 EST
Nmap scan report for 10.11.1.5
Host is up (0.037s latency).
PORT STATE SERVICE
21/tcp closed ftp
22/tcp closed ssh
23/tcp closed telnet
25/tcp closed smtp
53/tcp closed domain
80/tcp closed http
110/tcp closed pop3
Host script results:
| nbstat: NetBIOS NAME: ALICE, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:89:70:15
smb-os-discovery:
| OS: Windows XP (2000 LAN Manager)
```
