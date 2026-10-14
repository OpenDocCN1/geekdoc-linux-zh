
`matthew@semour:~$ sudo ifconfig eth1 0.0.0.0 up`

```
使用 `adsl-setup` 命令配置你的系统，如下：
```

点击此处查看代码图片

```
matthew@semour:~$ sudo /sbin/adsl-setup
```

你将看到一个文本提示，要求输入用户名和用于连接的以太网接口（例如 `eth1`）。然后，你会被要求使用“按需”服务或保持连接始终开启（由 root 操作员断开）。如果需要，你还可以设置一个秒级的超时时间。如果你还没有配置系统的 `/etc/resolv.conf` 文件，将会被要求输入 ISP DNS 服务器的 IP 地址。

之后，系统会提示你输入两次密码，并必须选择使用的防火墙类型和 IP 伪装（你之前在本章较早的“在 Ubuntu 中使用 IP 伪装”章节中学习过 IP 伪装）。实际配置将自动完成。在今天，使用防火墙至关重要，除非你打算自己编写一套防火墙规则（对此的讨论超出了本书的范畴）。在你选择完防火墙和 IP 伪装设置后，系统要求你确认、保存并实施这些设置。你还有一个允许用户管理连接的选择，这对家庭用户来说是一个非常实用的选项。

系统文件 `/etc/sysconfig/network-scripts/ifcfg-ppp0`、`/etc/resolv.conf`、`/etc/ppp/pap-secrets` 和 `/etc/ppp/chap-secrets` 将会被修改。

配置完成后，使用 `adsl-start` 命令启动连接和 DSL 会话，如下：

点击此处查看代码图片

```
matthew@seymour:~$ sudo /bin/adsl-start
```

DSL 连接应该是瞬间完成的，但如果发生问题，请通过检查调制调器上的状态 LED 灯来确认你的 DSL 模型正在与电话公司的局端通信。由于不同的调制调器不同，请咨询你的调制调器用户手册。

确保所有电缆都已正确连接，接口已正确配置，并且你在设置脚本中输入了正确的信息。

如果启用了 IP 伪装，局域网中具有相同子网地址（例如 `192.168.0.XXX`）的其他计算机可以使用互联网，但它们需要 `/etc/resolv.conf` 名称服务器条目以及一个以连接 DSL 的计算机为网关的路由条目。例如，如果主机计算机为 `192.168.0.1`，局域网上的其他计算机使用 `192.168.0.XXX` 范围内的地址，请在每台计算机上如下使用 `route` 命令：

点击此处查看代码图片

```
matthew@seymour:~$ sudo route add default gw 192.168.0.1
```

注意，如果每台计算机都有一个包含局域网主机名和 IP 地址条目的 `/etc/hosts` 文件，你可以使用主机名代替。要停止连接，请使用 `adsl-stop` 命令：

点击此处查看代码图片

```
matthew@seymour:~$ sudo /bin/adsl-stop
```

# 配置拨号上网访问

大多数 ISP 都提供支持 PPP 的拨号连接，因为它是在串行链上传输 TCP/IP 的一种快速且高效的协议。PPP 是为双向网络设计的；TCP/IP 为数据提供传输协议。Ubuntu 用户面临的一个障碍是如何使用 PPP 并连接到互联网。使用它并不需要理解 PPP 协议的细节，而且设置 PPP 连接非常简单。你可以使用命令行手动配置 PPP 连接，也可以在 X 会话期间使用 Ubuntu 的网络配置工具进行图形化配置。每方法产生相同的结果。

PPP 使用系统中的几个组件。第一个是名为 `pppd` 的守护进程，它控制 PPP 的使用。第二个是名为高级数据链路控制（HDLC）的驱动程序，它控制两台机器之间的信息流。PPP 的第三个组件是一个名为 `chat` 的程序，当你需要时会拨号连接的另一端。尽管 PPP 有许多“可调优”参数，但默认设置适用于大多数情况。

Ubuntu 包含了一些实用的工具让你的拨号连接运行起来。在会话中，我们将查看两种可以让你快速上网的选项。

