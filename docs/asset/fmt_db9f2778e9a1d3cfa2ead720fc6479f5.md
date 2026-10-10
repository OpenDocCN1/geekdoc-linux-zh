
172.17.2.4 AND 255.255.255.0 = 172.17.2.0

172.17.2.6 AND 255.255.255.0 = 172.17.2.0

由于结果相同，因此不需要路由。相反，如果我们从 172.17.2.4 到 172.17.6.6 执行相同操作，我们将看到通过 172.17.2.1 进行路由，并发生接口切换（`eth0` 切换到 `fdd0`）到达 172.17.1.1，然后从这里 172.17.1.2 再次发生接口切换（`fdd0` 切换到 `eth0`）到达 172.17.6.6。当没有任何规则匹配时，将使用默认路由。如果两条规则都匹配，将使用匹配最精确的路由（换句话说，就是零最少的）。为了构建路由表，我们可以在机器设置期间使用 `route` 命令；然而，如果需要使用更复杂的规则（自动路由），我们可以使用路由信息协议 (RIP) 命令，或者在独立系统之间使用外部网关协议 (EGP) 或边界网关协议 (BGP) 命令。这些协议通过 `gated` 命令实现。

为了在现有网络上安装机器，需要从网络提供商或管理员处获取信息：节点 IP 地址、网络 IP 地址、广播地址、子网掩码地址、路由器地址和 DNS 地址。

如果我们设置一个永远不会连接互联网的网络，我们可以选择任何的地址，但建议保持与所需网络大小相应的适当顺序，以避免该网络内部出现管理问题。我们现在知道如何定义私有网络的网络和节点了（我们必须小心，因为如果机器连接到网络，我们可能会给已分配该地址的用户带来不便）：节点地址 192.168.110.23，掩码 255.255.255.0，不是地址 192.168.110.0；节点部分 .23，网络地址 192.168.110.0，广播地址 192.168.110.255。

## 4. 如何配置网络

### 4.1. 网络接口适配器 (NIC) 配置

一旦 GNU/Linux 内核加载，它会执行 `init` 命令，该命令反过来读取配置文件 `/etc/init.ab` 并开始启动过程。通常，initab 包含如 `/etc/init.d/network` 之类的条目，它启动网络服务。在 Debian 中，配置位于 `/etc/network/interfaces`。

为了配置网络，我们可以使用以下命令：

- `ifup`: 启动网络接口
- `ifdown`: 停止网络接口
- `ifconfig`: 手动配置接口参数

例如，配置静态 IP 地址：

```
eth0 inet static

address 192.168.110.23

netmask 255.255.255.0

gateway 192.168.110.1
```

如果我们想通过 DHCP 自动获取 IP 地址，我们使用：

```
eth0 inet dhcp
```

配置接口后，我们可以使用 `ping` 命令测试连通性：

```
ping 192.168.110.1
```

#### 4.1.1. Fedora 风格的网络配置

Red Hat 和 Fedora 使用不同的网络配置结构：`/etc/sysconfig/network`。例如，配置静态网络：

| 键名 | 描述 |
| :--- | :--- |
| NETWORKING=yes | 由 `cmd hostname` 定义的主机名 |
| HOSTNAME=my-hostname | 对于 NAT 防火墙网关和路由器为真 |
| FORWARD_IPV4=true | 其他任何情况为假 |
| GATEWAY="XXX,XXX,XXX.YYY" | 指向互联网的网关 |

要配置 DHCP，必须删除 `GATEWAY` 行，因为它将由服务器分配。如果要整合 NIS，必须有一行包含服务器域名的行：`NISDOMAIN=NISProject1`

配置接口 `eth0`：

```
/etc/sysconfig/network-scripts/ifcfg-eth0:

DEVICE=eth0

BOOTPROTO=static

BROADCAST=XXX.XXX.XXX.255

IPADDR=XXX.XXX.XXX.XXX

NETMASK=255.255.255.0

NETWORK=XXX.XXX.XXX.0

ONBOOT=yes 启动时激活网络。
```

