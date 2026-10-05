

# HP-UX 配置示例

503

# $ lscan

| 硬件站 线路卡 硬件 网口接口 NM MAC HP-DLPI DLPI | 路径 地址 In# 状态 PPA ID 类型 支持 主设备# |
|---|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | 8/02/0 | 0x01... | 0 | UP | lan0 | snapo | 1 | ETHER | Yes | 130 |

# $ configlan

lan0: flags=843-UP,BROCAST,RUNNING,MULTICAST> inet 192.108.21.99
netmask fffff0 broadcast 192.108.21.255

# $ configsnap

ifsnap: no such interface

netstat -i 显示网络接口名称，netstat -nr 显示路由表：

# $ netstat -i

| 名称 | Mtu | 网络地址 | 入数据包 | 出数据包 |
|---|---|---|---|---|
| lan0 | 1500 | 192.108.21.0 | 6047 | 3648 |
| lo0 | 4136 | 127.0.0.0 | localhost.address.com | 231 | 231 |

# $ netstat -nr

| 目的/子掩码 | 网关 | 标志 | 引用 | 使用 | 接口 | Pmtu |
|---|---|---|---|---|---|---|
| 127.0.0.1 | 127.0.0.1 | UH | 0 | 231 | lo0 | 4136 |
| 192.108.21.99 | 192.108.21.99 | UH | 8 | 0 | lan0 | 4136 |
| 192.108.21.99 | 192.108.21.99 | U | 2 | 0 | lan0 | 1500 |
| 127.0.0.0 | 127.0.0.1 | U | 0 | 0 | lo0 | 4136 |
| default | 192.108.21.254 | UG | 0 | 0 | lan0 | 1500 |

lanadmin 命令显示每个接口的网络流量摘要。它还可以操作和监控接口。它是一个基于菜单的程序，带有实用的帮助引导你找到所需的信息。以下是一个显示 lan0 接口统计信息的示例：

% lanadmin

局域网在线管理，版本 1.0
Copyright 1994 Hewlett-Packard Company.
保留所有权利。

测试选择：
lan = LAN 接口管理
menu = 显示此菜单
quit = 退出管理
ter = 不显示命令
verbose = 显示命令

输入命令: lan

LAN 接口测试模式。PPA 号 = 0
clear = 清除统计数据
display = 显示 LAN 接口状态/统计
up = 1
menu = 显示此菜单
ppa = LAN 接口
quit = 退出管理，返回 shell
reset = 重置并执行 LAN 接口
specific = 进入驱动程序菜单

输入命令: display

| LAN 接口状态显示 | PPA 号 | 说明 | 类型 |
|---|---|---|---|
| 2009年6月2日 00:04:24 | 0 | lan0 | Intel PCI |
| (value) = ethernet-smacd(6) | MTU 大小 = 1500 | 速度 = 1000000 | 站地址 |
| 0x0030eea923 | 管理状态 (value) = up(1) | 操作状态 (value) = up(1) | - 入站单播数据包 = 4569
- 入站非单播数据包 = 2630
- 延迟传输 = 0
- 冲突 = 0
- 过度冲突 = 0

# HP-UX 配置其他网络参数配置，通过在 /etc/rc.config 中设置变量，可以在启动时开启 DHCP。变量名以 DHCP_ENABLE 开始。索引 [0] 指第一个接口，[1] 指第二个，依此类推。例如，

DHCP_ENABLE[0]=1 将第一个网络接口设置为 DHCP。它将从 DHCP 服务器获取 IP 地址、子掩码和其他参数。将变量设置为 0 将禁用 DHCP；你必须在配置文件中分配静态地址。如果没有 DHCP_ENABLE 子句，变量默认为 1启用bin/auto_parms 负责连接 DHCP 服务器的工作。它将 auto_parms 安全的参数输入配置文件，启动时读取。

# HP-UX 动态重新配置和调整

