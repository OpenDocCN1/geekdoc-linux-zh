
# 在启动时设置网卡

Linux 开源软件（FOSS）世界中管理网络解决方案领域充满了各种网络管理器的躯壳——换句话说，许多工具已来又去。目前的方法包括 `NetworkManager`、`systemd-network`、老式的脚本，以及作为任何其他工具的包装器的混合解决方案！Linux 发行版在自动化和维护网络配置方面采用了略有不同的方法。我们将在下一节中介绍 RedHat 系发行版（Fedora、CentOS 等）和类 Debian 发行版（Ubuntu、Mint 等）的细节。对于其他发行版，你需要通过两种方式之一来处理此过程：

- 使用带的网络管理工具来管理网络设置。这可能是最简单且可靠的方法。
- 使用负责配置网卡的启动脚本。在脚本末尾添加必要的 `ifconfig`、`ip` 或 `nmcli` 语句。另一个放置命令的地方是 `rc.local` 脚本或等效脚本——不漂亮，但有效！

## 在 Fedora、CentOS 和 RHEL 下设置 NIC

Fedora 和其他 Red Hat 类型版本倾向于使用 `NetworkManager` (NM) 在启动时配置网卡。幸运的是，使用 NM 为这些系统上的旧网络配置管理方法提供了后兼容性。旧方法本质涉及在 `/etc/sysconfig/network-scripts` 目录下创建启动时读取的文件。NM 现在可以透明地管理和创建这些文件。

对于每个网络接口，在 `/etc/sysconfig/network-scripts` 目录下都有一个 `ifcfg` 文件。该文件名以设备名称或 NetworkManager 连接/配置文件的名称结尾；因此，`ifcfg-eth0` eth0 设备，`ifcfg-eth1` 对应 eth1 设备，以此此类推。

以下是在操作系统安装期间，使用动态主机配置协议（DHCP）自动配置的网络接口的 `ifcfg-eth0` 配置片段：

```
TYPE=Ethernet

BOOTPROTO="dhcp"

DEFROUTE="yes"

IPV6INIT="yes"

IPV6_AUTONCF="yes"

IPV6_DEFROUTE="yes"

NAME="eth0"

UUID="28792a9c-57e2-4b76-9be9-21a58699976b"

ONBOOT="yes"
```

如果你在操作系统安装期间选择为 eth1 接口静态配置 IP 地址信息，那么相应的配置文件 `ifcfg-eth1` 可能会如下所示：

```
TYPE=Ethernet

ONBOOT=yes

BOOTPROTO=none

NAME=eth1

IPADDR=10.72.72.72

PREFIX=24

IPV6ADDR=2002:db8::1/64
```

这些字段决定了用于示例 eth1 设备的 IP 配置信息。

注意，某些值对应于 `nmcli` 调用中使用的参数。

要更改设备的配置信息，你可以直接修改相应的文本配置文件 `ifcfg*`，或者使用 `nmcli` 命令（或更高层的 GUI 工具）配合适当的选项来更新或创建文件。

在进行任何网络配置更改后，你可以快速运行以下命令序列来关闭并恢复你的接口：

```
master@fedora-server /$ sudo sudo ifdown eth0
master@fedora-server /$ sudo nm ifup eth0
```

使用 `nmcli` 关闭并启动接口的后续操作如下：

```
master@fedora-server /$ sudo nmcli device disconnect eth0
master@fedora-server /$ sudo nmcli device connect eth0
```

> 提示：在类 Red Hat 发行版中，文件 `/usr/share/doc/initscripts/sysconfig.txt` 提供了关于 `/etc/sysconfig/` 中使用的各种配置文件的信息。例如，它显示了可以在不同的 `/etc/sysconfig/network-scripts/ifcfg-*` 配置文件中使用的选项和变量。

### 第三部分 网络与安全

