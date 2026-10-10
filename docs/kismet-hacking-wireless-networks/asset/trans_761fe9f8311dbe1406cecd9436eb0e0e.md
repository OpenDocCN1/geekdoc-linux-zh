
## 是否锁定模式？

```
# Do we lock the mode? This overrides coordinates of lock "0", which will
# generate some bad information until you get a GPS lock, but it will
# fix problems with GPS units with broken NMEA that report lock 0
gpsmodelock=false
```

此参数用于解决那些在获得 GPS 卫星锁定之前不会发送正确数据的 GPS 设备的问题。如果您的 GPS 在启动时出现问题，请将此参数设置为 "true"。您可能还需要检查您的 GPS 是否有更新的固件。

## 包过滤选项

```
# Packet filtering options:
# filter_tracker - Packets filtered from the tracker are not processed or
#                recorded in any way.
# filter_dump  - Packets filtered at the dump level are tracked, displayed,
#                and written to the csv/xml/network/etc files, but not
#                recorded in the packet dump
# filter_export - Controls what packets influence the exported CSV, network,
#                xml, gps, etc files.
# All filtering options take arguments containing the type of address and
# addresses to be filtered. Valid address types are 'ANY', 'BSSID',
# 'SOURCE', and 'DEST'. Filtering can be inverted by the use of '!' before
# the address. For example,
# filter_tracker=ANY(!00:00:DE:AD:BE:EF)
# has the same effect as the previous mac_filter config file option.
# filter_tracker=...
# filter_dump=...
# filter_export=...
```

Kismet 可以在程序的各个层级过滤特定的 MAC 地址。如果您希望从日志或显示中排除已知的接入点（AP）和客户端，这将非常有用。您还可以限制数据包在客户端-服务器链中传播的程度，以及它是否记录在日志中。

- filter_tracker=: 如果任何数据包匹配指定的参数，它们将不会添加到显示或任何日志文件中，而是被直接丢弃。
- filter_export=: 如果任何数据包匹配指定的参数，它们将不会包含在 CSV、网络、xml、gps 等文件中，但会记录在 dump 文件中。
- filter_netclient=: 如果数据包来自特定的网络客户端，则不记录它。

MAC 地址可以指定为 SOURCE（源地址）、DEST（目的地址）、BSSID 和 ANY（任意）。源地址和目的地址有助于消除已知客户端，BSSID 用于指定无线 AP 的 MAC 地址。ANY 将过滤具有该 MAC 地址的任何数据包，无论它出现在帧中的哪个位置。仅指定 MAC 地址即可激活针对该地址的匹配过滤器，或者您可以在开头添加感叹号来指定反义，以过滤除指定地址以外的所有内容。

```
filter_tracker=ANY("!00:00:DE:AD:BE:EF")
```

这将过滤日志和包跟踪器中所有不匹配指定 MAC 地址 00:00:DE:AD:BE:EF 的数据包。

```
filter_dump=BSSID("00:00:DE:AD:BE:EF")
```

这一行将从 dump 文件中过滤掉来自 BSSID 为 00:00:DE:AD:BE:EF 的 AP 的数据包。

```
filter_tracker=ANY("00:00:DE:AD:BE:EF")
```
这一行将从显示和日志中丢弃所有 MAC 地址为 00:00:DE:AD:BE:EF 的数据包。如果您想要监控流氓网络，并从日志和显示中消除已知网络和客户端，这特别有用。

## 要报告的警报及节流速率

```
# Alerts to be reported and the throttling rates.

# alert=name,throttle/unit,burst/unit

# The throttle/unit describes the number of alerts of this type that are

# sent per time unit. Valid time units are second, minute, hour, and day.

# Burst rates control the number of packets sent at a time

# For example:

# alert=FOO,10/min,5/sec

# Would allow 5 alerts per second, and 10 alerts total per minute.

# A throttle rate of 0 disables throttling of the alert.

# See the README for a list of alert types.
```

Kismet 具有一些基本的 IDS（入侵检测系统）功能，用于检测数据包中已知的攻击模式，或检测某些可被恶意使用的软件的存在。

这些警报可以为网络管理员提供极大的权力，以判断其网络是否正在遭受攻击，或者问题是否来自其他来源。虽然某些数量和类型的警报是正常的，但过量的警报可能表明存在问题或攻击。

