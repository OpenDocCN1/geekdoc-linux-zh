
在这种情况下，映射不会被使用，因为 `"eth0-uni"` 没有被 `"eth0"` 文件通配符匹配；相反，使用模式如 `"eth0"` 模式的映射会导致映射被应用。另一种禁用映射的方法是通过对 `ifup` 使用 `--mappings` 命令行选项。

示例 `/etc/network/interfaces34` 包含了许多有趣的映射示例，包括一个如何将 PCMCIA 方案与 `ifupdown` 集成的示例。

## 处理热插拔网络设备

正如我们在 6.5.1 节中所示，Debian 使用 `hotplug` 处理热插拔硬件，包括位于 PCMC 和 USB 等热插拔总线的网络设备。当用户将网络设备连接到机器时，内核最终请求 `hotplug` 执行 `/etc/hotplug/net.agent`，该程序负责配置设备。

默认情况下，Debian 的 `hotplug` 在 `/etc/network/interfaces` 中标记为 `auto` 的接口可用时会配置它们，并在移除时取消配置。这种行为受所谓的网络代理策略控制，该策略可以在 `/etc/default/hotplug` 中配置或通过 `dpkg-reconfigure hotplug` 配置。策略如下：

- `all`

- 如果新的网络接口可以使用 `ifupdown` 配置，`hotplug` 会相应调用 `ifup` 和 `ifdown`。

- `auto`

- 仅自动处理 `/etc/network/interfaces` 中 `auto` 语句块中提到的网络接口。这产生了一个轻微的问题，因为热插拔接口在初始化期间可能不可用，且当 `/etc/rc.d/S40network` 尝试启动所有自动接口时，会发生错误。同样，调用 `ifup -a` 也会失败，尽管它可能成功配置了可用的网络接口。这是默认策略。

> 34 `/usr/doc/ifupdown/examples/network-interfaces.gz`

## hotplug

为了解决后一个问题，可以使用 `ifupdown` 配置接口，使其被 `hotplug` 自动使用，但又不在 `ifupdown` `auto` 语句块的意义上使其自动化。由于 `ifupdown` 并不知道 `hotplug`，而是使用接口映射。如果 `eth0` 出现，且 `hotplug` 网络代理策略生效，将告诉 `ifupdown` 处理 `eth0-hotplug` 而不是普通接口。使用 `grep` 和 `map` 参数，可以选择性将单个接口标记为可热插拔的：

```
# cat /etc/network/interfaces

[...]

mapping hotplug

script grep

map aero0

map prism0

iface aero0 inet dhcp

iface prism0 inet dhcp
```

当 `aero0` 或 `prism0` 可用时，`ifupdown` 使用 DHCP 配置它们。如果 `eth0` 出现，且策略生效，告诉 `ifupdown` 处理 `eth0-hotplug` 而不是普通接口。使用 `grep` 和 `map` 参数，可以选择性将单个接口标记为可热插拔的：

```
# cat /etc/network/interfaces

[...]
```

当 `aero0` 或 `prism0` 可用时，`ifupdown` 使用 DHCP 配置它们。如果 `eth0` 出现，且策略生效，告诉 `ifupdown` 处理 `eth0-hotplug` 而不是普通接口。我们可以通过直接调用来说明这一点：

```
# ifup eth0=hotplug

Ignoring unknown interface eth0=eth0.
```

显然，`all` 策略等于使用 `grep` 作为映射脚本。

## 重命名网络设备

如果你使用 Linux 有了一段时间，或者你拥有一带有热插拔设备的机器，你可能很熟悉这个故事：新内核或不同的插入顺序导致原来的 `eth0` 变成了 `eth1`，而 `eth1` 现在变成了 `eth0`；这很不方便。

该包提供了一个工具，可以根据静态数据（如 MAC 地址或总线位置）在接口启动之前自动重命名接口。此功能对于热插拔设备最有用，它与 `hotplug` 系统自动集成。例如，为了确保显示 MAC 地址的 PCMCIA 被命名为 `lan`，`/etc/iptables` 中的以下行会导致 `ifname` 在下次插入时执行更改：

```
echo lan mac 00:00:de:ad:ef >> /etc/iptables
```

一旦接口被重命名

```
# ifconfig

[...] lan encap Ethernet Hwaddr 00:00:de:ad:ef

[...]

# ifconfig eth0

eth0: error fetching information: Device not found
```

配置完成后，你可以确定显示 MAC 地址的网络设备将始终被命名为 `lan`，这应该让你的网络配置在接口名称方面更加健壮。

应该提到的是，`udev`（见第 6.5.1 节）也可以重命名接口，并配合 `ifname` 完成。以下 `udev` 规则与 `/etc/iptables` 中的上述条目相同：

```
# grep /etc/udev/rules.d/local-netifaces

KERNEL="eth*", SYSFS(address)="00:00:de:ad:ef", NAME="lan"
```

`udev` 只能在使用 2.6 内核的系统上重命名接口。在较旧内核上，必须使用 `ifname`。遗憾的是，为了重命名非热插拔接口，必须在配置接口之前进行。`ifname` 文档包含一个针对 `/etc/init.d/networking` 的补丁以恰好实现这一点³⁵。

## 自动位置检测与配置

如果你在网络之间穿梭，你可能不喜欢不断重新配置网络设备。接口映射极大促进了这一工作，通过适当脚本根据当地情况将接口映射到配置语句块，你可以让 `ifupdown` 确定要使用的配置并自动配置你的网络。

> ³⁵ 见 `/usr/share/doc/ifname/HOTPLUG.txt`.

`guessnet` 软件包提供了一个可以与 `ifupdown` 无缝集成的工具。通过在 `iface` 语句块中使用映射（`mappings`）和额外参数，它允许运行许多测试，并使用指定该测试返回成功的配置语句块。以下示例使用地址解析协议 (`ARP`) 来检查网络上具有指定 IP/MAC 地址组合的主机是否可访问，并据此配置接口。如果在 5 秒后仍未找到此类主机，`ifupdown` 将改用 DHCP 。。如果 `guessnet` 认为未连接网线，则接口将不会启动。注意，`guessnet` 使用 `map` 参数将选项传递给脚本。

```bash
# cat /etc/network/interfaces

mapping eth0

script guessnet-ifupdown

map default: dhcp

niface disconnected inet manual

pre-up false

test missing-cable

iface uni inet static

address 172.19.23.14

netmask 255.255.248.0

gateway 172.19.16.1

test peer address 172.19.16.1 mac 00:2d:2c:33:fe:le

iface dhcp inet dhcp
```

除了 ARP，`guessnet` 还允许搜索运行标准命令或脚本作为测试。进一步的测试包括搜索 PPPoE 汇聚器和无线接入点，尽管这些测试仍处于实验阶段。当定义了多个接口时，可以限制每个接口的测试。遗憾的是，这种限制在映射语句中的指定方式并不直观。可以使用通配符或类似的符号。以下将将工作配置限制为 `eth0`，将家庭配置限制为 `eth1`。`dhcp` 配置均适用于两者（且必须显式指定）：

```bash
# cat /etc/network/interfaces

mapping eth0

script guessnet-ifupdown

map default: dhcp

map work dhcp

mapping eth1

script guessnet-ifupdown

map default: dhcp

map home dhcp
```
