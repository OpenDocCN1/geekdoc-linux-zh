
现在你再也不需要在每个命令中都输入 `-v2c` 了。

> ³ 如果你收到了 `Timeout: No Response from localhost` 消息，可能是某些内容阻止了指向 161 端口的 UDP 请求。检查你的防火墙设置和 `/etc/hosts.deny`。如果你在 `hosts.deny` 中发现 `ALL`，请将其注释掉并尝试 SNMP 代理。

> ⁴ SNMP 之称为“基于社区的”，因为它使用了 SNMPv1 团体字符串（将它们想象成密码）。为 SNMPv2 设计的新安全框架还没有完善，因此 SNMPv2c 在发布时没有包含它。当该框架就绪后，新的安全框架在 SNMPv3 中发布了。

> ⁵ 注意到 MIB 对象是 `syslocation`，但 `snmp.conf` 文件中的命令是 `syslocation`。这并没有特殊意义；这只是实现者的设计选择，在配置文件的键中使用全小写字母。

如果你可以访问任何其他网络设备，可以尝试查询它们。例如，这里是对 ApplePort Base Station 运行的 `snmpwalk` 命令：

```
$ snmpwalk -c public 10.0.0.1:1

snmpv2-MIB::sysDesc.0 = STRING: Base Station V3.84 Compatible

snmpv2-MIB::sysObjectID = OID: Snmpv2-SM::dotZero

DISMAN-EVENT-MIB::sysTimeInstance = Timeticks:(49711868): 14:31:88

snmpv2-MIB::sysContact.0 = STRING: me@myaddr.com

snmpv2-MIB::sysName.0 = STRING: MyAirport

snmpv2-MIB::sysServices.0 = INTEGER: 79

snmpv2-MIB::sysServices.0 = No more variables left in the MIB View (It is the end of the MIB tree)
```

显然，`sysDesc.0`（系统描述）识别出这是一个 Apple Base Station。你也会识别该设备的 syslocation 和 sysContact 信息。该设备提供的信息不多，但足以识别它是什么、在哪里，以及当设备出现故障时应该联系谁。当然，系统位置和联系方式的可用性取决于该系统的管理员，由他在目标设备上配置这些值。注意，对于这次查询我们使用了 `snmpwalk` 而不是 `snmpget`，因为我们想看看此设备还提供了哪些信息。`snmpget` 使用一个 SNMP GET 单元（unit）检索一个实例，而 `snmpwalk` 使用多个 GETU 来“漫游”整个 MIB。你选择一个起点，`snmpwalk` 询问下一个对象；代理返回该对象及其 OID，`snmpwalk` 在新 OID 之后询问下一个实例。最终，代理响应无无可返回，漫游结束。

OID 的可读名称（如 `sysDesc` 和 `sysLocation`）的显示取决于客户端上是否有正确的 MIB 文件。在 Net-SNMP 的情况下，注册简单意味着将这些文件放在正确的目录中并设置 SNMP 命令（如 `snmpget` 和 `snmpwalk`）使用它们。你可以设置几个环境变量来完成这项工作（例如 `.bashrc`）：

```
export MIB-ALL

export MIBDIRS=/usr/share/snmp/mibs
```

当你安装 Net-SNMP 时，它会将一组标准 MIB 文件放置在 `/usr/share/snmp/mibs`，如下所示。这些都是人类可读且机器解析的纯文本文件。其中一些描述了 MIB，其他定义了 MIB 需要的信息。

如果没有任何 MIB 文件，Apple Base 组的显示将如下：

```
$ snmpwalk -On -v2c -c public 10.0.1 system

1.3.6.2.1.1.1 = STRING: Base Station V3.84 Compatible

1.3.6.2.1.1.2.1.0 = OID: .0

1.3.6.2.1.1.2.1.3.0 = Timets:(629726):44:57:26

1.3.6.2.1.1.2.1.4.0 = STRING: me@myaddr.com

1.3.6.2.1.1.2.1.5.0 = STRING: MyApp

1.3.6.2.1.1.2.1.6.0 = STRING: my

1.3.6.2.1.1.2.1.7.0 = INTEGER: 79

1.3.6.2.1.1.2.1.7.0 = No more variables in this MIB (It is the end of the MIB tree)
```

你可以检查响应了解一些设备信息，但知道 OID 的含义会更好。

# 网络打印机

让我们尝试另一个类型的设备：

```
$snmpwalk -c public 10.0.0.1

STRING: HP ETHERNET MULTI-ENVIRONMENT, ROM

SNMPv2-MIB:sysDesc.0 = STRING: L.20.07,DIRECT,JD84,EEPROM L.20.07

SNMPv2-MIB:sysObjectID = OID: Snmpv2-SM::dotZero

SNMPv2-MIB:sysUptime.0 = Timeticks:(3548750) 41 days, 04:07:50

SNMPv2-MIB:sysContact.0 = STRING: me@myaddr.com

SNMPv2-MIB:sysName.0 = STRING: Airport

SNMPv2-MIB:sysServices.0 = INTEGER: 79
```

这次，管理员没有设置 sysContact 和 sysLocation。不过，更难读的是 `sysDesc.0`，它显示为：`HP ETHERNET MULTI-ENVIRONMENT, ROM`。

# 用于可读名称的 MIB 文件

以下是 `/usr/share/snmp/mibs` 中的文件：

- `AGENTS-MIB.txt`
- `AGENT-EXAMPLES-MIB.txt`
- `AGENT-MP-BASE-MIB.txt`
- `DISMAN-EVENT-MIB.txt`
- `DISMAN-SCHEDULE-MIB.txt`
- `DISMAN-SCRIPT-MIB.txt`
- `EtherLike-MIB.txt`
- `HCNUM-TC.txt`
- `HOST-RESOURCES-MIB.txt`
- `HOST-RESOURCES-TYPES-MIB.txt`
- `RFC1155-S.txt`
- `RFC1213-MIB.txt`
- `RFC1215.txt`
- `RMON-MIB.txt`
- `SMUX-MIB.txt`
- `SNMP-COMMUNITY-MIB.txt`
- `SNMP-FRAMEWORK-MIB.txt`
- `SNMP-NOTIFICATION-MIB.txt`
- `SNMP-MPD-MIB.txt`
- `SNMP-PROXY-MIB.txt`
- `SNMP-TARGET-MIB.txt`
- `SNMP-USER-MIB.txt`
- `SNMP-VIEW-BASED-MIB.txt`
- `SNMPv2-CONF.txt`
- `SNMPv2-MIB.txt`
- `SNMPv2-SMI.txt`
- `SNMPv2-TC.txt`
- `TCP-MIB.txt`
- `IPV6-ICMP-MIB.txt`
- `IPV6-MIB.txt`
- `IPV6-TCP-MIB.txt`
- `IPV6-TC.txt`
- `UCD-DEMO-MIB.txt`
- `UCD-DISKO-MIB.txt`
- `UCD-DLMOD-MIB.txt`
- `UCD-IPWACC-MIB.txt`
- `UCD-SNMP-MIB.txt`
- `UDP-MIB.txt`

# snmable 命令

这台打印机的 SNMP 代理提供了比系统组多多的信息，让我们有机会机会演示另一个命令 `snmable`。该命令的行为类似于 `snmpwalk`，但输出格式不同。我们用它查看同一台直接打印机的 TCP 连接。

```
$ snmpwalk -v1 -c public 10.0.0.183 tcpConnTable

SNMP-table:tcpConnTable
```
