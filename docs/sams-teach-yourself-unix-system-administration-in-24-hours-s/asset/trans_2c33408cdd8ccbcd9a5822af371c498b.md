

![](img/5ced0c78d748bd190e9027e5549a3622_361_0.png)

> 如果你的客户端系统出现 RX 和 TX 错误，或者丢包/溢出约占数据包总量的 10% 以上，那么你的子网可能过于繁忙。解决办法是进一步划分子网。如果错误为零（如此处所示），那么合乎逻辑的结论是，网络上还有充足的空间容纳更多服务器。

显示 RX 字节数的摘要行是一个很好的补充，省去了一些手工计算：该服务器已接收总计 3.9MB 的数据包，并已发送 14.4MB 的数据包。

- 2. 与 Red Hat Linux 的冗长输出相比，来看看 Mac OS X 中同样的 ifconfig 输出：

    ```
    # ifconfig -a
    lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
    inet 127.0.0.1 netmask 0xff000000
    en0: flags=8863<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    inet 198.76.82.132 netmask 0xffffff00 broadcast 198.76.82.255
    ether 00:30:65:3d:e8:10
    media: autoselect (10baseT/UTP <half-duplex>) status: active
    supported media: none autoselect 10baseT/UTP <half-duplex> 10baseT/UTP <full-duplex> 100baseTX <half-duplex> 100baseTX <full-duplex>
    ```

    差异很大，而且这里完全没有 RX/TX 统计。不过 MTU 同样是正确的 1500 字节。

    Solaris 提供了更简洁的结果：

    ```
    # /sbin/ifconfig -a
    lo0: flags=1000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4> mtu 8232 index 1
    inet 127.0.0.1 netmask ff000000
    pcn0: flags=1000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2
    inet 198.76.82.155 netmask ffffff00 broadcast 198.76.82.255
    ether 0:50:56:54:45:9d
    ```

    输出更加精简，但仍提供了验证以太网接口配置所需的核心信息，包括 IP 地址、子网掩码（尽管格式较难解读）、广播地址和 MTU。

- 3. 全面了解某个系统上的网络流量非常有用，这正是多用途的 netstat 网络状态命令所提供的。

    ```
    # netstat
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address Foreign Address State
    tcp 0 208 10.10.2.200:ssh ds1-132.dsldesign:49172 ESTABLISHED

    Active UNIX domain sockets (w/o servers)
    Proto RefCnt Flags Type State I-Node Path
    unix 7 [ ] DGRAM 905 /dev/log
    unix 2 [ ] DGRAM 1226
    unix 2 [ ] DGRAM 1207
    unix 2 [ ] DGRAM 1162
    unix 2 [ ] DGRAM 961
    unix 2 [ ] DGRAM 914
    unix 2 [ ] STREAM CONNECTED 628
    ```

    ![](img/5ced0c78d748bd190e9027e5549a3622_361_1.png)

    默认情况下，第一部分显示处于活动状态的已建立网络连接（此处显示的是从 ds1-132.dsldesign 到 10.10.2.200 的 ssh 连接，连接 ID 为 49172）。第二部分是所有打开套接字的列表，其中一些与守护进程相关联，一些与特定文件（如 /dev/log）绑定，而且大多数相当难以理解。

    其他 Unix 系统上的 netstat 也会产生类似输出，但具体格式常有差异。Solaris 的输出格式尤其有帮助：

    ```
    # netstat

    TCP: IPv4
    Local Address Remote Address Swind Send-Q Rwind Recv-Q State
    solaris.32804 mac.6000 33304 0 66608 0 ESTABLISHED

    Active UNIX domain sockets
    Address Type Vnode Conn Local Addr Remote Addr
    e10c0d08 stream-ord 00000000 00000000
    e10cdea8 stream-ord 0be79920 00000000 /tmp/.X11-unix/X0
    ```

    清楚地表明正在发生远程 X11 事件。

    netstat 的各种标志会产生不同的输出。最有用的是 -a，它提供了另一种格式，既包含哪些协议在监听，也包含已建立的连接：

    ```
    # netstat -a

    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address Foreign Address State
    tcp 0 0 *:32768 *:* LISTEN
    tcp 0 0 localhost.localdomain:32769 *:* LISTEN
    tcp 0 0 *:sunrpc *:* LISTEN
    tcp 0 0 *:http *:* LISTEN
    tcp 0 0 *:ssh *:* LISTEN
    tcp 0 0 localhost.localdomain:smtp *:* LISTEN
    tcp 0 0 *:https *:* LISTEN
    tcp 0 224 10.10.2.200:ssh ds1-132.dsldesign:49172
    ->ESTABLISHED
    udp 0 0 *:32768 *:*
    udp 0 0 *:793 *:*
    udp 0 0 *:sunrpc *:*

    Active UNIX domain sockets (servers and established)
    Proto RefCnt Flags Type State I-Node Path
    unix 7 [ ] DGRAM 985 /dev/log
    unix 2 [ ] DGRAM 1226
    unix 2 [ ] DGRAM 1287
    unix 2 [ ] DGRAM 1162
    unix 2 [ ] DGRAM 961
    unix 2 [ ] DGRAM 914
    unix 2 [ ] STREAM CONNECTED 628
    ```

    我们可以看到，该系统支持 SunRPC（远程过程调用）、http（用于 Apache Web 服务器）、ssh（安全 Shell）、smtp（用于电子邮件）、https（安全的 Apache 连接），并且存在一个已建立的 ssh 连接。此外还有一些 UDP 监听器。

    netstat -a 的输出是一种验证方式，可以确认你认为已经禁用的服务实际上并没有在运行。（参见第 19 课时“运行 Internet 服务”，了解有关禁用服务的更多信息。）

