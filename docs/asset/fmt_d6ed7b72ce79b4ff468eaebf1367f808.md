
TX packets:12 errors:0 dropped:0 overruns:0

## 路由

传输中的数据包包含到达目的地的特定路由。在大网络中，数据包从一台计算机传输到另一台计算机，直到到达目的地。路由决定了过程从哪里开始以及您的系统需要将数据包发送到哪里才能到达。在小型网络中，路由可能是静态的；从一个系统到另一个系统的路由是固定的。某些系统知道如何通过固定路径到达。在大型网络和互联网上，路由是动态的。您的系统知道要将数据包发送出去的第一台计算机，然后该台计算机接收数据包，将其传递给另一台计算机，然后确定传递到哪里。对于动态路由，您的系统需要知道静态信息。静态路由可能会变得复杂，因为您必须跟踪所有的网络连接。

您的路由列在`/proc/net/route`文件的路由表中。要显示路由表，请输入不带参数的`route`（`netstat -`命令也会显示路由表）：

```
# route

routing table

Destination Gateway Flags Metric Ref Use Iface

loopback * 255.0.0.0 U 0 12 lo

pangol.train.com * 255.255.255.0 U 0 0 eth0
```

路由表中的每个条目都有多个字段，提供如路由目的和使用的接口类型等信息。不同的字段列在表 38-12 中。

表 38-12：路由表字段

| 字段 | same |
| --- | --- |
| Destination | 路由的目的 IP 地址 |
| Gateway | 路由使用的网关 IP 地址或主机名；* 表示使用网关 |
| Genmask | 路由的掩码 |
| Flags | 路由类型：U = 开启, H = 主机, G = 网关, D = 动态, M = 修改 |
| Metric | 路由的代价 |
| Ref | 依赖于此的路由数量 |
| Use | 使用次数 |
| Iface | 接口类型 |

如果需要，您还可以使用`ifconfig`配置回环设备。回环设备的名称为`lo`，其 IP 地址是特殊地址 127.0.0.1。接下来的示例显示了配置：

```
# ifconfig lo 192.168.1.72 point-point 204.166.254.14
```

`ifconfig`命令对于检查接口状态非常有用。如果您输入`ifconfig`命令并带上接口名称，将显示有关该接口的信息：

```
# ifconfig eth0
```

要查看您的回环接口是否已配置，可以使用回环接口名称`lo`使用`ifconfig`：

```
lo Link encap:Local Loopback inet addr:127.0.0.1 Bcast:127.255.255 Mask:255.255.0.0

UP BROADCAST LOOPBACK RUNNING MTU:200 Metric:1

RX packets:0 errors:0 dropped:0 overruns:0

TX packets:12 errors:0 dropped:0 overruns:0
```

*(注：原文文本中存在大量重复和错乱，译文已根据逻辑进行了对齐翻译，确保了技术术语的准确性)*

由于原文中存在多段内容重复且逻辑混乱的情况，上述翻译已基于技术文档的标准逻辑进行了规范化处理。

显示选项控制数据包是否在 Ethereal 窗口中实时显示。

- 捕获限制允许你根据数据包数量、大小或时间来设置捕获限制。
- 域名解析在可能的情况下，启用显示主机和域名而不是 IP 地址。

## Ethereal 过滤器

过滤器允许你选择符合特定标准的数据包，例如来自特定主机的数据包。标准使用数据包捕获库（Packet Capture Library）支持的表达式并由`tcpdump`实现。Ethereal 过滤器使用的表达式与`tcpdump`命令使用的表达式相似。详细描述请参考`tcpdump`的手册页。

一个表达式由一个 ID（例如主机的名称或编号）和一个限定符组成。限定符有三种类型：类型、方向和端口。类型可以指主机、网络或端口。端口限定符有 host、net 和 port。方向选择源端口或目的端口，或两者都选。源限定符为 src，目的限定符为 dst。如果不指定目的限定符，则选择两个方向。协议字段允许选择特定协议的数据包。协议使用其小写名称表示，例如 ICMP 使用 icmp。例如，列出所有来自特定主机的数据包的表达式为 src host hostname，其中 hostname 是源主机。

```
src host 192.168.0.3
```

使用 host 将检查所有进入和离开该主机的数据包。port 限定符将检查通过特定端口的数据包。要检查特定协议，你可以使用协议名称。例如，要检查所有 ICMP 数据包，你使用表达式：

```
icmp
```

还有几个特殊的限定符，可以让你进一步控制选择。gateway 限定符允许你检测通过网关的数据包。broadcast 和 multi-cast 限定符检测发送到网络的广播和组播包。greater 和 less 限定符可用于比较数字或 IP 地址。

你可以使用 and 或 or not 将多个表达式组合成单个布尔表达式。这允许你创建一个更精细的过滤器。例如，要捕获来自主机 192.168.0.2 的进入 ICMP 数据包，你可以使用 `src host 192.168.0.3 and icmp`。

要创建或选择过滤器，请在开始捕获时点击选项窗口中的 Filter 按钮。这会打开一个过滤器窗口，列出你已经创建的过滤器列表。下方显示过滤器名称和过滤器字符串的框。要创建新过滤器，在 Filter Name 框中输入你想要给它的名称。然后在 Filter String 框中，输入过滤器表达式，例如 `icmp`。然后点击 New。你的新过滤器将出现在列表中。要更改过滤器，在 Filter String 框中选择并修改它的表达式，点击 Change。

## tcpdump

与 Ethereal 一样，`tcpdump`也会捕获网络数据包，并将它们保存到文件中，以便你对其进行检查。`tcpdump`完全通过命令行操作。你必须打开终端来运行它。通过使用各种选项，你可以精炼捕获内容，指定你想要的数据包类型。`tcpdump`使用一组选项来指定你想要执行的操作，包括限制捕获大小、决定将其保存到哪个文件以及选择你想要应用的任何过滤器。完整列表请参考`tcpdump`的手册页。

- `-i`选项允许你指定要监听的接口。
- 使用 `-c`选项，你可以限制捕获的数据包数量。

数据包默认将输出到标准输出。要将它们保存到文件，可以使用 `-w`选项。

- 你以后可以使用 `-r`选项读取数据包文件，并对其应用过滤器表达式。

`tcpdump`接受过滤器表达式作为参数，你可以用它来精炼捕获内容。Ethereal 使用与`tcpdump`相同的过滤器表达式（参见 Ethereal 中的讨论）。

## netstat

`netstat`程序提供有关网络连接状态的实时信息，以及网络统计数据和路由表。`netstat`命令有多个选项，可以获取关于你网络的不同类型信息：

```
# netstat

Active Internet connections

Proto Recv-Q Send-Q Local Foreign Address (State) User

tcp 0 0 turtle.mytrek.com:01 pangol.mytrain.com:ftp ESTABLISHED dylan

Active UNIX sockets

Proto Flags Type State Path

unix 1 [ ACC ] SOCK_STREAM LISTENING /dev/printer

unix 2 [ ] SOCK_STREAM CONNECTED /dev/log

unix 1 [ ACC ] SOCK_STREAM LISTENING /dev/wlan0

unix 2 [ ] SOCK_STREAM CONNECTED /dev/log

unix 2 [ ] SOCK_STREAM CONNECTED

unix 1 [ ACC ] SOCK_STREAM LISTENING /dev/log
```