在 Solaris 中，你可以使用 ndd 调整许多网络参数。即时使用 ndd 的值是永久更改的，而在 /etc/rc.config 中输入是在启动时读取的。在 HP-UX 系统上，ndd -h（帮助）非常有用。如果不带参数，它会列出所有可以调整的参数。如果你指定变量名，ndd -h 会描述其最小值、最大值和默认值。更多关于 ndd 的细节请见。

# HP-UX 防火墙、过滤和 NAT

ndd 的输出声此版本的 HP-UX 允许源路由数据包。但这可能是内核的偏好，实际上 /etc/rc.config 文件禁用了这种行为：

TRANSPORT_NAME[2]=ip
NAME[2]=ip
VALUE[2]=0

这里的 2 表示在 config 中设置的十个变量中的第三个。如果你想更改下一个变量，只需添加相同的行并将 2 改为 3。遗憾的是，只能通过 config 设置 10 个参数。要手动查看和更改 ip_forward_routed 变量的值，请使用 ndd-get 和 ndd-set（语法与 Solaris 系统略有不同）：

$ ndd-get /dev/ip ip_forward_routed
0
$ ndd-set /dev/ip ip_forward_routed 1

# HP-UX 安全、防火墙和 NAT

表 14.12 显示了 HP-UX 的网络行为。有关这些行为影响的简要描述，请见第242 页的安全问题。你可以用 ndd 修改大部分内容。

# 表 14.12 HP-UX 中相关的网络行为

| 特性 | 默认 | 通过 ndd 控制 |
|---|---|---|
| IP 转发 | 动态* | 设置 ip_forwarding: 0 = 关闭, 1 = 开启, 2 = 动态 |
| ICMP 重定向 | 遵循** | 设置 ip_redirect_interval 为 0 以禁用 |
| 源路由 | 忽略 | 设置 ip_forward_src_routed 为 1 以启用 |
| 广播 ping (转发) | 阻塞 | 设置 ip_forward_directed_broadcasts |
| 广播 ping (响应) | 忽略 | 设置 ip_respond_to_echo_broadcast |

* a. 有 >1 个网络接口时；否则。
** b. 重定向条保留五分钟。

![](img/579efec8c67772f31ecf348441a2_553_0.png)

# 第14 章 TCP/IP 网络

与 Solaris 类似，HP-UX 包含了用于包过滤和 NAT 转换的 Darren Reed IPFilter 包。更多细节请见9939 页 UNIX 系统 IPFilter。IPFilter 部分完全相同，HP-UX 在启动时配置包的方式有所不同。不是使用 swadm 启用 IPFilter，而是编辑 /etc/rc.config/ipconf 并开启你需要的选项。ipf 和 ipnat 的配置文件应放在 /etc/rc.config 中。

# 14.15 AIX 网络

AIX 不是将网络信息保存在文本文件或脚本中，而是存在对象管理器（ODM）属性/值数据库中。另一层组将这些属性列表与特定设备（驱动程序实例）关联并将驱动程序绑定到配置中。

第432 页的对象管理器描述了 ODM 系统。整个方案相当复杂，允许从多个层访问网络配置。表 14.13 显示了设置接口地址的各种 AIX 命令。它们的主要区别在于影响的是运行配置、启动时配置还是两者都是。

# 表 14.13 在 AIX 设置接口 IP 地址的八种方法

| 命令 | 影响当前？ | 影响启动？ |
|---|---|---|
| smitty mktcpip (并填写表单) | 是 | 是 |
| mktcpip -i en3 -a 192.168.0.1 | 是 | 是 |
| chdev -i en3 -a netaddr=192.168.0.1 | 是 | 是 |
| chdev -i en3 -a netaddr=192.168.0.1 -P | 否 | 否 |
| chdev -i en3 -a netaddr=192.168.0.1 -T | 是 | 否 |
| ifconfig en3 inet 192.168.0.1 | 是 | 否 |
| odmchange -o CuAt_name=en3 AND attribute=netaddr < config! | 是 | 是 |
| echo 'Hey! 我设置了网络地址!' | 否 | 否 |

+   a. odmchange 需要属性/值列表作为输入。无法在命令行上指定属性值。

