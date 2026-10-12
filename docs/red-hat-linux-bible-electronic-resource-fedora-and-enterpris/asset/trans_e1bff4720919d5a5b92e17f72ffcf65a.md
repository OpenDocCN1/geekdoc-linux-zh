

| MASQUERADE | 对伪装的解释。 |
|---|---|
| REDIRECT | 将数据包重定向到新位置。 |
| RETURN | 从此链返回到调用它的链。继续在调用链中从离开的地方检查规则。 |

我已经向你展示了 *ipchains* 命令的各个组件。现在是时候将它们组合成一些实际示例了。使用 *ipchains* 可以创建非常复杂和复杂的规则列表，但我会保持示例相对简单。保持简单通常是好的策略，因为大型、复杂的规则链会影响系统性能。花费更多时间检查规则意味着交付数据包和提供信息的时间更少。你的 Linux 机器上的流量越高，这些复杂规则链的性能影响就越大。

## 更改 ipchains 防火墙规则

现在让我们尝试添加一条规则。例如，假设我们想阻止 ICMP 数据包以禁止对我们的 Linux 机器进行“ping”。你可以这样做以避免各种可能针对系统的拒绝服务攻击。使用以下类似的命令阻止 ICMP：

```
# ipchains -A input -p icmp -j DENY
```

这指定我们正在向输入链添加一条规则。它将匹配任何 ICMP 数据包并将其丢弃而不是允许其通过。现在如果您使用 *ping* 命令 ping 您的 Linux 机器，您应该不会收到任何响应。再次输入 **ipchains -L** 命令，您会看到类似以下内容：

```
Chain input (policy ACCEPT):
target     prot opt             source          destination ports
DENY       icmp  ------  anywhere    anywhere      any  --> any
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

你可以看到新规则已列出。此规则将阻止进入系统的所有 ICMP 数据包，无论哪个计算机发送了这些数据包。如果你的 Linux 系统充当路由器，它还将阻止从互联网转发到你的网络或反之的 ICMP 数据包。互联网上的人将无法 ping 你网络上的任何东西。同样，你也无法 ping 互联网上的任何东西。也许这不是你想要的。那么假设你希望阻止互联网上的人 ping 你网络上的系统，但允许 ping 路由器并允许路由器 ping 互联网上的主机。首先，我们应该使用 -F 参数刷新输入链的内容；然后我们可以添加新规则。

```
# ipchains -F input
# ipchains -A forward -p icmp -j DENY
```

现在我们可以 ping Linux 系统，Linux 系统也可以 ping 两个主机，但 ping 请求不会通过 Linux 系统传递。如果愿意，使用 `ipchains -L` 命令验证规则现在已添加到转发链而不是输入链。

你可能还希望阻止来自互联网的 telnet 协议。对于此示例，假设我们的 Linux 路由器通过名为 ppp0 的拨号连接连接到互联网，并通过名为 eth0 的以太网连接连接到内部局域网。在这种情况下，你可以使用以下类似的命令阻止 telnet：

```
# ipchains -A input -i ppp0 -p tcp --dport 23 -j DENY
```

此规则基本上表示，任何目标端口为 23（在 `/etc/services` 中指定的 telnet 端口）的 TCP 数据包，如果到达 ppp0 接口，则应被丢弃。这并不会阻止你从内部网络 telnet 到你的 Linux 机器，但它确实阻止了来自互联网的 telnet 访问。

我将用一个更有用的示例结束。假设你希望允许任何类型的出站 TCP 连接到互联网，但希望阻止任何入站 TCP 连接。每个 TCP 连接都在两个方向发送数据包，因此乍一看似乎不可能。阻止所有入站 TCP 数据包，你的出站连接的回复数据包也会被阻止。诀窍是只阻止用于启动入站连接的初始 TCP 数据包。我们可以这样做，因为所有 TCP 连接请求都以设置了称为 SYN 位的数据包开始。我们可以使用 `--syn` 选项告诉 ipchains 查找该位。尝试以下命令：

```
# ipchains -A input -i ppp0 -p tcp --syn -j DENY
```

使用 ipchains 过滤流量有很多有用的方法。我鼓励你阅读 ipchains 手册页（输入 `man ipchains`）和 ipchains HOWTO 文档以了解更多信息。你可以在 www.tldp.org/HOWTO/IPCHAINS-HOWTO.html 找到 HOWTO 文档。

## 保存 ipchains 防火墙规则

在创建了你想要的 ipchains 规则后，将其保存到文件中非常重要；否则，在重新启动服务器时它们将被丢失。幸运的是，有一对有用的脚本（`ipchains-save` 和 `ipchains-restore`）正是为此目的提供的。本质上，`ipchains-save` 会将当前的 ipchains 规则列表回显到屏幕上。`ipchains-restore` 脚本读取特殊格式的规则列表并使其生效。在自定义 ipchains 之后，通过运行 `ipchains-save` 并将输出定向到类似以下的文件来保存新规则：

```
# /sbin/ipchains-save > /tmp/ipchains.rules
```

接下来，你可以将创建的规则添加到 /etc/sysconfig/ipchains 文件中。以 root 用户身份，使用任何文本编辑器打开该文件。然后读取你在前一个示例中创建的 ipchains.rules 文件。

## 配置 iptables 防火墙

iptables 防火墙功能（也称为 netfilter）是在安装 Red Hat Linux 时的默认防火墙软件。今天，Red Hat Linux 同时提供 ipchains 和 iptables，但一次只能激活其中一个。如今 iptables 是得到更好支持的防火墙工具。

如果你当前在 Red Hat Linux 系统上使用 ipchains 并希望转换为 iptables，你需要在使用 iptables 之前禁用 ipchains。事实上，如果在 ipchains 模块加载时尝试使用 iptables 脚本 (/etc/init.d/iptables) 启动 iptables，iptables 启动脚本会静默退出。

虽然 iptables 通常被认为比 ipchains 更复杂，但它也被认为更强大、更灵活。由于 ipchains 的开发已不再继续，存在的少数损坏的 ipchains 功能可能仍会保持损坏状态。

本节描述如何打开 iptables 并为几种不同情况设置防火墙规则。它还说明如何打开与防火墙相关的功能，使你的 iptables 防火墙能够执行网络地址转换（NAT）、IP 伪装、端口转发和透明代理。

> **NOTE:** Red Hat Linux 启动脚本如果使用某些服务会“在你的防火墙上打洞”，因此即使它们未在 iptables 配置中明确启用，也能正常工作。例如，NTP（从网络时间服务器设置系统时间）和 DNS 解析（让你联系 DNS 服务器解析地址）都会在你的防火墙上打开它们需要的端口。

### 打开 iptables

要打开 iptables，你可能需要关闭 ipchains。（如果你刚从 Red Hat Linux 8 之前的版本升级，其中 ipchains 是默认的，可能就是这种情况。）
然后你可以添加模块并创建 iptables 防火墙所需的规则。以下过程描述如何在你的 Red Hat Linux 系统上启用 iptables。

> **TIP:** 在你关闭 ipchains、打开 iptables 并为 iptables 配置过滤规则期间，你的计算机可能未受网络保护。你应该在非关键计算机上测试防火墙规则，然后在关键计算机上快速执行切换，或通过暂时关闭网络接口进行切换。

- 1. 阻止 ipchains 脚本在启动时自动启动：
  ```
  # chkconfig ipchains off
  ```
- 2. 设置 iptables 脚本在启动时自动启动：

