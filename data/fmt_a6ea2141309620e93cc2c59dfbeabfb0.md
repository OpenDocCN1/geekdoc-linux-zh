
```
1  ipcop.localdomain (192.168.1.1)  1.066 ms  1.366 ms  1.720 ms

2  * * *

3  ge-4-13-ur01.rockville.md.bad.comcast.net (68.87.130.9)  14.622 ms  14.885 ms  15.169 ms

4  po-30-ur02.rockville.md.bad.comcast.net (68.87.129.154)  17.634 ms  17.626 ms  17.899 ms

5  po-50-ur02.rockville.md.bad.comcast.net (68.87.129.158)  15.992 ms  15.983 ms  16.256 ms

6  po-30-ar01.howardcounty.md.bad.comcast.net (68.87.136.5)  22.835 ms  14.23 ms  14.405 ms

7  po-10-ar02.whitemarsh.md.bad.comcast.net (68.87.129.34)  16.154 ms  13.600 ms  18.867 ms

8  te-0-3-0-1-cr01.philadelphia.pa.ibone.comcast.net (68.86.90.77)  21.951 ms  21.073 ms  21.557 ms

9  pos-0-8-0-0-cr01.newyork.ny.ibone.comcast.net (68.86.85.10)  22.917 ms  21.884 ms  22.126 ms

10  204.70.144.1 (204.70.144.1)  43.110 ms  21.248 ms  21.264 ms

11  cr1-pos-0-7-3-1.newyork.savvis.net (204.70.195.93)  21.857 ms  cr2-pos-0-0-3-1.newyork.savvis.net (204.70.204.238)  19.556 ms  cr1-pos-0-7-3-1.newyork.savvis.net (204.70.195.93)  19.634 ms

12  cr1-pos-0-7-3-0.chicago.savvis.net (204.70.192.109)  41.586 ms  42.843 ms  cr2-tengig-0-0-2-0.chicago.savvis.net (204.70.196.242)  43.115 ms

13  hr2-tengigabitethernet-12-1.elkgrovech3.savvis.net (204.70.195.122)  44.215 ms  41.833 ms  45.658 ms

14  csr1-ve241.elkgrovech3.savvis.net (216.64.194.42)  46.840 ms  43.372 ms  47.041 ms

15  64.27.160.194 (64.27.160.194)  56.137 ms  55.887 ms  52.810 ms

16  slashdot.org (216.34.181.45)  42.727 ms  42.016 ms  41.437 ms
```

从输出中可以看到，从我们的测试系统连接到 `http://www.slashdot.org/` 需要经过 16 个路由器。对于提供标识信息的路由器，我们会看到它们的主机名、IP 地址和性能数据，其中包括从本地系统到该路由器的三次往返时间采样。对于不提供标识信息的路由器（由于路由器配置、网络拥塞、防火墙等原因），我们会看到星号，如第二跳那一行所示。

## netstat——检查网络设置和统计信息

`netstat` 程序用于检查各种网络设置和统计信息。通过使用它的众多选项，我们可以查看网络配置中的各种特性。使用 `-ie` 选项，我们可以检查系统中的网络接口：

```
[me@linuxbox ~]$ netstat -ie

eth0

Link encap:Ethernet HWaddr 00:10:9b:99:67

inet addr:192.168.1.2 Bcast:192.168.1.255 Mask:255.255.255.0

inet6 addr: fe80::214:ff:fe9b:967/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:238488 errors:0 dropped:0 overruns:0 frame:0

TX packets:403217 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:100

RX bytes:15308921 (14.6 MB) TX bytes:261035246 (248.9 MB)

Memory:fdc00000-fdfe0000

lo

Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0.0

inet6 addr: ::1/128 Scope:Host

UP LOOPBACK RUNNING MTU:16436 Metric:1

RX packets:2208 errors:0 dropped:0 overruns:0 frame:0

TX packets:2208 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:0

RX bytes:111490 (108.8 KB) TX bytes:111490 (108.8 KB)
```

在上面的示例中，我们看到测试系统有两个网络接口。第一个名为 `eth0`，是以太网接口；第二个名为 `lo`，是回环接口，一种系统用来“与自己通信”的虚拟接口。

使用 `-r` 选项将显示内核的网络路由表。这显示了网络如何配置以将数据包从一个网络发送到另一个网络：

```
[me@linuxbox ~]$ netstat -r

Kernel IP routing table

Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface

192.168.1.0     *               255.255.255.0   U         0     0          0 eth0

default         192.168.1.1     0.0.0.0         UG        0     0          0 eth0
```

在这个简单的示例中，我们看到防火墙/路由器后面局域网（LAN）上客户端机器的典型路由表。列表的第一行显示目标为 `192.168.1.0`。IP地址以零结尾指的是网络而不是单个主机，因此此目标表示 LAN 上的任何主机。下一个字段，`Gateway`，是用于从当前主机到目标网络的网关（路由器）的名称或 IP 地址。此字段中的星号表示不需要网关。

最后一行包含目标 `default`。这表示发往表中未另行列出的网络的任何流量。在我们的示例中，我们看到网关被定义为地址为 `192.168.1.1` 的路由器，它 presumably 知道如何处理目标流量。

`netstat` 程序有许多选项，我们只查看了其中几个。查看 `netstat` 手册页以获取完整列表。

## 在网络上传输文件

如果我们不知道如何跨网络移动文件，网络有什么用呢？有许多程序可以在网络上传输数据。我们现在将介绍其中两个，并在后面的章节中介绍更多。

### ftp—使用文件传输协议传输文件

`ftp` 是真正的“经典”程序之一，它的名字来源于其使用的协议，即文件传输协议。`FTP` 在互联网上被广泛用于文件下载。大多数，如果不是全部，网络浏览器都支持它，你经常会看到以协议 `ftp://` 开头的 URI。

在出现网络浏览器之前，就有 `ftp` 程序。`ftp` 用于与 FTP 服务器通信，这些机器包含可以通过网络上传和下载的文件。

`FTP`（在其原始形式中）是不安全的，因为它以明文形式发送账户名和密码。这意味着它们未被加密，任何嗅探网络的人都可以看到它们。正因为如此，几乎所有通过互联网进行的 FTP 都是通过匿名 FTP 服务器进行的。匿名服务器允许任何人使用登录名 `anonymous` 和无意义的密码登录。

在下面的示例中，我们展示了使用 `ftp` 程序从匿名 FTP 服务器 `fileserver` 的 `/pub/cd_images/Ubuntu-8.04` 目录下载 Ubuntu ISO 映像的典型会话。

```
[me@linuxbox ~]$ ftp fileserver

Connected to fileserver.localdomain.

220 (vsFTPd 2.0.1)

Name (fileserver:me): anonymous
```
