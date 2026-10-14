
VirtualBox 的桥接支持是在你的 Linux 主机软件上实现的。桥接是一种通过将数据包从一个网络转发到另一个网络来连接多个网络的网络技术。在这种范围内，桥接通过将连接到你在 Ubuntu 上设置的软件桥接器，实现了物理和虚拟网络接口之间的通信。连接到此桥接器的设备包括你的系统主网络接口以及每个每个虚拟机的一个虚拟网络接口。因此，桥接器可以看到连接到它的物理接口原本会看到的任何流量，并将流量路由到桥接器上的任何其他设备。这包括与连接和基础设施相关的流量（例如 DHCP 请求），这使得你的虚拟机能够从本地网络上的 DHCP 服务器获取 IP 配置信息，为它们提供标准的地址、标准的 DNS 配置以及你在网络 DHCP 服务器中设置的任何其他配置。当然，你可以为虚拟机在本地网络上分配静态地址，并像处理任何其他具有静态 IP 的主机一样提供其他网络配置信息。这完全取决于你！

# 注意

许多无线网络接口的驱动程序不支持桥接。如果你想在带有无线接口（或仅有无线接口）的笔记本电脑上使用虚拟机，并让笔记本电脑与虚拟机之间能够通信，那么安装 VMware Server 比使用 VirtualBox 更容易。你可以选择性地重新映射选定的端口以启用使用 NAT 的 VirtualBox 虚拟机与其主机之间的交互，但这非常痛苦。（查看本节末尾的侧栏获取有关如何操作的特定信息。）■

得益于 Linux、Ubuntu 和 VirtualBox 的智能，在你的主机系统上设置桥接和虚拟网络接口不需要 Cisco 证书、不需要接收 OSI 网络模型七层的能力，也不需要牺牲任何形式的家禽。让我们开始吧！我将这些指令呈现为一系列步骤，以便遵循：

1. 使用你喜欢的包管理应用程序在系统上安装 `bridge-utils` 和 `uml-utilities` 包。`bridge-utils` 包包含用于创建桥接器、将设备附加到桥接器、显示状态等的命令。`uml-utils` 包包含用于创建和管理 Linux 点对点（TUN）和以太网（TAP）网络设备的实用程序。例如，你可以从终端使用以下命令通过 `aptitude` 安装这些包：

```
sudo aptitude -y install bridge-utils uml-utilities
```

2. 修改你的 `/etc/network/interfaces` 文件以为桥接添加条目，并连接与你系统物理接口关联的网络设备。你应该注释掉该网络设备的任何条目。以下是一个名为 `br0` 的桥接器的示例条目，网络设备 `eth0` 已附加在该：

```
auto eth0
iface eth0 manual
up ifconfig $IFACE 0.0.0.0
up link set $IFACE promisc on
down link set $IFACE promisc off

auto br0
iface br0 dhcp
bridge_ports eth0
bridge_fd 0
bridge_maxwait 0
metric 0
```

第一部分定义了 `eth0` 为 TCP/IP 网络设备，它在网络启动时自动启动，但手动配置为静态 IP 地址 0.0.0.0，并将其设置为混杂模式。混杂模式是一种特殊模式，网络接口可以接收网络上的所有流量，即使不是发送给特定设备或接口的。第二个条目说明 `br0` 在网络启动时自动启动，由于 `bridge_ports` 条目，它应该通过 DHCP 获取配置，在跨桥接器转发数据包时不施加任何延迟（`bridge_fd` 条目），桥接器一旦就绪应立即进入转发模式（`bridge_maxwait` 条目），并且此接口应被视为可以立即到达默认网关的高优先级接口（`metric` 条目）。

## 提示

遗憾的是，Ubuntu 系统没有提供描述如何在 `/etc/network/interfaces` 文件中定义桥接设置的页面。关于我使用的设置（以及我未使用的其他）的更多信息，请参阅 `bridge-utils-interfaces` 页面，你可以在 NET 的以下位置找到它：http://web.isodeira.com/cgi-bin/man/man2html?bridge-utils-interfaces-5。

## 第 24 章：使用虚拟机和模拟器

3. 修改系统启动过程中创建与 VirtualBox 关联的设备时使用的规则文件，添加一条规则指定 TUN/TAP 虚拟设备 `/dev/net/tun` 将允许 `vboxusers` 组中的任何人写入。你需要将以下条目添加到 `/etc/udev/rules.d/99-virtualbox-ose.rules` 文件的末尾。以下内容应单行输入，不要包含冒号：

