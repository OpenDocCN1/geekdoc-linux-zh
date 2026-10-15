
```
linux$ netstat -a
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 *:ldap *:* LISTEN
tcp 0 0 *:mysql *:* LISTEN
tcp 0 0 *:imaps *:* LISTEN
tcp 0 0 bull:ssh dhcp-32hw:4208 ESTABLISHED
tcp 0 0 bull:imaps nubark:54195 ESTABLISHED
tcp 0 0 bull:http dhcp-30hw:2563 ESTABLISHED
tcp 0 0 bull:imaps dhcp-18hw:2851 ESTABLISHED
tcp 0 0 *:http *:* LISTEN
tcp 0 0 bull:37203 baikal:mysql ESTABLISHED
tcp 0 0 *:ssh *:* LISTEN
...
```

此示例来自主机 otter，并且已被大幅精简；例如，UDP 和 UNIX 套接字连接未显示。上面的输出显示了一个入站 SSH 连接、两个入站 IMAPS 连接、一个入站 HTTP 连接、一个出站 MySQL 连接，以及一堆正在监听其他连接的端口。

地址显示为`hostname.service`，其中`service`是端口号。对于众所周知的服务，`netstat`会使用`/etc/services`中定义的映射以符号方式显示端口。你可以用`netstat`的`-n`选项获取数字地址和端口。与大多数网络调试工具一样，如果你的 DNS 出现故障，没有`-n`标志的`netstat`使用起来会很痛苦。

`Send-Q`和`Recv-Q`显示本地主机该连接的发送和接收队列的大小；TCP 连接另一端的队列大小可能不同。这些数字应趋向于 0，并且至少不应持续非零。（当然，如果你通过网络终端运行`netstat`，你的连接的发送队列可能永远不会为 0。）

连接状态仅对 TCP 有意义；UDP 是一种无连接协议。你最常看到的状态有`ESTABLISHED`表示当前活动的连接，`LISTEN`表示等待连接的服务器（通常在不使用`-a`时不显示），以及`TIME_WAIT`表示正在关闭的连接。

`netstat -a`主要用于在你已确定基本网络设施工作正常后调试更高层的问题。它可以让你验证服务器是否设置正确，并有助于诊断某些类型的通信故障，特别是与 TCP 有关的问题。例如，处于`SYN_SENT`状态的连接标识了一个正在尝试联系不存在或无法访问的网络服务器的进程。

如果`netstat`显示大量连接处于`SYN_WAIT`状态，你的主机可能无法处理正在请求的连接数量。这种不足可能是由于内核调优限制，甚至可能是恶意泛洪所致。

### 识别监听的网络服务

在这个注重安全的时代，一个常见的问题是“这台机器上有哪些进程正在网络上监听传入连接？” `netstat -a`显示所有正在主动监听的端口（任何处于`LISTEN`状态的 TCP 端口，以及潜在的任何 UDP 端口），但在繁忙的机器上，这些行可能会淹没在已建立的 TCP 连接的噪音中。

在 Linux 上，使用`netstat -l`仅查看监听端口。输出格式与`netstat -a`相同。你还可以添加`-p`标志，让`netstat`识别每个监听端口关联的具体进程。5 下面的示例输出显示了三个常见服务（`sshd`、`sendmail`和`named`），随后是一个不寻常的服务：

```
linux$ netstat -lp
...
tcp  0  0  0.0.0.0:22   0.0.0.0:*   LISTEN  23858/sshd
tcp  0  0  0.0.0.0:25   0.0.0.0:*   LISTEN  10342/sendmail
udp  0  0  0.0.0.53   0.0.0.*   30016/named
udp  0  0  0.0.0.962   0.0.0.*   38221/mudd
...
```

PID 为 38221 的`mudd`正在监听 UDP 端口 962。如果你不知道`mudd`是什么，你可能想进一步追查。

出于安全考虑，从外部视角查看机器也很重要，可以运行端口扫描器。`nmap`对此非常有帮助；参见第 914 页。

### 检查路由表

`netstat -r`显示内核的路由表。以下示例输出来自一台具有两个网络接口的 Red Hat 机器。（输出在不同操作系统之间略有差异。）

```
redhat$ netstat -rn
Kernel IP routing table
Destination Gateway Genmask Flags MSS Window irtt Iface
192.168.1.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
10.2.5.0 0.0.0.0 255.255.255.0 U 0 0 0 eth1
127.0.0.0 0.0.0.0 255.0.0.0 U 0 0 0 lo
0.0.0.0 192.168.1.254 0.0.0.0 UG 0 0 40 eth0
...
```

5. 在不支持`netstat -p`标志的 UNIX 系统上，`lsof`命令可以提供此信息（以及更多信息）。有关`lsof`的更多信息，请参见第 145 页。

有关内核调优的更多信息，请参见第 13 章。

有关路由表的更多信息，请参见第466页。

目标地址和网关可以显示为主机名或 IP 地址；`-n`标志请求数字输出。

标志位描述路由的特征：`U`表示 up（活动），`G`表示网关，`H`表示主机路由。`U`、`G`和`H`同时出现表示一条经过中间网关的主机路由。`D`标志（未显示）表示由 ICMP 重定向产生的路由。其余字段显示该路由上的 TCP 段大小和窗口大小，以及初始往返时间估计和接口名称。

使用这种形式的`netstat`来检查系统路由表的健康状况。特别重要的是验证系统是否具有默认路由，以及该路由是否正确。默认路由由全 0 的目标地址（`0.0.0.0`）或`default`一词表示。也可能不存在默认路由条目，但除了骨干路由器之外，这样的配置在任何设备上都是非常不典型的。

### 查看网络协议的操作统计

`netstat -s`会输出散布在整个网络代码中的计数器内容。输出分别包含 IP、ICMP、TCP 和 UDP 部分。以下是来自一台典型服务器的`netstat -s`输出片段；这些片段经过编辑，只显示最有价值的信息。

```
Ip:
  671349985 total packets received
  0 forwarded
  345 incoming packets discarded
  667912993 incoming packets delivered
  598623972 requests sent out
  60 dropped because of missing route
  203 fragments dropped after timeout
```

请务必确保数据包没有被丢弃或被舍弃。少量传入数据包被丢弃是可以接受的，但该指标快速上升通常表示内存不足或存在其他资源问题。

```
Icmp:
  242023 ICMP messages received
  912 input ICMP message failed.
  ICMP input histogram:
    destination unreachable: 72120
    timeout in transit: 573
    echo requests: 17135
    echo replies: 152195
  66049 ICMP messages sent
  0 ICMP messages failed
  ICMP output histogram:
    destination unreachable: 48914
    echo replies: 17135
```

在此示例中，输入部分的回显请求数量与输出部分的回显回复数量相匹配。请注意，即使所有数据包显然都可以转发，仍然可能生成“目标不可达”消息。

坏数据包最终到达拒绝它们的网关，然后错误消息会沿着网关链发送回来。
