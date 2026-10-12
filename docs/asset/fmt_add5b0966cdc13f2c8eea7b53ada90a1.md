
列表 7.2 由三个大部分组成。前三次 `iptables` 调用清空了所有现有的防火墙规则。这在你创建或调试脚本时尤为重要，因为你可能不想在现有规则上添加新规则；其结果将是旧规则和新规则的混乱混合。接下来的三次 `iptables` 调用将三个链的默认策略设置为 `DROP`。这是防火墙的基本起点。剩余的 `iptables` 调用配置 Linux 接受特定类型的流量：

**回环流量**：脚本将系统设置为接受来自回环接口（在 `127.0.0.1`）的特定流量。某些 Linux 工具允许你使用此接口，因为它是纯本地的，所以接受此类流量的安全风险非常小。请注意，允许此类访问的行代码同时使用了 IP 地址（通过 `-d` 和 `-s` 选项）和 `lo` 接口名称（通过 `-o` 和 `-i` 选项）。此配置防止了回环地址被欺骗——即攻击者从另一台计算机伪装成 `127.0.0.1`。此配置像大多数 `iptables` 配置一样需要两条 `iptables` 规则：一个允许入站，一个允许出站。

**DNS 流量**：第二块规则允许进往端口 `53` 的 `UDP` 流量，该端口处理 `DNS` 流量。大多数系统都需要此类配置，以允许计算机使用其本地 `DNS` 服务器。你可以通过仅指定 `DNS` 服务器的 IP 地址来加强此配置。（如果你有多个 `DNS` 服务器，则需要每个服务器准备一对规则。）

**客户端流量**：列表 7.2 允许 `TCP` 数据包从非权限端口（客户端程序使用）发送到任何系统。此配置使用有状态检测来允许新的、已建立的或相关的出站流量，同时仅允许已建立的或不相关的入站流量。此配置有效地阻止了在非权限端口上运行服务器的能力。因此，入侵者或恶意的授权用户将无法登录到运行在此类端口上的未经授权服务器——至少在没有配置 `root` 权限的情况下无法做到。

**SSH 服务器流量**：最后一块选项允许访问 `SSH` 服务器（`TCP` 端口 `22`）。然而，这种访问被限制在 `172.24.1/24` 网络（推测是该计算机的本地网络）。此配置使用有状态数据包检测来概述来自 `SSH` 服务器的已建立和相关的数据的出站流量，但不包括新的或无效数据包。对于 `SSH` 服务器的入站数据包允许新的、现有的或相关的流量，但不允许无效数据包。

诸如 7.2 所示的配置适用于运行 `SSH` 服务器进行远程管理但其他不运行任何其他服务器的工作站。对于运行许多服务器的计算机，你可能需要添加多个类似于 `SSH` 块的规则块，每个规则块都针对特定服务器进行定制。对于具有防火墙功能的专用路由器，重点将放在 `FORWARD` 链而不是 `INPUT` 和 `OUTPUT` 链，此类系统可能需要进行某些 `INPUT` 和 `OUTPUT` 链配置以支持自身的管理和使用。

# 练习 7.1

## 创建一个防火墙脚本

本练习将引导你创建一个简单的 `iptables` 防火墙脚本。该脚本的目标是保护工作站网络；防火墙运行在处理该网络流量的小型路由器上。（此系统应已配置为路由器。）由于受保护的网络没有从外部站点访问的服务器，所有入站连接尝试都被阻止，但允许出站连接尝试。要配置此防火墙，请按照以下步骤操作：

1. 以普通用户登录 Linux 系统。
2. 如果使用了 GUI 登录方法，从桌面环境菜单系统中启动 `xterm`。
3. 获取 `root` 权限。你可以在 `xterm` 中输入 `su`，在 `Konsole` 中选择 `Session > New Root Console`，或者使用 `sudo`（如果已配置）运行以下命令。
4. 使用你喜欢的编辑器创建一个防火墙脚本。该文件名为 `/usr/local/firewall`。
5. 将第 10 步之后的代码输入防火墙文件作为防火墙脚本。为你的网络更改变量 `LocalNet` 的值。

## 练习 7.1 (继续)

6. 保存防火墙脚本并退出编辑器。
7. 输入 `chmod a+x /usr/local/firewall` 使防火墙脚本具有可执行权限。
8. 输入 `/usr/local/firewall` 运行防火墙脚本。
9. 输入 `iptables -L` 验证防火墙规则是否已激活。
10. 配置系统在启动时运行防火墙脚本。这可以通过从本地启动脚本（如 `/etc/rc.d/rc.local`）中调用该脚本、创建一个调用防火墙脚本的新 `SysV` 启动脚本，或者用调用新脚本替换现有的防火墙启动脚本来实现。

```bash
#!/bin/bash

LocalNet=172.24.21.0/24

iptables -F INPUT
iptables -F FORWARD
iptables -F OUTPUT

iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

# 允许环回接口上的流量通过
iptables -A OUTPUT -d 127.0.0.1 -o lo -j ACCEPT
iptables -A INPUT -s 127.0.0.1 -i lo -j ACCEPT

# 允许 DNS 流量通过
iptables -A OUTPUT -p udp --port 53 -j ACCEPT
iptables -A INPUT -p udp --port 53 -j ACCEPT
```

## 第 7 章 文档与安全

## 练习 7.1 (继续)

```bash
# 允许从本地系统到外部的流量通过
iptables -A FORWARD -p tcp --port 1025:65535 -s $LocalNet -j ACCEPT
iptables -A FORWARD -p udp --port 1025:65535 -s $LocalNet -j ACCEPT
iptables -A FORWARD -p icmp -s $LocalNet -j ACCEPT

# 只允许已建立的入站连接通过
iptables -A FORWARD -p tcp --port 1025:65535 -d $LocalNet \
  -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -p udp --port 1025:65535 -d $LocalNet \
  -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -p icmp -d $LocalNet \
  -m state --state ESTABLISHED,RELATED -j ACCEPT
```

```bash
# 允许本地到本地 SSH 服务器的连接通过
iptables -A OUTPUT -p tcp --port 22 -d $LocalNet -m state \
  --state ESTABLISHED,RELATED -j ACCEPT

iptables -A INPUT -p tcp --port 22 -s $LocalNet -m state \
  --state NEW,ESTABLISHED,RELATED -j ACCEPT
```
