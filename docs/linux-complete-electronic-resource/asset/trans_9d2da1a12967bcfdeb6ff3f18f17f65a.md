
只有所在用户属于该组的用户才能执行它。上述示例仅允许用户 **radio** 和 **fred** 执行 *sliplogin*。

要将二进制文件安装到你的 `/sbin` 目录并将 *man* 手册页安装到第 8 节，请执行以下操作：

```
# cd /usr/src
# gzip -dc ../sliplogin-2.1.1.tar.gz | tar xvf -
# cd sliplogin-2.1.1
# <.edit the Makefile if you don't use shadow passwords..>
# make install
```

如果你想在安装前重新编译二进制文件，请在 **make install** 之前添加一个 **make clean**。如果你想在其他位置安装二进制文件，你需要编辑 *Makefile install* 规则。

请阅读随包提供的 *README* 文件以获取更多信息。

## 为 SLIP 主机配置 /etc/passwd

通常，你会在 `/etc/passwd` 文件中为 SLIP 调用者创建一些特殊的登录账户。一个常见的约定是使用调用主机的主机名，并在前面加上大写字母 “S” 作为前缀。例如，如果调用主机名为 **radio**，那么你可以创建一个如下所示的 `/etc/passwd` 条目：

```
Sradi o: Fvkurok73:1427:1:radio SLIP login:/sbin/sliplogin
```

账户名称具体叫什么并不重要，只要对你有意义即可。

注意：调用者不需要任何特殊的家目录，因为他们不会从这台机器获得 shell。因此 **/tmp** 是一个不错的选择。另外请注意，*sliplogin* 被用来替代正常的登录 shell。

## 配置 /etc/slip.hosts

`/etc/slip.hosts` 文件是 *sliplogin* 搜索与登录名匹配的条目以获取该调用者配置详情的文件。在这个文件中，你指定将分配给调用者并供其使用的 IP 地址和子网掩码。对于两个主机的示例条目，一个是主机 **radio** 的静态配置，另一个是用户主机 **albert** 的动态配置，可能如下所示：

```
#
Sradi o 44.136.8.99 44.136.8.100 255.255.255.0 normal -1
Salbert 44.136.8.99 DYNAMIC 255.255.255.0 compressed 60
#
```

`/etc/slip.hosts` 文件的条目包括：

1.  调用者的登录名。
2.  服务器机器（即本机）的 IP 地址。
3.  分配给调用者的 IP 地址。如果此字段编码为 `DYNAMIC`，则将根据稍后讨论的 `/etc/slip.tty` 文件中包含的信息分配一个 IP 地址。*注意*：要使此功能正常工作，你必须使用至少 1.3 版本的 sliplogin。
4.  分配给调用机器的子网掩码，以点分十进制表示，例如 C 类网络掩码为 255.255.255.0。
5.  SLIP 模式设置，允许你启用/禁用压缩和其他 SLIP 功能。这里允许的值是 `"normal"` 或 `"compressed."`。
6.  一个超时参数，指定在自动断开线路之前，线路可以保持空闲（未接收到数据报）的最长时间。负值将禁用此功能。
7.  可选参数。

注意：字段 2 和 3 可以使用主机名或点分十进制表示的 IP 地址。如果使用主机名，则这些主机必须是可解析的。也就是说，你的机器必须能够为这些主机名找到 IP 地址；否则脚本在调用时会失败。你可以通过尝试 telnet 到该主机名来测试这一点。如果你看到 “*Trying nnn.nnn.nnn.nnn...* ” 消息，说明你的机器已经能够为该名称找到 IP 地址。如果你看到 “*Unknown host,* ” 消息，则说明找不到。如果找不到，要么使用点分十进制表示的 IP 地址，要么修复你的名称解析器配置（参见“名称解析”部分）。

最常见的 SLIP 模式有：

-   **normal** 以启用正常的非压缩 SLIP。
-   **compressed** 以启用 van Jacobson 头部压缩 (cSLIP)。

自然地，这些模式是互斥的；你可以使用其中一个或另一个。有关其他可用选项的更多信息，请参阅 *man* 手册页。

