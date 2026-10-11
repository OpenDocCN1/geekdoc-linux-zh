

```
[root@rhel ~]# nmcli connection
 NAME               UUID                                  TYPE      DEVICE
 enp1s0             320f6572-672b-33c8-9014-b0fb087ae1a2  ethernet  enp1s0
[root@rhel ~]# nmcli connection show enp1s0 | grep IP4.
IP4.ADDRESS[1]:    192.168.122.145/24
IP4.GATEWAY:       192.168.122.1
IP4.ROUTE[1]:      dst = 192.168.122.0/24, nh = 0.0.0.0, mt = 100
IP4.ROUTE[2]:      dst = 0.0.0.0/0, nh = 192.168.122.1, mt = 100
IP4.DNS[1]:        192.168.122.1
```

*图 7.15：命令 nmcli 的输出示例。*

如果可能，请指定参数以添加连接、修改连接或删除连接等。图 7.16 展示了一些常见操作：

```
[root@rhel ~]# nmcli c add type ether con-name "test" ifname enp7s0 ip4 "10.10.0.22/24"
 Connection 'test' (f67e84a5-a754-4268-92ff-0d501a70d9ac) successfully added.
[root@rhel ~]# nmcli connection
 NAME   UUID                                  TYPE      DEVICE
 enp1s0 320f6572-672b-33c8-9014-b0fb087ae1a2  ethernet  enp1s0
 test   f67e84a5-a754-4268-92ff-0d501a70d9ac  ethernet  enp7s0
[root@rhel ~]# nmcli c modify test ip4 "10.10.10.23/24"
[root@rhel ~]# nmcli connection delete test
 Connection 'test' (f67e84a5-a754-4268-92ff-0d501a70d9ac) successfully deleted.
```

*图 7.16：命令 nmcli 的输出示例。*

*表 7.3* 展示了一些在基本网络配置和操作中常见操作的示例：

| 操作 | 命令 |
| --- | --- |
| 添加具有静态 IP、网关和 DNS 的新连接 | nmcli c a type ether con-name "test" ipv4.method manual ip4 "10.10.10.23/24" gw4 "10.10.10.1" ipv4.dns "10.10.10.2" |
| 停用连接 | nmcli connection down "test" |
| 启用连接 | nmcli connection up "test" |
| 向现有连接追加 DNS 服务器 | nmcli con modify "test" +ipv4.dns 8.8.8.8 |
| 移除 IP 地址 | nmcli con modify "test" -ipv4.addresses "10.10.4/24" |

*表 7.3：nmcli 示例命令*

## 命令 nmtui

该工具以可视化的方式帮助配置系统中的连接和设备，并进行查询。运行命令 **nmtui** 会显示*图 7.17* 所示的菜单：

![](img/863afa537de4eed7deb11978bfbfa90e_230_0.png)

图 7.17：命令 nmtui 的界面。

第一个选项 *Edit a connection*（编辑连接）会列出连接，并允许创建新连接或编辑现有连接。*图 7.18* 显示了该列表及可用的操作：

![](img/863afa537de4eed7deb11978bfbfa90e_231_0.png)

*图 7.18：nmtui 中的“编辑连接”菜单。*

使用 *Tab* 键，可以在可用连接和右侧菜单之间导航。在 `<Edit...>` 上按该键将显示所选连接的配置，如 *图 7.19* 所示：

![](img/863afa537de4eed7deb11978bfbfa90e_231_1.png)

*图 7.19：nmtui 中的“编辑连接”对话框。*

添加新连接时，可以指定接口是使用 DHCP 还是 *静态 IP* 配置，以及 DNS 和网关配置。根据系统和接口的需求，也可以禁用 IPv4 或 IPv6。

# Debian 和 Ubuntu 上的网络配置

Debian 使用基于文件的配置来管理网络。定义网络配置的主要文件是 */etc/network/interfaces*，以下代码块展示了一个静态 IP 配置的示例：

```
# The loopback network interface
auto lo
iface lo inet loopback
# The primary network interface
auto eth0
iface eth0 inet static
    address 37.139.7.55
    netmask 255.255.255.0
    gateway 37.139.7.1
    dns-nameservers 8.8.4.4 8.8.8.8 209.244.0.3
```

可以执行命令 **man interfaces** 来获取该文件中可能的语法和不同的配置。在配置完文件后，需要运行命令 **systemctl restart networking** 重启 *networking* 服务。

