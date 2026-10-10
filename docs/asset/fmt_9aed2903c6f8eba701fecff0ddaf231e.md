
```
Jun 20:43:51 maple pppd[2077]: pppd 2.4.1 started by root, uid 0
Jun 20:43:51 maple ifup-ppp: pppd started for ppp0 on /dev/modem at 115200
Jun 20:43:52 maple chat[2079]: abort on (BUSY)
Jun 20:43:52 maple chat[2079]: abort on (ERROR)
Jun 20:43:52 maple chat[2079]: abort on (NO CARRIER)
Jun 20:43:52 maple chat[2079]: abort on (NO DIALTONE)
Jun 20:43:52 maple chat[2079]: abort on (BUSY)
Jun 20:43:52 maple chat[2079]: abort on (ERROR)
Jun 20:43:52 maple chat[2079]: abort on (NO CARRIER)
Jun 20:43:52 maple chat[2079]: abort on (NO DIALTONE)
Jun 20:43:52 maple chat[2079]: abort on (BUSY)
Jun 20:43:52 maple chat[2079]: abort on (ERROR)
Jun 20:43:52 maple chat[2079]: abort on (NO CARRIER)
Jun 20:43:52 maple chat[2079]: abort on (NO DIALTONE)
```

# 第 16 章：连接互联网 707

计算机可能具有多个网络接口，例如环回接口、以太网局域网、到另一台计算机的直接线路或拨号接口。客户端计算机为了通过路由器访问互联网，可能在局域网上被分配一个私有 IP 地址。到路由计算机的连接将作为所有地址的网关。

以下是一个使用 Linux 作为局域网和互联网之间路由器的示例：

- Linux 系统至少有两个网络接口：一个连接到办公室局域网，一个连接到互联网。连接到互联网的接口可能是拨号 PPP 连接，在如今更有可能是高速 DSL 或电缆调制解调器连接。
- 局域网上不是目标为局域网内已知计算机的数据包将被转发到路由器（即作为路由器的 Linux 系统）。因此，每个客户端都将 Linux 系统识别为网关系统。
- Linux 路由器/防火墙被配置为接收来自本地局域网的数据包，然后将这些数据包转发到它的其他接口（可能是连接到互联网的 PPP 连接）。如果局域网使用私有 IP 地址，防火墙还会配置为使用 IP 伪装（IP masquerading）或网络地址转换（NAT）。

后续章节将描述如何设置 Linux 路由器，以及你局域网中的客户端计算机（Linux 和 MS Windows 客户端）将如何使用该路由器。将 Linux 作为路由器还提供了一个改进互联网连接安全的绝佳机会，通过设置防火墙来过滤流量并隐藏局域网内计算机的身份（IP 伪装）。

## 配置 Linux 路由器

要将你的 Linux 计算机配置为路由器，你需要准备一些工作。在设置路由之前，你需要执行以下操作：

- 连接到你的局域网。添加网卡并配置局域网上的计算机（如第 15 章所述）。
- 连接到互联网。从你的 Linux 计算机设置到互联网服务提供商（ISP）的拨号或其他类型的连接。这在本章前面的设置出站 PPP 连接章节中有所描述。
- 将你的 Linux 计算机配置为路由器。参见本节的其余部分。

### 选择 IP 地址

你在局域网上使用的 IP 地址类型将影响此过程中的几点。以下是它们的区别：

- 私有 IP 地址 —— 如果你局域网上的计算机使用私有 IP 地址（第 15 章中描述），你需要将 Linux 设置为防火墙以执行 IP 伪装或 NAT（如第 14 章所述）。由于这些数字是私有的，当 Linux 路由器转发它们的请求时，必须在互联网上隐藏它们。通过伪装或 NAT 转发的数据包在外部看来就像是来自转发这些数据包的 Linux 计算机。
- IP 地址 —— 如果你的局域网使用由 ISP 或其他注册机构正式分配的地址，则你不需要进行 IP 伪装或 NAT。（实际上，对于你任何想要暴露给世界的机器，例如公共服务器，你都会希望拥有一个有效的公网 IP 地址。）

在你不配置局域网服务器上的计算机的情况下，你可能会使用私有 IP 地址。

