
![](img/1744bde8c889adfab3fc911e1687fecf_651_0.png)

**图 15-12：** Orinoco Silver 无线局域网（WLAN）卡片可以配合 PCI 适配器使用（如图所示）。

## 检查卡片是否正常工作

如果模块已正确加载，cardmgr 应该会识别每个卡片并启动其以太网接口。要检查是否已发生此情况，请重新启动接口，步骤如下：

```bash
# /etc/init.d/pcmcia restart
Shutting down PCMCIA services: cardmgr modules.
Starting PCMCIA services: modules cardmgr.
```

检查 `/var/log/messages` 文件。你应该能在该文件的末尾附近看到一些消息，描述了 PCMCIA 接口关闭和重启时发生的情况。如果卡片启动成功，这些消息将提供大量信息，例如卡片的 MAC 地址、可用信道列表以及与卡片关联的接口名称。以下是一些示例：

```text
May 4 10:21:12 nsl kernel: PCI: Enabling device 01:09.0 (0000 -> 0002)
May 4 10:21:12 nsl kernel: PCI: Assigned IRQ 5 for device 01:09.0
May 4 10:21:12 nsl kernel: PCI: Sharing IRQ 5 with 00:1f.3
May 4 10:21:12 nsl kernel: Yenta IRQ list 0000, PCI irq5
May 4 10:21:12 nsl kernel: Socket status: 10000011
...
May 4 10:21:23 nsl cardmgr[1935]: starting, version is 3.1.22
May 4 10:21:23 nsl cardmgr[1935]: initializing socket 0
May 4 10:21:23 nsl kernel: cs: memory probe 0xa0000000-0xa0ffffff: clean
May 4 10:21:23 nsl cardmgr[1935]: socket 0: Lucent Technologies
WaveLAN/IEEE Adapter
May 4 10:21:23 nsl cardmgr[1935]: executing: 'modprobe orinoco_cs'
May 4 10:21:23 nsl cardmgr[1935]: executing: './network start eth1'
May 4 10:21:23 nsl /etc/hotplug/net.agent: invoke ifup eth1
```

上述代码显示内核识别了 PCI 卡片（位于 IRQ 5）。cardmgr 将 Orinoco 卡片识别为插槽 0 中的 WaveLAN/IEEE 适配器。网络脚本启动了一个以太网接口（eth1）。

如果无线局域网接口启动正常，你应该能够使用 `iwconfig` 命令看到新的接口。以下是 `iwconfig` 命令输出示例：

