

## 5.15.2. 理解富规则结构

富规则命令的格式或结构如下：

```
rule [family="rule_family" ]
    [ source [NOT] [address="address" ] [mac="mac_address" ] [ipset="ipset"]]
    [ destination [NOT] address="address" ]
    [ element ]
    [ log [prefix="prefix_text" ] [level="log_level"] [limit_value="rate/duration"] ]
    [ audit ]
    [ action ]
```

**注意**

文件中的富规则结构使用 **NOT** 关键字来反转源地址和目的地址命令的含义，但命令行使用 `invert="true"` 选项。

规则与特定的区域相关联。一个区域可以包含多个规则。如果某些规则相互作用或相互矛盾，则第一个匹配该数据包的规则将生效。

## 5.15.3. 理解富规则命令选项

### family

如果提供了规则族（`ipv4` 或 `ipv6`），则该规则分别限制为 **IPv4** 或 **IPv6**。如果未提供规则族，则该规则将同时添加到 **IPv4** 和 **IPv6** 中。如果在规则中使用了源地址或目的地址，则必须提供规则族。端口转发也是如此。

### 源地址和目的地址

#### source

通过指定源地址，可以将连接尝试的发起方限制为源地址。源地址或地址范围是带有 **IPv4** 或 **IPv6** 掩码的 IP 地址或网络 IP 地址。对于 **IPv4**，掩码可以是网络掩码或普通数字。对于 **IPv6**，掩码是普通数字。不支持使用主机名。可以通过添加 **NOT** 关键字来反转源地址命令的含义；除提供的地址外，所有地址都匹配。

如果未指定规则的 `family`，可以为 **IPv4** 和 **IPv6** 添加 MAC 地址以及类型为 `hash:mac` 的 IP 集合。其他 IP 集合需要与规则的 `family` 设置匹配。

#### destination

通过指定目的地址，可以将目标限制为目的地址。目的地址使用与源地址相同的 IP 地址或地址范围语法。使用源地址和目的地址是可选的，并且并非所有元素都允许使用目的地址。这取决于目的地址的使用情况，例如在服务条目中。您可以将 `destination` 和 `action` 组合使用。

### 元素

元素只能是以下元素类型中的**一种**：`service`、`port`、`protocol`、`masquerade`、`icmp-block`、`forward-port` 和 `source-port`。

#### service

`service` 元素是 `firewalld` 提供的服务之一。要获取预定义服务列表，请输入以下命令：

```bash
~]$ firewall-cmd --get-services
```

如果服务提供目的地址，它将与规则中的目的地址冲突并导致错误。内部使用目的地址的服务主要是使用组播的服务。该命令的形式如下：

```
service name=service_name
```

#### port

`port` 元素可以是单个端口号或端口范围，例如 `5060-5062`，后跟协议，协议可以是 `tcp` 或 `udp`。该命令的形式如下：

```
port port=number_or_range protocol=protocol
```

#### protocol

`protocol` 值可以是协议 ID 号或协议名称。有关允许的 `protocol` 条目，请参阅 `/etc/protocols`。该命令的形式如下：

```
protocol value=protocol_name_or_ID
```

#### icmp-block

使用此命令阻止一个或多个 `ICMP` 类型。`ICMP` 类型是 `firewalld` 支持的 `ICMP` 类型之一。要获取支持的 `ICMP` 类型列表，请输入以下命令：

```bash
~]$ firewall-cmd --get-icmptypes
```

此处不允许指定操作。`icmp-block` 内部使用操作 `reject`。该命令的形式如下：

```
icmp-block name=icmp_type_name
```

#### masquerade

在规则中启用 IP 伪装（Masquerading）。可以提供源地址以将伪装限制在此区域，但不能提供目的地址。此处不允许指定操作。

#### forward-port

将带有指定为 `tcp` 或 `udp` 协议的本地端口的数据包转发到本地另一个端口、另一台机器，或另一台机器上的另一个端口。`port` 和 `to-port` 可以是单个端口号或端口范围。目的地址是简单的 IP 地址。此处不允许指定操作。`forward-port` 命令内部使用操作 `accept`。该命令的形式如下：

```
forward-port port=number_or_range protocol=protocol to-port=number_or_range to-addr=address
```

#### source-port

