
关于依赖关系的更详细讨论，请参阅 Gentoo Handbook 中的“在脚本中编写”部分。

## 2.c. 变量名与

变量名是动态的。它们通常遵循 `variable_${interface}[address|mac]` 的结构。例如，变量 `dhcp_eth0` 保存 `eth0` 的 DHCP 选项值，而 `dhcp_essid` 存储接口连接到 SSID "essid" 时的 DHCP 选项值。

然而，这里没有硬性规定服务名必须是 `ethx`。事实上，许多接口的名称如 `wax`、`ras` 和 `xi`，定义的定义的接口（如网桥）也可以被命名为任何名称，例如 `foo`。为了方便起见，无线访问点可以拥有包含字母数字字符的名称，这很重要，因为你可以根据每个 ESSID 配置网络。

这一切的缺点是 Gentoo 在网络中使用下划线（bars） - `bash` 无法在英语字母数字之外使用它们。为了绕过这一限制，我们将每个非字母数字的变量更改为 `_` 字符。

`bash` 的另一个缺点是变量的内容 - 某些字符需要转义。这可以通过需要在转义的字符前面放置 `\` 字符来实现。例如 `\.` 和 `\'`。

在这个示例中，我们使用 ESSID，因为它们包含最广泛的字符集。我们将使用 ESSID My \NET：

### 代码列表 3：变量名示例

```
# 这可行，但域名是无效的

dns_domain_My___NET=My \ NET
```

# 当无线卡连接到 ESSID 为 My \ NET 的 AF 时，上述设置会将 dns 域设置为 My \ NET

## 3. 模块化网络

### 3.a. 网络模块

我们支持模块化网络脚本，这意味着我们可以轻松添加对新接口类型和配置模块的支持，同时与旧模块保持兼容。

如果模块所需的包已安装，则加载模块。如果你在这里指定了一个未安装对应包的模块，你将收到一个错误，说明你需要安装哪个包。理想情况下，只有当你安装了两个或多个提供服务的包且需要倾向于其中某一个时，才使用模块设置。

> 注意：除非另有说明，这里讨论的所有设置都在 `/etc/conf.d/net` 中。

### 代码列表 1：模块偏好

```
# 优先使用 iproute2 而非 ifconfig

modules=( "iproute2")
```

- 你也可以为接口指定其他模块
- 在这种情况下，我们优先使用 `dhcp6` 而非 `dhcpcd`
`modules_eth0="dhcp6"`
- 你也可以指定不使用的模块 - 例如，你可能正在使用 `supplicant` 或 `linux-ng` 来控制无线配置，但你仍然想通过关联的 ESSID 配置网络设置。
`modules=("iwiconfig")`

### 3.b. 接口处理器

我们目前提供两个处理器：`ifconfig` 和 `iproute2`。你需要其中之一来执行任何类型的网络配置。

`ifconfig` 是 Gentoo 的默认选择，它包含在系统配置中。`iproute2` 是一个更强大且灵活的包，但默认并不包含。

### 代码列表 2：使用 iproute2

```
# emerge sys-apps/iproute2

# 如果两者都安装，则优先使用 iproute2

modules=(\iproute2")
```

由于 `ifconfig` 和 `iproute2` 执行的操作非常相似，它们允许配置互通工作。

### 代码列表 3：ifconfig 和 iproute2

```
config_eth0="192.168.1.1/24"

config_eth0="192.168.1.1/24"
```

### 3.c. DHCP

DHCP 是从 DHCP 服务器获取信息（IP 地址、DNS 服务器等）的手段。DHCP 可以由 `dhclient`、`dhcped` 或 `udhcpc` 提供。

| 模块 | 包 | 优点 | 缺点 |
|---|---|---|---|
| dhclient | net-misc/dhclient | ISC 开发，可配置 | 配置复杂，软件臃肿 |
| dhcped | net-misc/dhcped | Gentoo 长期默认 | 不维护 |
| pump | net-misc/pump | 轻量级 | 不维护 |
| udhcpc | net-misc/udhcpc | 轻量级 - 客户端 | 不可靠 |

