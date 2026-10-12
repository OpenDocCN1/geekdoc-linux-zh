
```bash
[ramon]$ sudo iptables -A INPUT -p tcp --dport smtp -j ACCEPT
[ramon]$ sudo iptables -A INPUT -j DROP
```

这个简单示例向`input`内置链添加了两条规则。第一条规则匹配所有传输层协议为`TCP`且目标`TCP`端口为`25`（互联网邮件或`SMTP`）的数据包。如果数据包匹配此规则，`Netfilter`将接受该数据包。

第二条规则是一个`捕获所有规则`（有时称为`隐身规则`，因为它将服务器隐藏于所有未明确允许直接与其通信的外部系统之外）。捕获所有规则指示`Netfilter`丢弃所有其他`input`链流量。前一个示例中的两条规则可用于确保你的邮件服务器仅接受旨在连接至`SMTP`端口的连接。

> **注意** `Netfilter` 框架相较于`2.4`之前`Linux`内核中旧有的数据包过滤支持，最重要的增强之一是对`input`和`output`链的处理。在`Netfilter`之前，无论数据包最终是绑定到其他系统（路由）还是本地系统（本地处理），内核都会对所有从网络驱动程序接收到的数据包咨询`input`链。`output`链也适用同样的情况，即转发的和源自本地的数据包都适用。这迫使网络管理员对`input`链应用非直观的规则，以考虑这两种类型的数据包。使用`Netfilter`后，只有绑定到本地处理的数据包才受`input`链约束，只有源自本地主机并绑定到其他主机的数据包才受`output`链约束。

`iptables`及其前身（`ipfwadm`、`ipchains`）满足相同的需求：每次系统重启时，将一组数据包过滤规则重新安装到内核中。由于内核没有任何非易失性存储，你需要在每次系统启动时使用`iptables`脚本重新初始化你的数据包过滤策略。由于这些规则不会在系统重启后保留，你必须将`iptables`命令放在一个脚本文件中，并将该脚本放入`/etc/rc.d/init.d`目录中。

##### 使用 iptables

并非所有`Linux`发行版都默认附带`iptables`。只需浏览你喜欢的`RPM`仓库（我最喜欢的是`www.rpmfind.net`）并按如下方式安装最新版本：

```
[ramon]$ sudo rpm -i iptables-1.1.2-1386.rpm
```

此命令在`/usr/lib`中安装了一系列共享库，安装`iptables`的手册页，以及主可执行文件`/sbin/iptables`。

在调用`iptables`命令时，你必须始终拥有`root`权限，因为它实际上是在向正在运行的内核写入链规则。

`iptables`命令的一般命令行语法如下：

```
iptables -[ADC] chain rule-specifications [options]
iptables -[RI] chain rulenum rule-specifications [options]
iptables -D chain rulenum [options]
```

###### iptables

```text
iptables -L [chain] [options]
iptables -N chain
iptables -P chain target [options]
iptables -E old-chain-name new-chain-name
```

命令行开关及其含义列于表 9.3 中。

| 开关 | 含义 |
| :--- | :--- |
| `-L` | 列出链中的所有规则。 |
| `-N` | 创建新链。 |
| `-P` | 将链的策略设置为给定的目标。 |
| `-E` | 重命名链。 |
| `-t table` | 选择要操作表。目前共有三种：`filter`（默认）、`nat`（网络地址转换）和`mangle`（专用数据包转换）。 |
| `-A` | 向链中添加规则（追加到链的末尾）。 |
| `-D` | 从链中删除规则。 |
| `-C` | 创建新链。 |
| `-R` | 替换链中现有的规则。 |
| `-I` | 在链中插入带编号的规则。 |
| `-F` | 清空链中的所有规则（清空链）。 |
| `-Z` | 将所有链上的数据包和字节计数器清零（重置）。 |
| `-X` | 删除用户定义的链。 |

`iptables`命令的`options`字段可以取表 9.4 中列出的值之一。

