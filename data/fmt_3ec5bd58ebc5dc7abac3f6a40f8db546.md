
本节中的选项仅影响某个特定区域。如果与 `--zone=zone` 选项一起使用，它们将影响区域 `zone`。如果省略该选项，它们将影响默认区域（参见 `--get-default-zone`）。

### `[--zone=zone] --list-all`

列出为区域添加或启用的所有内容。如果省略区域，将使用默认区域。

### `[--zone=zone] --list-services`

以空格分隔的列表形式列出为区域添加的服务。如果省略区域，将使用默认区域。

### `[--zone=zone] --add-service=service`

为区域添加服务。如果省略区域，将使用默认区域。此选项可以多次指定。

该服务是防火墙提供的服务之一。要获取受支持服务的列表，请使用 `firewall-cmd --get-services`。

### `[--zone=zone] --remove-service-from-zone=service`

从 `zone` 中移除服务。此选项可以多次指定。如果省略 `zone`，将使用默认区域。

### `[--zone=zone] --query-service=service`

返回 `service` 是否已为 `zone` 添加。如果省略 `zone`，将使用默认区域。如果为真，返回 0；否则返回 1。

### `[--zone=zone] --list-ports`

以空格分隔的列表形式列出为 `zone` 添加的端口。端口的形式为 `portid[-portid]/protocol`，它可以是一个端口和协议的组合，或者是一个带协议的端口范围。如果省略 `zone`，将使用默认区域。

### `[--zone=zone] --add-port=portid[-portid]/protocol`

为 `zone` 添加端口。如果省略 `zone`，将使用默认区域。此选项可以多次指定。

端口可以是单个端口号或端口范围 `portid-portid`。协议可以是 `tcp` 或 `udp`。

### `[--zone=zone] --remove-port=portid[-portid]/protocol`

从 `zone` 中移除端口。如果省略 `zone`，将使用默认区域。此选项可以多次指定。

### `[--zone=zone] --query-port=portid[-portid]/protocol`

返回该端口是否已为 `zone` 添加。如果省略 `zone`，将使用默认区域。如果为真，返回 0；否则返回 1。

### `[--zone=zone] --list-icmp-blocks`

以空格分隔的列表形式列出为 `zone` 添加的互联网控制消息协议（ICMP）类型阻止规则。如果省略 `zone`，将使用默认区域。

### `[--zone=zone] --add-icmp-block=icmptype`

为 `zone` 添加针对 `icmptype` 的 ICMP 阻止规则。如果省略 `zone`，将使用默认区域。此选项可以多次指定。

`icmptype` 是 firewalld 支持的某种 ICMP 类型。要获取受支持的 ICMP 类型列表：`firewall-cmd --get-icmp-types`

### `[--zone=zone] --remove-icmp-block=icmptype`

从 `zone` 中移除针对 `icmptype` 的 ICMP 阻止规则。如果省略 `zone`，将使用默认 `zone`。此选项可以多次指定。

### `[--zone=zone] --query-icmp-block=icmptype`

返回针对 `icmptype` 的 ICMP 阻止规则是否已为 `zone` 添加。如果省略 `zone`，将使用默认 `zone`。如果为真，返回 0；否则返回 1。

### `[--zone=zone] --list-forward-ports`

以空格分隔的列表形式列出为 `zone` 添加的 `IPv4` 转发端口。如果省略 `zone`，将使用默认 `zone`。

对于 `IPv6` 转发端口，请使用富语言（rich language）。

### `[--zone=zone] --add-forward-port=port=portid[-portid]:proto=proto[,toport=portid[-portid]][:toaddr=address[/mask]]`

为 `zone` 添加 `IPv4` 转发端口。如果省略 `zone`，将使用默认 `zone`。此选项可以多次指定。

端口可以是单个端口号 `portid` 或端口范围 `portid-portid`。协议可以是 `tcp` 或 `udp`。目标地址是一个简单的 IP 地址。

对于 `IPv6` 转发端口，请使用富语言（rich language）。

### `[--zone=zone] --remove-forward-port=port=portid[-portid]:proto=proto[,toport=portid[-portid]][:toaddr=address[/mask]]`

从 `zone` 中移除 `IPv4` 转发端口。如果省略 `zone`，将使用默认 `zone`。此选项可以多次指定。

对于 `IPv6` 转发端口，请使用富语言（rich language）。

### `[--zone=zone] --query-forward-port=port=portid[-portid]:proto=proto[,toport=portid[-portid]][:toaddr=address[/mask]]`

返回该 `IPv4` 转发端口是否已为 `zone` 添加。如果省略 `zone`，将使用默认 `zone`。如果为真，返回 0；否则返回 1。

对于 `IPv6` 转发端口，请使用富语言（rich language）。

### `[--zone=zone] --add-masquerade`

为 `zone` 启用 `IPv4` 伪装（masquerade）。如果省略 `zone`，将使用默认 `zone`。如果机器是路由器，并且通过其他 `zone` 中的接口连接的设备应能使用第一个连接，则伪装非常有用。

#### 选项

### `[--zone=zone] --remove-masquerade`

为 `zone` 禁用 `IPv4` 网络地址伪装。如果省略 `zone`，将使用默认区域。

对于 `IPv6` 网络地址伪装，请使用富语言。

### `[--zone=zone] --query-masquerade`

返回是否已为 `zone` 启用 `IPv4` 网络地址伪装。如果省略 `zone`，将使用默认区域。如果为真则返回 0，否则返回 1。

对于 `IPv6` 网络地址伪装，请使用富语言。

### `[--zone=zone] --list-rich-rules`

以换行符分隔的列表形式列出已添加到 `zone` 的富语言规则。如果省略 `zone`，将使用默认区域。

### `[--zone=zone] --add-rich-rule=rule`

为 `zone` 添加富语言规则 `rule`。此选项可以指定多次。如果省略 `zone`，将使用默认区域。

关于富语言规则的语法，请参阅 `firewalld.richlanguage(5)`。

### `[--zone=zone] --remove-rich-rule=rule`

从 `zone` 中移除富语言规则 `rule`。此选项可以指定多次。如果省略 `zone`，将使用默认区域。

关于富语言规则的语法，请参阅 `firewalld.richlanguage(5)`。

### `[--zone=zone] --query-rich-rule=rule`

返回是否已为 `zone` 添加了富语言规则 `rule`。如果省略 `zone`，将使用默认区域。如果为真则返回 0，否则返回 1。

关于富语言规则的语法，请参阅 `firewalld.richlanguage(5)`。

## 处理接口绑定的选项

将接口绑定到区域意味着使用该区域的设置来限制通过该接口的流量。

本节的选项仅影响特定的一个区域。如果与 `--zone=zone` 选项一起使用，它们将影响 `zone` 区域。如果省略该选项，它们将影响默认区域（参见 `--get-default-zone`）。

要获取预定义区域的列表，请使用 `firewall-cmd --get-zones`。

接口名称是长度不超过 16 个字符的字符串，且不得包含 `,` `/` `!` 和 `*`。

### `[--zone=zone] --list-interfaces`
