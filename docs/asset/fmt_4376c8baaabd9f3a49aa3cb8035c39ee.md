
配置无线接入点的确切方法取决于设备的品牌和型号；厂商提供配置无线接入点的说明。通常，您通过 Windows PC 上的图形客户端应用程序进行配置，或使用 WAP 的基于 Web 的界面。如果启用加密，请记下加密密钥；您必须为笔记本电脑或台式电脑上的每个无线网卡指定相同的密钥。

## 配置无线网络

在您的 Linux 笔记本电脑上，PCMCIA 或 PC 卡管理器识别无线网卡并为该卡加载适当的驱动程序。Linux 将无线网卡视为另一个以太网设备并为其分配设备名称，例如 `eth0` 或 `eth1`。如果笔记本电脑中已有以太网卡，该卡将获得 `eth0` 设备名称，而无线 PC 卡则成为 `eth1` 设备。

您确实需要配置某些参数以使无线网卡能够与无线接入点通信。例如，您必须指定分配给接入点的无线网络名称，并且加密设置必须与接入点上的设置匹配。通常，您可以使用适用于您的 Linux 发行版的图形网络配置工具来配置所有内容。只需选择适当的无线网络选项，然后逐步完成配置对话框，例如图 3–2 所示的对话框。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_203_0.png)

图 3-2：

新无线连接的配置信息。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_203_1.png)

### 技术细节

网络配置工具将您的无线网络设置保存到文本文件中。文本文件的名称取决于无线网络设备的名称。如果无线网络设备的名称是 `eth0`，则配置存储在文本文件 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中。如果无线设备名称是 `eth1`，则文件为 `/etc/sysconfig/network-scripts/ifcfg-eth1`。此配置文件包含无线网卡的各种设置。表 3-1 解释了设置的含义。以下是来自我笔记本电脑的 `/etc/sysconfig/network-scripts/ifcfg-eth1` 文件的略作修改版本：

```
IPV6INIT=no
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:8c:f9:c4
BOOTPROTO=dhcp
ONBOOT=no
DHCP_HOSTNAME=
NAME=
ESSID='HOME'
CHANNEL=6
MODE=Managed
RATE=auto
```

在某些 Linux 发行版中，加密密钥单独存储。对于设备名称为 `eth1` 的无线以太网卡，加密密钥存储在 `/etc/sysconfig/network-scripts/keys-eth1` 文件中。以下是我的示例中此文件的内容：

```
KEY=1fdf3fdefe
```

## 表 3-1 无线以太网网络接口配置文件的设置

| 参数 | 含义 |
|---|---|
| `BOOTPROTO` | 用于获取接口 IP 地址的协议名称。用于以太网接口的协议是 `dhcp` 或 `bootp`。 |
| `CHANNEL` | 信道号（在美国和加拿大之间为 1 到 14），必须与无线接入点设置的信道相同。在受管模式下，您无需指定信道。 |
| `DEVICE` | 无线以太网网络接口的设备名称（第一个接口为 `eth0`，第二个为 `eth1`，以此类推）。 |
| `ESSID` | 扩展服务集 (ESS) 标识符 (ID)，也称为无线网络名称。名称区分大小写，必须与为无线接入点指定的名称相同。请在单引号内提供名称（例如，'HOME'）。 |
| `HWADDR` | 无线网卡的硬件地址（也称为 MAC 地址）（六对用冒号分隔的十六进制数字，例如 00:02:2d:8c:f9:c4）。无线卡的设备驱动程序会自动检测此地址。 |
| `IPV6INIT` | 设置为 `yes` 时，为无线接口初始化 IPv6 配置。如果不使用 IPv6，请将其设置为 `no`。 |
| `MODE` | 无线网卡的操作模式。对于通过无线接入点连接的典型网络，请将其设置为 `Managed`。 |
| `NAME` | 无线网络的昵称。如果未指定它，则使用主机名作为昵称。 |
| `ONBOOT` | 设置为 `yes` 以在启动时激活无线接口；否则设置为 `no`。 |
| `PEERDNS` | 设置为 `yes` 以使接口修改系统的 `/etc/resolv.conf` 文件以使用从 DHCP 服务器获得的 DNS 服务器（与为接口提供 IP 地址的同一服务器）。如果将此参数设置为 `no`，则 `/etc/resolv.conf` 文件保持不变。 |
| `RATE` | 无线连接的比特率，设置为以下选项之一：`1M`、`2M`、`5.5M`、`11M` 或 `auto`。M 表示 Mbps，即每秒百万位。设置为 `auto` 以使用最大可能的传输速率。 |
| `TYPE` | 对于无线网络接口，设置为 `Wireless`。 |
| `USERCTL` | 设置为 `yes` 时，未以 root 登录的用户可以控制设备。将其设置为 `no` 以便只有 root 可以控制设备。 |

