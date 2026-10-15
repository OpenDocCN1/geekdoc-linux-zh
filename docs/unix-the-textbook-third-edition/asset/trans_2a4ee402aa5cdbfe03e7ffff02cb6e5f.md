

该方案存在两个问题。首先，其实现取决于系统管理员如何配置系统。其次，由于互联网的庞大规模及其当前的增长速度，静态文件可能非常庞大。

你可以使用 ifconfig 命令查看和设置网络接口参数，包括 IP 地址、localhost、网络掩码、广播地址和最大传输单元（MTU）。网络掩码，也称为子网掩码，是 TCP/IP 使用的位掩码，用于识别主机是否在远程网络上或本地子网上。广播地址由主机中的 IP 层使用，用于将数据报发送到子网上的所有主机或远程网络。Ethernet 广播地址为全 1。TCP/IP 网络中的 MTU 是 IP 数据报（数据包）的最大大小，取决于用于连接到其他主机的链路层技术。以下是该命令在 Solaris 上的一个示例运行。命令输出显示你登录到一台主机，该主机具有 localhost 以及 IPv4 和 IPv6 地址的网络接口。对于 IPv4，localhost 为 127.0.0.1，MTU 为 8232 字节，网络掩码为 ff000000；网络 IP 地址为 202.147.169.197，MTU 为 1500 字节，网络掩码为 ffffffe0；广播 IP 地址为 202.147.169.223。对于 IPv6，localhost 为 ::1，MTU 为 8252 字节，外部流量的 IP 地址为 fe80::dad3:85ff:fe7b:21fe，MTU 为 1500 字节。系统管理员可以启用或禁用这些接口或其任何参数。关于该命令输出及其用于查看和设置各种网络参数的各种选项的进一步讨论超出了本书的范围。

```
$ ifconfig -a
lo0: flags=2001000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4,VIRTUAL>
mtu 8232 index 1 inet 127.0.0.1 netmask ff000000
net0: flags=10001000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4,PHYSRUNNING> mtu 1500 index 2 inet 202.147.169.197 netmask ffffffe0
broadcast 202.147.169.223
lo0: flags=2002000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv6,VIRTUAL>
mtu 8252 index 1 inet6 ::1/128
net0: flags=120002004841<UP,RUNNING,MULTICAST,DHCP,IPv6,PHYSRUNNING> mtu 1500 index 2 inet6 fe80::dad3:85ff:fe7b:21fe/10
$
```

ifconfig 命令通常位于 PC-BSD 上的 /sbin 目录和 Solaris 上的 /usr/bin 目录中。如果出现诸如 ifconfig: Command not found 之类的错误消息，你应该在搜索路径中包含相关目录并重新执行该命令。你可以运行 cat /etc/hosts 命令来显示网络上主机的域名和 IP 地址。

你可以使用 host 命令对作为命令行参数传递给它的主机的域名执行 DNS 查找。该命令允许你显示域名对应的 IP 地址或反之。在以下会话中，我们使用 host 命令显示主机 iastate.edu、berkeley.edu 和 facebook.com 的 IP 地址，以及两个 IPv6 地址对应的域名。host iastate.edu 命令的输出显示了 iastate.edu（爱荷华州立大学）的 IPv4 和 IPv6 地址。它还显示有 10 台机器处理爱荷华州的电子邮件。第二条命令的输出显示给定的 IPv6 地址属于 thumb.iastate.edu。第四条和第六条命令的输出显示了 berkeley.edu 和 facebook.com 的 IPv4 和 IPv6 地址，以及它们各自有 10 台主机处理电子邮件。最后一条命令的输出显示名称服务器未能将 IP 地址 198.175.96.33 映射到任何域名，这并不意味着该域名不存在。

```
% host iastate.edu
iastate.edu has address 129.186.1.99
iastate.edu has IPv6 address 2610:130:101:100::9
iastate.edu mail is handled by 10 mailin.iastate.edu.
% host 2610:130:101:100::9
9.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.1.0.1.0.1.0.0.3.1.0.0.1.6.2.i
p6.arpa domain name pointer thumb.iastate.edu.
% host thumb.iastate.edu
thumb.iastate.edu has address 129.186.1.99
thumb.iastate.edu has IPv6 address 2610:130:101:100::9
% host berkeley.edu
berkeley.edu has address 169.229.216.200
berkeley.edu has IPv6 address 2607:f140:0:81::f
berkeley.edu mail is handled by 10 mx.berkeley.edu.
% host 2607:f140:0:81::f
f.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.1.8.0.0.0.0.0.0.0.0.4.1.f.7.0.6.2
i.p6.arpa domain name pointer wf-web-prod-03.IST.Berkeley.EDU.
% host facebook.com
facebook.com has address 173.252.120.6
facebook.com has IPv6 address 2a03:2880:2130:cf05:face:b00c:0:1
facebook.com mail is handled by 10 msgin.vvv.facebook.com.
% host 198.175.96.33
Host 33.96.175.198.in-addr.arpa not found: 3 (NXDOMAIN)
%
```

在 Solaris 和某些其他 UNIX 系统上，你可以使用 nslookup 命令执行 DNS 查找。以下是该命令的一个示例运行。

```
$ nslookup stanford.edu
Server:              208.67.222.222
Address:  208.67.222.222#53

Non-authoritative answer:
Name:    stanford.edu
Address: 171.67.215.200
$
```
