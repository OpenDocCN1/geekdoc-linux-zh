
```
system.sysDescr.0 = Linux didymus 2.4.7-10 #1 Jun 6 17:27:27 EDT 2001 i686
system.sysObjectId.0 = OID: enterprises.ucdavis.uc5mpAgent.Linux
system.sysUpTime.0 = Timeticks: (168468) 0:28:04:68
system.sysContact.0 = Steve Maxwell (sjmawell@world.net)
system.sysName.0 = didymus
system.sysLocation.0 = Graphics Lab
system.sysLastChange.0 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysOID.1 = OID: ifMIB
system.sysOrTable.sysEntry.sysOID.2 = OID: iso.org.dom.internet.snmpv2.modules.snmpMIB
system.sysOrTable.sysEntry.sysOID.3 = OID: tcpMIB
system.sysOrTable.sysEntry.sysOID.4 = OID: ip
system.sysOrTable.sysEntry.sysOID.5 = OID: udpMIB
system.sysOrTable.sysEntry.sysOID.6 = OID: iso.org.dom.internet.snmpv2.modules.snmpMIB.vacmMIB.vacmMIBformance.vacmMIBGroupsnsnsmacBasicGroup
system.sysOrTable.sysEntry.sysOID.7 = OID: iso.org.dom.internet.snmpv2.snmpd.osmapframeworkKMIB.snmpFrameworkMIBCompliances.snmpFrameworkKMIBCompliance
system.sysOrTable.sysEntry.sysOID.8 = OID: iso.org.dom.internet.snmpv2.snmpd.osmpMIB.snmpMPOIDformance.snmpMPOIDCompliances.snmpMPDCompliances
system.sysOrTable.sysEntry.sysOID.9 = OID: iso.org.dom.internet.snmpv2.snmpd.osuseMsmMIB.usemMIBConformance.usemMIBCompliances.usemMIBCompliance
system.sysOrTable.sysEntry.sysDesc.1 = The MIB for generic objects for network-like
system.sysOrTable.sysEntry.sysDesc.2 = The MIB for SNMPv2 entities
system.sysOrTable.sysEntry.sysDesc.3 = The MIB for managing TCP implementations
system.sysOrTable.sysEntry.sysDesc.4 = The MIB for managing IP and ICMP implementations
system.sysOrTable.sysEntry.sysDesc.5 = The MIB for managing UDP implementations.
system.sysOrTable.sysEntry.sysDesc.6 = View-based Access Control for SNMP.
system.sysOrTable.sysEntry.sysDesc.7 = The MIB for Management Architecture MIB.
system.sysOrTable.sysEntry.sysDesc.8 = The MIB for Message Processing and Dispatching.
system.sysOrTable.sysEntry.sysDesc.9 = The management information definitions for the SNMP User-based Security Model
system.sysOrTable.sysEntry.sysUpTime.1 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.2 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.3 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.4 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.5 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.6 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.7 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.8 = Timeticks: (0) 00:00:00
system.sysOrTable.sysEntry.sysUpTime.9 = Timeticks: (0) 00:00:00
End of MIB
```

![](img/2928fe42a92e6fb43bbbe3768008092f_523_0.png)

# 504 UNIX 系统管理：初学者指南

要遍历给定代理中的整个 MIB 并将输出保存到文件，请使用以下命令：

```bash
# snmpwalk bedrock public .1 > walk.out
```

此命令使用 `.1` 作为开始列出对象的起点。此操作可确保每个对象都会显示。`.1` 是整个 MIB 树的根，从该点可以访问所有对象。通过代理遍历整个 MIB 树可以帮助识别 MIB 对象，并让你了解特定代理支持多少对象。要查看对象的大致数量，可以统计输出文件的行数：

```bash
# wc walk.out
```

# 506 UNIX 系统管理：初学者指南

这在网络带宽节省和提高 SNMP 性能方面具有巨大的意义。SNMP 批量请求是高效的，因为它尝试在 SNMP 响应包的变量绑定字段中放置尽可能多的 OID 值。唯一的限制是底层协议的最大包大小。

要遍历名为 `c-gw1` 的设备的 MIB 树，请使用以下命令：

```bash
# snmpwalk -v 2c cisco-gw1 public
```

`snmpwalk` 命令仅适用于 SNMPv2 或 SNMPv3 代理。这是因为批量请求功能是在 SNMPv1 广泛部署之后引入的。在 SNMPv1 代理上使用此命令将产生错误。

例如，以下命令尝试从 `system` 组遍历名为 `-gw` 的设备的 MIB 树。在示例中，`monet` 只支持 SNMPv1：

```bash
# snmpwalk -v 2c monet public system
```

由于该命令不支持 SNMP 批量请求，它最终会超时，并在 `snmpwalk` 命令执行后显示以下消息：

`Timeout: No Response from monet`

超时错误条件的发生是因为请求被发送到了设备，但设备中的代理并不理解 SNMP 批量请求格式。结果是代理没有对数据包做出响应，命令直接超时。在实践中，许多网络设备已经升级并支持批量请求操作。因此，随着旧设备的更换或升级，这一问题将会减少。

注意，`snmpwalk` 要求使用 `2c` 或 `2p` 安全选项。如果你在调用 `snmpwalk` 时未指定使用哪种 SNMP 协议版本，将显示以下错误：

```
snmpwalkwalk: Cannot send V1 PDU on V2 session
```

## 模块 16: SNMP 系统管理工具

默认情况下，如果命令行中没有指定 MIB 对象或组，`snmpbulkwalk` 命令将搜索整个 MIB-II 树。从实际角度来看，如果需要完整的 MIB-II 对象存储，这使得该工具用起来更加方便。

## 掌握情况检查

- 1. 在下面的命令示例中，`-M /var/mibs` 选项的用途是什么？

```
# snmpwalk -M /var/mibs cisco-gw1 public system
```

- A. 指定要加载的 MIB 模块列表。
- B. 提供一个目录列表，供命令在其中搜索 MIB 文件。
