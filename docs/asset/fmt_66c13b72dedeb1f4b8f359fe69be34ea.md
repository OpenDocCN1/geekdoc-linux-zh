
# 欺骗防护：拒绝内部网络上具有外部源地址的包

```bash
iptables -A INPUT -j DROP -i eth1 ! -s 192.168.0.0/24
iptables -A FORWARD -j DROP -i eth1 ! -s 192.168.0.0/24
```

# 欺骗防护：拒绝源地址为内部网络的外部包（非 eth0 上的包）

```bash
iptables -A INPUT -j DROP -i eth1 ! -s 192.168.0.0/24
iptables -A FORWARD -j DROP -i eth1 ! -s 192.168.0.0/24
```

# 欺骗防护：拒绝具有本地回环地址的外部包

接口（任何 `eth0` 或 `eth1`）上源地址为本地回环的包

```bash
iptables -A INPUT -j DROP -i eth1 ! -s 127.0.0.0/255.0.0.0
iptables -A FORWARD -j DROP -i eth1 ! -s 127.0.0.0/255.0.0.0
```

# 允许防火墙系统用户的所有入站消息

```bash
iptables -A INPUT -j ACCEPT
```

# 允许访问 Web 服务器（地址 10.0.0.2），端口为 www

```bash
iptables -A INPUT -j ACCEPT -p tcp -i eth0 --port www -s 10.0.0.2
```

# 允许从 Web 服务器到内部网络的已建立连接

```bash
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --port www -s 10.0.0.0/24 -d 192.168.0.0/24 -j ACCEPT
```

# 防止从 Web 服务器到内部网络的建立连接

```bash
iptables -A OUTPUT -m state --state NEW -o eth0 -p tcp --sport -d 192.168.0.0/24 -j DROP
```

# 允许系统向外的已建立和相关的通信

允许外部与防火墙的通信，但 ICMP 包

```bash
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -j ACCEPT
```

# 防止外部发起的连接

```bash
iptables -A INPUT -m state --state NEW -i eth0 -j DROP
iptables -A FORWARD -m state --state NEW -i eth0 -j DROP
```

# 允许本地网络通过 eth1 与防火墙进行的所有通信

```bash
iptables -A INPUT -j ACCEPT -p all -i eth1 -s 192.168.0.0/24
```

# 设置地址伪装，允许内部机器访问外部网络

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

# 接受 ICMP Ping (0 和 8) 以及目标不可达 (3) 消息

其他数据包将被 INPUT 和 FORWARD 的输出策略拒绝

```bash
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type echo-reply -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type echo-request -d 10.0.0.1
iptables -A FORWARD -j ACCEPT -p icmp -i eth0 --icmp-type destination-unreachable -d 10.0.0.1
```

# 开启 IP 转发

```bash
echo 1 >/proc/sys/net/ipv4/ip_forward
```

最初，你将使用 `flush (-)` 命令清空当前规则，然后为非用户定义的规则设置策略（默认目标）。在设置链规则期间，必须关闭 IP 转发：

```bash
echo 0 >/proc/sys/net/ipv4/ip_forward
```

## 丢弃策略 (Drop Policy)

首先，为 INPUT 和 FORWARD 内置 IP 链设置了 DROP 策略。这意味着如果一个数据包不符合任何规则中允许通过的条件，它将会被丢弃。然后，IP 欺骗攻击和任何从外部尝试发起连接的尝试（SYN 包）将被拒绝。外部连接也会被记录。这是一个非常基础的配置，可以通过添加 `iptables` 规则来轻松完善。

```bash
iptables -P INPUT DROP
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
```

## IP 欺骗 (IP Spoofing)

保护私网络免受 IP 欺骗的一种方法是拒绝来自私网络专用以太网设备上的地址。在示例中，任何在设备 `eth1`（私网络专用）上源地址不是私网络地址 `!s 192.168.0.0` 的数据包都会被拒绝。此外，还要检查是否有来自外部的将私网络指定为源地址的数据包。在本示例中，任何在任何以太网设备或针对私网络（`eth1`）上源地址为私网络的包会被拦截。相同的策略也可以应用于本地主机。

