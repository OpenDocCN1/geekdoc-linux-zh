

到名称服务器的 IP。如果可以 ping 通名称服务器但它没有响应，请跳到“远程端口是否打开？”部分。

## 缺少搜索路径或名称服务器问题

你执行 nslookup 命令时也可能收到以下错误：

```text
$ nslookup web1
Server:          10.1.1.3
Address:  10.1.1.3#53

** server can't find web1: NXDOMAIN
```

这里你可以看到服务器确实有响应，因为它返回了“server can't find web1”。这可能意味着两种不同的情况。其一，可能 web1 的域名不在你的 DNS 搜索路径中。这在 /etc/resolv.conf 中以 search 开头的行里设置。一个好的测试方法是执行相同的 nslookup 命令，只使用完全限定域名（本例中为 web1.example.net）。如果它能解析，那么要么始终使用完全限定域名，要么如果你想只使用主机名，就将域名添加到 /etc/resolv.conf 中的搜索路径。

如果即使完全限定域名也无法解析，那么问题出在名称服务器上。完整排查所有 DNS 问题的方法有点超出本章范围，但这里有一些基本提示。如果名称服务器本应有该记录，那么该区域的配置就需要检查。如果它是一个递归名称服务器，那么你需要通过查询其他域名来测试递归是否在名称服务器上不起作用。如果可以查询其他域名，那么你必须检查问题是否出在包含该区域的远程名称服务器上。

## 我能路由到远程主机吗？

在排除 DNS 问题并看到 web1 已解析为其 IP 10.1.2.5 之后，你必须测试是否可以路由到远程主机。假设你的网络已启用 ICMP，一个快速测试可能是 ping web1。如果可以 ping 通主机，你就知道数据包正在被路由到那里，可以进入下一节“远程端口是否打开？”。如果无法 ping 通 web1，尝试识别该网络上的另一台主机并查看是否可以 ping 通它。如果可以，那么 web1 可能已宕机或阻止了你的请求，因此请进入下一节。

如果无法 ping 通该网络上的任何主机，数据包没有被正确路由。测试路由问题的最佳工具之一是 traceroute。一旦你为 traceroute 提供一个主机，它将测试你与主机之间的每个跳点。例如，ubuntu1 与 web1 之间成功的 traceroute 如下所示：

```text
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  web1 (10.1.2.5)  8.039 ms  8.348 ms  8.643 ms
```

这里可以看到数据包从 ubuntu1 到其网关（10.1.1.1），然后下一跳是 web1。这意味着 10.1.1.1 很可能是两个子网的网关。在你的网络上，如果你和主机之间有更多路由器，你可能会看到略有不同的输出。如果无法 ping 通 web1，你的输出可能更像这样：

```text
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  * * *
 3  * * *
```

一旦你在输出中开始看到星号，你就知道问题出在你的网关上。你需要去该路由器并调查为什么它无法在两个网络之间路由数据包。如果相反你看到类似以下内容：

```text
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 1  10.1.1.1 (10.1.1.1) 3006.477 ms !H 3006.779 ms !H 3007.072 ms
```

那么你就知道 ping 在网关处超时，因此主机可能已宕机或即使从同一子网也无法访问。此时如果我还没有尝试从与 web1 相同子网的机器访问 web1，我会现在尝试 ping 和其他测试。

> **NOTE:** 如果你有一个那些讨厌的阻止 ICMP 的网络，不用担心，你仍然可以排查路由问题。你只需要安装 tcptraceroute 包（`sudo apt-get install tcptraceroute`），然后运行与 traceroute 相同的命令，只需将 traceroute 替换为 tcptraceroute 即可。

## 远程端口是否打开？

所以你能够路由到机器但仍然无法访问端口 80 上的 Web 服务器。下一个测试是查看端口是否甚至打开。有多种不同的方法可以做到这一点。例如，你可以尝试 telnet：

```text
$ telnet 10.1.2.5 80
Trying 10.1.2.5...
telnet: Unable to connect to remote host: Connection refused
```

如果看到 Connection refused，那么端口可能已关闭（很可能远程主机上的 Apache 未运行或未监听该端口）或防火墙阻止了你的访问。如果 telnet 可以连接，那么好吧，你根本没有网络问题。如果 Web 服务没有按你怀疑的方式工作，你需要在 web1 上调查你的 Apache 配置。与 telnet 相比，我更喜欢使用 nmap 来测试端口，因为它通常可以为我检测防火墙。如果未安装 nmap，运行 `sudo apt-get install nmap` 来安装它。要测试 web1，我会输入以下命令：

```text
$ nmap -p 80 10.1.2.5

Starting Nmap 4.62 ( http://nmap.org ) at 2009-02-05 18:49 PST
Interesting ports on web1 (10.1.2.5):
PORT STATE SERVICE
80/tcp filtered http
```

啊哈！nmap 足够智能，通常可以区分真正关闭的端口和防火墙后面的关闭端口。现在通常当端口真正关闭时，nmap 会报告为 closed。这里它报告为 filtered。这告诉我中间有一些防火墙正在丢弃我的数据包。这意味着我需要

