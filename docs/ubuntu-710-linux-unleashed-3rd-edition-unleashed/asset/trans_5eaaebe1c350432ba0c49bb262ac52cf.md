
on in this chapter) uses this interface to assign an IP address to your computer and is needed for Ubuntu to establish a PPP interface.

## 检查环回接口的可用性

你通常不需要手动创建环回接口，因为 Ubuntu 在安装期间会自动为你创建。 要检查是否已设置，可以使用 ifconfig 命令显示类似以下内容的信息：

```
$ ifconfig
lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:13 errors:0 dropped:0 overruns:0 frame:0
          TX packets:13 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:832 (832.0 b)  TX bytes:832 (832.0 b)
```

你在此示例中看到的内容证明环回接口存在且处于活动状态。 inet addr 是分配给 localhost 的 IP 号码，通常为 127.0.0.1 以及广播掩码 255.255.255.0，并且该接口的活动很少（RX = 接收，TX = 发送）。 如果你的输出与上面不同，你必须在完成本节其余部分后手动配置 localhost 接口。

## 手动配置环回接口

localhost 接口的 IP 地址指定在一个文本配置文件中，Ubuntu 使用该文件来记录各种网络范围的 IP 地址。 该文件称为 /etc/hosts，通常存在于系统上，即使它是空的。 该文件被 Linux 内核和其他网络工具使用，使它们能够访问本地 IP 地址和主机名。 如果你尚未配置任何其他网络接口，那么你可能会发现该文件只包含一行：

```
127.0.0.1      localhost.localdomain      localhost
```

此行定义了特殊的 localhost 接口，并为其分配了 127.0.0.1 的 IP 地址。 你可能会听到或读到 localhost、loopback 和 dummy interface 等术语； 所有这些术语都指的是使用 IP 地址 127.0.0.1。 术语环回接口表示对 Linux 网络驱动程序而言，看起来机器正在与仅由一台机器组成的网络对话； 内核在同一台计算机上向自身发送和接收网络流量。 虚拟接口表示就外部世界而言接口实际上不存在； 它仅为本地机器存在。

/etc/hosts 文件以添加 localhost 条目，然后使用 ifconfig 和 route 命令并使用你的 sudo 权限来创建接口，如下所示：

```
$ sudo /sbin/ifconfig lo 127.0.0.1
$ sudo /sbin/route add 127.0.0.1 lo
```

这些命令将在内存中创建 localhost 接口（所有接口，例如 eth0 或 ppp0，在使用 Linux 时都在内存中创建），然后将 IP 地址 127.0.0.1 添加到内部（内存）表中，以便 Linux 内核的网络代码可以跟踪到不同地址的路由。

使用 ifconfig 命令如前所示来测试接口。

你现在应该能够使用 ping 来检查接口是否正常响应，如下所示（使用 localhost 或其 IP 地址）：

```
$ ping -c 3 localhost
PING localhost (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.036 ms
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.028 ms
64 bytes from localhost (127.0.0.1): icmp_seq=3 ttl=64 time=0.028 ms

--- localhost ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 0.028/0.030/0.036/0.007 ms
```

-c 选项用于设置 ping 的次数，并且命令如果成功（像之前一样），将返回有关向指定主机发送测试数据包的往返速度的信息。

## 使用 TCP/IP 进行网络连接

基于 Unix 主机的任何网络的基本构建块都是传输控制协议/互联网协议（TCP/IP）套件中的三个协议。 该套件由互联网协议（IP）、传输控制协议（TCP）和通用数据报协议（UDP）组成。 IP 是基础协议。 TCP/IP 套件基于数据包，这意味着数据在发送端被拆分为小块以传输到接收端。 将数据拆分为可管理的包可以实现更快、更准确的传输。 在 TCP/IP 中，所有数据都通过 IP 数据包传输，这就是为什么地址被称为 IP 地址。 它是套件的最低层级。

TCP 是一种基于连接的协议。 在两台机器之间传输数据之前，会在它们之间建立连接。 建立连接后，一串数据被发送到 IP 以拆分为然后传输的数据包。 在接收端，数据包被重新排序并发送到正确的应用程序端口。 TCP/IP
