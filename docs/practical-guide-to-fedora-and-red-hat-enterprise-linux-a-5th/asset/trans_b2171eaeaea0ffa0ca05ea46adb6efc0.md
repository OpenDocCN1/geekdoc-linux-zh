

## 快速入门：使用 system-config-firewall 构建防火墙

![](img/f28adb66a7398a382f0505e0ba74a872_864_0.png)

图 25-3 防火墙配置窗口

要运行此实用程序，请在命令行中输入 `system-config-firewall` (*FEDORA*) 或 `system-config-securitylevel` (*RHEL*)，或者选择 **系统 > 管理 > 防火墙** (*FEDORA*) 或 **系统 > 管理 > 安全级别和防火墙** (*RHEL*)。`system-config-firewall` 和 `system-config-securitylevel` 实用程序构建的防火墙极其简单，但在处理复杂配置时会显得力不从心。`system-config-securitylevel` 实用程序显示一个更简单的窗口，其中包含 `system-config-firewall` 功能的一个子集。本节描述 `system-config-firewall` 实用程序，该实用程序会显示防火墙配置窗口（图 25-3）。

要启用防火墙，请单击工具栏上的 **启用**。防火墙会自动允许本地发出的数据包通过到外部（通常是互联网），并允许这些数据包的响应返回。

单击本地系统提供的服务旁边的复选框。这些复选框设置了一个防火墙，允许本地系统作为一个或多个类型的服务器运行，包括 FTP、邮件 (SMTP)、Samba、安全 WWW (HTTPS)、SSH 和 WWW (HTTP)。

### 开放受信任的服务

开放其他端口：通过单击窗口左侧的 **其他端口**，然后单击 **添加** 来打开“端口和协议”窗口，输入您想要开放的其他端口。此窗口允许您从列表中进行选择，或者如果在标记为 **用户定义** 的框中勾选，指定要开放的端口及其使用的协议（TCP 或 UDP）。单击 **应用** 和 **确定**，`system-config-firewall` 将设置防火墙。如有必要，单击 **启用**。有关更多信息，请参阅第 833 页的“system-config-firewall：生成一组规则”。

## iptables 命令结构

命令行：本节列出了位于工具名称 `iptables` 之后的 iptables 命令行组件。除特别说明外，`iptables` 工具对命令行中参数的位置不敏感。本章中的示例反映了一种普遍接受的语法，便于阅读、理解和维护。并非所有命令都包含所有组件。

iptables 命令行上的许多标记有两种形式：短形式，由单个连字符前的单个字母组成；长形式，由两个连字符前的一个单词组成。大多数脚本为了简洁使用短形式；使用长形式的行可能会变得笨重。以下 iptables 命令行是等价的，并在本节中作为示例使用：

