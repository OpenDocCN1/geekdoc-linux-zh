
以及从 ISP 获得的 IP 配置。当 xDSL 接口激活时，以下输出展示了 `ifconfig` 命令的输出结果：

```
[root@server1 root]# ifconfig
eth0
  Link encap:Ethernet  HWaddr 00:80:6C:F9:1B:8C
  inet addr:3.4.5.6  Bcast:255.255.255.255  Mask:255.0.0.0
  inet6 addr: fe80::280:6cff:fe9:1b8c/64 Scope:Link
  UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
  RX packets:47 errors:0 dropped:0 overruns:0 frame:0
  TX packets:13 errors:5 dropped:0 overruns:0 carrier:5
  collisions:0 txqueuelen:1000
  RX bytes:5560 (5.4 Kb)  TX bytes:770 (770.0 b)
  Interrupt:10 Base address:0x8000

lo
  Link encap:Local Loopback
  inet addr:127.0.0.1  Mask:255.0.0.0
  inet6 addr: ::1/128 Scope:Host
  UP LOOPBACK RUNNING  MTU:16436  Metric:1
  RX packets:3457 errors:0 dropped:0 overruns:0 frame:0
  TX packets:3457 errors:0 dropped:0 overruns:0 carrier:0
  collisions:0 txqueuelen:0
  RX bytes:3528110 (3.3 Mb)  TX bytes:3528110 (3.3 Mb)

ppp0
  Link encap:Point-to-Point Protocol
  inet addr:65.95.13.21  P-t-P:65.95.13.1  Mask:255.255.255.255
  UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1492  Metric:1
  RX packets:15 errors:0 dropped:0 overruns:0 frame:0
  TX packets:31 errors:0 dropped:0 overruns:0 carrier:0
  collisions:0 txqueuelen:3
  RX bytes:1448 (1.4 Kb)  TX bytes:3088 (3.0 Kb)
[root@server1 root]#
```

## 名称解析

在 TCP/IP 网络上通信的计算机使用唯一的 IP 地址来标识自身；然而，这种标识方案对人类使用来说不切实际，因为 IP 地址难以记忆。因此，计算机通过名称进行标识；由于网络上的每台计算机通常被称为主机（host），因此计算机名称被称为主机名（host names）。

对于参与互联网通信的计算机，很少使用简单的主机名；相反，它们被赋予一个名为**完全限定域名 (FQDN)**的主机名，这是根据一种称为**域名空间 (DNS)**的层次化命名方案命名的。域名空间由一个虚拟的根组成，根下有几个顶级域名，这些域名标识了运行你所在网络的机构类型。每个顶级域名下面存在若干二级域名，用于标识机构的名称，而简单的主机名列在二级域名之下，如 14-11 图所示。

![](img/09bf13b782f71165e17bb3839040c96a_562_0.png)

**图 14-11** *域名空间*

因此，14-11 图中所示的主机计算机的 FQDN 为 www.linux.org。

你可以使用**hostname 命令**来查看或设置 Linux 计算机的主机名，如下面的输出所示：

```text
[root@server1 root]# hostname
server1
[root@server1 root]# hostname computer1.sampledomain.com
[root@server1 root]# hostname
computer1.sampledomain.com
[root@server1 root]#
```

要在每次启动时配置前文中输出的主机名，只需修改 /etc/sysconfig/network 文件中的 HOSTNAME 行，如下例所示：

```text
[root@server1 root]# cat /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=server1
[root@server1 root]#
```

# **注意**

在安装前规划合适的主机名是一种良好的实践，因为许多应用程序在安装过程中会在其配置文件中记录该主机名。如果在安装后更改主机名，你可能需要修改这些文件。

虽然主机名在指定网络上的计算机时比 IP 地址更容易使用，但 TCP/IP 无法使用它们来标识计算机。因此，你必须将主机名映射到其关联的 IP 地址，以便通过网络联系其他计算机的应用程序能够找到特定主机名对应的合适 IP 地址。

将主机名映射到 IP 地址最简单的方法是向 /etc/hosts 文件中添加条目，如下例所示：

```
[root@server1 root]$ cat /etc/hosts
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1	server1 localhost.localdomain localhost
3.0.0.2	ftp.sampledomain.com fileserver
192.168.0.1	alpha
[root@server1 root]$ _
```

上述输出中的条目通过主机名 server1、localhost.localdomain 和 localhost 标识本地计算机 127.0.0.1。同样，你可以使用主机名 ftp.sampledomain.com 或 fileserver 来引用 IP 地址为 3.0.0.2 的计算机。此外，IP 地址为 192.168.0.1 的计算机被映射到主机名 alpha。

