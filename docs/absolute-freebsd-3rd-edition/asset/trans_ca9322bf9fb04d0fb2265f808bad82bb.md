

然后指定目的地址 5。目的是括号中的接口名称，这意味着“该接口上的任意 IP 地址”。

最后，定义此规则适用的端口 6。花括号允许你将多个实体组合在一起。该过滤器允许连接到端口 22 (ssh)、53 (DNS)、80 (HTTP) 和 443 (HTTPS)。你可以通过名称（来自 `/etc/services`）指定端口，但我发现数字更可靠。编辑 `/etc/services` 不应该导致你的防火墙崩溃！在此主机上部署新的 TCP 服务只需要在列表中添加一个端口并重新加载防火墙规则。

UDP 规则略有不同。

```
pass in on $ext_if proto udp to ($ext_if) port 53
```

最明显的变化是定义 UDP 协议而不是 TCP 4。一个不太明显的变化是该规则省略了源地址。它适用于来自任何地址的数据包。此数据包过滤器仅允许一个端口，即 53 2。具有单个端口的规则不需要花括号。

ICMP 规则看起来有点棘手，但其实是一样的。

```
pass in on $ext_if inet proto icmp to ($ext_if) icmp-type{ unreach, redir,
timex echoeq }
```

指定此规则适用于 ICMP 很直接 7。而且，该规则也没有列出源地址，因此它适用于来自任何地方的流量。

TCP 和 UDP 规则指定的是目的端口，而此 ICMP 规则列出了 `icmp-type` 2。ICMP 没有端口，但它有不同种类的流量。不过，就我们的用途而言，ICMP 类型很像端口。类型有数字代码，但名称更容易理解。

此规则指定了四种不同的 ICMP 流量类型 3。

整体来看，此规则允许对于正常互联网功能通常必需的 ICMP 流量。你的环境可能需要其他 ICMP 类型。你组织的安全策略可能规定了你可以通过和不能通过哪些 ICMP。但这四种类型对于面向互联网的服务器的组合来说是合理的。

这个简单策略定义了我们与服务器通信的基本规则。虽然它并不完美，但它可以为入侵者设置障碍。那个闯入你的 Web 服务器并在 10000 端口上启动命令提示符的家伙？如果你的防火墙规则不允许该端口的传入连接，他们所有的辛苦工作都将白费。真是一场悲剧。

## 管理 PF

使用 pfctl(8) 管理 PF。如果你的规则没有错误，pfctl(8) 会静默运行；只有在有错误时才会产生输出。你需要测试、激活、查看和删除规则。

### 测试规则

由于防火墙错误可能会给你带来很多麻烦，最好在激活规则之前检查它们。虽然规则检查只解析文件，检查规则本身的语法错误，但激活带有语法错误的规则要么使你的系统失去保护，要么把你锁在外面，或者两者兼有。使用 `-n` 标志检查文件中的问题，并使用 `-f` 指定 PF 规则文件。

```
# pfctl -nf /etc/pf.conf
```

如果出现错误，请修复它们并再次尝试。

### 激活规则

一旦你的语法检查静默运行，通过移除 `-n` 标志激活新规则。

```
# pfctl -f /etc/pf.conf
```

更改 PF 配置非常快。这意味着你可以为不同时间或情况准备多个 PF 配置。也许你只想在一天中的某些时间允许访问某些服务；你可以安排运行 pfctl(8) 以安装适用于那些时间的适当规则。或者，也许你为灾难情况准备了单独的规则，并希望在你失去互联网连接时安装特殊的规则集。使用 pfctl(8) 使所有这些配置都变得简单。

### 查看规则

如果你想查看当前在防火墙上运行的规则，请使用 `pfctl -sr`。

```
# pfctl -sr
scrub in all fragment reassemble
block drop in all

pass in on em1 proto tcp from any to (em1) port = ssh flags S/SA keep state
pass in on em1 proto tcp from any to (em1) port = domain flags S/SA keep state
pass in on em1 proto tcp from any to (em1) port = http flags S/SA keep state
pass in on em1 proto tcp from any to (em1) port = https flags S/SA keep state
pass in on em1 proto udp from any to (em1) port = domain keep state
pass in on em1 inet proto icmp from any to (em1) icmp-type unreach keep state
pass in on em1 inet proto icmp from any to (em1) icmp-type redirect keep state
pass in on em1 inet proto icmp from any to (em1) icmp-type timex keep state
pass in on em1 inet proto icmp from any to (em1) icmp-type echoreq keep state
pass out all flags S/SA keep state
```

