

和 **sshd** 从控制其操作的配置文件中读取数据不同，你必须为 **iptables** 提供一系列命令，以构建一组保存在内核中的数据包过滤规则。

## 显示规则
执行命令 **iptables** –L 或 **service iptables status** 以显示 **iptables** 正在运行的规则。

## 保存规则
有两种方法可以在每次系统启动时设置相同的规则集。首先，你可以将 **iptables** 命令放入脚本中，并在每次系统启动时运行该脚本。你可以从 /etc/rc.d/rc.local 调用此脚本。

其次，你可以将要执行的 **iptables** 命令的参数放入 /etc/sysconfig/iptables 中。**system-config-firewall** 实用程序（第 923 页）和 Anaconda 安装程序（第 62 页）都使用这种技术，它们构建规则集并将相应的 **iptables** 命令参数存储在 /etc/sysconfig/iptables 中。系统启动时，这些规则会被读取到内核中。如果你以这种方式使用 /etc/sysconfig/iptables 文件，请注意 **system-config-firewall** 会覆盖此文件。

有关在 kernel 中复制数据包过滤规则的信息，请参阅第 922 页。

## iptables-config
**iptables** 服务会执行 /etc/sysconfig/iptables-config 文件。请参阅该文件中的注释以了解你可以设置的选项。

## 重置 iptables
如果你遇到与防火墙规则相关的问题，你可以通过输入以下命令将内核中的数据包处理规则恢复为默认状态，而无需重新启动系统：

```
# iptables --flush
# iptables --delete-chain
```

这些命令删除所有链中的所有规则，并删除任何用户定义的链；它们不会更改策略。因此，如果策略为 ACCEPT（–P ACCEPT），清除规则会打开防火墙，使其接受所有数据包；如果策略为 DROP（–P DROP），清除规则会导致防火墙丢弃所有数据包。

如果你需要快速锁定系统，请参阅第 913 页的“紧急断开连接”。

# iptables 命令结构

### 命令行
本节描述了在实用程序名称 **iptables** 之后的 **iptables** 命令行组件。除非另有说明，**iptables** 实用程序不敏感于命令行中参数的位置。本章中的示例反映了一种普遍接受的语法，便于命令的阅读、理解和维护。并非所有命令都包含所有组件。

**iptables** 命令行上的许多标记有两种形式：短形式，由单个连字符前的单个字母组成；长形式，由两个连字符前的单词组成。大多数脚本为了简洁而使用短形式；使用长形式的行可能会变得冗长。以下 **iptables** 命令是等价的，并作为本节的示例使用：

