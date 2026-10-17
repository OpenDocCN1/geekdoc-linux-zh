
本节侧重于用户网络和公共构建，因为这些是 KVM 和 QEMU 中最常用的机制。关于 `iptables` 的更多信息，请参阅 www.netfilter.org 或 Ubuntu 特有的信息，地址为 http://ubuntuforums.org/showthread.php?id=11972。关于 VDE 的更多信息，请参阅 http://wiki.virtualsquare.org/index.php/VDE，或面向 QEMU 的信息地址为 http://alien.slackbook.org/dokuwiki/dock.php?id=slackware:vde。

### 注意

在为 KVM 或 QEMU 指定网络选项时，你通常使用 `-net` 选项。第一个选项标识你想要使用的网络接口卡（可选的包括设备总线和 VLAN），它在 KVM 中默认为仿真的 Realtek 8139 网卡。第二个选项标识你想要使用的网络模式，默认为用户（User Networking）。“两个 `-net` 选项”规则的例外是你想要指示不支持网络，这可以通过在启动虚拟机时在命令行上指定 `-net none` 来完成。■

### 使用用户网络运行 KVM

如上一节所述，KVM/QEMU 使用的默认网络模式称为用户网络，它作为从客户操作系统发送到外部网络的数据包的转发器/接收器，并包含一个自动为虚拟机分配 IP 地址（在 10.0.2.X 子网上）的 DHCP 服务器。用户网络较慢，并且不支持所有的网络协议（例如，没有 ICMP）。因此，某些标准命令（如 `ping`）无法从虚拟机外部运行。用户网络最大的缺点是它不支持入站连接。然而，

第二部分：Ubuntu 桌面用户

如果你的运行虚拟机的主要目的是为了让你偶尔运行某些专有软件（例如，某些 Microsoft Office 组件），那么缺少入站连接并不紧要，KVM/QEMU 的用户网络可能就是你需要的全部。用户网络默认激活，但你也可以在命令行上使用 `-net nic -net` 命令行选项显式地指定它。

KVM/QEMU 提供的用户网络阻止了进入你虚拟机的通信；它没有对其提供完全支持。在使用用户网络时，KVM 和 QEMU 提供了两种扩展虚拟机连接性的机制：

- `redir protocol:host-port:ip:guest-port:`：允许你将来自主机系统的入站连接重定向到虚拟机上的端口。`protocol` 为 tcp 或 udp，`host-port` 是主机系统上应重定向到虚拟机上 `guest-port` 的网络端口，`guest-ip` 是虚拟机的 IP 地址（如果不是默认值，由内部 KVM/QEMU DHCP 服务器分配的 10.0.2.）。在启动虚拟机时必须在命令行上提供此选项和关联值。你可以在命令行上多次指定 `-redir` 以将多个端口重定向到虚拟机。

- `-smb /path/to/directory`：使用内部的 KVM/QEMU SMB 服务器将指定的目录导出为名为 `qemu` 的共享，虚拟机随后可以将其挂载为 `\GATEWAY-IP\qemu`。`GATEWAY-IP` 是 KVM/QEMU 内部网络重定向的 IP 地址，对于 Windows XP 和 Vista 虚拟机为 10.0.2.2，尽管对于其他版本的 Windows 可能会有所不同。

由于 `redir` 选项始终有效，我在不同版本的 KVM 和 QEMU 中在 `-smb` 选项上遇到过问题。一个更简单的解决方案是在 Ubuntu 主机上运行 Samba，然后在你的 `/etc/samba/smb.conf` 文件中配置类似于如下内容的命名 `qemu`：

```
[qemu]
comment = Windows File Share for KVM/QEMU
path = /full/to/directory
browable = yes
read-only = no
public = yes
```

重启 Samba 后，你将能够从虚拟机通过 `\GATEWAY-IP\qemu` 挂载 `qemu` 共享。我在从虚拟机访问环境中的其他共享时遇到过问题，但这种方法对我一直有效。

898

## 第 24 章：使用虚拟机和仿真器

### 使用虚拟网桥运行 KVM

如果你需要从外部系统访问你的 KVM/QEMU 虚拟机，并希望它们成为与运行它们的主机系统同一网络上的完全参与者，那么 KVM/QEMU 支持的虚拟网桥和 TUN/TAP 的组合正是你需要的。

