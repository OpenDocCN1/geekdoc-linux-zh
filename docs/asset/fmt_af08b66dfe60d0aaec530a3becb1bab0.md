
这提供了临时的本地和远程地址，并告诉远程服务器它可以替换这些值。与其使用私有 IP 地址（如此处所示），你可以使用 `0.0.0.0` 代替。

（注：由于提供的原文中存在大量重复内容和乱码片段，译文已根据“不要重复输出原文”的原则进行了去重和清理，仅保留了核心逻辑部分的翻译。）

## 554 第四部分 + Red Hat Linux 网络与服务器设置

> 注意
不再建议使用 `ipfwadm` 包进行 IP 转发。相反，应该使用本章中描述的 `ipchains`。

- 有效的 IP 地址——如果您的局域网（LAN）使用的是由 ISP 或注册机构正式分配的地址，则无需进行任何特殊的 IP 伪装（masquerading）。

在您的 Red Hat 电脑已配置局域网和互联网接口后，请按照以下步骤将 Red Hat Linux 设置为路由器：

1. 输入 `netcfg` 打开 `netcfg` 窗口。
2. 点击 Routing（路由）。
3. 输入默认网关设备（Default Gateway Device）。如果您是从局域网路由数据包到连接互联网的 PPP 连接，则网关设备类似于 `ppp0` 或 `ppp1`（您可能不需要输入默认网关，因为 IP 地址已由 ISP 动态正确分配）。
4. 点击 Save（保存）。此操作的结果应该是 `/etc/network` 文件中的一些条目。完成后，该文件的内容应该类似于以下：

```
WORKING=yes

FORWARD_IPV4=yes

HOSTNAME=maple

DOMAINNAME=handsonhistory.com

GATEWAY=

GATEWAYDEV=ppp0
```

这应该导致 `ip_forward` proc 文件被设置为 1。要验证这一点，请输入以下命令：

```
# cat /proc/sys/net/ipv4/ip_forward

1
```

> 注意
在该值显示为 1 之前，您可能需要重启电脑（或其他重新启动网络）。

5. 如果您局域网上的电脑具有有效的 IP 地址，请直接跳到配置 Red Hat Linux 路由客户端的章节。如果您的电脑具有私有 IP 地址，请继续执行此过程。

> 警告
下一步中的 `ipchains` 示例并不十分安全，尽管在大多数情况下，它能让路由正常运行。我建议您稍后阅读本章后部分的 IP 伪装章节，以及第 14 章，以获取有关防火墙和其他安全问题的信息。

6. 要在您的 Red Hat Linux 路由器上启动 IP 伪装，您需要定义哪些地址将进行伪装和转发。这里有一个

## 第 16 章 + 连接互联网 555

示例，局域网上所有网络号为 10.0.0.0 的电脑都被接受转发和伪装：

```
ipchains -P forward DENY

ipchains -A forward 10.0.0.0/255.0.0.0 -j MASQ
```

此示例显示，默认情况下转发是被禁止的。然而，对于网络 10.0.0.0（子网掩码为 255.0.0.0）上的电脑，如果数据包来自本地 Red Hat Linux 系统，则将会被转发到默认路由并进行伪装（MASQ）。

您可以使用较短的表示法输入子网掩码。对于 A 类、B 或 C 类网络，值分别为 8、16 或 24。与其允许整个网络，您也可以允许单个主机。例如，您可以为 `10.0.0.10`、`10.0.0.11`、`10.0.0.12` 等设置单独的转发行。

要永久设置您的转发规则，您需要将它们添加到启动脚本中，该脚本会在每次系统重启（或网络重启）时运行。我将 `ipchains` 行添加到 `/etc/rc.d/init.d/network` 文件中，以便它们在网络启动时运行。我将它们放在 `case, start;` 和 `ipv4_forward_set` 行之后，这些行如下：

```
case "$1" in

start)

ip4_forward_set

ipchains -P forward DENY

ipchains -A forward -s 10.0.0.0/8 -j MASQ
```

7. 此时，您可能需要重启 Linux 系统。

8. 要检查您的 `ipchains` 命令是否生效，请按如下方式打印 `ip_fwchains` proc 内容：

```
# /proc/net/ip_fwchains

forward 00000000->000000000/00000000 - 10 0 0

0 0 0 0-65535 0-65535 AFF X 00000000 0 0 MASQ
```