```bash
# IP 欺骗，拒绝内部网络上具有外部源地址的包：
iptables -A INPUT -j LOG --in eth1 ! -s 192.168.0.0/24
iptables -A INPUT -j DROP -i eth1 ! -s 192.168.0.0/24
iptables -A FORWARD -j DROP -i eth1 -s 192.168.0.0/24

# IP 欺骗，拒绝源地址为内部网络的外部包（非 eth0 上的包）
iptables -A INPUT -j DROP -i eth1 ! -s 192.168.0.0/24
iptables -A FORWARD -j DROP -i eth1 ! -s 192.168.0.0/24

# IP 欺骗，拒绝具有本地回环地址的外部包
# （接口（任何 eth0 或 eth1）上源地址为本地回环的包）
iptables -A INPUT -j DROP -i eth1 ! -s 127.0.0.0/255.0.0.0
iptables -A FORWARD -j DROP -i eth1 ! -s 127.0.0.0/255.0.0.0
```

## 防火墙访问 (Firewall Access)

要允许访问防火墙，你允许除 ICMP 包以外的所有包。这些包稍后处理。防火墙由设备 `eth0` 指定。首先，允许已建立和相关的连接：

```bash
# 允许外部与防火墙的通信，
# 但 ICMP 包
iptables -A INPUT -m state --state ESTABLISHED,RELATED -i eth0 -p icmp -j ACCEPT
```

```bash
DROP all 192.168.0.0/24 anywhere
DROP all 127.0.0.1 anywhere
ACCEPT all anywhere anywhere
ACCEPT tcp 10.0.0.2 anywhere
ACCEPT tcp 192.168.0.0/24 tcp state RELATED,ESTABLISHED
ACCEPT !icmp anywhere anywhere tcp sppt dpt:http state RELATED,ESTABLISHED
DROP all 192.168.0.0/24 anywhere state NEW
ACCEPT icmp 10.0.0.1 icmp echo-reply
ACCEPT icmp 10.0.0.1 icmp echo-request
ACCEPT icmp 10.0.0.1 icmp destination-unreachable
Chain FORWARD (policy ACCEPT)
target prot source destination
DROP all 192.168.0.0/24 anywhere
DROP all 192.168.0.0/24 anywhere
DROP all 127.0.0.1 anywhere
DROP all anywhere anywhere state NEW
Chain OUTPUT (policy ACCEPT)
target prot source destination
DROP tcp anywhere 192.168.0.0/24 state NEW tcp ppt:http
# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
target prot source destination
Chain POSTROUTING (policy ACCEPT)
target prot source destination
MASQUERADE all anywhere anywhere
Chain OUTPUT (policy ACCEPT)
target prot source destination
```

# 用户自定义规则

对于更复杂的规则，你可能想为 INPUT 和 FORWARD 链都创建自定义链，这样你就不需要为每个链重复 DROP 操作。相反，你只需要一个链，让 FORWARD 和 INPUT 链都向该链输入进行 DROP 操作。请记住，FORWARD 和 INPUT 操作可能会在它们共享的规则之外有单独的添加。在下一个示例中，有一个名为 `arriving` 的自定义链。该链在脚本顶部使用 `-N` 选项定义：

```bash
iptables -N arriving
```

用户链在被用作其他规则的目标之前必须先定义。因此，你必须首先定义并添加该链链的所有规则，然后将其作为目标。首先定义 `arriving` 链并添加其规则。然后，在文件末尾，将其用作 INPUT 和 FORWARD 链的目标。INPUT 链列出了接受数据包的规则，而 FORWARD 链有一个 ACCEPT 策略，默认会接受这些数据包。

```bash
iptables -N arriving
iptables -F arriving
# 伪欺攻击，拒绝内部网络上
# 具有外部源地址的所有数据包。
iptables -A arriving -j LOG -i eth1 ! -s 192.168.0.0/24
iptables -A arriving -j DROP -i eth1 ! -s 192.168.0.0/24
iptables -A arriving -j DROP -i eth1 -s 192.168.0.0/24
# 脚本末尾项
iptables -A INPUT -j arriving
iptables -A FORWARD -j arriving
```

