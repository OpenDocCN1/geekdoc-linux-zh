
### account
提供账户验证类型的服务：该用户的密码是否已过期？用户是否被允许访问请求的服务？

### authentication
验证用户并设置凭据。这通常通过用户必须满足的挑战-响应请求来实现：如果你是你所声称的身份，请提供你的密码。并非所有认证都是这种类型，还存在基于硬件的认证方案（例如使用智能卡和生物识别设备），通过合适的模块，可以无缝替换更标准的认证方法——这正是 `Linux-PAM` 的灵活性所在。

### password
此组的职责是更新认证机制的任务。通常，此类服务与 `auth` 组紧密耦合。某些认证方法适合通过此类函数更新。标准的 `UN*X` 基于密码的访问是一个显而例子：请输入替换密码。

### session
此组的任务涵盖了在提供服务之前和撤回服务之后应该执行的事。此类任务包括审计跟踪的维护和用户主目录的挂载。会话管理组非常重要，因为它为模块提供了开启和关闭的钩子，以影响用户可用的服务。

## FILES

`/etc/pam.conf`

配置文件

`/etc/pam.d`

`Linux-PAM` 配置目录。通常，如果存在此目录，则忽略 `/etc/pam.conf` 文件。

## 错误

通常由 `Linux-PAM` 系统库生成的错误将将写入 `syslog(3)`。

## 遵循标准

`DCE-RFC 86.0`, 1995年10月。包含额外功能，但仍与此 RFC 向后兼容。

## 参见

`pam(3)`, `pam_authenticate(3)`, `pam_sm_setcred(3)`, `strerror(3)`, `PAM(8)`

# IP-ROUTE

名称 - 路由表管理

## 概要

```
ip [OPTIONS] route { COMMAND | help }
ip route { list | flush }
ip route save
ip route restore
ip route get ADDRESS [from ADDRESS]
ip route { add | del | append | replace }
```

## 描述

`ip route` 用于操作内核路由表中的条目。

路由类型：

- `unicast`（单播） - 该条目描述了通往前缀覆盖目的地的路径。
- `unreachable`（不可达） - 这些目的不可到达。数据包被丢弃并生成 ICMP 不可达消息。本地发送者将获得 `EHOSTUNREACH`。
- `blackhole`（黑洞） - 这些目的不可到达。数据包被静默丢弃。本地发送者将获得 `EINVAL`。
- `prohibit`（禁止） - 这些目的不可到达。数据包被丢弃并生成 ICMP 禁止消息。本地发送者将获得 `EACCES`。
- `local`（本地） - 目的地分配给此主机。数据包将环回并在本地递递。
- `broadcast`（广播） - 目的地是广播地址。数据包作为链路发送。
- `throw`（抛弃） - 一种配合策略规则使用的特殊控制路由。如果选择了此类路由，在此表中的查找将终止，表示未找到路由。在没有使用策略路由的情况下，它等同于路由表中不存在该路由。数据包被删除并生成 ICMP 不可达消息。本地发送者将获得 `ENETUNREACH`。
- `nat`（地址转换） - 一种特殊路由。前缀覆盖的终被视为虚拟（外部）地址，在转发之前需要翻译为真实的（内部）地址。要翻译的地址通过 `via` 属性选择。警告：Linux 2.6 不再支持 NAT 路由。
- `anycast`（任播） - 分配给此主机的目的主要等同于本地，但区别在于：此类地址作为数据包的源地址是无效的。
- `multicast`（多播） - 用于多播路由的特殊类型。它不存在于路由表中。

路由表：Linux-2.x 可以将路由打包到多个路由表中，这些表通过 1 到 2^31 范围内的数字或通过文件 `/etc/iproute2/rt_tables` 中的名称来标识。所有普通路由都插入到主表（ID 254），内核仅在计算路由时使用此表。某些值（0, 253, 254 和 255）被留供内置使用。

实际上，始终存在一个表，它是不可见的，但更为重要。它是本地表（ID 255）。该表由本地地址和广播地址的路由组成。内核自动维护此表，管理员通常不需要修改它甚至不需要查看它。

