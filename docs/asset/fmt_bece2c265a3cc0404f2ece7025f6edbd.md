
`imap:tcp`

这允许来自你的网络通过 TCP 协议对 IMAP 服务（端口 143）的请求。你也可以通过逗号分隔多个端口来添加它们。例如：

`53, 110`

这将允许计算机成为域名系统服务器或使用 POP3 提供信箱服务。

> 注意：仅当你的计算机是邮件服务器时才打开 IMAP 和 POP3 端口。如果你在计算机上下载和读取邮件，可以在不打开这些端口的情况下从 IMAP 或 POP3 服务器免费获取邮件。

- **选择设备 (Select devices)**——Red Hat Linux 在 Core 3 之前的另一个功能是选择设备框，它显示了与计算机上网卡关联的接口。对于以太网设备，你会看到 `eth0`、`eth1`，如果你想接受来自这些接口之一的所有请求，请勾选旁边的复选框。例如，如果你计划拨号 (`ppp0`) 获取互联网，但计划与局域网 (`eth0`) 上的人员连接共享你的互联网连接，你可以点击 `eth0`。

> 注意：一旦安装了 Fedora 或 RHEL，运行 `system-config-level` 命令来打开安全级别配置窗口。该窗口提供了一种选择可信网络设备并将可访问端口（通过名称或数字）添加到你的 `iptables` 防火墙的方法。

在你安装并重启 Red Hat Linux 发行版后，将启动该防火墙。当你的系统运行时，检查 `/etc/sysconfig/iptables` 文件以查看你通过防火墙配置窗口的选择创建的防火墙规则。这些规则由 `/etc/init.d/iptables` 脚本加载到内核（该脚本设置为启动 Red Hat 时自动运行）。使用“带有 iptables 的防火墙”部分详细了解如何手动操作你的防火墙。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_457_0.png)

我喜欢检查一些服务以使用防火墙配置所创建的规则。稍后，如果我想在计算机上添加其他服务，只需复制允许服务的某行，然后将服务名称或数字更改为我想要的。服务号和名称包含在 `/etc/services` 文件中。常见的服务可能想要使用并是 Windows 文件和打印机共享（在 Linux 中使用 Samba）。要与 Samba 共享文件，你可能需要在防火墙中打开端口 137、138 和 139。（将 Samba 端口开放给本地可信网络，绝不要开放给互联网。）

# 在 Mandrakelinux 中创建防火墙

Mandrakelinux 提供了一种在 Mandrakelinux 安装后配置防火墙的方法：

- 1. 从主菜单选择系统配置 (System Configuration) -> 配置你的计算机。提示你输入 root 密码。
- 2. 输入 root 密码并点击 OK。出现 Mandrake 控制中心。
- 3. 选择安全 (Security) -> 窗口中防火墙服务。
- 4. 选择你希望在桌面系统中提供的特定服务并点击 OK。
- 5. 点击网络设备 (Net Device) 面旁边的向下箭头，选择连接到互联网的接口。对于拨号连接，选择 `ppp0`。对于有线连接，选择 `eth0`、`eth1` 或类似的。点击 OK。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_457_1.png)

# 设置某些规则

学习以下步骤将帮助你理解防火墙规则的语法，以及你可以通过这些规则设置的信息类型。此过程设计用于在你所控制的计算机上从头到尾运行。在设置防火墙规则的过程中，你将临时切断与该机器的所有通信，因此请勿在保持网络连接的机器上尝试此操作。

此示例说明了在一台计算机上有两个以太网接口（这是专用防火墙的典型配置）的情况。定义为 `eth0` 的接口连接到互联网，定义为 `eth1` 的接口连接到防火墙所保护的计算机私有网络。推测，这些私有计算机只是一堆通过防火墙浏览互联网的台式计算机。

`iptables` 允许你设置表规则，以处理进入计算机的互联网协议 (IP) 数据包。如果在 `iptables` 命令中没有指定，过滤表（filtering table）就是你默认使用的表（`-t filter`）。你还可以配置的其他表包括 NAT (`-t nat`) 和 mangle (`-t mangle`)。NAT 和 mangle 表的特殊用途将在后文中解释。本示例使用的是过滤表。

