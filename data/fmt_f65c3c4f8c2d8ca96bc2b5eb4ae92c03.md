
- 用于发送或接收数据包的物理接口
- 某些标志的状态，如`SYN`和`ACK`位或`TOS`（服务类型）标志。`SYN=1 & ACK=0`的意义在于此类数据包是建立`TCP/IP`连接第一个包。如果设置了`ACK`（等于`1`），则该数据包是已连接的一部分
- 数据包是否为较大数据包碎片。如果你也进行伪装或`NAT`，则这不是问题，因为代码要求在转发之前对所有分片进行重组，但在某些对性能敏感的仅进行数据包过滤的情况下，匹配分片可能会很有用。

### netfilter 的术语

如所述，`netfilter`是模块化的，而这一思想的核心是使用表（tables）。表通过进入内核网络栈钩子（hooks）来实现，无法由用户空间工具创建。目前，可用的表有`filter`、`nat`和`mangle`。每个表实现了你可能对数据包执行的特定类操作：作为过滤器、执行网络地址转换或通过其他方式修改数据包（例如标记数据包以强制特定的队列算法顺序）。在数据包路径中有五种不同类型（上述的钩子），`netfilter`在此有机会检查并影响数据包的效果。表可以通过其链（chains）——链的名称以钩子名称命名——来抑制其中一个或多个钩子。我打算避免与某些解释`netfilter`的非常优秀的互联网资源产生任何混淆，并防止你将`mangle`表中的`PREROUTING`与`nat`表的`PREROUTING`钩子混淆。没有任何表关联的钩子如图 4.5 所示。现在不要纠结它们；一旦我们讨论了各种表，它们的用途将变得更加清晰。

表内部包含一组链（chains），链中包含规则（rules）。其中一些链是构建在内核中的，无法删除或重命名（但你可以向它们添加规则）。这些是内置链。链还具有策略（policies），这些策略指示了对于不匹配链上任何规则的数据包要采取什么默认操作。链中的每条规则都有一个目标（target），它指示了对匹配该目标的数据包要执行什么操作。目标可以是另一个用户定义的链，可以是表的预定义目标之一，或者是一个

![](img/e98e3956bdbeb0fcebd99cf9c0434e1b_141_0.png)

返回调用链。如果这听起来很复杂，不要被吓倒。这只是因为处理数据包的方案非常灵活，当你想要对你的路由器做一些有趣的事情时，你会感谢这种灵活性。

一点说明：数据包并不跨越“表”，而是跨越由链组成，链中包含规则。其中一些链是构建在内核中的，无法删除或重命名（但你可以向它们添加规则）。这些是内置链。链还具有策略，这些策略指示了对于不匹配链上任何规则的数据包要采取什么默认操作。链中的每条规则都有一个目标，它指示了对匹配该目标的数据包要执行什么操作。目标可以是另一个用户定义的链，可以是表的预定义目标之一，或者

### 4.3.4 iptables——netfilter 的接口

控制`netfilter`的用户空间工具是`iptables`。像它的前身`ipchains`一样，它提供了丰富的语法，因此我们将分节介绍。也像`ipchains`，但在更大程度上，某些参数在加载特定模块时适用。最后，你必须指定你希望命令应用的表，或者假设默认表`filter`。我们在表 4.3 中涵盖第一组命令。这些用于管理整个链。

注意，对于某些命令，如果不指定链，该命令将影响表中所有的链。下一组命令（表 4.4）操纵给定链内的规则，因此要求指定链。正如你从参考表的第一列中观察到的（几乎）所有`iptables`的命令行选项都以短形式和长形式可用。这些可以使网络配置脚本更具自文档性，特别是当我们遇到表 4.5 中长长的规则规范时。在规则规范中，你可以手动插入。规则规范的部分是`-j`或`--jump`。有效的目标列表取决于三个因素：你使用的表、你可能加载了哪些扩展（例如，有一个提供数据包日志功能的`LOG`目标），

表 4.3 操作链的命令

