
您可以使用 `route del <route>` 命令从路由表中删除条目。

也可以使用 `ip command` 来操作路由表。命令 `ip route add 1.0.0.0/8 via 2.0.0.1` 可用于向路由表添加与上述输出相同的路由。

路由表的内容在计算机断电时丢失；要在每次启动时都将通往远程网络的路由加载到路由表中，只需将适当的 `route` 或 `ip` 命令放入 `/etc/rc.d/rc.local` 文件中即可。

您还可以在网络内的路由器上使用路由协议，以自动化向路由表添加路由的过程。两种常见的路由协议是路由信息协议 (RIP) 和开放最短路径优先 (OSPF)。

如果您网络上的计算机无法连接到远程网络上的其他计算机，问题很可能与路由有关。用于排查路由问题的常用工具是 `traceroute` 命令；它显示当前计算机与远程计算机之间的所有路由器。要追踪从本地计算机到 IP 地址为 `3.4.5.6` 的计算机的路径，您可以使用以下命令：

```
[root@server1 root]# traceroute 3.4.5.6
traceroute to 3.4.5.6 (3.4.5.6), 30 hops max, 38 byte packets
 1 server1 (192.168.0.1) 2.048 ms 0.560 ms 0.489 ms
 2 pbn.pso.com (7.43.111.2) 2.560 ms 0.660 ms 0.429 ms
 3 tfs.nhfcid.net (3.0.0.1) 3.521 ms 0.513 ms 0.499 ms
 4 sri.lala.com (3.4.5.6) 5.028 ms 0.710 ms 0.554 ms
[root@server1 root]# 
```

#### 防火墙服务

另一个没有直接由守护进程提供的网络服务是 `netfilter/iptables`，它可以用于在您的 Linux 计算机上创建防火墙。回想一下第 1 章的内容，防火墙可用于在您的组织中阻止不需要的网络流量；因此，防火墙通常在路由器接口上启用。

`netfilter/iptables` 根据存储在计算机内存中的 `rules` 丢弃某些网络数据包。默认情况下，您可以为三种类型的链指定某些规则：

- `INPUT` 链，用于目的地为您的计算机的网络数据包
- `FORWARD` 链，用于必须通过您计算机转发的网络数据包（如果您是路由器）
- `OUTPUT` 链，用于源自您计算机的网络数据包

在 Red Hat Fedora Core 2 安装后，默认情况下，`INPUT`、`FORWARD` 或 `OUTPUT` 链不存在任何规则。要创建用于每个链的规则，您必须使用 `iptables` 命令。规则可以基于源 IP 地址、目的 IP 地址、使用的协议（`TCP`、`UDP`、`ICMP`）或数据包状态。例如，要清除内存中所有先前的规则，指定默认情况下丢弃转发的数据包，并且只有源自 `192.168.1.0` 网络的数据包才被转发，您可以使用以下命令：

```
[root@server1 root]# iptables -F
[root@server1 root]# iptables -P FORWARD DROP
[root@server1 root]# iptables -A FORWARD -s 192.168.1.0/24 -j ACCEPT
[root@server1 root]#
```

然后，您可以使用以下命令验证内存中每个链的规则列表：

