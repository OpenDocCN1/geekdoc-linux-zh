
# OpenBSD 与 FreeBSD 无线接入点配置指南

## OpenBSD 接口配置合并

在 OpenBSD 上，你可以通过创建 `/etc/interfaces` 将这两个步骤合并为一步。

你可以通过 `ifconfig` 检查接入点是否已启动运行：

```
wlan0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
lldaddr 00:25:9c:72:cf:60
priority: 4
groups: wlan
media: IEEE802.11 autoselect mode 1g hotspot
status: active
ee80211:npa unwired broadcast 1 bssid 00:25:9c:72:cf:60 wpa displayed
protocols wpa1,wpa2 wpa-ms wp paciphers tkip,tcmp wpagroupcipher tkip 100dbm
inet 6 fe80::225:cff:fe64 prefixlen 64 scope 0x2
inet 6 2001:db8::baad:f0d:1 prefixlen 64
inet 10.50.90.1 netmask 255.255.255 broadcast 10.255.255.
```

注意状态：`active` 指示，以及我们没有显式显示的 WPA 选项使用了其合理的默认值。

## FreeBSD WPA 接入点

从我们之前配置的 WEP 接入点迁移到更安全的设置是简单的。FreeBSD 的 WPA 支持以 `hostapd` 的形式出现（该程序与 OpenBSD 的 `hostapd` 类似，但并不相同）。我们首先通过编辑 `/etc/start_if0` 来移除身份验证信息。编辑后的文件应该像所示：

```
wlans_0="wlan0"
create_args wlan0="wlan0 wlanmode hostapd"
ifconfig wlan0=inet 10.50.90.1 netmask 255.255.255.0 ssid unwiredbroad mode 11g"
ifconfig wlan0_ipv6="2001:db8::baad:f0d:1 prefixlen 64"
```

接下来，在 `/etc/rc.conf` 中为 `hostapd` 添加启用行：

```
hostapd_enable="YES"
```

最后，`hostapd` 需要在 `/etc/hostapd.conf` 中进行一些配置：

```
interface=wlan0
debug=1
ctrl_interface=/var/run/hostapd
ctrl_interface_group=wheel
ssid=unwiredbroad
wpa=1
wpa_passphrase=0xideadebeef9
wpa_key_mgmt=WPA-PSK
wpa_pairwise=CCMP TKIP
```

在这里，此接口规范是自言自明的，`debug` 值用于产生最少的消息。范围是从 0 到 4，其中 0 表示完全没有调试消息。除非你正在开发 `hostapd`，否则不需要更改 `ctrl_interface*` 设置。接下来的五行第一行设置了网络标识符。随后的行启用 WPA 并设置密码。最后两行指定了密钥管理算法和加密方案。（更多细节和更新，请参阅 `hostapd(8)` 和 `hostapd.conf(5)` 手页）。

配置成功后（运行 `/etc/rc.hostapd` 强制生效），`ifconfig` 会产生关于两个接口的输出，类似于：

```
wlan0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 mtu 2290
ether 00:24:1d:9a:bf:67
media: IEEE 802.11 Wireless Ethernet autoselect 11g <1>
status: running
wlan0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 mtu 1500
ether 00:24:1d:9a:bf:67
inet 10.50.90.1 mask 0ffffffff0 10.50.90.255
inet6 2001:db8::bad:bf00:prefixlen 64
media: IEEE 802.11 Wireless Ethernet autoselect 11g <1>
status: running
ssid unwiredbroad channel 6 (2437 Mhz 11g) bssid 00:24:1d:9a:bf:67
country US home Wpa priority MIXED deft tkp 2:128-bit
txpower 0 scanid 60 promote dtim-period 1 -dfs
```

`status: running` 一行意味着你已经启动运行，至少在链路层面是如此。

## 接入点的 PF 规则集

接口配置完成后，是时候开始将接入点配置为数据包网关了。你可以开始通过 `sysctl.conf` 或 `rc.conf` 文件设置章节中的相应条目进行配置，并复制 `pf.conf` 文件。根据上一章中对你最有用的部分，`pf.conf` 文件可能如下所示：

```
ext_if = "em0" # 外部接口的宏 - 使用 tun0 或 ppPoE
int_if = "int0" # 内部接口的宏
localnet = $int_if:network
nat_address = 203.0.113.5 # 设置 nat-to 的地址
client_out = { ssh, domain, pop3, ... }
...
```

## OpenBSD 客户端设置

以 OpenBSD 为例，为了连接到你已配置的 WEP 接入点，你的 OpenBSD 客户端需要一个带有主机名（例如，`/etc/hostname.ral0`）配置文件，其中包含以下行：

```
up media autoselect mode 11g chan 1 nwid unwiredbsd mwkey 0x1adebeef9
rtsol
```

第一行设置了比通常要求的更详细的链路层参数。只有 `up` 以及 `nwid` 和 `mwkey` 参数是严格必要的。在几乎所有情况下，驱动程序将在适当的信道上以最佳可用的模式与接入点关联。第二行用于 DHCP 配置，在实践中，它会使系统运行 `dhclient` 命令来获取 TCP/IP 配置信息。最后一行调用 `rtsol(8)` 来启动 IPv6 配置。

如果你选择使用 WPA 配置，文件将看起来如下所示：

```
up media autoselect mode 11g chan 1 nwid unwiredbsd wpkey 0x1adebeef
rtsol
```

