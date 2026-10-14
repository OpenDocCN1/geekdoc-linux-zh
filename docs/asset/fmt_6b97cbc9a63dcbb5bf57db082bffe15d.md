
```
dpdk-devbind.py --bind=igb_uio eth1
```

将 `0000:01:00.0` 从任何驱动程序上解绑

```
dpdk-devbind.py -u 0000:01:00.0
```

将 `0000:02:00.0` 和 `0000:02:00.1` 绑定到 `ixgbe` 内核驱动

```
dpdk-devbind.py -b ixgbe 02:00.0 02:00.1
```

# DPDK 设备配置

`dpdk` 软件包提供了初始化脚本，可以简化设备分配和巨页（huge pages）的配置。它使得这些配置在重启后依然有效。

以下是文件 `/etc/dpdk/interfaces` 的一个示例，该配置了网卡的两个端口。一个使用 `uio_pci_generic`，另一个使用 `vfo-pci`。

```
# <bus> 目前支持 "pci"
# <id> 指定总线上的设备 ID
# <driver> 要重新绑定的驱动 (vfo-pci 或 uio_pci_generic)
#
# 注意，两个 DPDK 兼容的驱动 uio_pci_generic 和 vfo-pci
# 是 linux-image-extra-<VERSION> 软件包的一部分。
# 该包并不总是默认安装的 - 例如在云镜像中。
# 如果你遇到模块问题，请安装它。
# <bus> <id>
pci 0000:04:00.0 uio_pci_generic
pci 0000:04:00.1 vfo-pci
```

网卡通过其 PCI-ID 进行标识。如果你不确定，可以使用 `dpdk_nic_bind.py` 工具显示当前可用设备以及它们被分配的驱动。

```
dpdk_nic_bind.py --status
```

## 使用 DPDK 兼容驱动的网络设备

| PCI ID | 描述 | 接口 | 驱动 | 未使用 |
| :--- | :--- | :--- | :--- | :--- |
| 0000:04:00.0 | 'Ethernet Controller 10-Gigabit X540-AT2' | - | uio_pci_generic | ixgbe |
| 0000:02:00.0 | 'Xtreme BCM5719 Gigabit Ethernet PCIe' | eth0 | tg3 | uio_pci_generic *Active* |
| 0000:02:00.1 | 'Xtreme BCM5719 Gigabit Ethernet PCIe' | eth1 | tg3 | uio_pci_generic |
| 0000:02:00.2 | 'Xtreme BCM5719 Gigabit Ethernet PCIe' | eth2 | tg3 | uio_pci_generic |
| 0000:02:00.3 | 'Xtreme BCM5719 Gigabit Ethernet PCIe' | eth3 | tg3 | uio_pci_generic |
| 0000:04:00.1 | 'Ethernet Controller 10-Gigabit X540-AT2' | eth5 | ixgbe | uio_pci_generic |

## 使用内核驱动的网络设备

## 其他网络设备

<none>

# DPDK 巨页配置

DPDK 大量使用巨页来消除对 TLB 的压力。因此，必须在你的系统中配置巨页。

`dpdk` 软件包包含一个配置文件和脚本，尝试以 `/etc/dpdk/dpdk.conf` 的形式简化 DPDK 的巨页配置。如果你的系统中还有除 DPDK 之外的巨页，或者你对巨页的设置有非常特殊的要求，你可能想要自己分配/控制。如果是这样，对于满足你的需求配置 DPDK 可能不是一个很好的简化方法。

这里是配置 1024 个 2M 页和 4G 页的示例。

```
NR_2M_PAGES=1024
NR_1G_PAGES=4
```

如所示，它支持配置 2M 和更大的 1G 巨页（或两者的混合）。它将确保无论你的默认页大小如何，都能找到适当的 `hugetlbfspoints`。配置文件本身包含了边缘情况的详细信息，以及关于如何通过内核参数手动分配巨页的提示。

这取决于你的需求，你想要哪种 - 1G 页在减轻 TLB 压力方面更有效。但有报告称在 DPDK 内存分配内部存在碎片。在系统生命周期的后期，获取足够的空间来设置数量的 1G 页可能更加困难。