所示规则列表如下：
Chain INPUT (policy DROP)

| target | prot | source | destination |
| :--- | :--- | :--- | :--- |
| arriving | all | -- | 0.0.0.0/0 |
| Chain FORWARD (policy ACCEPT) | | | | |
| target | all | -- | 0.0.0.0/0 |
| arriving | all | -- | 0.0.0.0/0 |
| Chain arriving (2 references) | | | | |
| target | all | 192.168.0.0/24 | 0.0.0.0/0 LOG flags 0 level 4 |
| LOG | all | 192.168.0.0/24 | 0.0.0.0/0 |
| DROP | all | 192.168.0.0/24 | 0.0.0.0/0 |
| DROP | all | 192.168.0.0/24 | 0.0.0.0/0 |

对于链不同的规则，你仍然需要输入单独的规则。在 **myfile** 脚本中，FORWARD 链具有 ACCEPT 策略，允许所有转发到本地网络的数据包通过防火墙。如果 FORWARD 链可以接受数据包。在本示例中，FORWARD 和 INPUT 链对于在 **eth1** 设备上接受数据包有不同的规则。INPUT 规则更严格。要让网络通过防火墙接收转发的数据包，你可以使用单独的 FORWARD 规则在其设备上启用转发，如下所示：

```bash
iptables -A FORWARD -j ACCEPT -p all -i eth1
```

INPUT 链将仅接受来自本地网络的数据包。

```bash
iptables -A INPUT -j ACCEPT -p all -i eth1 -s 192.168.0.0/24
```

# IP 伪装 (IP Masquerading)

在 Linux 系统上，你可以设置一个网络，你只有一个连接到互联网，而网络上的几个系统可以使用该连接。通过这种方式，只需一个 IP 地址，多个不同的系统就可以连接到互联网。这种方法被称为 IP 伪装，在这种网络中，一个系统通过自己的 IP 地址连接到互联网，而其他系统连接在本地局域网（LAN）上。当本地系统想要访问网络时，它会伪装连接互联网的系统。

IP 伪装是在 Linux 上使用 `iptables` 工具实现的。如果你，设置了一个防火墙，就可以将其配置为 IP 伪装。目前，IP 伪装支持所有网络服务，如网页浏览、telnet 和 ping。其他服务（如 IRC、FTP 和 Real Audio）需要特定的模块。你希望本地系统访问的规则也必须在防火墙上，因为请求和响应由该系统处理。

你可以在 IP 伪装资源网站找到更多信息。特别是，Linux IP Masquerade HOWTO 提供了在系统上设置 IP 掩的详细步骤指南。在使用它之前，内核必须支持 IP 伪装。如果你的内核不支持，你可能需要重新编译内核以包含 ip masquerade 支持，或者加载模块来添加它。更多信息请查看 IP Masquerade HOWTO。

通过 IP 伪装，防火墙使用 `iptables` 工具进行配置。如果你，设置了一个防火墙，就可以将其配置为 IP 伪装。目前，IP 伪装支持所有网络服务，如网页浏览、telnet 和 ping。其他服务（如 IRC、FTP 和 Real Audio）需要特定的模块。你希望本地系统访问的规则也必须在防火墙上，因为请求和响应由该系统处理。

# 伪装 NAT (Masquerading NAT)

在 Linux 系统上，你可以设置一个网络，你只有一个连接到互联网，而网络上的几个系统可以使用该连接。通过这种方式，只需一个 IP 地址，多个不同的系统就可以连接到互联网。这种方法被称为 IP 伪装，在这种网络中，一个系统通过自己的 IP 地址连接到互联网，而其他系统连接在本地局域网（LAN）上。当本地系统想要访问网络时，它会伪装连接互联网的系统。

# IP 转发

然后通过如下所示手动设置 IP 转发，使用 `sysctl`（第 33 章），或者使用 `redhat-config` 工具（系统工具中的内核调优）并在网络下的 IP 面板中勾选 IP Forward。这将设置 `/etc/sysctl.conf` 文件中的 `net.ipv4.ip_forward` 变量（你也可以手动修改此文件）。IP 转发默认是关闭的。

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```
