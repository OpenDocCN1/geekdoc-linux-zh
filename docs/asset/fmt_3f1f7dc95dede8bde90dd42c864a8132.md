
```bash
## nvram set lan_ipaddr="192.168.1.40"
## nvram set lan_gateway="192.168.1.1"
## nvram set lan_dns="192.168.1.10"
## nvram commit
## ifup lan
```

注意我们还添加了默认网关和 DNS 服务器。这是必须的，因为除了其他外，你可以使用 `ipkg` 命令保持软件包更新并安装软件。接下来，我们将启用桥接并禁用动态主机配置协议 (DHCP)：

```bash
# nvram set wlo_mode="wet"      bridged client
## nvram commit
## wifi
# cd /etc/init.d
# mv s50dnsmasq disabled_s50dnsmasq
## chmod -x s50dnsmasq
## killall dnsmasq
```

WPA 需要 `nas` 包，而 `wl` 包则不需要，但它允许你做一些很酷的事情，例如查看周围所有的无线网络及其加密类型：

```bash
# ipkg install nas wl
```

www.syngress.com

# 来自地底的笔记……

## 升级后重新安装 NAS 包

OpenWrt 中的 `NAS` 包是一个专有的二进制工具，允许你为无线连接设置 WPA/WEP 加密。在设置 WET 桥接器时，我们遇到了问题，并意识到从 RC5 升级到 RC6 是原因。解决方法是按照如下方式重新安装 `NAS` 包：

```bash
## ipkg remove nas
## ipkg install nas
```

我们在 OpenWrt 论坛中发现了这一点，我们强烈建议你注册并定期查阅。它们对于排排除 OpenWrt 的问题非常有用。以下论坛帖子引导我们发现了前述的解决方案：http://forum.openwrt.org/viewtopic.php?pid=38430。帖子中提到的论坛账号“mbm” 是 Mike Baker，他是 OpenWrt 项目的联合创始人兼首席开发者。关于 `NAS` 的更多信息，请参阅 http://wiki.openwrt.org/OpenWrtDocs/nas。

接下来，遵循此操作来扫描无线网络：

```bash
# wl scan
```

在我们的示例中，我们看到一个名为 paulcom 的网络，支持 WPA：

```bash
## wl status
```

# 第 4 章 • WRT54G 趣味项目

第一个命令将 `lan_names` 变量设置为仅 `vlan0`。默认情况下，在 WRT54GL 上它还会包含 `eth1`，即无线接口。由于我们希望无线接口显示为广域网（WAN）端口，请运行下一个命令并将 `eth1` 设置为 `wan_interface`，这告诉网络子系统将此接口视为 WAN 端口，从而避免了重新配置防火墙规则的麻烦。

## 警告

在更改 WRT54G 上的 VLAN 分配之前，请务必确认与你的路由器模型相对应的 VLAN！完整参考请参阅以下指南：

http://wiki.openw.org/OpenWrtDocs/Configuration#NetworkInterfaceNames

这是一个非常重要的步骤，因为它将引入一种新层次的“变砖”风险，极可能需要安装 JTAG 连接器和电缆。你可能会问：“这种情况发生过作者身上吗？”答案是定的，确实发生过。请参考第 8 章。

图 4.4 展示了我们如何更改 WRT54G 上的 VLAN 分配的图形表示。无线接口 `eth1` 被分配到与 WAN 接口相关的 VLAN，这需要路由能力（而不是桥接）将流量从以太网交换机发送到无线网络。

## 图 4.4 路由桥接口配置

![](img/41991837f74596e7c29a2498b6ec56e8_193_0.png)

## 注意

OpenWrt Wiki 中的两份文档在解释网络子系统工作原理方面做得非常出色：

http://wiki.openw.org/OpenWrtDocs/NetworkInterfaces 在此文档，使用 Asus WL-500G Premium 设备作为示例解释了 OpenWrt 网络子系统的工作原理。

http://wiki.openw.org/OpenWrtNVRAM 在名为“1. Interface Settings”的章节中，该文档进一步解释了所有接口设置之前的所有接口名称的含义（即 `lan` 和 `wan`）。

![](img/41991837f74596e7c29a2498b6ec56e8_193_1.png)

## WRT54G 趣味项目 • 第 4 章

现在你可以通过 wrt-livingm 提供的无线网络为你的 WAN 适配器（`eth1`）配置静态 IP 地址。虽然你可以使用 DHCP 配置，但连接回的静态 IP 地址易于管理。

```
# nvram set wan_proto="static"
# nvram set wan_ipaddr="192.168.1.56"
# nvram set wan_netmask="255.255.255.0"
# nvram set wan_gateway="192.168.1.1"
# nvram set wan_dns="192.168.1.10"
## nvram commit
```

重新加载无线设置，现在这将包括重新加载 WAN 适配器：

```
# ifdown wan
# ifup wan
# /sbin/wifi
```

## 配置防火墙

为了管理我们正在使用的路由桥（图 4.3）WRT54G，我们需要调整适用于 WRT54G 内部路由过程的防火墙规则。默认防火墙规则不接受 WAN 端口上的连接；因为我们把无线适配器放在 WAN VLAN 中，我们需要调整规则。你可以通过编辑 `/etc/firewall.user` 文件轻松地调整运行 OpenWrt 的 WRT54G 上的防火墙规则。要允许通过端口 22 传输控制协议 (SSH) 和端口 80 TCP (HTTP) 进行管理，请添加以下规则：

```
iptables -t nat -A Prerouting_rule -i $WAN -p tcp --dport 22 -j ACCEPT
iptables -A Input_rule -i $WAN -p tcp --dport 22 -j ACCEPT
iptables -t nat -A Prerouting_rule -i $WAN -p tcp --dport 80 -j ACCEPT
iptables -A Input_rule -i $WAN -p tcp --dport 80 -j ACCEPT
```

然后，按如下方式执行 `/etc/firewall.user`：

```
# /etc/firewall.user
```

此脚本将清除所有防火墙规则并重置它们，包括你的新更改。如果你在 WRT54G 上启了 HTTPS 管理，请允许端口 443 代替（或取决于你的保护级别，额外）端口 80：

```
iptables -t nat -A Prerouting_rule -i $WAN -p tcp --dport 443 -j ACCEPT
iptables -A Input_rule -i $WAN -p tcp --dport 443 -j ACCEPT
```

你可能还需要在防火墙中打开一个映射到连接到 LAN VLAN 主机的端口。例如，如果你需要对游戏系统进行 FTP 访问，你应该添加以下规则：

```
iptables -t nat -A Prerouting_rule -i $WAN -p tcp --dport 21 -j DNAT --to 10.10.10.10:21
```

![](img/41991837f74596e7c29a2498b6ec56e8_194_0.png)

## 第 4 章 • WRT54G 趣味项目

之前的规则将允许：

```
iptables -t nat -A Prerouting_rule -i $WAN -p tcp --dport 22 -j ACCEPT
```

## 强制门户 (Captive Portal)

强制门户是一个实用的工具，允许用户加入无线网络并显示一个可以注册的页面。在 WRT54G 上有多种强制门户解决方案。Wifidog 和 Chillspot 是两个项目，但它们通常需要外部服务器或账户。如果我们有一个运行在 WRT54G 上且不需要其他服务器或账户的一体化强制门户就好了。

> 关于强制门户如何重定向流量，请参考维基百科文章 http://en.wikipedia.org/wiki/Captive_portal，特别是“Implementation”章节。