进入和离开防火墙的数据包处理规则定义在“链”（chains）的范围内。过滤表可用的链包括 `INPUT`（防火墙接收的数据包）、`FORWARD`（通过防火墙路由的数据包）和 `OUTPUT`（在本地防火墙本身创建的数据包）。过滤是根据你设置的规则集在这些链上进行的。

当数据包到达防火墙时，它将顺序通过链中的规则，直到找到匹配的规则。例如，匹配可能取决于数据包的来源或去向。一旦匹配成功，链将跳转到该规则的动作（也称为目标，target），该动作可能定义数据包应该被接受或丢弃，或者对其执行某些其他操作。

> 设置防火墙是一件严肃的事情。配置不当的防火墙可能会拒绝合法请求、将数据包转发到错误位置，或使你的计算机在网络中完全无法访问。如果你在你赖的安全且可从网络访问的计算机上尝试以下步骤，请务必小心。

- 1. 从终端（Terminal）窗口，变为 root 用户：

```
$ su -
Password: ***********
```

- 2. 输入以下命令查看系统上设置了哪些防火墙规则：

```
# iptables -L
Chain INPUT (ACCEPT)
  target prot opt source destination
Chain FORWARD (ACCEPT)
  target prot opt source destination
Chain OUTPUT (ACCEPT)
  target prot opt source destination
```

示例输出显示你的 Linux 系统目前没有设置任何过滤规则，这意味着所有数据包都是接受的（策略为 ACCEPT）。如果你选择了一组复杂的防火墙规则，可能考虑使用不同的方法来尝试。

- 3. 这三条命令更改了你的计算机过滤数据包的行为方式：

```
# iptables -p INPUT DROP
# iptables -p INPUT DROP
# iptables -p FORWARD DROP
```

在此示例中，默认行为被更改，使得所有流出网络接口（`OUTPUT`）或请求通过这些接口（`FORWARD`）的数据包都会被丢弃。此时，数据包应该能够从任何网络接口进入。你可以运行 `iptables -L` 查看所有策略都已从 `ACCEPT` 更改为 `DROP`。如果你不想这样做，可以再次运行命令，将 `DROP` 改为 `ACCEPT`，以便让你的防火墙完全开放。同样，重启将使你回到原始状态。

在以下示例中，接受来自互联网的 ICMP 请求数据包是 ICMP 类型 8 和 11。类型 8 允许你的计算机接受回显消息（echo messages），使人们能够 ping 你的计算机以检查是否可用。类型 11 与传输过程中存活时间（TTL）的的数据包有关，你正在接受返回给你的类型超时（Time exceeded）消息。你需要接受类型 11 消息以便使用 `traceroute` 命令链接到你可以到达的主机。

```
# iptables -A INPUT -p ICMP -i eth0 -s 0/0 --icmp 8
# iptables -A INPUT -p ICMP -i eth0 -s 0/0 --icmp 11
```

这两行定义了通过第一个以太网接口（`eth0`）从任何源（`-s 0/0`）进入计算机的 ICMP 数据包规则。第一行表示类型 8 服务，第二行表示类型 11 服务![](img/23f52a815d30c05fbbf68ff8ce6d21ac_460_0.png)

- 5. 以下命令示例定义了允许从本地计算机或其保护的私有网络进入和离开计算机的数据包：

```
# iptables -A INPUT -p ALL -i lo -s 127.0.0.1 -j ACCEPT
# iptables -A INPUT -p ALL -i lo -s 10.0.0.1 -j ACCEPT
# iptables -A INPUT -p ALL -i lo -s 323.45.67.89 -j ACCEPT
# iptables -A INPUT -p ALL -i eth0 -s 10.0.0.0/24 -j ACCEPT
# iptables -A INPUT -p ALL -i eth0 -d 10.0.0.255 -j ACCEPT
```
