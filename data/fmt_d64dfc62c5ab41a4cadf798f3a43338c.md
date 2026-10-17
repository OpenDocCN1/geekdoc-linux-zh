
```
$ telnet smtppsrv 25
Trying 12...
Connected to smtppsrv.example.com.
Escape character is '^'
helo example.com
220 smtppsrv.example.com SMTP Method 8.13.1/8.13.1; Wed, 4 May 2011 00:13:43 -0500 (CDT)
250 smtppsrv.example.com Hello desktop.example.com [192.168.1.97], pleased to meet you
mail from:user@spammer.com
571 5.0.0 Domain banned for spamming
quit
221 2.0.0 smtppsrv.example.com closing connection
```

`telnet`允许你使用任何想要的协议，只要你对它足够到可以手动输入命令。

## ftp: 在网络上传输

`FTP`（文件传输协议）是一种通过网络上的`TCP/IP`从远程系统下载文件和向其上传文件的方法。浏览器可以从`FTP`服务器下载文件。一些供应商使用匿名`FTP`（第707页）来接受调试会话上传或允许客户端下载固件。`FTP`不是一种安全的协议；仅用于从公下载公共信息。有关`FTP`安全性的更多信息，请参阅第702页。使用以下的

# 第 10 章 网络与互联网

第18章描述了用于安全通信的`OpenSSH`工具。第19章涵盖了`FTP`工具和服务器。

## ping: 测试网络连接

本节中提到的`ping`和`ping6`工具统称为`ping`（你可以在`http://arp.ril/mike/ping.html`查看`ping`的故事），它们向远程计算机发送`ECHO_REQUEST`（回显请求）数据包。这种交换是验证远程系统是否可用以及检查网络运行状况、速度或是否存在丢包的快速方法。`ping`工具使用`ICMP`（互联网控制消息协议）协议。在不带任何选项参数的情况下，`ping`每秒测试一次连接，直到你使用`CONTROL-C`终止它。

```
$ ping www.slashdot.org
PING www.slashdot.org (216.34.181.48): 56(84) bytes of data.
64 bytes from slashdot.org (216.34.181.48): icmp_seq=1 ttl=238 time=70.2 ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=2 ttl=238 time=72.6 ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=3 ttl=238 time=57.5 ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=4 ttl=238 time=71.2 ms
CONTROL-C
---
--- www.slashdot.org ping statistics
4 packets transmitted, 0% packet loss, timeout 302ms
rtt min/avg/max/mdev = 57.5/67.89/72.605/6.039
```

此示例显示到`www.slashdot.org`的连接得到了`slashdot.org`（`www.slashdot.org`的别名）的响应，且该系统在网上是启用并可用的。

默认情况下，`ping`发送包含56字节数据的包。在前面的示例中，向系统发送了四个数据包，直到用户按`CONTROL-C`中断。每行括号内的数字是数据序列号（命名为`icmp_seq`）。还列出了往返时间（毫秒），即数据包从本地系统发送到远程系统直到收到远程系统回复所经历的时间。在`ping`终止之前，它汇总结果，指示发送和接收了多少数据包，以及最小、最大和平均往返时间值。使用`ping6`测试`IPv6`网络。`ping`的名称模仿声呐脉冲的声音，用于识别和相互通信。`ping`这个词也扩展到了互联网探测器。

> **提示** 如果无法连接远程系统，`ping`将继续尝试，直到你按`CONTROL-C`中断。系统可能无响应的原因有多个：远程计算机宕机、系统之间的网络接口或部分可能损坏、发生了软件故障，或者远程机器出于安全原因设置为不允许`ping`（尝试`ping www.microsoft.com`或`ping www.ibm.com`）。

## traceroute: 追踪互联网路由

`traceroute`和`traceroute6`工具（本节中统称为`traceroute`，`traceroute`包）追踪`IP`数据包遵循的路由，包括经过的所有中间网关（称为网络跳），直到到达目的地（`traceroute`的参数）。它们会显示主机列表（如果可用）和`IP`地址，以及数据包到达路径上每个路由器以及本地系统接收响应所花费的往返时间。当你进行追踪以识别网络瓶颈位置时，可以使用这些信息。

`traceroute`工具没有从一个路径到下一个路径的概念；相反，它发送具有递增`TTL`（生存时间）值的`UDP`数据包。`TTL`是`IP`头部中的一个字段，指示数据包在被丢弃或返回之前允许的跳数。路径上的每个路由器都会检查`TTL`并将其减1。当`TTL`达到0时，路由器向本地系统发送`ICMP TIME EXCEEDED`，`traceroute`记录返回该路由器的`IP`。结果是数据包到达目的地所经过的主机列表。

`traceroute`工具可以帮助解决路由问题并定位故障。当你无法访问主机时，使用`traceroute`可以发现数据包遵循的路径、到达了多远以及延迟是多少。

下一页的示例显示了`traceroute`从本地电脑到`www.linux.org`遵循路由时的输出。第一行指示目标`IP`地址、将追踪的最大跳数以及将使用的包大小。每个数字行都包含中间目的地的名称和`IP`地址，随后是数据包往返所需的时间。`traceroute`向每个目标发送三个数据包；每行出现三次。第1行显示小于3毫秒。第4-6行显示数据包在进入`San Jose`之前在`Mountain View`（加州）附近跳转。在第13跳和第14跳之间，数据包跨越了美国（东部）。到第18跳时，数据包已找到`www.linux.org`。当`traceroute`未收到响应时会显示星号（*）。使用`traceroute6`测试`IPv6`。