当使用策略路由时，多个路由表就会介入。

- `ip route add` 添加新路由
- `ip route change` 修改路由
- `ip route replace` 替换或添加新路由

### TYPE 前缀（默认）

路由的终。如果省略 `TYPE`，`ip` 假设类型为 `unicast`（单播）。`TYPE` 的其他值列在上方。`PREFIX` 是 IP 或 IPv6 地址，可选跟随一个斜杠和前缀长度。如果缺少前缀长度，`ip` 假设为全长度主机路由。还有一个特殊的 `PREFIX` 默认值 - 等同于 IP `0/0` 或 IPv6。

### tos TOS

`dsfield TOS`

服务类型（TOS）键。此键没有关联的掩码，最长匹配理解为：首先，比较路由和数据包的 TOS。如果它们不等，数据包仍可能匹配 TOS 为零的路由。TOS 是一个 8 位十六进制数或来自 `/etc/iproute2/rt_tables` 的标识符。

### metric 数值

`priority NUMBER`

路由的数值。`NUMBER` 是任意的 32 位数字。

### table 表 ID

将此路由添加到该表。`TABLEID` 可以是数字或 `/etc/iproute2/rt_tables` 中的字符串。如果省略此参数，`ip` 默认使用主表，本地、广播和 `nat` 路由除外。

### dev 名称

输出设备名称。

### via 地址

下一跳的地址。

### src 地址

向前缀覆盖的终发送数据时首选的源地址。

### realm 区域

分配此路由的区域。`REALMID` 可以是数字或 `/etc/iproute2/rt_realms` 中的字符串。

### mtu MTU

通往目的路径上的 MTU。如果不使用锁定，MTU 可能会通过路径 MTU 发现更新。如果锁定，则不会尝试 MTU 发现，IPv4 将不带 DF 位发送，IPv6 将分片。

### window 数值

向这些目的发布的 TCP 最大窗口，以字节为单位。

### rtt 时间

初始 RTT（往返时间）估计。如果没有指定后缀，单位为直接传递给内核的原始值以兼容之前的版本。否则，如果使用 `s`、`sec` 或 `secs` 表示秒，`ms`、`msec` 或 `msecs` 表示毫秒。

### rttvar (2.3.15+)

初始 RTT 方差估计。值由上述 `rtt` 指定。

### rto_min 时间 (2.6.23+)

与目的通信时使用的最小 TCP 重传超时。值由上述 `rtt` 指定。

### sstresh 数值 (2.3.15+)

初始启动阈值的估计值。

### cwnd 数值 (2.3.15+)

拥塞窗口的限制。如果没有锁定标志，则会被忽略。

### initcwnd 数值 (2.5.70+)

与这些目的连接的初始拥塞窗口大小。实际窗口大小为该值乘以连接的 MSS（最大段大小）。默认值为零，意味着使用 RFC2414 中指定的值。

### initrw 数值 (2.6.33+)

与这些目的连接的初始接收窗口大小。实际窗口大小为该值乘以连接的 MSS。默认值为零，意味着使用慢启动值。

### quickack 布尔值 (3.11+)

为这些目的连接启用或禁用快速确认。

### advmss 数值 (2.3.15+)

建立 TCP 连接时向这些目的发布的 MSS（最大段大小）。如果没有给出，Linux 使用根据第一个跳跳设备 MTU 计算的默认值。（如果通往这些目的的路径是对称的，这个猜测可能是错误的）。

### 重排序 reordering NUMBER (仅限 2.3.15+)

通往目的地路径上的最大重排序。如果未指定，Linux 将使用 sysctl 变量 `net/ipv4/tcp_reordering` 选择的值。

### 下一跳 nexthop NEXTHOP

- 多路径路由的。`NEXTHOP` 是一个复杂值，其语法与顶层参数列表类似：
- `via ADDRESS` - 下一跳路由器。
- `dev NAME` - 输出设备。
- `weight NUMBER` - 该多路径路由中该元素的权重，反映了其相对带宽或质量。

### 范围 scope SCOPE_VAL

