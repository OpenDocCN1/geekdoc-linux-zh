
## 3.5.1.5 确保配置了 `ufw` 出站连接（手动）

**适用范围：**

- 等级 1 - 服务器
- 等级 1 - 工作站

**描述：**

为新的出站连接配置防火墙规则。

**备注：**

- 在网络连接时更改防火墙设置可能会导致被锁定系统之外。
- 与 `iptables` 不同，当添加新的出站规则时，`ufw` 会自动处理关联的已连接，因此不需要为后者创建规则。

**原理：**

如果没有为新的出站连接设置规则，所有数据包将被默认策略丢弃，从而防止网络使用。

**审计：**

运行以下命令并验证所有新的出站连接规则是否符合站点策略：

```bash
# ufw status numbered
```

**修复：**

根据站点策略配置 `ufw`。以下命令将实施允许在所有接口上所有出站连接的策略：

```bash
# ufw allow out on all
```

### CIS 策略

| 控制版本 | 控制措施 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 4.4 在服务器上实施和管理防火墙<br><br>在支持的情况下，在服务器上实施和管理防火墙。示例实现包括虚拟防火墙、操作系统防火墙或第三方防火墙代理。 | ● | ● | ● |
| v8 | 4.5 在端用户设备上实施和管理防火墙<br><br>在端用户设备上实施和管理基于主机的防火墙或端口过滤工具，并带有默认拒绝规则，丢弃所有显式允许的服务和端口以外的流量。 | ● | ● | ● |
| v7 | 9.4 应用主机防火墙或端口过滤<br><br>在端系统上应用主机防火墙或端口过滤工具，并带有默认拒绝规则，丢弃所有显式允许的服务和端口以外的流量。 | ● | ● | ● |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| `T1562`, `T1562.004` | `TA0011` | `M1031`, `M1037` |

## 3.5.1.6 确保所有开放端口都存在 `ufw` 防火墙规则（自动）

**适用范围：**

- 等级 1 - 服务器
- 等级 1 - 工作站

**描述：**

任何在回环地址上打开的端口都需要防火墙规则来管理流量。

**备注：**

- 在网络连接时更改防火墙设置可能会导致被锁定系统之外。
- 修复命令将端口开放给来自所有源的流量。请咨询 `ufw` 文档并根据站点策略设置任何限制。

**原理：**

如果没有为开放端口配置防火墙规则，默认防火墙策略将丢弃发送到这些端口的数据包。

**审计：**

运行以下脚本以验证所有开放端口都存在防火墙规则：

```bash
#!/usr/bin/env bash

ufw_out="$(ufw status verbose)"
ss -tun | awk '($5!~/:lo; && $5!~/127.0.0.1:/ && $5!~/:1/) (split($5, a, ":"); print a[2])' | sort | uniq | while read -r lpn; do
grep -Pq "^h$lpn\b" <<< "$ufw_out" || echo "$lpn missing a firewall rule"
done
```

不应返回任何内容

**修复：**

对于审计识别出的每个没有防火墙规则的端口，添加接受或拒绝入站连接的规则：

示例：

```bash
# ufw allow in <port>/<tcp or udp protocol>
```

### CIS 策略

| 控制版本 | 控制措施 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 4.4 在服务器上实施和管理防火墙<br><br>在支持的情况下，在服务器上实施和管理防火墙。示例实现包括虚拟防火墙、操作系统防火墙或第三方防火墙代理。 | ● | ● | ● |
| v7 | 9.4 应用主机防火墙或端口过滤<br><br>在端系统上应用主机防火墙或端口过滤工具，并带有默认拒绝规则，丢弃所有显式允许的服务和端口以外的流量。 | ● | ● | ● |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| `T1562`, `T1562.004` | `TA0011` | `M1031`, `M1037` |

## 3.5.1.7 确保 `ufw` 默认拒绝（自动）

**适用范围：**

- 等级 1 - 服务器
- 等级 1 - 工作站

**描述：**

拒绝策略确保任何未配置的流量都会被拒绝。

**注意：**

使用拒绝策略时，任何不可接受的使用将被阻止。

**原理：**

使用拒绝策略，建立白名单比建立黑名单更容易。

**影响：**

默认策略将阻止任何显式允许的内容。在默认设置之前应考虑以下规则：

```bash
ufw default deny
ufw allow in http
ufw allow out
ufw logging on
```

**审计：**

运行以下命令并验证入站、出站和路由方向的默认设置为拒绝：

```bash
# ufw status | grep Default:
```

示例输出：

```text
Default: deny (incoming), deny (outgoing)
```

**修复：**

运行以下命令实施默认拒绝：

