
安装和配置 Kerberos 服务器是一个复杂的过程。请仔细检查各个版本的文档。这里列了一些关键领域。Kerberos 配置文件 `krb5.conf` 可以设置如加密方法和数据库名称等功能。安装 Kerberos 时，务必遵循提供管理访问的说明。你可以使用 `/etc/init.d` 目录下的 `krb5-admin-server` 和 `krb5-kde` 命令启动和重启它。

你需要为网络配置服务器，以及每个客户端（`krb5-server`）。在配置服务器时，首先指定你的 Kerberos 域和名称。然后你可以使用 `kdb5_util` 命令和 `create` 选项创建数据库：

```
kdb5_util create -s
```

系统将提示输入主密钥。然后你需要添加一个本地主体，即在运行服务器的主机上具有完全管理权限的本地用户。启动 `kadmin` 工具并使用 `addprincipal` 命令添加本地主体。

> 注意：当你在使用认证工具配置 Kerberos 时，你可以输入域、KDC 服务器和 Kerberos 服务器。默认项将使用大写的域示例显示。在 `/etc/krb5.conf` 的 realm 部分将为你的域创建一个新条目，列出 kdc 服务器和你所创建的条目。

## 第20 章 防火墙

当前连接到互联网的系统容易受到外部用户尝试未经授权访问的攻击。外部用户可以尝试通过远程连接系统来直接获取访问，或者通过拦截用户的有效通信，而可以使用身份验证程序来防止此类攻击。防火墙可以防止任何直接的未经授权访问尝试，加密可以保护授权远程用户的传输，而身份验证则可以验证请求访问的用户是否有权这样做。当前的 Linux 内核集成了对使用 netfilter (`iptables`) 数据过滤包的防火墙的支持。要实现防火墙，你只需提供一系列规则，来管理你想在系统上允许的访问类型。如果私有网络也有网关，系统的防火墙功能可以有效帮助网络免受外部攻击。

与 Linux 系统一样，Ubuntu 使用 `iptables` 实现其防火墙。然而，你可以从几个不同的防火墙管理工具中进行选择。Ubuntu 现在提供了自己的防火墙管理工具——简单防火墙（`ufw`）。`iptables` 和 `ufw` 位于 Ubuntu 仓库中，而所有其他防火墙都在 universe 仓库中。你也可以选择使用其他流行的管理工具，如 Firestarter 或 Firewall Builder (`fwbuilder`)。Firestarter 提供桌面界面，而 `ufw` 仅限命令行。本章将涵盖 `ufw` 和 Firestarter，以及底层的 `iptables` 防火墙应用。在 Synaptic 中搜索“firewall”可以查看更完整的列表。防火墙规则列如表 20-1 所示。

### 简单防火墙 (Uncomplicated Firewall)

简单防火墙（`ufw`）现在是 Ubuntu 的官方防火墙应用。它提供了一个可以通过少量命令行操作进行管理的简单防火墙。与所有防火墙应用一样，`ufw` 使用 `iptables` 来定义规则并保护防火墙。`ufw` 应用是 `iptables` 的管理接口。默认 `iptables` 规则保留在 `before` 和 `after` 文件中，添加的规则在用户文件中。`iptables` 规则保存在 `/etc/ufw` 目录下。某些软件包的 `ufw` 防火墙配置将放在 `/usr/share/ufw.d` 目录下。`ufw` 防火墙在启动时通过 `/etc/init.d/ufw` 脚本启动。

| 防火墙 | 说明 |

| :--- | :--- |

| `iptables` | netfilter, NAT, 和 mangle: netfilter.org (主仓库) |

| `ufw` | 简单防火墙: https://wiki.ubuntu.com/UbuntuFirewall (Ubuntu 主仓库); 另见 http://doc.ubuntu.com 的 Ubuntu Server Guide |

| Firestarter | Firestarter 防火墙配置工具, www://fs-security.com (universe 仓库) |

| Firewall Builder | 防火墙配置工具：允许更复杂的配置, www.fwbuilder.org (universe 仓库) |

| gnome-loklock | 基本防火墙配置 (universe 仓库) |

| Shorewall | Shoreline 防火墙: www.shorewall.net (universe 仓库) |