路由前缀所覆盖的目的地的范围（scope）。`SCOPE_VAL` 可以是一个数字，也可以是来自文件 `/etc/iproute2/rt_scopes` 的字符串。如果省略此参数，`ip` 假设所有通过网关的单播路由作用范围为 `global`（全局），直接单播路由和广播路由的作用范围为 `link`（链路），本地路由的作用范围为 `host`（主机）。

### 协议 protocol PROTO

此条路由的路由协议标识符。`RTPROTO` 可以是一个数字，也可以是来自文件 `/etc/iproute2/rt_protos` 的字符串。如果没有给出路由协议 ID，`ip` 假设作用范围为 `boot`（启动），该路由是由某个不知道自己在做什么的人添加的。某些协议值具有固定解释：

- `redirect` - 路由由于 ICMP 重定向而安装的。
- `kernel` - 路由是由内核在自动配置期间安装的。
- `boot` - 路由在启动过程中安装的。如果启动了路由守护，它将清除所有此类路由。
- `static` - 路由是由管理员安装以覆盖动态路由的。路由守护将尊重它们可能会将其发布给对等节点。
- `ra` - 路由是由路由协议（Router Discovery）安装的。

其余值未保留，管理员可以自由分配（或不分配）协议标签。

### 链上 onlink

假设下一跳直接连接到此链路，无视它不匹配任何接口前缀。

### 删除路由 ip route delete route

- `ip route del` 的参数与 `ip route add` 相同，但语义略有不同。

关键值（to, tos, preference 和 table）选择要删除的路由。如果存在可选属性，`ip` 会验证这些属性与要删除的路由的属性一致。如果未找到给定键和属性的路由，`ip route del` 将失败。

`ip route show` 列出路由

`t` 命令显示路由表的内容或根据某些标准选择的路由。

### 选择器 SELECTOR (默认)

仅从给定的目的地范围内选择路由。`SELECTOR` 由一个可选的修饰符（root, match 或 exact）和一个前缀组成。`root PREFIX` 选择前缀短于 `PREFIX` 的路由。例如，`root 0/0` 选择整个表。`match PREFIX` 选择前缀长于 `PREFIX` 的路由。例如，`match 10.0/16` 选择 10.0/16、10/8 和 0/0，但不会选择 10.1/16 和 10.0.0/24。而 `EXACT PREFIX`（或直接 `PREFIX`）选择具有此精确前缀的路由。如果这两个选项都不存在，`ip` 假设为 `root 0/0`，即列出整个表。

### 服务类型 TOS

`dsfield TOS`

仅选择具有给定 TOS 的路由。

### 表 ID TABLEID

显示来自此表（这些表）的路由。默认设置是显示 `main` 表。`TABLEID` 可以是真实表的 ID，也可以特殊值之一：

- `all` - 列出所有表。
- `cache` - 导出路由缓存。

### 克隆 cloned

缓存的克隆路由，即由于某些路由属性（例如 MTU）更新而从其他路由动态派生的路由。实际上，它等同于 `cache` 表。

### 源自 from SELECTOR

语法与 `to` 相同，它绑定的是源地址范围而不是目的地。注意 `from` 选项仅适用于克隆路由。

### 协议 protocol RTPROTO

仅列出此协议的路由。

### 范围 scope SCOPE_VAL

仅列出此范围的路由。

### 类型 type TYPE

仅列出此类型的路由。

### 设备 dev NAME

仅列出通过此设备的路由。

### 通过 via PREFIX

仅列出通过 `PREFIX` 选择的下一跳路由器的路由。

### 源地址 src PREFIX

仅列出由 `PREFIX` 选择的优选源地址的路由。

### 领域 realm REALMID

### 领域 realms FROMREALM/TOREALM

仅列出具有这些领域的路由。

### 清除路由表 ip route flush routing tables

此命令清除根据某些标准选择的路由。

参数的语法和语义与 `ip route show` 的参数相同，但不是列出路由表而是将其清除。唯一的区别在于默认操作：`show` 导出所有 IP 路由表，而 `flush` 打印帮助页。

带有 `-statistics` 选项，命令将变得详细。它会打印删除路由的数量和重建路由表的轮数。如果给出两次选项，`ip route flush` 还会按照上一个节描述的格式导出所有删除的路由。

