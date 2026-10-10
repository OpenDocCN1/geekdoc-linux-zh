
## 表 25-2. 参数类型

在浏览需要特定参数的操作之前，让我们先定义表 25-2 中的参数类型。

| 参数类型 | 含义 |
| :--- | :--- |
| **Chain** | 调用 *ipchains* 将要操作的链的名称。三个默认链分别为 input（输入）、forward（转发）和 output（输出）。 |
| **Rulespec** | 规则规范。规则规范的格式将在本节稍后解释。 |
| **Rulenum** | 您要操作的规则的编号。（假设规则编号已存在。） |
| **Target** | 内核在找到与链中列出的某条规则匹配的包时应采取的操作：有效目标为 ACCEPT、REJECT 和 DENY。ACCEPT 表示允许该数据包通过其当前正在处理的任何链。DENY 表示丢弃数据包，系统简单地假装从未收到它。REJECT 是 DENY 的友好版本：它拒绝接受数据包，但会向发送者发送一条 ICMP 消息以表明这一点。 |
| **Options** | 可应用于每条规则的附加修饰符。当然，这些并非必需。选项将在本节稍后讨论。 |

既然您理解这些定义，我们就可以查看每个操作所需的参数：

- **要添加规则，请使用**
  `[root@ford/root]# ipchains -A chain rulespec options`
- **要删除规则，请使用**
  `[root@ford/root]# ipchains -D chain rulespec options`
  或者您可以使用格式
  `[root@ford/root]# ipchains -D chain rulenum options`
- **要替换规则，请使用**
  `[root@ford/root]# ipchains -R chain rulenum rulespec options`
- **要插入规则，请使用**
  `[root@ford/root]# ipchains -I chain rulenum rulespec options`
- **要列出规则，请使用**
  `[root@ford/root]# ipchains -L chain options`
- **要清空选定的链，请使用**
  `[root@ford/root]# ipchains -F chain options`
- **要将链的一组计数器清零，请使用**
  `[root@ford/root]# ipchains -Z chain options`
- **要创建新链，请使用**
  `[root@ford/root]# ipchains -N chain options`
- **要删除链，请使用**
  `[root@ford/root]# ipchains -X chain options`
- **要为给定链设置策略，请使用**
  `[root@ford/root]# ipchains -P chain target options`

## 规则规范

规则规范（*或简写为 rulespec*）由一系列独立的命令行参数组成。这些参数如下：

- **-P protocol**: 指定该规则应适用的 IP 数据包类型。
  有效的协议是那些列在 `/etc/protocols` 文件中的协议，或者是未列在那里任何协议的数字值。典型值为 tcp、udp、icmp 或 all，其中 all 指所有有效协议。如果您在协议前加上感叹号 (!)，则反转测试。例如，说 “-P !icmp” 实际上意味着 “对于所有不是 icmp 的协议”。

- **-s source [mask port]**: 陈述为了让该规则匹配，源 IP 地址必须是什么。典型用途是拒绝已知的敌对或不可信网络。在此选项中，source 是 IP 地址，mask 是可以用点分十进制表示法（例如 255.255.255.0）或指定子网掩码中的位数（例如，25 等同于子网掩码 255.255.255.128）表示的子网掩码。端口值允许您指定想要操作源端口号。您可以使用 port1:port2 格式使用值范围，其中 port1 是下限，port2 是上限。端口号是可选的。例如，要指定来自 192.168.42.0 网络中任何主机的 1024 到 65535 范围内的任意端口，我们会说 “-s 192.168.42.0/24 1024:65535”。在 IP/子网掩码组合或端口号前加上感叹号 (!) 会否定表达式。例如，要指定除 192.168.42.7 以外的任何主机，我们会说 “-s !192.168.42.7”。

- **-source-port port**: 指定一个端口（如果 port 格式为 port1:port2，则为端口范围），其中 port 是最低端口号，port2 是最高端口号，无需指定 IP 地址。例如，如果您想为源端口为 0 到 1023 的所有主机设置规则，您会使用 “-source-port 0:1023”。

- **-d destination [mask port]**: 与 -s 选项相同，但这适用于目的而不是源 IP 地址。

- **-destination-port port**: 与 -source-port 选项相同，只不过此选项适用于目的端口而不是源端口。

- **-icmp-type typename**: 对类型为 typename 的 ICMP 数据包应用规则。您可以运行 “ipchains -h icmp” 来查看类型列表。最常见的类型是 echo-reply，用于 ping 程序。在 typename 前加上感叹号 (!) 会反转类型。例如，要为除 port-unreachable 消息外的所有 ICMP 数据包设置规则，我们会说 “-icmp-type ! port-unreachable”。