这些警报模式内置于 Kismet 源代码中，并不易于修改。然而，触发警报的阈值是可以配置的。“alert=” 行指定了源代码中内置的警报及其在触发警报日志记录之前的阈值。如果您想禁用该警报，只需在其前面添加注释符 “#” 即可。

每个警报都有自己的参数。*alert=FOO,10/min,5* 将启用 FOO 警报。当 FOO 事件在一秒钟内发生 5 次时，会触发一个警报。在此初始触发之后，如果在相同时间范围内再次发生 FOO，它将生成另一个警报，每分钟最多 10 个警报，以避免用数千个相同警报堵塞警报窗口。

这些警报会提醒您某些正在运行的网络发现应用的存在，以及一些表明攻击的异常模式。像 Kismet 这样的被动嗅探器无法被检测到，离线攻击显然也无法被检测到。它不是一个全面的 IDS 系统，但可以快速识别常见的攻击和问题非常有用。

```
alert=NFTSTUMBLER,10/min,1/sec
```

此警报通过检测其使用时广播的独特数据包，来检测 Netstumbler 网络发现工具的存在。

```
alert=WELLENREITER,10/min,1/sec
```

此警报检测另一种网络发现工具 Wellenreiter 的存在。具体而言，此警报检测 Wellenreiter 的 SSID 暴力破解器。如果网络没有广播其 SSID，可以通过使用字典进行探测并监听响应来揭示 SSID。当 Wellenreiter 执行此操作时，它会通过特定的行为触发此警报，即在每次探测尝试之间，将重置卡片以探测 *“this_is_used_for_wellenreiter.”*

```
alert=LUCENTTEST,10/min,1/sec
```

此警报用于检测 Lucent 网络链路测试的存在。这是一种站点调查工具，可用于基础的漫游和侦察。

```
alert=DEAUTHFLOOD,10/min,2/sec
```

此警报检测去认证洪泛。如果攻击者正在伪造来自 AP MAC 地址的去认证数据包发送给客户端，则会生成警报。如果分离是正常发生的，且只有过度的去认证行为发生时，才会触发警报。

```
alert=BCASTDISCON,10/min,2/sec
```

此警报用于广播洪泛，这在正常情况下不应发生。在广播洪泛中，攻击者用分离或去认证数据包淹没网络，试图使客户端与其当前 AP 断开关联并关联到流氓网络。

```
alert=CHANGE,5/min,1/sec
```

此警报记录之前检测到的网络突然更改频道的情况。这是伪造网络尝试的一个良好指标，因为大多数网络不会定期更改频道。

```
alert=AIRJACKSSID,5/min,1/sec
```

此警报查找名为 “airjACK” 的探测 SSID 名称，这是 airjACK 工具的初始 SSID。airjACK 工具允许原始模式注入和接收，并用于许多可能具有恶意的工具。此警报仅检测 airjACK 的 SSID，而不检测工具本身。熟练的攻击者可以轻松地更改初始 SSID 为更无害的内容。

```
alert=PROBENOJOIN,10/min,1/sec
```

如果客户端探测现有网络并被接受但未加入，这表明存在基于固件的网络发现工具，例如 Netstumbler。在某些情况下，这可能产生大量的假阳性，并且可能不表明存在攻击。某些在关联前等待用户输入的网络客户端应用程序也可能触发此警报。

```
alert=DISSASOCTRAFFIC,10/min,1/sec
```

如果客户端似乎与 AP 断开关联，通常它随后不应尝试与 AP 通信。如果触发此警报，很可能警报中指定的客户端遭受了分离攻击，攻击者向 AP 发送伪造数据包表明客户端正在离开。

```
alert=NULLPROBERESP,10/min,1/sec
```

这是针对许多制造商的某些固件版本的攻击迹象，如果接收长度为 null（无长度）的 SSID 探测，会出现致命错误。这可能是拒绝服务（DoS）攻击或行为异常客户端的迹象。

```
alert=BSSTIMESTAMP,10/min,1/sec
```

来自 AP 的每个数据包都有时间戳，并且应该以类似于连续流的方式接收。使用正常的驱动程序不可能伪造时间戳，因此接收到差异巨大的时间戳表明有人可能正在尝试伪造 AP 的 SSID 和/或 MAC 地址。在高丢包率导致并非所有数据包都被接收的情况下，这可能会触发一些假阳性。

