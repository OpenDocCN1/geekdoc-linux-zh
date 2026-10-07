
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

在会话关闭之前，客户端可能仅发送单个 TCP 段。这允许客户端通过建立的 TCP 连接发送 SPA 负载，而不发送其他任何内容。然后，通过使用 Tor 所需的 socks5 代理的 `socat` 程序，结合 `fwknop` 命令行上的 `--socat` 参数，可以将 SPA 包通过 Tor 网络发送。

注意：关于 `socat` 的更多信息，请参阅 http://www.dest-unreach.org/socat。

# 结语

本章和第 12 章展示了计算机安全领域的强大技术，说明了服务器如何通过默认丢弃（default-drop）数据包过滤器受到保护，只有向被动监控设备证明其身份的客户端才能获得访问权限。端口触发（Port knocking）是实现这一理念第一个技术，但由于端口触发架构的严重局限性（包括难以充分解决重放问题，以及无法传输超过几十字节的数据），SPA 已证明自己是一种更健壮的技术。将授权以太网嗅探器与默认丢弃数据包过滤器相结合的概念在计算机安全领域是一个较新的概念，但似乎每天都有新的实现方案涌现。

`fwknop` 是基于 `iptables` 的 SPA 开源实现，为在 SPA 范式内管理多个用户提供了灵活机制。

> 甚至有一个项目尝试将基于 HMAC 的 SPA 直接放入 `iptables`；请参阅 http://svn.berlios.de/svnroot/portknocking，以及 Netfilter 开发列表存档中的一个讨论帖：http://lists.netfilter.org/pipermail/netfilter-dev/2006-October/thread.html。

# 14

## 可视化 IPTABLES 日志

![](img/84e6ec42d170b9df6cf29b40151f3d15_278_0.png)

在当今开放互联网的威胁环境中，安全数据的可视化变得越来越重要。安全设备——从入侵检测系统到防火墙——在处理来自全球各地的攻击时，会产生大量的事件数据。理解这些海量数据是一项巨大的挑战。安全数据的图形化表示允许管理员快速看到新兴趋势和异常活动，如果没有专门的代码，这些活动是很难检测到的。也就是说，图表能够有效地传递上下文和变化，因为人眼可以快速辨别出其他难以察觉的关系。

