
![](img/f265c9d1f2610aca197c430cbfcd51f5_502_0.png)

**图 9.4 MRTG 周报、月报和年报。**

信息会为每个被监控的接口获取。你也可以自定义此更新间隔（或刷新率）。

## MRTG 的基本配置

MRTG 使用配置文件来指定要监控的设备。MRTG 包不带预定义的配置，因为列出的设备不太可能与您站点的设备匹配。相反，包中包含一个名为 **cfgmaker** 的实用程序，用于构建基本配置，这样你就不必从头创建。该实用程序的目的是轮询网络设备以获取特定的 SNMP 对象（例如，接口表）并构建适用于 MRTG 的配置文件。**cfgmaker** 的语法如下：

```
cfgmaker community@device
```

需要两个参数：设备的 community 字符串和主机名（或 IP 地址）。因为 **cfgmaker** 输出到标准输出，所以当你想保存结果时，应将输出重定向到文件。为了说明此实用程序的使用，假设我们想要监控远程办公室中的一台路由器。在此示例中，我们有一台名为 remote-gw 的 Cisco 2500 系列路由器，其 community 字符串为 louvre。因此命令为：

```
# cfgmaker louvre@remote-gw > cisco.conf
```

探测 remote-gw 设备并构建名为 cisco.conf 的 **MRTG** 配置文件。假设提供给 **cfgmaker** 的参数正确且设备响应 SNMP 请求，列表 9.1 显示了 **cfgmaker** 脚本将生成的配置（不包括 **cfgmaker** 添加的注释）：

### 列表 9.1 cfgmaker 配置文件示例

```
Target[10.0.2.75.1]: 1:public@10.0.2.75
MaxBytes[10.0.2.75.1]: 124994
Title[10.0.2.75.1]: remote-gw (No hostname defined for IP address): Ethernet0
PageTop[10.0.2.75.1]: <H1>Traffic Analysis for Ethernet0
</H1>
<TABLE>
    <TR><TD>System:</TD><TD>remote-gw in Graphics Lab 11-BK</TD></TR>
    <TR><TD>Maintainer:</TD><TD>Steve Maxwell</TD></TR>
    <TR><TD>Interface:</TD><TD>Ethernet0 (1)</TD></TR>
    <TR><TD>IP:</TD><TD>No hostname defined for IP address (161.135.59.129)</TD></TR>
    <TR><TD>Max Speed:</TD>
        <TD>1250.0 Kbytes/s (ethernetCsmacd)</TD></TR>
</TABLE>
# --------------------------------------------------
Target[10.0.2.75.2]: 2:public@10.0.2.75
MaxBytes[10.0.2.75.2]: 6982
Title[10.0.2.75.2]: remote-gw (No hostname defined for IP address): Serial0
PageTop[10.0.2.75.2]: <H1>Traffic Analysis for Serial0
</H1>
<TABLE>
    <TR><TD>System:</TD><TD>remote-gw in Graphics Lab 11-BK</TD></TR>
<TR><TD>MaxSpeed:</TD><TD>6982.0 Bytes/s (rfc877x25)</TD></TR>
</TABLE>
#
```

要在 MRTG 配置文件中支持注释，请在每行开头使用井号（#）字符。文件忽略空行。配置文件包含一个或多个轮询实例，其中包含标记和相关值。这些标记共同代表一个被监控的元素。每个元素代表一个被轮询的实体，其中包括从被监控设备查询的 SNMP 对象以及结果信息的额外显示格式。每个元素由单个井号（#）后跟一系列“...”字符分隔（如列表 9.1 的最后一行所示）。此特定路由器仅包含几个网络条目，并且关键字 target 对应于每个路由器接口。这是一个关键观察：任何要由 MRTG 监控和显示的数据都需要一个 target 条目。