匹配数据包的源端口 - 即连接尝试发起方使用的端口。要匹配当前机器上的端口，请使用 port 元素。source-port 元素可以是单个端口号或端口范围（例如 5060-5062），后跟协议 tcp 或 udp。该命令的形式如下：

```
source-port port=number_or_range protocol=protocol
```

### 日志记录

#### log

使用内核日志记录（例如 syslog）记录针对规则的新连接尝试。您可以定义前缀文本，该文本将作为前缀添加到日志消息中。日志级别可以是 emerg、alert、crit、error、warning、notice、info 或 debug。使用 log 是可选的。可以按以下方式限制日志记录：

```
log [prefix=prefix_text] [level=log_level] [limit_value=rate/duration]
```

速率是自然正整数 [1, ..]，时长单位有 s、m、h、d。s 表示秒，m 表示分钟，h 表示小时，d 表示天。最大限制值为 1/d，表示每天最多一条日志条目。

#### audit

Audit 提供了一种使用发送到 `auditd` 服务的审计记录进行日志记录的替代方法。审计类型可以是 ACCEPT、REJECT 或 DROP，但在 audit 命令后不指定审计类型，因为审计类型将从规则操作中自动收集。Audit 没有自己的参数，但可以可选地添加 limit。使用 audit 是可选的。

### 操作

#### accept|reject|drop|mark

操作可以是 accept、reject、drop 或 mark。规则只能包含一个元素或一个源。如果规则包含一个元素，则匹配该元素的新连接将使用指定的操作进行处理。如果规则包含一个源，则来自源地址的所有内容都将使用指定的操作进行处理。

```
accept | reject [type=reject_type] | drop | mark set="mark[/mask]"
```

使用 accept 时，所有新连接尝试都将被允许。使用 reject 时，它们将被拒绝，其源将收到拒绝消息。拒绝类型可以设置为使用其他值。使用 drop 时，所有数据包将被立即丢弃，并且不会向源发送任何信息。使用 mark 时，所有数据包都将被标记为给定的标记和可选掩码。

## 5.15.4. 使用富规则日志命令

可以使用 Netfilter 日志目标和 audit 目标进行日志记录。会为所有区域添加一个新的链，名称格式为“zone_log”，其中 zone 是区域名称。这在 deny 链之前处理，以确保正确的顺序。根据规则的操作，规则或其部分被放置在独立的链中，如下所示：

- zone_log
- zone_deny
- zone_allow

所有日志记录规则都将被放置在“zone_log”链中，该链首先被解析。所有 reject 和 drop 规则都将被放置在“zone_deny”链中，该链在 log 链之后被解析。所有 accept 规则都将被放置在“zone_allow”链中，该链在 deny 链之后被解析。如果规则包含 log 以及 deny 或 allow 操作，则指定这些操作的规则部分将被放置在匹配的链中。

### 5.15.4.1. 使用富规则日志命令示例 1

启用新的 IPv4 和 IPv6 连接用于认证头协议 AH：

```
rule protocol value="ah" accept
```

### 5.15.4.2. 使用富规则日志命令示例 2

允许新的 IPv4 和 IPv6 连接用于协议 FTP，并使用 audit 每分钟记录 1 次：

```
rule service name="ftp" log limit value="1/m" audit accept
```

### 5.15.4.3. 使用富规则日志命令示例 3

允许来自地址 192.168.0.0/24 的新 IPv4 连接用于协议 TFTP，并使用 syslog 每分钟记录 1 次：

```
rule family="ipv4" source address="192.168.0.0/24" service name="tftp" log prefix="tftp" level="info" limit value="1/m" accept
```

### 5.15.4.4. 使用富规则日志命令示例 4

来自 1:2:3:4:6:: 的用于协议 RADIUS 的新 IPv6 连接全部被拒绝，并以每分钟 3 次的速率记录日志。来自其他源的新 IPv6 连接被允许：

```
rule family="ipv6" source address="1:2:3:4:6::" service name="radius" log prefix="dns" level="info" limit value="3/m" reject
rule family="ipv6" service name="radius" accept
```

### 5.15.4.5. 使用富规则日志命令示例 5

将从 1:2:3:4:6:: 接收的、端口为 4011 且协议为 TCP 的 IPv6 数据包转发到 1:2:3:4:7 的端口 4012。

```
rule family="ipv6" source address="1:2:3:4:6::" forward-port to-addr="1::2:3:4:7" to-port="4012" protocol="tcp" port="4011"
```