第一种方法使用 `pppconfig` 配置连接，这是一个命令行工具，可帮助你配置特定的拨号连接设置。

输入以下命令：

点击此处查看代码图片

```
matthew@seymour:~$ sudo pppconfig
```

在第一次连接之前，你需要使用这些命令将自己加入 `dip` 和 `dialout` 组：

点击此处查看代码图片

```
matthew@seymour:~$ sudo adduser USERHERE dip
matthew@seymour:~$ sudo adduser USERHERE dialout
```

完成这些操作后，你可以创建所需的多个配置文件（profile）。将 `USERHERE` 替换为你的实际用户名。

要停止连接，请使用命令：

```
matthew@seymour:~$ sudo pppconfig
```

## 注意

许多调制调器由于缺少驱动程序无法在 Linux 下工作。请在本章末尾检查兼容性。

# 故障排除

以下是从多年经验中总结的故障排除技巧：

- 如果你的调制调器连接后立即挂断，可能是身份验证问题。
- 始终确保所有电缆都已插好。
- 如果在 Windows 中可以使用但无论你怎么做在 Linux 中都无法使用，可能是 ISP 或电话公司的故障。休息一下，给他们一些时间。
- 永远不要睡眠不足或咖啡因过量时配置连接；你将不得不重来。

# 相关的 Ubuntu 和命令

在管理系统网络连接时请使用这些命令：

- `dhclient`: 自动为网卡获取并设置 IP
- `ethereal`: GNOME 图形化网络扫描器
- `ufw`: Ubuntu 的基础防火墙
- `ifconfig`: 显示和管理 Linux 网络设备
- `iwconfig`: 显示并设置无线网络设备
- `route`: 显示和管理 Linux 路由
- `ssh`: OpenSSH 远程登录客户端，telnet 的首选替代品
- `nm-connection-editor`: Ubuntu 网络配置 GUI

# 参考

- https://help.ubuntu.com/14.04/serverguide/networking.html: Ubuntu 官方网络帮助。
- www.ietf.org/rfc.html: 在此处搜索或获取意见请求（RFC）。
- www.oth.net/dyndns: 动态 DNS 服务提供商列表。
- www.isc.org/products/DHCP/: DHCP 网站。
- www.ieee.org: 电子工程师协会（IEEE）网站。
- Joe Casad, *Teach TCP/IP Network Administration in 21 Days*, Sams Publishing, ISBN: 0-672-31250-6.
- Craig Hunt and Gigi Estabrook, *TCP/IP Network Administration*, O’Reilly Publishing, ISBN: 1-56592-322-7.
- Frank J. Derfler, Frank Derfler, and Jeff Koch, *Practical Networking*, Que Publishing, ISBN: 0-7897-2252-6.
- Steve Litt, *Samba Unleashed*, Sams Publishing, ISBN: 0-672-31862-8.
- Ralph Droms and Ted Lemon, *The DHCP Handbook*, Sams Publishing, ISBN: 0-672-32327-3.

## 第 19 章. 使用 SSH、Telnet 和 VNC 进行远程访问

本章内容

- 设置 Telnet 服务器
- Telnet 与 SSH
- 设置 SSH 服务器
- SSH 工具
- 虚拟网络计算 (VNC)
- 参考文献

远程控制系统是使用 Ubuntu 可以实现的最酷的功能之一。只需少量配置，你就可以以多种方式从任何 Linuxget 连接到另一台计算机。如果你只是想快速检查某些内容，或者带宽有限，你可以选择仅使用命令行，但你也可以直接连接到 X 服务器并获得完整的图形控制。

了解可用工具的选择很大程度上是一堂历史课。例如，Telnet 是早期通过命令行连接到另一台计算机的方法，但它已已被安全 Shell (SSH) 所取代。这并不是说你应该忽略 Telnet；你需要知道如何使用它，以便作为备用方案。然而，SSH 更受青，因为它更安全。我们在本章中将涵盖这两者。

## 设置 Telnet 服务器
