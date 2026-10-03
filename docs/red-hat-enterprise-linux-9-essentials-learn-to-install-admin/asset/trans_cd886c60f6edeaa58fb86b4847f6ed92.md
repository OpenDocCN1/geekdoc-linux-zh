
## 12.4 使用连接配置文件

到目前为止，我们已经探讨了使用连接，但没有解释连接是如何配置的。连接的配置被称为连接配置文件，并存储在位于 /etc/NetworkManager/system-connections 目录中的文件中，其内容可能如下所示：

```
# ls /etc/NetworkManager/system-connections
zoneone.nmconnection    eno1.nmconnection
zonethree.nmconnection  zonetwo.nmconnection
```

例如，考虑 eno1.nmconnection 文件的内容：

```
id=eno1
uuid=efc69a99-17a3-3636-b68f-bfcc56a73844
type=ethernet
autoconnect-priority=-999
interface-name=eno1
timestamp=1679678184

[ethernet]

[ipv4]
method=auto

[ipv6]
addr-gen-mode=eui64
method=auto

[proxy]
```

该文件包含有关连接的基本信息，包括当前分配给它的设备类型（Ethernet）和连接将在系统启动时自动激活并使用 DHCP（auto）获取 IP 地址的事实。可以通过修改此文件并指示 nmcli 重新加载连接配置文件来实现对连接配置文件的更改：

```
# nmcli con reload
```

新的连接配置文件也可以手动创建或由 nmcli 自动生成。例如，假设系统上安装了一个新的网络设备。发生这种情况时，NetworkManager 服务将检测到新硬件并为其创建设备。在下面的示例中，新设备被分配了名称 eno2：

```
# nmcli dev status
```

| 设备 | 类型 | 状态 | 连接 |
|---|---|---|---|
| eno1 | 以太网 | 已连接 | eno1 |
| eno2 | 以太网 | 已连接 | Wired connection 1 |

NetworkManager 自动检测到该设备，激活了它，并将其分配给名为“Wired connection 1”的连接。这是一个默认连接，我们对其没有配置控制，因为在 /etc/NetworkManager/system-connections 中没有它的接口配置文件。因此，下一步是删除“Wired connection 1”连接，并使用 nmcli 创建新的连接并将其分配给设备。删除连接的命令如下：

```
# nmcli con delete "Wired connection 1"
```

接下来，nmcli 可用于创建新的连接配置文件，该配置文件可以配置为静态 IP 地址或从 DHCP 服务器获取的动态 IP 地址。要创建名为 dyn_ip 的动态连接配置文件，将使用以下命令：

```
# nmcli connection add type ethernet con-name dyn_ip ifname eno2
Connection 'dyn_ip' (160d9e10-bbc8-439a-9c47-a2ec52990472) successfully added.
```

要创建不绑定到特定设备的新的连接配置文件，只需在命令中省略 ifname 选项即可：

```
# nmcli connection add type ethernet con-name dyn_ip
```

创建连接后，名为 dyn_ip.nmconnection 的文件将被添加到 /etc/NetworkManager/system-connections 目录。

或者，要创建名为 static_ip 并分配静态 IP 地址（在本例中为 192.168.1.200）的连接，将使用以下命令：

```
# nmcli con add type ethernet con-name static_ip ifname eno0 ip4 192.168.1.200/24 gw4 192.168.1.1
Connection 'static_ip' (3fccafb3-e761-4271-b310-ad0f28ee8606) successfully added.
```

相应的 static_ip.nmconnection 文件内容如下：

```
[connection]
id=static_ip
uuid=41eca181-381c-4d12-b6c9-30446d4e29d1
type=ethernet
interface-name=eno0

[ethernet]

[ipv4]
address1=192.168.1.200/24,192.168.1.1
method=manual

[ipv6]
addr-gen-mode=default
method=auto

[proxy]
```

## RHEL 9 网络管理

添加新连接的命令可以稍作修改以分配 IPv4 和 IPv6 静态地址：

```
# nmcli con add type ethernet con-name static_ip ifname eno0 ip4 192.168.1.200/24 gw4 192.168.1.1 gw4 192.168.1.1 ip6 cabf::4532 gw6 2010:d
```