同样，第一行设置了链路层参数，其中关键参数是网络选择和加密参数 `nwid` 和 `wpkey`。你可以尝试操作 `mode` 和 `chan` 参数；在几乎所有情况下，驱动程序将在适当的信道上以最佳可用的模式与接入点关联。

如果你在将配置提交到 `/etc/hostname.if` 文件以设置客户端之前，想从命令行尝试配置命令，测试 WEP 网络的命令如下：

```
$ sudo ifconfig ral0 up 11g chan 1 nwid unwiredbsd mwkey 0x1adebeef
```

`ifconfig` 命令应该在没有任何输出的情况下完成。然后你可以使用 `ifconfig` 检查接口是否已成功配置。输出应该像下面所示：

```
ral0: flags=EE802<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
laddr 00:25:9c:72:cf:60
priority: 4
groups: wlan
media: IEEE802.11 autoselect (OFDS4 mode 11g)
status: active
ieee802.11: nwid unwiredbsd chan 1 bssid 00:25:9c:72:cf:60 mwkey <not displayed> 100dbm
inet6 6fe0::225:cff:fe72:cf60%ral0 prefixlen 64 scopeid 02
```

注意，`ieee802.11:` 行显示了网络名称和信道，以及其他几个参数。这里显示的信息应该与你在 `ifconfig` 命令行上输入的内容匹配。

以下是配置 OpenBSD 连接到 WPA 网络的命令：

```
$ sudo ifconfig ral0 nwid unwiredbsd wpkey 0x1adebeef
```

该命令应该在没有任何输出的情况下完成。如果你使用 `ifconfig` 检查接口状态，输出将看起来像这样：

```
$ ifconfig ral0
ral0: flags=883<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
laddr 02:25:9c:72:cf:60
priority: 4
group: wlan
media: IEEE802.11 autoselect(OFMS5 mode 11g)
status: active
ieee802.11: nwid unwiredbsd 1 bssid 00:25:9c:72:cf:60 wpkey not displayed> wapprotos wpa1,wpa2 aapakms pksim wcpapers tkip,ccmp wpgroupcipher tkip 100dbm
inet6 fe80::225:9cc:72:cf:60%ral0 prefixlen 64 scopeid02
```

检查 `ieee802.11:` 行是否显示了正确的网络名称和合理的 WPA 参数。

一旦你确认接口已在链路层配置完成，使用 `dhclient` 命令为接口配置 TCP/IP，如下所示：

```
$ sudo dhclient ral0
```

`dhclient` 命令应该会打印出它与 DHCP 服务器对话的摘要，看起来像这样：

```
DHCPREQUEST on ral0 to 255.255.255.255 port 67
DHCPREQUEST on ral0 to 255.255.255.255 port 67
DHCPACK from 10.50.90.1 (00:25:9c:72:cf:60)
bound to 10.50.90.11 -- renewal in 1800 seconds.
```

要为接口初始化 IPv6，输入以下内容：

```
$ sudo rtsol ral0
```

`rtsol` 命令通常在没有任何消息的情况下完成。使用 `ifconfig` 检查接口配置，以确认接口确实收到了 IPv6 配置。

## FreeBSD 客户端设置

在 FreeBSD 上，你可能需要做比 OpenBSD 稍多一些的工作。根据你的内核配置，你可能需要在 `/boot/loader.conf` 中添加相关的模块加载行。在我其中一个测试系统上，`/boot/loader.conf` 看起来如下：

```
if_ral_load="YES"
wlan_if_load="YES"
wlan_sta_load="YES"
wlan_wep_load="YES"
wlan_ccmp_load="YES"
wlan_tkip_load="YES"
```

加载相关模块后，你可以通过执行以下命令加入之前配置的 WEP 网络：

```
$ sudo ifconfig wlan0 ssid unwiredbsd mode 11g wepmode on wepkey 0x1adebeef
```

然后，执行此命令以获取接口的 IPv4 配置：

```
$ sudo dhclient wlan0
```

要为接口初始化 IPv6，输入以下内容：

```
$ sudo rtsol wlan0
```

`rtsol` 命令通常在没有任何消息的情况下完成。使用 `ifconfig` 检查接口配置，以确认接口确实收到了 IPv6 配置。

若要进行持久配置，创建一个 `start_if` 文件（如果物理接口名称不同，请将 `wlan0` 替换为实际名称），内容如下：

```
wlans_ral0="wlan0"
create_args_wlan0="wlanmode sta"
ifconfig_wlan0="ssid unwiredbsd wepmode on wepkey 0x1adebeef DHCP"
```

## 使用 authpf 保护你的无线网络

MAC 地址过滤本身并不是一个稳固的防御。安全专家倾向于认为，即使是 WEP 加密也帮助有限，因为更改 MAC 地址太容易了。OpenBSD 开发者在 3.1 版本引入 `authpf` 时，选择了一种完全不同的方法。与其将访问权限绑定到硬件标识符（网卡的 MAC 地址），他们认为现有的、灵活的用户认证机制更为合适。`authpf` 允许系统按用户加载 PF，从而决定哪个用户可以做什么。

要使用 `authpf`，你需要创建以 `authpf` 程序作为 shell 的用户。为了网络访问，用户通过 SSH 登录网关。用户成功完成 SSH 认证后，`authpf` 会加载为该用户或用户类定义的规则。这些规则通常适用于用户登录的 IP 地址，只要用户通过 SSH 连接保持连接，规则就会一直加载并生效。一旦 SSH 会话终止，规则将卸载；在大多数情况下，来自用户 IP 的非 SSH 流量将被拒绝。在合理的配置下，只有由授权用户产生的流量会被允许。