- 4. 如果使用 -i 标志，netstat 命令还以非常简洁的方式提供发送/接收统计信息：

    ```
    # netstat -i
    Kernel Interface table
    Iface MTU Met RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
    eth0 1500 0 37597 0 0 0 36220 0 0 0 BMRU
    lo 16436 0 98 0 0 0 98 0 0 0 LRU
    ```

    这与 ifconfig 报告的内容一致：大量进出的数据包，且没有任何小故障或异常。

    Solaris 报告 Ipkts 和 Opkts（输入和输出）数据包，而不是 RX 和 TX 数据包，但除此之外，数据的呈现方式非常相似：

    ```
    # netstat -i
    Name Mtu Net/Dest Address Ipkts Ierrs Opkts Oerrs Collis Queue
    lo0 8232 loopback localhost 125 0 125 0 0 0
    pcn0 1500 198.76.82.128 solaris 6780 0 4728 0 0 0
    ```

    最后，Mac OS X 的有点不同寻常，但这段较长的输出中也包含了相同的基本信息：

    ```
    # netstat -i
    Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll
    lo0 16384 <Link> 1662 0 1662 0 0
    lo0 16384 127 localhost 1662 0 1662 0 0
    en0 1500 <Link> 00:30:65:3d:e8:10 6565 0 11226 0 0
    en0 1500 198.76.82.128 ds1-132.dsldesi 6565 0 11226 0 0
    ```

    Ipkts 是输入数据包（RX），Opkts 是输出数据包（TX）。

- 5. 让我们从分析系统转向探索网络连接本身。完成这一任务有两个基本工具：ping 和 traceroute。

    ping 命令的名字源自潜艇声纳在尝试识别远处物体时发出的声音，它会向指定的远程系统发送一个 ECHO_REQUEST 数据包，计算发送加上回波返回的时长，并将结果报告给你。

    按照惯例，使用 ping 的第一步始终是尝试检查与路由器的连接。如果路由器已启动并正常工作，我们就确认了网卡工作正常、以太网线没问题，并且这台计算机能够与其以太网卡通信。

    ```
    # ping -c 10 198.76.82.129
    PING 198.76.82.129 (198.76.82.129): 56 data bytes
    64 bytes from 198.76.82.129: icmp_seq=0 ttl=255 time=59.642 ms
    64 bytes from 198.76.82.129: icmp_seq=1 ttl=255 time=33.371 ms
    64 bytes from 198.76.82.129: icmp_seq=2 ttl=255 time=33.787 ms
    64 bytes from 198.76.82.129: icmp_seq=3 ttl=255 time=33.842 ms
    64 bytes from 198.76.82.129: icmp_seq=4 ttl=255 time=55.218 ms
    64 bytes from 198.76.82.129: icmp_seq=5 ttl=255 time=33.934 ms
    64 bytes from 198.76.82.129: icmp_seq=6 ttl=255 time=60.519 ms
    64 bytes from 198.76.82.129: icmp_seq=7 ttl=255 time=69.425 ms
    64 bytes from 198.76.82.129: icmp_seq=8 ttl=255 time=34.3 ms
    64 bytes from 198.76.82.129: icmp_seq=9 ttl=255 time=34.241 ms

    --- 198.76.82.129 ping statistics ---
    10 packets transmitted, 10 packets received, 0% packet loss
    round-trip min/avg/max = 33.371/44.827/69.425 ms
    ```

    -c 10 指定 ping 发送 10 个 ECHO_REQUEST 数据包，默认间隔一秒。每次 ping 都会显示各自的统计信息，从中可以看到系统的不确定性导致回波时间在 33.3 毫秒到 69.4 毫秒之间变化。最后两行最重要：丢失百分比（0%）和平均速度（44.8ms）。

    如果你不想看到逐行输出，-q 标志会将其隐藏，只显示第一行和最后一行输出，如下一个例子所示，其中 ping 显示了到“线路另一端”的连接速度，即我们 ISP 的一台 DNS 服务器：

    ```
    # ping -q -c10 dns1.dsldesigns.com
    PING dns1.dsldesigns.com (192.216.138.10): 56 data bytes

    --- dns1.dsldesigns.com ping statistics ---
    10 packets transmitted, 10 packets received, 0% packet loss
    round-trip min/avg/max = 33.851/58.407/113.713 ms
    ```

    性能与本地路由器非常相似，因此它们之间的连接显然不会造成明显的减速。

