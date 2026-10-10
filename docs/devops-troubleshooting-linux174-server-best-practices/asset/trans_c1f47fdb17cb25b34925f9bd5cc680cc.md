
以下命令适用于基于 Red Hat 的系统：

```bash
$ sudo service network restart
```

顺便说一句，令人惊讶的是，这些发行版即使在如此基础的事项上也存在差异。

一旦你确定了网关，请使用 ping 命令确认能否与网关通信：

```bash
$ ping -c 5 10.1.1.1
PING 10.1.1.1 (10.1.1.1) 56(84) bytes of data.
64 bytes from 10.1.1.1: icmp_seq=1 ttl=64 time=3.13 ms
64 bytes from 10.1.1.1: icmp_seq=2 ttl=64 time=1.43 ms
64 bytes from 10.1.1.1: icmp_seq=3 ttl=64 time=1.79 ms
64 bytes from 10.1.1.1: icmp_seq=4 ttl=64 time=1.50 ms
64 bytes from 10.1.1.1: icmp_seq=5 ttl=64 time=1.50 ms
--- 10.1.1.1 ping statistics ---
5 packets transmitted, 4 received, 20% packet loss, time 4020ms
rtt min/avg/max/mdev = 1.436/1.966/3.132/0.686 ms
```

正如你所见，我们成功 ping 通了网关，这意味着我们至少可以与 10.1.1.0 网络进行通信。如果你无法 ping 通网关，这可能意味着几种情况。这可能意味着你的网关正在阻止 ICMP 数据包。如果是这样，请告诉你的网络管理员，阻止 ICMP 是一种令人烦恼且安全收益甚微的做法，然后尝试 ping 同一子网内的另一台 Linux 主机。如果 ICMP 未被阻止，那么你的主机上的交换机端口可能配置了错误的 VLAN，因此你需要进一步检查与其连接的交换机。

## DNS 是否正常工作？

一旦你确认可以与网关通信，下一步需要测试的是 DNS 是否正常工作。`nslookup` 和 `dig` 工具都可以用于排查 DNS 问题，但由于目前只需进行基本测试，你可以直接使用 `nslookup` 来查看是否能将 web1 解析为 IP 地址：

```bash
$ nslookup web1
Server:    10.1.1.3
Address:   10.1.1.33

Name: web1.example.net
Address: 10.1.2.5
```

在这个示例中，DNS 工作正常。web1 主机扩展为 web1.example.net，并解析到地址 10.1.2.5。当然，请务必确认该 IP 地址与 web1 应有的 IP 地址一致！在这种情况下，DNS 工作正常，因此我们可以进入下一节；不过，DNS 也有多种失败的方式。

### 未配置名称服务器或名称服务器无法访问

如果你看到以下错误，这可能意味着你的主机没有配置名称服务器，或者名称服务器无法访问：

```bash
$ nslookup web1
;; connection timed out; no servers could be reached
```

无论哪种情况，你都需要检查 `/etc/resolv.conf` 文件，看看是否在其中配置了任何名称服务器。如果你没有看到任何 IP 地址，则需要向该文件中添加一个名称服务器。否则，如果你看到类似以下内容，则需要开始排查你与名称服务器之间的连接问题，从 ping 开始：

```bash
search example.net
nameserver 10.1.1.3
```

如果你无法 ping 通名称服务器，且其 IP 地址位于同一子网（在本例中，10.1.1.3 位于该子网内），则名称服务器本身可能已完全宕机。如果你无法 ping 通名称服务器，且其 IP 地址位于不同的子网，则跳转到 *能否路由到远程主机？* 部分，但仅针对名称服务器的 IP 地址应用那些故障排除步骤。如果你可以 ping 通名称服务器但它没有响应，则跳转到 *远程端口是否开放？* 部分。

### 缺少搜索路径或名称服务器问题

你的 `nslookup` 命令也可能出现以下错误：

```bash
$ nslookup web1
Server: 10.1.1.3
Address: 10.1.1.53
** server can't find web1: NXDOMAIN
```

在这里，你可以看到服务器做出了响应，因为它给出了回复：*server can’t find web1*。这可能意味着两种不同的情况。其一，这可能意味着 web1 的域名不在你的 DNS 搜索路径中。这是在 `/etc/resolv.conf` 中以 `search` 开头的行中设置的。一个好的测试方法是执行相同的 `nslookup` 命令，但使用完全限定域名（在本例中为 web1.example.net）。如果可以解析，那么要么始终使用完全限定域名，要么如果你希望仅使用主机名，则将域名添加到 `/etc/resolv.conf` 中的搜索路径中。

