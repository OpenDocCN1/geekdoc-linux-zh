
```
[root@server1 root]# mail
Mail version 8.1 6/6/93. Type ? for help.
"/var/spool/mail/root": 27 messages 27 unread
>U 1 root@localhost.local Sat Jul 24 00:24 22/850 "Anacron job `cron.daily'"
U 2 root@localhost.local Sat Jul 24 04:02 108/3362 "LogWatch for server1"
U 3 root@localhost.local Sat Jul 24 04:08 26/977 "Cron `root@server1'"
U 4 root@localhost.local Wed Jul 28 20:43 22/850 "Anacron job `cron.daily'"
U 5 root@localhost.local Thu Jul 29 13:59 63/1795 "LogWatch for server1"
U 6 root@localhost.local Thu Jul 29 14:06 22/850 "Anacron job `cron.daily'"
U 7 root@localhost.local Fri Jul 30 19:17 1123/3686 "LogWatch for server1"
U 8 root@localhost.local Fri Jul 30 19:25 22/850 "Anacron job `cron.daily'"
U 9 root@localhost.local Sat Jul 31 10:28 121/3509 "LogWatch for server1"
U 10 root@localhost.local Sat Jul 31 10:35 22/850 "Anacron job `cron.daily'"
U 11 root@localhost.local Sun Aug 1 08:17 138/4319 "LogWatch for server1"
U 12 root@localhost.local Sun Aug 1 08:25 22/847 "Anacron job `cron.daily'"
U 13 root@localhost.local Mon Aug 2 04:02 105/2949 "LogWatch for server1"
U 14 root@localhost.local Mon Aug 2 04:08 26/974 "Cron `root@server1'"
U 15 root@localhost.local Tue Aug 2 11:07 499/36033 "server1 08/02/04:11.0"
U 16 root@localhost.local Tue Aug 3 12:40 111/3310 "LogWatch for server1"
U 17 root@localhost.local Tue Aug 3 12:48 22/847 "Anacron job `cron.daily'"
U 18 root@localhost.local Mon Aug 9 13:17 21/793 "Low disk space warning"
U 19 root@localhost.local Mon Aug 9 14:01 21/793 "Low disk space warning"
U 20 root@localhost.local Mon Aug 9 14:33 22/847 "Anacron job `cron.daily'"
```

接下来，您只需在 `&` 提示符下输入适当的编号即可阅读消息。类似地，您可以通过使用 `d` 命令后跟消息编号来删除消息，或者在 `&` 提示符下输入 `q` 命令退出 `mail` 实用程序。

另一种可以在终端中运行的流行邮件用户代理是 `mutt`，它在屏幕顶部显示常用功能列表，并允许您使用键盘上的光标键显示电子邮件消息。`mutt` 实用程序的一个示例如图 14-15 所示。

![](img/09bf13b782f71165e17bb3839040c96a_576_0.png)

图 14-13 在 Mozilla 邮件中配置邮件账户

![](img/09bf13b782f71165e17bb3839040c96a_576_1.png)

图 14-14 使用 Mozilla 邮件

![](img/09bf13b782f71165e17bb3839040c96a_577_0.png)

## 本章小结

- 网络是相互连接并共享信息的计算机的集合。
- 协议定义了通过网络传输的信息格式。互联网和大多数网络使用的协议是 `TCP/IP`。
- 每个 `TCP/IP` 网络上的计算机都必须拥有一个有效的 `IP` 地址和子网掩码。
- `/etc/sysconfig/network-scripts` 目录包含 `NIC` 和 `PPP` 接口的配置。
- 网络接口的 `TCP/IP` 配置可以手动指定，也可以从 `DHCP` 或 `BOOTP` 服务器自动获取。
- 主机名用于轻松识别网络上的计算机；遵循域名空间的主机名称称为完全限定域名。
- 在进行网络通信之前，必须将主机名解析为 `IP` 地址。
- 文件、应用程序和电子邮件可以通过相应的网络实用程序跨网络访问。

## 关键术语

**与运算（ANDing）** — 通过比较二进制位来从 `IP` 地址和子网掩码计算网络 `ID` 和主机 `ID` 的过程。

**广播** — 发送给网络上所有计算机的 `TCP/IP` 通信。

**无类域间路由（CIDR）表示法** — 一种常用于表示 `IP` 地址及其子网掩码的表示法。

**默认网关** — 用于向远程网络发送数据包的路由器的 `IP` 地址。

**域名空间（DNS）** — 用于主机名的分层命名空间。

**以太网** — 当今网络中最常见的媒体访问方法。

**完全限定域名（FQDN）** — 遵循 `DNS` 约定的主机名。

**ftp 实用程序** — 一种可用于从 `FTP` 服务器下载文件的实用程序。

**主机 ID** — `IP` 地址中标识主机的部分。

**主机名** — 分配给计算机的用户友好名称。

**hostname 命令** — 用于显示和更改计算机主机名的命令。

**ifconfig 命令** — 用于显示和修改网络接口 `TCP/IP` 配置信息的命令。

**互联网协议（IP）地址** — 由四个 8 位数字组成的序列，表示网络上的计算机。

**互联网服务提供商（ISP）** — 提供互联网接入的公司。

**局域网（LANs）** — 计算机在物理上彼此接近的网络。

**mail 实用程序** — 一种常见的 Linux 邮件用户代理。

**媒体访问方法** — 定义网络上计算机如何共享访问物理介质的系统。

**组播** — 发送给特定计算机组的 `TCP/IP` 通信。

**mutt 实用程序** — 一种常见的 Linux 邮件用户代理。

**网络** — 通过网络介质连接在一起并能够交换信息的两台或多台计算机。

**网络 ID** — `IP` 地址中标识网络的部分。

**八位组** — `IP` 地址中表示八个二进制位的部分。

**包互联网寻呼机（ping）命令** — 用于检查网络上 `TCP/IP` 连接性的命令。

**数据包** — 由网络协议格式化的数据包。

**协议** — 网络上计算机之间使用的通信规则集。

**路由器** — 能够将数据包从一个网络传输到另一个网络的设备。

**安全外壳（ssh）** — 一种可用于在 Linux 计算机上运行远程应用程序的实用程序；它加密所有客户端-服务器流量。

**smbclient 实用程序** — 一种用于连接到 Windows 系统共享的实用程序。

**smbmount 命令** — 一种用于将 Windows 计算机上的目录挂载到 Linux 计算机上挂载点的命令。

**子网掩码** — 由四个 8 位数字组成的序列，确定 `IP` 地址的网络部分和主机部分。

**子网划分** — 将单个大型网络细分为几个较小的网络以控制数据流的过程。

**telnet** — 一种可用于在 Linux 计算机上运行远程应用程序的实用程序。

**令牌环** — 一种流行的媒体访问方法。

**可信访问** — 一种配置，允许计算机在无需首先提供密码的情况下访问给定计算机。

**单播** — 发送给单台计算机的 `TCP/IP` 通信。

**广域网（WANs）** — 计算机在地理上被大距离分隔开的网络。

## 复习题

1. 目前最常用的局域网（`LAN`）协议是什么？
   a. `DLC`
   b. `AppleTalk`
   c. `IPX/SPX`
   d. `TCP/IP`

2. `C` 类 `IP` 地址的子网掩码是什么？
   a. `0.0.0.0`
   b. `255.0.0.0`
   c. `255.255.0.0`
   d. `255.255.255.0`

3. 以下哪一种是北美地区常用的高速连接技术？
   a. 调制解调器 (modems)
