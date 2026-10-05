

# 第 30 章 与 Windows 协作

此功能非常有用。按照表 30.1 所示，添加以下 PAM 会话配置文件：

```
session required pam_mkhomedir.so umask=0022 skel=/etc/skel
```

通过此配置，PAM 会创建八进制权限为 755 的主目录，并从 /etc/skel 拷贝账户配置文件。

你可能还希望将本地系统的访问限制在特定 Active Directory（AD）组的用户。要实现这一点，请在 PAM 会话配置文件中添加以下行：

```
session required /lib/security/$ISA/pam_winbind.so use_first_pass require_membership_of=unix_users
```

在这里，只有 AD 组 unix_users 中的用户才能登录。

## winbind 的替代方案

虽然“免费”的 Active Directory 客户端方案运行良好，但它容易出错且充满了复杂性。对于希望从知名的第三方获得相对轻松的安装和故障排除支持的管理员来说，存在替代方案。

Likewise Software 的产品为超过 100 种 Linux 发行版和 UNIX 变体自动化了 winbind、名称服务切换（nss）、PAM 和身份映射配置，包括书中引用的所有示例。Likewise 还包含一个组策略对象代理，允许对启用 AD 的 UNIX 系统进行集中化配置。多个 GUI 插件（包括管理控制台和 Active Directory 插件）简化了安装和配置。提供免费限制版，或者你可以付费购买支持和完整功能。详情请参阅 likewise.com。

另一个避开 winbind 的选项是名为 Authentication Services 的工具。它提供了与 Quest 工具许多相同的功能，但增加了额外的组策略管理功能。请准备好钱包，因为 Quest 的产品并不便宜。请访问 quest.com/authentication-services 了解完整范围。

## 30.10 推荐阅读

TERSTRA, JOHN H. Samba-3 by Example: Practical Exercises to Successful Deployment (2nd Edition). Upper Saddle River, NJ: Prentice Hall PTR, 2006. (此书的在线版本可在 samba.org 获取。)

TERSTRA, JOHN H., JELMER R. VEROI. The Official Samba-3 HOWTO and Reference Guide (2nd Edition). Upper Saddle River, NJ: Prentice Hall PTR, 2006. (此书的在线版本可在 samba.org 获取。)

## 30.11 练习

- E30.1 为什么你想要阻止 Samba 服务器上端口 137–139 和 445 的互联网访问？

- E30.2 在 Windows 机器上安装 Cygwin 软件，并在 rxvt 中 ssh 连接到 UNIX机器。你发现它与 PuTTY 有什么不同？

- E30.3 在实验中，比较通过 Samba 访问文件的客户端与从原生 CIFS 服务器（即 Windows 机器）访问文件的性能。如果你的两个测试服务器硬件不同，请设计一种方法来调整硬件差异，使比较结果更能反映服务器软件的性能。（可能需要 root 权限。）

- E30.4 在实验中，使用如 tcpdump 或 Wireshark 等数据包分析器监控 Windows 与 UNIX 服务器之间的 telnet 会话。获取并安装 PuTTY 软件并重复监控。在每种情况下，你用数据包分析器可以看到什么？（需要 root 权限）

- E30.5 设置一个 Samba 打印服务器，为其共享的所有打印机提供 Windows 打印机驱动程序。确保打印机带有合理的默认配置。

- E30.6 配置你选择的系统身份验证到 Active Directory 环境。确保密码更改有效，并且新用户在登录时会自动创建主目录。

# 31 串口设备与终端

一个拥有 40 多年历史的操作系统无疑会携带着一些“遗留问题”。一些人会将对串口设备的支持归为此类，认为这这是一项过时的技术，最好被遗忘。与如今的 USB 等多兆比特串口接口相比，传统的串口端口可能确实太慢、太繁琐而变得没有价值。

事实上，对串口接口的理解是任何系统管理员工具箱中必不可少的一部分。无论好坏，UNIX 命令行界面都是基于古老的串口终端概念，相关的命令和控制结构仍在在使用。即使你从未离开硬接终端 50 步之内，你仍然在使用相同的底层操作系统设施，或者 Linux 桌面实际上是一个伪终端（pseudo-terminal），你通过网络登录时看似连接的设备也是如此。

真实的 RS-232C 串口端口仍然存在。它们不再是过去那样的通用设施，但在几种情况下仍然重要。它们是启动所有类型硬件设备的共同标准，从无人值守的企业级服务器管理器到指甲盖大小的嵌入式系统（包括自定义硬件项目）。你可以使用这种媒介

## RS-232C 标准

与遗留系统进行通信。有时你可能会遇到真实的硬接终端，例如在制造车间。

本章介绍了在现代世界如何连接和使用基于 RS-232 的串口设备。前几节介绍了串口硬件和布线的迭代。然后，从第 1171 页，我们讨论了支持硬接终端和……的软件基础设施。

## 31.1 RS-232C 标准

大多数 RS-232 标准规定了图 A 所示每个信号的电气特性和含义。

| 引脚 | 功能 | 引脚 | 标识 |
|---|---|---|---|
| 1 | FG | 14 | STD |
| 2 | TD | 15 | TC |
| 3 | RD | 16 | SR |
| 4 | RTS | 17 | RC |
| 5 | CTS | 18 | |
| 6 | DSR | 19 | SRS |
| 7 | SG | 20 | DTR |
| 8 | DCD | 21 | SQ |
| 9 | | 22 | RI |
| 10 | | 23 | DRS |
| 11 | | 24 | SCTE |
| 12 | SDCD | 25 | BUSY |
| 13 | SCTS | | |

不像 USB 和以太网等连接标准，RS-232 需要你知道连接的设备类型。存在两种接口配置：DTE（终端设备）和 DCE（数据通信设备）。DTE 和 DCE 具有相同的引脚，但它们对 RS-232 信号的解释不同。

每个设备都配置为 DTE 或 DCE；少数设备支持两者，但不同同时支持。计算机、终端和打印机通常是 DTE，而大多数是 DCE。

