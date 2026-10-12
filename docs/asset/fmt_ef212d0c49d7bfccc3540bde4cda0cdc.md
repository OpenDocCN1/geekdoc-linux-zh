
从命令行嗅探器之一开始是一个很好的方法。它们可以在不对对其运行的系统产生大量开销的情况下解锁网络细节，并在接收到数据包时将其抛出。

### 3.3.1 `tcpdump`

`tcpdump` 可能是原始的数据包嗅探器，首次于 1991 年。它由负责 `libpcap` 的同一组人——Van Jacobson、Craig Leres 和 Steven McCann 编写，并可以在几个版本的 Unix 上运行。最基本的形式下，你可以不带任何参数启动它，它将从第一个以太网接口（通常是 `eth0`）发送和接收的数据包头部转到标准输出（`stdout`）。当然，你可以调整嗅探器获取输入的地方、输出格式、输出去向以及嗅探器应该使用的种种过滤器。以下是使用 `tcpdump` 时的一些常用选项：

- `-adeflnNpOqRStvXX` `[-c count]` `[-F file]`
- `[-i interface]` `[-m module]` `[-r file]`
- `[-s snaplen]` `[-T type]` `[-w file]`
- `[-E algorithm:secret]` `[expression]`

#### 控制 `tcpdump` 从何获取输入

- `-i interface`—一个受 `libpcap` 支持的封装格式的网络接口。对于 Linux 来说，几乎几乎你会遇到的任何东西，包括 PPP 和帧中继等链路协议。
- 或者
- `-r file`—读取文件作为输入。`file` 应该是由 `tcpdump -w` 或写入相同格式的程序创建的。指定 `"-"` 读取标准输入（`stdin`）。
- `-c count`—指定从每个数据包中读取的不同字节数。通常，`tcpdump` 只读取字节以确保头部被保存，但你可能想要增加此值，特别是当你打算在链路上使用 `-x` 时。
- `[ expression ]`—这是一个用于限制输出的表达式。这是一个限制数据包范围的表达式。默认情况下，`tcpdump` 匹配所有包。以下是使用该语法的一些示例：

```
tcpdump -i eth0
tcpdump -i eth0 port 110
tcpdump -i eth0 host 192.168.1.1
tcpdump -i eth0 net 192.168.1.0/24
tcpdump -i eth0 and port 80
tcpdump -i eth0 and not port 22
tcpdump -i eth0 host 192.168.1.1 and port 80
```

在未指定接口的情况下，`tcpdump` 打开找到的第一个接口并开始监听发生的情况。为了让我们不必在数百兆字节的数据中寻找两个系统之间的特定交换，我们需要一种方法让 `tcpdump` 限制显示的内容。这是通过表达式实现的。表达式是一个或多个原语，通过 `and`、`or`、`not` 组合。原语可以使用括号进行分组，但当你这样做时，你需要对 `( )` 字符进行转义以防止 shell 解释。所以你可以像 `(p1&&(p2||p3))`。但到底什么是原语？它由一个标识符组成，前面可能有一个限定符。关于这个主题的权威来源是手册以及你在命令行上有效的任何方法。

#### 伯克利过滤器限定符

- `type`—指定标识符的类型。它可以取 `host`、`net` 或 `port` 的值，默认为 `host`。
- `direction`—是 `src` 或 `dst` 之一，在未指定方向时（默认）为 `src` 或 `dst`。

```
tcpdump -n -i eth0 src or dst port 110
tcpdump -n -i eth0 port 110
```

是等价的。记住 `src` 和 `dst` 不适用于 IP 头部。它们也可以适用于其他协议，例如 `ether`（并指示源或目的以太网地址）。

- `protocol`—当单独使用时（不带限定符），是 `fddi`、`tr`、`ip`、`ip6`、`arp`、`rar`、`decnet`、`tcp` 和 `udp` 之一。如果你用协议族对其限定，会有更多的协议规范。例如，你可以指定 `ip proto igrp` 来匹配网关路由协议数据包，或指定 `ip proto` 来捕获 IPSec 封装安全负载数据包。有很多组合，你的需求将引导你找到需要嗅探的协议，或者在你需要时和经理一起喝杯咖啡。如果你不指定协议，那么对于标识符来说任何协议类型都会匹配。因此，如果你只指定了端口，那么 `tcp` 和 `udp` 协议都是隐含的。

### 伯克利数据过滤器（Berkeley Packet-Filter）标识符类型

