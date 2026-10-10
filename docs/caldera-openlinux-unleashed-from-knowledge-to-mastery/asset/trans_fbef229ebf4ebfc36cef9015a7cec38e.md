
## 背景资料

我们已经见过 lo 和 eth 接口。tr 接口用于令牌环网络，sl 用于 SLIP 接口（一种在串行链路上运行 IP 的较旧协议），而 ppp 是点对点协议接口（在第 13 章中讨论）。

## 接口配置

每个接口都有一个名为 `/etc/sysconfig/network-scripts/ifcfg-ifname` 的配置脚本。例如，eth0 接口的配置脚本为 `/etc/sysconfig/network-scripts/ifcfg-eth0`。该脚本大致如下所示：

```bash
#!/bin/sh

# Device type: ethernet
# Variable declarations:
DEVICE=eth0
IPADDR=192.168.2.3
NETMASK=255.255.255.0
NETWORK=192.168.2.0
BROADCAST=192.168.2.255
GATEWAY=192.168.2.1
ONBOOT=yes
DYNAMIC=...
# End variable declarations
REMIP=0.0.0.0
MTU=1500
```

这些变量具有以下含义：

-   DEVICE 是接口名称。
-   IPADDR 是接口的 IP 地址。
-   NETMASK 是接口的网络掩码。
-   NETWORK 是接口的网络地址。
-   BROADCAST 是接口的广播地址。
-   GATEWAY 是网关主机的 IP 地址。如果网络中没有网关，则将此变量设置为 none。网关的存在会导致网络脚本使用网关设置一条默认路由。
-   ONBOOT 的值为 yes 或 no。如果为 yes，则接口在计算机启动时自动激活。这对于以太网接口是合适的，但对于调制解调器线路可能并不合适。
-   DYNAMIC 为空或者是动态地址分配协议（如 dhcp 或 bootp）。如果 DYNAMIC 非空，系统将动态配置 IP 地址、网络掩码等。（动态地址分配在“DHCP”一节中有介绍。）
-   REMIP 指定远程 IP 地址。这对于点对点链路非常有用；对于以太网接口而言则无意义。
-   MTU 指定最大传输单元。以太网接口的 MTU 无法更改，但串行链路的 MTU 可以调整。

## 启动和停止网络

在启动时，Shell 脚本 `/etc/rc.d/init.d/network` 会以参数 `start` 执行。该脚本执行以下操作：

-   根据 `/etc/sysconfig/network` 中的设置启用或禁用 IP 转发。IP 转发允许你将 Linux 机器用作路由器。要启用它，请将行 `IPFORWARDING=yes` 放入 `/etc/sysconfig/network`。
-   初始化环回接口 lo。
-   对于 IF_LIST（来自 `/etc/sysconfig/network`）中的每种类型的每个接口，运行另一个名为 `/sbin/ifup` 的 Shell 脚本。该脚本从 `/etc/sysconfig/network-scripts` 读取相应的 `ifcfg-interface` 文件，并实际执行 ifconfig 和 route 命令来激活接口。
-   如果 Shell 脚本 `/etc/sysconfig/network-scripts/ifcfg-routes` 存在，则执行它。你可以在此脚本中放入 route 命令，以设置所需的任何特殊路由。

要停止网络（例如，在系统关闭时），你调用 `/etc/rc.d/init.d/network` 脚本并传入参数 `stop`，这将导致接口被关闭。

尽管这些 Shell 脚本内部相当复杂，但使用起来非常简单。不幸的是，它们的文档并不完善。你应该阅读这些脚本以了解其工作原理。

## 添加接口

添加额外的接口非常简单。只需创建相应的 `/etc/sysconfig/network-scripts/ifcfg-interface` 脚本即可。你可以使用文本编辑器或图形化的 Caldera Open Administration System 面板来创建此脚本。要通过 COAS 添加接口，请从 COAS 菜单中选择 Network-Ethernet Interfaces。随后会弹出图 11.3 所示的窗口。

![](img/df365d352a104b50fea29e59a052de4d_323_0.png)

在此窗口中，只需填写相关字段以创建配置脚本。这些字段包括：