设置虚拟网桥并为你的每个 KVM/QEMU 虚拟机创建 TAP 设备的步骤如下：

- 1. 使用你的包管理应用程序在系统上安装 `bridge-utils` 和 `uml-utilities` 软件包。`bridge-utils` 软件包包含了用于创建网桥、将设备附加到网桥上、显示状态信息等命令。`uml-utilities` 软件包包含了用于创建和管理 Linux 虚拟点对点（TUN）和以太网（TAP）网络设备的工具。例如，你可以从终端使用 `aptitude` 安装这些软件包。

2. 修改你的 `/etc/network/interfaces` 文件，为网桥添加条目，并将与系统物理网络接口关联的网络设备连接到它。你还应该注释掉该网络设备的任何现有条目。是一个名为 `br0` 的网桥示例，网络设备 `eth0` 已附加于：

```
sudo apt -y install bridge-utils uml-utilities
```

```
auto eth0
iface eth0 inet manual
down ifconfig $IFACE 0.0.0.0 up
down ip link set $IFACE promisc on
down ip link set $IFACE promisc off
down ifconfig $IFACE down

auto br0
iface br0 inet dhcp
bridge_ports eth0
bridge_fd 0
bridge_wait 0
metric 0
```

第一部分将 `eth0` 定义为 TCP/IP 网络设备，该设备在网络启动时自动启动，但手动配置为静态 IP 地址 0.0.0.0，并且被设置为混杂模式。混杂模式是一种特殊模式，网络接口可以接收网络上的所有流量，即使这些流量不是针对特定网卡或接口的。注释掉网络设备的任何现有条目（在本节使用的示例中为 `eth0`！）。第二

第二部分：Ubuntu 桌面用户

条目说明 `br0` 在网络启动时自动启动，是一个 IP 网桥（因为有 `bridge_ports` 条目），它应该通过 DHCP 获取配置，在跨网桥转发数据包时不施加延迟（`bridge_fd` 条目），网桥在启动后应立即进入转发模式（`bridge_maxwait` 条目），并且此接口应被视为可以立即到达网关的高优先级接口（`metric` 条目）。

## 提示

遗憾的是，Ubuntu 系统没有提供描述你在 `/etc/network/interfaces` 中定义设置的页面。关于我使用的设置（以及许多其他的）的更多信息，请参阅桥-utils 接口添加，你可以在 NET 等位置找到：http://web.lesrodeira.com/cgi-bin/man2htmlbridge-utils-interfaces+5 .

- 3. 修改在系统启动过程中创建与 KVM 关联设备的文件，添加规则指定 TUN/TAP 虚拟网络设备 `/dev/net/tun` 对 kvm 组中的任何人可写。你可能需要在 `/etc/udev/rules.d/45-kvm.rules` 文件末尾添加以下条目。单行输入，不要 \

```
KERNEL="tun", NAME="net/*", OWNER="root",
GROUP="kvm", MODE="0660"
```

### 注意

我遇到过 udev 正确设置 tun/tap 设备所有权的问题。为了消除这种可能性，你可以将以下内容加入你的 `/etc/rc.local` 文件（在 "exit" 条目之前）：

- `chown root:kvm /dev/net/tun`

`chmod 0660 /dev/net/tun` ■

- 4. 确保你可以通过执行命令访问 tap0 虚拟网络设备：

```
sudo tunctl -u YOUR-USER-NAME
```

重启你的系统。当系统重启后，你可以使用 `brctl` 命令验证是否已创建网桥以及正确的物理和虚拟

900

## 第 24 节：使用虚拟机和模拟器

网络设备已连接到其上。我所使用的示例相关的输出如下所示：

```
$ brctl show
bridge name bridge id STP enabled interfaces
br0 8000.0019d1239f01 no eth0
```

你还可以通过执行 `route -n` 命令来验证路由是否已设置——你只会看到少数条目，它们都与桥有关。

- 5. 使用类似下面的命令启动你的虚拟机：

```
sudo kvm -hda kvm_disk_image.img -m 512 -net nic -net tap,ifnametap0
```