| Guarddog | KDE 防火墙配置工具: www.simonzone.com/software/guarddog (universe 仓库) |

**表 20-1** Ubuntu 防火墙配置工具

`iptables` 防火墙规则通过在终端窗口的命令行输入 `ufw` 命令来设置。大多数用户可能只需要使用 `ufw` 命令来允许或拒绝 Web 服务器或 Samba 服务器等服务的访问。要检查防火墙状态并列出这些允许或封锁的服务，请使用 `status` 命令：

```
sudo ufw status
```

如果防火墙未启用，你必须先使用 `enable` 命令将其启用：

```
sudo ufw enable
```

> 你可以使用 `/etc/init.d/ufw restart` 命令重启防火墙并重新加载规则：

```
sudo /etc/init.d/ufw restart
```

你可以使用 `allow` 和 `deny` 命令及其选项来添加规则，如表 20-2 所示。要允许某项服务，请使用 `allow` 命令和服务名称——即 `/etc/services` 文件中列出的服务名称。以下命令允许 ftp 服务器：

```
sudo ufw allow ftp
```

如果该服务不在 `/etc/services` 列表中，且你知道它所使用的端口和协议，你可以直接指定端口和协议。例如，Samba 服务使用端口 137 和 TCP 协议：

```
sudo ufw allow 137/tcp
```

随后 `status` 操作将显示允许了哪些服务：

```
sudo ufw status
```

| 动作源自 | |

| :--- | :--- |

| 21:tcp ALLOW Anywhere |

| 21:udp ALLOW Anywhere |

| 137:tcp ALLOW Anywhere |

| 命令 | 说明 |

| :--- | :--- |

| enable, disable | 开启或关闭防火墙 |

| status | 显示状态以及已允许或拒绝的服务 |

| logging on, logging off | 开启或关闭日志记录 |

| default allow, default deny | 设置默认策略，allow 是开放的，deny 是限制性的 |

| allow service | 允许通过服务访问；服务在 /etc/services 中定义，该文件指定了该服务的端口 |

| allow port-number/protocol | 使用指定协议允许特定端口访问；协议是可选 |

| deny service | 拒绝通过服务访问 |

| delete rule | 删除已安装的规则；使用 allow 和 deny 并包含规则 |

| proto protocol | 在 allow 或 deny 规则中指定协议 |

| from address | 在 allow 或 deny 规则中指定源地址 |

| to address | 在 allow 或 deny 规则中指定目的地址 |

| port port | 在 from 和 address 操作的 allow 或 deny 规则中指定端口 |

**表 20-2** `ufw` 防火墙，前缀加上 `delete` 命令：

```
sudo ufw delete allow 137/tcp
```

你可以使用 `allow` 和 `deny` 命令及其选项来添加规则，如表 20-2 所示。要允许某服务，请使用 `allow` 命令和服务名称——即 `/etc/services` 文件中列出的服务名称。以下命令允许 ftp 服务器：

```
sudo ufw allow ftp
```

如果该服务不在 `/etc/services` 列表中，且你知道它所使用的端口和协议，你可以直接指定端口和协议。例如，Samba 服务使用端口 137 和 TCP 协议：

```
sudo ufw allow 137/tcp
```

随后 `status` 操作将显示允许了哪些服务：

```
sudo ufw status
```

（注：OCR 包含了一些重复片段和损坏的表格。我将提供清理的合并版本。）

### 第 20 章：防火墙

**图 20-1** Firestarter Wizard，网络设备设置窗口

网络设备以及设备信息，例如接收到的包数和平均活动率。通常只会列出一个设备（作为网关运行的计算机会有多个）。扩展列表将显示“活动连接”（Active Connections），显示当前活动的连接类型，例如 Samba 或 Internet 连接。“事件”（Events）选项卡将被拒绝的连接列为被阻止连接。工具栏上的保存（Save）、清除（Clear）和重新加载（Reload）按钮允许你保存事件日志、清除日志或重新加载以查看最新事件。

**图 20-2** Firestarter 防火墙

策略（Policy）选项卡显示允许主机和服务连接的规则。弹出菜单允许你查看入站或出站流量策略。在此选项卡上，你可以为入站或出站主机添加自己的简化规则。工具栏有添加规则（Add Rule）、删除规则（Remove Rule）、编辑规则（Edit Rule）和应用规则（Apply Rule）按钮。