本章探索了使用 `psad` (http://www.gnuplot.info) 和 `AfterGlow` (http://afterglow.sourceforge.net/) 项目生成 `iptables` 日志数据的图形化表示。我们的主要数据源将来自 Honeynet Project 的 `iptables` 日志（参见 http://www.honeynet.org）。

Honeynet Project 是安全社区不可比拟的资源；它公开发来自受攻击的活跃蜜网系统的原始安全数据（Snort 告警和 `iptables` 日志）。Honeynet Project 的主要目标是通过一系列“安全挑战”让这些安全数据用于分析，这些挑战的结果会发布在 Honeynet Project 网站上。在本章中，我们将可视化来自 Scan34 Honeynet 挑战的数据（参见 http://www.honeynet.org/scans/scan34）。你可以从 http://www.cipherdyne.org/LinuxFirewalls 下载本章提到的所有图表和 Gnuplot 文件。

本章中的所有示例均假设 Scan34 `iptables` 数据文件在当前目录中名为 `iptables.data`。

## 观察异常

考虑以下组数字：

+ 5, 4, 2, 1, 3, 4, 55, 58, 70, 85, 120, 9, 2, 3, 1, 5, 4

该数据集代表某个特定 IP 地址每分钟连接的 TCP 或 UDP 端口数量；这些信息可以通过解析 `iptables` 日志数据获取。注意数据集中的峰值，端口数量从 4 快速增加到 120，然后回到 1 到 5 之间的稳定状态。

当使用 `Gnuplot` 将这些数据以图形形式表示时（如图 14-1 所示），峰值一目了然。

![](img/84e6ec42d170b9df6cf29b40151f3d15_279_0.png)

图 14-1：每分钟到达端口的数据包数量

端口扫描是这种峰值的可能解释之一。其他解释可能是 `iptables` 策略配置不当，记录了良性流量，或者错误记录了属于已连接的 TCP ACK 包。峰值的实际解释在这里并不重要——重要的是这个峰值是异常的。图表可以轻松快速地显示现状的剧变，并允许你将精力集中在这个问题区域上。

在前面的示例中，在如此小的数据集中发现模式相对容易。现在，假设你面对的是一个由 1,000 或 100,000 个数字组成的类似数据集。如果不制图，肉眼从这么多数据中提取趋势是令人生畏的。

图 14-2 是一个包含 800 多个点的图表，记录了 `iptables` 策略在约五周时间内记录的 TCP SYN 包数量，速率为每月一个数据点。数据源来自 Scan34 Honeynet 挑战的 `iptables` 日志文件，并使用 `ps` 解析数据以

![](img/84e6ec42d170b9df6cf29b40151f3d15_280_0.png)

图 14-2：每小时到达端口的 SYN 包数量

> 1 这可能是由于 TCP 连接关闭周围的时间问题导致的。特别是，Netfilter 连接跟踪子系统会对处于 CLOS_WAIT 状态的 TCP 连接设置 60 秒定时器；在内核源码的 `linux/net/ipv4/netfilter/ip_conrack_proto.tcp` 文件中，超时时间是变量，但有时在定时器过期后仍会发送意外的 TCP ACK 包（通过 CLOSING 和 LAST-ACK 状态结束连接）。这导致 TCP ACK 包不被识别为现有连接的一部分，因此可能会应用 `iptables` 的 LOG 和 DROP 规则。

如你所见，很容易从图表中挑选出感兴趣的区域。x 轴划分为单独的小时并以周为增量标记；y 轴显示端口数量，并以 500 为增量进行标记。3 月 27 日的大峰值迅速引导你关注一个值得仔细审视的时间段。

## Gnuplot

`Gnuplot` 项目可以生成许多类型的图表，从直方图到三维曲面图。它在绘制大型数据集方面表现出色，例如源自数十万行 `iptables` 数据的点。

对于本章中 `iptables` 日志数据的可视化，我们使用 `Gnuplot` 生成二维和三维的图表。`Gnuplot` 需要格式化数据作为输入，本身并不具备解析 `iptables` 日志消息所需的机制。`Gnuplot` 的理想输入是一个包含列整数值的文件——每一列对应二维或三维图中的一个轴。这正是 `ps` 使用 `--gnuplot` 模式的用武所在。在此模式下，`ps` 解析 `iptables` 日志数据并将结果写入可供 `Gnuplot` 处理的文件。

为了在你的 Linux 系统上复制本章中的图表（或根据你的 `iptables` 数据生成新图表），你需要同时安装 `ps` 和 `Gnuplot`。

## Gnuplot 图表指令

`Gnuplot` 在绘制数据图表时遵循一系列配置指令。这些指令描述了渲染细节，如图表类型、坐标范围、输出模式（例如输出到图形文件或终端）、轴标签和图表标题。每个指令都可以通过 `Gnuplot` 交互式 shell 的命令提示符进行设置，也可以通过由 `Gnuplot` 加载的文件设置。例如，图 14-2 中的每小时端口数据是这样绘制的：

```
$ fig14-2.gnu

reset
```

+   - set title "ps iptables log visualization: timestamp dp:counterhour"
- set terminal transparent nocrop enhanced
- set output "fig14-2.png"
- set xdata time
- set timefmt "%s"
- set format "%m/%d"
- set xlabel "time"
- set xrange ["1140887484":"1143867180"]
- set ylabel "dp:counterhour"
- set yrange [0:3000]
- plot "fig14-2.dat" using 1:2 with lines

上述 `fig14-2.gnu` 文件中最重要的指令是以下几个：

- **set title** ① 处的图表标题，在本例中它由 `psad` 设置，我们将在下一节中介绍。

- **set terminal** ② 处的终端设置和输出文件，如果你使用 `Gnuplot` 启动一个交互式窗口（你可以在图表上移动光标），则可以省略此项。（这在查看复杂数据集时很有帮助。）

- **set xdata time** ③ 处的时间设置，以及后续几行的时间输入和输出格式，它们告诉 `Gnuplot` 每个点的 x 坐标是一个时间值。

- **set xrange** ④ 处的 x 轴范围，设置了 Scan34 数据的起始和结束值。（时间值是自 Unix 纪元 1970 年 1 月 1 日 00:00 UTC 以来的秒数。）

- **plot** ⑤ 处的绘图是最重要的 `Gnuplot` 指令，因为它告诉 `Gnuplot` 数据所在位置以及如何绘制。在本例中，二维折线图是由 `fig14-2.dat` 文件中的数据制成的。在本章中我们还将看到其他绘图样式，例如点图（`plot` 指令将 `Gnuplot` 置于二维模式）。使用 `1:2` 字符串指定要绘制的图表列数；在三维模式下，使用 `1:2:3` 告诉 `Gnuplot` 将第 1、2、3 列作为 x、y、 和 z 轴。

## 结合 psad 和 Gnuplot

如第 6 和 7 节所示，`psad` 的核心功能之一是解析和解释 `iptables` 日志。通过一系列命令行开关，`psad` 的解析能力可以与 `Gnuplot` 的功能相结合。这些开关中最重要的的是 `--command` 参数，它为 `psad` 解析 `iptables` 日志数据并构建 `Gnuplot` 数据提供了配置性，选项如下：

`--CSV-fields` 设置从 `iptables` 日志中提取的字段。常用的字段有 `src`、`dst`、`dp` 和 `proto`（分别映射到 `iptables` 日志中的 SRC、DST、DPT 字段）。接受额外的匹配标准以排除或包含特定值。例如，如果源 IP 地址位于 `192.168.50.0/24` 子网内，目标 IP 地址位于 `10.100.0.0/24` 子网内且目标端口为 `80`，可以使用 `--CSV-fields "src:192.168.50.0/24 dst:10.100.0.0/24 dp:80"`。此外，支持按时间跨度（天、小时或分钟）计数字段字符串 `countmin`。

`--CSV-regex` 对原始 `iptables` 日志执行正则表达式匹配，只有当正则表达式匹配时才包含消息字段。例如，要创建一个三位的日志排序（见第 10 节），`nnn` 是三位数可以使用 `--CSV-regex "SID[d]{3}"`。同样支持反正则表达式 `--CSV-neg-regex` 命令行参数。

`--gnuplot-graph` 设置 `Gnuplot` 图样式。可能的值包括点（`dots`）、结（`knots`）和线（`lines`）。

`--gnuplot-file-prefix` 设置 `psad` 使用的文件前缀以创建两个文件：`prefix.dat` 和 `prefix.gnu`。`prefix.gnu` 文件包含了用于绘制 `prefix.dat` 数据 `Gnuplot` 指令。

## Afterglow

`Afterglow` 专门将数据可视化为链接图和节点。链接图是节点之间关系的表示。这种图非常适合显示 IP 地址和端口号。`Afterglow` 由 Rafael Marty 开发，安全可视化网站 http://www.secviz.org 包含了从 SSH 连接到 `iptables` 策略的可视化。`psad` 的接口类似于 `Gnuplot`。对于 `Afterglow`，`--CSV-fields` 命令行参数再次变得重要，用于从 `iptables` 日志文件中提取字段，`--CSV-regex` 和 `--CSV-neg-regex` 参数允许通过正则表达式过滤数据。例如，要让 `Afterglow` 构建发送从 `11.11.0.0/16` 网络到外部系统的 SYN 包的图表，你可以执行以下命令：

```
psad iptables.data -CSV --CSV-fields "src:11.11.0.0/16 dst:not11.11.0.0/16 dp" --CSV-regex "SYN?" | perl afterglow.pl -c color.nf | neato -Tpng -o webconnections.png
```

上述命令的结果是 `webconnections.png` 文件中解析出的数据可视化。我们将在本章后面看到 `Afterglow` 生成的链接图，但需要注意的一个重要特性是，你可以通过提供配置文件控制每个图节点的颜色。这是一个修改后的配置文件示例：

```
# Afterglow Color File

（此处省略重复的注释行...）
```

## 端口扫描

1. 端口扫描

端口扫描的关键特征是扫描器将数据包发送到范围内的端口。因此，在可视化大型 `iptables` 数据集时，将 IP 地址与唯一端口数绘制图是提取端口扫描活动的好方法。以下 `psad` 执行使用 `--src:not11.11.0.0/16 dp:countuniqu` 命令行参数来绘制非本地源地址与唯一端口数的图表：

```
psad -m iptables.data --src:not11.11.0.0/16 dp:countuniqu --gnuplot-graph points --gnuplot-xrange 0:26500 --gnuplot-file-prefix fig14-1
```

+   + 进入 gnuplot 模式...
+ 解析来自文件 iptables.data 的 iptables 日志
+ 解析了 179753 条 iptables 日志。
+ 将解析后的 iptables 数据写入：fig14-3.dat
+  gnuplot 指令文件：fig14-3.gnu
+ $ gnuplot fig14-3.gnu

`Gnuplot` 生成了如图 14-3 所示的图。

![](img/84e6ec42d170b9df6cf29b40151f3d15_285_0.png)

图 14-3：源 IP 地址与唯一端口数

如你在图 14-3 中所示，该图绘制的是单个点而不是绘制连续线（此选项在上面的 `psad` 执行中以粗体显示），大多数源地址仅向一个发送了包

或者两个唯一端口，尽管有一些地址连接了大约 10 个端口。然而，正如你在图表左上角看到的，其中一个 IP 地址（在 x 轴的 1,000 范围附近）连接了 60 个唯一端口；这是整个数据集中排名第一的端口扫描器。

注意，端口扫描的时间跨度未纳入图表中。源 IP 地址扫描这 60 个端口的快慢并不重要——该扫描可能跨越了数据集涵盖的整个五周时间范围，但在图 14-3 中它仍会显示为排名第一的端口扫描器。

## 注意事项

由于 Gplot 处理整数数据时效果最好，`psad` 在解析 `iptables` 日志时，会将所有 IP 地址映射为唯一的正整数（从 0 开始）。因此，IP 地址 192.168.3.2 会被映射为类似 502 的数字，而 11.71.92 则被映射为 10210，具体取决于日志文件中唯一地址的数量。在 Gplot 数据文件的每行中，IP 地址始终以尾随逗号的形式出现在行末。这让你能够看到该整数地址映射到了哪个地址。

`psad` 产生的 fig 14-3.dat 文件在文件顶部包含以下三个数据点：

```
905, 66 ### 905=60.248.102

12415, 10 ### 12415=63.135.2.15

15634, 30 ### 15634=63.186.32.94
```

这告诉我们排名第一的端口扫描器是 IP 地址 60.248.102，总共扫描了 66 个目标端口。接下来的两个违规者各仅扫描了 10 个唯一端口。

现在让我们为 Scan34 数据集的每小时唯一端口数量绘制图。这将向我们展示是否存在快速的端口扫描，或者扫描者是否都试图避开可能监控蜜罐网的任何 IDS 的端口扫描阈值：

```bash
# psad -m iptables.data --gnuplot --CSV-fields timestamp
p:countuniqu --gnuplot lines --gnuplot-xrange 1140887484:1143867180
--CSV-neg-regex 'SRC=11.11.* --gnuplot-yrange 0:100 --gnuplot-line-prefix
fig14-gnu
```

执行 Gnu 会生成一个每小时连接唯一端口数量的图。（注意上方**加粗**的部分，`psad` 命令命令行针对目标端口的 `countuniqu` 指令解析了 Scan34 数据集，生成生成图表所需的原始数据。）图 14-4 显示了生成的图表，3 月 31 日每小时唯一端口数量出现大幅峰值。

![](img/84e6ec42d170b9df6cf29b40151f3d15_287_0.png)

图 14-4：时间 vs. 唯一端口

```bash
$ grep 60.248.80.102 iptables.data | tail -1
Mar 31 10:43:28 bridge kernel: INBOUND TCP=IN-bro PHYSIN=eth0 OUT-bro
PHYSOUT=eth1 SRC=60.248.80.102 DST=11.11.79.125 LEN=40 TOS=0x00 PREC=0x00
TTL=108 ID=23 PROTO=TCP SPT=51129 DPT=4000 WINDOW=16384 RES=0x00 SYN
URGP=0
$ grep 60.248.80.102 iptables.data | tail -1
```