如果你需要配置第二个网络网卡（例如，ens3），你可以通过复制并重命名现有的 `ifcfg-eth0` 文件为 `ifcfg-ens3` 来使用 `ifcfg-eth0` 文件中的语法，并更改新 `ifcfg-ens3` 文件中的信息以反映第二个网卡的信息。在执行此同时，你必须确保新文件中的 `HWADDR` 变量（介质访问控制，MAC 地址）反映了你尝试配置的实际物理网络设备的 MAC 地址。一旦新的 `ifcfg-ens3` 文件存在，Fedora 将在下次启动或下次重启网络时自动查询该文件以配置设备。

你也可以重启 NetworkManager 服务来使你的更改生效，如下：

```
master@fedora-server: sudo systemctl restart NetworkManager
```

## 在类 Debian 系统下设置 NIC（Ubuntu, Kubuntu, Mint 等）

基于 Debian 的系统（如 Ubuntu）使用不同的机制来管理配置。传统上，网络配置是通过 `/etc/network/interfaces` 文件完成的。我们说“传统上”是因为较新的 Ubuntu 发行版（18.04 及更高版本）正在标准化 netplan（后文将讨论）来配置网络。

`/etc/network/interfaces` 文件的格式简单且有详尽的文档。接下来讨论示例 interfaces 文件中的条目（注意为了可读性添加了行号）：

- 1. # 回环网络接口
- 2. auto lo
- 3. iface lo inet loopback
- 4. 
- 5. # 第一个网络接口 eth0
- 6. auto eth0
- 7. iface eth0 inet static
- 8. address 192.168.1.45
- 9. netmask 255.255.255.0
- 10. gateway 192.168.1.1
- 11. 
- 12. # 第二个网络接口 ens5
- 13. auto ens5
- 14. iface ens5 inet dhcp
- 15. iface ens5 inet6 static
- 16. 
- 17. address 2001:DB8::3
- netmask 64

- 第 1 行：任何以井号 (`#`) 开头的行都是注释并会被忽略。空行也是如此。
- 第 2 行：以单词 `auto` 开头的行用于标识在执行 `ifup` 命令时（例如在系统启动或运行网络控制脚本时）需要启动的物理接口。在此情况下，`lo` 指的是回环设备。可以在同一段落的后续行中提供额外的选项。可用选项取决于族和方法。
- 第 7 行：`iface` 指令定义了正在处理的接口名称。在此情况下，它是 eth0 接口。示例中的 `iface` 支持 `inet` 方法。
- 第 8-10 行：`iface` 指令定义了正在处理的接口名称。在此情况下，它是 eth0 接口。示例中的 `iface` 支持 `inet` 方法。
- 第 12-14 行：`iface` 指令定义了正在处理的接口名称。在此情况下，它是 eth0 接口。示例中的 `iface` 支持 `inet` 方法。
- 第 15-17 行：`iface` 指令定义了正在处理的接口名称。在此情况下，它是 eth0 接口。示例中的 `iface` 支持 `inet` 方法。

# 第 13 章 网络配置

执行各种操作并学习不同子系统的语法和细微差别。`netplan` 是解决这些问题的最新尝试。`netplan` 背后的理念简单得具有欺骗性：它使用基础的 YAML（一种不是标记的语言）配置文件来“统领一切”。在这种情况下，“所有”指的是 NM、`systemd-network` 以及未来可能提供的其他网络管理器。在 netplan 中，网络管理器被称为渲染器（renderer）。`netplan` 配置文件（或多个文件）类似于类型清单（manifest），供“其他”系统（渲染器）查询，并据此创建它们原生的网络配置。`netplan` 目前在类 Debian 派发行版中被广泛采用。让我们快速回顾如何使用 netplan 为基于 Ubuntu 的服务器设置静态 IP 地址。

检查系统上是否安装了 netplan 软件包：

```bash
[master@ubuntu-server ~]$ hash netplan 2> /dev/null || echo "Netplan is NOT installed"
```

如果之前的命令显示“Netplan is NOT installed”，您可以通过输入以下命令在基于 Debian 的服务器上安装 netplan 软件包：

```bash
[master@ubuntu-server ~]$ sudo apt -y install netplan.io
```

为了避免现有的或默认 netplan 配置文件出现意外行为，请通过重命名将任何现有的配置目录移开：

```bash
