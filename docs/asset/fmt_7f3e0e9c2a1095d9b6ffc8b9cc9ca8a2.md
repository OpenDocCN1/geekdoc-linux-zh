
因为我们在本章中多次使用了“用户空间”这个术语，我们想到这可能会让那些不是长期使用 Linux 的用户和开发者感到困惑。

内核开发者将人们实际使用和交互的程序称为“用户空间”代码。本质上，用户空间程序是那些真正让你完成有用工作的程序，而 Linux 内核则在后台默默运行，不为人知，也得不到应有的赞赏，除非出了什么问题。

当用户空间代码和内核功能具有相同的名称时（如 `ipchains` 和 `iptables` 的情况），可能会让 Linux 新手感到有些困惑。

如果你没有 `ipchains`，或者想确认是否拥有最新版本，你可以在 `http://netfilter.gnumonks.org/ipchains/` 找到代码和 HOWTO 文档。

自从 `2.4.x` 内核发布以来，`ipchains` 的开发似乎明显放缓。撰写本文时，`ipchains` 的最新版本是 2000 年 10 月 5 日发布的 `1.3.10`。

## ipchains 语法

自然，要修改内核设置，你需要以 root 身份登录。我们强烈建议，如果你正在试验 `ipchains`，请使用一台对你公司网络运营不关键的机器——或者至少等到下班后，那时一个小错误不会招致全体员工和老板的愤怒。如果你的公司规模足够大，需要安排两班或更多班次，这会使下班后工作变得极其不便或不可能，那么它也应该有能力购置几台测试机器。

`ipchains` 的语法相当简单。基本命令语法为 `ipchains [-action] chainname [options]`。使用 `ipchains` 命令可以在内核中创建、修改或删除规则链。规则可能会变得有些复杂，但它们是由简单规则组合而成的。

演示 `ipchains` 最简单的方式是举一个简单的例子。在处理你的链之前，你可能想查看已加载了哪些链，所以运行 `ipchains -L` 查看已有哪些规则。如果尚未设置任何规则，应该会看到类似如下的输出：

