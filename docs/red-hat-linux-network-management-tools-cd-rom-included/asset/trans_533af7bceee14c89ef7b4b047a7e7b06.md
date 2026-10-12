
```
PageTop[^]: <H1>The Engineering Lab</H1>
PageTop[10.0.2.100.1]: <H1>Traffic Analysis for ATM</H1>
```

在此输出中，第二个实例的 **PageTop**[^] 会覆盖第一个，并在整个配置文件中被使用，除非遇到额外的 **PageTop**[^] 关键字。

此外，使用 ^ 和 $ 定义的先前值可以通过仅使用字符而不提供任何字符串定义来重置为空或取消设置。因此，

```
PageTop[^]:
PageTop[$]:
```

将关键字重置为无值的默认状态。

下划线字符 _ 与 MRTG 关键字一起使用，并为该关键字指定默认值。如果没有明确的关键字值或附加值，则将使用默认值，如以下示例所示：

```
Target[10.0.2.75.1]: 1:public@10.0.2.75
```

带有标签 10.0.2.75.1 的 **Target** 定义可以在不使用标签字符串的情况下复制。因此，

```
MaxBytes[_]: 1249991
Title[_]: remote-gw : Ethernet0
Options[_]: growright
PageTop[_]: <H1>Traffic Analysis for Ethernet0</H1>
```

都是有效的 MRTG 条目——因为下划线指向 10.0.2.75.1 标签。

要重置下划线，请指定空值：

```
Options[_]:
```

## 主索引

MRTG 可以被视为 *以接口为中心*。这意味着其主要关注点是被监控设备的接口。如果使用 MRTG 监控具有五个接口的 Cisco 路由器，将创建五个单独的 MRTG 报告。不幸的是，虽然这种结构对于少量接口来说足够，但面对大量接口或许多设备和接口的组合时，使用和管理变得困难。为协助完成此任务，MRTG 发行版中提供了一个名为 indexmaker 的脚本，该脚本可生成所有被监控设备和接口的索引。此脚本可在 /usr/lib/mrtg 目录中找到。indexmaker 的语法如下：

```
indexmaker label config result_file
```

此命令支持多个命令行参数。表 9.5 显示了其中许多更重要的参数。至少需要三个参数：MRTG 配置文件、图形标签以及包含应添加到索引中的所有被监控接口的正则表达式。由于 indexmaker 输出到标准输出，因此应将输出重定向到文件。因此，示例命令

```
# indexmaker -t 'Summary of Interfaces' *.conf > backbone.html
```

使用文件 backbone.html 为 10.0.2.75 设备中包含的所有接口构建主接口索引。

## 表 9.5 indexmaker 命令行参数

| Option | Description |
| :----- | :---------- |
| -1 | 构建单列网页。图形将堆叠在彼此之上 |
| -2 | 构建双列网页。图形并排放置而不是堆叠在彼此之上。这是默认模式 |
| -b | 设置背景颜色。默认值为白色（或无颜色）。值必须以十六进制格式指定。例如，#ffffff 是黑色的代码 |
| -r | 使用指定的正则表达式匹配目标接口。默认值为“.*” |
| -t | 设置索引页面的标题。默认值是 All Targets |
| -P | 设置解析索引页面中图形名称的 PageTop 标签。这是默认值 |

## 表 9.5 indexmaker 命令行参数（续）

| Option | Description |
| :--- | :--- |
| `-P` | 不设置解析 `index page` 中图形名称的 `PageTop` 标签 |
| `-H` | 设置图形之间使用 `<HR>` 标签。这是默认值 |
| `-h` | 不设置图形之间使用 `<HR>` 标签 |
| `-S` | 按字母顺序排序图形。这是默认排序顺序 |
| `-s` | 不对图形排序。它们将按配置文件中找到的顺序出现 |
| `-N` | 在每个图形开头添加序列号 |
| `-n` | 不对图形编号。这是默认值 |
| `-X` | 指定每个图形的宽度。默认值是 500 |
| `-Y` | 指定每个图形的高度。默认值是 135 |
| `-A` | 在 HTML 代码中将参数作为注释包含 |
| `-a` | 不将参数作为注释包含 |
| `-G` | 将图形添加到索引页面。默认情况下已启用 |
| `-g` | 不向索引页面添加任何图形 |