对于入站，你可以为连接、服务或转发设置规则。点击该段，然后点击添加规则按钮。出现的对话框取决于你正在设置的规则类型。对于连接，添加规则对话框允许你输入接收连接的主机、IP 地址或网络。对于服务，你可以从弹出菜单中选择服务以及端口，以及是否允许任何人访问，或仅允许来自特定主机或网络的连接访问。默认情况下，入站流量被拒绝，除非被规则允许。如果你正在为连接到网络的个人电脑设置防火墙，你将为本地网络地址输入一条规则。你也可以设置设置规则来访问 Samba 或 BitTorrent 等服务。

设置出站流量更为复杂。你可以设置“许可（Permissive）”或“限制（Restrictive）”策略。默认选择许可策略。许可条目将拒绝黑名单中的主机和服务，而限制条目将把主机和服务列入白名单。每个策略都包含连接和服务段落，与入站连接一样，具有相同的选项。

如果选择了许可，你将允许所有出站流量，你明确拒绝的流量除外。对于此配置，你可以为某些主机和创建创建“拒绝（Deny）”规则。在为服务设置拒绝规则时，你可以从弹出菜单中选择服务并指定其端口。对于连接，你可以选择拒绝使用此服务，或指定特定的主机或网络。对于连接，你指定可以连接的主机、IP 地址或网络。连接规则就像你的黑名单，即你或你的网络无法连接的主机或网络。

如果选择了限制，你将拒绝所有出站流量，你明确允许的流量除外。在这种情况下，你可以设置规则允许某些主机和服务的连接，拒绝其他所有内容。限制选项通常不使用，除非你添加规则允许连接，否则它将切断从你的计算机到互联网的所有连接。

要配置防火墙，请点击首选项（Preferences）按钮。这将打开一个首选项窗口，你可以在其中选择接口（Interface）或防火墙（Firewall）设置。对于接口设置，你可以设置记录的事件或策略。事件选项卡允许你指示消除不需要的事件，例如冗余事件或来自特定主机或端口的事件。策略选项卡有一个让你立即应用更改的选项。

对于防火墙设置，选项卡提供了网络设置、ICMP 过滤、TOS 过滤和高级选项的选项。网络设置允许你选择你的网络设备。在这里，你可以将网络设备更改为以太网、无线或现代模式。ICMP 过滤选项卡检查 Internet 控制消息协议（ICMP）包攻击（参见本章后面的“ICMP 数据包”）。选项允许某些 ICMP 包通过，例如通过“不可达（Unreachable）”通知你未知站点。TOS 过滤选项卡允许你根据服务类型和最大效率对数据包进行排序。对于服务类型，你可以选择工作站（Workstations）、服务器或 X Window 系统。对于最大效率，你可以选择可靠性（Reliability）、吞吐量（Throughput）或交互性（Interactivity）。默认选择工作站和吞吐量。

高级选项选项卡允许你选择方法（静默或错误报告）、内外部连接的广播流量拒绝策略（外部广播默认被阻止），以及流量验证拦截保留地址。

## iptables, NAT, Mangle, and ip6tables

Linux 系统（包括 Ubuntu）通过 Netfilter 软件包实现防火墙。Netfilter 为 Linux 2.4 及以上版本的内核实现了数据包过滤、网络地址翻译（NAT）和数据包改边（packet mangling）。数据包过滤、NAT 和数据包改边是通过规则表实现的。Netfilter 软件由 Netfilter 项目开发，地址为 http://netfilter.org，该项目提供了详细的文档和教程。

数据包过滤是决定由防火墙主机过滤的数据包是否应该发送到本地网络的过程。数据包过滤软件检查数据包的源地址和目的地址，如果允许，则发送该数据包。即使你的系统不是网络的一部分而是直接连接到互联网，你也可以使用防火墙功能来控制对你系统的访问。当然，这提供了更高的安全性。

防火墙执行的额外任务是网络地址翻译（NAT），它执行如重定向数据包到某些主机、转发数据包到其他网络以及更改数据包的主机源来实现 IP 伪装。数据包改边表用于修改数据包信息。专门应用于此表的规则通常设计用于控制数据包的行为，例如路由、连接大小和优先级。