## 12.5 交互式编辑

除了使用命令行选项使用 nmcli 之外，该工具还包括一个交互模式，可用于创建和修改连接配置文件。例如，以下转录显示了交互模式被用于创建名为 demo_con 的新以太网连接：

```
# nmcli con edit
Valid connection types: 6lowpan, 802-11-olpc-mesh (olpc-mesh), 802-11-wireless (wifi), 802-3-ethernet (ethernet), adsl, bluetooth, bond, bridge, cdma, dummy, generic, gsm, infiniband, ip-tunnel, macsec, macvlan, ovs-bridge, ovs-interface, ovs-port, pppoe, team, tun, vlan, vpn, vxlan, wimax, wpan, bond-slave, bridge-slave, team-slave
Enter connection type: ethernet

===| nmcli interactive connection editor |===

Adding a new '802-3-ethernet' connection

Type 'help' or '?' for available commands.
Type 'print' to show all the connection properties.
Type 'describe [<setting>.<prop>]' for detailed property description.

You may edit the following settings: connection, 802-3-ethernet (ethernet), 802-1x, dcb, sriov, ethtool, match, ipv4, ipv6, tc, proxy
nmcli> set connection.id demo_con
nmcli> set connection.interface eno1
nmcli> set connection.autoconnect yes
nmcli> set ipv4.method auto
nmcli> set 802-3-ethernet.mtu auto
nmcli> set ipv6.method auto
nmcli> save
Saving the connection with 'autoconnect=yes'. That might result in an immediate activation of the connection.
Do you still want to save? (yes/no) [yes] yes
Connection 'demo_con' (cb837408-6c6f-4572-9548-4932f88b9275) successfully saved.
nmcli> quit
```

另一方面，以下转录修改了之前创建的 static_ip 连接配置文件，使其使用与最初指定的不同的静态 IP 地址：

```
# nmcli con edit static_ip

===| nmcli interactive connection editor |===
```

正在编辑现有的 '802-3-ethernet' 连接：'static_ip'

输入 'help' 或 '?' 查看可用命令。
输入 'print' 显示所有连接属性。
输入 'describe [<setting>.<prop>]' 获取详细的属性描述。

```
You may edit the following settings: connection, 802-3-ethernet (ethernet), 802-1x, dcb, sriov, ethtool, match, ipv4, ipv6, tc, proxy
nmcli> print ipv4.addresses
ipv4.addresses: 192.168.1.200/24
nmcli> set ipv4.addresses 192.168.1.201/24
nmcli> save
Connection 'static_ip' (3fccafb3-e761-4271-b310-ad0f28ee8606) successfully updated.
nmcli> quit
```

修改现有连接后，请记住指示 NetworkManager 重新加载配置文件：

```
# nmcli con reload
```

使用交互模式时，了解有一个广泛的内置帮助系统来学习如何使用该工具是有用的。可以通过在 nmcli > 提示符下键入 help 或 ? 来访问帮助主题：

```
nmcli> ?
--------------------------------------------------------------------------------
---[ Main menu ]---
goto      [<setting> | <prop>]              :: go to a setting or property
remove    <setting>[.<prop>] | <prop>      :: remove setting or reset property value
set       [<setting>.<prop> <value>]       :: set property value
describe  [<setting>.<prop>]               :: describe property
print     [all | <setting>[.<prop>]]       :: print the connection
verify    [all | fix]                      :: verify the connection
save      [persistent|temporary]           :: save the connection
activate  [<ifname>] [/<ap>|<nsp>]         :: activate the connection
back                                      :: go one level up (back)
help/?    [<command>]                      :: print this help
nmcli     <conf-option> <value>            :: nmcli configuration
quit                                      :: exit nmcli
--------------------------------------------------------------------------------
```

## 12.6 配置 NetworkManager 权限

除了使 RHEL 9 上的网络管理更轻松之外，NetworkManager 还允许为连接指定权限。例如，以下命令将连接配置文件限制为 root 和名为 john 和 caitlyn 的用户帐户：