### 配置 /etc/slip.login 文件

当 *sliplogin* 搜索 /etc/slip.hosts 并找到匹配的条目后，它将尝试执行 /etc/slip.login 文件，以使用其 IP 地址和子网掩码实际配置 SLIP 接口。*sliplogin* 包中提供的示例 /etc/slip.login 文件如下所示：

```
#!/bin/sh -
# 
#      @(#)/slip.login 5.1 (Berkeley) 7/1/90
#
#  generic login file for a SLIP line. sliplogin invokes this
#  with the parameters:
#   $1   $2   $3 $4, $5, $6 ...
#  SLIPunit tyspeed  pid  the arguments from the slip.host
#  entry
#
/sbin/ifconfig $1 $5 pointopoint $6 mtu 1500 -trailers up
/sbin/route add $6
arp -s $6 <hw_addr> pub
exit 0
#
```

你会注意到，此脚本简单地使用 *ifconfig* 和 *route* 命令使用其 IP 地址、远程 IP 地址和子网掩码配置 SLIP 设备，并通过 SLIP 设备为远程地址创建路由。这与你使用 *slattach* 命令时的做法完全一样。

还请注意使用 *Proxy ARP* 以确保与服务器机器在同一以太网上的其他主机知道如何到达拨入主机。<hw_addr> 字段应该是机器中以太网卡（Ethernet card）的硬件地址。如果你的服务器机器不在以太网网络上，那么你可以完全省略这一行。

### 配置 /etc/slip.logout 文件

当通话结束时，你希望确保串行设备恢复到其正常状态，以便未来的调用者能够正确登录。这是通过 /etc/slip.logout 文件来实现的。其格式相当简单，并像 /etc/slip.login 文件一样使用相同的参数调用。

```
#!/bin/sh -
#
#       slip.logout
#
/sbin/ifconfig $1 down
arp -d $6
exit 0
#
```

它所做的只是将接口“down”（关闭），这将删除之前创建的手动路由。它还使用 arp 命令删除放置的任何代理 arp。同样，如果你的服务器机器没有以太网端口，则脚本中不需要 arp 命令。

### 配置 /etc/slip.tty 文件

如果你正在使用动态 IP 地址分配（即，/etc/slip.hosts 文件中有任何主机配置了 DYNAMIC 关键字），那么你必须配置 /etc/slip.tty 文件以列出哪些地址分配给哪个端口。只有当你希望服务器动态地向用户分配地址时才需要此文件。

该文件是一个表格，列出了将支持拨入 SLIP 连接的 tty 设备以及应分配给在该端口拨入的用户的 IP 地址。其格式如下：

```
# slip.tty _ tty -> IP address mappings for dynamic SLIP
# format: /dev/tty?? xxx.xxx.xxx.xxx
/
/dev/tty50  192.168.0.100
/dev/tty51  192.168.0.101
#
```

此表格表示，在端口 /dev/tty50 拨入且 /etc/slip.hosts 文件中的远程地址字段设置为 DYNAMIC 的调用者将被分配地址 192.168.0.100。

通过这种方式，对于不需要专用地址的所有用户，你只需要为每个端口分配一个地址。这有助于你将所需的地址数量保持在最低限度，以避免浪费。

## 使用 dip 的 SLIP 服务器

让我首先说明，下面的一些信息来自 dip 手册页，其中简要记录了如何运行 Linux 作为 SLIP 服务器。此外请注意，以下内容基于 dip337o-uri.tgz 包，可能不适用于 dip 的其他版本。dip 有一种输入操作模式，它会自动找到调用该命令的用户的条目，并根据在 /etc/diphosts 文件中找到的信息将串行线路配置为 SLIP 链接。这种输入操作模式是通过将 dip 作为 diplogin 调用来激活的。因此，通过使用 diplogin 作为登录 shell 创建特殊账户，就可以使用 dip 作为 SLIP 服务器。你需要做的第一件事是创建如下所示的符号链接：

```
# ln -sf /usr/sbin/dip /usr/sbin/diplogin
```

