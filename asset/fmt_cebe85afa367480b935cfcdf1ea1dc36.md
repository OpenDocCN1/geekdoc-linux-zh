
使用 `firewall-cmd` 工具的 `--direct` 选项可以在运行时添加和删除链。这里列出了一些示例。更多信息请参见 `firewall-cmd(1)` 手册页。

如果您不太熟悉 `iptables`，使用直接接口是危险的，因为这可能会无意中导致防火墙出现漏洞。

直接接口模式旨在让服务或应用程序在运行时添加特定的防火墙规则。可以使用 `firewall-cmd --permanent --direct` 命令添加 `--permanent` 选项或修改 `/etc/firewalld/direct.xml` 来使规则永久化。有关 `/etc/firewalld/direct.xml` 文件的信息，请参见手册 `firewalld.direct(5)`。

### 5.14.1. 使用直接接口添加规则

若要向 `IN_public_allow` 链添加规则，请以 `root` 身份输入以下命令：

```bash
~]# firewall-cmd --direct --add-rule ipv4 filter IN_public_allow \
     0 -m tcp -p tcp --dport 666 -j ACCEPT
```

添加 `--permanent` 选项以使设置持久化。

### 5.14.2. 使用直接接口删除规则

若要移除 `IN_public_allow` 链中的规则，请以 `root` 身份输入以下命令：

```bash
~]# firewall-cmd --direct --remove-rule ipv4 filter IN_public_allow \
    0 -m tcp -p tcp --dport 666 -j ACCEPT
```

添加 `--permanent` 选项以使设置持久化。

### 5.14.3. 使用直接接口列出规则

若要列出 `IN_public_allow` 链中的规则，请以 `root` 身份输入以下命令：

```bash
~]# firewall-cmd --direct --get-rules ipv4 filter IN_public_allow
```

请注意，此命令 ` --get-rules ` 选项仅列出之前使用 `--add-rule` 选项添加的规则。它不列出通过其他方式添加的现有 `iptables` 规则。

## 5.15. 使用“丰富语言”语法配置复杂防火墙规则

使用“丰富语言”语法，可以创建比直接接口方法更容易理解的复杂防火墙规则。此外，配置可以永久化。该语言使用带有值的关键词，是 `iptables` 规则的抽象表示。可以使用此语言配置区域；当前的配置方法仍将得到支持。

### 5.15.1. 丰富语言命令的格式

本节中的所有命令都需要以 `root` 身份运行。添加规则命令的格式如下：

```bash
firewall-cmd [--zone=zone] --add-rich-rule='rule' [--timeout=timeval]
```

这将针对区域 `zone` 添加丰富语言规则 `rule`。此选项可以指定多次。如果省略区域，则使用默认区域。如果提供了超时时间，则该规则或这些规则仅在指定的时间段内保持活动状态，之后将自动移除。时间值后可以跟随 `s`（秒）、`m`（分钟）或 `h`（小时）以指定时间单位。默认是秒。

要删除规则：

```bash
firewall-cmd [--zone=zone] --remove-rich-rule='rule'
```

这将移除针对区域 `zone` 的丰富语言规则 `rule`。此选项可以指定多次。如果省略区域，则使用默认区域。

要检查规则是否存在：

```bash
firewall-cmd [--zone=zone] --query-rich-rule='rule'
```

这将返回针对区域 `zone` 是否已添加丰富语言规则 `rule`。如果启用，命令打印 `yes` 且退出状态为 `0`。否则打印 `no` 且退出状态为 `1`。如果省略区域，则使用默认区域。

有关在区域配置文件中使用的丰富语言表示的信息，请参见 `firewalld.zone(5)` 手册页。

### 5.15.2. 理解富规则结构

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

文件中的富规则结构使用 `NOT` 关键字来反转源地址和目的地址命令的含义，但命令行使用 `invert="true"` 选项。

规则与特定的区域相关联。一个区域可以包含多个规则。如果某些规则相互作用或相互矛盾，则第一个匹配该数据包的规则将生效。

### 5.15.3. 理解富规则命令选项

#### family

如果提供了规则族 `ipv4` 或 `ipv6`，则该规则分别限制为 `IPv4` 或 `IPv6`。如果未提供规则族，则该规则将同时添加到 `IPv4` 和 `IPv6` 中。如果在规则中使用了源地址或目的地址，则必须提供规则族。端口转发也是如此。

#### 源地址和目的地址

##### source

通过指定源地址，可以将连接尝试的发起方限制为源地址。源地址或地址范围是带有 `IPv4` 或 `IPv6` 掩码的 IP 地址或网络 IP 地址。对于 `IPv4`，掩码可以是网络掩码或普通数字。对于 `IPv6`，掩码是普通数字。不支持使用主机名。可以通过添加 `NOT` 关键字来反转源地址命令的含义；除提供的地址外，所有地址都匹配。

如果未指定规则的 `family`，可以为 `IPv4` 和 `IPv6` 添加 MAC 地址以及类型为 `hash:mac` 的 IP 集合。其他 IP 集合需要与规则的 `family` 设置匹配。

##### destination

通过指定目的地址，可以将目标限制为目的地址。目的地址使用与源地址相同的 IP 地址或地址范围语法。使用源地址和目的地址是可选的，并且并非所有元素都允许使用目的地址。这取决于目的地址的使用情况，例如在服务条目中。您可以将 `destination` 和 `action` 组合使用。

#### 元素

元素只能是以下元素类型中的一种：`service`、`port`、`protocol`、`masquerade`、`icmp-block`、`forward-port` 和 `source-port`。

##### service

`service` 元素是 `firewalld` 提供的服务之一。要获取预定义服务列表，请输入以下命令：

```bash
~]$ firewall-cmd --get-services
```

如果服务提供目的地址，它将与规则中的目的地址冲突并导致错误。内部使用目的地址的服务主要是使用组播的服务。该命令的形式如下：

```
service name=service_name
```

##### port

`port` 元素可以是单个端口号或端口范围，例如 `5060-5062`，后跟协议，协议可以是 `tcp` 或 `udp`。该命令的形式如下：

```
port port=number_or_range protocol=protocol
```

##### protocol

`protocol` 值可以是协议 ID 号或协议名称。有关允许的 `protocol` 条目，请参阅 `/etc/protocols`。该命令的形式如下：

```
protocol value=protocol_name_or_ID
```

##### icmp-block

使用此命令阻止一个或多个 `ICMP` 类型。`ICMP` 类型是 `firewalld` 支持的 `ICMP` 类型之一。要获取支持的 `ICMP` 类型列表，请输入以下命令：

```bash
~]$ firewall-cmd --get-icmptypes
```

此处不允许指定操作。`icmp-block` 内部使用操作 `reject`。该命令的形式如下：

```
icmp-block name=icmp_type_name
```

##### masquerade

在规则中启用 IP 伪装 `Masquerading`。可以提供源地址以将伪装限制在此区域，但不能提供目的地址。此处不允许指定操作。

##### forward-port