```
root@host:/ > ipchains -L
Chain input (policy ACCEPT):
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

默认情况下，`ipchains -L` 会列出所有规则。如果你想指定某个链，可以使用类似下面的命令：

```
root@host:/ > ipchains -L input
Chain input (policy ACCEPT):
```

## 向链中添加规则

默认存在三条链：`input`、`forward` 和 `output`。你大概不会感到意外：`input` 链处理传入的数据包，输出链处理传出的数据包，`forward` 链处理到达路由器/防火墙但目标是转发到其他主机的数据包。

向链中添加规则的语法很简单：`ipchains [-A] chainname options`。如果你特别喜欢打字，也可以用 `[-append]` 代替 `[-A]`。记住，必须先将链创建出来，才能向其中添加规则。如果你指定了一个不存在的链，只会收到一条错误消息。

举例来说，假设你想默认拒绝所有传入的数据包，然后允许一些特定的流量。第一步是定义一条默认规则，如下所示：

```
root@host:/ >ipchains -P input REJECT
```

这将创建一条默认规则，拒绝所有传入的数据包。这样做有点极端，所以让我们添加一条规则，允许部分流量通过，如下所示：

```
root@host:/ >ipchains -A input -i eth0 -s 10.0.0.0/24 -j ACCEPT
```

`-s 10.0.0.0/24` 参数告诉 `ipchains` 接受（`-j ACCEPT`）来自内部（`10.0.0.0`）网络、子网掩码为 `255.255.255.0`、发往任意目的地的所有传入数据包。如果你愿意，也可以使用 `-d` 选项指定目标地址。有时，明确哪些 IP 地址不应匹配某条规则会更容易。在这种情况下，可以使用 `-s ! 10.0.0.0/24`，即使用“!”表达式。

`-j` 选项告诉 `ipchains` “跳转”到某条规则，基本上就是针对匹配该规则的任何数据包做出一项决定。在本例中，我们是在告诉 `ipchains` 接受这些数据包。顺带一提，对于匹配给定规则的目标数据包，你可以选择 `ACCEPT`、`DENY`、`REJECT`、`MASQ`、`REDIRECT` 或 `RETURN`。完整细节请参阅 `ipchains` 手册页。

## 链名称与大小写敏感

值得指出的是，规则链或表的名称是大小写敏感的，这与 *NIX 世界中的大多数事物一样。在使用 `2.2.x` 系列时，默认链是 “`input`、`forward`、`output`”。在使用 `2.4.x` 系列时，默认链变为 “`INPUT`、`FORWARD`、`OUTPUT`”。

## 刷新链

如果你为一条链创建了一组规则，现在想清除它们，只需使用 `-F` 选项“刷新”该链。例如，如果你想清除所有 `input` 规则，可以输入 `ipchains -F input`。

这将完全重置规则链。但是，如果你只想从链中删除一条规则，则应改用 `-D`（drop）选项。每条链中的规则都带有编号，因此如果你想删除链中的第一条规则，可以执行 `ipchains -D input 1`。记住，要检查已设置的规则，可以使用 `ipchains -L` 或 `ipchains -L chainname`。

## 从 1 开始计数

刚接触 Linux 和/或编程的人，可能会觉得从 1 开始编号的做法相当直白。然而，对于与 Linux 内核内部相关的事物，编号方案从 1 开始并不常见。通常任何编号方案都是从 0 开始依次递增。例如，如果你有一个多处理器系统，它们会被编号为 `CPU0`、`CPU1`，依此类推。

## 保存和恢复配置

在摆弄了一整天 `ipchains` 之后，你终于得到了完全想要的配置。恭喜！现在该确保在需要重启或系统断电时，能够恢复你的黄金配置。记住，你用 `ipchains` 设置的规则不会永久生效；每次计算机重启后都需要重新恢复。

不过这非常简单。`ipchains` 的作者附带了两个脚本：`ipchains-save` 和 `ipchains-restore`，让你的生活轻松很多。当你的配置完全符合心意时，运行 `ipchains-save > router_config`。这会将当前规则保存到一个名为 `router_config` 的文件中，你可以通过 `ipchains-restore router_config` 重新加载它。

## 更多关于 ipchains 的内容

虽然这并不是对 `ipchains` 的详尽介绍，但应该足以让你入门。如果你有兴趣进行全面的防火墙设置，可能想看看 Robert L. Ziegler 所著的《Linux 防火墙》，该书同样由 New Riders 出版。（没错，即使这本书不是 New Riders 出版的，我们也会推荐……这只是个巧合。）书中非常详细地介绍了如何使用 `ipchains` 创建防火墙。

## Netfilter 和 iptables 简介

`Netfilter` 与 `iptables` 之间的区别似乎被混淆得相当严重。实际上，`Netfilter` 是 Linux 内核网络协议栈中的一组“钩子”，允许各种模块与网络数据包协同工作。当数据包在栈中传输时，`Netfilter` 可以允许模块丢弃数据包、转发它、将其排队供内核外的程序处理，或以某种方式更改它。

`iptables` 程序是一个用户空间程序，用于向网络表添加规则。从技术上讲，使用除 `iptables` 之外的程序与 `Netfilter` 框架交互应该是可行的。

`Netfilter` 框架和 `iptables` 是 `ipchains` 的直接后继者，这意味着 `iptables` 与 `ipchains` 有很多共同之处。在很大程度上，它们共享相同的语法和选项，只有一些细微的改动。

`Netfilter` 不仅仅是 `iptables` 的另一个名称。`Netfilter` 还支持 NAT、用于向后兼容的 `ipchains` 和 `ipwadm` 模块以及连接跟踪系统。

## 2.2.x 与 2.4.x 之间的差异

从你的角度来看，`2.2.x` 系列和 `2.4.x` 系列之间数据包过滤、IP 伪装和 NAT 发生了多少变化取决于你的观点。内部发生了相当多的变化，并且增加了新的功能，允许有状态过滤和其他功能，使 Linux 成为路由方面不可忽视的力量。

然而，`ipchains` 和 `iptables` 语法之间的差异并不太剧烈。有些变化，但任何做过 `ipchains` 工作的人都应该能够轻松掌握 `iptables`。

## 使用 iptables

与 `ipchains` 一样，你需要拥有适当的内核模块已编译/启用，并且也安装了 `iptables` 程序。如果没有 `iptables`，你可以从 Netfilter 项目主页 `http://netfilter.gnumonks.org` 下载它。

## 最新版本
