
```
-j DNAT --to-destination 192.168.0.3
```

指定端口可以让您更改到达特定端口的数据包的目的地。实际上，这允许您实现端口转发。在下一个示例中，所有到达端口 80（Web 服务端口）的数据包都会被重定向到 10.0.0.3，在这种情况下，该系统将运行 Web 服务器。

```
# iptables -t nat -A PREROUTING -i eth0 -dport 80 \
-j DNAT --to-destination 10.0.0.3
```

使用 TOS 和 MARK 目标，您可以修改数据包以控制其路由或优先级。TOS 目标为数据包设置服务类型，可以通过诸如标准服务、最小化成本、最大化吞吐量等标准来设置优先级。

仅适用于 NAT 表的目标如下所示：

|  |  |
|---|---|
| SNAT | 修改源地址，使用 --to-source 选项指定新的源地址。 |
| DNAT | 修改目标地址，使用 --to-destination 选项指定新的目标地址。 |
| REDIRECT | 重定向数据包。 |
| MASQUERADE | IP 伪装。 |
| MIRROR | 反转源地址和目标地址并发送回给发送者。 |
| MARK | 修改 Mark 字段以控制消息路由。 |

## NAT 重定向：透明代理

NAT 表可用于实现各种类型的数据包重定向，这是一个对用户透明的过程。重定向常用于实现透明代理。数据包的重定向通过 REDIRECT 目标执行。使用透明代理时，接收到的数据包可以自动重定向到代理服务器。例如，到达 Web 服务端口 80 的数据包可以重定向到 Squid 代理服务端口，通常是 3128。这涉及使用 PREROUTING 链上的 REDIRECT 目标重定向数据包的命令：

```
# iptables -t nat -A PREROUTING -i eth1 --dport 80 -j REDIRECT --to-port 3128
```

## 数据包修饰：Mangle 表

数据包修饰表（mangle 表）用于实际修改数据包信息。专门应用于此表的规则通常旨在控制数据包的常规行为，如路由、连接大小和优先级。实际修改数据包（而不仅仅是重定向或停止它）的规则只能用于 mangle 表。例如，TOS 目标可以直接在 mangle 表中用于更改服务类型（Type of Service）字段以修改数据包优先级。TCPMSS 目标可以设置用于控制连接大小。ECN 目标允许您绕过 ECN 黑洞，而 DSCP 目标允许您更改 DSCP 位。诸如 ROUTE 扩展等几个扩展将修改数据包，在这种情况下，是重写其目标地址，而不仅仅是重定向它。

mangle 表通过 -t mangle 选项表示。使用以下命令查看您的 mangle 表中列出的链：

```
iptables -t mangle -L
```

此处显示了几个 mangle 表目标。

|  |  |
|---|---|
| TOS | 修改服务类型字段以管理数据包优先级。 |
| TCPMSS | 修改连接允许的数据包大小，启用更大的传输。 |
| ECN | 移除 ECN 黑洞信息。 |
| DSCP | 更改 DSCP 位。 |
| ROUTE | 扩展目标，用于修改数据包中的目标信息。 |
| Note | iptables 包被设计为可扩展的，允许轻松添加自定义目标。这涉及对内核应用补丁并重新构建它。有关更多详细信息以及扩展目标列表，请参阅 www.netfilter.org。 |

## IP 表脚本

虽然您可以从 shell 命令行输入 iptables 规则，但当您关闭系统时，这些命令将会丢失。在 Red Hat 上，您可以利用 iptables 服务脚本中内置的支持来保存和读取 iptables 规则。或者，您可以自己管理这个过程，保存到您自己选择的文件中。无论哪种情况，您很可能需要将 iptables 规则放在一个可以直接执行的脚本中。这样，您可以编辑和管理复杂的规则集，添加注释并保持其顺序。

注意 在 Red Hat 二进制文件中，内核中的 IPtables 支持默认启用。如果您重新编译内核以启用数据包过滤支持，请检查 2.4 内核中的 Networking Options 以及 2.6 内核中 Device Drivers 下的 Networking Support/Networking Options。

### Red Hat iptables 支持

Red Hat 作为系统配置的一部分提供对 iptables 的支持。当您安装 iptables 的 RPM 包时，将安装一个 iptables 服务脚本，该脚本使用 /etc/sysconfig/iptables 文件读取和保存 iptables 命令。如果您已设置 iptables 在系统启动时自动启动，则该文件将被检查以确认其存在且不为空。如果是这样，iptables 将自动读取其中包含的 iptables 命令。这有助于将 iptables 更顺利地集成到系统设置过程中。

