
2. 在 VirtualBox 上启动 `RHEL-VM1`，并突出 `server10`。

3. 点击顶部的 `Settings`（设置）然后点击 `Network`（网络）。在弹出窗口中点击“Adapter 2”（适配器 2）并勾选“Enable Network”（启用网络）。在“Attached to”（连接到）列表中选择“Internal”（内部）。参见图 17-1。

4. 点击 `OK` 返回 VirtualBox 界面。

5. 开启 `RHEL8-VM1` 启动。

6. 当服务器启动后，以 `user1` 身份登录并运行以下 `ip` 命令验证网络：

```
[user1@server10 ~]$ ip a
1: lo: <LOOPBACK, UP, LOWER_UP> 65536 qdisc noque state UNKNOWN
	group default qlen 1000
	link/loopback 00:00:00:00:00:00 00:00:00:00:00:00
	inet 127.0.0.1/8 scope lo
	valid_lft preferred_ft forever
inet6 ::1/64 scope host
	valid_lft preferred_ft forever
2: enp0s:<BROCAST, MULTICAST, UP, LOWER_UP> mtu 1500 qdisc noodel enp03 state UP
	group default qlen 1000
	link/ether 08:00:27:bf:55:8e brd ff:ff:ff:ff:ff:ff
	inet 192.168.0.10/24 brd 192.168.0.255 scope noprefixroute enp0s
	valid_lft preferred_ft forever
inet6 fe80::a001:27ff:fe58:56/64 scope link
	valid_lft preferred_ft forever
3: enp0s:<BROCAST, MULTICAST, UP, LOWER_UP> mtu 1500 qdisc noodel state UP
	group default qlen 1000
	link/ether 08:00:27:42:4e:1d brd ff:ff:ff:ff:ff:ff
```

输出显示了一个名为 `enp0s8` 的新网络设备。这是你添加到虚拟机的接口。

7. 重复步骤 1 到 6，为 `server20` 添加网络接口并进行验证。

这完成了向 `server10` 和 `server20` 添加新网络接口的操作。。你现在已经准备好在接下来的练习中使用它们了。

## 网络设备和连接管理工具

有几种工具和方法可以配置和管理网络接口、连接以及连接配置文件。`NetworkManager` 服务也包含一个用于此目的工具集。让我们来看表 17-3 中的基础管理工具。

| 命令 | 描述 |
| --- | --- |
| `ip` | 一种强大且多功能的工具，用于显示、监控和管理接口、连接、流量等。 |
| `ifup` | 激活连接 |
| `ifdown` | 停用连接 |

## 表 17-3 基础网络管理工具

你可以手动创建连接配置文件并将其附加到网络设备上。许多 Linux 管理员更倾向于这种方法。RHEL 还为该目的提供了另一种替代方法，将在本章的后后部分进行讨论。

在练习 17-3 中，你将使用手动方法为练习 17-2 中添加的新型网络设备配置连接配置文件，并使用表 17-3 中列出的工具。

## 练习 17-3：手动配置新网络连接

此练习应在 `server10` 上以 `user1` 身份执行，并在需要时使用 `sudo`。

在此练习中，你将使用文本编辑工具为新的网络接口 `enp0s8` 创建连接配置文件。你将分配 IP `172.10.10.110/24` 以及网关 `172.10.10.1`，并设置在系统重启动时自动激活。你将在命令行提示符停用并重新激活此接口。

- 1. 在 `/etc/sysconfig/network-scripts` 目录下创建一个名为 `ifcfg-enp0s8` 的文件，并输入以下信息以建立连接配置文件：

```
user@server10 ~]$ sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s8
TYPE=Ethernet
BOOTPROTO=static
DEFROUTE=yes
IPV4FAILURE_FATAL=no
IPV6INIT=no
NAME=enp0s8
DEVICE=enp0s8
ONBOOT=yes
IPADDR=172.10.10.110
PREFIX=24
GATEWAY=172.10.10.1
```

- 2. 使用 `ifdown` 和 `ifup` 命令停用并重新激活此接口：

```
user@server10 ~]$ sudo ifdown enp0s8
Connection 'enp0s8' successfully deactivated (D-Bus active path: /org/freedesktop/p/NetworkManager/ActiveConnection/2)
user@server10 ~]
user@server10 ~]$ ifup enp0s8
Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/3)
```

- 3. 验证 `enp0s8` 连接的激活情况：

```
user@server10 ~]$ ip a

3: enp0s8:<BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc qlen 1000
link/eth8 08:00:27:4e:11:1d br:ff:ff:ff:ff:ff
inet 172.10.10.110/24 172.10.10.255 scope global noprefix enp0s8
valid_l forever preferred_l forever
inet6 fe80::a00:27ff:fe42:1/64 scope link
valid_l forever preferred_l forever
```

新的连接配置文件 `enp0s8` 已应用到名为 `enp0s8` 的新网络设备上。该连接现在已准备使用了。通过此新连接到 `server10` 的连通性将在本章稍后进行测试。

## NetworkManager 服务

`NetworkManager` 是 RHEL 8 中默认的接口和连接配置、管理和监控服务。该服务有一个名为 `NetworkManager` 的守护进程，负责保持可用接口和连接处于开启和激活状态。它提供了一个强大的命令行工具 `nmcli` 来管理接口和连接，并控制服务。该实用程序为它们的有效管理提供了许多选项。`NetworkManager` 服务还提供了一个名为 `nmui` 的文本界面和一个等效的图形界面 `nm-connection-editor`，你可以用它们来替代 `nmcli`。

## nmcli 命令

`nmcli` 是一个 `NetworkManager` 命令行工具，用于创建、查看、修改、删除、激活和停用网络连接，并控制和报告网络设备状态。它在七种对象类别上运行，每个类别都支持多个选项以组成完整的命令。这七类类别是通用（general）、网络（networking）、连接（connection）、设备（device）、无线（radio）、监控（monitor）和代理（agent）。本文讨论仅关注连接和设备对象类别。它们在表 17-4 中描述，以及它们可以执行的管理操作。

| 对象 | 描述 |
| --- | --- |
| Connection | 激活、停用和管理网络连接 |
| show | 列出连接 |
| up / down | 激活/停用连接 |
| add | 添加连接 |
| edit | 编辑现有连接或添加新连接 |
| modify | 修改连接的一个或多个属性 |
| delete | 删除连接 |
| reload | 指示 NetworkManager 重新读取所有配置文件 |
| load | 指示 NetworkManager 重新读取一个配置文件 |

### 表 17-4 网络连接和设备工具

对象类别和其中的对象可以以缩写形式编写。例如，连接类别可以写为 “c”，设备类别可以写为 “d”。

## 练习 17-4：使用 nmcli 配置新网络连接

此练习应在 `server20` 上以 `user1` 身份执行，并在需要时使用 `sudo`。

在此练习中，你将使用 `nmcli` 命令为练习 17-2 中添加的新网络接口 `enp0s8` 创建连接配置文件。你将分配 IP `172.10.10.120/24` 以及网关 `172.10.10.1`，并设置在系统启动时自动激活。你将在命令行提示符停用并重新激活此接口。

- 检查 `NetworkManager` 服务的运行状态：