```
KERNEL==="vboxdrv", NAME="vboxdrv", OWNER="root", MODE="0660"
```

4. 如果你正在使用 Network Manager 或 WicD 管理网络接口，请确保它不会自动激活或连接 `eth0`。

5. 重启你的系统。当系统重新启动后，你可以使用 `brctl` 命令验证是否已创建桥，以及正确的物理和虚拟网络设备已附加到其上。在本节中使用的示例相关输出如下：

```
$ brctl show
bridge name id STP enabled interfaces
br0 8000.019d1239f01 no eth0
```

你还应该执行 `route -n` 命令来验证路由设置是否正确——你只会看到几条记录，它们都与桥有关。

6. 启动 VirtualBox 并更新每台虚拟机的网络配置信息。操作步骤如下：

- a. 在左窗格中选择一个虚拟机，点击 VirtualBox 工具栏中的设置图标。设置对话框将弹出，显示虚拟机的当前配置。点击左窗格中的“Network”项，将显示如图 24-19 所示的对话框。

# 注意

设置图标仅适用于已正常关闭且没有快照或保存状态信息的系统。在修改虚拟机的任何设置之前，你必须删除你的快照和保存状态信息。■

- b. 点击“Attached to”旁边的向下箭头，从下拉列表中选择“Bridged Adapter”（桥接适配器）。点击“Name”下拉列表并选择你之前创建的桥名称（如果你完全按照此操作，则选择 `br0`）。对话框看起来应该如图 24–20 所示。

- c. 点击 OK 保存更新后的网络配置信息。

# 第二部分：面向桌面用户的 Ubuntu

## 虚拟机的默认网络设置

![](img/1a233c34336fbf5a85d6eb785e401709_927_0.png)

## 虚拟机的主机接口设置

![](img/1a233c34336fbf5a85d6eb785e401709_927_1.png)

更新完所有虚拟机后，现在启动的任何虚拟机都将成为你本地网络的真正公民。真不错！

# 为 VirtualBox 虚拟机访问重新映射端口

端口转发是一种技术，一个系统将某些网络端口上的请求转发到另一个系统。现在，端口转发通常用于家庭网关，将来自外部网关的请求转发到内部网络上的特定系统。VirtualBox 提供了内置的端口转发支持，允许外部系统（或你的主机系统）直接访问虚拟机上的服务，而无需让虚拟机成为本地网络的完全参与者。

你使用 `VBoxManage` 命令来设置端口转发，这必须在虚拟机未实际运行时进行。对于你想要连接到虚拟机的每个服务，需要三条命令，如下所示，该示例允许外部访问运行在旧虚拟机 Ubuntu-Hardy 上的 SSH 服务器：

```
VBoxManage setextradata "Ubuntu-Hardy" \
VBoxInternal/Devices/pcnet/0/LINU/Config/ssh/Protocol" TCP
VBoxManage setextradata "Ubuntu-Hardy" \
VBoxInternal/Devices/pcnet/0/LINU/Config/ssh/GuestPort" 22
VBoxManage setextradata "Ubuntu-Hardy" \
VBoxInternal/Devices/pcnet/0/LINU/Config/ssh/HostPort" 2222
```

（这些命令通常在单行中输入——每行中的反斜杠仅是为了书中的格式化目的。）

这些命令中的第一条识别你正在转发的网络协议。第二条识别虚拟机上的端口，主机上特定端口的请求应被转发到该端口。第三条识别主机上的端口，外部系统通过它联系与此规则关联的服务。该规则的名称是 Config 条目之后、规则关键字之前的字段——在本例中，规则名称为 `ssh`。

一旦你输入了上述命令，该规则就会永久地定义在指定虚拟机（在本例中为 Ubuntu-Hardy）的 VirtualBox 配置中。启动虚拟机后，网络上的任何主机都可以类似 `ssh host-system -p 2222` 的命令访问虚拟机上的 SSH 服务。

在 VirtualBox 中设置端口转发时，你需要识别虚拟机上运行服务的端口（可以通过检查 `/etc/services` 文件来实现），并在主机上选择一个没有正在运行服务的端口。你应该始终使用大于 1 的端口号。