| 开关 | 参数(s) | 说明 |
|---|---|---|
| -N 或 --new | chain | 创建一个新的用户定义的链 |
| -E 或 --rename-chain | old-chain new-chain | 重命名一个用户定义的链 |
| -X 或 --delete-chain | [chain] | 删除链/所有链 |
| -Z 或 --zero | [chain] | 清零链计数器/所有链 |
| -P 或 --policy | chain target | 设置链策略为目标 |
| -F 或 --flush | [chain] | 清空链中的规则/所有链 |

# 表 4.4 修改规则的命令

| 选项 | 参数(s) | 描述 |
| --- | --- | --- |
| -A or --append | 链规则 | 向链中添加规则 |
| -D or --delete | 链规则 | 从链中删除规则 |
| -D or --delete | 链 [n] | 删除链中的第 n 条/第一条规则 |
| -I or --insert | 链 [rulenum] | 将规则插入链中（如果给出，则插入到位置 n） |
| -R or --replace | 链 n 规则 | 将链规则 n 替换为 |

# 表 4.5 指定规则

| 选项 | 参数(s) | 描述 |
| --- | --- | --- |
| -j or --jump | 目标 | 数据包匹配时要执行的操作 |
| -s or --source | [!] 地址/掩码 | [不是] 源地址 |
| -d or --destination | [!] 地址/掩码 | [不是] 目的地址 |
| -i or --in-interface | dev!] | [不是] 输入接口 + 是通配符，例如 eth+| |
| -o or --out-interface | dev!] | [不是] 输出接口 (不)真分片数 ≥ 2 |
| -f or --fragment | 协议 | [不是] 协议 协议（见注释） |
| -p or --proto | | |

在上面的表中你还创建了哪些其他自定义链。请注意，你可以创建一组形成循环的规则（或仅在某些条件下形成循环）。以下是一个愚蠢的示例，我配置了一个链来监控网络流量，另一个链来记录流量，并让它们相互调用。它们利用了`filter`过滤表，该表在第 7.3 节之前不会进行介绍，并且需要内核支持数据包过滤，但该示例的目的是展示如何将链连接起来。（而且在`nat`中，这样的规则完全没有任何意义！）

```bash
drone3: #modprobe ipt_filter
drone3: #modprobe ipt_LOG
drone3: #iptables -t filter -N test2
drone3: #iptables -t filter -A OUTPUT -j ytest2
drone3: #iptables -t filter -A ytest2 --proto tcp --dport 22
drone3: #iptables -t filter -N testchain2
drone3: #iptables -t filter -R ytest1 --proto tcp --dport 23 --jump testchain2
drone3: #iptables -t filter -A testchain2 --proto tcp --dport 23 -j LOG
drone3: #iptables -t filter -I testchain2 --proto tcp --dport 23 -j ytest2
```

`iptables`：表中发现循环

在这种情况下，我将`testchain`中的第 1 条规则替换为跳转到`testchain2`的规则，但`testchain2`尚未被创建。由于内核找不到该名称，它假设这是一个要加载的目标（就像`LOG`目标一样）。因此了这条可能具有误导性的错误信息。但我们也从这条错误信息中学习到了一些东西——`iptables`在调用时动态链接代码，以执行参数的解析和某些规则的配置。这有助于`iptables`具有扩展性，而无需重新编译或增大二进制文件的体积。在我看来，这是一个非常聪明的技巧。

# 第 4.3 节 Linux 的 netfilter 概念

```bash
drone3:~ iptables -t filter -R tonytest1 --proto tcp \
--dport 23 --jump testchain2
```

`iptables` v1.2.2: Couldn't load target 'testchain2':

`/lib/iptables/libipt_testchain2.so`:

cannot open shared object file: No such file or directory

在匹配源地址或目的地址时，你可以使用主机名以及`IP`地址。如果主机名解析为多个地址，则所有地址都将匹配。你还可以使用掩码表示法指定子网掩码。如果没有指定源地址或目的地址，则匹配任何地址。

# 4.4 使用 netfilter 进行伪装 NAT