Ubuntu 发行版使用 *netplan* 来定义网络配置。这些文件采用 YAML 格式定义，位于 */etc/netplan/* 目录中。**图 7.20** 展示了 *netplan* 中的配置如何被 *systemd-networkd*（默认）或 *NetworkManager* 使用：

![](img/863afa537de4eed7deb11978bfbfa90e_233_0.png)

*图 7.20：Netplan 示意图。来源：Canonical。*

在安装期间，会创建一个名为 `00-installer-config.yaml` 的文件，其中包含安装过程中指定的配置。以下代码块展示了一个示例：

```
# This is the network config written by 'subiquity'

network:
  ethernets:
    enp1s0:
      dhcp4: true
  version: 2
```

以下代码块展示了静态 IP 配置的示例：

```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp7s0:
      addresses:
        - 10.10.10.2/24
      nameservers:
        addresses: [10.10.10.1, 1.1.1.1]
      routes:
        - to: default
          via: 10.10.10.1
```

命令 **netplan** 有两个主要参数：

- **try**：尝试 /etc/netplan/ 文件中定义的配置，并要求用户确认新配置。如果用户不接受新设置或在 120 秒内未做出回应，配置将被还原。
- **apply**：将 /etc/netplan/ 文件中定义的配置应用到系统。

*图 7.21* 展示了运行命令 **netplan try** 的输出：

```
root@ubuntu:/etc/netplan# netplan try
Do you want to keep these settings?

Press ENTER before the timeout to accept the new configuration

Changes will revert in 100 seconds
Configuration accepted.
```

*图 7.21：命令 netplan 的输出示例*

## 路由

另一个重要的网络概念是路由，即选择到达网络的路径。Linux 系统可以定义规则以使用不同的网关访问网络。此外，Linux 系统可以被配置为同一网络中其他系统的路由器。

如前所述，使用参数为 `route` 的命令 `ip` 可以列出系统中配置的路由。可以使用网络文件、netplan 或 NetworkManager 定义静态路由器。表 7.4 展示了配置内容或定义路由的命令：

| 元素 | 内容 / 命令 |
| :--- | :--- |
| Debian 的 interfaces 文件 | `allow-hotplug enp1s0` <br> `iface enp1s0 inet dhcp` <br> `up ip route add 192.168.10.0/24 via 192.168.122.10 dev enp1s0` <br> `up ip route add 192.168.11.0/24 via 192.168.122.11 dev enp1s0` |
| Ubuntu 的 netplan 配置 | `network:` <br> `  ethernets:` <br> `    enp1s0:` <br> `      dhcp4: true` <br> `      routes:` <br> `        - to: 192.168.10.0/24` <br> `          via: 192.168.122.10` <br> `        - to: 192.168.11.0/24` <br> `          via: 192.168.122.11` <br> `  version: 2` |
| Red Hat 的 route-eth0 示例 | `192.168.10.0/24 via 192.168.122.1 dev eth0` <br> `192.168.11.0/24 via 192.168.122.1 dev eth0` |
| 使用 nmcli 进行 NetworkManager 操作 | `nmcli con mod test +ipv4.routes "192.168.10.0/24 192.168.122.10,192.168.11.0/24 192.168.122.11"` |

表 7.4：路由配置

配置静态路由后，命令 `ip route` 的输出示例如图 7.22 所示：

![](img/863afa537de4eed7deb11978bfbfa90e_235_0.png)

图 7.22：命令 ip 的输出示例。

配置 Linux 系统作为 *路由器* 时，如果使用的是同一个接口来将从源客户端到目的地的流量重定向，则通常不需要高级配置。使用不同接口则需要了解与安全防火墙相关的知识，这在下一章中有所描述。

系统中用于确定是否允许转发流量的参数由 `sysctl` 配置中的键 `net.ipv4.ip_forward` 定义。出于安全考虑，默认情况下它是禁用的（值为 `0`），可以使用命令 `sysctl` 临时启用它，或使用文件 `/etc/sysctl.conf` 永久启用。

*图 7.23* 到 *7.26* 展示了如何检查和配置 IP 转发，并确保该 Linux 系统作为路由器正常工作：

- 检查名为 ubuntu 的服务器上系统参数 `ip_forward` 的值：

```
root@ubuntu:~# sysctl net.ipv4.ip_forward
net.ipv4.ip_forward = 0
```

*图 7.23：命令 sysctl 的输出示例。*

- 配置名为 `rhel` 的系统使用 ubuntu 系统的 IP（`192.168.122.101`）作为网关，并尝试访问一个外部 IP（Google 的 DNS IP `8.8.8.8`）：

```
[root@rhel ~]# ip route del default
[root@rhel ~]# ip route add default via 192.168.122.101
[root@rhel ~]# ping -c1 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 0 received, 100% packet loss, time 0ms
```

*图 7.24：使用命令 ip 操作及命令 ping 的输出示例。*

- 在名为 `ubuntu` 的系统中启用 `ip forwarding`（IP 转发）：

```
root@ubuntu:~# sysctl net.ipv4.ip_forward=1
net.ipv4.ip_forward = 1
```

*图 7.25：命令 sysctl 的输出示例*

- 从节点 `rhel` 尝试使用 `ping` 命令以确保通信可行：