/etc/sysconfig/iptables 脚本由 redhat-config-securitylevel 自动生成，该工具在安装过程中运行。当您首次启动系统时，/etc/sysconfig/iptables 文件将包含在您运行 redhat-config-securitylevel 时所选配置的 iptables 规则。如果您再次运行 redhat-config-securitylevel 并更改配置，/etc/sysconfig/iptables 文件将被新的 iptables 规则覆盖。您可以通过 System Settings 菜单或窗口中的 Security Level 条目访问 redhat-config-securitylevel。

只需删除 /etc/sysconfig/iptables 文件即可绕过此自动 iptables 设置。（运行 redhat-config-securitylevel 并选择 No Firewall 会产生相同的效果）。确保首先备份该文件，以防其中包含重要命令。可以直接编辑 /etc/sysconfig/iptables 文件并输入 iptables 命令，但不建议这样做。相反，应将此文件视为包含 iptables 命令的最终安装结果。

应将 Red Hat 提供的 iptables 服务脚本视为一种多功能管理工具，而不是服务启动脚本。对该脚本使用 service 命令可能会令人困惑。iptables 脚本仅管理 iptables 规则，即刷新、添加或报告它们。它不会启动和停止 iptables 服务。如果 Netfilter 未运行，您需要指定在系统启动时启动它。为此，您可以使用 redhat-config-service（Server Settings 窗口中的 Services），然后从服务列表中选择 iptables。

```
service iptables status
```

思考 iptables 服务脚本的最有效方式之一是将其视为 iptables 开发工具。在创建复杂的防火墙规则（超出 redhat-config-securitylevel 生成的简单集合）时，您应首先创建一个脚本并将规则放入其中，如后文 iptables 脚本示例中所述。使脚本可执行。在调试防火墙期间需要进行的任何更改，都应在该脚本中进行。在运行它之前，使用 stop 选项运行 iptables 服务脚本以清除任何以前的规则：

```
service iptables stop
```

然后运行您的脚本，如下所示为 myfilters 脚本：

```
./myfilters
```

要查看 iptables 如何解释命令，请使用带有 status 选项的服务脚本：

```
service iptables status
```

对于任何更改，请编辑您的 iptables 脚本。然后再次运行服务脚本以清除旧规则。再次运行 iptables 脚本，并使用带有 status 选项的服务脚本查看它们是如何实现的：

```
service iptables stop
./myfilters
service iptables status
```

一旦您对 iptables 规则正确工作感到满意，您可以将规则保存到 /etc/sysconfig/iptables 文件。使用带有 save 选项的 iptables 服务脚本。现在，当系统启动时您的规则将被自动读取。可以将 save 操作视为在系统上安装 iptables 规则，使它们成为每次启动系统时系统设置的一部分。

```
service iptables save
```

要进行更改，请修改您的 iptables 脚本，使用 stop 运行服务脚本以清除旧规则，运行 iptables 脚本，然后使用带有 save 选项的服务脚本生成新的 /etc/sysconfig/iptables 文件。

您可以使用 iptables-save 脚本代替服务脚本来保存规则。推荐使用的文件是 /etc/iptables.rules。服务脚本实际上使用带有 -c 选项的 iptables-save 将规则保存到 /etc/sysconfig/iptables 文件。iptables-save 的 -c 选项在输出中包含计数器（iptables 服务脚本旨在解析命令中的计数器信息）。iptables-save 命令将规则输出到标准输出。要将它们保存到文件中，必须使用重定向运算符 > 将输出重定向到文件，如下所示：

```
iptables-save -c > /etc/sysconfig/iptables
```

您还可以将规则保存到您自己选择的文件，例如 /etc/iptables.rules。/etc/rc.d/init.d/iptables 服务脚本定义了 IPTABLES_CONFIG 变量，它保存 iptables 配置文件的名称，即 /etc/sysconfig/iptables。

```
iptables-save > /etc/iptables.rules
```

然后，要恢复规则，请使用 iptables-restore 脚本从该保存的文件中读取 iptables 命令：

```
iptables-restore < /etc/iptables.rules
```

## 一个 iptables 脚本示例

您现在已有足够的信息来创建一个简单的 iptables 脚本，为连接到 Internet 的单个系统提供基本保护。以下脚本 myfilter 提供 IP 表过滤过程，以保护局域网和 Web 站点免受外部攻击。它为一私有网络配置了一个简单的防火墙（有关更复杂的示例，请查阅 iptables HOWTO）。如果您有本地网络，可以对此脚本进行改编以适配它。在此配置中，所有从外部发起的远程访问都被阻止，但允许网络内用户与外部系统建立连接时的双向通信。在此示例中，防火墙系统充当私有网络的网关，其网络地址为 192.168.0.0（参见图 19-1）。为了示例方便起见，Internet 地址为 10.0.0.1。该系统有两个以太网设备：一个用于私有网络（eth1），一个用于 Internet（eth0）。网关防火墙系统还支持位于地址 10.0.0.2 的 Web 服务器。本示例中太长的条目将在第二行继续，换行符用反斜杠引用。

