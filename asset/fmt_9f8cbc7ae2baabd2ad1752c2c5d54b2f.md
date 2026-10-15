
配置网络接口包括为接口分配 IP 地址、子网掩码和广播地址，定义 IP 别名、手动激活和禁用接口、系统重启时自动激活、更新 `/etc/hosts` 文件以及修改接口设置。这些任务可以使用命令或网络配置器执行。

# 配置网络接口

要在 `rhel01` 上成功配置具有 C 类 IP 地址 `192.168.2.201`、默认子网掩码 `255.255.255.0` 的接口 `eth2`，请运行以下 `ifconfig` 命令：

```bash
# ifconfig eth2 192.168.2.201 netmask 255.255.255.0 192.168.2.255
```

## 网络接口管理

运行以下命令验证 IP 分配：

```bash
# ifconfig eth2
```

```
eth2 Link encap:Ethernet  hwaddr 00:03:47:3B:EB:6F
        inet 192.168.2.201  mask:255.255.255  broadcast:192.168.2.255
        UP,BROADCAST,RUNNING,MULTICAST mtu=1500
        rx bytes=0 packets=0  errors=0  dropped=0
        tx bytes=0 packets=0  errors=0  dropped=0
```

# 配置 IP 别名

如果你计划在单个系统上运行多个应用程序（假设 `eth2` 只有一个物理接口），可以通过以下方式为 `eth2` 分配三个 IP 地址：

运行 `ifconfig` 或 `ip` 命令检查结果：

```bash
# ifconfig eth2:1 192.168.3.201 mask 255.255.255 192.168.3.255
# ifconfig eth2:2 192.168.4.201 mask 255.255.255 192.168.4.255
# ifconfig eth2:3 192.168.5.201 mask 255.255.255 192.168.5.255
```

```bash
# ifconfig
```

```
eth2 Link encap:Ethernet  hwaddr 00:03:47:3B:EB:6F
        inet 192.168.2.201  mask:255.255.255  broadcast:192.168.2.255
        UP,BROADCAST,RUNNING,MULTICAST mtu=1500
        rx bytes=0 packets=0  errors=0  dropped=0
        tx bytes=0 packets=0  errors=0  dropped=0
eth2:1 Link encap:Ethernet  hwaddr 00:03:47:3B:EB:6F
        inet 192.168.3.201  mask:255.255.255  broadcast:192.168.3.255
        UP,BROADCAST,RUNNING,MULTICAST mtu=1500
        rx bytes=0 packets=0  errors=0  dropped=0
        tx bytes=0 packets=0  errors=0  dropped=0
eth2:2 Link encap:Ethernet  hwaddr 00:03:47:3B:EB:6F
        inet 192.168.4.201  mask:255.255.255  broadcast:192.168.4.255
        UP,BROADCAST,RUNNING,MULTICAST mtu=1500
        rx bytes=0 packets=0  errors=0  dropped=0
        tx bytes=0 packets=0  errors=0  dropped=0
eth2:3 Link encap:Ethernet  hwaddr 00:03:47:3B:EB:6F
        inet 192.168.5.201  mask:255.255.255  broadcast:192.168.5.255
        UP,BROADCAST,RUNNING,MULTICAST mtu=1500
        rx bytes=0 packets=0  errors=0  dropped=0
        tx bytes=0 packets=0  errors=0  dropped=0
```

现在用户可以使用四个 IP 地址中的任何一个访问系统。

# 设置系统启动时激活网络接口

之前小节中执行的网络接口配置在下次重启后不会保留。为了在系统重启后保留设置并自动分配给接口，你需要在 `/etc/rc.d/init.d/network` 启动脚本中创建文件——`/etc/sysconfig/network-scripts/ifcfg-eth2`、`/etc/sysconfig/network-scripts/ifcfg-eth2:1`、`/etc/sysconfig/network-scripts/ifcfg-eth2:2` 和 `/etc/sysconfig/network-scripts/ifcfg-eth2:3`，该脚本在系统进入运行级别 2 时的启动时执行。脚本会读取接口配置文件并在已配置的接口上执行 `ifup` 命令。

`/etc/sysconfig/network-scripts/ifcfg-eth2` 和 `eth2:1` 的文件内容所示：

```bash
# /etc/sysconfig/network-scripts/ifcfg-eth2
DEVICE=eth2
BOOTPROTO=none
BROADCAST=192.168.2.255
HWADDR=00:03:47:3B:EB:6F
IPADDR=192.168.2.201
NETMASK=255.255.255.0
NETWORK=192.168.2.0
ONBOOT=yes
TYPE=Ethernet
ONPARENT=yes
```

```bash
# /etc/sysconfig/network-scripts/ifcfg-eth2:1
DEVICE=eth2:1
BOOTPROTO=none
BROADCAST=192.168.3.255
HWADDR=00:03:47:3B:EB:6F
IPADDR=192.168.3.201
NETMASK=255.255.255.0
NETWORK=192.168.3.0
ONBOOT=yes
ONPARENT=yes
TYPE=Ethernet
```

# 手动激活和禁用网络接口

可以使用 `ifup` 和 `ifdown` 命令手动激活或禁用网络接口。要禁用 `eth2`，请运行以下命令：

![](img/3f35ec29a294974bc1a4fdae3ae46652_460_0.png)

```bash
# ifdown eth2
# ifdown ifcfg-eth2
```

执行以下任意命令来重新激活 `eth2`：

```bash
# ifup eth2
# ifup ifcfg-eth2
```

要停用 `eth2:1`，请运行以下任意命令：

```bash
# ifdown eth2:1
# ifdown ifcfg-eth2:1
```

执行以下任意命令来重新激活 `eth2:1`：

```bash
# ifup eth2:1
# ifup ifcfg-eth2:1
```

# 向 /etc/hosts 文件添加 IP 地址和主机名

你需要为每个单独的 IP 地址选择分配的主机名。例如，`eth2` 上配置的四个 IP 地址需要唯一的主机名，如 `server1`、`server2`、`server3` 和 `server4`。这些条目将所示添加到 `/etc/hosts` 文件中：

```
192.168.2.201 server1 db01 # 第逻辑服务器
192.168.3.201 server2 db02 # 第二个逻辑服务器
192.168.4.201 server3 db03 # 第三个逻辑服务器
192.168.5.201 server4 db04 # 第四个逻辑服务器
```

文件中的每行第一列包含一个 IP，第二列跟随一个官方（或规范）主机名。你也可以为每个条目定义一个或多个别名（上述示例中的 `db01`、`db02`、`db03` 和 `db04`）。官方主机名和一个或多个别名允许你为单个 IP 地址分配多个主机名。这使得可以使用任何一个主机名来访问系统。

`/etc/hosts` 文件通常用于仅访问局域网上的系统时。该文件必须在每个单独的系统中进行维护，并在需要更新时进行编辑。

# 通过网络配置器配置网络接口

若要在 `rh01` 上成功配置具有 C 类 IP 地址 `192.168.2.201`、默认子网掩码 `255.255.255.0` 和广播地址 `192.168.2.255` 的网络接口 `eth2`，请按照以下步骤使用网络配置器：
