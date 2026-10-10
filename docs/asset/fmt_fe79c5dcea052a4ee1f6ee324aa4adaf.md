
```
firewall_enable="YES"
firewall_type="open"
```

第二行是可选的，且不建议用于高安全性网络。如果你不指定防火墙类型为 `open`，IPFW 启动将从默认规则开始，其索引为 65535（最大值），指定从任何地方到任何地的 IP。换句话说，如果你在默认配置下重启 IPFW，你的机器将完全与网络隔离开，你必须通过物理控制台访问它才能恢复连接。为了最大的安全性，最好让防火墙保持在此配置中，并添加特定规则以允许来自某些主机和某些端口的流量。

## 注意

如果你在没有控制台访问权限的情况下尝试 IPFW 是危险的，因为这很容易让你的机器置于无法访问的状态。在你足够熟悉 IPFW 能够确切知道自己在做什么之前，请务必确保你可以通过控制台访问机器。

如果你最终通过实验 IPFW 导致机器被从网络中屏蔽，唯一的方法是去机器物理所在地并从控制台登录。从那里，你可以通过删除 `/etc/rc.conf` 中的行来禁用 IPFW，或者进行正确配置并重启。

防止掉入此陷阱的一个技巧是设置一个 cron 任务每五分钟关闭一次防火墙（`/etc/rc.d/ipfw stop`）；每当你尝试防火墙时，启用此自动化命令作为“安全网”。这样，如果你最终把自己锁在外面，只需要等五分钟，系统就会恢复正常。![](img/9d11c158b3f7a22d28ac4f03f601d54f_859_0.png)

## 网络安全

`open` 设置更改了默认规则，使得 IP 流量默认被通过（允许），而不是被阻塞。默认阻塞流量会创建一个真正安全的系统，但对于存在于安全环境中的系统来说，限制可能过于严格。同时，默认允许流量（仅阻塞指定的流量）消除了实现完全安全的可能。如果你的系统位于已经由防火墙保护的的网络中，请使用 `open` 设置；你不需要应用两次相同的保护。

在正确设置好 `/etc/rc.conf` 后，你也可以从物理控制台（而不是从远程终端）发出 `ipfw start` 命令，这是非常危险的，因为可能导致你丢失连接并变得无法访问。如果你看到以下行，则说明防火墙已正确启用：

```
Firewall module loaded
Flushed rules.
00100 allow ip from any to lo0
00200 deny ip from any to 127.0.0/8
00300 deny ip from any to 127.0.0/8 to any
65000 allow ip from any to any
```

你也可以使用 `kldstat` 检查 IPFW 模块是否已加载：

| Id | Address | Name |
| :--- | :--- | :--- |
| 1 | 0xc10000 | kernel |
| 2 | 0xceeeee | ipfw.ko |
| 3 | 0xcf19000 | linux.ko |

你现在可以完全访问 `ipfw` 命令，它可以让你决定允许什么类型的流量并查看积累的信息。

## 设计 IPFW 规则

`ipfw` 命令用于从内核过滤器和统计系统中添加或删除规则。规则的构建类似于自然英语的语法；它由一个动作（如 `deny`）、其应用的协议（如 `tcp`）和一个涉及子句的地址规范组成。例如，`deny host.com to any` 这样的规则会阻止来自名为 `host.com` 主机的流量。你可以像这样将此规则添加到内核防火墙：

```
# ipfw add deny host.com to any
```

该主题下有许多变体。你可以根据网络掩码指定地址，既可以使用模式（例如 `255.255.255.0`），也可以使用 CIDR 掩码（例如 `/24`）。你还可以阻塞单个端口而不是整个系统；这种技术可以防止具有不可预测 IP 地址的大型 ISP 内部的主机针对你机器上的单一服务。这样的规则可能像这样：

```
# ipfw add deny all from evil.isp.com/16 to www.example.com 80
```

同样，你可以通过添加 `allow` 规则作为异常，使主机免于之前的规则，如下所示：

