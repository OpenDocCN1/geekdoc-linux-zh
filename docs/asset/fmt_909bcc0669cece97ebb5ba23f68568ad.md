
添加 `-n` 选项将以数字形式列出 IP 地址和端口。这将加快列表速度，因为 `iptables` 将不会尝试进行 DNS 查询来确定 IP 地址的主机名。

# 第 19 章：网络防火墙：Netfilter

## Nat 目标与链

此外，还有两种 NAT 操作：源 NAT（指定为 `SNAT` 目标）和目的 NAT（指定为 `DNAT` 目标）。`SNAT` 目标用于更改源地址的规则，`DNAT` 目标用于更改目的地址的规则。

`NAT` 表中的三条链被内核用于 NAT 操作。这些链是 `PREROUTING`、`POSTROUTING` 和 `OUTPUT`。`PREROUTING` 用于目的 NAT (`DNAT`) 规则。这些规则用于正在到达的数据包。`POSTROUTING` 用于源 NAT (`SNAT`) 规则。`OUTPUT` 用于本地生成数据包的目的 NAT 规则。

通过数据包过滤，您可以指定源地址 (`-s`) 和目的地址 (`-d`)，以及输入 (`-i`) 和输出 (`-o`) 设备。`-j` 选项将指定一个目标，如 `MASQUERADE`。当您向 `POSTROUTING` 链添加一条 `MASQUERADE` 规则时：

