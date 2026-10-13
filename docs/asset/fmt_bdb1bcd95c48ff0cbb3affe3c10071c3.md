
```
# iptables -t nat -A PROUTING -o eth0 -j MASQUERADE
```

要更改离开你系统的数据包的源地址，你会使用带有 `SNAT` 目标的 `PROUTING` 规则。对于 `SNAT` 目标，你使用 `--to-source` 选项来指定源地址：

```
# iptables -t nat -A PROUTING -o eth0 -j SNAT --to-source 192.168.0.4
```

要更改到达你系统的数据包的目的地址，你会使用带有 `DNAT` 目标和 `--to-destination` 选项的 `PRERUTING` 规则：

```
# iptables -t nat -A PRERUTING -i eth0 \
-j DNAT --to-destination 192.168.0.3
```

要重定向数据包，请在 `PRERUTING` 链上使用 `REDIRECT` 规则：

```bash
# iptables -t nat -A PRERUTING -i eth1 --dport 80 -j REDRECT --to-port 3128
```

通过 `TOS` 和 `MARK` 目标，你可以对数据包进行标记改处理以控制其路由或优先级。`TOS` 目标设置数据包的服务类型，可以使用如普通服务、最小成本、最大吞吐量等标准来设置优先级。

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_884_0.png)

# Red Hat Linux 8：完整参考

此处显示了仅对 `NAT` 表有效的目标：

| | 描述 |
| --- | --- |
| `SNAT` | 修改源地址，使用 `--to-source` 选项指定新的源地址 |
| `DNAT` | 修改目的地址，使用 `--to-destination` 选项指定新的目的地址 |
| `REDIRECT` | 重定向数据包 |
| `MASQUERADE` | IP 伪装 |
| `MIRROR` | 反转源并发送回给发送者 |
| `MARK` | 修改标记（Mark）字段以控制消息路由 |
| `TOS` | 修改服务类型字段以管理数据包的优先级 |

## IP Tables 脚本

虽然你可以从命令行输入 `iptables` 规则，但当你关闭系统时，这些更改将会丢失。在 Red Hat 上，你可以利用 `iptables` 服务脚本内置的支持来保存和读取 `iptables` 规则。或者你也可以自己管理过程，将其保存到你选择的文件中。无论何种情况，你可能都需要在一个可以直接执行的脚本中运行你的 `iptables` 规则。这样，你可以编辑和管理复杂的规则集，添加注释并保持它们的顺序。

## Red Hat iptables 支持

Red Hat 作为系统配置的一部分提供了 `iptables` 支持。当你安装 `iptables` 的 RPM 包时，会安装一个 `iptables` 服务脚本，它将使用 `/etc/sysconfig/iptables` 文件读取并保存 `iptables` 命令。如果你设置了 `iptables` 在系统启动时自动启动，系统将检查此文件是否存在且不为空。如果是，`iptables` 将自动读取它包含的 `iptables` 命令。这有助于将 `iptables` 更顺利地集成到系统设置过程中。

`/etc/sysconfig/iptables` 脚本由 `redhat-config-securitylevel` 自动生成。当你启动系统时，如果运行 `redhat-config-securitylevel`，`/etc/sysconfig/iptables` 文件将包含配置时的 `iptables` 规则。如果你更改了配置，`/etc/sysconfig/iptables` 文件将被新的 `iptables` 规则覆盖。你可以通过系统设置菜单或窗口中的“安全级别”（Security Level）项访问 `redhat-config-securitylevel`。

你可以通过简单删除 `/etc/sysconfig/iptables` 文件来跳过这种自动的 `iptables` 设置。运行 `redhat-config-securitylevel` 并选择“无防火墙”（No Firewall）也能达到相同的效果。确保备份它，以防其中有重要的命令。可以直接编辑 `/etc/sysconfig/iptables` 文件并输入 `iptables` 命令，但不建议这样做。相反，你应该将此文件视为存储你 `iptables` 命令的最终安装版本。

你应该将 Red Hat 提供的 `iptables` 服务脚本视为多功能管理工具，而不是服务启动脚本。使用 `service` 命令处理该脚本可能会产生困惑。`iptables` 脚本只管理 `iptables` 规则、刷新、添加或报告。它并不启动和停止 `iptables` 脚本。如果 Netfilter 未运行，你需要指示它在系统启动时启动。为此，你可以使用 `redhat-config-service`（设置窗口中的 Services），然后从服务列表中选择 `iptables`。

`/etc/rc.d/init.iptables` 服务脚本支持多种选项来管理你的规则。`status` 选项显示你所有的当前规则。`stop` 选项将刷新当前规则。与 `start` 和 `save` 选项直接绑定到 `/etc/sysconfig/iptables` 文件不同，`start` 选项将刷新 `/etc/sysconfig/iptables` 文件中的当前规则。`save` 选项将你的当前规则保存到 `/etc/sysconfig/iptables` 文件。请记住，`stop` 和 `status` 操作作用于当前的 iptables 规则，无论是在命令行手动添加的、通过你自己的脚本添加的，还是通过 `start` 选项从 `/etc/sysconfig/iptables` 添加的。以下命令将列出你的当前规则：

- `iptables status`

对于任何更改，请编辑您的 iptables 脚本。然后，再次运行服务脚本以清除旧规则。再次运行 iptables 脚本，并使用服务脚本的 `status` 选项查看它们是如何实现的：

```
service iptables stop
./myfilters
service iptables status
```

一旦您确认 iptables 规则运行正常，就可以将规则保存到 `/etc/sysconfig/iptables` 文件中。使用带有 `save` 选项的服务脚本即可。这样您的规则在系统启动时就会被自动读取。您可以将 `save` 操作视为将您的 iptables 规则安装到系统中，使其在您每次启动系统时都成为系统设置的一部分：

```
service iptables save
```

要进行更改，请修改您的 iptables 脚本，运行带有 `stop` 选项的服务脚本以清除旧规则，运行 iptables 脚本，然后使用带有 `save` 选项的服务脚本生成新的 `/etc/sysconfig/iptables` 文件。

除了使用服务脚本，您可以使用 `iptables-save` 脚本保存规则。推荐使用的文件是 `/etc/iptables.rules`。服务脚本实际上使用了带有 `-c` 选项的 `iptables-save` 将规则保存到 `/etc/sysconfig/iptables` 文件。`iptables-save` 的 `-c` 选项在输出中包含计数器（iptables 服务脚本设计用于解析计数器信息）。`iptables-save` 命令将规则输出到标准输出。要将其保存到文件中，您必须使用重定向运算符 `>` 将输出重定向到文件，如下：

```
iptables-save -c > /etc/sysconfig/iptables
```

您也可以将规则保存到您选择的文件，例如 `/etc/iptables.rules`。`/etc/rc.d/init.d/iptables` 服务脚本定义了 `IPTABLES_CONFIG` 变量，该变量存储了 iptables 配置文件的名称 `/etc/sysconfig/iptables`。

```
iptables-save > /etc/iptables.rules
```

然后，要恢复规则，请使用 `iptables-restore` 脚本从该保存的文件读取 iptables 命令：

```
iptables-restore < /etc/iptables.rules
```

## 第 35 章：网络防火墙：Netfilter

## iptables 脚本示例