indexmaker 程序可在 /usr/lib/mrtg 目录中找到。显示新文件时，其外观应类似于图 9.5 所示的窗口。它显示每个接口的每日图形，并包含指向每个定义页面的链接，这些页面包含该接口的剩余图形。

![](img/f265c9d1f2610aca197c430cbfcd51f5_520_0.png)

**图 9.5** 被监控设备的主索引。

## 监控附加信息

MRTG 可以使用 **target** 命令来监控其他信息——包括额外的 SNMP 对象和非 SNMP 信息。**target** 命令接受可用于监控和绘制信息图表的额外输入格式。这些格式包括直接 OID 字符串、SNMP 缩写对象和自定义命令。直接 OID 格式使用对象标识符（OID）字符串，以完全限定的点分十进制表示法表示，指定 MRTG 应监控哪个对象。**完全限定** 表示已提供从根到对象的完整路径。例如，要从设备 `10.0.2.200` 监控 `ifInErrors` 和 `ifOutErrors`，请使用以下命令：

Target [10.0.2.200.1]:1.3.6.1.2.1.2.2.1.14.1&1.3.6.1.2.1.2.2.1.20.1, \
public@10.0.2.200

此命令检索接口 1 的输入和输出错误计数。

请注意前述命令中使用 & 字符。MRTG 在显示数据时需要两个变量；该字符用作分隔符。或者，可以使用 SNMP 缩写对象名称代替直接 OID 惯例。因此，命令

```
Target[10.0.2.200.1]:ifInErrors.1&ifOutErrors.1:public@10.0.2.200
```

在功能上等同于之前的 **Target** 命令。MRTG 知道有限数量的 SNMP 对象；可以通过修改和向 mibhelp.txt 文件添加对象来扩展对象列表。此文件包含某些 SNMP MIB-II 对象与完全限定 OID 路径之间的映射。以下是该文件的一个示例：

```
Descriptor:	ifInErrors
Identifier:	1.3.6.1.2.1.2.2.1.14
ASN.1 Syntax:	Counter32

The number of inbound packets that contained errors preventing them from being deliverable to a higher-layer protocol.
```

此文件示例显示了前述 **Target** 命令中使用的 ifInErrors 对象，并包含该对象的描述符、标识符和 ASN.1 语法。描述符命名 MRTG 将使用的对象，并与标识符字符串关联；只要在 mibhelp.txt 文件中唯一，可以是任何字符串名称。标识符是对象的完全限定路径名，不包括实例。ASN.1 语法指对象类型，应与定义该对象的 MIB 中找到的对象定义相匹配。最后，条目包含解释对象定义的描述性文本。虽然此文本不是必需的，但非常有用，在向此文件添加额外对象时建议包含它。

表 9.6 列出了 mibhelp.txt 文件中预定义的 SNMP 对象。请参阅第 6 章“Overview of MIB-II”，以获取有关这些 MIB-II 对象的更多信息。

## 表 9.6 预定义的 SNMP MRTG 对象

| SNMP Object | Object information |
| :--- | :--- |
| *ifOperStatus* | 接口的当前运行状态 |
| *ifAdminStatus* | 接口的当前管理状态 |
| *ifInOctets* | 接口接收的总八位字节数，包括帧字符 |
| *ifInUcastPkts* | 交付给高层协议的子网单播数据包数 |
| *ifNUcastPkts* | 交付给高层协议的非单播（即子网广播或子网多播）数据包数 |
| *ifInDiscards* | 被选为丢弃的入站数据包数 |
| *ifInErrors* | 包含错误导致无法交付给高层协议的入站数据包数 |
| *ifInUnknownProtos* | 因未知或不受支持的协议而被丢弃的通过接口接收的数据包数 |
| *ifOutOctets* | 从接口传输的总八位字节数，包括帧字符 |
| *ifOutUcastPkts* | 高层协议请求传输到子网单播地址的数据包总数，包括被丢弃或未发送的数据包 |
| *ifOutNUcastPkts* | 高层协议请求传输到非单播（即子网广播或子网多播）地址的数据包总数 |