```bash
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

要更改离开您系统的数据包地址，您将使用带有 NAT 目标的 `POSTROUTING` 规则。对于 `SNAT` 目标，您使用 `--to-source` 选项来指定源地址：

```bash
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.0.4
```

要更改到达您系统的数据包地址，您将使用带有 `DNAT` 目标的 `PREROUTING` 规则以及 `--to-destination` 选项：

```bash
# iptables -t nat -A PRERUTING -i eth0 \
-j DNAT --to-destination 192.168.0.3
```

指定端口允许您更改到达特定端口的数据包的终地。实际上，您实现了端口转发。在下一个示例中，每个到达端口 80 端口（Web 服务端口）的数据包都会被重定向到 `10.0.0.3`，在这种情况下，它将是一个运行 Web 服务器的系统。

```bash
# iptables -t nat -A PREROUTING -i eth0 \
-j DNAT --to-destination 10.0.0.3
```

使用 `TOS` 和 `MARK` 标记，您可以对数据包进行流量整形以控制其路由或优先级。`TOS` 目标设置数据包的服务类型，可以设置优先级标准，如普通服务、最小成本、最大吞吐量等。仅适用于 `NAT` 表的目标所示所示：

| 目标 (Target) | 描述 (Description) |
| :--- | :--- |
| `SNAT` | 修改源地址，使用 `--to-source` 选项指定新的源地址。 |
| `DNAT` | 修改目的地址，使用 `--to-destination` 选项指定新的目的地址。 |

| `REDIRECT` | 重定向数据包。 |
| `MASQUERADE` | IP 伪装。 |
| `MIRROR` | 反转源和目的并发送回给发送者。 |
| `MARK` | 修改 Mark 字段以控制消息路由。 |

## 第四部分：安全

命令行、通过你自己的脚本添加，或通过 `/etc/sysconfig/iptables` 中的启动选项添加。以下命令将列出你当前的规则：

```
service iptables status
```

或许认为 `iptables` 服务脚本最有效思考方式是将其视为一个开发工具。在创建复杂的防火墙规则（超过了 `redhat-config-security-level` 生成的简单集合）时，你应该先创建一个脚本并将你的规则放入其中，正如后文的 `iptables` 脚本示例所示。使该脚本具有可执行权限。你在调试防火墙时需要进行的任何更改，都需要在这个脚本中进行。在运行它之前，先使用 `stop` 选项运行 `iptables` 服务脚本以清除任何之前的规则：

```
service iptables stop
```

然后运行你的脚本，如下所示的 `myfilters` 脚本：

```
./myfilters
```

要查看 `iptables` 是如何解释命令的，请使用带有 `status` 选项的服务脚本：

```
service iptables status
```

对于任何更改，请编辑你的 `iptables` 脚本。然后再次运行服务脚本以清除旧规则。再次运行 `iptables` 脚本，并使用服务脚本的 `status` 选项查看它们是如何实现的：

```
service iptables stop
./myfilters
service iptables status
```

一旦你确认你的 `iptables` 规则运行正常，你就可以将规则保存到 `/etc/sysconfig/iptables` 文件。使用带有 `save` 选项的服务脚本。现在，你的规则将在系统启动时自动被读取。你可以将 `save` 操作想为将你的 `iptables` 规则安装到系统中，使它们在你每次启动系统时都成为系统设置的一部分：

```
service iptables save
```

要进行更改，请修改你的 `iptables` 脚本，运行带有 `stop` 选项的服务脚本以清除旧规则，运行 `iptables` 脚本，然后使用带有 `save` 选项的服务脚本生成新的 `/etc/sysconfig/iptables` 文件。

与其使用服务脚本，你可以使用 `iptables-save` 命令保存规则。推荐使用的文件是 `/etc/iptables.rules`。该服务实际上将规则保存到 `/etc/sysconfig/iptables` 文件。`-c` 选项在输出中包含计数器（`iptables` 服务脚本设计为与命令一起解析计数器信息）。`iptables-save` 命令将规则输出到标准输出。要将它们保存到文件中，你必须将输出重定向到重定向运算符 `>`，如下：

```
iptables-save -c > /etc/sysconfig/iptables
```

## 第19 章：网络防火墙：Netfilter

你也可以将规则保存到你选择的文件，例如 `/etc/iptables.rules` `/etc/rc.d/ipt` `iptables` 服务脚本定义了 `IPTABLES_CONFIG` 变量，该变量持有 `iptables` 配置文件的名称 `/etc/sysconfig/iptables`。

```
iptables-save > /etc/iptables.rules
```

然后，要恢复规则，请使用 `iptables-restore` 脚本从该保存文件中读取 `iptables` 命令：

```
iptables-restore < /etc/iptables.rules
```

### iptables 脚本示例

你现在有了足够的信息来创建一个简单的 `iptables` 脚本，它可以为连接到互联网的简单系统提供基本保护。前者 **`myfilter`** 提供了一个 IP 表过滤过程，以保护本地网络和网站免受外部攻击。它为私有网络配置了一个简单的防火墙（查看 `iptables` HOWTO 获取更复杂的示例）。如果你有一个本地网络，可以针对该网络调整此脚本。在此配置中，所有从外部发起的远程访问都被阻断，但网络中的用户与外部系统建立的连接允许双向通信。在这个示例中，防火墙系统充当私有网络的网关，其网络地址为 `192.168.0.0`（见图 19-1）。为了本示例，互联网地址为 `10.0.0.1`。该系统有两个以太网设备：一个用于私有网络 (`eth1`)，另一个用于互联网 (`eth0`)。网关防火墙系统还支持地址为 `10.0.0.2` 的 Web 服务器。示例中过大而无法放在单行的条目将延续在第二行，并用反斜符引用换行符。

通过 ISP 连接到互联网

![](img/b575339375dd1a4a4eb2f8188c6df286_376_0.png)

图 19-1 带有防火墙的网络

## 第四部分：安全

应用于网络不同部分的基本规则如图 19-2 所示。

```
myfilter
防火墙网关 IP 地址为 10.0.0.1，使用以太网设备 eth0
# 私有网络地址为 192.168.0.0，使用以太网设备 eth1
# 网站地址为 10.0.0.2
# 关闭 IP 转发
echo 0 > /proc/sys/net/ipv4/ip_forward
# 清空链规则
iptables -F INPUT
iptables -F OUTPUT
iptables -F FORWARD
# 设置默认（策略）规则
iptables -P INPUT DROP
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
# IP 欺骗，拒绝任何来自内部网络
# 具有外部源地址的数据包：
```
