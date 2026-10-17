
```
# nmcli dev status
DEVICE      TYPE      STATE       CONNECTION
eno1        ethernet  connected   eno1
wlp0s26ulu2 wifi      connected   zoneone
virbr0      bridge    connected   virbr0
lo          loopback  unmanaged   --
virbr0-nic  tun       unmanaged   --
```

输出还可以通过使用 `-p`（pretty）选项来修改，使输出更易于人类阅读：

```
# nmcli -p dev status
====================
    Status of devices
====================
DEVICE      TYPE      STATE       CONNECTION
------------------------------------------------------------
eno1        ethernet  connected   eno1
wlp0s26ulu2 wifi      connected   zoneone
virbr0      bridge    connected   virbr0
lo          loopback  unmanaged   --
virbr0-nic  tun       unmanaged   --
```

相反，可以使用 `-t` 选项使输出更简洁，适合自动化处理：

```
# nmcli -t dev status
eno1:ethernet:connected:eno1
wlp0s26ulu2:wifi:connected:zoneone
virbr0:bridge:connected:virbr0
lo:loopback:unmanaged:
virbr0-nic:tun:unmanaged:
```

状态输出显示系统安装了两个物理设备，一个是以太网，另一个是 WiFi 设备。

`bridge`（`virbr`）条目是用于为虚拟机提供网络的虚拟设备（虚拟化的主题将从标题为“虚拟化技术概述”的章节开始介绍）。最后，环回接口是一个特殊的虚拟设备，允许系统与自身通信，通常用于执行网络诊断。

在使用 NetworkManager 时，了解设备和连接之间的区别很重要。如上所述，设备是物理或虚拟网络设备，而连接是设备连接到的网络配置。

以下命令显示系统上配置的连接信息：

```
# nmcli con show
```

| 名称 | UUID | 类型 | 设备 |
|---|---|---|---|
| zoneone | 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 | 无线 | wlp0s26ulu2 |
| eno1 | 99d40009-6bb1-4182-baad-a103941c90ff | 以太网 | eno1 |
| virbr0 | e13e9552-1765-42d1-b739-ff981668fbee | 网桥 | virbr0 |
| zonetwo | f940a2d1-8c18-4a9e-bf29-817702429b8a | 无线 | -- |
| zonethree | fd65c5e5-3e92-4e9e-b924-1b0b07b70032 | 无线 | -- |

上述输出显示 WiFi 设备（`wlp0s26ulu2`）已连接到名为 `zoneone` 的无线网络，而以太网设备（`eno1`）已连接到名为 `eno1` 的连接。除了 `zoneone` 之外，NetworkManager 还列出了另外两个名为 `zonetwo` 和 `zonethree` 的 WiFi 连接，目前均没有设备连接。

要查找分配给连接的 IP 地址，可以使用 `address` 选项使用 `ip` 工具：

```
# ip address
```

上述命令也可以缩写：

```
# ip a
```

```
. 
. 
3: wlp0s26ulu2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 74:da:38:ee:be:50 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.121/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s26ulu2
        valid_lft 57584sec preferred_lft 57584sec
. 
.
```

`ip` 命令将输出系统上检测到的所有设备的信息。例如，上述输出显示 WiFi 设备已被分配 IP 地址 `192.168.1.121`。

如果我们只想列出活动连接，可以使用 `-a` 选项使用 `nmcli` 命令：

```
# nmcli con show -a
```

| 名称 | UUID | 类型 | 设备 |
|---|---|---|---|
| zoneone | 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 | 无线 | wlp0s26ulu2 |
| eno1 | 99d40009-6bb1-4182-baad-a103941c90ff | 以太网 | eno1 |
| virbr0 | e13e9552-1765-42d1-b739-ff981668fbee | 网桥 | virbr0 |

要将 WiFi 设备连接从 `zoneone` 切换到 `zonetwo`，我们可以运行以下命令：

```
# nmcli device wifi connect zonetwo -ask
Password:
```

`-ask` 标志会导致 `nmcli` 提示用户输入 WiFi 网络的密码。要在命令行中包含 WiFi 密码（如果命令在脚本中执行则特别有用），请使用 `password` 选项：

```
# nmcli device wifi connect zonetwo password <password here>
```

`nmcli` 工具也可以按如下方式用于扫描可用的 WiFi 网络：

```
# nmcli device wifi list
IN-USE  SSID      MODE   CHAN  RATE       SIGNAL  BARS  SECURITY
        zoneone   Infra  6     195 Mbit/s 80            WPA2
*       zonetwo   Infra  11    130 Mbit/s 74            WPA1 WPA2
```

可以按如下方式停用当前活动的连接：

```
# nmcli con down <connection name>
```

同样，不活动的连接可以随时重新启用：

```
# nmcli con up <connection name>
```

当连接被关闭时，NetworkManager 会自动搜索另一个连接，激活它，并将其分配给先前连接建立的设备。为防止在此情况下使用连接，请按如下方式禁用 `autoconnect` 选项：

```
# nmcli con mod <connection name> connection.autoconnect no
```

可以使用以下命令获取有关特定连接的附加信息。这包括所有连接属性的当前值：