`host`—指示主机的 IP 地址。与此相关的修符有 `src` 和 `dst`——请记住，默认意味着 `host` 既可以是源也可以是目的。`host` 也可以是一个解析为多个 IP 地址的 DNS 名称，在这种情况下，所有这些地址都会匹配。请注意 `host` 是关键字，而 `host` 是标识符的值。

`ether host`—指示以太网地址。再次，`ether host` 是关键字，而 `host` 是一个格式为 `xx:xx:xx:xx:xx:xx` 的 6 字节以太网（MAC）地址，或者是来自 `/etc/ethers` 的名称。`src` 和 `dst` 修饰符适用于 `host`。

`gateway host`—如果正在检查的数据包是由充当网关的 `host` 转发的或即将由 `host` 转发（仅限下一跳），则产生匹配项。指定的 `host` 必须同时出现在 `/etc/hosts` 和 `/etc/ethers` 文件中。顺便说一下，`/etc/ethers` 的文档并不十分完善。以太网地址和主机名之间只有一个空格。

`tcpdump` 需要这些文件来实现此功能的原因是，使用像 `ether host host and not host` 这样的表达式非常有用，因此它需要网关的 MAC 地址来识别以太网（`host`），以及该网关的主机 IP（`host`）以忽略某些流量。这是因为 `/etc/ethers` 处理起来很棘手，而且在编写时，支持 IPv6 的 `tcpdump` 版本无论如何都不允许你使用 `gateway`（即上面提供的替代表达式）。

`net net/masklen | mask mask`—仅仅是指定 IP 子网的几种不同方法之一。必须使用关键字 `net`，而 `/masklen`（与第 2 节中相同的“1 的个数”格式，用于 `ipfwadm` 和 `ipchains`）和 `mask`（`ifconfig` 使用的点格式）适用于 `dst` 和 `src` 修饰符。

`port`—指示端口位于 IP 数据包的一个（或两个）上。`port` 可以是一个整数端口，也可以是来自 `/etc/services` 的服务名。`dst` 和 `src` 修饰符照常适用，可选在前面加上 `tcp` 和 `udp`。请注意，在以下示例中，关键字 `port` 之前的修饰符顺序是重要的：

```
tcpdump -n i eth0 src port 110      # 正确
tcpdump -n i eth0 src tcp port 110      # 错误
```

`less`—匹配长度（字节）小于或等于 `length` 的数据包。请注意，长度是负载（`payload`）+ 传输头部，你不能使用 `1` 来捕获空数据包（ACK 等）。由于不同协议的长度不同，你可能需要实验一下来找到那个“魔法数字”。我的经验是，在嗅探以太网设备时，在你查找的任何长度基础上加上 `64`，对于 PPP 设备则加 `40`。

### 3.3 IP 监控工具

`greater length`—匹配长度（字节）大于或等于 `length` 的数据包。针对 `less` 的头部相同注释同样适用于此处。

`ip broadcast`—匹配三种不同的 IP 广播。

- 发送到 `255.255.255.255` 的数据包（全 1）
- 发送到 `0.0.0.0` 的数据包（全 0）
- 发送到本地子网广播地址的数据包（适用于正在监听的 `-i` 接口）

`ip multicast`—匹配 IP 多组播数据包。

`ether broadcast`—如果数据包是以太广播则进行匹配——任何以太网目的地址为 `ff:ff:ff:ff:ff:ff` 的数据包（例如 ARP 请求）。关键字 `ether` 是可选的，但为了避免与 `ip broadcast` 混淆，我建议使用它。

`ether multicast`—匹配多组数据包（我个人从未见过这种……）。

`expr relbinop`—最后但同样重要，这种语法是一种进入数据包内部，将 `2` 或 `4` 字节的数据包头部与已知数量进行比较的方法。第一个 `expr` 格式应该是 `protocol[offset:size]`：

- `protocol` 是修饰符类型列表中列出的协议之一
- `offset` 是该协议所隐含的从头部开始计算的字节数
- `size` 是可选的，默认值为 `1`

`relbinop` 是 `>`, `<`, `<=`, `=`, `!` 列表中的相对二运算符，而第二个 `expr` 是 C 语言语法的整数数学表达式（没有变量！）!。

如果这激发了你的兴趣，那就尽管去尝试吧。它可能作为教学辅助，或者用于观察某些竞态条件（可能是怀疑的协议违规）。我认为这是完全的高级用法，所以我留给你自己去研究如何利用它。