####### 表 9.4 iptables 命令行选项

| 选项 | 含义 |
| :--- | :--- |
| `--verbose` | 显示丰富（详细）的输出。 |
| `--numeric` | 以数字格式输出`IP`地址（不进行`DNS`查找）。 |
| `--exact` | 在输出中展开数字。 |
| `--line-numbers` | 在列出规则时显示行号。 |

##### iptables 规则规范

`iptables`命令的真正威力在于它使用丰富的规则集来匹配特定类型流量的能力。每个从服务器转发、到达服务器或由服务器发出的数据包，都会与相应链（`forward`、`input`和`output`）的规则集进行比较。如果数据包匹配该规则，则会执行指定的操作（由`-j action`选项定义）。表 9.5 列出了用于`iptables`命令中`rulespecifications`部分的参数。

###### 表 9.5 iptables 规则规范参数

| 参数 | 含义 |
| :--- | :--- |
| `-p [!]protocol` | 要匹配的协议 ID。它可以是`tcp`、`udp`、`icmp`，或者`/etc/services`中服务的任何数字或字母表示形式。 |
| `-s [!]address[/mask]` | 要匹配的源地址。它可以是主机名、`IP`地址，或以`network/mask`格式表示的网络名称。 |
| `--sport [port:[port]]` | 源端口或源端口范围的指定。 |
| `-d [!]address[/mask]` | 要匹配的目的地址。这里适用与`-s`参数相同的规则。 |
| `--dport [port:[port]]` | 目的端口或目的端口范围的指定。 |
| `-i [!]interface` | 接收数据包所经过的接口，如`eth0`、`ppp0`等。 |
| `-o [!]interface` | 发送数据包所经过的接口，如`eth0`、`ppp0`等。 |
| `[!] -f` | 数据包是更大的分片数据包的第二个或后续片段。 |

请注意，对于表 9.5 中列出的每个参数，前导的感叹号`[!]`指示`iptables`查找不符合该标准的数据包。`iptables`的规则规范参数与`ipchains`可用的参数非常相似，它们包括匹配传入数据包协议 ID（`-p`）、源地址和目的地址（`-s`和`-d`）以及源端口和目的端口号（`-sport`和`-dport`）的选项。

除了这些基本参数外，你还可以使用特定于协议的规则，为特定类型的数据包（例如，`tcp`、`udp`和`icmp`）指定扩展匹配参数。例如，下面这条`iptables`语句将匹配并允许所有携带`echo-request`类型的`ICMP`数据包（`ping`应用程序使用的数据包类型）。

```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

上一条命令的反向操作是

```bash
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

这里允许本地系统使用`echo-reply`回复`echo-request`，从而使你的系统能够正确响应`ping`请求。

表 9.6 列出了`iptables`中包含的`TCP`、`UDP`和`ICMP`流量类型对应的特定于协议的参数。

###### 表 9.6 iptables 特定于协议的数据包匹配参数

| 参数 | 含义 | 协议类型 |
| :--- | :--- | :--- |
| `--sport [! port:[port]]` | 匹配具有给定源端口或来自给定`port:port`范围的数据包。 | `tcp`, `udp` |
| `--dport [! port:[port]]` | 匹配具有给定目的端口或来自给定`port:port`范围的数据包。 | `tcp`, `udp` |
| `--port [! port]` | 匹配源端口和目的端口相等的数据包。 | `tcp`, `udp` |
| `--tcp-flags [! mask comp]` | 匹配具有指定`TCP`标志的数据包。标志包括`SYN`、`ACK`、`FIN`、`RST`、`URG`、`PSH`、`ALL`和`NONE`。 | `tcp` |
| `[!] --syn` | 匹配设置了`SYN`位且清除了`ACK`和`FIN`位的`TCP`数据包。 | `tcp` |
| `--tcp-option [! number]` | 如果数据包设置了`TCP`选项，则匹配。 | `tcp` |