### 启用转发和伪装

当 Linux 计算机的局域网和互联网接口就绪后，你将使用以下步骤将 Linux 设置为路由器。完成此步骤后，局域网上的任何客户端计算机都可以将你的计算机识别为网关以便以便 Linux 访问互联网。

1. 以 root 用户身份用文本编辑器打开 `/etc/sysconfig/network` 文件。然后按照下文描述添加默认网关或默认网关设备。你的默认网关是发往你网络之外流量的去处。这就是你识别互联网连接的地方。以下是选择一个并输入的方法：

- 默认网关 —— 如果你有一个访问互联网的静态 IP 地址，在此处输入该 IP 地址。例如，如果你的互联网连接通过连接到网卡地址为 192.168.0.1 的 DSL 调制解调器，请如下输入该地址：
- 默认网关 —— 如果你使用连接到特定接口时分配的动态地址访问互联网，在此处输入该接口。例如，如果你在第一个 PPP 设备上有一个到互联网的拨号接口，你将如下输入 `ppp0` 作为默认网关设备：

```
GATEWAY=192.168.0.1
```

```
GATEWAY=ppp0
```

当你完成时，该文件的内容应该类似于以下：

```
NETWORKING=yes
HOSTNAME='maple.handsonhistory.com'
DOMAINNAME='handsonhistory.com'
#GATEWAY=
GATEWAYDEV=ppp0
```

在这种情况下，计算机被配置为通过拨号连接 (`ppp0`) 将数据包路由到互联网。

2. 开启 IP 数据包转发。其中一种方法是将 `/etc/sysctl.conf` 文件中的 `net.ipv4.forward` 值更改为 1。以 root 用户身份用任何文本编辑器打开该文件并按如下方式更改：

`net.ipv4.forward = 1`

> 注意：你可以重启网络以使此更改生效（`service network restart`）。要在不重启网络的情况下使更改生效，输入 `echo 1 > /proc/sys/net/ipv4/forward`。

3. 如果你局域网上的计算机具有 IP 地址，请跳到“网络客户端”部分。如果你的计算机具有 IP 地址，请继续此处操作。

> 警告：应使用以下配置 `iptables` 的行。它们本身不仅仅是描述了如何操作。

4. 为了在你的路由器上实现 IP 伪装，你需要定义哪些地址将进行伪装。以下示例假设你对第一个拨号接口 (`ppp0`) 的所有出包进行伪装。

以 root 身份输入以下命令：

```
# iptables -t nat -A POSTROUTING -o ppp0 -j MASQUADE
# iptables -A FORWARD -s 10.0.0.0/24 -j ACCEPT
# iptables -A FORWARD -d 10.0.0.0/24 -j ACCEPT
# iptables -A FORWARD -s ! 10.0.0.0/24 -j DROP
```

之前的命令通过为 `ppp0` 接口附加 POSTROUTING 规则来开启伪装。接下来的两行允许来自 `10.0/24` 网络的转发。最后一行丢弃不是来自 `10.0/24` 网络的包。

之前的行将规则添加到运行中的 `iptables`。要使当前规则持久化，请保存为：

```
# service iptables save
```

这将所有规则复制到 `/etc/sysconfig/iptables` 文件，系统每次重启时都会从那里读取规则。如果新规则不起作用，只需将 `iptables.save` 文件复制回原始的 `iptables` 文件即可。

5. 此时，你可能需要如下重启网络：

```
# /etc/init.d/network restart
```

6. 然后，要重启防火墙，输入以下内容：

```
# /etc/init.d/iptables restart
```

7. 要查看你的新规则是否生效，输入 `iptables -L`。要查看 NAT 规则，输入 `iptables -L -t nat`。

如果从 Linux 到互联网的路由是由拨号连接提供的，你可能希望开启按需拨号。

## 配置网络客户端

- 将请求的名称（例如 www.redhat.com）解析为 IP 地址。
- 使用网络接口查找本地系统到远程系统的路由。

```
order hosts,bind
```

2. 以 root 用户身份输入以下内容重启网络接口：

```
# /etc/init.d/network restart
```

3. 启动后，输入以下内容：

```
# netstat -r
```
