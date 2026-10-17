
```
kali@kali:~ nmap -sT 192.168.0.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 06:44 EST
nmap scan report for 192.168.0.149
host is up (0.1ms latency).
not shown: 998 closed tcp ports (conn-refused)
PORT STATE
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open mssprc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open passwd5
593/tcp open http-rpc-epmap
636/tcp open ldapsis
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPss
```

> 列表 59 - 使用 `nmap` 执行 TCP 连接扫描

输出显示，连接扫描发现了几个仅在 Windows 主机上活跃的开放，特别是域控制器（我们稍后会介绍）。即使从这个简单的扫描中，一个主要的收获是：我们可以推断出目标主机的底层操作系统和角色。

在回顾了最常用的 `Nmap` TCP 扫描技术后，让我们学习 UDP 扫描。

在执行 UDP 扫描时，`Nmap` 将结合两种不同的方法来确定端口是开放还是关闭的。对于大多数端口，我们将使用之前描述的标准“ICMP 端口不可达”方法，通过向端口发送空包。然而，对于 SNMP 使用的常用端口，我们将发送一个协议-SNMP 包，尝试从绑定到端口的获取响应。要执行 UDP 扫描，我们将使用 `-U` 选项并配合 `sudo` 访问原始接字。

```
kali@kali:~ sudo nmap -U 192.168.0.149
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:46 EST
nmap scan report for 192.168.1.131
host is up (0.1ms latency).
not shown: 977 closed udp ports (port-unknown)
```

² (`Nmap`, 2022), https://nmap.org/scan-methods-connect-scan.html

¹ (`Wikipedia`, 2022), https://en.wikipedia.org/wiki/Berkeley_sockets

(`Nmap`, 2022), https://nmap.org/scan-methods-udp-scan.html

`PWK` - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

## 使用 Kali Linux 进行渗透测试

| PORT | STATE | SERVICE |
|---|---|---|
| 123/udp | open | ntp |
| 389/udp | open | ldap |

Nmap done: 1 IP address (1 host) scanned in 22.49 seconds

列表 60 - 使用 `nmap` 执行 UDP 扫描

UDP 扫描 (`-SU`) 也可以与 TCP SYN 扫描 (`-SS`) 结合使用，以构建我们目标的完整画像。

```
kali@kali:~ sudo nmap -SU -sS 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 08:16 EST
Nmap scan report for 192.168.50.149
Host is up (0.12s latency).
Not shown: 989 closed ports (reset), 977 closed udp ports (port-unreachable)
```

| PORT | STATE | SERVICE |
|---|---|---|
| 53/tcp | open | domain |
| 88/tcp | open | kerberos-sec |
| 135/tcp | open | msprc |
| 139/tcp | open | netbios-ssn |
| 389/tcp | open | ldap |
| 445/tcp | open | microsoft-ds |
| 464/tcp | open | kpasswd5 |
| 593/tcp | open | http-rpc-epmam |
| 636/tcp | open | ldapssl |
| 3268/tcp | open | globalcatLDAP |
| 3269/tcp | open | globalcatLDAPS |
| 53/udp | open | domain |
| 123/udp | open | ntp |
| 389/udp | open | ldap |

列表 61 - 使用 `nmap` 执行组合 UDP 和 SYN 扫描

我们的 TCP 和 UDP 扫描发现了额外的开放端口，揭示了目标主机上运行的服务。我们可以扩展从单个主机学到的知识并将其应用到整个网络范围。为了处理大量主机，或者为了节省流量，我们可以尝试从感兴趣的大范围开始探测目标。当使用 `-sn` 选项执行 `Nmap` 网络扫描时，发现过程不仅仅是发送 ICMP echo 请求。`Nmap` 还会向端口 443 发送 TCP SYN 包，向端口 80 发送 TCP ACK 包，并发送 ICMP 时间戳请求验证主机是否可用。

```
kali@kali:~ nmap -sn 192.168.50.1-253
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 03:19
Nmap scan report for 192.168.50.8
Host is up (0.12s latency).
Nmap scan report for 192.168.50.8
Nmap done: 254 hosts scanned in 3.74 seconds
```

`PWK` - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

在标准的 `Nmap` 输出中使用 `grep` 命令搜索机器非常麻烦。相反，使用 `nmap` 的 'greppable' 输出 `-oG`，将这些结果保存为更易管理的格式。

```
kali@kali:~ nmap -v 192.168.50.1-253 -oG ping-sweep.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 03:21
Initiating Scan at 03:21
Read data from: /usr/bin/../share/nmap done: 254 IP addresses (13 hosts) in 3.74 seconds
kali@kali~$ grep ping-sweep.txt | cut -d " " -f2
192.168.50.6
192.168.50.8
192.168.50.9
```

列表 62 - 使用 `nmap` 执行网络扫描

我们可以跨网络使用特定的 TCP 或 UDP 端口寻找可能有用或存在已知漏洞的系统。这种方法比 ping 扫描更准确。

```
kali@kali~$ nmap -p 80 192.168.50.1-253 -oG web-sweep.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 03:50
```

等待...

为了节省时间和网络资源，我们还可以扫描多个 IP 的一个常用端口列表。让我们使用 `--top-ports` 选项对前 20 个端口进行连接扫描，并开启操作系统检测、脚本扫描和 traceroute `-A`。

```
kali@kali~$ nmap -sT --top-ports=20 192.168.50.1-253 -oG top-port-sweep.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 04:04 EST
nmap scan report for 192.168.50.6
Host is up (0.12s latency).
```

| PORT STATE SERVICE VERSION
| 21/tcp open |
| 22/tcp open OpenSSH 8.2p1 Ubuntu 4ubuntu.3 (Ubuntu Linux; protocol 2.0) |