```bash
# ufw default incoming
# ufw default outgoing
# ufw default routed
```

### CIS 策略

| 控制版本 | 控制措施 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 4.4 在服务器上实施和管理防火墙<br><br>在支持的情况下，在服务器上实施和管理防火墙。示例实现包括虚拟防火墙、操作系统防火墙或第三方防火墙代理。 | | | |
| v8 | 4.5 在端用户设备上实施和管理防火墙<br><br>在端用户设备上实施和管理基于主机的防火墙或端口过滤工具，并带有默认拒绝规则，丢弃所有显式允许的服务和端口以外的流量。 | | | |
| v7 | 9.4 应用主机防火墙或端口过滤<br><br>在端系统上应用主机防火墙或端口过滤工具，并带有默认拒绝规则，丢弃所有显式允许的服务和端口以外的流量。 | | | |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| `T1562`, `T1562.004` | `TA0011` | `M1031`, `M1037` |

## 3.5.2 配置 `nftables`

如果您的环境中使用了不复杂的防火墙 (`UFW`) 或 `iptables`，请遵循相应章节的指南并忽略本节。

`nftables` 是 `Linux` 内核的一个子系统，提供网络数据包/数据报/帧的过滤和分类，是 `iptables` 的继任者。`nftables` 最大的变化在于其简单性。在 `iptables` 中，我们必须配置每一条规则，像 `BPF`（伯克利过滤器）一样，它更短且重复更少。`nftables` 应该编译进内核，以及相关的 `nftables` 模块。在选择此选项之前，请确保您的内核支持 `nf_table`。

**注意：**

- 本节广泛假设从空的 `nftables` 规则集开始（通过刷新规则建立）。
- 修复步骤仅影响实时系统，还需要配置默认防火墙配置以便启动时生效。
- 在远程连接时直接配置实时系统防火墙通常会导致被锁定。建议在启动时设置一个已知的良好配置，并在脚本中配置整个防火墙结构，然后在测试后保存到启动。

以下内容将实施本节的防火墙规则，并从所有地方开放 `ICMP`、`IGMP` 和端口 `22` (`ssh`)。开放 `ICMP`、`IGMP` 和端口 `22` (`ssh`) 需要根据本地站点策略进行更新。允许端口 `22` (`ssh`) 需要更新为仅允许需要 `ssh` 连接的系统连接。

将以下脚本保存为 `/etc/nftables.rules`：

```bash
#!/sbin/nft -f

# 此 nftables.rules 配置应保存为 /etc/nftables.rules
# 清除 nftables 规则集
flush ruleset
# 加载 nftables 规则集
# 使用名为 filter 的 inet 表配置 nftables
table inet filter {
    # 用于 input 钩子的基础链 input（过滤入站数据包）
    chain input {
        type filter hook input priority 0; policy drop;
        # 确保回环流量已配置
        iif "lo" accept
        ip saddr 127.0.0.8 counter packets 0 bytes 0 drop
        ip6 saddr ::1 counter packets 0 bytes 0 drop

        # 确保已建立的连接
        ct state established accept
        ct state related accept
        ct state new accept

        # 从任何地方接受端口 22 (SSH) 流量
        tcp dport ssh accept

        # 从任何地方接受 ICMP 和 IGMP
        icmp6 type { destination-unreachable, packet-to-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-node, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
        icmp type { destination-unreachable, router-advertisement, router-solicitation, time-exceeded, parameter-problem } accept
    }

    # 用于 forward 钩子的基础链 forward（过滤转发的网络数据包）
    chain forward {
        type filter hook forward priority 0; policy drop;
    }

    # 用于 output 钩子的基础链 output（过滤出站网络数据包）
    chain output {
        type filter hook output priority 0; policy drop;
        # 确保配置出站和已建立的连接
        ct state established,related,new accept
    }
}
```

运行以下命令将文件加载到 `nftables` 中：

```bash
# nft -f /etc/nftables.rules
```

`nftables` 子集中的所有更改都是临时的。

要使这些更改持久化：

运行以下命令创建 `nftables.rules` 文件：

```bash
nft list ruleset > /etc/nftables.rules
```

在 `/etc/nftables.conf` 中添加以下行：

```bash
include "/etc/nftables.rules"
```

### 3.5.2.1 确保安装了 `nftables`（自动化）

**适用范围：**

- 级别 1 - 服务器
- 级别 1 - 工作站

**描述：**

`nftables` 提供了一种新的内核态数据包分类框架，该框架基于特定于网络的虚拟机 (VM) 和新的 `nft` 用户空间命令行工具。`nftables` 重用了现有的 `Netfilter` 子系统，例如现有的钩子基础设施、连接跟踪系统、`NAT`、用户空间队列和日志子系统。

