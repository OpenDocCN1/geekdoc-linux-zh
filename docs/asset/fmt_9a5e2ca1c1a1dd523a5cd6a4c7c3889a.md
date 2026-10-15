
尽管现在宽带互联网已很常见，但使用 PPP（点对点协议）等协议的拨号连接仍然许多人连接互联网的方式。根据您的地理位置，这可能是您连接互联网的唯一选择。遗憾的是，许多调制调器是所谓的“Win-modems”，它们通过使用 Microsoft Windows 设备驱动程序节省硬件公司的成本，且操作系统与其命名的调制/解调（Modulation/DEModulation）绑定。遗憾的是，Linux 很少提供此类驱动程序。请访问 http://linmodems.org 获取有关您的调器是否为 Win-modem 以及可能使其在 ubuntu 上运行的软件的信息。

现在使用调制调器连接互联网很罕见，由于原因，Ubuntu 和 Ubuntu 系统默认不安装调制调器配置和连接设置的包。如果您需要使用可以在 Linux 系统上工作的调器，`gnome-pppd` 和 `ppp` 包可以轻松配置并启动基于调制调器的网络连接。同样，Ubuntu 仓库中提供的 `wvdial` 包是一个很棒命令行实用程序，用于通过调制调器启动 PPP 或 SLIP 连接。请查看 `wvdial` 的帮助页、其 FAQ (http://alumnit.net/wiki/index.php?page=WvdialFAQ) 或其首页 (http://freshmeat.net/projects/wvdial) 来配置和使用此包。如果您正在读这里，我很抱歉没有详细讨论这些包，但我不再有拨号账号了（也没有足够的电话线来测试地下室里那堆旧调器了！）

# 网络配置与安全

无线接口在您的 `/etc/network/interfaces` 文件中定义非常简单。例如，定义使用 DHCP 的以太网接口 `eth1` 以及 SSID 为 "wwhh" 的无线网络的条目如下：

```
auto eth1
iface eth1 inet dhcp
wireless-essid wwhh
```

该条目中的 `auto` 行表示接口 `eth1` 将在系统启动时自动启用。该条目中的行标识了 `eth1` 接口定义的开始，`eth1` 是一个使用 DHCP 获取配置信息的 TCP/IP (`inet`) 设备。`wireless-essid` 定义了该条目应连接的无线网络名称。如果您想连接到任何可用的开放无线网络，可以使用键而不是指定特定的 `wireless-essid`。

此类条目用于开放无线网络。与 WEP 无线网络相关的条目至少需要额外添加一个条目来指定无线密钥，如下所示：

```
auto eth1
iface eth1 inet dhcp
wireless-essid wwhh
wireless-key 0102030405
```

如果您需要使用 WPA 认证连接到想要连接的无线网络，将需要安装并配置如 `wpasupplicant` 的包，并将该包集成到您的无线配置条目中。（遗憾的是）描述如何安装和配置此包超出了本节的范围。请查看 http://ubuntuforums.org/showthread.php?t=202834 论坛帖子，获取有关比 WEP 更强大的无线安全机制的信息。

您也可以为无线接口定义静态 IP 地址，如下所示：

```
auto eth0
iface eth1 static
address 192.168.6.42
netmask 255.255.255.0
gateway 192.168.6.1
wireless-ess wwh
wireless-key 0102030405
```

`/etc/network/interfaces` 文件提供了一种简单、低开销的机制来配置相当简单或不经常更改的网络接口。本节中的示例仅触及该文件中可能条目的一角，但已经识别了最重要的条目。关于该文件中有线以太网的可能条目的完整信息，可以在任何命令行界面输入 `man 5 Interfaces` 命令来查看该文件的在线帮助页。这是查找与无线网络配置相关的该文件中关键词完整信息的最佳资源。

# 使用网络工具进行测试

无线接口在您的 `/etc/network/interfaces` 文件中定义非常简单。例如，定义使用 DHCP 的以太网接口 `eth1` 以及 SSID 为 "wwhh" 的无线网络的条目如下：

```
auto eth1
iface eth1 inet dhcp
wireless-essid wwhh
```

该条目中的 `auto` 行表示接口 `eth1` 将在系统启动时自动启用。该条目中的行标识了 `eth1` 接口定义的开始，`eth1` 是一个使用 DHCP 获取配置信息的 TCP/IP (`inet`) 设备。`wireless-essid` 定义了该条目应连接的无线网络名称。如果您想连接到任何可用的开放无线网络，可以使用键而不是指定特定的 `wireless-essid`。

此类条目用于开放无线网络。与 WEP 无线网络相关的条目至少需要额外添加一个条目来指定无线密钥，如下所示：

```
auto eth1
iface eth1 inet dhcp
wireless-essid wwhh
wireless-key 0102030405
```

如果您需要使用 WPA 认证连接到想要连接的无线网络，将需要安装并配置如 `wpasupplicant` 的包，并将该包集成到您的无线配置条目中。（遗憾的是）描述如何安装和配置此包超出了本节的范围。请查看 http://ubuntuforums.org/showthread.php?t=202834 论坛帖子，获取有关比 WEP 更强大的无线安全机制的信息。

您也可以为无线接口定义静态 IP 地址，如下所示：

```
auto eth0
iface eth1 static
address 192.168.6.42
netmask 255.255.255.0
gateway 192.168.6.1
wireless-ess wwh
wireless-key 0102030405
```

`/etc/network/interfaces` 文件提供了一种简单、低开销的机制来配置相当简单或不经常更改的网络接口。本节中的示例仅触及该文件中可能条目的一角，但已经识别了最重要的条目。关于该文件中有线以太网的可能条目的完整信息，可以在任何命令行界面输入 `man 5 Interfaces` 命令来查看该文件的在线帮助页。这是查找与无线网络配置相关的该文件中关键词完整信息的最佳资源。

## 使用网络工具进行测试

- **设备**：显示每个可用接口的配置和流量信息。这对应于传统的 Linux/UNIX 命令行 `ifconfig`。
- Ping：通过向指定的主机或 IP 地址发送数据包来显示连通性和可用性，并显示经过时间和成功失败信息。这对应于传统的 Linux/UNIX 命令行 `ping`。
- **网络统计**：显示系统上所有活跃的 TCP 和 UDP 网络端口状态信息。这对应于传统的 Linux/UNIX 命令行 `netstat`。
- **路由追踪**：显示到指定主机通信经过的系统以及每次系统通信所需的时间，以跳数的形式显示。这对应于传统的 Linux/UNIX 命令行 `traceroute` 应用。
- **端口扫描**：显示远程机器上可用的端口和服务。这大致对应于传统的 Linux/UNIX 命令行 `nmap` 应用。
- **查询**：显示指定系统的 IP 地址信息和可用 DNS 别名。这大致对应于传统的 Linux/UNIX 命令行 `nslookup` 或 `host` 应用。
- **指纹**：显示特定用户或指定主机的任何可用个人信息。这对应于传统的 Linux/UNIX 命令行 `finger` 应用。
- **Whois**：显示指定 Internet 域名的注册人和技术联系人信息。这对应于传统的 Linux/UNIX 命令行 `whos` 或 `whois` 应用。

# 第三部分 针对系统管理员的 Ubuntu 和 Kubuntu

作为 Network Tools 提供的信息和显示示例，图 25-25 显示了主机 `www.vivisim.com` 在其“查找”（Lookup）选项卡上显示的主机查找信息。

# 图 25-25

DNS 名称查找的图形化显示

![](img/e3248f698da647444405a34229bd9df5_1117_0.png)

# 系统安全防护建议

系统安全是一个开放的话题，因为它包含许多不同的方面。这些包括物理安全、登录认证、文件和文件系统保护等。关于安全主题已经有很多整本书著作，而且投入的资金也日益增加。正如本章引言提到的，由于网络化的无处不在，以及用于探测、探索和入侵远程机器的工具可用性不断提高，各种形式的安全将成为一个日益关注的问题。

以下是关于提高网络系统安全性的一些具体建议。正如你所预期的，这些建议包含了其他安全主题的方面，但也有它们自己独特的关注点：

- 如果你使用的是现成的家用网关，在投入使用之前请更改密码。如果可能，还应该更改认证用户的名称。如果因为人们没有更改默认密码导致系统被入侵一次就给我一个分硬币，我可能甚至不知道自己有多少个分硬币了，因为大多数入侵都是未被察觉的。

# 网络配置与安全