输出显示转发策略（forward）对于网络 10.0.0.0 上的电脑已设置为伪装（MASQ）。

此时，您应该设置客户端电脑以使用您的 Red Hat 路由器进行互联网连接。

### 配置 Red Hat Linux 路由客户端

在例示例中，局域网上有各种 Red Hat Linux 和 Windows 95/98 客户端。一台 Red Hat Linux 电脑连接到互联网，并乐于作为互联网与局域网其他电脑之间的路由器（如上一节所述）。为了让每个客户端能够访问互联网上的电脑，它必须能够执行以下操作：

## 第四部分 Red Hat Linux 网络与服务器设置

1. 将请求的名称（例如 `www.redhat.com`）解析为 IP 地址。
2. 找到从本地系统到远程系统的路由。

客户端知道如何查找的方法基于以下内容：

```
order hosts,bind
```

接下来，每个客户端必须知道如何访问互联网。您通过添加默认路由来实现。方法如下：

```
route default gw 10.0.0.1 eth0
```

这告诉系统使用路由器处理客户端不知道的地址。

如果您有多个 DNS 服务器，请将它们添加到 `/etc/resolv.conf`：

```
nameserver 8.8.8.8

nameserver 8.8.4.4
```

### 配置 Windows 95 路由客户端

如果您局域网中有某些 Microsoft 系统，您需要配置它们以便其通过路由器连接到互联网。要让私有网络上的 Windows 95/98 电脑通过您的路由器访问互联网，您只需要在每个 Windows 95/98 系统上添加少量信息。以下是在 Windows 95 中进行此操作的方法：

1. 点击“开始 -> 控制面板”。
2. 打开控制面板中的“网络”图标。
3. 双击连接到 Linux 路由器的接口。（对于局域网，它可能看起来：TCP/IP -> 拨号适配器）。
4. 点击网关（Gateway）选项卡，输入 Linux 路由器的 IP 地址，然后点击添加。
5. 点击 DNS 配置选项卡，输入用于解析互联网地址的 DNS 服务器编号，然后点击添加。如果您有多个 DNS 服务器，请重复此操作。
6. 点击确定。

此时，尝试从 Windows 95 电脑上的 浏览器访问一个网站。如果互联网连接位于您的 Red Hat Linux 电脑上，您应该能够通过局域网连接到 Red Hat Linux 电脑来访问互联网。

## 配置 IP 伪装和 ipchains 防火墙

通过 IP 伪装（IP masquerading），没有注册 IP 地址的计算机可以通过 Red Hat Linux 连接到互联网。对于互联网而言，来自你局域网（LAN）任何人的所有信息实际上都来自你的 Red Hat Linux 计算机。从互联网返回的所有响应数据包都会通过 Red Hat Linux 服务器，然后路由到它们在局域网上的正确目的地。

如果你的局域网拥有一有效且唯一的 IP 集合，则不需要 IP 伪装。这仅对于需要访问互联网的具有私有地址的计算机是必要的。

以下是伪装的工作原理：

- 客户端将你的 Red Hat Linux 系统识别为其网关。
- 客户端尝试访问互联网时，发送一个数据包到达 Red Hat Linux 节点。Linux 随后分配一个新的源端口号，在数据包头中添加自己的 IP 地址，并保存原始数据包。然后它将修改后的数据包发送到互联网。
- 当数据包从互联网到达目标为 Red Hat Linux 地址和客户端端口的 Red Hat Linux 系统时，原始端口和 IP 地址会被放入数据包头并发送给客户端。

使用 IP 伪装时，并非所有服务都受到支持。例如，伪装不支持任何指向伪装客户端的入站服务。同样，并非所有出站 IP 服务都受到支持。请参考描述支持 IP 伪装服务的侧边栏以获取信息。

`ipchains` 软件包提供了 IP 伪装服务以及其他防火墙服务。要检查是否配置了 ipchains，请检查 `/proc/net/ip_lw_ipchains` 文件是否存在。如果存在，则已安装 ipchains。ipchains 允许你设置规则，根据这些规则，防火墙会对数据包如何通过防火墙的处理做出决策。

当数据包到达 ipchains 系统时，防火墙会检查你设置的规则。根据这些规则，防火墙对数据包执行以下操作：

