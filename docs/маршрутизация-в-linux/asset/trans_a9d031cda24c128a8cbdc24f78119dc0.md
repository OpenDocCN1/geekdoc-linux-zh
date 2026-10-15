

## Netfilter 和 iptables 简介

Netfilter 与 iptables 之间的区别似乎被混淆得相当严重。实际上，Netfilter 是 Linux 内核网络协议栈中的一组“钩子”，允许各种模块与网络数据包协同工作。当数据包在栈中传输时，Netfilter 可以允许模块丢弃数据包、转发它、将其排队供内核外的程序处理，或以某种方式更改它。

iptables 程序是一个用户空间程序，用于向网络表添加规则。从技术上讲，使用除 iptables 之外的程序与 Netfilter 框架交互应该是可行的。

Netfilter 框架和 iptables 是 ipchains 的直接后继者，这意味着 iptables 与 ipchains 有很多共同之处。在很大程度上，它们共享相同的语法和选项，只有一些细微的改动。

Netfilter 不仅仅是 iptables 的另一个名称。Netfilter 还支持 NAT、用于向后兼容的 ipchains 和 ipwadm 模块以及连接跟踪系统。

## 2.2.x 与 2.4.x 之间的差异

从你的角度来看，2.2.x 系列和 2.4.x 系列之间数据包过滤、IP 伪装和 NAT 发生了多少变化取决于你的观点。内部发生了相当多的变化，并且增加了新的功能，允许有状态过滤和其他功能，使 Linux 成为路由方面不可忽视的力量。

然而，ipchains 和 iptables 语法之间的差异并不太剧烈。有些变化，但任何做过 ipchains 工作的人都应该能够轻松掌握 iptables。

## 使用 iptables

与 ipchains 一样，你需要拥有适当的内核模块已编译/启用，并且也安装了 iptables 程序。如果没有 iptables，你可以从 Netfilter 项目主页 http://netfilter.gnumonks.org 下载它。

## 最新版本

即使你的发行版已预装 iptables，你也应该检查一下是否拥有最新版本。截至本文撰写时，当前版本是 1.2.2。如果你拥有的版本早于 1.2.1a，你的版本在 ip_conntrack_ftp 模块中存在安全漏洞。很难过分强调保持像 iptables 这样工具的最新版本的重要性。有时更新是为了修复小错误或添加功能，但许多更新与安全相关或解决可能在以后引起问题的严重错误。每月花几个小时检查和安装更新可能会为你节省几天清理黑客后的时间——或者在脚本小子“接管”你的系统后，节省数周寻找新工作的痛苦。

## iptables 语法

你读过关于 ipchains 的章节吗？好吧，如果你读过，那么你对使用 iptables 已经有很好的感觉了。你使用 iptables 来向 Linux 内核中 IP 数据包过滤规则的表中添加、修改或刷新规则。

### 链、规则、表……这里发生了什么？

如果不知道发生了什么，关于规则、链和表的讨论可能会让人有点困惑。实际上，即使你知道发生了什么，有时也会有点模糊。

从最小的构建块开始，规则是描述匹配数据包的标准以及对该数据包应采取的操作的方式。如果数据包匹配，它就符合一条规则。匹配一条或多条规则的数据包称为目标。

链是一组匹配一组数据包或目标的规则。最后，表是一组链的集合。在 2.4.x 内核中，你默认拥有包含 INPUT、OUTPUT 和 FORWARD 链的 filter 表，nat 和 mangle。

### 检查链

在向链添加任何规则之前，先查看现有链，看看是否已有规则潜伏其中，这可能是一个好主意。即使你没有使用 iptables，一些发行版也可能在启动文件中加入几条规则。

要查看现有规则，输入：

```
iptables -L
```

你应该会看到类似这样的内容：

```
root@host: >
Chain INPUT (policy ACCEPT)
target  prot opt source      destination
Chain FORWARD (policy
ACCEPT)
target  prot opt source      destination
Chain OUTPUT (policy
ACCEPT)
target  prot opt source      destination
```

即使目前没有规则，你也会注意到 iptables 的输出比 ipchains 更详细。

在你向某些现有链添加规则或添加自己的链后，你可能只想查看该链。在这种情况下，只需指定你想要查看的链的名称，如下所示：

```
root@host: >iptables -L CHAINNAME
```

### 向链添加规则

要向现有链之一添加规则，你将使用追加 (-A) 命令并指定要追加规则的链。你还需要指定源 (-s)、目标 (-d)、协议 (-p) 以及对目标数据包要采取的操作 (-j)。