此特定路由器包含三个接口——一个以太网和两个串行——但 cfgmaker 仅报告两个接口。因为第三个接口处于管理关闭状态，cfgmaker 跳过了此接口。要么该接口未在路由器中配置，要么因其他原因被禁用。无论如何，cfgmaker 包含前两个接口，但在 cisco.conf 文件中在第三个接口前插入注释字符，以便它不会被 MRTG 软件轮询，如列表 9.2 所示。

### 列表 9.2
注释的接口条目

```
##
# This interface is one of the following
# - administratively not UP
# - it is in test mode
# - it is a softwareloopback interface
# - has a unrealistic speed setting
# It is commented out for this reason.
##
```

```
# Target[10.0.2.75.3]: 3:public@10.0.2.75
# MaxBytes[10.0.2.75.3]: 193000
# Title[10.0.2.75.3]: remote-gw (No hostname defined for IP address): Serial1
# PageTop[10.0.2.75.3]: <H1>Traffic Analysis for Serial1
# <BR></H1>
# <TABLE>
# <TR><TD>System:</TD><TD>remote-gw in </TD></TR>
# <TR><TD>Maintainer:</TD><TD></TD></TR>
# <TR><TD>Interface:</TD><TD>Serial1 (3)</TD></TR>
# <TR><TD>IP:</TD><TD> ()</TD></TR>
# <TR><TD>Max Speed:</TD>
# <TD>193.0 kBytes/s (propPointToPointSerial)</TD></TR>
# </TABLE>
# ---------------------------------------------------------------
```

禁用该接口是个好主意，因为当没有流量时，让 MRTG 轮询非活动接口是不合理的，这会产生空图表。此外，如果接口在未来某天启用并投入使用，只需简单地“取消注释”接口条目，即可允许 MRTG 监控该端口。MRTG 配置文件使用 HTML 格式化语言，特别是构建表格来格式化设备信息，如 <TABLE> 和 </TABLE> 标签所示。配置还包括一个或多个关键字，用于控制监控哪些设备以及如何绘制数据图表。每个关键字包含以下语法：

```
Command [label] args
```

其中 **Command** 是接下来显示的命令之一，后跟用括号括起的标签和一个或多个参数或命令选项。

配置文件中的每个被监控元素或接口通常包含以下关键字：

- Target
- MaxBytes
- Title
- PageTop

**target** 关键字指示 MRTG 应监控的内容。基本格式如下

```
Target[label]: port:community@device
```

*标签* 用作标识符，以便 MRTG 可以在一页 HTML 上显示一组关键字。*标签* 是设备 IP 地址和接口号的组合。*端口* 是 MRTG 应使用 SNMP *社区字符串* 的 *社区* 轮询的 *设备* 中定义的接口号。端口或接口号必须是被轮询设备上的有效接口。你可以使用 MRTG cfgmaker 程序确定给定设备上的有效接口。通过使用此程序，你将使给定设备内的所有已定义接口自动被发现。或者，使用 MIB 浏览器，你可以浏览设备的 MIB 树并检查接口表以手动发现接口。然而，如果你已经知道要监控哪些接口，手动指定可能是最简单的方法。使用上面的配置示例，考虑以下 **Target** 命令：

```
Target[10.0.2.75.1]: 1:public@10.0.2.75
```

此命令将定义 *标签* 10.0.2.75.1 并指示 MRTG 使用 *社区字符串* public 监控 IP 地址为 10.0.2.75 的设备的第一个接口的流量。默认情况下，*MRTG 轮询 MIB 对象* ifInOctets *和* ifOutOctets *从指定设备并随时间绘制此数据的图表。*

**MaxBytes** 关键字定义任何被监控流量统计的上限，并确定未缩放图表的 y 轴范围。对于任何接口，**MaxBytes** 关键字通常以每秒字节为单位指定，可以通过将接口的最大带宽除以八来计算。例如，因为 10M 以太网的最大带宽为 10Mbps，除以八（8）后，我们得到 1250000（10,000,000 / 8 = 1,250,000）。正确设置此值非常重要，因为这将确保图表显示真实的信息。例如，在列表 9.2 中，命令

```
MaxBytes[10.0.2.75.1]: 1250000
```