```
[root@server1 root]# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source		destination

Chain INPUT (policy DROP)
target     prot opt source		destination
ACCEPT    all  --  192.168.1.0/24	anywhere

Chain INPUT (policy ACCEPT)
target     prot opt source		destination
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_602_0.png)

#### 注意

由于链和规则存储在内存中，当计算机关机时它们会丢失；为了确保它们在每次启动时都加载，只需将适当的 `iptables` 命令放入 `/etc/rc/rc.local` 文件中即可。或者，您可以向 `/etc/sysconfig/iptables` 文件中添加条目。

表 15–5 列出了 `iptables` 命令的常用选项。

![](img/09bf13b782f71165e17bb3839040c96a_602_1.png)

#### 注意

较旧的 Linux 内核使用 `ipchains` 实用程序提供防火墙服务；Red Hat Fedora Core 2 中的 Linux 内核默认不支持此实用程序。

| 选项 | 描述 |
| :--- | :--- |
| `-s address` | 指定规则的数据包源地址。 |
| `-d address` | 指定规则的数据包目的地址。 |
| `-p protocol` | 指定规则的协议类型。 |
| `-j action` | 指定规则的采取的动作。 |
| `-L chain` | 列出特定链的规则。如果未指定链，则列出所有链。 |
| `-P chain policy` | 指定特定链类型的默认策略。 |
| `-D number` | 删除由附加参数指定的链的规则。规则从编号 1 开始。 |
| `-R number` | 替换由附加参数指定的链的规则。规则从编号 1 开始。 |
| `-F chain` | 删除特定链的所有规则。如果未指定链，则删除所有链的所有规则。 |

### 安全性

在过去十年中，已有数百种新服务向 Linux 系统提供，Linux 用户的数量也增加到了数百万。此外，当今的 Linux 系统通常通过互联网等网络提供。因此，当今的 Linux 更容易受到本地和跨网络的安全漏洞和攻击。为了保护您的 Linux 计算机，您应该采取措施提高本地和网络安全性，并了解如何检测设法突破您的 Linux 系统的入侵者。

#### 保护本地计算机

最重要的安全相关实践之一是限制对物理 Linux 计算机本身的访问。如果恶意用户能够访问 Linux 计算机，该用户可以通过包含小型操作系统的软盘、USB 闪存驱动器或 CD-ROM 引导计算机，并利用它访问 Linux 计算机硬盘分区上的文件，而无需登录到安装在硬盘上的操作系统。为了防止这种情况，您应该将重要的计算机（例如 Linux 服务器）锁定在一个只有 Linux 管理员或受信任用户有钥匙访问权限的特定房间内；这个房间通常被称为 `server rack`。不幸的是，某些 Linux 计算机，例如 Linux 工作站，必须放置在公共区域。对于这些计算机，您应该从计算机中移除软盘和 CD-ROM 设备。此外，您应该确保 `BIOS` 中列出的启动顺序中的 `com`

## 安全

请确保您的计算机 `BIOS` 阻止从 USB 端口启动，并且设置系统 `BIOS` 密码，以防止其他用户更改启动顺序。

基于同样的思路，任何能够物理接触 Linux 计算机的人都可能启动该计算机并与 `LILO` 或 `GRUB` 引导加载器进行交互。这允许用户指定选项，以单用户模式启动系统，从而在不输入密码的情况下获得系统的 `root` 访问权限。为了防止这种情况，只需确保在 `LILO` 或 `GRUB` 配置文件中设置引导加载器密码，如第 9 章所述。

对于 Linux 计算机，另一个重要的安全考量是限制对图形桌面和 shell 的访问。如果您离开工作站几分钟而仍保持登录状态，其他用户可以在您离开期间使用您的计算机。因此，在离开计算机之前锁定您的桌面环境或退出命令行 shell 是一个良好的安全实践。要锁定 `GNOME` 或 `KDE` 桌面，只需导航至 Red Hat 按钮并选择“锁定屏幕”；您需要输入密码才能再次使用您的桌面。退出命令行 shell 也会终止所有后台进程，因为这些进程的父进程是您的 shell。如果您运行需要较长时间完成的后台进程，可以使用 `nohup command` 运行它们；这样可以让您退出命令行 shell 而不会终止任何后台进程。例如，要运行 `updatedb` 命令并在之后退出系统，以便您可以离开工作站，只需执行以下命令：

```bash
[root@server1 root]# nohup updatedb &
[1] 3773
nohup: appending output to 'nohup.out'
[root@server1 root]# exit

Fedora Core release 2 (Tettnang)
Kernel 2.6.5-1.358 on an i686

server1 login:
```