如果你有多个 DHCP 客户端，需要指定使用哪一个 - 否则使用 `dhcpcd`。

要为 DHCP 模块指定选项，使用 `module_eth0="..."`（更改你使用的 DHCP 模块）。

尝试让 DHCP 与实现无关 - 我们通过 `dhcp_eth0` 变量支持以下功能：

- 释放 IP 地址供重用
- `nodns` - 不覆盖 `/etc/resol.conf`
- `nonstop` - 不覆盖 `/etc/ntp.conf`
- `nonis` - 不覆盖 `/etc/resol.conf`

### 代码列表 4：/etc/conf.d 中的示例 DHCP 配置

```
# 仅当有多个 DHCP 模块时需要

modules=(dhcpcd")

config_eth0="10" # 10 秒后超时

dhcpcd_eth0="lease nonstop nonis" # 获取地址
```

> 注意：`dhclient`、`udhcpc` 和 `pump` 默认会将主机名发送到 DHCP 服务器，你不需要指定。

### 3.d. ADSL 调制解调器

首先安装 ADSL 软件。

### 代码列表 5：安装 rp-pppoe 包

```
# emerge-netdialup/rp-pppoe
```

> 警告：baseline-1.11 仅支持 PPPoE。希望未来版本支持 PPPoA。

现在我们需要通过更新 `/etc/conf.d/net` 将 `eth0` 配置为 ADSL 接口并输入用户名。

### 代码列表 6：在 /etc/conf.d/net 中为 ethSL 配置 ADSL

```
config_eth0="*adsl"

adsl_user_eth0="username"
```

最后我们需要在 `/etc/ppp/pap-secrets` 中定义你的用户名和密码。

### 代码列表 7：示例 /etc/ppp/pap-secrets

```
```

APIPA 尝试通过在接口上对 `169.254.0.0-169.254.255.255` 范围内的地址进行 `arping` 来寻找空闲地址。如果没有找到响应，则仅适用于没有 DHCP 服务器且你没有直接连接互联网且所有其他计算机都使用 APIPA 的局域网。

若要支持 APIPA，请 `merge net-misc/iputils` 或 `net-analyze/arping`。

### 代码列表 8：/etc/conf.d/net 中的 APIPA 配置

```
# 尝试 DHCP - 如果失败则回退到 APIPA

config_eth0="dhcp"

fallback_eth0="apipa"

# 仅使用 APIPA

config_eth0="apipa"
```

## 3.5. 绑定 (Bonding)

对于链路绑定/汇聚（link bonding/trunking），请 `emerge net-misc/ifensave`。

绑定用于增加网络带宽。如果你有两个连接到同一个网络的网卡，可以将它们绑定在一起，这样你的应用程序只会看到一个接口，但实际上它们使用了两个网卡。

### 代码列表 9：/etc/conf.d/net 中的绑定配置

```
# 将接口绑定在一起

slaves_bond0="eth0 eth1 eth2"

# 你可能不想为绑定后的接口分配 IP

config_bond0="null"

# 依赖 eth0、eth1 和 eth2，因为它们可能需要额外配置

depend_bond0() {

  need net_eth0 net_eth1 net_eth2

}
```

## 3.6. 桥接 (支持 802.1d)

若要支持桥接，请 `emerge net-misc/bridge-utils`。
例如，你可能有一台服务器通过 ADSL 调制解器连接互联网并通过无线网卡让其他计算机通过 ADSL 调制解器上网。你可以创建一个桥接将这两个接口连接起来。

### 代码列表 10：/etc/conf.d/net 中的桥接配置

```
# 配置桥接 - 更多详情请 man brctl-

brctl_br0="setethlo 0" "stp.off"

# 将端口添加到桥接 br0

bridge_br0="eth0"

# 你需要将端口连接到 null 值，因为 dhcp 不启动

config_eth0="null"

config_eth1="null"

# 最后给桥接分配地址 - 你也可以使用 DHCP

conf_br0="192.168.0.1/24"

# 依赖 eth0 和 eth1，因为它们可能需要额外配置

depend_br0() {

need net_eth0 net_eth1

}
```
