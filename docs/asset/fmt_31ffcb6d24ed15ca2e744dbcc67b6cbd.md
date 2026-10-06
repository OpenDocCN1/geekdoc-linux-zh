
`no ip directed-broadcast`

```
```

但第 3 层设备不是应该停止广播的吗？这防止了网络成为此类网络攻击的中间站点。类似的命令是路由器接口上的默认值或已启用：

```
no ip directed-broadcast
```

（注：由于提供的文本在第 501 页存在大量重复的 OCR 错误，翻译已根据逻辑流进行了去重和处理。）

当发现新病毒或蠕虫时，就会创建一个新的特征码或新定义。大多数商业杀毒软件会在病毒出现后的几小时内准备好新的特征码/定义并供客户下载。那么，为什么保持杀毒软件更新到最新版本很重要呢？大多数杀毒软件在操作系统启动时启动并在此时尝试更新其特征码和定义。当计算机上发现病毒时，病毒程序通常会被隔离或删除。一些流行的杀毒软件有 McAfee、Norton、趋势科技（Trend Micro）、Sophos、AVG 等。

## 个人防火墙

计算机另一种常用的软件保护形式是个人防火墙。大多数操作系统（Windows、Mac OS 和 Linux）都配备了个人防火墙。其中某些可能默认未启用。个人防火墙通常基于数据包过滤系统，防火墙根据数据包 TCP 或 IP Header 中包含的信息来接受或拒绝入站的网络流量。某些个人防火墙提供更细粒度的控制，允许特定的主机或子集。某些个人防火墙还提供基于应用程序的防火墙，可以在其中定义信任程序。防火墙允许源自或发往信任程序的网络流量。

在 Windows 操作系统中，防火墙保护作为 Windows XP 服务包 2 的一部分引入。它已经从 Windows XP 中的简单防火墙演变为具有更细粒度的控制；Windows 7 防火墙允许数据包过滤和基于应用程序的防火墙。它还赋予了防火墙软件入站和出站控制权。在 Linux 世界，`iptables` 长期以来事实上的防火墙程序。在 Mac OS X 中，在 10.5 版本之前一直部署 `ipfw`（一种基于 BSD Linux 的防火墙）。从 10.5 版本开始，Mac OS X 转变为基于应用程序的防火墙。以下示例了如何为 Windows 7、XP、Mac OS X 和 Linux 配置防火墙设置。

### Windows 7

要启动 Windows 7 防火墙配置，请使用以下步骤：

- 1. 点击“开始”并选择控制面板 > 连接到；然后选择“系统和安全”。
- 2. 图 12-8 显示了 Windows 防火墙，它提供了 2 个选项：检查防火墙状态和允许程序通过 Windows 防火墙。

![](img/ec00be08b0c45b337e7cb610696f1b45_504_0.png)

FIGURE 12-8 Windows 7 防火墙。

选择“检查防火墙状态”以显示图 12-9 中的状态窗口。此屏幕表示对于名为“网络 3”的公共连接，防火墙已开启，且防火墙正在阻止所有不在允许程序列表中的程序连接。

![](img/ec00be08b0c45b337e7cb610696f1b45_504_1.png)

FIGURE 12-9 Windows 7: 防火墙状态。

- 4. 选择“允许程序或功能通过 Windows 防火墙”，以显示图 12-10 所示的通过 Windows 防火墙通信的允许程序窗口。此屏幕显示了根据所使用的网络位置允许通过防火墙的程序。如果 Windows 7 计算机第一次建立新的网络连接，Windows 7 会提示用户识别此网络连接是用于家庭/工作（私有）还是公共位置。然后会相应地调整防火墙和安全设置。

![](img/ec00be08b0c45b337e7cb610696f1b45_505_0.png)

FIGURE 12-10 Windows 7: 允许的程序。

- 5. Windows 7 提供高级防火墙设置。使用“高级设置”选项来控制计算机的入站和出站流量。高级设置防火墙选项可以在图 12-9 防火墙状态窗口的左列找到。图 12-11 显示了带有高级安全性的防火墙。

![](img/ec00be08b0c45b337e7cb610696f1b45_505_1.png)

FIGURE 12-11 Windows 7: 高级设置。