- **-j target**: 指定如果规则匹配时执行的操作应为 target，其中 target 是用户定义的链或预定义目标之一（ACCEPT、DENY、REJECT）。

- **-i interface**: 指定该规则应适用的接口，其中 interface 是设备名称（例如 eth0）。如果规则未指定此选项，则假设规则适用于所有接口。如果 interface 前缀有感叹号 (!)，则反转规则。例如，要将规则应用于除 ppp1 以外的所有接口，我们会说 “-i !ppp1”。

- **-f**: 将此规则应用于任何数据片段。由于 IP 片段头部信息未包含在每个片段中，因此无法将其应用于任何现有规则。您可以通过配置内核在交付所有数据包之前进行分片重组来完全避免这种混乱。如果您确实允许来自某些接口的片段，请将此选项与 -i 选项结合使用。通过在 -i 前缀加上感叹号 (!)，您可以反转其含义。例如，为了表示我们要拒绝除来自 eth0 外的所有片段，我们会使用 “-f -i !eth0”。

OPTIONS: 可以为规则指定附加选项，如表 25-3 所示。

### 表 25-3. 可以为规则指定的附加选项

| 选项 | 描述 |
| :--- | :--- |
| -b | 双向应用规则。这实际上等同于设置一条额外的规则，其中源和目的信息被反转。 |
| -v | 详细输出。 |
| -n | 给出数字输出。通常，使用详细选项列出所有规则或更改规则会导致所有 IP 地址解析其名称，使输出更具可读性。如果您正在调试问题且主机名解析不可用，应使用此选项，以免系统因等待 DNS 请求超时而停滞。 |
| -1 | 为所有匹配规则的数据包开启内核日志记录。 |
| -x | 在使用 -1 操作打印规则信息时显示精确数字。通常，输出会四舍五入到最接近的 1,000 或 1,000,000。 |
| -y | 仅匹配设置了 SYN 标志但未设置 ACK 或 FIN 位的数据包。TCP 头中的 SYN 位用于发起连接。通常此选项用于阻止传入连接但允许传出连接。您可以在此选项前加上感叹号 (!) 来反转它，从而匹配所有未设置 SYN 位且设置了 ACK 或 FIN 位的数据包。 |

## 使用 IPCHAINS 的示例

正如我们目前所见，ipchains 可能有点让人头疼难以理解。不过通常，只要几个实际操作的例子就能更好地理解所有操作及其相应选项之间的关系。所以让我们通过一些例子来了解。

示例：我们想要设置一条规则，使得来自 192.168.1.8 的连接被丢弃，但我们允许向它们打开连接。

```bash
[root@ford /root]# ipchains -A input -p tcp -s 192.168.1.8 -j DENY -y
```

示例：我们想要阻止任何人对我们的 8080 端口的所有连接，并记录所有尝试：

```bash
[root@ford /root]# ipchains -A input -p tcp -destination-port 8080 -j DENY -1
```

示例：我们想要阻止所有来自 ntp.ucsd.edu 的数据包，除了来自 123 端口的数据包。这通过两个过滤器完成：第一个允许来自 ntp.ucsd.edu 123 端口数据包；第二个拒绝来自 ntp.ucsd.edu 的其他所有内容。这之所以有效是因为规则按顺序检查——如果数据包来自 ntp.ucsd.edu 的 123 端口，它将匹配第一条规则并立即接受数据包。第二条规则将被检查。另一方面，如果数据包来自 ntp.ucsd.edu 的 124 端口，第一条规则将不适用，但第二条规则适用，因此数据包将被拒绝。

```bash
[root@ford /root]# ipchains -A input -p tcp -s ntp.ucsd.edu 123 -j ACCEPT
[root@ford /root]# ipchains -A input -p tcp -s ntp.ucsd.edu -j DENY
```

## 烹饪书解决方案

人们在使用数据包过滤时有很多常见的需求。在本节中，我们提出了四种烹饪书解决方案，针对两种常见场景：

- 过滤掉 Ping of Death（死亡之 ping）
- 过滤掉外部人员不需要的外部服务

### 过滤掉 Ping of Death

Ping of Death 已经存在相当一段时间了。虽然大多数操作系统已发布修复此问题的补丁，但您的网络上可能仍有一些未受保护的旧系统。如果您的 Linux 系统正作为它们的路由器，您希望使用数据包过滤提供保护。

但在我们为 Ping of Death 构建过滤器之前，我们必须首先了解它是什么。要理解这一点，我们必须先了解什么是 ping。

正如我们在本章早些时候看到的，IP 数据包封装了许多其他协议，例如 TCP 和 UDP。另一种常见的 IP 数据包类型是 ICMP，即 Internet