即使完全限定域名也无法解析，那么问题出在名称服务器上。排查所有 DNS 问题的完整方法在第 6 章中有介绍，但这里有一些基本要点。如果名称服务器本应包含该记录，则需要检查该区域的配置。如果它是一个递归名称服务器，那么你将通过查找其他域来测试该名称服务器上的递归功能是否正常工作。如果你可以查找其他域，则必须检查包含该区域的远程名称服务器是否存在问题。

## 能否路由到远程主机？

在排除 DNS 问题并看到 web1 已解析为其 IP 地址 10.1.2.5 之后，你必须测试能否路由到远程主机。假设你的网络中启用了 ICMP，一种快速的测试方法是 ping web1。如果你可以 ping 通该主机，说明你的数据包正在被路由到那里，你可以进入下一节 *远程端口是否开放？*。如果你无法 ping 通 web1，尝试识别该网络上的另一台主机，看看能否 ping 通它。如果可以，则 web1 可能已宕机或正在阻止你的请求，因此进入下一节。如果你无法 ping 通远程网络上的任何主机，说明数据包未被正确路由。测试路由问题的最佳工具之一是 `traceroute`。一旦你向 `traceroute` 提供主机名，它将测试你与该主机之间的每一跳。例如，dev1 和 web1 之间一次成功的 `traceroute` 将看起来像这样：

```bash
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  web1 (10.1.2.5)  8.039 ms  8.348 ms  8.643 ms
```

在这里你可以看到，数据包从 dev1 发送到其网关（10.1.1.1），然后下一跳是 web1。这意味着 10.1.1.1 很可能是两个子网共用的网关。如果你的网络中你和目标主机之间有路由器，输出可能会略有不同。如果你无法 ping 通 web1，你的输出将更像以下内容：

```bash
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  * * *
 3  * * *
```

一旦你在输出中看到星号，你就知道问题出在你的网关上。你需要前往该路由器，调查为什么它无法在两个网络之间路由数据包。或者，你看到的输出可能更像以下内容：

```bash
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 1  10.1.1.1 (10.1.1.1) 3006.477 ms !H 3006.779 ms !H 3007.072 ms
```

在这种情况下，你知道 ping 在网关处超时，因此主机可能已宕机，或者即使在同一子网内也无法访问。此时，如果你尚未尝试从与 web1 位于同一子网的机器上访问 web1，请现在尝试 ping 及其他测试。

> 如果你所在的网络是那些烦人的阻止 ICMP 的网络之一，别担心。你仍然可以排查路由问题。你只需安装 `tcptraceroute` 软件包（`sudo apt-get install tcptraceroute`），然后运行与 `traceroute` 相同的命令，只需将 `traceroute` 替换为 `tcptraceroute` 即可。

## 远程端口是否开放？

你可以路由到该机器，但仍然无法访问 80 端口上的 Web 服务器。下一步测试是查看端口是否开放。有几种不同的方法可以做到这一点。首先，你可以尝试使用 `telnet`：

```bash
$ telnet 10.1.2.5 80
Trying 10.1.2.5 ...
telnet: Unable to connect to remote host: Connection refused
```

如果你看到 `Connection refused`，则要么端口未打开（很可能是远程主机上未运行 Apache，或未在该端口上监听），要么是防火墙正在阻止你的访问。如果 `telnet` 能够连接，那么，好吧，你根本不存在网络问题。如果 Web 服务未按你预期的方式工作，则需要调查 web1 上的 Apache 配置。Web 服务器问题的故障排除在第 8 章中有介绍。

相比于 `telnet`，我更喜欢使用 `nmap` 来测试端口，因为它通常可以检测到防火墙。如果未安装 `nmap`，请使用你的软件包管理器安装 `nmap` 软件包。要测试 web1，输入以下内容：

```bash
$ nmap -p 80 10.1.2.5
Starting Nmap 4.62 ( http://nmap.org ) at 2009-02-05 18:49 PST
Interesting ports on web1 (10.1.2.5):
PORT STATE SERVICE
80/tcp filtered http
```

啊哈！`nmap` 足够聪明，通常可以区分真正关闭的端口和位于防火墙后的关闭端口。通常当端口确实关闭时，`nmap` 会报告其为 closed。这里它报告为 filtered。这告诉我们，有某个防火墙挡在了中间，正在丢弃数据包。这意味着你需要调查网关（10.1.1.1）和 web1 本身的任何防火墙规则，看看是否正在阻止 80 端口。

## 在本地测试远程主机

此时，我们要么已将问题缩小为网络问题，要么认为问题出在主机本身。如果我们认为