### 获取单条路由 ip route get a single route

此命令获取到目的地的单条路由，并按照内核看到的原始格式打印其内容。

### 目的地址 ADDRESS (默认)

目的地。

### 源地址 ADDRESS

源地址。

### 服务类型 TOS

### dsfield TOS

服务类型。

### 接口 if NAME

预期数据包将到达的设备。

### 输出接口 oif NAME

强制路由此数据包的输出设备。

### 连接 connected

如果没有给出源地址（选项 `from`），则 `ip` 假设所有通过网关的单播路由作用范围为 `global`，直接单播和广播路由的作用范围为 `link`，本地路由的作用范围为 `host`。

### 连接 connected

`connected`-此命令获取到目的地的单条路由，并按照内核看到的打印其内容。

### 目的地址 ADDRESS (默认)

目的地。

### 源地址 ADDRESS

源地址。

### 服务类型 TOS

### dsfield TOS

服务类型。

### 接口 if NAME

预期数据包将到达的设备。

### 输出接口 oif NAME

强制路由此数据包的输出设备。

### 连接 connected

如果没有给出源地址（选项 `from`），则 `ip` 假设所有通过网关的单播路由作用范围为 `global`，直接单播和广播路由的作用范围为 `link`，本地路由的作用范围为 `host`。

`unicast` - 规则规定返回该规则引用的路由表中找到路由。

`blackhole` - 规则规定静默丢弃数据包。

`unreachable` - 规则规定生成“网络不可达”错误。

`prohibit` - 规则规定生成“通信管理性禁止”错误。

`nat` - 规则规定将 IP 数据包的源地址翻译为其他值。

## ip rule add - 插入新规则

## ip rule delete - 删除规则

### type TYPE (默认值)

此规则的类型。有效类型列表在上一小节中给出。

### from PREFIX

选择要匹配的源前缀。

### to PREFIX

选择要匹配的目的前缀。

### iif NAME

选择要匹配的入站设备。如果接口是环回接口，规则仅匹配源自此主机的数据包。这意味着你可以为转发数据包和本地数据包创建路由表，从而将它们完全隔离。

### oif NAME

选择要匹配的出站设备。出站接口仅适用于源自绑定设备本地套字的数据包。

### tos TOS

### dsfield TOS

选择要匹配的 TOS 值。

### fwmark MARK

选择要匹配的 fwmark 值。

### priority PREFERENCE

此规则的优先级。每个规则都应该显式设置唯一的优先级值。选项 `preference` 和 `order` 是 `priority` 的同义词。

### table TABLEID

如果规则选择器匹配，则查找的路由表标识符。可以使用 `lookup` 代替 `table`。

### realms FROM/TO

如果规则匹配且路由表查找成功，则选择领域（Realm）。Realm TO 仅在路由未选择任何领域时使用。

### nat ADDRESS

要翻译的 IP 地址块基地址（针对源地址）。`ADDRESS` 可以是 NAT 地址块的起始地址（由 NAT 路由选择），也可以本地主机地址（甚至是 0）。在最后一种情况下，路由器不翻译数据包，而是将其伪装成该地址。使用 `map-to` 代替 `nat` 含义相同。

**警告：** 通过这些命令对 RPDB 进行的更改不会立即生效。假设在脚本完成批量更新后，它通过 `ip route flush cache` 刷新路由缓存。

**ip rule flush - 同时也导出所有已删除的规则。** 此命令没有参数。**ip rule show - 列出规则** 此命令没有参数。选项 `list` 或 `1st` 是 `show` 的同义词。

## 参见

`ip(8)`

## 作者

由 Michail Litvak <mci@owl.openwall.com> 编写原始 Manpage

# IP-TCP_METRICS

名称

`ip-tcp_metrics` - TCP 指标管理

## 概览

```
ip [ OPTIONS ] tcp_metrics { COMMAND | help }
ip tcp_metrics { show | flush } SELECTOR
ip tcp_metrics delete [ address ] ADDRESS
SELECTOR := [ [ address ] PREFIX ]
```

## 描述
