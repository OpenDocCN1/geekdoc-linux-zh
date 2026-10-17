
该工具的优势在于，它不仅检测扫描，还允许用户对源采取反制措施。该工具可以检测普通扫描以及隐蔽扫描。它作为攻击和潜在入侵的前兆发挥作用。`PortSentry`可以通过多种方式响应，包括以下：

- 可以通过`syslog`实用程序记录扫描。
- 可以在`/etc/hosts.deny`文件中添加条目，以禁止来自该主机的连接。
- 意识到系统上开放的可用端口可以启动扫描，以确定该主机正在运行哪些服务。
- 它监控`TCP`和`UDP`扫描，并检测诸如连接扫描、`SYN`扫描和`FIN`扫描等隐蔽扫描。

# LIDS（Linux 入侵检测系统）

`LIDS`有一个内置的端口扫描检测器，在内核中运行，并通过`syslog`记录任何违规主机。

# Linux 中的密码破解

## 工具：John the Ripper

`John the Ripper`旨在通过标准的猜测技术找到标准的`UNIX` 8 字符`DES`加密密码。该工具可以破解标准和双长度`DES`、`MDS`以及`Blowfish`算法。由于该工具可用于不同平台，因此可以在机器之间传输。用户可以指定要使用的单词表或规则。任何会话都可以暂停或重新启动，并且可以获取中断或正在运行的会话的状态。

还可以指定要针对的用户或组。它可以通过在命令行上传递密码文件来运行（这通常是`/etc/shadow`的副本）。由于其中包含加密的密码，因此应仅允许`root`读取。

图 1-8 展示了 `John the Ripper` 的截图。

## 工具：Slurpie

该工具可以在分布式环境中运行。它提供一个密码文件供程序在单个主机或多个主机上运行。因为它同时在多个主机上运行，所以可以显著加快破解过程。

# Linux 中的防火墙：IPTables

`Linux`在内核层面处理数据包过滤。进入或穿过系统的数据只有在匹配允许该数据包的规则集（称为过滤器）时才会通过。过滤器可以根据协议的、源和目标地址，或目标端口对数据包进行分类。

不同的内核使用不同的过滤程序。2.2 内核使用`IPChains`。自 2.4 内核起，过滤程序已变为`IPTables`。`IPTables`比`IPChains`拥有更多功能。

![](img/0c79e6db97822eb68322dfe40d8564fe_37_0.png)

图 1-8 这是 `John the Ripper` 密码猜测界面。

要运行 `IPTables`，必须在内核中配置以下选项。`CONFIG_PACKET`选项允许应用程序和实用程序直接与各种网络设备交互。它简化了内置链（`INPUT`、`OUTPUT`和`FORWARD`）中数据包协商的行为。`iptables`命令用于配置`IP`过滤和网络地址转换（`NAT`）。数据包过滤和`NAT`功能是分开的。为此，有两个称为`filter`和`nat`的规则表。如果用户未指定`-t`选项来覆盖它，则使用`filter`表。

还提供了五个内置链。`INPUT`和`FORWARD`链可用于`filter`表，`PREROUTING`和`POSTROUTING`链可用于`nat`表，而`OUTPUT`链可用于两个表。除本地生成的数据包（在`OUTPUT`链中处理）外，所有连接跟踪都在`PREROUTING`链中处理。`IPTables`在`PREROUTING`链内完成所有状态重算。如果在流中发送第一个数据包，状态会在`OUTPUT`链中设置为`NEW`，当系统接收返回数据包时，门控会在`PREROUTING`链中更改为`ESTABLISHED`。如果本地机器不是第一个数据包的发起者，`NEW`状态会在`PREROUTING`链中设置。因此，所有状态更改和计算都在`nat`表的`PREROUTING`和`OUTPUT`链中完成。

## IPTables 的工作原理

除了能够根据`TCP`标志和`TCP`选项以及`MAC`地址进行过滤外，它还可以控制限速连接和记录功能。以下步骤展示了 `IPTables` 的工作方式：

1. 一个数据包进入网络接口。
2. 接口解包数据链路层信息。
3. 接口将数据包转发到内核。
4. 内核检查数据包并选择拒绝、丢弃或接受它。

图 1-9 展示了 `IPTables` 决策树。图 1-10 展示了数据包如何与 `IPTables` 交互。

## 工具：Netfilter

为了简化内核防火墙代码中数据报处理的某些方面，并创建一个更清晰、更灵活的过滤框架，`Paul Russell`创建了一个名为`Netfilter`的新框架。`IPTables`实用程序用于配置`Netfilter`过滤规则。其语法大量借用了`IPChains`命令，但其区别在于其功能可以在不重新编译的情况下扩展。它通过使用共享库来实现这一点。

`Netfilter`提供三种基本功能：

1. 接受数据包或允许数据包通过
2. 拒绝数据包并通知过滤规则的源
3. 丢弃数据包

## IPTables 命令

`IPTables`检查每个传入数据包并决定如何处理它。根据被监控的数据包类型以及对数据包采取的操作，可以使用多个表。`IPTables`命令的语法如下：

```bash
iptables [-t <table-name>] <command> <chain-name> <parameter-1> <option1> <parameter-n> <option-n>
```

以下命令配置 `IPTables` 允许防火墙接受经由接口到达、来自任何 `IP` 地址且目标为防火墙 `IP` 地址 `192.168.1.1` 的 `TCP` 数据包：

```bash
iptables -A INPUT -s 0/0 -i eth0 -d 192.168.1.1 -p TCP -j ACCEPT
```

以下命令对配置 `IPTables` 允许防火墙发送 `ICMP` 回显请求（ping），并相应地接受预期的 `ICMP` 回显应答：

```bash
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

![](img/0c79e6db97822eb68322dfe40d8564fe_39_0.png)

版权所有 © EC-Council

保留所有权利。严禁复制

### 图 1-9

这是一个 `IPTables` 决策树。

![](img/0c79e6db97822eb68322dfe40d8564fe_39_1.png)

版权所有 © EC-Council

保留所有权利。严禁复制

### 图 1-10

此图展示了数据包如何与 `IPTables` 进行交互。

# 基本的 Linux 操作系统防御

`Linux`拥有许多内置的保护机制，网络管理员应通过`/etc/sysctl.conf`文件修改`/proc`文件系统下的系统内核参数来激活这些机制。
