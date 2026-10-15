

## 7.3.4 使用 nmap 测试系统

首先警告：在使用 nmap 之前，你必须确保在你所在的地方使用它不是一种可惩罚的违法行为。这不是开玩笑；这对整个安全社区来说是一个严重的威胁。有些人正试图禁止使用甚至持有这种类型的软件。通常情况下，你对自己的系统或你负责的系统做什么，没人会过问。然而要明确；对你不拥有的系统运行 nmap 可能会导致坐牢。

那么 nmap 用来做什么？该程序可用于通过扫描活动 IP 地址来映射现有网络，或测试活动 IP 地址是否存在开放端口，等等。上面提到的两种用途也可以合并为一次扫描。现在，应该很明显为什么这个程序会对公司的安全构成真正威胁。另一方面，nmap 在安全社区中获得了众多奖项和推荐，被认为是最好的监控你负责的网络的程序之一。许多大型公司使用该程序持续监控其网络——在一种情况下甚至涉及超过一百万个 IP 地址的网络。该公司在该示例中使用了一台配备了几块网卡的专用机器。

如果你需要检查某个系统或一系列系统是否可用，你可以使用如 7.16 节所示的方式使用该程序。

### LISTING 7.16 使用 nmap 列出 IP 段中的可用机器

```
root@unixhost> nmap -sP 192.168.0.1-254

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Host (192.168.0.1) appears to be up.
Host linuxhost (192.168.0.2) appears to be up.
Host osxhost (192.168.0.3) appears to be up.
Host unixhost (192.168.0.5) appears to be up.
Host cvs host (192.168.0.200) appears to be up.
Nmap run completed -- 254 IP addresses (5 hosts up) scanned in 6 seconds
```

选项 -sP 指示 nmap 以不同的方式联系 192.168.0.1-254 范围内的每个地址。如果有应答，则 IP 地址将被添加到列表中。如果你需要运行此类扫描，请务必先与负责安全的人员交谈。这种扫描会在大多数防火墙和 IDS（入侵检测系统）上显示出来，从而触发警报。

如果你需要扫描单个系统的开放端口，你可以使用如 7.17 节所示的方式使用该程序。

### LISTING 7.17 对单个主机使用 nmap 进行端口扫描

```
root@unixhost> nmap -P0 -v -v 192.168.0.3

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
No tcp,udp, or ICMP scantype specified, assuming SYN Stealth scan. Use -sP if you really don't want to portscan (and just want to see what hosts are up).
Host osxhost (192.168.0.3) appears to be up ... good.
Initiating SYN Stealth Scan against osxhost (192.168.0.3)
The SYN Stealth Scan took 852 seconds to scan 1601 ports.
Interesting ports on osxhost (192.168.0.3):
(The 1600 ports scanned but not shown below are in state: filtered)
Port      State    Service
123/tcp   closed   ntp

Nmap run completed -- 1 IP address (1 host up) scanned in 852 seconds
```

选项 -P0 指示 nmap 不要通过发送 ICMP 数据包来测试指定系统的可用性，而 -v -v 告诉程序要极其健谈，这意味着程序的输出包含更详细的信息。由于命令行上未指定特定的扫描，程序执行了所谓的 SYN 扫描。这意味着程序向系统发送某些数据包，试图说服它以某种方式作出响应。如果收到该特定响应，则被测试的端口是开放的。程序在 7.17 节中报告了 1600 个被测试端口中的一个开放端口。在这种情况下，原因是该机器使用防火墙将数据包限制到端口 123（NTP）仅限于某些 IP 地址，并阻止其他所有内容。

程序的另一种用途（大多数 ISP 使用此功能）是借助 -O 选项确定连接到网络的操作系统。7.18 节显示了一个示例。

### LISTING 7.18 使用 nmap 揭示所使用的操作系统（1）

```
root@unixhost> nmap -P0 -v -v -O 192.168.0.5

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
No tcp,udp, or ICMP scantype specified, assuming SYN Stealth scan. Use -sP if you really don't want to portscan (and just want to see what hosts are up).
Host unixhost (192.168.0.5) appears to be up ... good.
Initiating SYN Stealth Scan against unixhost (192.168.0.5)
Adding open port 22/tcp
The SYN Stealth Scan took 919 seconds to scan 1601 ports.
```