```bash
# iptables --append FORWARD --in-interface eth1 --out-interface eth0 --jump ACCEPT
# iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

表：指定命令操作的表的名称：Filter（过滤）、NAT（网络地址转换）或 Mangle（更改）。您可以在任何 iptables 命令中指定表名。如果不指定表名，命令将操作 Filter 表。本章中的大多数示例不指定表名，因此操作 Filter 表。使用 `-t tablename` 或 `--table tablename` 指定表。

命令：告诉 iptables 对命令行的其余部分执行什么操作——例如，添加或删除规则、显示规则或添加链。示例命令 `-A` 和 `--append` 将命令行指定的规则附加到指定的表和链中。请参阅第 827 页的命令列表。

链：指定该规则所属的链的名称，或该命令操作的链的名称。该链是 INPUT（输入）、OUTPUT（输出）、FORWARD（转发）、PREROUTING（预路由）、POSTROUTING（后路由）或用户定义链的名称。通过在命令行上输入链的名称（前面没有任何连字符）来指定链。本节开头的示例操作 FORWARD 链。

有两种匹配准则：*数据包匹配* 准则，用于匹配网络数据包；以及 *规则匹配* 准则，用于匹配现有规则。

数据包匹配准则识别网络数据包并实现针对匹配该准则的数据包执行操作的规则。数据包匹配准则和操作的组合称为 **规则规范**。规则规范构成了数据包过滤的基础。本节开头的第一个示例使用 `--in-interface eth1 --out-interface eth0` 规则匹配准则。第二个示例使用相同准则的短形式：`-i eth1 -o eth0`。这两个规则都转发通过设备 `eth1` 进入并通过设备 `eth0` 出去的数据包。

规则匹配准则识别现有规则。`iptables` 命令可以修改、删除或将在规则匹配准则指定的规则旁边定位的新规则。识别现有规则有两种方法：您可以使用创建该规则时使用的相同规则规范，或者可以使用该规则的序数，称为 **规则号**。规则号从 1 开始，表示链中的第一个规则，并可以使用 `iptables -L`（或 `--line-numbers`）显示。下面的第一个命令删除本节开头列出的规则；第二个命令将 INPUT 链中的规则号 3 替换为一个拒绝来自 IP 地址 192.168.0.10 的所有数据包的规则：

```bash
# iptables --delete FORWARD -i eth1 -o eth0 -j ACCEPT
# iptables -R INPUT 3 --source 192.168.0.10 -j REJECT
```

**跳转或目标** 指定内核对匹配规则所有匹配准则的数据包采取什么操作。使用 `-j target` 或 `--jump target` 指定跳转或目标。本节开头的示例使用以下命令指定 ACCEPT 目标：`--jump ACCEPT` 和 `-j ACCEPT`。

跳转将控制权转移到同一表内的不同链。以下命令向 INPUT 链添加一条规则（`--append`），该规则将使用 TCP 协议（`--protocol tcp`）的数据包转移到名为 `tcp_rules` 的用户定义链（`--jump tcp_rules`）：

```bash
# iptables --append INPUT --protocol tcp --jump tcp_rules
```

当数据包完成遍历 `tcp_rules` 链后（假设它没有被丢弃或拒绝），它将继续从它跳转出来的那条规则之后的 INPUT 链规则中遍历。

目标指定内核对数据包采取的操作；最简单的操作是 ACCEPT（接受）、DROP（丢弃）和 REJECT（拒绝）。以下命令向 FORWARD 链添加一条规则，该规则拒绝来自 FTP 端口（1）（/etc/services，iptables 用于确定使用哪个端口的文件显示 FTP 使用端口 21）的数据包：

```bash
# iptables --append FORWARD --sport ftp --jump REJECT
```

一些目标，如 LOG，是 **非目标性的：** 执行目标后，控制权传递给下一条规则。有关如何使用目标的信息，请参阅第 831 页。

## 构建一组规则

要指定表，常见的做法是将表声明放在紧跟在 `iptables` 之后的命令行上。例如，以下命令刷新（删除所有规则）NAT 表：

```bash
# iptables -t NAT -F
```

## 命令

以下是 iptables 命令列表：

- `--append -A` 将由规则规范指定的规则添加到链的末尾。当数据包匹配其中一个规则规范时，目标将处理它。

```bash
iptables -A chain rule-specifications --jump target
```

- `--delete -D` 根据规则号或规则规范从链中删除一个或多个规则。

```bash
iptables -D chain rule-numbers | rule-specifications
```

- `--insert -I` 将由规则规范和目标指定的规则添加到链中由规则号指定的位置。如果未指定规则号，默认为 1，即链的头部。

```bash
iptables -I chain rule-number rule-specifications --jump target
```

- `--replace -R` 用规则规范和目标替换链中规则号的规则。如果规则号或规则规范解析出多于一个地址，命令将失败。

```bash
iptables -R chain rule-number rule-specification --jump target
```

- `--list -L` 显示链中的规则。省略链以显示所有链的规则。使用 `--line-numbers` 显示规则号，或从第 828 页的列表中选择其他显示标准。

```bash
iptables -L [chain] display-criteria
```

- `--flush -F` 从链中删除所有规则。省略链以从所有链中删除所有规则。

```bash
iptables -F [chain]
```

- `--zero -Z` 将链中或未指定链时所有链中所有数据包和字节计数器的值更改为零。与 `-L` 一起使用以在清除之前显示计数器。

```bash
iptables -Z [-L] [chain]
```

- `--delete-chain -X` 删除名为 chain 的用户定义链。如果未指定 chain，则删除所有用户定义链。不能删除目标指向的链。

```bash
iptables -X chain
```

- `--policy -P` 为内置链 builtin-chain 设置默认目标或策略 builtin-target。此策略应用于不匹配链中任何规则的数据包。如果链没有策略，未匹配的数据包将被 ACCEPT（接受）。

```bash
iptables -P builtin-chain builtin-target
```

- `--rename-chain -E` 将链 old 的名称更改为 new。

```bash
iptables -E old new
```