-   **网络设备**：网络设备名称。
-   **PNP 配置**：这与即插即用硬件无关。相反，它表示一种集中式 IP 地址分配协议，如 DHCP。
-   **接口地址、网络掩码和广播地址**：接口的 IP 地址、网络掩码和广播地址。
-   **默认路由**：如果启用此选项，接口将使用该接口设置一条默认路由。
-   **默认网关**：如果你正在使用该接口作为默认路由，此字段包含网关的 IP 地址。
-   **启动时初始化**：如果启用此选项，接口及其路由将在启动时初始化。这对于以太网接口通常来说是合适的。

## 背景资料

**New Alias** 按钮允许你创建接口别名。别名允许你将单个物理接口划分为多个逻辑接口，每个接口都有自己独立的 IP 地址。这种安排在虚拟 Web 主机中非常有用，例如，你希望让一台机器看起来像是许多不同的机器。别名在线 WWW-HOWTO 中有详细的描述。

## 名称服务

总是使用 IP 地址来代表主机和网络地址是非常麻烦的。Linux 支持多种名称服务，用于在名称和数字之间进行映射，反之亦然。

文件 `/etc/nsswitch.conf` 控制使用哪些名称服务及其顺序。在本节中，我们关注的行大致如下所示：

```
hosts:      files nis dns
networks:    nis files dns
```

第一行意味着在查找主机名或地址时，系统首先咨询 **files** 服务。如果失败，系统会尝试 **nis** 服务，最后尝试 **dns** 服务。这些服务是什么意思？

-   **files** **files** 服务会导致在简单文本文件中查找。具体使用哪个文件取决于正在查找的内容。对于主机到地址的映射，系统会咨询 `/etc/hosts` 文件。这是一个纯文本文件。空行和以 `#` 开头的行会被忽略；其他行由一个 IP 地址后跟主机的“规范”名称，再后跟主机的“昵称”组成。例如，以下是 shishi 的 `/etc/hosts` 文件内容：
    ```
    192.168.2.1  shevy, shevy.sk011.ca shevy
    192.168.2.2  scruffy, scruffy.sk011.ca scruffy
    192.168.2.3  shishi, shishi.sk011.ca shishi
    ```
    每个地址后面跟着完全限定主机名和短名称。

### 背景资料

`/etc/hosts` 中的注释建议你最好不要编辑它。但认真的 Linux 用户还是会去编辑它。

-   **nis** **nis** 服务是由 Sun Microsystems 设计的一种数据库查询系统。它允许你存储许多查询文件（如 `/etc/hosts`）的集中式版本，并让客户端在服务器上进行查询。
    NIS（网络信息服务）旨在用于小型网络。它不适用于整个互联网的查询。NIS 在第 14 章中有介绍。
-   **dns** **dns** 服务指的是域名系统，即整个互联网上的分布式主机名到地址映射数据库。第 12 章详细介绍了 DNS。

## 解析器配置

用于查找主机地址的一组函数驻留在解析器库中。它执行文件查找、NIS 查找和 DNS 查找。解析器库的 DNS 查找部分由文件 `/etc/resolv.conf` 控制。该文件大致如下所示：

```
domain skoll.ca
nameserver 192.168.2.1
nameserver 192.168.2.22
nameserver 192.168.2.33
```

domain 行指定本地 DNS 域。如果 DNS 查找失败，未限定的主机名将附加此域。

nameserver 行指定名称服务器的 IP 地址。这些是专门配置为响应 DNS 请求的主机。第一行是主名称服务器，通常也是唯一使用的服务器。如果主名称服务器宕机，则依次尝试备用名称服务器。

nsswitch.conf 文件在 info 中有文档记录；输入 `info "(libc6)NSS Configuration File"` 即可查看相关文档。

## 有用的诊断程序

Linux 包含两个有用的诊断程序（ping 和 traceroute），它们可以让你判断计算机是否成功联网以及路由是否正确设置。

## ping

ping 程序测试从一台主机到另一台主机的连接性。

> ping 的名字来源于声呐回声定位器，它通过声音脉冲对物体进行“ping”。

要 ping 一台主机，请使用：

```
$ ping host
```

host 可以是 IP 地址或主机名。（如果你的名称服务未正常工作，你可能需要提供 IP 地址。）