```text
io        no wireless extensions.

eth0      no wireless extensions.

eth1      IEEE 802.11-DS  ESSID:"Wavelan Network"  Nickname:"a.abc.com"
          Mode:Ad-Hoc  Frequency:2.457GHz  Cell: 02:02:2D:2E:8C:A8
          Bit Rate:2Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
          Retry limit:4  RTS thr:off  Fragment thr:off
          Encryption key:7365-6375-31
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

如果你的无线局域网接口似乎无法正常工作，请参阅本章后面的“排查无线局域网故障”部分。如果接口似乎工作正常，你就准备好调整无线局域网卡片接口并设置 TCP/IP 以使用该接口了。

# 配置无线接口

> **注意：** Red Hat Linux 7.3 在最后一刻从“网络配置”窗口中移除了对无线局域网卡片的显式支持。本节中的步骤描述了如何手动配置无线卡片。结果是一个无线配置文件，类似于由“网络配置”窗口生成的文件。

检测到无线卡片后，会在你的 `/etc/sysconfig/network-scripts` 目录中创建一个接口配置文件。配置文件的名称为 `ifcfg-` 后跟接口名称（如 eth0、eth1 等）。因此，如果你的无线卡片提供的是你唯一的网络接口，它将被称为 `ifcfg-eth0`。

使用任何文本编辑器以 root 用户身份打开 `ifcfg-eth?` 文件。以下是一个 `ifcfg-eth1` 文件的示例：

```text
USERCTL=no
HWADDR=00:02:2d:2e:8c:a8
BOOTPROTO=none
ONBOOT='yes'
DEVICE=eth1
TYPE=Ethernet
NETMASK='255.255.255.0'
IPADDR='10.0.1.1'
BROADCAST='255.255.255.255'
GATEWAY='10.0.1.2'
```

在这个示例中，无线卡片的硬件（MAC）地址自动设置为 00:02:2d:2e:8c:a8。接口设置为在启动时开启（ONBOOT='yes'）。你的 MAC 地址会不同。接口设备是 eth1（这与接口文件名 ifcfg-eth1 相匹配），因为计算机在 eth0 接口上还有另一个以太网卡片。接口类型设置为 Ethernet。

文件中的其他信息设置了标准的 TCP/IP 地址信息。NETMASK 设置为 255.255.255.0，卡片的 IP 地址设置为 10.0.1.1。广播地址是 255.255.255.255。在这种情况下，计算机使用无线网络上的另一台计算机（10.0.1.2）作为通往互联网的网关。

你还可以通过此文件设置许多特定于你无线网络的选项。以下是一些你可能想要设置的选项列表：

- **ESSID** — 用于标识属于同一网络的小区（cell）的网络名称（或网络 ID）。如果你有一组小区（可能包括客户端可以漫游的多个节点和中继器），此名称可以标识所有这些小区隶属于同一个虚拟网络。选择任何你喜欢的名称，然后将该名称用于虚拟网络中的所有计算机。（ESSID 代表扩展服务集标识符 Extended Service Set ID。）
- **MODE** — 指示无线局域网卡片的工作模式。因为我只设置了一个由一个小区组成的无线局域网（换句话说，没有在其他区域设置可漫游的小区），所以我可以将模式设置为 Ad hoc（临时对等）或简单地保留为 Auto（自动）。Ad hoc 模式允许卡片直接与其每个对等方通信。如果你有多个小区，需要你的卡片直接与访问点通信，可以使用 Managed（管理）模式。对于点对点网络（例如使用无线局域网将网络从一栋楼扩展到另一栋楼）也可以使用 Managed 模式。
- **NWID** — 标识网络上此特定计算机的名称。如果你不使用 NWID 设置，则默认使用计算机的主机名（由 uname -n 命令确定）。
- **FREQ** — 你可以选择传输的特定频率。由于选择信道意味着某种频率，因此不需要输入值。如果你确实输入了频率，该值必须是一个数字，后跟 k（千赫兹）、M（兆赫兹）或 G（吉赫兹）。你所选信道的默认值范围从 2.412G（信道 1）到 2.484G（信道 14），其他信道以 .005G 的增量出现。默认值是 2.422G。
- **CHANNEL** — 选择 1 到 14 之间的信道。你可以从信道 1 开始，如果在该信道上受到干扰，请尝试更改为其他信道。
- **SENS** — 你可以选择接入点的灵敏度级别。SENS 可以设置为 1（低密度）、2（中密度）、3（高密度）。默认值为 1。灵敏度阈值会影响漫游。
- **RATE** — 从以下速率中选择传输速率：11M、5.5M、2M、1M 或 auto（自动）。选择 auto（默认值）允许接口根据需要自动降低速度。较低的速度允许接口在更远的距离上传输并处理嘈杂的信道。
- **KEY** — 所有相互通信的无线局域网卡片都需要相同的加密密钥。正确获取此值至关重要。此密钥用于加密所有传输的数据并解密无线接口上接收的所有数据。虽然你可以保留默认密钥，但你可以通过选择一个新密钥并输入到网络上每台无线计算机的卡片上来确保更高的安全性。你可以输入数字（最多 10 位）作为 XXXXXXXXXXXX 或 XXXX-XXXX-XX（其中每个 X 都是数字）。你也可以输入少于 10 位数字。例如，输入 99 将导致数字 9900-0000-00。

> **注意：** 802.11 网络使用的加密算法是有线等效保密（Wired Equivalent Privacy, WEP）算法。虽然使用加密密钥比不使用更安全，但一些专家认为 WEP 存在一些固有的缺陷，可能允许路过的黑客解密你的无线局域网流量。因此，我强烈建议使用额外技术来保护你的无线局域网，如防火墙和严格的日志检查。有关更多信息，请参阅无线安全侧边栏。

除了上述选项外，你还可以向 `iwconfig` 命令（实际上由该命令解释这些值）传递任何有效的选项，只需在配置文件中添加 IWCONFIG 选项即可。显示 `iwconfig` 手册页（`man iwconfig`）以查看所有无线选项。此外，查看 `/etc/sysconfig/network-scripts/ifup-wireless` 脚本以了解你刚刚添加的选项是如何被处理的。

> **注：** 在作为你的互联网连接网关的计算机上，你需要开启 IP 数据包转发。在 `/etc/sysctl.conf` 文件中将 `net.ipv4.ip_forward` 的值更改为 1。以 root 用户身份使用任何文本编辑器打开该文件，并更改该行如下：
> `net.ipv4.ip_forward = 1`

对局域网上的每台运行 Red Hat Linux 的无线计算机重复此操作。此时，你的无线网络应该已准备就绪。按照以下步骤重启你的网络，以确保其正常工作。

# 重启无线接口

为了使你刚刚输入的信息对无线卡片生效，只需重启 Linux 计算机上的 PCMCIA 接口即可。然后，你可以使用标准的 TCP/IP 工具（如 `ping` 命令）测试两台无线计算机之间是否可以通信。

要重启无线接口，请在每台无线计算机的终端窗口中以 root 用户身份输入以下内容：

