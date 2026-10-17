
完成这些操作后，只需执行 `pon` 命令进行连接，执行 `poff` 命令断开连接即可。你可以根据需要创建任意数量不同的配置文件，并使用命令 `pon filename` 启动特定的配置，同样使用 `poff` 命令断开连接。

> 注意
>
> 许多软件调制调器无法在 Linux 下工作，因为制造商不会发布关于它们的编程信息，也不会提供 Linux 驱动程序。外部端口调制调器或 ISA 总线调制调器几乎总是有效的；USB 和 PCI 调制调器则有问题。建议使用你的调制调器名称和型号进行 Google 搜索，看看他人是如何解决该特定调制调器问题的。本章最后列出了软件调制调器性网站的链接。

# 排除连接故障

`tld.org` 的 Linux 项目为配置和排除这些连接故障提供了许多深度资源。Google 是处理这些连接特定问题非常有价值的工具。有关许多其他有用的参考，请参见本章末尾的“参考文献”部分。

以下是多年经验总结的一些故障排除提示：

- 如果你的调制调器连接后立即挂断，你你可能使用了错误的密码或拨打了错误的号码。如果密码和电话号码正确，可能是身份验证协议问题。
- 如果你已连接但无法访问网站，很可能是域名解析问题，意味着 DNS 没有正常工作。如果昨天还能用，而你没有“调整”过相关文件，那么可能是 ISP 端的问题。请打电话询问。
- 务必确保所有设备都已插好。再次检查（再检查一遍）。
- 如果调制调器在 Windows 中可以工作但在 Linux 中无论你怎么做都不行，那么它可能是软件调制调器，无论包装上是怎么说的。
- 如果一切突然停止工作（且你没有看到冒烟），这可能是 ISP 或电话公司的故障。休息一下，给他们一点时间修复。
- 永远不要在睡眠不足或咖啡因过量时配置网络连接；你只能在明天重做。

## 相关的 Ubuntu 和 Linux 命令

在 Ubuntu 系统中管理网络连接性时，你将使用这些命令：

- `dhclient`—自动获取并为网卡（NIC）设置 IP 信息。
- `ethereal`—GNOME 图形网络扫描器。
- `ufw`—Ubuntu 的基本防火墙。
- `ifconfig`—显示并管理 Linux 网络设备。
- `iwconfig`—显示并设置无线网络设备参数。
- `route`—显示并设置 Linux 内核路由表。
- `ssh`—OpenSSH 远程登录客户端，telnet 的首选替代方案。
- `nm-connection-editor`—Ubuntu 用于配置网络连接的 GUI 工具。

## 参考文献

https://help.ubuntu.com/10.04/serverguide/C/network-configuration.html—Ubuntu 的官方网络帮助。

www.ietf.org/rfc.html—前往搜索或获取意见征求（RFC）列表。

www.oth.net/dyndns.html—动态服务提供商列表，请访问此网站。

www.isc.org/products/DHCP/dhcp3-README.HTML—此站提供的 DHCP README 文件。

www.ieee.org—电气电子工程师协会（IEEE）网站。

Joe Casad, *Sams Teach Yourself TCP/IP Network Administration in 21 Days*, Sams Publishing, ISBN: 0-672-31250-6.

- Craig Hunt and Gigi Estabrook, *TCP/IP Network Administration*, O'Reilly Publishing, ISBN: 1-56592-322-7.
- Frank J. Derfler, Frank Derfler, and Jeff Koch, *Practical Networking*, Que Publishing, ISBN: 0-7897-2252-6.
- Steve Litt, *Samba Unleashed*, Sams Publishing, ISBN: 0-672-31862-8.
- Ralph Droms and Ted Lemon, *The DHCP Handbook*, Sams Publishing, ISBN: 0-672-32327-3.

# 第 18 章

## 使用 SSH 和 Telnet 进行远程访问

## 本章内容

- 设置 Telnet 服务器
- Telnet 对比 SSH
- 设置 SSH 服务器
- SSH 工具
- 虚拟网络计算
- 参考文献

远程控制你的系统是使用 Ubuntu 可以做的最酷酷的事情之一。只需少量配置，你就可以以各种方式从任何 Linux 机器连接到另一台计算机。如果你只是想快速检查某些东西，或者带宽有限，你可以选择仅使用命令行，但也可以直接连接到。

### 设置 Telnet 服务器

Telnet 是一个旧的服务。服务器会返回“Welcome to babbage, Ubuntu 10.04 LTS”，这是一个自定义消息。你的机器将做出类似的响应。这可能是不安全的：对于一台可能从安全网络外部访问的机器，提供版本号绝不是秘密手段。事实上，即使使用 Ubuntu 也是值得商榷。在这种情况下，你可以编辑 `/etc` 目录下的 `issue` 和 `issue.net` 文件来更改显示的消息。

> 提示 服务器会返回“Welcome to babbage, Ubuntu 10.04 LTS”，这是一个自定义消息。你的机器将做出类似的响应。这可能是不安全的：对于一台可能从安全网络外部访问的机器，提供版本号绝不是秘密手段。事实上，即使使用 Ubuntu 也是值得商榷。在这种情况下，你可以编辑 `/etc` 目录下的 `issue` 和 `issue.net` 文件来更改显示的消息。

使用 Telnet 连接到不同的计算机，使用网络上该计算机的 IP 地址而不是你自己的。你可以 telnet 到本地网络和互联网，连接到任何在开放端口运行服务器的计算机。

Telnet 使用端口 23，但你可以通过在 IP 地址后添加端口号来使用其他端口，例如此示例所示，我们连接到端口 110 以以测试 POP3 连接/服务器：

```
mattew@seym-$ telnet 192.168.1.102 110
```

## Telnet 与 SSH

尽管 Telnet 仍然作为一种万备未然的最后选择存在，但 SSH 在几乎每一个方面都优于它。Telnet 速度快，但不安全。正如前面提到的，它以明文形式发送你的所有文本（包括密码），任何拥有相应工具的人都可以读取。相比之下，SSH 对你所有的通信都进行加密，虽然更消耗资源，但更安全——即使政府安全机构出于某种原因嗅探你的数据包，破解其加密仍然非常困难。

Andy Green 在 fedora 邮件列表上发帖时完美地总结了 Telnet 的状况：“由于 Telnet 众所公认为会助长邪恶，因此默认情况下不启用 `telnetid` 服务。” 值得注意这一提示：Telnet 仅能作为最后手段使用。

## 设置 SSH 服务器

如果尚未安装，可以通过 Synaptic 添加 `openssh-server` 软件包来安装 OpenSSH 服务器。你可能猜到了，`sshd` 是 SSH 守护进程的名字。

首先，配置你的防火墙允许通过 22 端口进行连接。如果此端口被阻塞，你将无法使用 SSH。请参阅第 19 章获取此类操作帮助。

SSH 有两个不同的版本：SSH1 和 SSH2。后者更新、更安全、功能更多，并且是 Ubuntu 的默认设置。最好禁用对 SSH1 客户端的支持，以免旧客户端能够连接。这通过 `/etc/ssh/sshd_config` 文件中的此行实现：

```
Protocol 2
```

如果你没有其他选择且绝对必须允许旧客户端连接，请添加新的一行：

```
Protocol 1
```