从 FC3 开始，还可以添加：
`TYPE=Ethernet`
`HWADDR=XX:XX:XX:XX:XX:XX`
`GATEWAY=XXX.XXX.XXX`
`IPV6INIT=no`
`USERCTL=no`
`PEERDNS=yes`

或者，使用 DHCP 配置：

```
DEVICE=eth0

ONBOOT=yes

BOOTPROTO=dhcp
```

要禁用 DHCP，将 `BOOTPROTO=dhcp` 更改为 `BOOTPROTO=none`。这些文件中的任何更改都必须通过 `service network restart`（或 `/etc/init.d/network restart`）重启服务来实现。

更改主机名必须采取以下三个步骤：

1) 执行命令 `hostname new-name`。
2) 在 `/etc/sysconfig/network` 中修改网络配置，编辑 `HOSTNAME=new-name`。
3) 恢复所有服务（或重启）：
    - `service network restart`（或执行 `/etc/init.d/network restart`）
    - 通过在控制台模式粘贴 `init 3` 并切换到 GUI 模式 `init 5` 来重启桌面。

验证名称是否未在 `/etc/hosts` 中注册。主机名可以在执行期间通过 `sysctl -w kernel.hostname="newname"` 进行更改。

#### 4.1.2. Wi-Fi（无线）网络配置

为了配置 Wi-Fi 接口，我们基本上使用 `wireless-tools` 软件包（以及 `ifconfig` 或 `ip2`）。该包使用 `iwconfig` 命令来配置无线接口，但也可以在 `/etc/network/interfaces` 中进行。

示例：在 Debian (Etch) 中配置 WiFi（与 FC6 类似）

假设我们正在使用 Intel/Wireless2200b 网卡（许多笔记本电脑中都有此型号，如 Dell、HP...）。控制网卡的软件分为两部分：通过 `modprobe` 命令加载到内核中的软件模块，以及加载到网卡中并可由制造商更新的固件（请参阅该型号的网站）。由于我们讨论的是模块，因此使用 Debian 模块化包很重要，它允许我们轻松地创建和安装模块（另一个选项是安装相应的模块）。我们可以创建并安装软件（可以在制造商网站上找到），并使用 `module-assistant` 包中的 `mod` 命令调用它。

```
apt-get install module-assistant (安装软件包)

mod -a -f get ipw200

mod -a -t - ipw200

mod -a -t install ipw200
```

我们可以从制造商提供的网站（在产品文档中）下载固件版本以及我们需要的驱动程序，在我们的案例中将是驱动版本 1.8 和固件版本 2.0.4，从以下地址获取：

`http://ipw2000.sourceforge.net/firmware.php`

然后我们应该压缩并安装固件：

此复制将创建三个包（`ipw2200-bsf`、`ipw2200-ibs` 和 `ipw2200-sniffer-fw`）。通过 `modprobe ipw2200` 加载模块，系统重启，然后从控制台执行 `dmesg | grep ipw` 命令，这将显示与下面类似的行，指示模块正在加载（可以使用 `lsmod` 检查）。

```
ipw2200: Intel(R) PRO/Wireless 2200/2915 Network Driver, gti.0.8

ipw2200: Detected Intel PRO/Wireless 2200BG Network Connection
```

然后我们应该下载包含 `iwconfig` 的无线工具包以通过 `apt` 安装无线工具以及许多其他工具，如果我们执行 `iwconfig`，将出现类似以下的内容：

```
ethl1 IEEE 802.11 SSID:"Name-of-the-Wifi"

Managed Frequency:2.437 GHz

Access Point:00:0E:3E:34:C8:72

Bit Rate=11 Mb/s TxPower=20 dB

Security mode:open
```

我们必须配置网络文件，例如 `gedit /etc/network/interfaces`，并带有 eth1 接口，例如：

```
iface eth1 inet dhcp

pre-up iwconfig eth "Name of the Wifi"
```