### Iptables

执行数据包过滤、NAT 任务和改边的命令是 `iptables`，该软件通常被简称为 `iptables`。Netfilter 使用不同的表分别实现数据包过滤、NAT 任务和数据包改边。一个命令将包含其应用的一系列命令。这种方法简化了数据包过滤任务，让 `iptables` 在执行检查时无需承担进行地址翻译或改边的开销。NAT 操作也免于被混合在数据包过滤检查中。你使用 `iptables` 命令进行数据包过滤、NAT 任务和改边。每个操作都有自己的自己的规则表：`filter` 用于数据包过滤，`nat` 用于 NAT，`mangle` 用于数据包改边。对于 NAT，你通过 `-t nat` 选项指定 NAT。对于改边，你使用 `-t mangle` 选项。数据包过滤是默认的。可以通过 `-t filter` 指定，但 netfilter 也在 `raw` 表中处理连接跟踪操作异常。

在 Ubuntu 上，防火墙应用如 `ufw` 和 Firestarter 会设置包含 `iptables` 的 `iptables` 文件。当它们运行时，将设置用于过滤、翻译和改边数据包的表和规则。Firestarter 的 `iptables` 文件位于 `/etc/`，在 `ufw` 中位于 `/etc/ufw`。

### ip6tables

`iptables` 软件包提供了对 IPv6 地址的支持。它与 `iptables` 完全相同，只是使用 IPv6 地址而不是 IPv4 地址。但没有 NAT 表。`filter` 表支持在 `iptables` 中支持的所有选项和命令。`mangle` 表将允许特殊的数据包更改，就像 `iptables` 中的表一样，使用 `PREROUTING`、`INPUT`、`OUTPUT`、`FORWARD` 和 `POSTROUTING` 规则。某些扩展的名称中带有 `ipv6` 标签，例如 `ipv6-icmp`，对应于 `iptables` 的 `icmp` 扩展。`ipv6headers` 扩展用于选择 IPv6 头部。

# 434 第六部分：安全

## 模块

与其前身 `ipchains` 不同，`netfilter` 的设计是模块化且可扩展的。可以通过以模块的形式添加功能，例如状态模块（state module），它添加了连接跟踪。大多数模块作为 `iptables` 服务的一部分被加载。其他模块是可选的；你可以选择在安装规则之前加载它们。`iptables` 模块位于 `/usr/lib/kernel-version/kernel/net/iptfilter`，其中 `kernel-version` 是你的内核版本号。对于 IPv6 模块，检查 `ipv6-netfilter` 目录。自动加载的模块具有 `ipt_` 前缀，而可选模块具有 `ip_` 前缀。如果你正在编写 `iptables` 脚本，你需要添加 `modprobe` 命令来加载可选模块。

## 数据包过滤

Netfilter 本质上是一个数据包管理框架，它可以检查数据包是否符合特定协议，并通知内核正在监听这些数据包。在 netfilter 框架之上构建了 `iptables` 实现的数据包选择系统。通过 `iptables`，可以设置不同类型的规则来根据不同的标准选择数据包。Netfilter 目前支持三个表：`filter`（过滤）、`NAT`（网络地址转换）和 `mangle`（修改）。数据包过滤通过一个处理丢弃或接受数据包规则的表来实现。网络地址转换（如 IP 伪装）通过处理 IP 伪装的 NAT 表来实现。`mangle` 表用于特殊数据包。可以在数据包发送出去之前、接收时或在转发时对数据包进行更改。这种结构是可扩展的，因为新模块可以定义定义自己的规则。这还提高了效率：不需要所有数据包都检查一个大表，它们只需要访问它们所需的规则表。

如果使用 `iptables` 命令管理 `iptables` 规则。对于此命令，你需要指定想要管理的表。默认是 `filter` 表，使用 `-L` 和 `-n` 选项可以列出你任何时候添加的规则，如文所示。`-n` 选项允许你对 IP 地址和端口仅使用数字输出，从而避免对主机名进行 DNS 查找。然而，你可以使用 `-L` 选项来查看端口和主机名：

```
iptables -L -n
```

> 注意：`iptables` 命令、链名必须大大写，就像链名 `INPUT`、`OUTPUT` 和 `FORWARD` 一样。

## 链 (Chains)