- ACCEPT—允许数据包通过。
- DENY—丢弃数据包且不转发。
- REJECT—丢弃数据包且不转发，但向发送者发回消息，告知其数据包已被丢弃。
- MASQ—数据包被伪装为看似来自防火墙路由主机。
- REDIRECT—将数据包重定向到用户定义的本地套字，该套字被配置为提供代理服务。

规则可以在四种不同类别之一中设置：IP 输入链、IP 输出链、IP 转发链和用户定义链。输入链与从本地局域网接口进入计算机的数据包规则有关。输出链为从本地计算机发送到网络的数据包设置规则。转发链与请求由防火墙计算机转发的数据包有关。用户定义链可以是为本地系统设置的任何规则。

有关 IP 伪装的更多信息，请检查随 Red Hat Linux 一带的 `ipchains` 和 `ipfw` 手册页。你也可以访问 Web上的 IP 伪装资源页（http://ipmasq.cjb.net）。在 `/usr/doc/HOWTO/mini` 目录下有一个 IP-Masquerade mini-HOWTO。有关 `ipchains` 的更具体信息，请参阅 `IPCHAINS-HOWTO`。

## IP 伪装支持的服务

当你使用 IP 伪装服务从 Linux 互联网时，Red Hat Linux 默认支持以下服务：

- HTTP—通过互联网浏览器访问万维网的服务。
- FTP—支持大多数使用文件传输协议的客户端。
- Telnet—远程登录服务。
- POP/SMTP—支持邮局协议和简单邮件传输协议。
- NNTP—支持 Usenet 新闻服务。
- Archie/Gopher/Wais—支持这些过时的文档存储和搜索工具（针对大多数客户端）。
- VRML—支持用于虚拟现实内容的虚拟现实标记语言服务。
- Traceroute/Ping—支持这些以及相关的 TCP/IP 管理工具。

此外，Red Hat Linux 默认安装了特殊模块，支持通过防火墙为 Quake II、Cu-SeeMe、IRC 聊天、RealAudio 流媒体音频和 VDOLive 流媒体视频的服务。

## 将 Red Hat Linux 设置为代理服务器

你的 Red Hat Linux 计算机上建立了一个局域网，它既连接到局域网，也连接到互联网。在不设置路由的情况下，为局域网内的计算机提供 Web 浏览服务的一种方法是将 Red Hat Linux 计算机配置为代理服务器。

Squid 代理缓存服务器软件包随 Red Hat Linux 一起。在基础配置中，你可以快速地启动该软件。然而，该软件包充满了许多配置功能，你可以启用这些功能来适应你的需求。你可以控制哪些主机可以访问代理服务、如何使用内存缓存数据、如何进行日志记录以及其他各种功能。以下是 Squid 提供的代理服务：

- 允许 HTTP 代理服务是使用 Squid 的主要原因。这让客户能够通过他们的浏览器（通过你的 Red Hat Linux 计算机）访问互联网上的 Web 页面。换句话说，它将为你查找并返回类似 http://www.com 这种地址的内容。
- FTP — 这代表文件传输协议 (FTP) 代理服务。当你为客户端启用 HTTP 时，会自动启用 FTP（例如，ftp/www.com）。
- Gopher — gopher 协议代理服务是互联网上组织和搜索文档的早期机制之一（它比 Web 早十多年）。

## 启动 squid 守护进程

在安装 Red Hat Linux 时，你有机会安装 Squid 并标记守护进程自动启动。如果你不确定是否已设置，有几种方法可以检查。首先，以 root 用户身份输入以下：

```
ps x | grep squid
```

如果 squid 守护进程正在运行，你应该能看到一个类似于下面的条目：

```
774 ? S    0:00 squid -D
```

如果你没有看到运行的 squid 进程，则守护进程可能没有设置成自动启动。要设置守护进程在启动时启动，请使用 System V Run-Level Manager。要启动它，以 root 用户身份输入以下：

```
/usr/X11R6/bin/x
```

打开 System V Run-Level Manager，显示设置为在不同运行级别运行的启动脚本。假设你启动到默认运行级别（运行级别 3），为了让 squid 在启动时启动，你需要将 squid 脚本添加到第 3 列的启动行中。首先，滚动到数字 3 Start 列。如果 squid 不在那里，你可以按照以下方式设置：

