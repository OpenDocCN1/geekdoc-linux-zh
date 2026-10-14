
port 1194

dev tun

remote whereiw.com

```
# 第二部分：适用于桌面端用户的 Ubuntu
```

tls-client

ca ca.crt

cert vonhagen.crt

key vonhagen.key

tu-test

tun-mtu 1500

tun-mtu-extra 32

msffif 1450

pull

comp-lzo

verb 0

```

OpenVPN 配置文件中的这些 `remote`、`ca`、`cert` 和 `key` 条目对于每个 VPN 连接都是不同的。`remote` 关键字标识运行连接 OpenVPN 服务器的主机，`ca` 关键字标识包含远程站点根证书机构（CA）证书的文件，`cert` 关键字标识包含客户端证书的文件，`key` 关键字标识客户端的私钥。在本示例中，后者是用户特定的，但也可以用于启用站点范围连接。用户特定的密钥通常由 root 用户所有，并存储为 `600` 权限，因此只有 root 用户读取。

问题在于当私钥需要密码才能使用时，OpenVPN 连接是否可以在启动时自动创建。系统管理员可以使用 `--pass-file:password` 选项创建不需要密码的密钥文件（其中 password 是设置时自动使用的密码）。存储用户名和密码信息通常是不支持的，因为在配置文件中以明文存储这些信息是一个巨大的安全漏洞。

执行以下命令 `/etc/init.d/openvpn restart` 来启动所有连接：

```
sudo /etc/init.d/openvpn restart
```

一种更优雅的方法是使用以下命令，在不中断现有连接的情况下启动 VPN：

```bash
sudo openvpn --config config.conf
```

`--config` 选项指定配置文件名。`--daemon` 选项允许 OpenVPN 在后台运行。`--dev` 选项指定你想要启动的接口类型。

除非 `/etc/openvpn` 目录中存在配置文件，否则 OpenVPN 会自动启动任何 VPN 连接。

# 第二部分：Ubuntu 桌面版用户

为特定接口分配静态 IP 地址的条目同样简单。例如，为太网接口 `eth0` 分配静态 IP 地址的条目如下：

```
auto eth0
if eth0 inet static
    address 192.168.6.64
    netmask 255.255.255.0
    gateway 192.168.6.1
```

该条目中的该行表示接口 `eth0` 将在系统启动时自动启用。该条目中的接口行标识了 `eth0` 接口定义的开始，这是一个具有静态配置的 TCP/IP (`inet`) 设备。接下来的三行定义了该接口的 IP 地址、子网掩码和网关。

## 手动 DNS 配置

如果网络接口使用静态 IP 地址，您的系统将不会从 DHCP 服务器获取 DNS 服务器地址等通用网络信息。因此，您应该手动配置并填充系统用于识别名称服务器的 `/etc/resolv.conf` 文件。这是一个使用 OpenDNS.org 开放服务器的 `/etc/resolv.conf` 示例：

```
domain vonhagen.org
nameserver 208.67.222.222
nameserver 208.67.220.220
```

该文件的第一行标识了系统在查找未指定域名的主机时应搜索的默认域名。（您可能会使用除我的主域名以外的默认域名。）您应该为该默认域名提供的任何 DNS 服务器添加条目，这些条目应该出现在 OpenDNS 等开放服务的 DNS 服务器条目之前。当您的系统尝试查找与特定主机关联的 IP 地址时，将按照它们在文件中列出的顺序查询 DNS 服务器。

有关普通公众可用的其他 DNS 服务器的信息，请参阅 `www.dnsserverlist.org`。

无线接口在 `/etc/network/interfaces` 文件中的定义也同样简单。例如，一个将太网接口 `eth1` 定义为使用 DHCP 且使用 ESSID 为 `wvh` 的无线网络的条目如下：

```
auto eth1
if eth1 inet dhcp
  wireless-essid wvh
```

## 第 21 章：网络配置与安全

该条目中的 `auto` 行表示接口 `eth1` 将在系统启动时自动启用。该条目中的 `if` 行标识了 `eth1` 接口定义的开始，这是一个使用 `dhcp` 获取其配置信息的 TCP/IP (`inet`) 设备。`wireless-essid` 条目定义了该条目应连接的无线网络名称。如果您想连接到任何可用的开放无线网络，可以使用关键字而不是指定特定的 `wireless-essid`。

此类条目对于开放无线网络是足够的。与 WEP 无线网络相关的条目则至少需要一个条目来指定无线密钥，如下例所示：

```
auto eth1
iface eth1 inet dhcp
wireless-essid vwhv
wireless-key 0102030405
```

如果您想要连接的无线网络使用 WPA 身份验证，您将需要安装并配置如 `wsupplicant` 的包，并将该包集成到您的无线配置条目中。幸运的是，描述如何安装和配置此包超出了本节的范围。请查看 `http://ubuntuforums.org/showthread.php?id=202834` 上的论坛帖子，获取更多关于使用比 WEP 更强大的无线安全机制的信息。

您也可以为无线接口定义静态 IP 地址，如下例所示：

```
auto eth1
iface eth1 inet static
address 192.168.6.42
netmask 255.255.255.0
gateway 192.168.6.1
wireless-essid vwhv
wireless-key 0102030405
```

`/etc/network/interfaces` 文件提供了一种简单、低开销的机制，用于配置相当简单或不经常更改的网络接口。本节中的示例仅是该文件中可能条目的冰一角，但识别了最重要的条目。有关该文件中用于有线太网接口的可能条目的信息，请从任何命令行界面输入 `man interfaces` 命令查看该文件的在线帮助页。网网是查找该文件中与无线网络配置相关的关键字信息的最佳资源。

## 第二部分：用于桌面的调制解调器的 Ubuntu

### 配置宽带接入接入和拨号连接

尽管宽带接入接入现在已很常见，但使用 PPP（点对点协议）等协议的拨号连接仍然是一些人连接互联网的方式。取决于您的地理位置，这可能是您连接互联网的唯一选择。遗憾的是，许多现代调制解调器是所谓的 Win-modems，它们通过使用 Microsoft Windows 设备驱动和操作系统本身进行调制/解调具有硬件意义，这使得它们更多更多。遗憾的是，取决于您的调制解调器是否是 Win-modem 或者是否有软件可以使其在 Linux 上工作。

现在使用调制解调器连接网络已很罕见，因此 Ubuntu 系统默认不安装用于调制解调器配置和设置的包。如果您需要在 Linux 系统上使用调制解调器，图形化的 `ppp` 和 `kppp` 包可以轻松地帮助您。

### 使用网络工具进行网络测试

为了保持其易用图形化工具的传统，Ubuntu 提供了一个方便的图形化工具，简化任何网络接口的当前配置。Ubuntu 提供了 GNOME 的 Network Tools 应用，提供网络配置图形界面，并方便访问各种网络工具。选择 System Administration Network Tools 启动 Network Tools 应用。这将显示类似于图 21 的对话框。

默认情况下，Network Tools 应用显示回环接口的信息。要查看特定接口的信息，请点击 Network Device 下拉菜单并选择您感兴趣的太网接口。图 21-1 实际上显示了主太网接口 `eth0` 的信息。

识别一个太网接口当前配置最简单、最快的方法始终是在 GNOME Terminal 窗口中运行 `ifconfig interface-name` 命令，这将显示如下的输出：

### ifconfig eth0
```
