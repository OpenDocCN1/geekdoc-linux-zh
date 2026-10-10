
该命令还有几种其他选项可用，但它们使用得较少。与 /sbin/route 命令一样，man 手册页可以提供关于所有选项和参数的详细信息。

## 网络配置文件

正如前文所述，可以修改七个网络配置文件以更改系统的基本网络交互。这些文件如下：

- /etc/hosts—地址、主机名和别名的列表
- /etc/services—网络服务和端口连接
- /etc/nsswitch.conf—Linux 网络信息服务配置
- /etc/resolv.conf—域名服务域（搜索）设置
- /etc/host.conf—网络信息搜索顺序（默认为先 /etc/hosts，后 DNS）
- /etc/sysconfig/network—主机名、IP 地址、启动激活控制以及网关设置（附带可选的 IPv6 设置）
- /etc/sysconfig/network-scripts/ifcfg-eth0—eth0 网络设备设置；有关可选设置的详细信息，请参阅 /usr/share/doc/init-scripts/ 目录下的 sysconfig.txt 文件

修改上述前六个文件后，更改即生效。与大多数配置文件一样，可以在注释前加上井号（#）来添加注释。最后一个文件（/etc/sysconfig/network）要求重启网络守护进程后才能使用该文件。这七个文件都有相应的 man 手册页提供更多详细信息。

## 向 /etc/hosts 添加主机

/etc/hosts 文件是 IP 到主机名的映射。如果你没有使用 DNS 或其他命名服务，并且连接到大型网络，这个文件可能会变得相当大，管理起来也可能是一个真正的难题。一个小型的 /etc/hosts 文件可能如下所示：

```
127.0.0.1 localhost.localdomain localhost
128.112.50.69 myhost.mydomain.com myhost
128.112.50.169 yourhost.mydomain.com yourhost
```

第一条条目是环回条目。第二条是机器名称。第三条是网络中的另一台机器。如果网络上没有使用命名服务，myhost 通过名称识别的唯一主机是 yourhost。（仍然可以使用网络上的 IP 地址。）

如果你的网络正在使用命名服务，则最后一行不需要，可以删除。然而，如果 myhost 经常连接到 yourhost，保留该条目可能是个好主意，这样 myhost 就不必每次都要咨询命名服务。这可以节省时间并减轻网络或名称服务服务器的负担。如果你需要更改主机名或 IP 地址，或者你未使用命名服务且网络中新增了主机，请编辑此文件。

## /etc/services 中的服务设置

/etc/services 文件将端口号映射到服务。前几行看起来类似于此（/etc/services 文件可能相当长，超过 500 行）：

```
# Each line describes one service, and is of the form:
#
# service-name port/protocol [aliases ...] [# comment]

tcpmux    1/tcp           # TCP port service multiplexer
tcpmux    1/udp           # TCP port service multiplexer
rje       5/tcp           # Remote Job Entry
rje       5/udp           # Remote Job Entry
echo      7/tcp
echo      7/udp
discard   9/tcp          sink null
discard   9/udp          sink null
systat   11/tcp          users
```

通常，每个服务有两个条目，因为大多数服务可以使用 TCP 或 UDP 进行传输。通常在 /etc/services 初始配置完成后，你就不需要修改它了。

## 更改命名服务后使用 /etc/nsswitch.conf

该文件最初由 Sun Microsystems 开发，用于指定系统中访问服务的顺序。/etc/nsswitch.conf 文件列出了许多服务，但最常修改的条目是 hosts 条目。该文件的一部分可能如下所示：

```
passwd:	files
shadow:	files
group:	files

#hosts:	db files nisplus nis dns
hosts:	files dns
```

这告知服务它们应该查阅标准 UNIX/Linux 文件进行 passwd、shadow 和 group（分别为 /etc/passwd、/etc/shadow、/etc/group）查找。对于主机查找，系统会检查 /etc/hosts，如果没有条目，则检查 DNS。被注释的 hosts 条目列出了 hosts 的可能值。只有当你的命名服务发生变化时，才需要编辑此文件。

## 使用 /etc/resolv.conf 设置名称服务器