- 滚动 Available 列直到看到 squid，然后点击它。如果你在 Available 列中没有看到 squid，则 squid 可能未安装。你可以从 Red Hat Linux 分发磁盘安装软件包。
- 点击 Add。应该弹一个 Add Squid 弹出窗口。
- 点击 Start Squid 和数字 3，然后点击 Done。一个弹出窗口询问你希望 Squid 在启动过程的哪个数字失败。
- 在 "Number for Squid is:" 框中输入一个两位数字。像 90 这样的数字就可以。（只要确保该数字比 "network" 脚本大即可）。
- 点击 Add。squid 脚本应该出现在 3 Start 列中。

# 562 第四部分 + Red Hat Linux 网络与服务器设置

如果你的 Red Hat Linux 系统是从 GUI 界面启动的，你可能正在将系统启动到 init 状态 5。如果是如此，请参考第 5 列的操作步骤而不是第 3 列。

此时，squid 守护进程应该在系统启动时自动启动。默认情况下，squid 守护进程将带有 `-D` 选项运行`-D` 选项允许 squid 在没有活动 Internet 连接的情况下启动。如果你想为 squid 守护进程添加其他选项，可以编辑该启动脚本。首先创建一个副本 (`cp /etc/rc.d/init.d/squid /etc/rc.d/init.d/squid.default`)，然后编辑 `/etc/rc.d/init.d/squid` 脚本。寻找类似于下面的行：

```
SQUID_OPTS="-D*"
```

你可以在引号内添加 `-D` 选项以外的任何选项。这些选项大部分对于调试 Squid 很有用。

| 选项 | 说明 |
| :--- | :--- |
| -a port | 用数字# 替换端口，该数字将用于替代默认端口号 (3128) 来处理 HTTP 代理请求。这对于临时尝试替代端口很有用。 |
| -f squidfile | 使用此选项指定备用的 squid.conf 文件（/etc/squid/squid.conf 之外）。将 squidfile 替换为备用 squid.conf 的文件名。这是在替换旧文件之前尝试新 squid.conf 文件的好方法。 |
| -d level | 将调试级别更改为 level 指定的数字。这也会导致调试信息发送到 stderr。 |
| -X | 使用此项检查你的 squid.conf 文件中的值是否设置得当。它会在解释 squid.conf 文件时开启完整调试。 |

当 squid 守护进程运行时，你有几种方法可以通过使用这些选项运行命令来更改守护进程的工作方式：

| 命令 | 说明 |
| :--- | :--- |
| squid -z | 使用带有清理后的缓存重启 squid。 |
| squid -k check | 检查 squid 当前是否正在运行。 |
| squid -k reconfigure | 让 squid 重新读取其配置文件。 |
| squid -k shutdown | 让 squid 在短暂等待连接退出后退出。 |
| squid -k interrupt | 立即关闭 squid，而不等待连接关闭。 |
| squid -k kill | 立即杀死 squid，不关闭连接或日志文件。（仅当其他方法不起作用时使用此方法。） |

# 第 16 章 + 连接到互联网 563

随着 squid 守护进程的运行，你现在需要设置 squid.conf 配置文件。

## 使用简单的 squid.conf 文件

Squid 主页 (http://squid.nlanr.net) 提供了一个基础的 squid.conf 配置文件，你可以直接使用它来开始。因为它的权限非常宽松，你可能只想使用此文件让 Squid 运行起来。那么，一旦一切运行正常，你就可以更改 squid.conf 文件使其更具限制性，它将更符合你的需求（如本章的其余部分所述）。

要开始，请创建一个 `/etc/squid/squid.conf` 文件，其中仅包含以下基本内容：

```
#squid.conf - 一个用于 squid 的非常基础的配置文件

#将日志调至最低级别

debug_options ALL,1

# 定义一个包含所有 IP 地址的组（或访问控制列表）

acl all src 0.0.0.0/0.0.0

#允许所有站点通过 HTTP 连接到我们

http_access allow all

#允许所有站点将我们作为兄弟节点

icp_access allow all

#测试以下站点以检查我们是否已连接

dns_testnames internic.net usc.edu cs.colorado.edu mit.edu

yale.edu

#以 squid 用户身份运行
```