![](img/322157d1fa7d965f05bcd68ed0ffc36b_204_0.png)

密钥对于 40 位密钥（例如 1fdf-3fde-fe）有 10 个十六进制数字，或对于 104 位密钥有 26 个十六进制数字。密钥分别为 64 位和 128 位，但加密算法会自动生成密钥的 24 位，因此您只需指定剩余的位。密钥越长，加密越安全。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_205_0.png)

如果您手动编辑无线以太网配置文件中的参数，请在编辑配置文件后键入以下命令以重新激活无线网络接口：

```
/etc/init.d/network restart
```

![](img/322157d1fa7d965f05bcd68ed0ffc36b_205_1.png)

在 SUSE Linux 中，使用 YaST 配置无线网络。SUSE 将无线配置参数存储在以 `ifcfg-wlan` 开头的文件中，后跟 0 或 1 等数字，具体取决于无线网络接口的序列号。

配置文件存储在 `/etc/sysconfig/network` 目录中。以下是 SUSE Linux 中配置文件中的典型无线配置参数列表：

```
WIRELESS_MODE='Managed'
WIRELESS_ESSID='HOME'
WIRELESS_NICK=''
WIRELESS_RATE='auto'
WIRELESS_AUTH_MODE='open'
WIRELESS_KEY_0='0123-4567-89'
```

![](img/322157d1fa7d965f05bcd68ed0ffc36b_205_2.png)

要检查无线网络接口的状态，请键入以下命令：

```
iwconfig
```

以下是带有无线以太网 PC 卡的笔记本电脑的典型输出。（输出在其他 Linux 发行版中应相似。）

```
lo no wireless extensions.
eth0 no wireless extensions.
sit0 no wireless extensions.
eth1 IEEE 802.11b ESSID:"HOME" Nickname:"localhost.localdomain"
Mode:Managed Frequency:2.437 GHz Access Point: 00:30:AB:06:E2:5D
Bit Rate=11 Mb/s Sensitivity:1/3
Retry limit:4 RTS thr:off Fragment thr:off
Encryption key:1FDF-3FDE-FE Security mode:open
Power Management:off
Link Quality=51/92 Signal level=-40 dBm Noise level=-91 dBm
Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:27
Tx excessive retries:0 Invalid misc:0 Missed beacon:0
```

这里，`eth1` 接口指的是无线网卡。我编辑了加密密钥和其他一些参数以隐藏这些细节，但示例输出显示了无线链路正常工作时您通常会看到的内容。

## 本章内容

- 探索 TCP/IP 配置文件
- 检查 TCP/IP 网络连通性
- 在启动时配置网络

## 第 4 章

### 管理网络

与 Linux 中的几乎所有其他事物一样，设置传输控制协议/互联网协议（TCP/IP）是一项准备大量配置文件（可以用任何文本编辑器编辑的文本文件）的任务。这些配置文件中的大多数位于 `/etc` 目录中。Linux 安装程序试图通过填写值并避免您需要直接与每个 TCP/IP 配置文件交互来提供帮助。尽管如此，如果您知道文件的名称及其用途，手动编辑文件（如果必要）通常更容易。

### 发现 TCP/IP 配置文件