/etc/resolv.conf 被 DNS（域名服务）使用。（DNS 在第 23 章中有详细讲解。）以下是 resolv.conf 的一个示例：

```
nameserver 192.172.3.8
nameserver 192.172.3.9
search mydomain.com
```

这会设置 DNS 使用的名称服务器以及域名的顺序。如果你使用动态主机配置协议（DHCP），此文件的内容会自动设置（参见本章稍后关于“DHCP”的部分）。

> **注意**
> 
> 如果你使用 NetworkManager 处理网络连接，请不要修改 /etc/resolv.conf，因为这会导致 NetworkManager 出现问题。相反，让 NetworkManager 自行动态处理此文件。

## 使用 /etc/host.conf 设置 DNS 搜索顺序

/etc/host.conf 文件列出了你的机器解析主机名时的搜索顺序。以下是默认的 /etc/host.conf 文件：

```
order hosts, bind
```

在此示例中，主机首先检查 /etc/hosts 文件，然后执行 DNS 查找。还有几个其他选项控制命名服务的使用方式。修改此文件的唯一原因可能是你使用 NIS 作为命名服务，或者你想要使用某个可选服务。no_nospf 选项可能是系统安全的一个好选择。它将标准 DNS 查找与反向查找（从主机到 IP 再从 IP 到主机）进行比较，如果两者不匹配则失败。缺点是，当使用代理服务时，查找通常失败，因此在使用此选项时需格外小心。

## 查看 /etc/sysconfig/network 中的主机网络设置

对 /etc/sysconfig/network 的修改只有在重启网络守护进程或重启系统后才生效。如果你使用 Fedora 的图形化网络配置工具（在下一节中描述），则不应编辑此文件。该文件可能如下所示：

```
NETWORKING=yes
HOSTNAME=myhost
GATEWAY=192.112.50.99
```
还可以使用 GATEWAYDEV 设置将特定的网络设备（如 eth0 或 eth1 等）相关联。/etc/sysconfig/network 的一个额外可选条目用于 NIS 域机器，形式如下：

```
NISDOMAIN=rebel
```
网络文件以前支持 FORWARD_IPV4 值，该值决定主机是否转发 IP 数据包（路由器通常设为“yes”）。现在，此设置保存在 /etc/sysctl.conf 中，作为 net.ipv4.ip_forward 设置，如果需要更改转发设置，可以修改此项。更多信息请参阅 sysctl.conf 的 man 手册页。

## 奠定基础：localhost 接口

在成功连接到网络甚至互联网之前，需要做的第一件事是创建 localhost 接口，有时也称为环回接口，但更常见的称呼是 lo。TCP/IP 协议（参见本章稍后的“使用 TCP/IP 进行网络通信”）使用此接口为计算机分配 IP 地址，并且对于 Fedora 建立 PPP 接口也是必需的。

## 检查环回接口是否可用

通常你不需要手动创建环回接口，因为 Fedora 在安装过程中会自动为你创建一个。要检查是否已设置，你可以在以 root 用户操作时使用 ifconfig 命令，显示类似以下内容：

```
# ifconfig
lo
Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:12 errors:0 dropped:0 overruns:0 frame:0
TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:760 (760.0 b) TX bytes:760 (760.0 b)
```
在此示例中看到的证据表明环回接口存在且处于活动状态。它显示 inet addr 是分配给 localhost 的 IP 地址，通常是 127.0.0.1，并带有广播掩码 255.255.255.0，并且该接口上的活动很少（RX = 接收，TX = 发送）。如果你的输出与上述不同，则必须在完成本节其余内容后手动配置 localhost 接口。

## 手动配置环回接口

localhost 接口的 IP 地址在一个文本配置文件中指定，Fedora 使用该文件记录各种全网 IP 地址。该文件名为 /etc/hosts，即使为空，通常也存在于系统中。Linux 内核和其他网络工具使用此文件来访问本地 IP 地址和主机名。如果你没有配置其他网络接口，你可能会发现该文件仅包含一行：

```
127.0.0.1 localhost.localdomain localhost
```

