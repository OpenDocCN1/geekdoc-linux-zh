

## 第 21 章：网络配置与安全

此条目中的 `auto` 行表示系统启动时接口 `eth1` 将自动启用。条目中的 `iface` 行标识了 `eth1` 接口定义的开始，它是一个使用 `dhcp` 获取配置信息的 TCP/IP (inet) 设备。`wireless-essid` 项定义了该条目连接的无线网络名称。如果你想连接到任何可用的开放无线网络，可以使用关键字代替指定特定的 `wireless-essid`。

像这样的条目用于开放无线网络。与 WEP 无线网络相关的条目至少需要额外的一个条目来指定无线密钥，如下例所示：

```
auto eth1
iface eth1 inet dhcp
wireless-essid vwh
wireless-key 0102030405
```

如果你想要连接的无线网络采用 WPA 认证，你将不得不安装并配置如 `wsupplicant` 的包，并将该包集成到你的无线配置条目中。遗憾的是，描述如何安装和配置该包超出了本节的范围。有关使用比 WEP 更强大的无线安全机制的更多信息，请参阅 http://ubuntuforums.org/showthread.php?id=202834 论坛。

你也可以为无线接口定义静态 IP 地址，如下例：

```
auto eth1
iface eth1 inet static
address 192.168.6.42
netmask 255.255.255.0
gateway 192.168.6.1
wireless-essid vwh
wireless-key 0102030405
```

`/etc/network/interfaces` 文件为配置相当简单或不经常更改的网络接口提供了一种简单、低开销的机制。本节中的示例仅是该文件中可能条目的一山角，但识别了最重要的项。有关该文件中用于以太网接口的可能条目的完整信息，请在任何命令行界面输入命令 `man 5 interfaces` 来查看该文件的在线页面。网络是查找该文件中与无线网络配置相关的关键字信息的最佳资源。

## 第二部分：面向桌面用户的 Ubuntu

### 配置宽带调制解调器和拨号连接。

尽管如今宽带网络访问已很常见，但使用 PPP（点对点协议）等协议的拨号连接仍然是一些人连接互联网的方式。根据你所在的地理位置，这可能是你连接互联网的唯一选择。遗憾的是，许多现代调制解调器是所谓的 Win-modems，通过使用 Microsoft Windows 设备驱动程序和操作系统本身进行调制/解调（MODulation/Demodulation）来节省硬件成本，因此命名。遗憾的是，这类设备很少支持 Linux。访问 http://linmodems.org 了解你的调制解调器是否为 Win-modem，以及是否有可以在 Linux 上运行的软件。

现在使用调制解调器连接网络已很少见，因此 Ubuntu 系统默认不安装用于调制解调器配置和设置的包。如果你需要使用调制解调器并且有一个可以在 Linux 系统上工作的解调器，图形化的 `gnome-ppp` 和 `ppp` 包可以让你轻松地配置和启动基于调调器的连接。同样，Ubuntu 仓库中提供的 `wdwial` 包是一个极好的命令行工具，用于通过调制解调器启动 PPP 或 SLIP 连接。请查看 `wdwial` 的手册页、其常见问题解答 (http://alumnit.ca/wiki/index.php?page=WdialFAQ) 或其主页 (http://freshmeat.net/projects/wdwial/index.php) 获取有关配置和使用该包的信息。如果你正在读这里，我为没有详细讨论这些包表示歉，但我不再有拨号账户了（也没有足够的线路来测试我地下室里那堆旧的调制解调器）。

### 使用网络工具进行网络测试

为了保持易用图形网络工具的传统，Ubuntu 提供了一个方便的工具，可以简化任何网络接口的当前配置。Ubuntu 提供了 GNOME 的 Network Tools 应用程序，为你提供网络配置信息的图形化显示，并方便访问各种网络工具。选择“System -> Network Tools”菜单项启动 Network Tools 应用程序。这将显示一个如图 21-11 所示的对话框。

默认情况下，Network Tools 应用程序显示有关系统环回接口的信息。要查看特定接口的信息，点击“Network Device”下拉菜单并选择你感兴趣的以太网接口。图 21-11 实际上显示了主以太网接口 `eth0` 或你测试之一的信息。

786

## 第 21 章：网络配置与安全

图 21-11
Network Tools 应用程序中 eth0 的信息

![](img/1a233c34336fbf5a85d6eb785e401709_826_0.png)

识别一个以太网接口当前配置最简单、最快的方法可能是在 xterm 或 GNOME Terminal 窗口中运行 `ifconfig -name interface-command`，它的显示的内容如下：

```
$ ifconfig eth0
Link encap:Ethernet HWaddr00:16:EC:CA:AE:20
      inet addr:192.168.6.6 Bcast:192.168.6.255
      netmask:255.255.255.0 scope:192.168.6.1
      UP,BROADCAST,RUNNING,MULTICAST,mtu:1500 metric:1
      inet6 addr:fe80::26:ff:feca:ae20/64 scope:link
      collision:0 txuelen:0
      RX bytes:12108607 (11.5 MiB) TX bytes:4603767 (4.3 MiB)
```

如你所见，`ifconfig` 提供的接口信息的文本显示与图 21-11 中更友好的显示相比，需要一定的解读。

## 第二部分：面向桌面用户的 Ubuntu

除了更易读的基础网络配置显示外，Network Tools 应用程序还支持多种标准网络工具信息的图形化显示，这些工具传统上只在文本模式下运行。Network Tools 应用程序提供的标签及其对应的作用从左到右如下：

- **Devices**（设备）：显示每个可用网络接口的配置和流量摘要。这对应于传统的 Linux/UNIX 命令行 `ifconfig` 提供的信息。
- **Ping**：通过向指定主机或 IP 地址发送数据包来显示连接性和可用性信息，并显示经过时间和成功/失败。这对应于传统的 Linux/UNIX 命令行 `ping` 程序提供的信息。
- **Netstat**：显示系统上所有活动且可用的 TCP 和 UDP 端口的状态信息。这对应于传统的 Linux/UNIX 命令行 `netstat` 程序提供的信息。
- **Traceroute**：显示通信到指定主机经过的系统以及每个系统间通信所需的时间（称为“跳”）。这对应于传统的 Linux/UNIX 命令行 `traceroute` 程序提供的信息。
- **Port Scan**（端口扫描）：显示指定远程机器上可用端口和服务的信息。这大致对应于传统的 Linux/UNIX 命令行 `nmap` 程序提供的信息。
- **Lookup**（查询）：显示指定系统的 IP 地址信息和可用 DNS 别名。这大致对应于 `nslookup` 或 `host` 程序提供的信息。
- **Finger**：显示特定用户或指定主机的个人信息。这对应于传统的 Linux/UNIX 命令行 `finger` 程序提供的信息。现在很少主机提供此类信息。
- **Whois**：显示指定 Internet 域名的注册人和技术联系人信息。这对应于传统的 Linux/UNIX 命令行 `whois` 或 `whois` 程序提供的信息。

作为 Network Tools 应用程序提供的信息和显示示例，图 21-12 显示了主机 `www.vivisim.com` 在 Lookup 标签页上的 DNS 主机名查询信息。