```
# iptables --append FORWARD --in-interface eth1 --out-interface eth0 --jump ACCEPT
# iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

该表格指定命令操作的表格名称：**Filter**、**NAT** 或 **Mangle**。你可以在任何 `iptables` 命令中指定表名。如果不指定表名，命令将作用于 Filter 表。本章中的大多数示例都不指定表名，因此作用于 Filter 表。将表格指定为 `--tablename` 或 `--table` *tablename*。

该命令告诉 `iptables` 如何处理命令行的其余部分——例如，添加或删除规则、显示规则或添加链。示例命令 `-A` 和 `--append` 将命令行指定的规则追加到指定的表（默认为 Filter 表）和链中。有关命令的信息，请参阅第 916 页。

链指定此规则所属的链的名称，或者此命令操作的链的名称。链是 **INPUT**、**OUTPUT**、**FORWARD**、**PREROUTING**、**POSTROUTING**，或者是用户定义链的名称。通过在命令行上不带前导连字符的链名来指定链。本节开头的示例处理 FORWARD 链。

有两种类型的匹配标准：*数据包匹配* 标准，它匹配网络数据包；以及 *规则匹配* 标准，它匹配现有规则。

数据包匹配标准识别网络数据包并实现对匹配标准的数据包采取行动的规则。数据包匹配标准和操作的组合称为 *规则规范*。规则规范是数据包过滤的基础。本节开头的第一个示例使用 `--in-interface` *eth1* `--out-interface` *eth0* 规则匹配标准。第二个示例使用相同标准的短形式：`-i` *eth1* `-o` *eth0*。这两个规则都转发进入设备 *eth1* 并离开设备 *eth0* 的数据包。

规则匹配标准识别现有规则。`iptables` 命令可以修改、删除新规则或将其放置在由规则匹配标准指定的规则旁边。识别现有规则有两种方法：你可以使用创建该规则时使用的相同规则规范，或者使用规则的 *序号*，称为 *规则编号*。规则编号从 1 开始，表示链中的第一条规则，可以使用 `iptables` `-L` `--line-numbers` 显示。下面的第一条命令删除本节开头列出的规则；第二条命令用一条拒绝来自 IP 地址 192.168.0.10 的所有数据包的规则替换 INPUT 链的第 3 号规则 `(-R)`：

```
# iptables --delete -A FORWARD -i eth1 -o eth0 -j ACCEPT
# iptables -R INPUT 3 --source 192.168.0.10 --jump REJECT
```

跳转或目标指定内核对匹配规则所有匹配标准的数据包采取的操作。将跳转或目标指定为 `-j` *target* 或 `--jump` *target*。本节开头的示例使用以下命令指定 **ACCEPT** 目标：`--jump` **ACCEPT** 和 `-j` **ACCEPT**。

跳转将控制权转移到同一表内的不同链。以下命令向 **INPUT** 链添加一条规则，该规则将使用 TCP 协议 `(--protocol` *tcp*) 的数据包转移到名为 *tcp_rules* (`--jump` *tcp_rules*) 的用户定义链：

```
# iptables --append INPUT --protocol tcp --jump tcp_rules
```

当数据包完成遍历 **tcp_rules** 链后，假设它没有被丢弃或拒绝，它将从跳转来源规则之后的规则继续遍历 INPUT 链。

## 目标
目标指定内核对数据包采取的操作；最简单的操作是 **ACCEPT**、**DROP** 和 **REJECT**。以下命令向 FORWARD 链添加一条规则，拒绝来自 FTP 端口的 TCP 数据包（\*/etc/services，文件 \*iptables* 用于确定要使用哪个端口，显示 FTP 使用端口 21）：

```
# iptables --append FORWARD -p tcp --sport ftp --jump REJECT
```

某些目标，如 LOG，是非终结性的：在执行目标后，控制权传递给下一条规则。有关如何使用目标的信息，请参阅第 921 页。

# 使用 iptables 构建规则集

本节描述了组成 \*iptables* 规则的详细信息。它从 \*iptables* 命令开始；继续介绍数据包匹配标准、显示标准和匹配扩展；并以目标结束。

要指定表格，常见的做法是将表格声明放在紧随 \*iptables 之后的命令行上。例如，以下命令刷新（删除 NAT 表中的所有规则）NAT 表：

```
# iptables -t NAT -F
```

## 命令

- **\-\-append -A** 将 *rule-specifications* 指定的规则添加到 *chain* 的末尾。当数据包匹配所有 *rule-specifications* 时，*target* 处理它。
  - `iptables -A chain rule-specifications --jump target`

- **\-\-delete -D** 根据 *rule-numbers* 或 *rule-specifications* 从 *chain* 中删除一个或多个规则。
  - `iptables -D chain rule-numbers | rule-specifications`

- **\-\-insert -I** 将 *rule-specifications* 和 *target* 指定的规则添加到 *chain* 中由 *rule-number* 指定的位置。如果你不指定 *rule-number*，默认为 1，即链的头部。
  - `iptables -I chain rule-number | rule-specifications --jump target`

- **\-\-replace -R** 用 *rule-specification* 和 *target* 替换 *chain* 中的规则编号 *rule-number*。如果 *rule-number* 或 *rule-specification* 解析出多个地址，命令将失败。
  - `iptables -R chain rule-number | rule-specification --jump target`

