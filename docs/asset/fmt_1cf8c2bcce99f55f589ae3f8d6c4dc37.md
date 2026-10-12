
*列表 126 - 登录到 FTP 服务器*

为了进一步缩小背景流量的范围，让我们利用显示过滤器来仅关注 FTP 协议。显示过滤器比捕获过滤器灵活得多，并且语法略有不同。显示过滤器顾名思义，仅过滤显示的数据包，而 Wireshark 继续在后台捕获 `10.11.1.0/24` 地址范围内的所有网络流量。因此，通过点击显示过滤器右侧的“X”图标（图 13），可以清除过滤器而无需重新启动捕获。与捕获过滤器一样，我们还可以点击 `Analyze > Display filters` 从预定义列表中选择过滤器。

让我们应用一个显示过滤器，该过滤器仅显示 FTP 数据，或者端口 21 上的 TCP 流量：

![](img/ec25e59d75726b7041242a56d3376832_98_0.png)

图 13：设置针对端口 21 上所有流量的显示过滤器

这个过滤器效果非常好。现在我们清楚地看到只有端口 21 上的 FTP 流量。

#### 4.4.5 跟踪 TCP 流

Wireshark 允许我们查看网络流量，包括每个数据包的内容。然而，我们通常更感兴趣的是不同应用程序之间的数据流。我们可以利用 Wireshark 重组特定会话并以各种格式显示的能力。要查看特定的 TCP 流，我们可以右键点击感兴趣的数据包，例如包含我们 FTP 会话中 `USER` 命令的数据包，然后选择 *Follow > TCP Stream*：

![](img/ec25e59d75726b7041242a56d3376832_98_1.png)

图 14：在 Wireshark 中跟踪 TCP 流

重组的 TCP 流更容易阅读，我们可以回顾与 FTP 服务器的交互。由于 FTP 是一种明文协议，我们可以看到 FTP 客户端发送和接收的命令和输出：

![](img/ec25e59d75726b7041242a56d3376832_99_0.png)

图 15：在 Wireshark 中跟踪 TCP 流

#### 4.4.5.1 练习

- 使用 Wireshark 捕获网络活动，同时尝试使用 Netcat 连接到 `10.11.1.217` 的 `110` 端口，然后尝试登录。
- 阅读并理解输出。三次握手在哪里发生？连接在哪里关闭？
- 跟踪 TCP 流以阅读登录尝试。
- 使用显示过滤器仅监控 `110` 端口的流量。
- 运行一个新的会话，这次使用捕获过滤器仅收集 `110` 端口的流量。

### 4.5 Tcpdump

`Tcpdump` 是一个基于文本的网络嗅探器，尽管缺乏图形界面，但它简洁、强大且灵活。它是迄今为止最常用命令行数据包分析器，可以在大多数 Unix 和 Linux 操作系统上找到，但本地用户权限决定了捕获网络流量的能力。

`Tcpdump` 既可以捕获网络流量，也可以读取现有的捕获文件。让我们看看 `password_cracking_filtered.pcap` 文件中 发生了什么，该文件是在防火墙上捕获的。下载该文件并跟随我们分析数据。首先，我们将使用 `sudo` 启动 `tcpdump`（以授予捕获权限），并使用 `-r` 选项打开文件：

<sup>100</sup> (Wireshark, 2019), https://www.wireshark.org/
<sup>101</sup> (Tcpdump & Libcap, 2019), http://www.tcpdump.org/
<sup>102</sup> (WinPcap, 2018), https://www.winpcap.org/
<sup>103</sup> (Wireshark, 2016), http://wiki.wireshark.org/CaptureFilters
<sup>104</sup> (Wireshark, 2017), http://wiki.wireshark.org/DisplayFilters
<sup>105</sup> (Berkeley Packet Filter), http://biot.com/capstats/bpf.html
<sup>106</sup> (Tcpdump & Libcap, 2019), http://www.tcpdump.org/
<sup>107</sup> (Offensive Security, 2019), https://www.offensive-security.com/pwk-online/password_cracking_filtered.pcap

#### 4.5.2 过滤流量

![](img/ec25e59d75726b7041242a56d3376832_100_0.png)

```
kali@kali:~$ sudo tcpdump -r password_cracking_filtered.pcap
reading from file password_cracking_filtered.pcap, link-type EN10MB (Ethernet)
08:51:20.800917 IP 208.68.234.99.60509 > 172.16.40.10.81: Flags [S], seq 1855084074, win 14600, options [mss 1460,sackOK,TS val 25538253 ecr 0,nop,wscale 7], length 0
08:51:20.800953 IP 172.16.40.10.81 > 208.68.234.99.60509: Flags [S.], seq 4166855389, ack 1855084074, win 14480, options [mss 1460,sackOK,TS val 71430591 ecr 25538253,nop,wscale 4], length 0
08:51:20.801023 IP 208.68.234.99.60509 > 172.16.40.10.81: Flags [S], seq 1855084074, win 14600, options [mss 1460,sackOK,TS val 25538253 ecr 0,nop,wscale 7], length 0
08:51:20.801030 IP 172.16.40.10.81 > 208.68.234.99.60509: Flags [S.], seq 4166855389, ack 1855084074, win 14480, options [mss 1460,sackOK,TS val 71430591 ecr 25538253,nop,wscale 4], length 0
08:51:20.801048 IP 208.68.234.99.60509 > 172.16.40.10.81: Flags [S], seq 1855084074, win 14600, options [mss 1460,sackOK,TS val 25538253 ecr 0,nop,wscale 7], length 0
08:51:20.801051 IP 172.16.40.10.81 > 208.68.234.99.60509: Flags [S.], seq 4166855389, ack 1855084074, win 14480, options [mss 1460,sackOK,TS val 71430591 ecr 25538253,nop,wscale 4], length 0
...
```

*列表 127 - 使用 tcpdump 读取数据包捕获*

起初输出结果可能令人应接不暇，因此让我们尝试使用 `awk` 和 `sort` 来更好地理解其中涉及的 IP 地址和端口。

首先，我们将使用 `-n` 选项跳过 DNS 名称查找，并使用 `-r` 从我们的数据包捕获文件中读取。然后，我们可以将输出通过管道传递给 `awk`，打印出目标 IP 地址和端口（第三个以空格分隔的字段），并再次通过管道传递给 `sort` 和 `uniq -c`，分别对该字段进行排序和统计其在捕获文件中出现的次数。最后，我们使用 `head` 仅显示输出的前 10 行：

```bash
kali@kali:~$ sudo tcpdump -n -r password_cracking_filtered.pcap | awk -F " " '{print $3 }' | sort | uniq -c | head

13224 172.16.40.10.81

18 208.68.234.99.32768

18 208.68.234.99.32769

18 208.68.234.99.32770

18 208.68.234.99.32771

18 208.68.234.99.32772

18 208.68.234.99.32773

18 208.68.234.99.32774

18 208.68.234.99.32775

18 208.68.234.99.32776

...
```
