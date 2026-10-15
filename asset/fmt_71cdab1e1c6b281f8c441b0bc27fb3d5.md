
```
eth1 Link encap:Ethernet HWaddr 00:AO:CC:25:8A:EC

inet addr:192.168.1.1 Bcast:192.168.1.255

Mask:255.255.255.0

UP BROADCAST RUNNING PROMIS MULTICAST MTU:1500

Metric:1

RX packets:4648466 errors:0 dropped:0 overflows:0

frame:0

TX packets:679303 errors:0 dropped:0 overflows:0

carrier:0

collisions:33062 txqueuelen:100

Interrupt:11 Base address:0x6000
```

Copyright©2000 SYBEX, Inc., Alameda, CA www.syex.com

## 第 23 章 • 理解辅助网络服务

注意 `BROADCAST` 和 `MULTICAST` 关键词，它们将出现在输出的第三行。如果不存在这些关键词，DHCP 将无法正常工作。要解决此问题，可能需要执行以下任或全部操作：

- 使用 `ifconfig` 命令重新配置接口。
- 用支持 `MULTICAST` 的网卡替换网络接口。

### 配置 DHCP

DHCP 配置文件为 `/etc/dhcpd`。以下是一个典型的配置，包含了动态和静态信息：

```bash
default-lease-time 64800;

max-lease-time 64800;

option subnet-mask 255.255.255.0;

option broadcast-address 192.168.1.255;

option routers 192.168.1.1;

option domain-name-servers 192.168.1.1;

option domain-name "azusapacific.com";
```

```bash
subnet 192.168.1.0 netmask 255.255.255.0 {
  server-identifier 192.168.1.1;
  host sara {
    hardware ethernet 00:50:04:d2:d3:15;
    fixed-address 192.168.1.33;
    default-lease-time 64800;
  }
}
```

主机身份和位置的结合决定了分配的配置。

租约分配给有限的时间，在 `/etc/dhcpd` 中指定，客户端必须对其进行续约。在启动 DHCP 服务器之前，你必须创建 `/var/lib/dhcp/leases` 文件。

```bash
subnet 192.168.1.0 netmask 255.255.255.0 {
  server-identifier 192.168.1.1;
  host sara {
    hardware ethernet 00:50:04:d2:d3:15;
    fixed-address 192.168.1.33;
    default-lease-time 64800;
  }
  range 192.168.1.20 192.168.1.100;
}
```

与主机关联的 IP 地址每次主机启动时都可能不同。DHCP 配置可以是动态的也是静态的，为指定的主机提供静态配置，为其他主机提供动态配置。

# 图 23.1 linuxconf 主机基础配置界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_583_0.png)

你可以通过执行命令来检查泵的状态：

```bash
/bin/pump -s
```

要强制立即刷新租约，请执行命令：

```bash
/bin/pump -i eth0 -R
```

# 关于 DHCP 和 pump 的更多信息

关于 DHCP 的更多信息，请参考：

- www.isc.org 的 DHCP 网页
- Vladimir Vuksan 编写的 DHCP mini-HOWTO，位于 `/usr/doc/dhcp-*`
- `/usr/doc/dhcp-*` 下的 DHCP 文档

关于 `pump` 的更多信息，请参阅其页面。

# IPX 协议

Red Linux 包含了 `mars-nwe` 软件包。该包为基于 IPX 协议的 Novell 网络提供了文件和打印机共享功能。相关的 `iputils` 软件包包含了有用的 IPX 工具程序。如果你正在使用基于 IPX 的网络，应该安装这两个软件包。

`marsnwe` 允许你使用 `mount` 命令或通过指定文件类型为 `ncp` 的 `mount` 命令来挂载 IPX 文件系统。你也可以在 `/etc/fstab` 文件中指定 IPX 文件系统。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_584_0.png)

`mount` 命令报告的文件系统类型为 `ncpfs`；但你可以将 `ncp` 或 `ncpfs` 作为 `mount` 命令以及 `/etc/fstab` 文件的参数指定。

关于在 Linux 下使用 IPX 的更多信息，请参阅 `/usr/doc/mars-nwe-*` 下的 `mars-nwe` 文档以及 `/usr/doc/iputils-*` 下的 `iputils` 文档。还有以下 man pages：

- `ipx_cmd`
- `ipx_config`
- `ipx_interface`
- `ipx_internal_net`
- `ipx_route`
- `ncopy`
- `ncpmount`
- `ncpumount`
- `nprint`
- `nsend`
- `nwauth`
- `nwbocreate`
- `nwbols`
- `nwboprops`
- `nwborm`
- `nwbpadd`
- `nwbcreate`
- `nwbprm`
- `nwbpset`
- `nwbvalues`
- `nwclient`
- `nwdir`
- `nwfsctrl`
- `nwfsinfo`
- `nwfstime`
- `nwgrant`
- `nwmsg`
- `nwpasswd`
- `nwpurge`
- `nwrevoke`
- `nwrights`
- `nwsfind`
- `nwtrustee`
- `nwuserlist`
- `nwvolinfo`
- `pqlist`
- `pqrm`
- `pqstat`
- `pserver`
- `slist`

Copyright ©2000 SYBEX, Inc., Alameda, CA www.sybex.com

# 通过 lpd 远程访问打印机

你可以轻松地访问 Red Hat 打印机。当然，你必须首先配置服务器和客户端系统。要配置服务器系统，请在 `/etc/hosts.lpd` 中列出客户端主机。如果客户端主机与服务器处于相同的管理控制下，你也可以选择将其列在 `/etc/hosts.equiv` 中。此外，确保客户端主机的名称可以通过 IP 地址解析；如有必要，向 `/etc/hosts` 中添加一行。

要配置客户端，请在客户端的 `/etc/printcap` 文件中添加如下格式的条目：

```text
remlp:
:lpr=host:rp=printer:sd=dir
```

在此条目中，`host` 是服务器的名称，`printer` 是服务器 `/etc/printcap` 文件中列出的目标打印机名称，`dir` 是在客户端上使用的溢打印目录。溢打印目录通常是 `/var/spool` 的子目录。

一旦配置好服务器，你应该能够通过客户端主机上执行命令来访问服务器的打印机。例如，你可以使用 `lpr` 命令打印文件，并使用 `lpq` 命令检查打印队列。

# 网络新闻

`inn` 软件包提供了 `inn` 以及其他支持网络新闻传输协议（NNTP）和互联网新闻的程序。互联网新闻在互联网新闻组中传输和接收帖子，在 Web 出现之前，这是多用户间交互的主流方法。如今，Web 论坛提供了一种更简单的多用户间交互方式。然而，尽管互联网新闻的使用非常复杂且需要大量资源，但它仍然是一项流行的服务。你可以使用 `inn` 支持本地新闻组或提供对互联网新闻组的访问。为了充分支持互联网新闻组，主机系统必须拥有数 GB 的空闲磁盘空间和高速互联网连接。

与电子邮件一样，互联网新闻已成为传输垃圾信息的手段。为了抑制垃圾新闻文章，你可以安装 `cleanfeed` 软件包。

# 时间同步

Red Hat Linux 提供了两种同步时间：

- `rdate`，与另一个主机同步
- `xntp`，与协调时间（UTC）同步

包含 `rdate` 软件包的 `rdate` 程序是较旧且不复杂的方法。要与另一端同步，请执行如下格式的命令：

```bash
rdate -s host
```
