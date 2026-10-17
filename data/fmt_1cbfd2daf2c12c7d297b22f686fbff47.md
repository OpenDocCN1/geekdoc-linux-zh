
`net-setup` 会向您询问一些关于环境的问题。完成后，您应该有一个工作的连接。按照说明测试您的连接。如果测试成功，恭喜！您现在可以安装 Gentoo 了。跳过本节其余部分继续操作磁盘。如果您的网络不起工作，请继续手动配置。

假设您需要连接互联网，安装 CD（任何版本）已通过 PoE 让事情变得简单。使用提供的 `adsl-setup` 配置您的网络。系统会提示您连接到 ADSL 调制器的以太网设备、用户名和密码、DNS 服务器的 IP 以及您是否需要基础防火墙。

## 代码列表 6：使用 PoE

```
# adsl-setup
# adsl-start
```

如果出现问题，请通过 `/etc/ppp/pap-secrets` 或 `/etc/ppp/chap-secrets` 检查用户名和密码输入是否正确。确保使用了正确的以太网设备。如果以太网设备不存在，将必须加载正确的网络模块。在这种情况下，请继续手动配置，我们将说明如何加载正确的网络模块。如果一切正常，继续操作磁盘。

> 注意：PPTP 支持仅适用于 x86

如果您需要 PPTP，可以使用安装 CD 提供的 `pppclient`。但首先您需要确保您的配置是正确的。编辑 `/etc/ppp/pap-secrets` 或 `/etc/ppp/chap-secrets` 以包含正确的用户名/密码组合：

### 代码列表 7：编辑 /etc/ppp/chap-secrets

```
# nano -w /etc/ppp/chap-secrets
```

然后根据需要调整 `/etc/ppp/options.ppt`：

### 代码列表 8：编辑 /etc/ppp/options.ppt

```
# nano -w /etc/ppp/options.ppt
```

完成后，运行 `pptp`（带有 `options.ppt` 中设置的选项）连接到服务器：

### 代码列表 9：连接到拨号服务器

```
# pptp <server ip>
```

## 3.c. 手动配置网络

### 加载正确的网络模块

当安装 CD 启动时，它尝试检测您所有的硬件设备并加载相应的内核模块（驱动程序）来支持您的硬件。在大多数情况下，它工作得很好。但在某些情况下，它可能不会自动加载您所需的内核模块。

如果 `net-setup` 或 `add-setup` 失败，可能是网卡没有被立即发现。这意味着您可能需要手动加载正确的内核模块。

要确定哪些内核模块提供网络功能，请使用 `ls`：

#### 代码列表 10：搜索提供的模块

```
# ls /lib/modules/$(uname -r)/kernel/drivers/net
```

如果您找到了网卡的驱动程序，使用 `modprobe` 加载内核模块：

#### 代码列表 11：使用 modprobe 加载内核模块

（作为一个示例，我们加载 `pcnet32` 模块）

```
# modprobe pcnet32
```

要检查网卡是否被检测，请使用 `ifconfig`。检测到的网卡结果如下：

#### 代码列表 12：网卡可用性测试，成功

```
# ifconfig eth0
link encap:Ethernet Hardware:00:00:00:00:00:00
BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:0 dropped:0 overruns:0 frame:0
TX packets:0 dropped:0 overruns:0 carrier:0
collisions:0 queue:0
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)
```

如果您收到错误则网卡未被检测：

#### 代码列表 13：网卡可用性测试，失败

```
# ifconfig eth0
eth0: error fetching interface information: Device not found
```

如果您的系统中有多个网卡，它们被命名为 `eth0`、`eth1` 等。请确保您想要使用的网卡运行良好，并在整个文档中使用正确的名称。我们假设使用的是网卡 `eth0`。

#### 代码列表 14: 使用 dhcp

```
# dhcp
某些网络管理员要求你使用由 DHCP 服务器提供的
主机名和域名。
在这种情况下，请使用
# dhcp -HD eth0
```

如果这有效（例如 `ping` 通某个服务器，如 Google），那么你已经准备就绪，可以继续下去了。跳过本节的其余部分，继续“准备磁盘”。

### 准备无线访问

> 注意：`ifconfig` 的支持仅适用于 x86 和 PPC 安装光盘。你仍然可以通过遵循 linux-wlan-ng 项目的说明来使扩展功能工作。

如果你正在使用 (802.11) 网卡，在进一步操作之前可能需要配置无线设置。要查看网卡上的当前设置，可以使用 `iwconfig`。`iwconfig` 可能会显示如下内容：

#### 代码列表 15: 配置无线设置

```
# iwconfig eth0
IEEE 802.11-DS SSID:GentooNode
eth0  Managed Frequency:24.222GHz Access Point:00:09:SB:11:CC:F2
BitRate:1M Power:20dBm Sensitivity:0/65535
Retries:16 Fragment:off Power:Management:off
Link Quality:0/70 Signal level:-51 dbm Noise level:-102 dbm
Rx wv invalid:0 Tx wv invalid:0 Tx
excessive retries:27 Invalid miss:350282 Missed beacon:84
```

> 注意：某些无线网卡的设备名称可能是 `wlan0` 而不是 `eth0`。运行不带命令行参数的 `iwconfig` 来确定设备名称。

对于大多数用户来说，只有两个设置可能需要更改：ESSID（网络名称）或 WEP 密钥。如果你需要更改 SSID 或添加 WEP 密钥，可以使用以下命令：

#### 代码列表 16: 更改 ESSID 并添加 WEP 密钥

```
# 这将网络名称设置为 "GentooNode"
# iwconfig eth0 SSID GentooNode

# 这设置 WEP 密钥
# iwconfig eth0 key 12345678901234567abcd

# 这设置一个 ASCII 密钥 - 前缀加上 "s:*"
# iwconfig eth0 key s:some-password
```

然后你可以通过 `iwconfig` 确认你的无线设置。如果你有无线网络，可以继续在下一节（理解网络术语）中配置网络选项，或按之前描述的方法使用 net-tool。

### 理解网络术语

> 注意：如果你知道自己的 IP 地址、广播地址、子网掩码和 DNS 服务器，可以跳过本节并继续使用 `ifconfig` 和 `route`。

如果上述所有方法都失败，你将必须手动配置网络。这并不困难。然而，你需要熟悉网络术语，这样就能按照你的意愿配置网络。阅读后，你将知道什么是网关、什么是服务器、什么是广播地址，以及你为什么需要 DNS 服务器。

在网络中，主机通过其 IP 地址（互联网协议地址）进行标识。这种地址是 0 到 255 之间四个数字的组合。嗯，至少我们是这样理解的。实际上，这样的 IP 地址由 32 位（0 和 1）组成。让我们来看一个一个示例：

#### 代码列表 17: IP 地址示例

| IP 地址 (数字): | 192.168.0.2 | 11000000 10101000 00000010 |

| IP 地址 (位): | 192 | 168 | 2 |

对于所有关联网络而言，这样的 IP 地址对主机来说是唯一的（即每个可以到达的主机都必须有唯一的 IP 地址）。为了区分网络内部和外部的主机，IP 地址分为两部分：网络部分和主机部分。

这种分离是通过子网掩码进行的，一部分是网络部分，另一个是主机部分。通常，子网掩码可以写成 IP 地址。

#### 代码列表 18: 网络/主机分离示例

| IP 地址: | 192.168.0.2 | 11000000 10101000 00000010 |

| 子网掩码: | 255.255.255.0 | 11111111 11111111 11111111 0 |

| 网络 主机: | | |