**备注：**

- `nftables` 可用于 `Linux` 内核 `3.13` 及更高版本
- 仅安装并配置一个防火墙工具
- 在网络连接时更改防火墙设置可能会导致被锁定在系统之外

**理由：**

`nftables` 是 `Linux` 内核的一个子系统，可以防止来自企业网络内部的威胁，包括恶意移动代码和主机上配置不当的软件。

**审计：**

运行以下命令验证是否安装了 `nftables`：

```bash
# dpkg-query -s nftables | grep 'Status: install ok installed'
Status: install ok installed
```

**修复：**

运行以下命令安装 `nftables`：

```bash
# apt install nftables
```

### CIS 控制

| 控制版本 | 控制 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 4.4 在服务器上实施和管理防火墙<br><br>在支持的情况下，在服务器上实施并管理防火墙。示例实现方法包括虚拟防火墙、操作系统防火墙或第三方防火墙代理。 | | ● | ● |
| | 4.5 在终端用户设备上实施和管理防火墙<br><br>在终端用户设备上实施并管理基于主机的防火墙或端口过滤工具，带有默认拒绝规则，丢弃显式允许的服务和端口之外的所有流量。 | | ● | ● |
| v7 | 9.4 应用基于主机的防火墙或端口过滤<br><br>在终端系统上应用基于主机的防火墙或端口过滤工具，带有默认拒绝规则，丢弃显式允许的服务和端口之外的所有流量。 | | ● | ● |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| `T1562`, `T1562.004` | `TA0011` | `M1031`, `M1037` |

### 3.5.2.2 确保 `ufw` 已卸载或通过 `nftables` 禁用（自动化）

**适用范围：**

- 级别 1 - 服务器
- 级别 1 - 工作站

**描述：**

`Uncomplicated Firewall (UFW)` 是一个易于使用的 `netfilter` 防火程序。

**理由：**

同时运行 `nftables` 和 `ufw` 可能会导致冲突。

**审计：**

运行以下命令验证 `ufw` 是否安装：

```bash
# dpkg-query -s ufw | grep 'Status: install ok installed'
Status: install ok installed
```

**修复：**

运行以下命令移除 `ufw`：

```bash
# apt purge ufw
```

运行以下命令禁用 `ufw`：

```bash
# ufw disable
```

### CIS 控制

| 控制版本 | 控制 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 4.4 在服务器上实施和管理防火墙<br><br>在支持的情况下，在服务器上实施并管理防火墙。示例实现方法包括虚拟防火墙、操作系统防火墙或第三方防火墙代理。 | | ● | ● |
| | 4.5 在终端用户设备上实施和管理防火墙<br><br>在终端用户设备上实施并管理基于主机的防火墙或端口过滤工具，带有默认拒绝规则，丢弃显式允许的服务和端口之外的所有流量。 | | ● | ● |
| v7 | 9.4 应用基于主机的防火墙或端口过滤<br><br>在终端系统上应用基于主机的防火墙或端口过滤工具，带有默认拒绝规则，丢弃显式允许的服务和端口之外的所有流量。 | | ● | ● |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| `T1562`, `T1562.004` | `TA0011` | |

### 3.5.2.3 确保 `iptables` 已通过 `nftables` 清空（手动）

**适用范围：**

- 级别 1 - 服务器
- 级别 1 - 工作站

**描述：**

`nftables` 是 `iptables`、`ip6tables`、`ebtables` 和 `arptables` 的替代品。

**理由：**

可以混合使用 `iptables` 和 `nftables`。但这增加了复杂性和引入错误的可能性。为了简单起见，请清除所有 `iptables` 规则并确保其未运行。

**审计：**

运行以下命令确保没有 `iptables` 规则。

对于 `iptables`：

```bash
# iptables -L
```

应返回为空。

对于 `ip6tables`：

```bash
# ip6tables -L
```

应返回为空。

**修复：**

运行以下命令清空 `iptables`：

对于 `iptables`：

```bash
# iptables -F
```

对于 `ip6tables`：

```bash
# ip6tables -F
```

### CIS 控制

| 控制版本 | 控制 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 4.4 在服务器上实施和管理防火墙<br><br>在支持的情况下，在服务器上实施并管理防火墙。示例实现方法包括虚拟防火墙、操作系统防火墙或第三方防火墙代理。 | | ● | ● |
| | 4.5 在终端用户设备上实施和管理防火墙<br><br>在终端用户设备上实施并管理基于主机的防火墙或端口过滤工具，带有默认拒绝规则，丢弃显式允许的服务和端口之外的所有流量。 | | ● | ● |
