
最好的解决办法是联系被用作中继的组织，告知他们滥用情况。通常，他们只需重新配置其互联网路由器即可阻止未来的攻击。如果该组织不配合，你可以通过在路由器上拦截 `ICMP` 协议来减少攻击的影响。这至少可以阻止流量进入你的内部网络。如果你能说服你的 `ISP` 拦截针对你网络的 `ICMP` 数据包，效果会更好。`ICMP` 是网络流量控制所必需的，因此你只需暂时拦截即可。你可以永久拦截类型 8 的数据包（echo 请求）。

## 防范分布式拒绝服务攻击

分布式拒绝服务（`DDoS`）攻击更难发起，几乎不可能阻止。`DDoS` 攻击始于渗透数百甚至数千台安全防护薄弱的机器。随后，这些机器可以根据攻击者的意愿被指挥去攻击单一的主机。

随着 `DSL` 和电缆调制解调器的普及，数百万人正享受着几乎无速度限制的互联网接入。在急于上网的过程中，这些人中的许多甚至忽略了实施最基本的安全措施。由于这些人中的绝大多数运行的是 Microsoft 操作系统，他们往往很快就会遭受蠕虫和病毒的侵袭。机器被渗透后，蠕虫或病毒常常会在受害者的机器上安装一个程序，指示其静默地*呼叫家园*，并宣布它已准备好听从*主人的命令*。

在主人的一声令下，受感染的机器现在可以被用来将集中的垃圾数据流聚焦于选定的主机。与成千上万其他受感染的机器协同工作，一个*脚本小子*（指那些没有知识去创建蠕虫或病毒，但具备寻找并启动它们所需的倾向和技能的人，通常是年轻人）现在拥有了关闭互联网上几乎任何网站的能力。

检测 `DDoS` 类似于检测 `DoS` 攻击。可能会存在以下一个或多个迹象：

- 持续饱和的数据链路
- 在非高峰时段链路饱和程度没有降低
- 数百甚至数千个并发的网络连接
- 系统性能极度缓慢

要确定你的数据链路是否饱和，`Ping` 外部主机这一操作往往能揭示许多情况。延迟比平时高得多是一个明显的征兆。正常的 `Ping` 延迟（即 `Ping` 响应从远程主机返回所需的时间）看起来如下所示：

```
# ping www.example.com
PING www.example.com (192.0.32.10) from 10.0.0.11: 56(84) bytes of data
64 bytes from 192.0.32.10: icmp seq=1 ttl=49 time=40.1 ms
64 bytes from 192.0.32.10: icmp seq=2 ttl=49 time=42.5 ms
64 bytes from 192.0.32.10: icmp seq=3 ttl=49 time=39.5 ms
64 bytes from 192.0.32.10: icmp seq=4 ttl=49 time=38.4 ms
64 bytes from 192.0.32.10: icmp seq=5 ttl=49 time=39.0 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 4035ms
rtt min/avg/max/mdev = 38.472/39.971/42.584/1.432 ms
```

在上面的示例中，`Ping` 数据包完成往返的平均时间约为 39 毫秒。

指向一个接近饱和链路的 `Ping` 看起来如下所示：

```
# ping www.example.com
PING www.example.com (192.0.32.10) : from 10.0.0.11: 56(84)bytes of data
64 bytes from 192.0.32.10: icmp seq=1 ttl=62 time=1252 ms
64 bytes from 192.0.32.10: icmp seq=2 ttl=62 time=1218 ms
64 bytes from 192.0.32.10: icmp seq=3 ttl=62 time=1290 ms
64 bytes from 192.0.32.10: icmp seq=4 ttl=62 time=1288 ms
64 bytes from 192.0.32.10: icmp seq=5 ttl=62 time=1241 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 5032ms
rtt min/avg/max/mdev = 1218.059/1258.384/1290.861/28.000 ms
```

在这个示例中，`Ping` 数据包平均需要 1.3 秒才能完成往返。从第一个示例到第二个示例，延迟增加了 31 倍！一条从正常工作状态变慢至 31 倍的数据链路，是链路利用率需要被调查的明确迹象。

若要更准确地衡量数据吞吐量，可以使用诸如 `tcpt` 之类的工具。若要使用 `tcpt` 测试你的连接，必须在你网络的*内部*和*外部*的机器上安装 `tcpt` `RPM` 软件包。如有需要，请使用 `yum` 命令安装 `tcpt` 软件包。如果你不确定该软件包是否已安装，只需在命令提示符下输入 `tcpt` 即可。你应该会看到类似以下内容：

```
# tcpt
Usage: tcpt -t [-options] host [ < in ]
	tcpt -r [-options > out]

Common options:
-4  	Use IPv4
-6    Use IPv6
-l ## length of bufs read from or written to network (default 8192)
-u    use UDP instead of TCP
-p ## port number to send to or listen at (default 5001)
-s  -t: source a pattern to network
    -r: sink (discard) all data from network

-A ## align the start of buffers to this modulus (default 16384)
-O ##start buffers at this offset from the modulus (default 0)
-v    verbose: print more statistics
-d    set SO_DEBUG socket option
-b ## set socket buffer size (if supported)
-f X    format for rate: k,K = kilo{bit,byte}; m,M = mega; g,G = giga
Options specific to -t:
-n ## number of source bufs written to network (default 2048)
-D    don't buffer TCP writes (sets TCP_NODELAY socket option)
-w ## number of microseconds to wait between each write
Options specific to -r:
-B    for -s, only output full blocks as specified by -l (for TAR)
-T    "touch": access each byte as it's read
-I if Specify the network interface (e.g. eth0) to use
```

第一步是在服务器机器上启动接收进程：

```
# tcp -rs
tcp-r: bufLen=8192, nbuf=2048, align=16384/0, port=5001 tcp
tcp-r: socket
```

`-r` 标志表示服务器机器将作为接收端。与 `-r` 标志结合使用的 `-s` 标志，告诉 `tcp` 你希望忽略任何接收到的数据。

下一步是让数据链路外部的人，使用与你的速度相近的网络链路，设置一个 `tcp` 发送进程：

```
# tcp -ts server.example.com
tcp-t: bufLen=8192, nbuf=2048, align=16384/0, port=5001 tcp -> server.example.com
tcp-t: connect
```

让该进程运行几分钟，然后在发送端按下 `Ctrl+C` 以停止测试。接收端随后将花一点时间计算并呈现结果：
