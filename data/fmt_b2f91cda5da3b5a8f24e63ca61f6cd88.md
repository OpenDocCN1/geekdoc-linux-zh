
与配置网卡（`NIC`）类似，Internet 配置向导将设备信息存储在 `/etc/sysconfig/network-scripts` 目录下的字段中。之前配置的调制解器存储在 `/etc/sysconfig/network-scripts/ifcfg-pp0` 文件，而 `ISDN` 信息存储在 `/etc/sysconfig/network-scripts/ifcfg-isdn0`，`DSL` 信息存储在 `/etc/sysconfig/network-scripts/ifcfg-pp01` 中。这些文件如输出所示：

```
[root@localhost ~]# cat /etc/sysconfig/network-scripts/ifcfg-pp0
USERCTL=yes
BOOTPROTO=dialup
NAME=sample_ISP
DEVICE=pp0
TYPE=Modem
ONBOOT=no
BSDCOMP=off
CCP=off
VJCCMP=off
AC=off
VJ=off
PC=off
LINESPEED=115200
MODEMPORT=/dev/modem
DEMAND=no
PROVIDER=sample_ISP
DEFROUTE=no
PERSIST=no
PAPNAME=user1
WVDALSECT=sample_ISP
```

```
MODEMNAME=Modem0
PEERDNS=yes
[root@localhost root]# cat /etc/sysconfig/network-scripts/ifcfg-isdn0
USERCTL=yes
BOOTPROTO=dialup
DEVICE=isdn0
TYPE=ISDN
ONBOOT=off
BUNDLING=off
DEFROUTE=yes
SECURE=off
PERSIST=off
PROVIDER=sample_ISP
ARECODE=578
PREFIX=519
PHONE_OUT=801
USER=user2
PASSWORD=secret
PEERDNS=yes
BSDCOMP=off
CCP=off
AC=off
VJ=off
[root@localhost root]# cat /etc/sysconfig/network-scripts/ifcfg-ppp1
USERCTL=yes
BOOTPROTO=dialup
DEVICE=pppp1
TYPE=DSL
ONBOOT=no
PIDFILE=/var/run/pppo-adsl.pid
FIREWALL=NONE
PPOE_TIMEOUT=20
LCP_FAILURE=3
LCP_INTERVAL=20
LCAMSS=1412
CONNECT_POLL=6
CONNECT_TIMEOUT=60
DEFROUTE=yes
SYNCHRONOUS=no
PERSIST=no
ETH=eth0
PROVIDER=sample_ISP
USER=user3
PASS=secret
PEERDNS=yes
[root@localhost root]#
```

其他使用 `PPP` 守护程序的配置存储在 `/etc/ppp` 目录中。检查在连接到互联网服务提供商时使用的密码错误是 `PPP` 连接最常见的问题。这些密码存储在两个文件中：`/etc/ppp/pap-secrets`（密码协议）和 `/etc/ppp/chap-secrets`（握手协议）。如果互联网服务提供商接受更安全的方法，则将使用 `/etc/ppp/chap-secrets` 文件；然而，之前的 Internet 配置向会在会在输出所示的两个文件中都添加密码：

```
[root@localhost ~] cat /etc/ppp/pap-secrets
# Secrets for PAP
client server addresses
user3 * "secret"
user2 * "secret"
user1 * "secret"
redhat-config-network will overwrite this part
```

```
[root@localhost ~] cat /etc/ppp/chap-secrets
# Secrets for CHAP
client server addresses
user3 * "secret"
user2 * "secret"
user1 * "secret"
redhat-config-network will overwrite this part
```

配置好设备后，必须通过连接（或拨号）图 15-15 所示的 Red Hat 拨号器来激活它。启动 Red Hat 拨号器，您可以在 `GNOME` 桌面环境中导航到 `GNOME` 按钮、程序、Internet、拨号器，或者在 `KDE` 桌面环境中导航到 `K` 按钮、Internet、拨号器。

![](img/6148a12ef656b46c092b21c2e023d928_723_0.png)

图 15-15 激活 `PPP` 连接

激活后，`ifconfig` 命令将显示上述示例中使用的 `ppp0`、`isdn0` 和 `ppp1` 等接口名称，以及从互联网服务提供商获得的 `IP` 地址。以下输出显示了 `ppp` 接口激活时 `ifconfig` 命令的输出：

```
[localhost root]# ifconfig
eth0 link:Ethernet Hwaddr 00:80:D6:74:43
inet addr:3.0.0.88 Bcast:255.255.255 Mask:255.0.0
UP BROADCAST RUNNING MTU:1500 Metric:1
RX packets:23068 errors:0 dropped:0 overflows:0 frame:0
TX packets:29730 errors:0 dropped:0 overflows:0 carrier:0
RX bytes:1908993 (1.8 Mb) TX bytes:32792075 (31.2 Mb)
```

```
lo link:Local Loopback
inet addr:127.0.0.1 Mask:255.255.0.0
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:508 errors:0 dropped:0 overflows:0 frame:0
TX packets:508 errors:0 dropped:0 overflows:0 carrier:0
RX bytes:34319 (33.5 Kb) TX bytes:34319 (33.5 Kb)
```

```
ppp0 link:Point-to-Point Protocol
inet addr:65.95.13.63 P-T:65.95.13.11 Mask:255.255.255.255
UP POINTPOINT RUNNING NOARP MULTICAST MTU:1492 Metric:1
RX packets:5 errors:0 dropped:0 overflows:0 frame:0
TX packets:3 errors:0 dropped:0 overflows:0 carrier:0
RX bytes:110 (110.0 b) TX bytes:54 (54.0 b)
```

```
[localhost root]#
```

还有许多其他工具可供您配置和激活 `PPP` 接口，例如上一节介绍的 `Linuxconf`。这些工具中的大多数执行相同的任务，但方式不同。用于配置和拨号调制解器连接常用的工具之一是图 15-16 所示的 `KDE PPP Manager`，可以在登录桌面环境后在终端提示符输入 `kpppp` 来启动。

## 名称解析

在 `TCP/IP` 网络上通信的计算机使用唯一的 `IP` 地址标识身份；然而，这种识别方案对于人类来说是不实用的，因为很难记住 `IP` 地址。因此，我们通过名称识别计算机；由于网络上的每台计算机通常称为主机（`host`），计算机名称称为主机名（`hostname`）。

对于参与互联网的计算机很少使用简单的主机名；相反，您可以根据域名空间（`DNS`）的分层命名方案为计算机提供称为完全限定域名（`FQDN`）的主机名。域名空间由一个虚拟根和若干个顶级域名组成，顶级域名标识运行您计算机的网络的组织类型。每个顶级域名下存在多个二级域名，用于识别组织名称，如图 15-17 所示，简单的主机名列在二级域名之下。

你可以使用 `hostname` 命令来查看或设置 `Linux` 计算机的主机名，输出如下：

```
[root@localhost root]# hostname
localhost.localdomain
[root@localhost]# hostname computer1.sampleddomain
[root@localhost]# hostname
computer1.sampleddomain.com
[root@localhost]# -
```

为了在每次启动时都配置上述输出中的主机名，只需修改 `/etc/sysconfig/network` 文件中的 `HOSTNAME` 行即可，如下所示：