```
# ipfw add allow all from goodhost.isp.com to www.example.com 80
```

更有用的是，你可以根据外部主机使用的 TCP 或 UDP 端口来阻塞或允许其流量。例如，你可能选择只允许网页和邮件流量到达服务器，分别使用 TCP 端口 80 和 25：

```
# ipfw add deny tcp from any to www.example.com 80
# ipfw add allow tcp from any to www.example.com 80
# ipfw add allow tcp from any to www.example.com 25
```

注意，IPFW 规则是以“链”形式进入的，其中每个规则按照其指定的顺序进行评估。每个规则都有一个索引，通常与相邻规则间隔 100，你可以通过在 `ipfw` 命令的 `add` 或 `deny` 关键字之后指定索引数字来控制；这就是你执行规则顺序的方法。使用 `ipfw -a list` 查看现有规则集：

```
# ipfw -a list
00100 0 allow ip from any to any via lo0
00200 0 deny ip from any to 127.0.0/8
00300 0 deny ip from 127.0.0/8 to any
00400 0 deny tcp from badhost.com to any
00500 0 ipfw add deny all from evil.isp.com/16 to www.example.com 80
00600 0 ipfw add allow all from goodhost.isp.com to www.example.com 80
65000 121 79688
65535 10 deny ip from any to any
```

## IPFW 故障排除

你可能会发现，你认为非常直接的配置导致了完全无法预料的结果。例如，你为所有主机添加了拒绝（deny）规则，并为你的远程机器的 IP 地址添加了允许（allow）规则，但你仍然发现无法访问 FreeBSD 机器。

始终记住，IPFW 规则按照特异性增加的顺序进行指定和应用。列表后出现的规则将覆盖列表中较早指定的规则；数据包将按照索引号指定的顺序与每条规则进行比较。在大多数情况下（尽管这在很大程度上取决于所采取的操作和系统设置），数据包将继续检查其他可能以更特定方式匹配的后续规则；这就是“异常”规则的工作原理。然而，索引为 65536 的“默认”规则仅匹配那些未匹配任何其他规则的数据包。

让你的索引按照特异性增加的顺序应用规则。为了使配置变得更简单，请考虑使用防火墙配置文件，我们稍后会讨论这一点。

你可以在 `/etc/rc.conf` 中指定多种不同的防火墙类型。每个关键字都有不同的含义，如表 30.2 所示。这些配置文件的定义是从 `/etc/rc.firewall` 中的 shell 脚本代码解析出的。

### 表 30.2 可用的防火墙类型

| 关键字 | 含义 |
|---|---|
| open | 允许从所有地方访问所有地方 |
| closed | 禁止除环回 lo0 接口外的所有 IP |
| client | 设置旨在保护此台机器的规则 |
| simple | 设置旨在保护整个网络的规则 |
| UNKNOWN | 默认值；除了索引为 65535 的默认拒绝规则外，不加载任何规则 |
| filename | 从 *filename* 加载规则 |

对于你的需求，如果你的设置不复杂，使用名为 `client` 或 `simple` 的“预制”IPFW 配置方案可能是合适的。然而，随着系统的不断演进，你可能需要专门的配置。

## 使用防火墙配置文件

由于防火墙规则不是持久的（它们每次重启时都会清空），如果你自定义了防火墙设置，你将希望通过配置文件来维护你的防火墙。这具有比从命令行操作 IPFW 更易维护和更快排除故障的优点。

将你的特殊规则集放入你选择的文件中；对于此示例，将其命名为 `/etc/firewall.conf`。在该文件中列出你需要的规则，省略 `ipfw` 命令本身：

```
add deny tcp from badhost.com to any
add deny all from evil.isp.com/16 to www.example.com 80
```

## 防止入侵和破坏

```
add allow all from goodhost.evil.isp.com to www.example.com 80
add 65000 allow from any to any
```

现在，更改你 `/etc/rc.conf` 中的 `firewall_type`：

`firewall_type="/etc/rc.conf"`
