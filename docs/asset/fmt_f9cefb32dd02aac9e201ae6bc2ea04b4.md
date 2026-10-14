
```
$ snmpwalk -v 2c -c public test.net-snmp.org
SNMPv2-MIB::sysDescriptor.0 = STRING: test.net-snmp.org
SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB.1
DISMAN-EVENT-MIB::sysUpTimeInstance = (5337593) 14:49:35.9
SNMPv2-MIB::sysContact.0 = STRING: Net-SNMP
SNMPv2-MIB::sysName.0 = STRING: test.net-snmp.org
SNMPv2-MIB::syslocation.0 = STRING: Undis
SNMPv2-MIB::sysLastChange.0 = Timeticks: (5) 00:00:00.5
SNMPv2-MIB::sysObjectID.1 = OID: SNMPv2-MIB:snmpMIB
SNMPv2-MIB::sysObjectID.2 = OID: VIEW-BASED-ACM-MIB:BasicGroup
SNMPv2-MIB::sysObjectID.3 = OID: SNMP-MPD-MIB:snmpObjects.3.1
SNMPv2-MIB::sysObjectID.4 = OID: USER-BASED-SM-MIB:snmpFramework
SNMPv2-MIB::sysObjectID.5 = OID: SNMP-FRAMEWORK-MIB:snmpFrameworkCompliance
SNMPv2-MIB::sysDescr.2 = STRING: View-based Access Control Model for SNMP.
SNMPv2-MIB::sysDescr.3 = STRING: The MIB for Message Processing.
SNMPv2-MIB::sysDescr.4 = STRING: The MIB for Message Processing.
SNMPv2-MIB::sysDescr.5 = STRING: The Management Architecture MIB.
SNMPv2-MIB::sysUpTime.1 = Timeticks: (4) 00:00:00.4
SNMPv2-MIB::sysUpTime.2 = Timeticks: (4) 00:00:00.4
SNMPv2-MIB::sysUpTime
```

你可以看到，命令返回了带有名称的值。让我们看看如何配置 SNMP 服务器。运行 `snmpconf` 程序。程序将询问它需要读取的配置文件以及要生成的文件。选择 `snmpd.conf`（通常是项 1）。

之后，进入章节菜单：

- 1: 扩展代理 `Extending the Agent`
- 2: 监控运行主机各个方面 `Monitor Various Aspects of the Running Host`
- 3: 陷阱目的地 `Trap Destinations`
- 4: 代理运行模式 `Agent Operating Mode`
- 5: 系统信息 `System Information`
- 6: 访问控制设置 `Access Control Setup`

我们对第 4、5、6 节感兴趣。在第 4 节中，你可以指定运行代理的地址（接口），以及代表它运行的用户组。第 5 节是关于服务器的数据，位于系统树。第 6 节允许你指定用户名（针对 SNMP v3）以及用于读取或写入社区名称（默认针对所有值）：

- 1: SNMPv3 写入用户
- 2: SNMPv3 只读用户
- 3: SNMPv1/SNMP2 只读访问社区名称
- 4: SNMPv1/SNMP2 写入社区名称

例如，让我们为名为 `public` 的社区设置 `192.168.0.0` 网络的读取权限（用户输入以粗体显示）：

选择节： 3

正在配置: `rocommunity`

描述:

- an SNMPv1/SNMPv2 read-only access community name

`arguments: community [defaulthostnamenetwork/bits] [oid]`

要添加只读访问的社区名称 `public`

接受此社区的主机名或网络地址 [回车表示全部]: `192.168.0.0`

该社区应限制的 OID [回车表示无限制]:

完成输出: `rocommunity public 192.168.0.0`

配置完成后，程序将配置文件写入当前目录，可以将其复制到 `/etc/snmp/`。

## 第19 章 集群状态监控系统

`snmpconf` 程序并不总是能生成正确的配置文件；务必保存原始文件（`cp /etc/snmp/snmpd.conf .bak`），如果发生错误，将新文件与备份文件进行对比。

现在，我们可以通过网络对服务器进行监控了。遗憾的是，并不是所有参数都很有趣，而且保护并非最好，但大多数标准的监控软件包都能检测到它并能够从其接收数据。如果需要，可以扩展监控功能。

让我们考虑另一个对我们非常重要的服务 - `snmptrapd`。该程序接收由其他 SNMP 设备（服务器、路由器、空调、UPS 等）发送的通知（陷阱）。

要让它工作，你需要配置设备，将必要的通知发送到运行 `snmptrapd` 的服务器地址！

现在我们来编辑 `snmptrapd` 配置文件 - `/etc/snmp/snmptrapd.conf`。对于最小配置，只需添加以下行即可：

`authCommunity log,execute,net public`

重启 `snmptrapd` 服务器并运行命令：

```
snmptrap -v 2c -c localhost "" \
NET-SNMP-EXAMPLES-MIB:netSnmpExampleHeartbeatNotification \
SnmpExampleHeartbeatRate i 123456
```

此命令将向本地发送一个通知。如果 `snmptrapd` 正在运行，日志中将出现条目（通常在 `/var/log/syslog` 或 `/var/log/messages`）：

```
UDP: [127.0.0.1]:48680-[127.0.0.1]:#012iso.3.6.1.2.1.1.1.3.0 = =
timicks: (189767908) \
21 days, 23:07:59.08#011iso.3.6.1.6.3.1.1.1.4.1.0 =
OID: iso.3.6.1.4.1.8072.2.3.0.1#011iso.3.6.1.4.1.8072.2.3.2.1 =
INTEGER: 123456
```

这意味着消息已被接受。如果什么都没有发生，但 `snmptrapd` 正在运行，那么它可能使用了 `tcpwrappers`。此时请在 `/etc/hosts.allow` 文件中写一行：

`snmptrapd: 0.0.0.0.`

你可以配置 `snmptrapd` 仅接受来自特定地址和社区（communities）的消息；帮助文档对此有很好的说明。

通常情况下，通过通知发送的消息是关键或非常重要的，因此记录这些信息是有用的，但还不够。我们希望在此类事件发生时采取某些操作。`snmptrapd` 正可以帮我们这一点。再次打开 `/etc/snmp/snmptrapd.conf` 文件并添加以下行：

```
trapand NET-SNMP-EXAMPLES-MIB::netSnmpExampleHeartbeatNotification \
/tmp/demo demo-trap
```

让我们创建一个 `/tmp/demo` 脚本，内容如下：

```bash
#!/bin/sh
read host
read ip
vars=
while read oid val
do
  if [ "x$vars" = "x" ]
  then
    vars="$oid $val"
  else
    vars="$vars,\n$oid = $val"
  fi
done
echo -e "trap: $1 $host $ip $vars" > /tmp/demo.log
```

使用 `chmod a+x /tmp/demo` 允许其执行。现在重启 `snmptrapd` 并再次运行 `snmtrap` 命令发送测试通知。`/tmp/demo.log` 文件中应该出现类似的一行：

`trap: demo-trap localhost UDP: [127.0.0.1]:51240->[127.0.0.1],

SNMPv2-SMI::mib-2.1.3.0 = 21:23:11.65,

SNMPv2-SMI::snmpModules.1.1.4.1.0 = NET-SNMP-EXAMPLES-MIB::netSnmpExampleHeartbeatNotification,

NET-SNMP-EXAMPLES-MIB::netSnmpExampleHeartbeatRate = 123456`
