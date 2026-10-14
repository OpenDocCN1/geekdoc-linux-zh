
`sudo dnf update -y`

此命令获取并应用所有可用更新，保持系统安全并处于最新状态。

### 第 2 步：安装旧工具

安装 `net-tools` 包，它提供了对 `ifconfig` 和 `netstat` 等经典命令的支持。

```bash
sudo dnf install net-tools -y
```

安装后，可以使用以下命令进行验证：
- `ifconfig`
- `netstat -rn`

## 与 Rocky 版本的兼容性

与 Rocky Linux 8 相比，Rocky Linux 9 在网络工具上引入了许多改进。关键增强包括：
- NetworkManager：Rocky Linux 9 对高级绑定和聚合配置提供了更广泛的支持，而 Rocky Linux 8 在这方面的能力有限。
- firewall：第 9 版本改进了区域管理，并支持将运行时规则持久化到永久配置中。相比之下，Rocky Linux 8 执行此类任务需要更多手动操作。
- 内核参数：Rocky Linux 9 内核的更新在 IPv6 处理和 TCP 优化行为方面发生了细微变化。

建议管理员在切换 Rocky 版本之间验证已安装的网络工具版本。可以使用以下命令完成：
- `rpm -q NetworkManager`
- `firewall --version`

## 管理网络接口

有效的网络管理对于可靠的 IT 基础设施至关重要，本章提供了 Rocky Linux 9 中配置网络接口的实操指南，使用 `nmcli` 和 `nmui` 等命令行工具以及手动方法——帮助初学者和资深管理员确保物理、虚拟和云环境的连接性。

### 第 1 步：关闭 Rocky Linux 9 虚拟机

在进行硬件更改之前，确保虚拟机已关闭。

### 第 2 步：添加新的网络适配器
- a. 在 VMware Workstation 中，右键点击我们的 Rocky Linux 9 虚拟机并选择“设置”（Settings）。
- b. 点击“添加（Add...）”，选择“网络适配器”（Network Adapter），然后点击“完成（Finish）”。
- c. 选择 NAT 作为网络连接类型。
- d. 点击确定以应用更改。

## 步骤 3：启动 Rocky Linux 9 虚拟机

## 步骤 4：识别新的网络接口

打开终端并执行 `ip` 来列出所有网络接口。
通过名称识别新接口，例如 `ensX`（例如 `ens224`）、`eth1` 或系统分配的其他名称。接口名称通常遵循基于硬件或虚拟化环境的模式。

寻找一个新的接口，例如 `ensX`、`eth1` 或类似的接口。

## 步骤 5：启用接口

将 `ensX` 替换为我们实际的接口名称：`sudo ip link set ensX up`

## 步骤 6：通过 DHCP 获取 IP 地址
`sudo dhclient ensX`

## 步骤 7：验证网络连通性

测试互联网访问：`ping -c 4 google.com`
验证已分配的 IP：`ip a show ensX`

## 使用 nmcli

在开始实验之前，我们需要在 VMware Workstation 中为 Rocky Linux 9 虚拟机添加一个额外的的 NAT 网络接口。这个新接口允许虚拟机通过宿主机访问互联网或其他网络。

一旦在 VMware 中添加了接口，我们将在终端中使用以下命令对其进行设置并检查其工作情况：
`sudo nmcli con type ethernet con-name ens224 ifname ens224`

该命令创建了一个名为 `ens224` 的新线路连接，并将其链接到同名的网络接口上。

```bash
sudo nmcli con up ens224
```

此命令激活（启动）`ens224` 连接。

## 网络命令与预期输出

`nmcli` 是一个用于通过 NetworkManager 管理网络设置的命令行工具。在没有图形界面的环境中工作时它特别有用。

要查看所有当前网络接口及其状态，请使用以下命令：
- `nmcli device status`

```
[cesarmserver@localhost ~]$ nmcli device status

DEVICE TYPE STATE CONNECTION

ens160 ethernet connected ens160

ens224 ethernet connected ens224

lo loopback connected (externally) lo

[cesarmserver@localhost ~]
```

图 5.1：网络接口

图 5.1 中的输出显示了三个太网接口和一个环回接口。环回接口（通常命名为 `lo`）是系统内部用于同一机器内测试和通信的特殊网络。

理解此网络配置对于有效的网络管理和排除连通性问题至关重要。知道哪些接口处于激活或禁用状态有助于我们识别问题并正确配置连接。

## 使用 nmcli（NetworkManager 命令行工具）

要激活特定的网络接口（即将其上线），请使用以下命令：
- `sudo nmcli up <connection-name>`

```
[cesarmserver@localhost ~] sudo nmcli up ens224

[password] for cesarmserver:

Connection successfully activated (D-Bus active: /org/freedesktop/NetworkManager/ActiveConnection/4)

[cesarmserver@localhost ~]
```

图 5.2：启动接口

此图说明了使用命令行实用程序启动网络接口的过程。此操作激活了指定的接口，允许其在网络上发送和接收数据。一旦接口启动，系统就能够参与网络通信，这对于访问服务、传输数据以及在本地和云环境中维护连通性至关重要。这一步是网络配置和故障排除的关键部分。

以下命令将将禁用特定的网络接口。
- `sudo nmcli con down <connection-name>`

```
[casmerserver@local] ~# sudo nmcli con down ens224

[sudo] password for casmerserver:

Connection successfully deactivated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/4)

[casmerserver@local] ~#
```