# 编译 DPDK 应用程序

目前还没有稳定且发布的 DPDK 库的消费者。OpenSwitch-DPDK 是一个例外（见下文），并且越来越多的项目正在出现。但通常情况下，你可能仍然想要针对该库进行编译。

你会发现一些指南，告诉你获取 DPDK 源码，根据你的需求进行构建，并最终通过为构建系统设置 `RTE_*` 值来基于 DPDK 构建你的应用程序。由于 Ubuntu 已经为你提供了已经编译好的 `pkg-DPDK`，我们可以跳过所有这些。

DPDK 提供了一个有效的 `pkg-config` 文件来简化变量和选项的设置。

```
sudo apt-get install dpdk-dev libdpdk-dev
gcc testdpdk $(pkg-config --cflags --libs libdpdk) -o testdpdk
```

# 优化 OpenvswitchDPDK

DPDK 有许多选项 - 与 Openvswitch-DPDK 结合使用时常用的两个是：

`ovs-vsctl set Open_vSwitch . other_config:n-dpdk-rxqs=2`

`ovs-vsctl set Open_vSwitch . other_config:pmd-cpu-mask=0x6`

第一个控制每个 DPDK 接口使用多少个接收队列（rx queues），而第二个控制在何时以及何运行 PMD 线程。上面的示例将利用两个接收队列，并在 CPU 1 和 2 上运行 PMD 线程。更多信息请参考本文末尾的“EAL 命令行选项”和“Openvswitch DPDK 安装”链接。

与调优一样，你必须非常熟悉你的系统和负载——因此请通过与你的实际用例匹配的负载来验证任何调优。

# 支持与故障排除

DPDK 是一个快速发展的项目。在任何寻求支持和进一步指南的情况下，强烈建议首先检查这些内容是否适用于当前版本。

在以下位置检查是否为已知问题：

- DPDK 邮件列表 (Mailing Lists)
- Openvswitch-DPDK 的 OpenStack 邮件列表
- DPDK Launchpad 区域中的已知问题
- 加入 freedom 上的 IRC 频道 `#DPDK` 或 `#openvswitch`。

问题通常由于通用设置中缺少细小的细节。随后，这些缺失的细节会导致问题，且难以追溯到根源。一个常见的情况似乎是“无法打开网络设备 dpd0 (No such device)”问题。这在带有 DPDK 的 Open vSwitch 中设置端口时发生得很晚。根源大多数时候在设置和初始化的早期。这里有一个设备正确初始化的示例——你可以在启用 DPDK 启动 Open vSwitch 的 syslog/journal 中找到。

```
ovs-vsctl [3560]: EAL: PCI device 0000:04:00.01 on NUMA socket 0
ovs-vsctl [3560]: EAL: probe driver: 8056:1528 rte_igbe_pmd
ovs-vsctl [3560]: EAL: PCI memory mapped at 0x7f2140000000
ovs-vsctl [3560]: EAL: PCI memory mapped at 0x7f2140200000
```

如果由于网卡、初始化失败或其他原因出现此问题，稍后将没有可以引用的 DPDK 设备。遗憾的是，负载分布在 syslog/journal 和 openvswitch 日志中。为了方便在此检查，以下是这些日志中可以找到内容的示例，与输入的命令相关。

```
#Note：此日志是使用 dpdk 2.2 和 openvswitch 2.5 记录的，但现在看起来仍然非常相似（内容稍微扩展了一些）
```

图例说明：

CMD: 你输入的的命令

SYSLOG:（包含 EAL OVS 消息）

OVS-LOG:（Openvswitch 消息）

```
#准备
将接口绑定到 DPDK UIO 驱动，使大页（Hugepages）可用，在 OVS 上启用 DPDK
```

CMD: sudo service openvswitch-restart

# SYSLOG:

2016–01–22T08:58.31.372Z|00003|daemon_unix(monitor)|INFO|pid 3329 died, killed (Terminated), exiting
