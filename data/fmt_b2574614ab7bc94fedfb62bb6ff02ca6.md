
```
C:\WINNT\System32\cmd.exe
>nslookup /zoneinfo sample.tld
Zone query result:
ptr = 00075420
name = sample.tld
zone type = 1
dns = 0
Be interpreted = 0
data time = sample.tld.dns
Using WMI = 0
aging = 0
refresh interval = 168
no refresh = 0
scavenging available = 352259
NULL IP Array = 0
Zone Secondaries = 0
NULL IP Array = 0
secure sq = 0
Command completed successfully.
C:\>
```

图 A-8：查看区域信息。

`/Info` 命令和 `/ZoneInfo` 命令用于快速查看特定区域的配置。输出可以由脚本解析，正如我们提到的。

# 288 DNS 入门教程

```
C:\DnCmd <ServerName>/Config [<ZoneName>;..,AllZones] <Property> <Value>
Server <Property>
  /Protocol
  /EventLogLevel
  /Enabled
  /ForwardDelegations
  /ForwardTimeout
  /Is$
  /NoRetry
  /Recursion
  /RecursionInterval
  /MaxTTL
  /MaxNegativeCacheTTL
  /BoundLoad
  /LocalPriority
  /Boundaries
  /WriteCacheType
  /NameCacheFlushing
  /StrictTime
  /UpdateOptions
  /DisableNotifyZones
  /Temp
  /ConnectTimeout
  /PublishInterval
  /RefreshInterval
  /ScavengingInterval
  /ExpireInterval
  /DefaultNoRefreshInterval
  /DefaultRefreshInterval
```

图 A-9:

列出所有可配置属性。

Zone `<Property>`

  `/ZoneCounters`

  `/AllowUpdate`

  `/RefreshInterval <Value>`

  `/RefreshInterval <Value>`

`<Value>`: DWORD 值用于指示十六进制值。

注意：更改某些区域 DNSWORD 属性时必须重置它们。

使用区域 `"AllZones"` 应用于所有区域。

更多信息请参见 `descnd`。

命令执行成功。

```
C:\>
```

# 更改区域配置

就像你可以使用 `DNSCMD` 全局配置 DNS 服务器一样，你也可以使用命令配置单个区域。`DNSCMD` 可以替代 DNS MMC 快速插单元的所有功能。本节介绍了 `DNSCMD` 的某些选项，允许你调整区域设置。

## `/Config /Config <zone name> <property> <value>`

我们在前一个节中已结合全局服务器配置描述了此命令，但你也可以通过指定名称来使用它来配置单个服务器：

输入 `DNSCMD /Config ?` 会在 `Zone <Property>` 部分（参见图 A-9）显示用于区域配置的可用属性。可以使用本附录早些讨论过的 `DNSCMD /ZoneInfo` 命令（位于“收集信息”部分）来查看区域属性。

## ZoneAdd

`DNSCMD /ZoneAdd <zone name> /Primary /File <filename>`

`DNSCMD /ZoneAdd <zone name> /Secondary <IP Address> /File <filename>`

`DNSCMD /ZoneAdd <zone name> /DsPrimaryDSPrimary`

`DNSCMD /ZoneAdd` 命令将区域添加到 DNS 服务器中，并可以使用三种方式之一添加主区域、从用区域或 Active Directory (AD) 集成区域。为了添加集成区域，DNS 服务器必须已与 Active Directory 集成。这三条命令的形式如下：

添加主区域只需要一个存储区域数据的文件名。添加从用区域至少一个区域主服务器的 IP 地址，尽管你可以指定多个由空格隔开的地址。文件名是可选的，你可以省略 `/File` 参数。添加 Active Directory 集成区域不需要任何参数。使用此命令添加区域后，你就可以开始向该区域添加记录了。

## ZoneDelete

`DNSCMD /ZoneDelete <zone name>`

如你所料的，`/ZoneDelete` 选项会从 DNS 服务器中删除区域；然而，如果它是一个 Active Directory 集成区域，它将保留在目录服务器中。若要从 DNS 和目录服务器中同时删除集成区域，请在命令中添加 `/DsDel` 选项。默认情况下，系统会提示你确认删除区域。如果你不想被提示（如果你是从脚本运行该命令），请添加 `/f` 选项。

## ZonePause and ZoneResume

`DNSCMD /ZonePause <zone name>`

`DNSCMD /ZoneResume`

这些命令用于暂停和恢复（或继续）区域。被暂停的区域在恢复之前不会对查询做出响应。此功能对于在不禁用整个服务器的情况下临时禁用域非常有用。

## ZoneReload

`DNSCMD /ZoneReload <zone name>`

此命令在区域文件或目录服务器发生更改时，将区域重新加载到内存中。当区域文件手动更改后，使用此命令可以重新加载区域。对于集成区域，此命令会将区域重新加载到内存。

## `/ZoneWriteBack`

```
DNSCMD /WriteBack <zone name>
```

此命令在区域文件发生更改时，将区域写入。

## `/ZoneRefresh`

```
DNSCMD /ZoneRefresh <zone name>
```

为了刷新从用区域，使用此命令。当主服务器更改时，此命令对该区域进行刷新。对于从用区域，这种方法非常有用。当主 区域数据更改时，使用此命令对指定的区域进行刷新。

## `/ZoneUpdateFrom`

```
DNSCMD /ZoneUpdateFrom <zone name>
```

此命令与 `/ZoneRefresh` 命令类似，不同之处在于它从目录服务器刷新区域。此方法适用于集成区域，当该区域数据更改时。

## `/ZoneResetType`

```
DNSCMD /ZoneResetType <zone name> <type>
```

此命令更改区域类型。区域类型选项如下：

- `/Primary <filename>`

- `/Secondary <IP Address>`

- `/DsPrimary`

与 `/ZoneAdd` 命令一样，`/Primary` 选项需要文件名；`/Secondary` 选项需要至少一个 IP 地址。

## 附录 A：使用 DNSCMD 工具

`/ZoneResetType` 命令还有两个其他选项：

- `/OverWrite_Mem` 覆盖内存中的区域数据。

- `/OverWrite_Ds` 覆盖目录服务器中的数据。

## `/ZoneResetSecondaries`

`DNSCMD /ZoneResetSecondaries <zone name> <security> <notify>`

此命令用于主区域更改更改从用服务器设置。安全选项有：

- `/NoXfr`: 允许传输。

- `/NonSecure`: 允许向任何主机传输。

- `/SecureNs`: 允许向具有 NS 记录的任何主机传输。

- `/SecureList`: 允许向指定的主机传输。

默认的安全设为 `/NonSecure`。通知选项有：

- `/NoNotify`: 不发送通知消息。

- `/Notify`: 向所有从用服务器发送通知。

- `/NotifyList`: 仅向指定的主机发送通知。

默认的通知设置为 `/Notify`。

## `/ZoneResetMasters`

`DNSCMD /ZoneResetMasters <zone name> <IP address>`

类似于从用区域的 `/ZoneResetSecondaries`，此命令更改主服务器。`<IP address>` 选项必须包含至少一个 IP 地址，多个 IP 地址之间用空格隔开。

## `/ZoneResetScengeServers`

`DNSCMD /ZoneResetScenge <zone name> <IP address>`

此命令配置哪些服务器允许清理。如果没有指定 IP 地址，所有托管区域的主服务器或从用服务器都可以清理。如果指定了 IP 地址或地址列表，则指定的服务器可以清理。