你可以完全按照此处所示的格式编写 PF 规则。

请注意，虽然我们在配置文件中指定了多个 TCP 端口，但在数据包过滤器中，每个 TCP 和 UDP 端口都有其自己的规则。同样，每个 ICMP 类型也有其自己的规则。

### 删除规则

最后，使用 `-Fa`（刷新所有）标志从你的运行配置中删除所有规则。（你可以使用除 `a` 以外的标志来删除防火墙配置的一部分，但这可能会使你的系统处于不一致状态。）

```
# pfctl -Fa
```

你会看到 PF 系统地擦除所有规则、NAT 配置以及配置中的其他内容。在加载新配置之前不要手动清除配置；只需加载新的规则文件以擦除旧规则。

PF 极其强大，非常灵活，并且可以以任何你喜欢的方式（以及某些你不喜欢的方式）滥用 TCP/IP。我们才刚刚触及皮毛。查看第 462 页“Packet Filtering”开头列出的一些资源，以深入探索 PF。

## Blacklistd(8)

有时，你想要的不仅仅是简单的允许或拒绝所允许的那种深思熟虑的数据包过滤。我经常将 SSH 服务器开放给公共互联网，以便我可以从任何地方登录。但我相当反感僵尸网络认为我会愚蠢到允许无密码登录。这就是 blacklistd(8) 发挥作用的地方。

Blacklistd 允许守护进程报告：“嘿，这个 IP 地址在困扰我。”一旦 blacklistd 收到针对某个地址的足够多的投诉，它就会告诉防火墙阻止该地址。那些永远在戳你 SSH 服务器的机器人？它们已成为历史。

这种类型的黑名单对于像 Hail Mary Cloud 这样的分布式僵尸网络只有边际上的用处，但即使如此，你也许可以配置灵敏度以屏蔽最烦人的客户端。这完全取决于每个僵尸网络成员具有多大的侵入性。

要使用 blacklistd，你必须配置数据包过滤器以接受来自 blacklistd 的输入，为每个服务设置容忍级别，并配置服务以使用 blacklistd。

### PF 和 Blacklistd

PF 通过锚点（anchors）处理动态规则。你可以使用 pfctl(8) 编辑活动锚点，让你可以在策略的特定点插入规则。将 blacklistd 锚点添加到你的规则中，就在你的第一个 block 和 pass 语句之前。使用上一节中的策略，你的规则看起来像这样：

```
--snip--
anchor "blacklistd/*" in on $ext_if
block in
pass out
--snip--
```

你必须在锚点名称周围包含引号，并且必须指定接口。

数据包过滤器现在已准备好进行动态黑名单处理。

### 配置 Blacklistd

Blacklistd 从其配置获取自 `/etc/blacklistd.conf`。虽然其大部分配置在此文件中，但你也可以使用命令行选项修改服务的行为。

通过在 `/etc/rc.conf` 中启用 blacklistd 开始。

```
# sysrc blacklistd_enable=YES
blacklistd_enable: NO -> YES
```

在你重启或手动启动它之前，守护进程不会启动，因此你现在可以配置它。

### /etc/blacklistd.conf

Blacklistd 规则每个支持单个服务、端口或地址组。将你的规则放入 `/etc/blacklistd.conf`，每行一个规则。Blacklistd 规则分为两组：本地和远程。

本地 blacklistd 规则适用于运行 blacklistd 的机器上的本地项目。这是你为本地 SSH 服务、端口 99 或任何其他本地项目设置规则的地方。本地规则部分以 `[local]` 作为前缀。

远程 blacklistd 规则适用于非本地机器上的项目。在这里，你可以定义诸如“此块获得降低的容忍度”、“在更短的时间内禁用这些地址”或“永远不要阻止这些地址”等规则。远程规则部分以 `[remote]` 作为前缀。我们首先讨论本地规则，然后讨论远程规则支持的新增功能。

这是一个 `blacklistd.conf` 条目示例：

```
[local]
ssh stream * * * 3 24h
```