![](img/09bf13b782f71165e17bb3839040c96a_563_0.png)

> 你可以使用网络信息服务 (NIS) 在网络中的多台 Linux 计算机之间共享 /etc/hosts 配置文件。NIS 在第 15 章“配置网络服务和安全”中进行了讨论。

由于在互联网上的所有主机名称都列入 /etc/hosts 文件会非常繁琐，ISP 可以在互联网上的 DNS 服务器中列出 FQDN。应用程序随后可以向 DNS 服务器查询与特定 FQDN 关联的 IP 地址。要配置系统通过联系 DNS 服务器来将名称解析为 IP 地址，只需在 /etc/resolv.conf 文件中指定 DNS 服务器的 IP 地址即可。该文件最多可以包含三个 DNS 服务器；如果第一个 DNS 服务器不可用，系统将尝试联系文件列出的第二个 DNS 服务器，然后是第三个 DNS 服务器。以下输出展示了一个 /etc/resolv.conf 文件示例：

```
[root@server1 root]$ cat /etc/resolv.conf
nameserver 209.121.197.2
nameserver 192.139.188.144
nameserver 6.0.4.211
[root@server1 root]$ _
```

![](img/09bf13b782f71165e17bb3839040c96a_564_0.png)

# **注意**

要通过将名称解析为 IP 地址来测试 DNS 配置，你可以在命令提示符下输入 `nslookup name`、`dig name` 或 `host name`，其中 *name* 是远程主机的主机名或 FQDN。

当使用某个应用程序并指定主机名时，该应用程序必须通过搜索本地 /etc/hosts 文件、DNS 服务器或 NIS 服务器来将该主机名解析为合适的 IP 地址。应用程序解析主机名的方法由 /etc/nsswitch.conf 文件中的 "hosts" 行决定；该文件的一个示例如下所示：

```
[root@server1 root]# grep hosts /etc/nsswitch.conf
hosts:      files dns nis
[root@server1 root]# _
```

上述输出表明，应用程序首先尝试使用 /etc/hosts 文件（files）来解析主机名。如果失败，应用程序将联系 /etc/resolv.conf（dns）中列出的 DNS 服务器，随后如果配置了 NIS 服务器，则联系 NIS 服务器（nis）。

在较旧的 Linux 编译器上，使用 /etc/host.conf 文件代替 /etc/nsswitch.conf；/etc/host.conf 文件至今仍存在，以支持较旧的应用程序，并且应包含与 /etc/nsswitch.conf 相同的名称解析顺序。以下输出展示了一个 /etc/host.conf 文件示例，它指示应用程序先搜索 /etc/hosts 文件，然后搜索 DNS 服务器（bind）和 NIS 服务器：

```
[root@server1 root]# cat /etc/host.conf
order hosts,bind,nis
[root@server1 root]# _
```

## 连接网络资源

在配置了网络接口后，Linux 计算机可以使用网络上的资源，例如共享打印机、应用程序和文件。要使用网络资源，你首先必须拥有能够连接到该资源的合适网络工具。一些网络工具易于使用，例如使用 Web 浏览器访问网络上的 Web 服务器上的 Web 页面，而其他网络工具如 FTP 要求你在使用前学习特定命令。

本节介绍了用于在系统上执行各种网络任务的最常见的网络工具。

### 使用 FTP 下载文件

跨互联网传输文件最常用的方法是使用文件传输协议 (FTP)，如第 1 章“Linux 简介”中所述。大多数 Web 浏览器内置了 FTP 工具，允许你输入形如 `ftp://ftp.sampledomain.com` 的 FQDN，并使用 Web 浏览器屏幕查看远程计算机上公开可用的文件和目录，如 14-12 图所示。

![](img/09bf13b782f71165e17bb3839040c96a_565_0.png)

> 你也可以使用 `ftp://IP_address` 连接公共 FTP 服务器，而无需进行名称解析。

![](img/09bf13b782f71165e17bb3839040c96a_565_1.png)

**图 14-12** *使用 Web 浏览器 FTP 客户端*

使用鼠标点击 14-12 图中显示的文件，会出现一个对话框，允许你将文件保存到本地文件系统的适当位置。

或者，你可以将运行 FTP 服务的计算机的主机名或 IP 地址作为参数指定给 `ftp utility`，以打开一个允许向该计算机传输文件或从该计算机传输文件的连接。随后，你可以以该计算机上的有效用户身份登录，并被放置在该计算机的主目录中，或者以用户 “anonymous” 登录，并