- 6. 下一个示例检查了 Windows 7 中的一个入站“Ping 请求”规则。在高级安全窗口中；你会发现选中“入站规则”时，有很多规则，但并非所有规则已启用。已启用规则由“启用”列中的值指示。在“启用”列右侧是“操作”列。此列显示“允许”以允许连接或“阻止”以拒绝连接。

双击中间窗格中的“Ping 请求”规则，将显示如图 12-12 所示的 Ping 属性窗口。在此窗口的“常规”选项卡中，规则设置为“已启用”，且操作为“允许”连接。

![](img/ec00be08b0c45b337e7cb610696f1b45_506_0.png)

FIGURE 12-12 Windows 7: Ping 请求属性。

选择“协议和端口”选项卡以显示图 12-13 所示的窗口。这说明了防火墙如何通过将其协议定义为 ICMPv4 协议来管理 Ping 请求。“自定义”窗口将弹出自定义 ICMP 设置，显示已选中了回显请求（Echo Request）ICMP 类型。

![](img/ec00be08b0c45b337e7cb610696f1b45_506_1.png)

FIGURE 12-13 Windows 7: Ping 请求。

### Mac OS X

要启动 Mac OS X 防火墙，请使用以下步骤：

- 1. 转到系统偏好设置并选择“安全性”。
- 2. 在“安全性”窗口中，选择“防火墙”。防火墙显示的状态如图 12-14 所示。

![](img/ec00be08b0c45b337e7cb610696f1b45_507_0.png)

FIGURE 12-14 Mac OS X: 防火墙。

- 3. 点击“高级”按钮打开高级设置，如图 12-15 所示。

**阻止入站连接：** 此选项阻止所有必需的入站连接。

**自动允许签名软件：** 此选项允许签名的软件接收入站连接。

**启用隐身模式：** 这将不会响应或确认访问此计算机的尝试。

![](img/ec00be08b0c45b337e7cb610696f1b45_507_1.png)

FIGURE 12-15 Mac OS X: 高级设置。

| 阻止入站连接 |
| :--- |
| 此选项阻止所有必需的入站连接。 |
| 自动允许签名软件 |
| 此选项允许签名的软件接收入站连接。 |
| 启用隐身模式 |
| 这将不会响应或确认访问此计算机的尝试。 |

### Linux

要启动 Linux 防火墙 (`iptables`)，请使用以下步骤：

- 1. 使用 `iptables` 命令。例如，要查看防火墙配置，只需以 root 身份执行 `iptables --list` 命令。
- 2. `iptables --list` 命令的输出如图 12-16 所示。它显示了链（chains）的列表：链可以由防火墙规则或其他链组成。在此示例中，唯一包含规则的链是 RH-Firewall-INPUT。该链允许入站 HTTP、HTTPS、SSH、SMTP、域名 (DNS) 和 IMAP 流量，并拒绝任何不匹配列表的入站流量

```
ssh 11030

root@localhost:~ (iptables) --list

Chain INPUT (policy ACCEPT)

target destination --source destination

RH-Firewall-1-INPUT all -- anywhere anywhere

Chain FORWARD (policy ACCEPT)

target destination --source destination

RH-Firewall-1-FORWARD all -- anywhere anywhere

Chain OUTPUT (policy ACCEPT)

target destination --source destination

Chain default (2 references)

ACCEPT udp -- anywhere anywhere

ACCEPT tcp -- anywhere anywhere

ACCEPT icmp -- anywhere anywhere

ACCEPT ipv6-anywhere -- anywhere anywhere

ACCEPT any -- anywhere anywhere state RELATED,ESTABLISHED

ACCEPT tcp -- anywhere anywhere state NEW tcp:http

ACCEPT tcp -- anywhere anywhere state NEW tcp:ssh

ACCEPT tcp -- anywhere anywhere state NEW tcp:smtp

ACCEPT udp -- anywhere anywhere state NEW udp:dns

ACCEPT udp -- anywhere anywhere state NEW udp:domain

ACCEPT udp -- anywhere anywhere

REJECT all -- anywhere anywhere

REJECT all -- anywhere anywhere reject-with icmp-host-prohibited
```
