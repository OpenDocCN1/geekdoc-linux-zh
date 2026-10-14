

通过在 traceroute 命令中添加 -T 或 -I 选项来克服这个问题。

## ip

ip 程序是一个多用途的网络配置工具，它利用了现代 Linux 内核中可用的全套网络功能。它取代了早期的 ifconfig 程序，现已弃用。使用 ip，我们可以检查系统的网络接口和路由表。

```
[me@linuxbox ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN
   group default
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP
   group default qlen 1000
   link/ether ac:22:0b:52:cf:84 brd ff:ff:ff:ff:ff:ff
   inet 192.168.1.14/24 brd 192.168.1.255 scope global eth0
       valid_lft forever preferred_lft forever
   inet6 fe80::ae22:bff:fe52:cf84/64 scope link
       valid_lft forever preferred_lft forever
```

在前面的示例中，我们看到测试系统有两个网络接口。第一个名为 lo，是环回接口，一个虚拟接口，系统用它来“自说自话”，第二个名为 eth0，是以太网接口。

在进行非正式的网络诊断时，需要注意的重要事项是每个接口的第一行中是否存在单词 UP，表示网络接口已启用，以及第三行的 inet 字段中是否存在有效的 IP 地址。对于使用动态主机配置协议（DHCP）的系统，该字段中的有效 IP 地址将验证 DHCP 是否正常工作。

## netstat

netstat 程序用于检查各种网络设置和统计信息。通过使用其众多选项，我们可以查看网络设置中的各种功能。使用 -ie 选项，我们可以检查系统中的网络接口。

```
[me@linuxbox ~]$ netstat -ie
eth0      Link encap:Ethernet  HWaddr 00:1d:09:9b:99:67
          inet addr:192.168.1.2  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::21d:9ff:fe9b:9967/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:238488  errors:0  dropped:0  overruns:0  frame:0
          TX packets:403217  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:100 
          RX bytes:153098921 (146.0 MB)  TX bytes:261035246 (248.9 MB)
          Memory:fdfc0000-fdfe0000

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:2208  errors:0  dropped:0  overruns:0  frame:0
          TX packets:2208  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:0 
          RX bytes:111490 (108.8 KB)  TX bytes:111490 (108.8 KB)
```

使用 -r 选项将显示内核的网络路由表。这显示了网络如何配置以在网络之间发送数据包：

```
[me@linuxbox ~]$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
192.168.1.0     *               255.255.255.0   U       0   0       0   eth0
default         192.168.1.1     0.0.0.0         UG      0   0       0   eth0
```

在这个简单的示例中，我们看到防火墙/路由器后面局域网（LAN）上客户端机器的典型路由表。列表的第一行显示目标为 192.168.1.0。以零结尾的 IP 地址指的是网络而不是单个主机，因此此目标表示 LAN 上的任何主机。下一个字段 Gateway 是用于从当前主机到目标网络的网关（路由器）的名称或 IP 地址。此字段中的星号表示不需要网关。

最后一行包含目标 default。这意味着发往表中未列出的任何网络的流量。在我们的示例中，我们看到网关被定义为地址为 192.168.1.1 的路由器，它 presumably 知道如何处理目标流量。

与 ip 类似，netstat 程序有许多选项，我们只查看了其中几个。查看 ip 和 netstat 手册页以获取完整列表。

## 在网络上传输文件

如果不能在网络上传输文件，网络有什么用呢？有许多程序可以在网络上传输数据。我们现在将介绍其中两个，并在后面的章节中介绍更多。

## ftp

ftp 是真正的“经典”程序之一，它的名字来源于它使用的协议，即文件传输协议。FTP 曾经是互联网上下载文件的最广泛使用的方法。大多数，如果不是全部，网络浏览器都支持它，你经常会看到以协议 ftp:// 开头的 URI。

在有网络浏览器之前，就有 ftp 程序。ftp 用于与 FTP 服务器通信，这些机器包含可以通过网络上传和下载的文件。

FTP（在其原始形式中）是不安全的，因为它以明文形式发送账户名和密码。这意味着它们未加密，任何嗅探网络的人都可以看到它们。正因为如此，几乎所有通过互联网进行的 FTP 都是通过匿名 FTP 服务器进行的。匿名服务器允许任何人使用登录名“anonymous”和无意义的密码登录。
